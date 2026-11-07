---
title: "WebSocket"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/websocket-jp"
---

本ドキュメントでは、BytePlus CDNにおけるWebSocketのサポートについて説明します。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">プロトコルのメカニズムが異なるため、WebSocket を有効にすると、HTTP/2 および HTTP/3 (QUIC) を有効にできません。同様に、HTTP/2 または HTTP/3 (QUIC) を有効にすると、WebSocket を有効にできません。</div>


<span id="websocketの概要"></span>
## WebSocketの概要

WebSocketは、単一のTCP接続上で全二重通信を行うアプリケーション層プロトコルです。クライアントとサーバー間のリアルタイムな双方向通信を可能にし、従来のHTTPリクエスト\-レスポンスモデルとは異なります。

WebSocketは以下の利点を提供します：


1. リアルタイム性：サーバーがクライアントにメッセージをプッシュできるため、クライアントが定期的にサーバーの状態を確認する必要がなく、メッセージの遅延と帯域幅の消費を削減します。

2. 双方向通信：クライアントとサーバーの両方が相手にデータを送信でき、柔軟な対話を実現します。

3. 効率性：不要なHTTPリクエストとレスポンスを削減し、通信効率を向上させます。

4. 永続的な接続：TCP接続が確立された後は維持され、通信のたびに接続を確立するオーバーヘッドを削減します。


WebSocketは、リアルタイムチャット、オンラインゲーム、リアルタイムデータ更新などのシナリオでよく使用されます。WebSocketは、リアルタイム性の要求が高いアプリケーションに効果的なソリューションを提供します。

<span id="cdnのwebsocketサポート"></span>
## CDNのWebSocketサポート

CDNはWebSocketをサポートしています。この機能はデフォルトで無効になっています。クライアントとオリジンサーバー間の双方向通信が必要な場合は、この機能を有効にすることができます。WebSocketが有効になると、クライアントからWebSocketリクエストを受信した場合、CDNはCDNとオリジンサーバー間で低遅延のパブリックネットワークルートを見つけ、オリジンサーバーとWebSocket接続を確立します。その後、クライアント、CDN、オリジンサーバー間で低遅延の双方向通信が可能になります。

CDNとオリジンサーバー間で確立されたWebSocket接続のデフォルトのタイムアウト時間は60秒です。つまり、60秒以内にWebSocket接続上でデータ転送がない場合、CDNはそのWebSocket接続を切断します。WebSocketを有効にする際に、タイムアウト時間を指定することもできます。

<span id="操作手順"></span>
## 操作手順


1. **WebSocket**設定ペイジを開きます。操作手順については[ドメイン名設定](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_jp)をご参照ください。

2. **WebSocket**の下で、**状態**を有効に設定します。

3. **WebSocketタイムアウト時間**を設定します。この設定の単位は秒で、範囲は1\-300、デフォルト値は60です。

4. 設定が完了したら、**保存**をクリックします。


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_6edba3eec54a96da7802c6a127a4b4fa.jpeg) </span>
