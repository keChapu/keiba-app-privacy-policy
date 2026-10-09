# DESIGN.md ライブラリ:有名プロダクトのデザイン言語を AI 用に変換

- 出典: X(Twitter)の投稿(@Voxyz_ai の動画と、日本語の紹介投稿。ユーザーが共有)
  - 投稿: https://x.com/Voxyz_ai/status/2093766772029559077
- 関連サイト・リポジトリ:
  - https://github.com/VoltAgent/awesome-design-md(MIT。2026-10-09 に取得して確認。最新コミット 13be5c0)
  - https://getdesign.md/(VoltAgent チームのサイト)
  - 類似: designmd.app(759件)、designmd.directory(87件)、designmd.co
- 保存日: 2026-10-09
- タグ: #デザイン #DESIGN.md #UI #ClaudeCode #デザインシステム

## 投稿の主張

- 世界の有名プロダクト2,000以上のデザイン言語を、Claude Code / Codex が読める `DESIGN.md` に変換した。無料。
- 中身: 色とトークン、フォント(サイズ・太さ)、余白とレイアウト、コンポーネントのスタイル、使う / 避けるのルール。
- プロジェクトに1枚置くだけで「AIっぽい汎用デザイン」から脱却できる。Tailwind v4 や CSS 変数の形式もある。

## 確認できたこと

- **「2,000以上」は未確認。** 調べたサイトの件数:

| 場所 | 件数 |
| --- | --- |
| VoltAgent/awesome-design-md | **74件** |
| designmd.app | 759件 |
| designmd.directory | 87件 |

- 投稿の数字は、複数サイトの合計か誇張の可能性がある。
- VoltAgent 版の収録例:
  - Linear / Notion / ElevenLabs / **Lamborghini** / Apple / Stripe / Vercel / Spotify / Airbnb / Nike / Tesla / Ferrari など。
- **ファイルの形式:**
  - 先頭の YAML に `colors`(primary / ink / canvas / surface / hairline など)と `typography`(display-xl〜、サイズ・太さ・行間・字間)を書く。
  - 本文は「どう使うか / 使わないか」のルールを文章で書く。
  - 例: Linear は「ほぼ黒の背景 `#010102` に、ラベンダー `#5e6ad2` をアクセント1色だけ。装飾には使わない」。
- 公式のブランドガイドではなく、**第三者がサイトを分析したもの**。同じ ElevenLabs でも、サイトによって内容が食い違っている。

## このアプリ(競馬アプリ)での活かし方

- **他社のデザインをそのまま使うのではなく、自分のアプリ専用の `DESIGN.md` を作る。**
  1. 雰囲気の近い DESIGN.md を2〜3個参考に読む。例: 情報量が多く見やすいなら Linear 系、親しみやすさなら Notion 系。
  2. Claude に、競馬アプリ用の DESIGN.md を作らせる。内容:
     - 色: ブランド色1色 + 背景・文字・区切り線の段階
     - 文字サイズの段階
     - 余白の単位
     - コンポーネント: 出馬表の行、オッズのセル、ボタン
     - 「やらないこと」リスト
  3. アプリ本体のリポジトリに置く。`CLAUDE.md` から「UI を作るときは DESIGN.md に従う」と参照させる。
- **SwiftUI への変換:** 色は Asset Catalog の Color Set(ライト / ダーク)、文字は Dynamic Type に対応した `Font` 拡張、余白は定数に落とし込む。
- **同じ DESIGN.md を全部に使う:** このリポジトリの `index.html` / `support.html`、ストア画像(Compositor)、動画(Remotion / Motion)にも適用して、見た目を統一する。
- 競馬アプリ向けの決めごとの例:
  - 枠番の色(白・黒・赤・青・黄・緑・橙・桃)は競馬の慣習どおりに定義する。
  - 数字(オッズ・タイム)は等幅数字(`monospacedDigit()`)で表示する。

## 注意点

- 有名ブランドの見た目を丸ごと真似ると、トレードドレス(見た目の模倣)や商標の問題になりうる。App Store 審査の「模倣」(ガイドライン 4.1)にも注意する。参考にとどめ、独自色を入れる。
- 収録ファイルのカスタムフォント(例: Linear Display)は使えない。代わりのフォントを決めておく。
- iOS アプリは、Web 向けの DESIGN.md より Apple の Human Interface Guidelines を優先する。例: タップ領域44pt、Dynamic Type、ダークモード。
