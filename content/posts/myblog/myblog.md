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
featuredImage: ""
lightgallery: true
summary: "このブログで試用されているHugoの説明と導入方法"

---
# MYブログを作ってみた！
---
皆さんブログを書いていますか？

僕は[wordpress](https://wordpress.com/ja/)や[はてなブログ](https://hatenablog.com/guide)、[zenn](https://zenn.dev/about)(zennってブログなのかな???)

で迷っていましたが、色々調べた結果[Hugo](https://gohugo.io/)にたどり着きました:clap:

<br />

## なぜHugoにしたのか？
このブログでは[Hugo](https://gohugo.io/)という静的サイトジェネレータを試用しています。

Hugoは静的なので表示速度が速く、さらにビルド時に最適化されるのでwordpressなどと比べると物凄く早いです。

>こちらが参考になると思います⇒
[Hugoとは？](http://www.study-hugo.com/basic/whats-hugo/)

<br />

## Githubへ公開
このブログは[Github](https://github.com/kzt-wt/My-blog)にパブリックリポジトリで公開しています。
理由は多々ありますが...
<br />
<br />
## Netlifyを使う
[Netlify](https://www.netlify.com/)は静的サイトをホスティングできるWebサービスです。ブログとして使う分にはほぼほぼ無料なのでありがたく使わせていただきました。
<br />
<br />
## Github Actionsも併用する
Netlify単体でも基本的には無料で収まるのですが、念には念を入れてGithub Actionsでビルドすることにしました。

Github Actionsはパブリックリポジトリでは無料で使えるはずです。

![github actions](https://user-images.githubusercontent.com/87252429/147384859-22cc80f2-ca23-4638-8abb-7537cf868419.png)

これ(↓)が最終的なGithub Actionsのコードです。Pushした際に実行されるようにしました。
``` yml
name: build

on:
  push:
    branches: [main]

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v2
      #Hugoをセットアップ
      - name: Setup Hugo
        uses: peaceiris/actions-hugo@v2
        with:
          hugo-version: "latest"
          #extended: true

      - name: Build Project
        run: hugo --gc --minify #ここでビルド
      #node.jsをセットアップ
      - name: Setup npm
        uses: actions/setup-node@v2
        with:
          node-version: 16.x
      #atomic-algoliaをセットアップ
      - name: atomic-algolia install
        run: npm install atomic-algolia
      #検索エンジンににalgoliaを使っているので何か更新があったらここでalgoliaに送信する。
      - name: Algolia
        run: npm run algolia
        env:
          ALGOLIA_APP_ID: ${{ secrets.ALGOLIA_APP_ID }}
          ALGOLIA_ADMIN_KEY: ${{ secrets.ALGOLIA_ADMIN_KEY }}
          ALGOLIA_INDEX_NAME: ${{ secrets.ALGOLIA_INDEX_NAME }}
          ALGOLIA_INDEX_FILE: ${{ secrets.ALGOLIA_INDEX_FILE }}

      # Netlifyにデプロイする。
      - run: npx netlify-cli deploy --dir=public --prod
        env:
          NETLIFY_AUTH_TOKEN: ${{ secrets.NETLIFY_AUTH_TOKEN }}
          NETLIFY_SITE_ID: ${{ secrets.NETLIFY_SITE_ID }}

```
<br />

## 最後に
Algoliaの設定とGithub Actionsの設定にだいぶてこずりましたが、無事記事が書ける状態まで持っていけてよかったです。このブログはGitHubで公開しているので遠慮なくissuesやプルリクエストを送ってください。