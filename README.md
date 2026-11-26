# riho-portfolio

山本里帆のポートフォリオサイトです。

環境は、案件で使っている Gulp + webpack + EJS + Sass の構成をそのまま使っています。

## 使い方

```
npm install
npm run start   # ローカルサーバー起動。/src を保存すると /dist に書き出される
npm run build   # 本番用ビルド。/dist を消してから書き出し直す
```

`/dist` はビルドのたびに消えるので、直接触らないでください。

## ページ

| ページ | ファイル |
| --- | --- |
| トップ | `src/index.ejs` |
| ケーススタディ ノラネコぐんだん | `src/works/noraneko.ejs` |
| ケーススタディ 山遊部 | `src/works/yamaasobu.ejs` |
| ケーススタディ Hello Novelty! | `src/works/marutatsu.ejs` |

頭に `_` が付いたファイル・フォルダはパーツ扱いで、ページとしては書き出されません。

## Sass のルール

- SPファーストで書き、`@include pc` でPC（920px以上）を上書きする
- SPは375pxを基準に可変
  - `spCalc(24)`：375px幅のデザインで24pxの幅を、親要素に対する % にする
  - `spf(15)`：375px幅で15pxの文字を vw にする（大きくなりすぎないよう1.4倍で止める）
- PCは最大幅1200pxのコンテナの中で、px で指定する
- 色は `_common.scss` の変数を `c.$accent` のように使う

## 文字落ち対策

見出しや短い文は、1文字だけ次の行に落ちないように調整しています。

- 意味の区切りで改行するときは `<br class="sp">` / `<br class="pc">`
- 途中で改行させたくない語句は `<span class="nowrap">`
- 見出しには `word-break: auto-phrase` と `text-wrap: pretty` を指定（対応ブラウザのみ効く）
- 本文の約物は `font-feature-settings: "palt"` で詰める

## JavaScript（STEP 2 で自分で書く）

`src/assets/js/_modules/` に、書く予定の動きのファイルを空の状態で用意しています。jQueryは使わず、素のJSで書きます。

| ファイル | 動き | HTML側の目印 |
| --- | --- | --- |
| `_menu.js` | SPのメニューの開閉 | `[data-menu-button]` `[data-menu]` |
| `_header.js` | 下にスクロールでヘッダーを隠し、上で出す | `[data-header]` |
| `_hoverVideo.js` | PCはホバー、SPは画面に入ったら動画を再生 | `[data-hover-video]` |
| `_toc.js` | ケーススタディの目次で、読んでいる見出しをハイライト | `[data-toc]` `[data-toc-target]` |

どの動きも、`prefers-reduced-motion: reduce` のときは止めるか弱めます。
