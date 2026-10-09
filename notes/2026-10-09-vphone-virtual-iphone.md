# vphone-aio / vphone-cli:Mac上で動く仮想iPhone(脱獄済み)

- 出典: X(Twitter)の投稿(ユーザーが本文を共有。投稿URLは未記録)
- リポジトリ:
  - https://github.com/34306/vphone-aio(投稿のリンク。最新コミット 1db79dc / 2026-08-27)
  - https://github.com/Lakr233/vphone-cli(作者が推奨する本家。MITライセンス。最新コミット c39628a / 2026-10-09)
- 保存日: 2026-10-09
- タグ: #iOS #仮想化 #テスト #脱獄 #セキュリティ

## 投稿の主張と実態

| 投稿の主張 | 実態(README・リポジトリから確認) |
| --- | --- |
| PCで動く | **Appleシリコン搭載の実機Macのみ**。Windows / Linux PC では動かない。macOS の VM の中でも不可 |
| 開封即脱獄 | vphone-aio は iOS 26.1 の脱獄済み・ブートストラップ入りイメージを丸ごと配布するもの(約12GB、7分割) |
| オープンソース | vphone-aio は配布用スクリプトと**中身の確認できないバイナリ**の組み合わせ。LICENSEなし。本家 vphone-cli はソース公開(MIT) |
| iPhoneを買わなくて済む | 下記のとおり用途が限られる。アプリ開発の実機の代わりにはならない |

- vphone-aio 作者自身が「勝手に拡散された。更新・サポートのある vphone-cli を使って」と書いている。vphone-cli は iOS 27 にも対応。
- 仕組み: Apple の Virtualization.framework と **PCC(Private Cloud Compute)研究用VM** の仕組みを使って iOS を起動する。用途は**セキュリティ研究・リバースエンジニアリング・デバッグ**。

## ホストMacのセキュリティ設定(重要)

- **vphone-aio:**
  - **SIPを無効化**し、`amfi_get_out_of_my_way=1`(コード署名チェックを無効化)する必要がある。
  - Mac全体の防御が大きく下がる。
  - 普段使い・開発用のMacではやるべきでない。
- **vphone-cli:**
  - `csrutil enable --without debug` と `csrutil allow-research-guests enable` を使う。
  - SIPは有効のまま、デバッグ制限だけ緩める方式。vphone-aio よりはまし。
- 必要なもの: ディスク 64GB〜(vphone-aio は 128GB以上推奨)、ネット接続(復元時に署名チケットを取得する)。
- vphone-cli は自動操作API(HTTP / WebSocket、トークン認証、`127.0.0.1` 限定で起動可)と、Claude Code 向けの Skill を同梱している。

## このアプリ(競馬アプリ)開発での位置づけ

- **実機iPhoneの代わりにはならない。** 主な理由:
  - ATTダイアログ、プッシュ通知、課金(StoreKit本番)、App Store / TestFlight の挙動、実際の性能・発熱・通信状況は、実機で確認する必要がある。審査用の動画(`att_confirmation.mp4` など)も実機が無難。
  - 脱獄環境なので、正規端末と挙動が違う可能性がある。
- 普段のUI確認は **Xcode の Simulator で十分**(無料・公式・安全)。
- 使い道があるとすれば、自分のアプリの**セキュリティ確認**くらい。例:
  - 通信内容・保存データが脱獄環境から丸見えにならないか
  - APIキーを端末内に埋め込んでいないか
  - その場合も、作業用の別Macで行う。

## 注意点・リスク

- 12GB の脱獄済みイメージは中身を検証できない。マルウェアが混入していても気づけない。SHA-256 は「壊れていないか」の確認にすぎず、「安全か」の保証にはならない。
- iOS を Apple 純正の実機以外で動かすことは、Apple のソフトウェア使用許諾に抵触する可能性がある。研究目的以外での利用は自己責任。
- Apple ID でのサインインやアプリ購入は、アカウント停止などのリスクがある。避ける。
