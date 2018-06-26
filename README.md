# Mattermost紹介記事を書きたい

## 目的
社内でもMatterostの利用例が増えてきたため、基本的な機能に関するリファレンスを提供することで導入しやすくなるようなベースを作りたい。

## 想定読者
* Mattermostの各機能を触ったことがない人
  * チャットを触ったことがない人
  * Mattermostを使ったことがない人(Slack利用者とか)
  * Mattermostの連携機能を使ったことがない人(投稿はしている人)

## ゴール
上記の想定読者に、下記のような感情をいだかせること
* チャットを触ってみたい
* Mattermostの様々な機能を試してみたい
* Mattermostと連携する機能を作ってみたい

# Mattermost特集 目次

## 1. Mattermostことはじめ

### 1.1 [ChatOpsとは](./docs/1_Introduction/1.1_WhatsMattermost.md)
### 1.2 Mattermostの位置づけ(Slackなどと比較して) (1P)
### ~~1.2 実際のユースケース(2P)~~

### 1.3. [Mattermostを触ってみよう](./docs/1_Introduction/1.x_GettingStarted.md)
* docker online previewでおためし
* 起動からログイン、投稿、チャンネル作成など基本的な操作
* その他のインストール方法は「ドキュメント見てね」程度に紹介

### ~~1.4 デスクトップアプリ/モバイルアプリ~~

## 2. Mattermostの運用

### 2.1 [本格的なセットアップ](./docs/2_Usage/2.x_Setup.md)
* 想定マシンスペック
* Ubuntu?へのインストール方法
* バックアップについて

### 2.2. [Basic Usage - 使い方](./docs/2_Usage/2.x_posts.md)

* Markdown, mathjax
* メンション
* [アカウント設定など](./docs/2_Usage/2.x_settings.md)

## 3. 連携機能

### 3.0 [連携機能概要](./docs/3_Advanced/3.0_integrations.md)
### 3.1 [outgoing / incoming webhook](./docs/3_Advanced/3.1_webhook.md)

### 3.2 [custom slash command](./docs/3_Advanced/3.2_slash_command.md)
* Interactive Message Button (1P)
### 3.3 [plugin(beta](./docs/3_Advanced/3.3_plugin.md)

## 4. contributing(ページが余ったら)

# 参考資料
* https://docs.mattermost.com/guides/user.html
  * 「使い方」の章についてはここから入れられるだけ入れたい（調整ポイント）
* [Software Design 2016年1月号｜技術評論社](http://gihyo.jp/magazine/SD/archive/2016/201601)
* [技術評論社ソフトウェアデザイン編集長による「技術書原稿執筆の心得」 \- Togetter](https://togetter.com/li/835478)

* Software Design
  * 1P -> 1680文字 = 21(文字) * 40(行) * 2(段組み)
