---
layout: post
title: Kindle本をブクログで蔵書管理する最初の一歩
tags:
  - kindle
---

未読本を管理するためにブクログを始めました。

[hush_in 本棚 - ブクログ](http://booklog.jp/users/hush1n/)

まず本棚にある紙の未読本（70冊程）はブクログのアプリでバーコードスキャンしました。

次にKindleで買った本の蔵書管理へ。
Kindleで買っている本が 800冊 くらいあり、手動で登録するのは辛いので、
[コンテンツと端末の管理](https://www.amazon.co.jp/gp/digital/fiona/manage) からデータを取るようにしました。

## 備忘録

ここではデータを取得してCSVで登録する備忘録を書いておきます。自分用のメモなので解説少な目です。

### JSONを取得

Chromeの開発者ツールを開き、 ref=myx_ajax のリクエストのうち OwnershipData を取っているリクエストがあるので、curlでコピーする。 あとはcurlをいじってローカルにJSONをDLする。
batchSizeは18になっているので100くらいにする（1000は弾かれた）。
startIndexが0なので100ずつ増やして全部取得する。ファイル名は適当にdata1.json, data2.json ... と連番で取る。

### jq コマンドでCSVにする

[jqコマンド](http://stedolan.github.io/jq/) を使って整形していく。

手始めに `jq '.OwnershipData.items[] | .title' data1.json` などと実行するとタイトル一覧が表示されることを確認。

次に抜き出したい要素を選んでCSV化する。 slurpオプションで複数JSONを扱える。

```
jq -r -s '.[].OwnershipData.items[] | [.title, .authors, .asin, .acquiredDate, .acquiredTime, .sortableTitle, .sortableAuthors, .numericFileSize, .isPurchased] | @csv' *.json > all.csv
```

### GoogleスプレッドシートでCSVを読み込んで整形

Googleスプレッドシートで先程のCSVを読み込んで整形していく。

- ブクログに登録しない本はここで削除する。
- CSVで読書状況も登録できるので列を追加してつける
![spreadsheet](/images/2016/spreadsheet.png)


[まとめて登録 (CSV)](http://booklog.jp/input/file)
ここにフォーマットが載っているので別シートで揃える。
![spreadsheet2](/images/2016/spreadsheet2.png)

- 読み終わった本は登録日時の一日後など適当に埋めた。
- スプレッドシートから出力されるCSVにはダブルクオーテーションがついてないので手動で微修正。`,`を`","`に置換して行頭と行末に`"`を追加。
- 800件のCSV読み込ませるのが不安だったが、十秒くらいでインポートできた。


## やってみたまとめ

- Kindleでは800冊中約600冊は読み終えていて、200冊積読していました。
  - ブクログ登録前は何を読んでないか把握できていない状態でモヤモヤしていましたが、登録することで一覧できてすっきりしました。
  - 読書状況が思い出せないのがチラホラありました。それだけ記憶に残ってないと思うとちょっともったいない。
- 追加で登録していくのは簡略化したいです。こちらの記事が参考になりそうです。 [Kindle本をブクログに自動登録する - tateren’s diary](http://tateren.hateblo.jp/entry/2016/10/03/025425)
