# GitHub で人気の AI エージェント系リポジトリ5選

- 出典: X(Twitter)の投稿(ユーザーが本文を共有。URLは未記録)
- 保存日: 2026-10-09(5つとも取得して README とライセンスを確認)
- タグ: #AIエージェント #ClaudeCode #並列化 #動画 #MCP #トークン節約
- ※ 投稿のスター数(148K / 76K / 57K / 54K / 41K)は、この環境から GitHub API を使えないため未確認。

## 一覧

| # | リポジトリ | 何をするか | ライセンス | 最新コミット |
| --- | --- | --- | --- | --- |
| 1 | [msitarzewski/agency-agents](https://github.com/msitarzewski/agency-agents) | 役割別の AI エージェント定義(Markdown)集。**306ファイル・約20分野**(engineering / design / marketing / testing / security など)。Claude Code なら `~/.claude/agents/` にコピーして使う | MIT | f99f6aa(10/07) |
| 2 | [Panniantong/Agent-Reach](https://github.com/Panniantong/Agent-Reach) | エージェントにネットを読む力を付ける。Web / YouTube 字幕 / RSS / 検索は設定なしで使える。X / Reddit / 小紅書などは**自分のログイン Cookie が必要** | MIT | 94f06c1(10/08) |
| 3 | [stablyai/orca](https://github.com/stablyai/orca) | Codex / Claude Code / OpenCode / Pi を、別々の git worktree で並列実行するデスクトップアプリ。1つの指示を5体に投げて結果を比べられる。スマホのアプリから監視・指示もできる | MIT | bd85767e(10/09) |
| 4 | [calesthio/OpenMontage](https://github.com/calesthio/OpenMontage) | コーディングエージェントを動画スタジオにする。調査 → 台本 → 素材生成 → 編集 → 書き出し(Remotion など)。生成 AI の動画・音声サービス(有料 API)も使える | **AGPL-3.0** | 9327439(10/03) |
| 5 | [DeusData/codebase-memory-mcp](https://github.com/DeusData/codebase-memory-mcp) | コードを tree-sitter で解析して知識グラフ化する MCP サーバー(162言語)。構造的な質問5件で約3,400トークン(ファイルを1つずつ読むと約412,000トークン)と主張している。ツールは17個 | MIT | 72a2c0b(10/09) |

## このアプリ(競馬アプリ)での活かし方

- **agency-agents:** 全部入れずに、必要な定義だけ選んで自分用に直す。全部入れるとエージェントの選択が迷子になる。
  - `engineering/engineering-mobile-app-builder.md`(モバイルアプリ開発)
  - `engineering/engineering-mobile-release-engineer.md`(リリース作業)
  - `marketing/marketing-app-store-optimizer.md`(ASO。App Store アセットのメモと組み合わせる)
  - `testing/` 配下(テスト)
- **codebase-memory-mcp:**
  - アプリのコードが大きくなってきたら効果がある。Swift も対応言語に含まれる。
  - Claude の利用上限対策になる。「変更の影響範囲」「使われていないコード」の調査に使える。
- **orca:**
  - 同じ UI の案を Claude Code と Codex に並列で作らせて、良いほうを採用する、などに使える。
  - 前回の「マルチモデル振り分け」の発想を、人が手動でやる版。
- **OpenMontage:**
  - 宣伝動画の自動制作に使える(動画系の過去メモ: Remotion / HyperFrames / Claude Motion と比較)。
  - 生成 AI の動画 API を使うと費用がかかる。
- **Agent-Reach:**
  - **このナレッジ集めの目的(X の有益情報を読む)に一番近い。**
  - ただし X を読むには、自分の X アカウントの Cookie を書き出して渡す必要がある。
  - 手元の Mac で使う前提。いまのクラウド環境は x.com への接続自体が遮断されている。

## 注意点

- **Agent-Reach の Cookie 利用:**
  - X・Reddit などの規約(自動取得の禁止)に触れる可能性がある。アカウント凍結のリスクもある。
  - 使うなら本アカウントではなく閲覧専用のサブアカウントにする。Cookie はリポジトリに入れない。
  - 現状は「本文を貼ってもらってメモにする」今のやり方が一番安全。
- **OpenMontage は AGPL-3.0:**
  - 改変してネット上のサービスとして提供すると、ソース公開の義務が生じる。
  - 自分の動画を作る道具として手元で使う分には問題になりにくい。
- **codebase-memory-mcp:**
  - インストールすると、エージェントの設定ファイル・フック・常駐デーモンまで自動で書き換える。
  - `--skip-config` で中身を確認してから設定する。
  - Windows Defender の誤検知があると README に記載がある。
- **`curl ... | bash` 形式のインストール:** スクリプトを一度読んでから実行する。
- 「エージェンシーや開発チームの半分を置き換えられる」は誇張。導入するほど管理(権限・費用・レビュー)の手間が増える。まずは1つずつ試す。
