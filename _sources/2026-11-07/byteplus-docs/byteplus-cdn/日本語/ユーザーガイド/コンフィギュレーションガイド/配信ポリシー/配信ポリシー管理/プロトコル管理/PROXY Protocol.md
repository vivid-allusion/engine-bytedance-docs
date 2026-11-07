---
title: "PROXY Protocol"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/proxy-protocol_jp"
---

**背景**

PROXY プロトコルは、プロキシ環境でサーバーがクライアントの実際の情報を取得できないという問題を解決するために設計されたネットワークプロトコルです。この情報には、クライアントの IP アドレスとポート、およびクライアントがアクセスする必要のある宛先 IP アドレスとポートが含まれます。サーバーとの TCP/UDP 接続を確立する際、プロキシサーバーは PROXY プロトコルヘッダーを送信して、クライアントの実際の情報を転送します。

**機能紹介**

BytePlus CDN は、バージョン 1 とバージョン 2 の両方の PROXY プロトコルをサポートしています。CDN で PROXY プロトコルを有効にすると、CDN は受信した PROXY プロトコルヘッダーを解析して、クライアントの実際の IP アドレスを取得できます。

 **ユースケース** 

ビジネスアーキテクチャでは、BytePlus Global Accelerator（GA）などのプロキシが CDN の前に展開されており、このプロキシは PROXY プロトコルヘッダーを送信します。また、IP アドレスに基づいて CDN へのアクセスを制御するために、IP アローリスト/ブロックリストも設定しています。

**手順**


1. **Proxy Protocol** 設定ページを開きます。操作手順については、[ドメイン名設定](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_jp) を参照してください。

2.  **ステータス**  を有効に設定します。

3. 設定が完了したら、**保存** をクリックします。


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_1470e115d5bb455adc70c3eb955d1a80.jpg) </span>
