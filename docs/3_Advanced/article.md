# 第3回: Mattermostプラグイン開発

Mattermostの統合機能は自分たちでも開発することができます。
前号でも紹介しましたが、Mattermostと外部サービスを連携する統合機能には、下記のような複数の方法があります。

* 内向き/外向きのウェブフック(Incoming/Outgoing Webhook)
* カスタムスラッシュコマンド (Custom Slash Command)
* プラグイン(ベータ版) (Plugin)

今号では、Mattermostプラグインの開発方法について紹介していきます。

## プラグイン機能とは

Mattermost v4.4.0から、ウェブフック、カスタムスラッシュコマンドに続く統合機能としてプラグイン機能が追加されています。プラグイン機能はMattemostに対して柔軟な機能追加を行うことができ、組織内のコミュニケーション基盤としてのMattermostを一層強化できる可能性を秘めています。

プラグイン機能は2018/6/25現在ベータ版のため、今後破壊的な変更がないとは言い切れませんが、ここではMattermost v5.0.0リリース段階でのプラグイン開発方法について紹介していきます。

### Mattermost開発者向けドキュメント

プラグイン開発を行う際は、最近公開されたばかりのMattermost開発者向けドキュメントサイトが参考になります。
https://developers.mattermost.com/

ここではプラグイン開発についてだけでなく、その他の統合機能のウェブフックやスラッシュコマンドなどの開発方法や、Mattermostへのコントリビュート手順などについてもまとめられています。
オープンソースプロジェクトらしくドキュメントサイト自体もPullRequest歓迎なので間違いなどを見つけたら報告してあげましょう。

https://github.com/mattermost/mattermost-developer-documentation

また、下記のリポジトリではMattermostプラグイン開発プロジェクトのGitHubリポジトリがまとめられています。文書よりも動くコードのほうが分かりやすいという方には参考になると思います。

https://github.com/mattermost/mattermost-plugins

### Mattermostプラグインの種類

Mattermostプラグインでは、サーバーサイドとフロントエンド両方の拡張が行えます。
MattermostはサーバーサイドがGo言語、フロントエンドがReact.jsで開発されているため、この二つのプラグインは基本的には別物（協調することも可能）です。
今回は主にサーバーサイドプラグインの開発方法について紹介していきますが、それぞれのプラグインで出来ることについてここで簡単に紹介します。

#### Serverプラグイン

サーバーサイドに処理を追加できるServerプラグインでは下記のようなことができます。

##### スラッシュコマンドの登録
既存のカスタムスラッシュコマンド機能では、スラッシュコマンドを実行した際にMattermostからの送信されるリクエストを処理するためのサーバーアプリケーションを起動しておかなくてはいけませんでしたが、プラグインではMattermostサーバー内でその処理を行うことができます。
これによりスラッシュコマンド用のサーバーを管理する必要がなくなるため、インフラ運用コストを削減することができます。

実際に行える処理としては、プラグイン専用のAPIを通じたメッセージ、チャンネル、ユーザーなどのCRUD操作に加えプラグイン用のKeyValueStoreも使用できるようになっているため、大抵のことは実現できると思います。

##### Post Interception
2018/6/16にリリースされたMattermost v5.0.0からserverプラグインにPost Interceptionの機能が追加されました。

この機能はMattermostに投稿されたメッセージがデータベースに保存される処理の前後に処理を追加できる機能です。Post Interceptionを使うことで、不適切な発言のフィルタリングや特定文字列の置き換えを自動で行うことができます。

MattermostのCTOが特定文字列をURLリンクに変換するプラグインを公開しているので、実際の実装についてはこちらが参考になるかと思います。
https://github.com/mattermost/mattermost-plugin-autolink

#### webappプラグイン

フロントエンド側の機能を拡張できるwebappプラグインでは下記のことが実現できます。

##### React Componentの上書き
Mattermostの画面を構成しているReactComponentの一部を上書きすることができます。
ただし、あるReactComponentを上書きする場合、そのComponentから呼ばれる子コンポーネントとの関係なども考えながら開発する必要があるため、コアとなるコンポーネントを上書きしようとすると多大な開発コストがかかるようになってしまう点に注意が必要です。

今の所、ユーザーのアイコンをクリックすることで出現するポップオーバーに関するコンポーネントの入れ替えぐらいしか例がないような気がします。

また、現時点では複数のプラグインで同一コンポーネントを上書きするようなことはできず、この点については議論・改良が進められています。

Mattermostコアチームのメンバーが開発しているサンプルアプリは下記になります。
https://github.com/jwilander/hovercardexample

##### チャンネルヘッダーボタンの追加
Mattermostチャンネルのヘッダー部分にボタンを追加することができる拡張ポイントです。
Mattermostではビデオ会議用の[Zoom](https://zoom.us/)というサービス用のボタンを追加するプラグインがデフォルトでインストールされています。

![Zoom Plugin]()

https://github.com/mattermost/mattermost-plugin-zoom

### Mattermostプラグインのファイル形式

Mattermostプラグインの実体は`.tar.gz`形式の圧縮ファイルとなります。
サーバープラグインでは、この圧縮ファイルの中身として最低限必要なファイルは**マニフェストファイル**と**実行バイナリ**の二つだけです。

#### マニフェストファイル
JSON形式かYAML形式で、プラグインのID、名前、バージョンや実行バイナリのパスなどのメタ情報を記述するファイルです。個人的にはJSONよりコメントが書けるYAMLの方が好きです。

マニフェストファイルのリファレンスには下記になります。
https://developers.mattermost.com/extend/plugins/server/hello-world/

#### 実行バイナリ
Goプログラムをビルドして生成できるバイナリファイルです。
Mattermostサーバーが動作しているサーバーOS(Windows、Linux、Macなど)に合わせてGoプログラムをビルド必要があります。

### プラグインのインストール

上述の**マニフェストファイル**と**実行バイナリ**を`tar.gz`形式で圧縮した、下記のようなファイルがMattermostプラグインとなります。

```
mattermost-plugin.tar.gz
- plugin.yaml
- plugin-binary
```

このプラグインファイルをMattermostの**システムコンソール** > **プラグイン(ベータ版)** > **管理** > **ファイルを選択する** > **アップロード**からアップロードすることでインストールが完了します。
次に登録されたプラグインの下にある**有効にする**ボタンを押すことで、プラグインが使えるようになります。

![Plugin Upload]()

このあたりについて、詳しくはHello Worldプラグインのチュートリアルドキュメントを参照してください。
https://developers.mattermost.com/extend/plugins/server/hello-world/

## Mattermostプラグイン開発

ここからは実際のMattermostプラグインの開発方法について紹介します。

### ディレクトリ作成

基本的に作業用のディレクトリは好きな場所に作ればよいのですが、Go言語公式の依存ライブラリ管理ツールの`dep`を使用する場合、環境変数`GOPATH`配下のディレクトリで作業する必要があります。

```
go version
echo $GOPATH
mkdir -p $GOPATH/src/github.com/kaakaa/mm-compliance-plugin
```

Go言語の慣習として、プロジェクトのディレクトリは`$GOPATH/src/${HOSTNAME}/${User}/${REPO}`というソースコードリポジトリと同じディレクトリ階層にすることになっています。依存ライブラリをダウンロードする`go-get`コマンドでも、このディレクトリ構成で依存プロジェクトがダウンロードされます。

`GOPATH`などのGo言語の開発環境に関する説明については、多くの記事が公開されていますのでググってください。

### マニフェストファイル作成

作業用のディレクトリが作成できたら、その直下にプラグインの定義ファイル`plugin.yaml`を作成します。

```yaml
id: org.kaakaa.compliance.report
name: mm-compliance-plugin
version: '0.0.1'
backend:
  executable: compliance-plugin
```

プラグインのIDは、Mattermostサーバー内でユニーク、かつ3~190文字、`^[a-zA-Z0-9-_\.]+$`に従う必要があります。
https://developers.mattermost.com/extend/plugins/manifest-reference/#id

`plugin.yaml`の中で`backend.executable: compliance-plugin`を指定しているので、`compliance-plugin`という実行バイナリを作れば良いということになります。

### Goプログラム開発

次に、実行バイナリ`compliance-plugin`を作成するために、下記のようなGoプログラムを`server/plugin.go`という名前で作成します。

```golang
package main

import (
        "github.com/mattermost/mattermost-server/model"
        "github.com/mattermost/mattermost-server/plugin"
        "github.com/mattermost/mattermost-server/plugin/rpcplugin"
)

type CompliancePlugin struct {
        api plugin.API
}

func (p *CompliancePlugin)OnActivate(api plugin.API) error {
        p.api = api
        if err := p.api.RegisterCommand(&model.Command{
                Trigger:                "compliance",
                AutoComplete:           true,
                AutoCompleteDesc:       "We must keep order",
        }); err != nil {
                return err
        }
        return nil
}

func (p *CompliancePlugin)ExecuteCommand(args *model.CommandArgs) (*model.CommandResponse, *model.AppError) {
        return &model.CommandResponse{
                ResponseType:   model.COMMAND_RESPONSE_TYPE_IN_CHANNEL,
                Username:       "Justice",
                Attachments:    []*model.SlackAttachment{{
                        AuthorName:     "Compliance Line",
                        AuthorLink:     "http://example.com/compliance/report",
                        Text:           "Please report",
                }},
        }, nil
}

func main() {
        rpcplugin.Main(&CompliancePlugin{})
}
```

Go言語では`main`パッケージの`main`メソッドが実行バイナリのエンドポイントとなります。
ここでは、`CompliancePlugin`型のインスタンスをプラグインとして登録しており、Mattermost上でプラグインが有効化されたときに`CompliancePlugin`の`OnActivate`メソッドが呼ばれて処理が行われるというコードになっています。
`OnActivate`メソッド内ではプラグイン用のAPIインスタンスを使って`/compliance`というスラッシュコマンドを登録しています。
ここで登録したスラッシュコマンドが実行されると`CompliancePlugin`の`ExecuteCommand`メソッドの処理が実行され、コンプライアンスラインへのリンクがMattermostに投稿されるという流れになります。

以上のように、これはプラグイン内でスラッシュコマンドの登録と実行を行うコードとなります。
ここではGoプログラムについての詳しい解説は行うつもりはないため、コードの説明はこれまでとなります。

### ビルド: 実行バイナリの作成

上記のコードをビルドするには`go-build`コマンドを使いますが、その前に上記のプラグインコードでは`github.com/mattermost/mattermost-server`パッケージを使用しているため、この依存ライブラリのダウンロードが必要です。
`ディレクトリ作成`で紹介した通り、`GOPATH/src`配下にディレクトリを作成している場合は下記のように`dep`のインストールとセットアップを行ってください。

```
go get -u -v github.com/golang/dep/cmd/dep
cd $GOPATH/src/${ルートディレクトリ}
dep init
```

`dep`はGoプログラムを解析して必要なライブラリを自動で認識し、ダウンロードしてくれるため非常に便利なのですが、今回依存している`github.com/mattermost/mattermost-server`のサイズが巨大なため処理が完了するまでにとても時間がかかります。
気長に待ちましょう。

もし、`dep`を使用しない場合は下記のコマンドでも依存ライブラリをダウンロードして利用できるかと思います（未確認）。

```
go get -u github.com/mattermost/mattermost-server
```

依存ライブラリをダウンロードできたら、次に実行バイナリ`compliance-plugin`を生成します。
今回はLinuxサーバー上のMattermostにプラグインをインストールする予定のため、下記のようなコマンドとなります。
```
GOOS=linux GOARCH=amd64 go build -o compliance-plugin server/main.go
```

その他のサーバーOS向けにバイナリをビルドする場合は`GOOS`、`GOARCH`の値を変える必要があります。
これら２つの値に使用できる値は下記のドキュメントを参考にしてください。
https://golang.org/doc/install/source#environment

### tar.gz形式への変換

実行バイナリ `compliance-plugin` が作成できたら、`tar`コマンドを使ってマニフェストファイルと共に.tar.gz形式に圧縮します。

```
tar -czvf compliance-plugin.tar.gz compliance-plugin plugin.yaml
```

これでMattermostプラグインが完成しました。

先に述べたの`プラグインのインストール`と同じようにプラグインをアップロードして有効化すると、`/compliance`コマンドが利用可能になっているはずです。
もし、有効化時にエラーとなった場合はシステムコンソールのログにエラーメッセージが出力されているはずなので確認して対処してください。

![Uploaded Plugin]()

### コマンド実行

Mattermostチャンネルに戻り、登録されたコマンドを実行するとコンプライアンスラインへのリンクが投稿されます。

![Compliance Command]()

## おわりに

以上がMattermost severプラグインの開発方法になります。
Mattermostプラグインでは、今回紹介したスラッシュコマンド登録機能の他にも、プラグイン専用のHTTPエンドポイントを作成したり、システムコンソール画面への設定画面の追加などができます。

プラグイン機能はベータ版のため度々変更が入ったりしますが、非常に簡単に機能追加が行えるので是非チャレンジしてみてください。
また、その際に気づいた点をMattermostコアチームに報告してあげると非常に喜ばれるので、下記のコアチームのチャットに参加しMattermost自体の開発にも協力いただければと思います。

https://pre-release.mattermost.com/core/