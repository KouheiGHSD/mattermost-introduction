# 第2回: Mattermost使いこなし術

## Mattermostの高度な機能

### カスタム絵文字
### GitLab連携
### リンクプレビュー(Proxy設定)

### チャンネルのグループ化
チャンネルが増えてくると、１画面に収まりきらなくなり、投稿が行われたチャンネルを作業が必要になってきます。
その労力を減らすために、特定のチャンネルを目立つようにグループ化する機能があります。
チャンネル名の横にある星マークをクリックすることで、そのチャンネルを**お気に入りチャンネル**として、サイドバーのトップにまとめて表示することができます。
また、**アカウント管理** > **サイドバー** > **未読チャンネルのグループ化** をオンにすることで、未読の投稿があるチャンネルがサイドバーのトップに表示されるようになります。ただ、この未読チャンネルのグループ化機能は、まだ実験的な機能のため、Mattermostの設定ファイルを手で編集する必要があるので、もしこの機能がどうしても必要な場合はシステム管理者に問い合わせてみてください。

### 通知の管理
Mattermostをブラウザなどで開いていると、メッセージの投稿が行われるごとにデスクトップに通知されます。
これが煩わしい場合は、アカウント設定の**通知**タブから通知設定のオン/オフなどを設定することができます。
また、メッセージ入力欄で`/dnd`という投稿を行うことで、一時的に通知を受け取らないよう設定することができます。この設定は再度`/dnd`というメッセージを投稿することで解除できます。
チャンネル単位で通知のオン/オフを設定したい場合は、通知をオフにしたいチャンネルで`/mute`というメッセージを投稿すると、そのチャンネルからの通知をミュートすることができます。
ミュートを解除したい場合は、再度`/mute`と投稿すると通知をオンにすることができます。


## Mattermostnの統合機能

さて、ここからはMattermostの統合機能について説明していきます。

今では業務を進めるために必要なメールや課題管理システムなどは、ほとんどがブラウザで利用可能なWebサービスを利用しているはずです。
これらのWebサービスとMattermostを連携することで、今効率的に業務を進めることができるようになります。
例えば、課題管理システムに新しいバグが登録された時に、それをリアルタイムにMattermostへ書き込まれるような統合機能を使っていれば、その書き込まれたコメントに即座に気づき、チャット上で対応を議論することができます。
また、チャットでの会話から新機能のアイデアが生まれそうな場合に、チャットから課題管理システムへ登録できるようにすることで、チーム内のコミュニケーションからシームレスに課題の登録ができるようになります。

現在ではOSSも含め便利なWebサービスが数多く存在するため、それらの情報が集約される中心としてMattermostを置くことで、それらのサービスで発生するイベントの全てに対応することができるようになります。

### 統合機能の種類

Mattermostの統合機能には、下記のような種類があります。

* 内向き/外向きのウェブフック(Incoming/Outgoing Webhook)
* カスタムスラッシュコマンド (Custom Slash Command)
* プラグイン(ベータ版) (Plugin)

現在、Mattermostと連携する機能として100を超えるOSSが開発され、だれでも使えるよう公開されています。
Mattermost公式チーム、およびコミュニティによって開発されている統合機能は以下のページにまとめられています。

[Apps and Integrations – Mattermost](https://about.mattermost.com/community-applications/)

ここではいくつかの統合機能の使い方をみてみましょう。

[jenkinsci/mattermost\-plugin: Jenkins plugin for Mattermost](https://github.com/jenkinsci/mattermost-plugin)
[makmu/outlook\-matters: Add\-In to forward e\-mails from MS Outlook to Mattermost](https://github.com/makmu/outlook-matters)
[matterhorn\-chat/matterhorn: A terminal client for the Mattermost chat system](https://github.com/matterhorn-chat/matterhorn)

現在でも多くの統合機能が開発されていますが、まだ公開されていない統合機能を使用したくなった場合、自分で機能を開発することもできます。
自作統合機能の開発方法については、次号で説明いたします。

### Slackとの互換性

Mattermostは`Open source, private cloud
Slack-alternative`を掲げている通り、統合機能についてもSlackとの互換性を重視しています。
そのため、Slack向けに開発された統合機能をそのまま利用することもできます。

例えば、    などは通知先をMattermostサーバーにするだけで同等の機能を利用できるようになります。

欲しい機能がMattermost向けに開発されていない場合、Slack向けに開発された統合機能がないかを探して見るのも良いかもしれません。

ただ、やはり完全な互換性を保つのは難しいらしく、互換性の無い部分については公式ページの各統合機能の解説ページにて`Slack Compatibility`としてまとめられています。

[Incoming Webhooks — Mattermost 4\.10 documentation](https://docs.mattermost.com/developer/webhooks-incoming.html#slack-compatibility)

