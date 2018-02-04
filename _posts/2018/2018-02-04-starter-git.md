---
layout: post
title: 入門git読んだ
date: '2018-02-04 22:37'
tags: git
---

数年前買った『入門git』、昔ちょっとだけ読んだ後放置していた。

普段からgit使うようになったこともあり、久々に読んだらだいぶ分かるようになっていた。

あんま使ったことないものメモ

- 前回のコミット修正
  - `git commit -m "message" --amend`
  - `git commit -C HEAD --amend`
- `git merge --squash <ブランチ>`
  - rebase -i か no-ff 使うこと多い
- `git blame -C -C <ファイル>` 行の移動、どのファイルから来ているかを調べる
- `git gc`
- `git bisect`
- `git submodule`
