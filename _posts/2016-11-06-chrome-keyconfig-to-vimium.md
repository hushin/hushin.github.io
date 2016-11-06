---
layout: post
title: chrome keyconfig to vimium
---

Chrome拡張のKeyconfigでキーボードショートカットを変えていたのですががChrome Version54から使えなくなりました。
スクロールなどショートカットで行っていたのでこれができないと大変苦痛なので他の拡張を探すことに。

いろいろ試した結果 [Vimium](https://vimium.github.io/) を使ってみることにしました。
調べてみた時系列順に箇条書きでメモを残します。

* [Chromeバージョン54はKeyconfigが使えないので代わりの拡張機能の紹介とか](http://pasokatu.com/15313)
* 昔インストールしていた [Hometype](http://tkengo.github.io/hometype/) を再度試す
  * スクロールが滑らかでなかったりして若干合わないと思う
* [キー設定がすべてundefinedになってしまう · Issue #11 · os0x/ChromeKeyconfig](https://github.com/os0x/ChromeKeyconfig/issues/11)
* 修正版を作っている方がいたので入れてみることに。動いた。 [haburibe/ChromeKeyconfig](https://github.com/haburibe/ChromeKeyconfig)
  * [diff](https://github.com/haburibe/ChromeKeyconfig/commit/05ed8adf2771c2118f438799ce5cb2bfb1e16cf1) を見ると設定を`Esc`から`Escape`など、修正が必要そう
* せっかくだしVimperatorっぽいものを使ってみようと思い、[Vimium](https://vimium.github.io/)を導入
  * 設定はこんな感じ
```
# Atom みたいに Cmd-pで開けるように
map <m-p> Vomnibar.activateInNewTab
# a-p でtogglePinTab動かなかったので c-tへ
map <c-t> togglePinTab
# クリップボードの内容を開くは誤爆しそうだったので削除
unmap p
unmap P
# iは誤爆し易いのでc-i に insert mode 割当。insert mode は多分使わない
unmap i
map <c-i> enterInsertMode
# 手軽に別タブで開きたい
map e LinkHints.activateModeToOpenInNewTab
```

### 良かった点

- スクロールがKeyconfigよりなめらか
- Hit a Hint 便利 （[Moly HaH](https://chrome.google.com/webstore/detail/moly-hah/pjoacnohgednppackhamgfalpkffeeek?hl=ja) などでもできましたが、、）
- `o` `O` で履歴やブックマークなど高速に検索できる

### 悪かった点

- 普段Emacs使っているのでキーバインドがもやもやする
  - 設定書けばいいだけだけど、、参考：[raamdev/vimium: My Vimium key bindings (Emacs-style).](https://github.com/raamdev/vimium)
- 特定のURLを開くことができない
  -  Keyconfigではブックマークレットを登録してショートカット一発で呼べるのが良かったが、それができない
  - issueはあったが作られてない [Quick Marks · Issue #53 · philc/vimium](https://github.com/philc/vimium/issues/53)
  - cVimという別の拡張でその機能があったが、ブックマークレットを動かすとgoogle検索結果に飛んでだめでした。参考：[cVim: Google ChromeのVimperatorみたいな拡張](http://rcmdnk.github.io/blog/2014/10/22/computer-firefox/)
- ブックマークレット妥協案
  - ブックマークレットをブックマークに登録
  - `b`からのブックマークレット名で実行。参考：[Vimiumで快適なコピペ生活(Title/URL) - Qiita](http://qiita.com/nakataka777/items/c70dd9730fb96aa1d537)
  - どうせならブックマークレットいろいろ登録したい
    - [Bookmarkleter](http://chriszarate.github.io/bookmarkleter/) がminifyなどしてくれて便利
    - Markdown形式でURLをクリップボードにコピーする下記scriptを書いた。ブックマークレットをクリックしたら成功するが、Vimiumから上記の方法で実行するとコピーされない！
      - execCommandはユーザー操作からじゃないとfalseを返して失敗するっぽい？
      - しょうがなくこれだけはアドレスバーから名前打って実行。。
```js
function copyToClipboard (text) {
  var clipNode = document.createElement('textarea');
  document.body.appendChild(clipNode);
  clipNode.value = String(text).replace();
  clipNode.select();
  document.execCommand('copy', false, null);
  document.body.removeChild(clipNode);
}
copyToClipboard('['+document.title.replace(/([\[\]])/g,'\\$1')+']'+'('+location.href+')');
```
