# ゼロのタロット ブログ 引き継ぎメモ

## 基本情報
- **サイトURL**: https://tarot-blog.pages.dev
- **GitHubリポジトリ**: noctisluciscaelumversus-boop/tarot-blog
- **ローカルフォルダ**: `~/public/tarot-blog`
- **ホスティング**: Cloudflare Pages（GitHubへpushすると自動デプロイ）

---

## フォルダ構成（2026-05-09 整理済み）

```
~/public/tarot-blog/public/
├── index.html              ホーム
├── 404.html
├── hajimeni.html           はじめにページ
├── cat_kareshi.html        カテゴリ：元彼の気持ちを占ってみた
├── cat_cardguide.html      カテゴリ：カード解説
├── google4480c465297673ad.html  Search Console認証ファイル
├── cards/                  タロット画像（PNG）
├── lenormand_cards/        ルノルマン画像（PNG）
├── articles/               ブログ記事HTML（article_*.html）
└── cardguide/              カード解説HTML（card_*.html）
```

**パスの注意：**
- `articles/` や `cardguide/` 内のファイルから画像を参照するときは `../cards/`
- ルート（index.html等）から記事へのリンクは `articles/article_xxx.html`
- ルートからカード解説へのリンクは `cardguide/card_xxx.html`

---

## 作業ルール

### 必須：作業後は必ずgit pushまで実行する
```bash
cd ~/public/tarot-blog
git add <ファイル>
git commit -m "メッセージ"
git push
```
pushしないとサイトに反映されない。ユーザーに確認を求めず、作業完了時に自動でpushまで実行すること。

### ホームのRecent Posts：常に5枚キープ
- 「はじめに」カード：**固定・削除しない**
- 最新記事：**4枚まで**
- 新記事を追加したら、4枚の中の最古の1枚を削除する
- 古い記事はcat_kareshi.htmlで全件表示（削除しない）

---

## ブログ記事の作成手順

### ファイル名規則
- ブログ記事：`articles/article_kareshi_YYYY_MMDD.html`
- 日付は記事の投稿日に合わせる

### 記事HTMLのフォーマット
- 参照ファイル：`public/articles/article_kareshi_2026_0502.html`
- 画像パス：`../cards/ファイル名`
- ホームへのリンク：`../index.html`
- カード解説へのリンク：`../cardguide/card_xxx.html`
- サイドバーのリンク：`../hajimeni.html`、`../cat_kareshi.html`、`../cat_cardguide.html`

### 記事の構成ルール（5/2フォーマット準拠）
1. リード文（`.lead`）
2. 目次（`.toc`）
3. **① 今回出たカード** → `.card-spread` のリスト形式で全カードを一覧表示（HTMLテーブルは使わない）
4. **② 彼の今の気持ち** → カード全体の解釈をまとめたテキスト
5. **③ それぞれのカードの意味** → `.card-block` を1セクションにまとめて並べる（カードごとに個別のh2を立てない）
6. 追加セクション（「連絡してくるか」「どう受け取るか」など）
7. **まとめ**（`.summary` ダークブルーボックス）

**注意：** `.card-table`（HTMLテーブル）は使用しない。カード一覧は必ず `.card-spread` + `.spread-list` で表示する。

### 逆位置カードの書き方
```html
<img src="../cards/Wands04.png" alt="ワンドの4" class="reverse">
```

### 記事追加時に更新するファイル（4つ）
1. `public/articles/article_kareshi_YYYY_MMDD.html`（新規作成）
2. `public/cat_kareshi.html`（カテゴリ一覧に先頭追加）
3. `public/index.html`（Recent Postsを5枚に保つよう調整）
4. `CLAUDE.md`（「現在の記事一覧」と「ホームに表示中」を最新状態に更新）

---

## カード画像ファイル名

### 大アルカナ（`../cards/`）
`00-TheFool.png` 〜 `21-TheWorld.png`（英語正式名、2桁番号）。不明なファイル名は `ls ~/public/tarot-blog/public/cards/` で確認。

### 小アルカナ（`../cards/`）
- カップ：`Cups01.png` 〜 `Cups14.png`
- ペンタクル：`Pentacles01.png` 〜 `Pentacles14.png`
- ソード：`Swords01.png` 〜 `Swords14.png`
- ワンド：`Wands01.png` 〜 `Wands14.png`
- 11=ペイジ、12=ナイト、13=クイーン、14=キング

---

## 現在の記事一覧（cat_kareshi）

| 日付 | ファイル名 | タイトル |
|------|-----------|---------|
| 2026/5/12 | article_kareshi_2026_0512c.html | 元彼は私のことをもう諦めた？タロットで世界逆・カップ2逆・カップ7逆・女教皇逆が出た意味 |
| 2026/5/12 | article_kareshi_2026_0512b.html | 元彼から連絡は来る？ルノルマンで手紙が2枚目・ジャンピングで太陽が出た意味 |
| 2026/5/12 | article_kareshi_2026_0512.html | 元彼の気持ちをタロットで占った結果｜ペンタクル2逆・ソード2逆・ペンタクル6正 |
| 2026/5/10 | article_kareshi_2026_0510.html | 元彼の私への気持ち｜カップ8正位置・ペンタクル9逆位置・月逆位置・カップ5逆位置 |
| 2026/5/4 | article_kareshi_2026_0504.html | 音信不通の元彼の今の状況は？タロットで見えた現在の彼の状態 |
| 2026/5/3 | article_kareshi_2026_0503.html | 音信不通の元彼の気持ちは？後悔と再評価が見えるタロット結果 |
| 2026/5/2 | article_kareshi_2026_0502.html | 元彼はもう諦めた？連絡してこない理由をタロットで占った結果 |
| 2026/4/29 | article_kareshi_2026_0429.html | 静かに進む心の整理と新しい感情 |
| 2026/4/28 | article_kareshi_2026_0428.html | 揺れる本音と止まったままの関係 |
| 2026/4/26 | article_kareshi_2026_0426.html | 気持ちはあるのに動けない理由 |

**ホームに表示中（5枚）：**
- はじめに（固定）
- article_kareshi_2026_0512c（最新）
- article_kareshi_2026_0512b
- article_kareshi_2026_0512
- article_kareshi_2026_0510 ← 次回新記事追加時に削除
