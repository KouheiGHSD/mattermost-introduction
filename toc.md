
- [第一回: Mattermostとは](#%E7%AC%AC%E4%B8%80%E5%9B%9E-mattermost%E3%81%A8%E3%81%AF)
  * [まえがき](#%E3%81%BE%E3%81%88%E3%81%8C%E3%81%8D)
  * [Mattermostとは](#mattermost%E3%81%A8%E3%81%AF)
  * [チャットツール戦国時代](#%E3%83%81%E3%83%A3%E3%83%83%E3%83%88%E3%83%84%E3%83%BC%E3%83%AB%E6%88%A6%E5%9B%BD%E6%99%82%E4%BB%A3)
    + [(コラム) Mattermost v5.0](#%E3%82%B3%E3%83%A9%E3%83%A0-mattermost-v50)
  * [Mattermostを動かしてみよう](#mattermost%E3%82%92%E5%8B%95%E3%81%8B%E3%81%97%E3%81%A6%E3%81%BF%E3%82%88%E3%81%86)
    + [Mattermostの起動](#mattermost%E3%81%AE%E8%B5%B7%E5%8B%95)
    + [初期設定](#%E5%88%9D%E6%9C%9F%E8%A8%AD%E5%AE%9A)
      - [画面の日本語化](#%E7%94%BB%E9%9D%A2%E3%81%AE%E6%97%A5%E6%9C%AC%E8%AA%9E%E5%8C%96)
    + [投稿](#%E6%8A%95%E7%A8%BF)
      - [ファイル添付](#%E3%83%95%E3%82%A1%E3%82%A4%E3%83%AB%E6%B7%BB%E4%BB%98)
      - [メンション](#%E3%83%A1%E3%83%B3%E3%82%B7%E3%83%A7%E3%83%B3)
      - [ハッシュタグ](#%E3%83%8F%E3%83%83%E3%82%B7%E3%83%A5%E3%82%BF%E3%82%B0)
      - [フラグ](#%E3%83%95%E3%83%A9%E3%82%B0)
      - [ピン留め](#%E3%83%94%E3%83%B3%E7%95%99%E3%82%81)
      - [絵文字リアクション](#%E7%B5%B5%E6%96%87%E5%AD%97%E3%83%AA%E3%82%A2%E3%82%AF%E3%82%B7%E3%83%A7%E3%83%B3)
      - [(コラム)メールにはない絵文字リアクション機能](#%E3%82%B3%E3%83%A9%E3%83%A0%E3%83%A1%E3%83%BC%E3%83%AB%E3%81%AB%E3%81%AF%E3%81%AA%E3%81%84%E7%B5%B5%E6%96%87%E5%AD%97%E3%83%AA%E3%82%A2%E3%82%AF%E3%82%B7%E3%83%A7%E3%83%B3%E6%A9%9F%E8%83%BD)
    + [チャンネル](#%E3%83%81%E3%83%A3%E3%83%B3%E3%83%8D%E3%83%AB)
      - [チャンネルの作成](#%E3%83%81%E3%83%A3%E3%83%B3%E3%83%8D%E3%83%AB%E3%81%AE%E4%BD%9C%E6%88%90)
    + [チーム](#%E3%83%81%E3%83%BC%E3%83%A0)
      - [メンバーを招待する](#%E3%83%A1%E3%83%B3%E3%83%90%E3%83%BC%E3%82%92%E6%8B%9B%E5%BE%85%E3%81%99%E3%82%8B)
      - [(コラム) チーム・チャンネルの分け方について](#%E3%82%B3%E3%83%A9%E3%83%A0-%E3%83%81%E3%83%BC%E3%83%A0%E3%83%BB%E3%83%81%E3%83%A3%E3%83%B3%E3%83%8D%E3%83%AB%E3%81%AE%E5%88%86%E3%81%91%E6%96%B9%E3%81%AB%E3%81%A4%E3%81%84%E3%81%A6)
        * [チームの分け方について](#%E3%83%81%E3%83%BC%E3%83%A0%E3%81%AE%E5%88%86%E3%81%91%E6%96%B9%E3%81%AB%E3%81%A4%E3%81%84%E3%81%A6)
        * [チャンネルの分け方](#%E3%83%81%E3%83%A3%E3%83%B3%E3%83%8D%E3%83%AB%E3%81%AE%E5%88%86%E3%81%91%E6%96%B9)
  * [弊社でのMattermost活用状況](#%E5%BC%8A%E7%A4%BE%E3%81%A7%E3%81%AEmattermost%E6%B4%BB%E7%94%A8%E7%8A%B6%E6%B3%81)
  * [おわりに](#%E3%81%8A%E3%82%8F%E3%82%8A%E3%81%AB)

- [第2回: Mattermost使いこなし術](#%E7%AC%AC2%E5%9B%9E-mattermost%E4%BD%BF%E3%81%84%E3%81%93%E3%81%AA%E3%81%97%E8%A1%93)
  * [Mattermostの高度な機能](#mattermost%E3%81%AE%E9%AB%98%E5%BA%A6%E3%81%AA%E6%A9%9F%E8%83%BD)
    + [チャンネルのグループ化](#%E3%83%81%E3%83%A3%E3%83%B3%E3%83%8D%E3%83%AB%E3%81%AE%E3%82%B0%E3%83%AB%E3%83%BC%E3%83%97%E5%8C%96)
      - [お気に入りチャンネル](#%E3%81%8A%E6%B0%97%E3%81%AB%E5%85%A5%E3%82%8A%E3%83%81%E3%83%A3%E3%83%B3%E3%83%8D%E3%83%AB)
      - [未読チャンネル](#%E6%9C%AA%E8%AA%AD%E3%83%81%E3%83%A3%E3%83%B3%E3%83%8D%E3%83%AB)
    + [通知の管理](#%E9%80%9A%E7%9F%A5%E3%81%AE%E7%AE%A1%E7%90%86)
      - [取り込み中](#%E5%8F%96%E3%82%8A%E8%BE%BC%E3%81%BF%E4%B8%AD)
      - [チャンネルのミュート](#%E3%83%81%E3%83%A3%E3%83%B3%E3%83%8D%E3%83%AB%E3%81%AE%E3%83%9F%E3%83%A5%E3%83%BC%E3%83%88)
    + [キーボードショートカット](#%E3%82%AD%E3%83%BC%E3%83%9C%E3%83%BC%E3%83%89%E3%82%B7%E3%83%A7%E3%83%BC%E3%83%88%E3%82%AB%E3%83%83%E3%83%88)
    + [カスタム絵文字](#%E3%82%AB%E3%82%B9%E3%82%BF%E3%83%A0%E7%B5%B5%E6%96%87%E5%AD%97)
    + [リンクプレビュー(Proxy設定)](#%E3%83%AA%E3%83%B3%E3%82%AF%E3%83%97%E3%83%AC%E3%83%93%E3%83%A5%E3%83%BCproxy%E8%A8%AD%E5%AE%9A)
    + [テーマカラー](#%E3%83%86%E3%83%BC%E3%83%9E%E3%82%AB%E3%83%A9%E3%83%BC)
    + [検索](#%E6%A4%9C%E7%B4%A2)
      - [日本語検索設定](#%E6%97%A5%E6%9C%AC%E8%AA%9E%E6%A4%9C%E7%B4%A2%E8%A8%AD%E5%AE%9A)
    + [GitLab連携](#gitlab%E9%80%A3%E6%90%BA)
  * [Enterprise版の機能?](#enterprise%E7%89%88%E3%81%AE%E6%A9%9F%E8%83%BD)
  * [Mattermostnの統合機能](#mattermostn%E3%81%AE%E7%B5%B1%E5%90%88%E6%A9%9F%E8%83%BD)
    + [統合機能の種類](#%E7%B5%B1%E5%90%88%E6%A9%9F%E8%83%BD%E3%81%AE%E7%A8%AE%E9%A1%9E)
    + [Slackとの互換性](#slack%E3%81%A8%E3%81%AE%E4%BA%92%E6%8F%9B%E6%80%A7)

- [第3回: Mattermostプラグイン開発](#%E7%AC%AC3%E5%9B%9E-mattermost%E3%83%97%E3%83%A9%E3%82%B0%E3%82%A4%E3%83%B3%E9%96%8B%E7%99%BA)
  * [プラグイン機能とは](#%E3%83%97%E3%83%A9%E3%82%B0%E3%82%A4%E3%83%B3%E6%A9%9F%E8%83%BD%E3%81%A8%E3%81%AF)
    + [Mattermost開発者向けドキュメント](#mattermost%E9%96%8B%E7%99%BA%E8%80%85%E5%90%91%E3%81%91%E3%83%89%E3%82%AD%E3%83%A5%E3%83%A1%E3%83%B3%E3%83%88)
    + [Mattermostプラグインの種類](#mattermost%E3%83%97%E3%83%A9%E3%82%B0%E3%82%A4%E3%83%B3%E3%81%AE%E7%A8%AE%E9%A1%9E)
      - [Serverプラグイン](#server%E3%83%97%E3%83%A9%E3%82%B0%E3%82%A4%E3%83%B3)
        * [スラッシュコマンドの登録](#%E3%82%B9%E3%83%A9%E3%83%83%E3%82%B7%E3%83%A5%E3%82%B3%E3%83%9E%E3%83%B3%E3%83%89%E3%81%AE%E7%99%BB%E9%8C%B2)
        * [Post Interception](#post-interception)
      - [webappプラグイン](#webapp%E3%83%97%E3%83%A9%E3%82%B0%E3%82%A4%E3%83%B3)
        * [React Componentの上書き](#react-component%E3%81%AE%E4%B8%8A%E6%9B%B8%E3%81%8D)
        * [チャンネルヘッダーボタンの追加](#%E3%83%81%E3%83%A3%E3%83%B3%E3%83%8D%E3%83%AB%E3%83%98%E3%83%83%E3%83%80%E3%83%BC%E3%83%9C%E3%82%BF%E3%83%B3%E3%81%AE%E8%BF%BD%E5%8A%A0)
    + [Mattermostプラグインのファイル形式](#mattermost%E3%83%97%E3%83%A9%E3%82%B0%E3%82%A4%E3%83%B3%E3%81%AE%E3%83%95%E3%82%A1%E3%82%A4%E3%83%AB%E5%BD%A2%E5%BC%8F)
      - [マニフェストファイル](#%E3%83%9E%E3%83%8B%E3%83%95%E3%82%A7%E3%82%B9%E3%83%88%E3%83%95%E3%82%A1%E3%82%A4%E3%83%AB)
      - [実行バイナリ](#%E5%AE%9F%E8%A1%8C%E3%83%90%E3%82%A4%E3%83%8A%E3%83%AA)
    + [プラグインのインストール](#%E3%83%97%E3%83%A9%E3%82%B0%E3%82%A4%E3%83%B3%E3%81%AE%E3%82%A4%E3%83%B3%E3%82%B9%E3%83%88%E3%83%BC%E3%83%AB)
  * [Mattermostプラグイン開発](#mattermost%E3%83%97%E3%83%A9%E3%82%B0%E3%82%A4%E3%83%B3%E9%96%8B%E7%99%BA)
    + [ディレクトリ作成](#%E3%83%87%E3%82%A3%E3%83%AC%E3%82%AF%E3%83%88%E3%83%AA%E4%BD%9C%E6%88%90)
    + [マニフェストファイル作成](#%E3%83%9E%E3%83%8B%E3%83%95%E3%82%A7%E3%82%B9%E3%83%88%E3%83%95%E3%82%A1%E3%82%A4%E3%83%AB%E4%BD%9C%E6%88%90)
    + [Goプログラム開発](#go%E3%83%97%E3%83%AD%E3%82%B0%E3%83%A9%E3%83%A0%E9%96%8B%E7%99%BA)
    + [ビルド: 実行バイナリの作成](#%E3%83%93%E3%83%AB%E3%83%89-%E5%AE%9F%E8%A1%8C%E3%83%90%E3%82%A4%E3%83%8A%E3%83%AA%E3%81%AE%E4%BD%9C%E6%88%90)
    + [tar.gz形式への変換](#targz%E5%BD%A2%E5%BC%8F%E3%81%B8%E3%81%AE%E5%A4%89%E6%8F%9B)
    + [コマンド実行](#%E3%82%B3%E3%83%9E%E3%83%B3%E3%83%89%E5%AE%9F%E8%A1%8C)
  * [おわりに](#%E3%81%8A%E3%82%8F%E3%82%8A%E3%81%AB)

