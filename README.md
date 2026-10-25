# hushin blog

https://hushin-text.fdempa.com/

Jekyll で生成したサイトを、ビルド済みの静的ファイルとして `public/` にコミットしています。Netlify は `public/` の内容をそのまま配信します。

## 構成

- `public/`: 配信される静的ファイル一式
- `netlify.toml`: Netlify のビルド・配信設定

## ローカルで確認する

```sh
python3 -m http.server 4000 --directory public
```

http://localhost:4000/ を開きます。

## 更新する場合

`public/` 配下の HTML / CSS を直接編集して commit・push してください。
Netlify ではビルドコマンドは実行されません。

以前の Jekyll ソース（記事の Markdown など）は git の履歴に残っています。

## License

- Contents: [Creative Commons Attribution 4.0 International (CC BY 4.0)](http://creativecommons.org/licenses/by/4.0/) <a rel="license" href="http://creativecommons.org/licenses/by/4.0/"><img alt="クリエイティブ・コモンズ・ライセンス" style="border-width:0" src="https://i.creativecommons.org/l/by/4.0/88x31.png" /></a>
- Software: [The MIT License (MIT)](http://opensource.org/licenses/MIT)
