# 自律型AIエージェントを組むための OSS 10選(フレームワーク・記憶・実行・評価)

- 出典: X(Twitter)の投稿(ユーザーが本文を共有。URLは未記録)
- 保存日: 2026-10-09(10個とも最新コミットとライセンスを確認)
- タグ: #AIエージェント #フレームワーク #評価 #記憶 #アーキテクチャ
- 関連: [人気のAIエージェント系リポジトリ5選](2026-10-09-five-ai-agent-repos.md) / [マルチモデル振り分け](2026-10-09-model-routing-orchestration-prompt.md)

## 投稿の主張

- 強力な AI モデルが1つあれば、周りの仕組みを OSS で組み合わせて、自律型システム全体を作れる。
- 全体の流れ: **モデル → コンテキスト → 計画 → 記憶 → ツール → 実行 → 評価 → 再試行**。
- 「モデル単体の性能」より「モデルの周りのシステムを作る」時代になった。

## 一覧

| 役割 | リポジトリ | 何をするか | 言語 | ライセンス |
| --- | --- | --- | --- | --- |
| 制御 | [LangGraph](https://github.com/langchain-ai/langgraph) | 状態を持つエージェントを、グラフ(ノードと分岐)で制御する。途中で止めて人が確認、も組める | Python / JS | MIT |
| 制御 | [PydanticAI](https://github.com/pydantic/pydantic-ai) | 型付きのエージェント。出力を Pydantic のモデルで検証する(構造化出力) | Python | MIT |
| 制御 | [Mastra](https://github.com/mastra-ai/mastra) | エージェント + ワークフロー + 記憶を TypeScript で | TypeScript | Apache-2.0(`ee/` 配下は別ライセンス) |
| 制御 | [Agno](https://github.com/agno-agi/agno) | 複数エージェントを連携させるマルチエージェント | Python | Apache-2.0 |
| 記憶 | [Cognee](https://github.com/topoteretes/cognee) | データを知識グラフ化し、エージェントの記憶にする | Python | Apache-2.0 |
| 記憶 | [Graphiti](https://github.com/getzep/graphiti) | 時間とともに変わる知識を管理する(時系列の知識グラフ) | Python | Apache-2.0 |
| 操作 | [Browser Use](https://github.com/browser-use/browser-use) | エージェントが Web サイトを直接操作する | Python | MIT |
| 実行 | [E2B](https://github.com/e2b-dev/E2B) | AI が書いたコードを、隔離されたサンドボックスで実行する(クラウドサービスと SDK) | Python / JS | Apache-2.0 |
| 運用 | [Langfuse](https://github.com/langfuse/langfuse) | 実行履歴の追跡、評価、コスト・品質の可視化 | TypeScript | MIT(`ee/` 配下は別ライセンス) |
| 運用 | [DeepEval](https://github.com/confident-ai/deepeval) | LLM / エージェントのテスト。pytest 風に評価指標で採点する | Python | Apache-2.0 |

- ※ 「オープンソース」でも、Mastra と Langfuse は一部(`ee/`)が企業向けの別ライセンス。E2B・Langfuse などは、ホスティング版が有料サービスになっている。

## 全体像の整理(自分用)

- **Claude Code を使う場合の対応:**
  - 制御と計画: Claude Code 本体 / Claude Agent SDK
  - 記憶: `CLAUDE.md`・メモリ・MCP(codebase-memory-mcp など)
  - ツール: MCP・Skills
  - 実行: クラウドセッション / サンドボックス
  - 評価: テスト・lint などの決定論的な検証
- 自前でエージェント製品を作るときに、上の10個から必要な部分だけ選ぶイメージ。
- 一番大事なのは最後の「**評価 → 再試行**」。作りっぱなしにせず、テスト(DeepEval)と記録(Langfuse)で品質を測る。マルチモデル振り分けのメモの「決定論的な検証を優先」と同じ考え方。

## このアプリ(競馬アプリ)での活かし方

- **アプリにAI機能を入れる場合(サーバー側):**
  - 例: 「レースの見どころ解説」「お気に入り馬の近況まとめ」。
  - **PydanticAI** で出力を型で固定する(例: `{馬名, 要点3つ, 出典}`)。崩れた出力をアプリに流さない。
  - **DeepEval** で「根拠のない断定をしていないか」「『必ず当たる』系の表現がないか」をリリース前にテストする。
  - **Langfuse** で本番の出力とコストを監視する。
- **開発の補助:** Browser Use で、自分のサイト(サポートページなど)の表示確認を自動化する。
- いまの規模(個人開発・iOS アプリ)なら、まずは Claude Code + 決定論的なテストで十分。サーバー側でAI機能を作る段階になったら、上の表から選ぶ。

## 注意点

- **Browser Use で他社サイト(競馬データの提供元など)を自動取得するのは避ける。** 規約違反や過剰なアクセスになりうる。データは正規の提供元・API を使う。
- AI 機能を入れたら、プライバシーポリシー(このリポジトリ)に、AI サービスへのデータ送信を追記する。App Store のプライバシー表示も更新する。
- 競馬の予想を AI に出させる機能は、根拠の明示と「参考情報」であることの表示が必須。
- 依存を増やしすぎない。1つずつ、必要になってから入れる。
