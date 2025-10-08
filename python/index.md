# TAKAYA RFID リーダライタ Python サンプルプログラム

このページでは、タカヤ製RFIDリーダライタをPythonで制御するためのサンプルプログラムを紹介します。これらのサンプルは、TR3シリーズおよびUTRシリーズのリーダライタに対応し、USBまたはLAN接続を通じてデバイスとの通信を行います。

各サンプルプログラムは、特定のデバイスと接続方法に特化しており、基本的な読み取り操作やデバイス設定のデモンストレーションを提供します。開発者はこれらのサンプルを基に、独自のRFIDアプリケーションを構築することができます。

## サンプルプログラム一覧

以下の表に、提供されているPythonサンプルプログラムの概要をまとめます。

| リポジトリ名 | 対象デバイス | 接続タイプ | 概要 | 主な機能 | 動作環境 |
|---|---|---|---|---|---|
| [TR3_LAN_Python](https://github.com/TamaruNorio/TR3_LAN_Python) | TR3XMシリーズ (HF帯) | LAN (TCP/IP) | TR3XMシリーズをLAN経由で制御する最小サンプル。安定した受信パースと典型フローを学ぶことを目的としています。 | ROMバージョン確認、コマンドモード切替、アンチコリジョン設定、アンテナ切替、Inventory2 (タグ読取)、ブザー制御、ログ出力 | Windows 10以降、Python 3.9+ (標準ライブラリのみ) |
| [TR3_USB_Python](https://github.com/TamaruNorio/TR3_USB_Python) | TR3シリーズ (HF帯) | USB (仮想COM) | TR3シリーズをUSBシリアル接続で制御するPythonサンプル。 | ROMバージョン確認、コマンドモード切替、Inventory2 (タグ読取)、ブザー制御 | Windows 10/11、Python 3.8+、pyserial |
| [UTR_LAN_Python](https://github.com/TamaruNorio/UTR_LAN_Python) | UTR-S201シリーズ (UHF帯) | LAN (TCP) | UTR-S201シリーズをLAN経由で制御するサンプル。USB版の構造を踏襲し、通信層のみTCPに置き換えられています。 | ROMバージョン確認、コマンドモード切替、送信出力値/周波数チャンネル取得、Inventory (タグ読取)、RSSI/PC+UII抽出、ブザー制御、ログ保存 | Windows 10/11、Python 3.10+ (標準ライブラリのみ) |
| [UTR_USB_Python](https://github.com/TamaruNorio/UTR_USB_Python) | UTR-S201/202シリーズ (UHF帯) | USB (仮想COM) | UTR-S201/202シリーズをUSBシリアル接続で制御するPythonサンプル。 | タグ読取結果のコンソール表示 | Windows 10/11、Python 3.8+、pyserial |

## 共通セットアップと実行方法

ほとんどのPythonサンプルプログラムは、以下の共通手順でセットアップおよび実行が可能です。

1.  **Python環境の準備**: Python 3.8以上（推奨は3.9+または3.10+）がインストールされていることを確認してください。必要に応じて、仮想環境の利用を推奨します。
    ```bash
    python -m venv .venv
    .venv\Scripts\activate
    pip install --upgrade pip
    ```
2.  **リポジトリのクローン**: 各サンプルプログラムのリポジトリをGitHubからクローンします。
    ```bash
    git clone [リポジトリURL]
    cd [リポジトリ名]
    ```
3.  **依存ライブラリのインストール**: `pyserial`が必要なサンプル（TR3_USB_Python, UTR_USB_Python）では、以下のコマンドでインストールします。
    ```bash
    pip install pyserial
    ```
    LAN接続のサンプル（TR3_LAN_Python, UTR_LAN_Python）は、通常、標準ライブラリ（`socket`など）のみを使用するため、追加のインストールは不要です。
4.  **実行**: 各リポジトリの`README.md`に記載されている実行コマンドに従ってプログラムを起動します。多くの場合、`python src/[スクリプト名].py`または`python [スクリプト名].py`の形式です。

## トラブルシューティング

-   **接続できない**: 
    -   IPアドレス、ポート番号、COMポート番号が正しいか確認してください。
    -   LAN接続の場合、ネットワークケーブルの接続、ファイアウォール設定、デバイスがTCPサーバーモードになっているかを確認してください。
    -   USB接続の場合、デバイスマネージャーでCOMポートが認識されているか、他のアプリケーションでポートが占有されていないかを確認してください。
-   **タイムアウトが多い**: 
    -   `timeout`設定を長くしてみてください。特にInventory（タグ読み取り）は時間がかかる場合があります。
    -   ネットワークの混雑状況や、USBケーブルの品質を確認してください。
-   **タグが読めない**: 
    -   リーダライタの出力設定、周波数チャンネル、アンテナ設定を確認してください。
    -   タグの位置、向き、リーダライタとの距離を調整してください。
    -   近傍に金属物や電波干渉源がないか確認してください。

## 参考資料

各サンプルプログラムは、タカヤ製のRFIDリーダライタの通信プロトコル仕様書に基づいて作成されています。詳細な仕様やデバイス設定については、以下の公式資料を参照してください。

-   [タカヤ RFID 製品情報・ユーティリティ](https://www.takaya.co.jp/product/rfid/)
-   [UTRシリーズ 通信プロトコル仕様書](https://www.product.takaya.co.jp/rfid/download/uhf.html)
-   [制御用ソフト開発方法 (TDR-OTH-PROGRAMMING-103)](https://www.takaya.co.jp/product/rfid/)

---
