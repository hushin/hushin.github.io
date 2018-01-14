---
layout: post
title: Chrome cVimの設定メモ
tags:
  - chrome
---
前回ChromeからFirefoxに乗り換えたのですが、
Firefoxのタブを閉じたり移動するときにCPU100%使って固まることが頻繁に起きるようになったので結局Chromeに戻ってきました。

Vimperatorライクな拡張を使いたかったので、
一番カスタマイズできそうなcVimを導入したのでメモしておきます。

## 設定

### chrome://extensions/ の cVim のオプション

gistから設定をインポートできるらしいので 下記を設定 [https://gist.github.com/hushin/f1a3d90b9db63026e798a90795733c6b](https://gist.github.com/hushin/f1a3d90b9db63026e798a90795733c6b)

CSSを一部修正してSave

```css
#cVim-link-container, .cVim-link-hint,
#cVim-hud, #cVim-status-bar {
  font-family: Helvetica, Helvetica Neue, Neue, sans-serif, monospace, Arial;
  font-size: 11pt !important;
  -webkit-font-smoothing: antialiased !important;
}

#cVim-link-container {
  position: absolute;
  pointer-events: none;
  width: 100%; left: 0;
  height: 100%; top: 0;
  z-index: 2147483647;
}

.cVim-link-hint {
  position: absolute;
  color: black !important;
  background: -webkit-gradient(linear, left top, left bottom, color-stop(0%,#FFF785),
  color-stop(100%,#FFC542));
  border: 1px solid #E3BE23;
  padding: 2px !important;
  font-size: 12pt !important;
  font-weight: 500 !important;
  text-transform: uppercase !important;
  border: 1px solid #ad810c;
  border-radius: 3px;
  display: inline-block !important;
  vertical-align: middle !important;
  text-align: center !important;
  box-shadow: rgba(0, 0, 0, 0.3) 0px 3px 7px 0px;
}
```

### chrome://extensions/ の キーボードショートカット

* cncpcompletion でCtrl-n を設定したいのですが、後述するバグがあるので現時点では設定見送り

### 参考にさせていただいたサイト

* [cVim カスタマイズ \| few light](http://fewlight.net/2015/10/23/09/40/24/)
* [chromeのcVimの社内用セッティング](https://gist.github.com/mtdtks/ca838c998128f4559359)


## 良かった点と不満点

* 良かった
  * スクロールがスムーズ
* 不満点
  * ~~vimperatorのcopy.jsプラグイン相当の機能が欲しい~~
    * Code blocks でJSが書けたので解決
  * Firefoxと違って新しいタブやページ読み込み中ショートカットが使えない
  * cncpcompletion のバグ
    * コマンドモードの候補をTABではなく`<C-n>` `<C-p>` で選択したいが、なぜか`<C-n>`で新しいタブが開いてしまう <https://github.com/1995eaton/chromium-vim/issues/390>
