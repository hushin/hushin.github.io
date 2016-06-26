---
layout: post
title: Jekyll と GitHub Pages で blog を書く
date:   2016-06-26 15:05:53 +0900
---

## ブログモチベーション

- markdown で書きたい
- git で管理したい
- GitHub Pages でホスティングしたい（無料なので）
- 既存のCMS飽きた

## Jekyll にした理由

静的サイトジェネレータは[いろいろあるようです。](https://staticsitegenerators.net/)
最初node.js製のHexoを試してみたのですが、下記理由によりやめました。

* deploy用のリポジトリとは別にソース用のリポジトリ（or ブランチ）が必要
* テーマを変えたらビルド時に失敗する

GitHub PagesだとJekyllで作ればpushしたらgithub側で自動的にhtmlを生成してくれるので便利そうでした。

Jekyll、調べると記事が多いとビルド時間がかかるそうですが、
いまのところ様子見で使ってみます。

最近だと [Big Sky :: GitHub Pages が Jekyll 3.0 になり、ますますブログが書きやすくなった。](http://mattn.kaoriya.net/software/20160215110235.htm) というポジティブな記事があったので追い風に。

## 導入備忘録

下記の記事を参考に導入してみました。

- [Using Jekyll as a static site generator with GitHub Pages - User Documentation](https://help.github.com/articles/using-jekyll-as-a-static-site-generator-with-github-pages/)
- [Jekyllバージョン3.1の導入とGitHub Pagesを試す](http://www.tbn.co.jp/posts/technology/2016/02/12/jekyll-3.html)

最終的な成果物は [hushin/hushin.github.io](https://github.com/hushin/hushin.github.io) に上げています

### インストール

あらかじめ rbenvが使えるように zshrc等で `eval "$(rbenv init -)”` を書いておく

```bash
rbenv install --list
rbenv install 2.3.1
rbenv global 2.3.1
rbenv global
gem update --system
gem install bundler
bundle init
```

Gemfile 編集

```
source 'https://rubygems.org'
gem 'github-pages', group: :jekyll_plugins
```

```
bundle install
```

nokogiri のinstallに失敗したので下記の記事のように実行したら直った。
[nokogiri 1.6.5 でコケる場合 for mac user](https://gist.github.com/koudaiii/adf0fa29bfb7fc13531b)
あと `bundle config build.nokogiri --use-system-libraries` も設定したけど関係があるのかよくわりません

```
bundle exec jekyll new . --force
bundle exec jekyll serve
```

としたがエラーになりました

`exclude: [vendor]` を _config.yml に追記するといいらしいです [invalid date '0000-00-00' from template · Issue #2938 · jekyll/jekyll](https://github.com/jekyll/jekyll/issues/2938)

一旦 commit , pushして反映されることを確認

### その他設定

最初は設定するものが多いので、 [issue](https://github.com/hushin/hushin.github.io/issues) を立てて管理するようにしました。

- 独自ドメイン
- コメント欄
  - [Disqus](https://disqus.com/)
- SEO対策
  - robots.txt
- SNS連携
  - [zenback](https://zenback.jp/)
- Theme
  - [Themes - Jekyll • Simple, blog-aware, static sites](https://jekyllrb.com/docs/themes/) 3.0だとまだ使えないので自分でカスタマイズするしかなさそう
- Google Analytics

### 記事の書き方

_posts/YEAR-MONTH-DAY-title.md にファイルを作る

参考：[Writing posts - Jekyll • Simple, blog-aware, static sites](https://jekyllrb.com/docs/posts/)

ファイルを生成するのも若干手間なので、
[jekyll/jekyll-compose](https://github.com/jekyll/jekyll-compose) を使ってコマンドラインで作り始めます。このあたりはHexoのほうがわかりやすかったです。

```
bundle exec jekyll post "hoge fuga"
```

## その他参考にさせていただいたサイト

- https://github.com/zerobase/zerobase.github.io
- https://github.com/efcl/efcl.github.io
