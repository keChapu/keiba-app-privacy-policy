# ArtCraft / Crafting Apps:Adobe代替のオープンソース制作アプリ群

- 出典: X(Twitter)の投稿(ユーザーが本文を共有。投稿URLは未記録)
- リンク: https://getartcraft.com/apps
- 保存日: 2026-10-09
- タグ: #デザイン #画像編集 #OSS #自動化 #MCP

## 投稿の主張

- 「Adobe崩壊」。Adobeの全ソフトをオープンソースで実装した。
  - ※ 煽り表現。実態は以下のとおり開発初期の段階。

## 確認できたこと(2026-10上旬の報道・検索結果から)

- 開発者は Brandon Thomas。
- 7本のアプリで構成される。すべて Rust でゼロから書かれたネイティブアプリ(Electron不使用)。一部はWebAssemblyでブラウザでも動く。macOS / Windows / Linux 対応。

| アプリ | 相当するAdobe製品 |
| --- | --- |
| PhotoCraft | Photoshop |
| VectorCraft | Illustrator |
| FilmCraft | Premiere |
| LightCraft | Lightroom |
| PrintCraft | Acrobat |
| EffectCraft | After Effects |
| DesignCraft | InDesign |

- **成熟度はまだ低い。**
  - 10/6時点で、アルファ版は PhotoCraft と PrintCraft の2本だけ。残りの5本は開発中。
  - PhotoCraft も、文字組み・ブラシ・プラグイン互換に制限がある。
  - 「1か月でAdobeと100%同等の機能」は開発者本人の目標で、達成されたものではない。
- **AIエージェントからの自動操作に対応**している(CLI / JSON / MCPサーバー)。
- getartcraft.com 本体は、別サービス(AI画像・動画生成)のサイトでもある。そちらはクレジット制の有料プランがある。
- 未確認: この環境からは getartcraft.com に接続できなかった。GitHubリポジトリの場所とライセンスもまだ見ていない。

## このアプリ(競馬アプリ)での活かし方

- **ストア画像の編集を自動化する。** PhotoCraft の CLI / MCP を Claude Code から操作し、スクショに文字や枠を入れる。そのまま `asc` で登録する(App Store Connect API のメモを参照)。
- アイコンやバナーの作成を、Adobeのサブスクなしで済ませられる可能性がある。

## 注意点

- 正式版ではないので、本番の素材作りはしばらく Figma / Canva / Pixelmator などと併用する。
- 使う前に、GitHubのライセンスとMCPサーバーの権限範囲(ファイル操作の範囲)を確認する。
- AI生成の有料サービスと、無料のOSSアプリを混同しない。
