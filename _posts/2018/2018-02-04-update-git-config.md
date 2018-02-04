---
layout: post
title: 'git, tig の設定を見直したら捗った'
date: '2018-02-04 23:51'
tags:
  - git
---

今まではSourcetreeでgitを操作することが多かったです。
ただ、複数リポジトリを管理しようとするとウィンドウが複数立ち上がりややこしいという問題がありました。<br />
CLIでも扱えるようになっていると何かと便利なのでgitの設定を見直したら操作が捗りました。
dotfilesはこちらになります <https://github.com/hushin/dotfiles>

- zsh系
  - ghq と peco と anyframe
- `.gitconfig`
  - 前は短く打てるようにいろいろ登録してたけど、ほとんどtig上で操作するので不要なものは削除。
  - showpr, openpr など tigと組み合わせると便利
- `.tigrc`
  - [Tig で Git を自由自在に操作するための .tigrc 設定例 - Qiita](https://qiita.com/sfus/items/063797a1dd8fdc7d032f) を参考に設定。

## tigでの操作メモ

- [超絶便利なGitクライアントのtigのすすめ - Qiita](https://qiita.com/vivid_muimui/items/7e7a740e6537749de0c0) がわかりやすいです

### ファイルから履歴を追う

1. `t` で tree
2. `enter` で blob
  - 更に `e` でエディタで開く
3. `b` で blame
4. `,` でそのコミットを起点にした blame
  - `<`で戻る
  - `B` で そのコミットを開く
  - `w` でそのコミットが含まれたプルリクを開く
