# pandoc-latex-template

## 目的

Pandocを使ってMarkdownをPDF変換する．

デフォルトのテンプレートだと細かいところで要求を満たせないので，カスタマイズして要求通りのPDFに仕上げられるようにする．

## やりたいこと

- 表紙をつける．
  - 画像を挿入．
  - 表を作って承認者みたいな欄を作る．
- 目次ページを作る．
- 変更履歴のページを作る．
  - できればコミットログを自動でマージするようにして手で編集しなくていいようにしたい．
  - それかchangelog.mdみたいなファイルに独立させて書くとか？ダサい．
- 各見出しに番号を振る．

## 実行コマンド

完全に自分の環境用．

```bash
find . -name '*.md' -o -name 'header.yaml' | xargs cat | pandoc -o output.pdf --template=customed-default.tex --pdf-engine=lualatex -V documentclass=ltjsarticle
```

