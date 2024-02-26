# md-to-pdfの使い方

md-to-pdfは、MarkdownファイルをPDFに変換するためのCLIツール。
Node.jsとヘッドレスChromeを使用してMarkdownをHTMLに変換し、さらにHTMLをPDFに変換。
コードハイライトにはhighlight.jsを使用。
このツールのソースコードは約250行のJavaScript、約500行のTypeScript、約100行のCSSで構成されており、クローンしてカスタマイズするのが容易。

## 主な特徴

* 複数のMarkdownファイルを同時に変換
* ウォッチモード
* 独自のスタイルシートやリモートスタイルシートの使用
* フロントマターでの設定
* ヘッダーとフッター
* ページブレーク
* コードブロック内のシンタックスハイライト
* 基礎となるツールのオプション拡張
* プログラムAPI
* 標準入出力のサポート
* HTML(またはインラインHTML)からPDFへの変換

## インストール方法:

### NPMを使用した場合

```css
npm i -g md-to-pdf
```

### Gitからクローンする場合

``` bash
git clone "https://github.com/simonhaenisch/md-to-pdf"
cd md-to-pdf
npm link # または npm i -g
```

これにより、md-to-pdfとmd2pdf（短縮形）コマンドがCLIで全体的に利用可能。
TypeScriptコンパイラ（tsc）をウォッチモードで起動するにはnpm startを使用。

## 使用方法

``` css
$ md-to-pdf [options] path/to/file.md
オプションには以下が含まれる
```

* -h, --help: 使用情報を表示
* -v, --version: バージョンを表示
* -w, --watch: 現在のファイルを監視し、変更があった場合に再変換
* --stylesheet: ローカルまたはリモートのスタイルシートへのパス（複数回指定可能）
* --css: スタイルの文字列
* その他多数のオプションがあり。

PDFはデフォルトでソースファイルと同じディレクトリに生成され、ファイル名も同じ（拡張子を.pdfに変更）。
シェルのglobbingを使用して複数のファイルを指定することもできる（例: md-to-pdf ./**/*.md）。

## プログラムAPI:

``` javascript
const fs = require('fs');
const { mdToPdf } = require('md-to-pdf');

(async () => {
    const pdf = await mdToPdf({ path: 'readme.md' }).catch(console.error);
    if (pdf) {
        fs.writeFileSync(pdf.filename, pdf.content);
    }
})();
```