---
title: "ブログ作りました"
date: 2021-12-18T21:23:24+09:00
draft: false
tags: ["Hugo","ブログ"]
categories: ["ブログ"]
weight: 1
series: ["Hugoでブログ作成"]
series_weight: 1
description: "MYブログを作りました。Hugoの説明も載せています。"
featuredImage: "https://d33wubrfki0l68.cloudfront.net/c38c7334cc3f23585738e40334284fddcaf03d5e/2e17c/images/hugo-logo-wide.svg"
lightgallery: true
seriesNavigation: true
toc:
  enable: ture
  auto: true
code:
  copy: true
linkToMarkdown: 
summary: "このブログで試用されているHugoの説明と導入方法"

---
# MYブログを作ってみた！
---
## Hugoでのブログ作成
このブログではHugoという静的サイトジェネレータを試用しています。
## 1 Hugoを導入
### インストール
各プラットフォームごとに提供されているので[リリース情報のページ](https://github.com/gohugoio/hugo/releases)の下の方にあるAssetsから適宜選択してください。(ちなみに僕はwindows-64bitを選択しました。)

そして、Cドライブ直下に`"C:\Hugo"`を作成し、さらにHugoの中に`"C:\Hugo\bin"`を作成します。

そこへ、先ほどダウンロードしたzipファイルを展開し、その中にあるhugo.exeを`"C:\Hugo\bin"`へ追加します。
### 環境変数(PATH)へ追加
windows10の場合
windowsマークを右クリック⇒システム⇒システムの詳細設定⇒環境変数に進む。
ログインしている現状のユーザーにパスを通す場合、「ユーザーの環境変数」でPathをダブルクリック⇒新規まで進み、C:\Hugo\binを入力⇒OKで各ウィンドウを閉じる。
### サイトのプレビュー
``` sh
hugo server
```
このコマンドを実行し,`http://localhost:1313`にブラウザでアクセス
