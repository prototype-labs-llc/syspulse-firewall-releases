# SysPulse Firewall

macOS のメニューバーで使える、シンプルな無料のファイアウォールです。受信・送信のブロックをワンクリックで切り替えられます。

## 主な機能

- **受信をブロック** — カフェの Wi-Fi などで、ほかの端末から始まる接続を止めます。自分から始めた通信への返事はそのまま届きます。
  - **近くの Apple 機器を許可** — ブロック中も AirDrop や AirPlay を使えるようにします。
- **送信をブロック** — すべてのインターネット通信を止める緊急用のスイッチです。
- **状態表示** — ブロックが実際に効いているか、この1時間で何台が接続を試みたかが一目で分かります。
- **ブロックした通信** — 「接続の試み」「自分の接続の名残」「全員あて」を見分け、相手やサービス名（例 `:7000 AirPlay`）も表示します。
- **ネットワーク情報**、**開いているポート**、**通信中のアプリ**の一覧。通信は見るだけで、記録や外部への送信はしません。
- **自動アップデート** — 新しい版が出ると、ワンクリックで更新できます（確認するかどうかは初回に選べます）。

## 動作環境

macOS 14 以降。Apple Silicon / Intel 対応。Developer ID 署名・公証済み。

## インストール

1. [Releases](https://github.com/prototype-labs-llc/syspulse-firewall-releases/releases/latest) から `SysPulse-Firewall-<バージョン>.dmg` をダウンロードします。
2. dmg を開き、SysPulse Firewall を「アプリケーション」フォルダへドラッグします。
3. 起動したら、**システム設定 › 一般 › ログイン項目と機能拡張** で SysPulse Firewall のバックグラウンド実行を許可します。
4. 通信中のアプリを表示するには、パネルの案内に従ってネットワーク機能拡張とコンテンツフィルタを許可します（ブロックだけならこの許可は不要です）。

## アップデート

パネル下部の「アップデートを確認…」、または自動確認（1日1回）で新しい版が見つかると、更新の画面が開きます。0.2.0 から更新した場合だけ、更新後に Mac を一度再起動してください。

## 緊急時の解除

SysPulse Firewall が動かず、ネットワークにもつながらない場合は、SysPulse Firewall を終了してからターミナルで**次の順に**実行してください。

```sh
sudo launchctl bootout system/net.prototype-labs.syspulse.firewall.helper   # 先にバックグラウンドサービスを止める（止めないとルールが戻されます）
sudo rm -f "/Library/Application Support/SysPulse Firewall/state.json"      # 保存された設定を消し、再起動後にブロックしないようにする
sudo pfctl -a com.apple/300.syspulse.firewall -F all                         # SysPulse Firewall のルールを消す
```

macOS 自身のファイアウォール設定は変わりません。

## 利用条件

無料でお使いいただけます。再配布・改変は禁止です。詳しくは [LICENSE.md](LICENSE.md) をご覧ください。

このリポジトリはアプリの配布専用です。ソースコードは公開していません。

© 2026 PROTOTYPE LABS, LLC
