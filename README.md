# おもろグ〜

Threads・X・Instagramで見つけた「コメント欄が大喜利みたいに盛り上がっている、平和で面白い投稿」を集めるキュレーションサイト。森のほっとニュースの姉妹サイト。

## 構成

- `index.html` — サイト本体（単一ファイル）。`data.js` を読み込んで投稿カードを描画する
- `data.js` — 投稿データ（`window.OMORO_DATA.entries`）。新しい投稿は配列の先頭に追加する（最新が一番上）。各エントリーは `{ id, date, dateLabel, platform, title, body, url }`。紹介文は自前の言葉で短く書く。架空のURLは入れない
- `omorocchi.png` — おもろっち（大人形、ヘッダー兼用）
- `omorocchi-icon.png` / `favicon.ico` — アイコン
- `stage-*.png` — 育成ステージ画像（下記）

## おもろボタンと育成

- いいねは「おもろボタン」（おもろっちの顔＋「おもろ」＋数字）。1人1投稿1回（localStorage `omoro-liked` で判定）
- 集計は Supabase（プロジェクト mizujoshinomori / ref twxxcjjffznjaeyconoc、ほっとニュースと共用・無料枠のみ）
  - テーブル `omoro_likes`（post_id text PK, count int, updated_at）
  - RPC `increment_omoro_like(p_post_id text)` → 新しい count を返す
- サイト全体のおもろ合計に応じて、ヘッダーのおもろっちが成長する（共同育成）
  - ステージ定義と閾値は `index.html` 内の `STAGES` 定数で調整する
  - 現在：ベビー（0〜）→ 子供（30〜）→ 大人（100〜）→ ダイダラ（300〜）→ 神（800〜）

## push

- リポジトリ：ankantakeshi-design/omoro-good
- `python3 push_omoro_repo.py` で FILES 固定リストを push する（生成中間ファイル `media-generation-*` は対象外）
