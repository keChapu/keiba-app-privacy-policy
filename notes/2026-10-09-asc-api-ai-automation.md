# App Store Connect API + AI でストア作業を自動化

- 出典: X(Twitter)の投稿(ユーザーが本文を共有。投稿URLは未記録)
- 参考リンク: https://developer.apple.com/app-store-connect/api/
- 保存日: 2026-10-09
- タグ: #自動化 #ASO #AppStoreConnect #ClaudeCode

## 要点

- **App Store Connect API + Claude Code** で、ストア画像(スクリーンショット)をダウンロード → 編集 → 再登録できた。
- **App Store Connect + ChatGPT** で、アップデート時の「このバージョンの新機能」の文章を作って追加できた。
- APIを使うと手作業より圧倒的に速い。
- 仕組み:
  - App Store Connect の「ユーザとアクセス → 統合 → App Store Connect API」で **APIキー(.p8)** を発行し、手元のMacに置く。
  - そのキーで動くCLI **`asc`** を、Claude Code に実行させる。
  - Apple IDのログイン情報は渡さない。画面操作(ブラウザ自動化)でもない。
  - Apple公式APIなので、画像の登録から反映後の読み戻し確認までコマンドで完結する。
- 安心できる点: キーは**権限(ロール)を絞れる**。**いつでも無効化(Revoke)できる**。

## このアプリ(競馬アプリ)での活かし方

- スクショの差し替え(レース時期・新機能に合わせた更新)をコマンドで一括実行。
- リリースノートをAIに下書きさせ、CLIで各ローカライズに反映。
- 審査提出前のメタデータ(説明文・キーワード・サポートURL・プライバシーポリシーURL)をコマンドで確認。
  例: このリポジトリの `index.html` と `support.html` のURLが正しく登録されているか確かめる。

## 導入時の注意点

- **`asc` という名前のCLIは複数ある**(2026-10時点の検索結果。どれを使うか要確認)。
  - rorkai/app-store-connect-cli (`brew install asc`)。AI向けの Agent Skills も別リポジトリで公開されている。
  - keremerkan/asc-cli (Swift製。`asc configure` でKey ID / Issuer ID / .p8パスを設定)
  - tddworks/asc-cli、ehmo/App-Store-Connect-CLI など
  - 同じ `asc` コマンド名で衝突しうるので、入れるのは1つにする。
- APIキーの扱い:
  - .p8 は一度しかダウンロードできない。Git管理下に置かない(`.gitignore` / リポジトリ外に保存)。
  - ロールは必要最小限にする(例: メタデータ・画像編集だけなら App Manager 相当。Admin は避ける)。
  - 使わなくなったらすぐ Revoke する。
- AIに実行させるときは、提出(submit)や公開など**取り消しにくい操作は人間が確認してから**実行させる。
