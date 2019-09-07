# pandoc-latex-template

## 目的

Pandocを使ってMarkdownをPDF変換する．

デフォルトのテンプレートだと細かいところで要求を満たせないので，カスタマイズして要求通りのPDFに仕上げられるようにする．

## やりたいこと

- 表紙をつける．
  - 画像を挿入．
  - 表を作って承認者みたいな欄を作る．
  - 会社，部門，チーム名を`header.yaml`で設定できるようにする．
- 目次ページを作る．
- 変更履歴のページを作る．
  - できればコミットログを自動でマージするようにして手で編集しなくていいようにしたい．
  - それかchangelog.mdみたいなファイルに独立させて書くとか？ダサい．
- 各見出しに番号を振る．

## 改造内容

### タイトルページ

タイトルページの右下あたりに表を出力するように改造．左から下記の順で名前を表示する．

1. 顧客のPM（プロジェクト責任者）
2. 顧客のPL（プロジェクト推進者）
3. 自社のPM（プロジェクト責任者）
4. 自社のPL（プロジェクト推進者）

表示させる名前は`header.yaml`で設定する．

|    キー    |      内容      |                   説明                   |
| :--------- | :------------- | :--------------------------------------- |
| customerPm | 顧客PMの名前   | 末尾に「半角スペース」＋「様」を自動付与 |
| customerPl | 顧客PLの名前   | 末尾に「半角スペース」＋「様」を自動付与 |
| ourPm      | 自社のPMの名前 |                                          |
| ourPl      | 自社のPLの名前 |                                          |

<!-- #### Pandocのデフォルトテンプレートで用意されているもの

|   キー   |     内容     |                説明                |     |
| :------- | :----------- | :--------------------------------- | --- |
| title    | タイトル     |                                    |     |
| subtitle | サブタイトル |                                    |     |
| date     | 日付         | `\today`ってすれば現在日付になる． |     |
| author   | 著者         |                                    || --> 

### ヘッダとフッタ

タイトル，目次ページには表示しない．ページ番号はタイトルページを1ページ目としてカウントしていく．

| ヘッダ・フッタ | 位置  |                説明                 |
| :------------- | :---: | :---------------------------------- |
| ヘッダ         |  左   | `\thesection`                       |
|                | 中央  | なし                                |
|                |  右   | `\rightmark`（`header.yaml`で設定） |
| フッタ         |  左   | なし                                |
|                | 中央  | `\thepage`                          |
|                |  右   | なし                                |

## 実行コマンド

完全に自分の環境用．

```bash
find . -maxdepth 1 -name '*.md' -o -name 'header.yaml' | xargs cat | pandoc -o output.pdf --template=customed-default.tex --pdf-engine=lualatex -V documentclass=ltjsarticle
```

