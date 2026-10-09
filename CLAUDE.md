# CLAUDE.md

## このリポジトリについて

- 競馬アプリのプライバシーポリシー(`index.html`)とサポートページ(`support.html`)を公開するためのリポジトリ。
- `notes/` には、X(Twitter)などで集めたアプリ開発用のナレッジメモを置いている。1トピック1ファイル。一覧は `notes/README.md`。
- メモを追加するときのルール:
  - ファイル名は `YYYY-MM-DD-topic.md`。`notes/README.md` の一覧表にも1行追加する。
  - 必ず書く項目: 出典、保存日、タグ、要点、活かし方、注意点。
  - 確認できたことと、投稿の主張(未確認)を区別して書く。
  - 宣伝・誘導リンクは記録しない。記事の全文は転載せず、要約する。
- 公開リポジトリなので、APIキー・個人情報・非公開の情報は書かない。

## アプリを作るときは必ず参照する(ユーザー指示)

- 新しいアプリの作成や既存アプリの改修では、**[`notes/APP_PLAYBOOK.md`](notes/APP_PLAYBOOK.md) を必ず参照する**。
  - 状況に応じて、課金・収益、デザイン・UI、素材・動画づくりの項目を提案・使用する。
- 別のリポジトリで作業するときも、このプレイブックの内容をそのリポジトリの `CLAUDE.md` に入れて使う。

## ナレッジの要約(2026-10-09 時点、33件)

### 共通の原則(複数のメモに共通する教訓)

1. **手順は文章で残す。** 毎回うまい指示を考えるより、手順を CLAUDE.md / SKILL.md に書いて使い回す。
2. **AIの判断より、決定論的な検証を信じる。** テスト・ビルド・lint・実ファイルを確認する。実行していない検証を「やった」と言わない。
3. **書く役と確かめる役を分ける。** 結果は「正しい / 誤り / 未確認」の表で返させる。推測で書かせず【要確認】の印を付けさせる。
4. **安いモデルから始め、証拠があるときだけ上げる。** 雑用は下請け(Haiku)に回す。下請けが読んだ中身は、指揮役の会話に残らない。
5. **取り返しのつかない操作は人が確認する。** 送信・公開・課金・審査提出・削除が対象。読む・下書きは自動でよい。
6. **SNSの投稿は話を盛りがち。** スター数・「全言語対応」・「2,000件」などは確認する。確認できたこととできないことを分けて書く。

### 1. AI開発ハーネス・エージェント

- [ハーネス入門の7つの仕掛け](notes/2026-10-09-claude-code-harness-7-parts.md):
  - 就業規則(CLAUDE.md)、業務マニュアル(Skills)、資料室の鍵(MCP)、立入禁止の札(permissions)、校閲担当(サブエージェント)、本気度(effort)、納品の条件(/goal)。
  - 引き継ぎメモ `progress.md` で翌日も続きから再開できる。
  - まずは CLAUDE.md と校閲担当の2つから始める。
- [Haiku の下請けに雑用を回す](notes/2026-10-09-claude-code-haiku-errand-delegation.md):
  - 読み取り専用のサブエージェント `errand` と、助言だけするフック。迷ったら委譲しない。
- [マルチモデル振り分けプロンプト](notes/2026-10-09-model-routing-orchestration-prompt.md):
  - 証拠があるときだけモデルを上げる。高リスクな変更は最上位モデルでレビューする。完了条件を明確にする。
- [SKILL.md でショート動画を量産](notes/2026-10-09-skill-md-short-video-factory.md):
  - SKILL.md を「入力 → 数値の基準 → 確認項目 → 出典ルール」の4点セットで作る。
- [OpenAI dots](notes/2026-10-09-openai-dots-agent.md):
  - 常時稼働エージェント。仕事は「担当」として渡す。権限は4段階で設定する。「下書きして」は「送ってよい」の意味ではない。
- [人気リポジトリ5選](notes/2026-10-09-five-ai-agent-repos.md):
  - agency-agents(役割定義集)、Agent-Reach(Webを読む。X は Cookie が必要で規約リスクあり)、orca(並列 worktree)、OpenMontage(動画、AGPL)、codebase-memory-mcp(トークン節約)。
- [エージェント構築OSS 10選](notes/2026-10-09-ten-agent-framework-repos.md):
  - LangGraph / PydanticAI / Mastra / Agno / Cognee / Graphiti / Browser Use / E2B / Langfuse / DeepEval。
  - 「評価 → 再試行」が一番大事。

### 2. App Store・ASO・課金

- [App Store Connect API + `asc` CLI](notes/2026-10-09-asc-api-ai-automation.md):
  - APIキー(.p8)で、ストア画像・リリースノートをコマンドで更新できる。キーは権限を絞り、Git に入れない。
- [新ヘッダー画像・検索結果アセット](notes/2026-10-09-app-store-header-search-assets.md):
  - iOS 27 以降。Asset Library で単体審査でき、アプリの更新は不要。
  - キーワード別の CPP で出し分けられる。PPO で A/B テストする。
  - **既存アプリも設定する価値が高い**(10/14 にリマインド設定済み)。
- [ペイウォールの改善例](notes/2026-10-09-paywall-redesign-example.md):
  - 実物を見せる、特典は1行のチェックリスト、年額を初期選択して割引率を表示、月額 / 年額 / 買い切りの3択、「◯日間無料で試す」ボタン。
  - 審査ではトライアル後の金額の明示、復元ボタン、規約リンクが必要。
- [アフィリエイト記事ルーティン](notes/2026-10-09-claude-amazon-affiliate-routine.md):
  - 曜日で作業を固定する。【要確認】【ここに体験】マーカーを使う。「向いている人 / 向いていない人」を両方書く。

### 3. デザイン・UI

- [DESIGN.md ライブラリ](notes/2026-10-09-design-md-library.md):
  - 有名プロダクトの色・文字・余白のルールを AI 用の Markdown にしたもの(VoltAgent 版は74件)。
  - 他社を真似るのではなく、自分のアプリ専用の DESIGN.md を作る。
- [UI 参考サイト](notes/2026-10-09-ui-reference-sites.md):
  - Mobbin / Refero / Page Flows / UI Pocket / Dribbble。
  - iOS では Apple HIG を最優先する。
- [調整用スライダーUI](notes/2026-10-09-tuning-panel-ui-adjustment.md):
  - 微調整は言葉で伝えず、AI にスライダー付きの調整画面を作らせる。決めた数値を反映させる。SwiftUI では `#Preview` で作れる。
- [ガチャ演出の分析](notes/2026-10-09-gacha-animation-artifact.md):
  - 溜め → 段階的な色の昇格 → 開封。効果音・フラッシュ・揺れ・振動を同時に出す。スキップと Reduce Motion に対応する。
  - 有料ガチャは確率表示が義務。
- [直進なのに回って見える錯視](notes/2026-10-09-straight-line-circular-illusion.md):
  - `sin()` + 位相のずらしで、軽いローディング演出が作れる。
- [球面のジェネラティブアート](notes/2026-10-09-procedural-spherical-patterns.md):
  - 規則 + 乱数(シード)で、ユーザー固有のアバターやエンブレムを作れる。
- [Progate の SwiftUI 生成](notes/2026-10-09-progate-works-swiftui.md):
  - 未確認。画面のたたき台づくり用。

### 4. 素材制作(画像・ドット絵・文字素材)

- [Compositor](notes/2026-10-09-compositor-photoshop-alternative.md):
  - MIT の Mac 用 Photoshop 代替。`.comp` は PNG + manifest.json なので、AI が直接編集できる。ストア画像の量産に使える。
- [ArtCraft](notes/2026-10-09-artcraft-open-source-adobe.md):
  - Adobe 代替の7アプリ(Rust 製)。まだ開発初期。
- [文字画像APNGメーカー](notes/2026-10-09-text-apng-maker.md):
  - 透過の動く文字素材を作る。アプリにも使える。公開時はクレジット表記が必要。
- ドット絵:
  - [Aseprite](notes/2026-10-09-aseprite-pixel-art-tool.md): 約$20、CLI で一括書き出しできる。
  - [円の描き分け](notes/2026-10-09-pixel-art-circles.md): 奇数サイズは中心が1ドットに決まる。
  - [ドット絵の学校](notes/2026-10-09-pixel-art-school-youtube.md)
  - [RPG アイコン集](notes/2026-10-09-franuka-rpg-icon-pack.md): ライセンスは「ゲーム向け」なので要確認。
  - iOS で表示するときは `.interpolation(.none)` + 整数倍で拡大する。

### 5. 動画・音声

- [Claude Motion](notes/2026-10-09-claude-motion-video.md):
  - チャットだけで MP4 を作れる(Team / Enterprise のベータ)。
  - 比較: HyperFrames(無料、Claude Code + HTML)、Remotion(React、量産向き)。
- [voicebox](notes/2026-10-09-voicebox-voice-cloning.md):
  - ローカルで声のクローン・TTS。MCP で Claude Code に声を付けられる。他人の声はクローンしない。
- [honoka-tts](notes/2026-10-09-honoka-tts-whisper.md):
  - ウィスパーと無声音を使い分ける TTS(未確認)。台本に役割タグを付けて声を出し分ける発想。

### 6. テスト・実機操作

- [phone-harness](notes/2026-10-09-phone-harness-iphone-control.md):
  - iPhone ミラーリング + OCR で、Claude Code が実機を操作する(MIT、iPhone に何も入れない)。
  - SNS のウォームアップや自動返信は規約違反なので使わない。
- [TouchSynthesis](notes/2026-10-09-iphone-touchsynthesis-agent.md):
  - iPhone 単体で操作する。非公開 API を使い、TCP に認証がない。
- [vphone](notes/2026-10-09-vphone-virtual-iphone.md):
  - Mac 上の脱獄済み仮想 iPhone。研究用。SIP を無効にする必要があり危険。実機の代わりにはならない。

### 7. API・データ・プライバシー

- [OpenPOI API](notes/2026-10-09-openpoi-api.md):
  - 全国約337万件の施設検索。無料・キー不要・MCP 対応。出典表示が必須。
  - 位置情報を送るならプライバシーポリシーを更新する。
- [DeepFace](notes/2026-10-09-deepface-face-recognition.md):
  - 顔認識ライブラリ。顔データは個人識別符号にあたる。ログインには Face ID、検出には Vision を使う。人種・感情の推定は製品に入れない。

## プライバシーポリシー(`index.html`)の更新が必要になる場面

アプリに次の機能を入れるときは、ポリシーの「3. 外部サービスへの提供」と、App Store のプライバシー表示を更新する。

- 位置情報の利用(例: OpenPOI API)
- AI サービスへのデータ送信
- 課金(Apple 経由の決済であること)
- 顔データ・音声データの取り扱い
