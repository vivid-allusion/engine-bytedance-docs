---
title: "HTTP/2"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/http2-jp"
---

本ドキュメントでは、BytePlus CDNにおけるHTTP/2プロトコルのサポートについて説明します。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">プロトコルのメカニズムが異なるため、HTTP/2とWebSocketを同時に有効にすることはできません。</div>


<span id="前提条件"></span>
### 前提条件

この設定を有効にするには、ドメインでHTTPS暗号化サービスが有効になっている必要があります。

<span id="http-2とは"></span>
## HTTP/2とは

HTTP/2はHTTP/1.xの機能を拡張したものです。HTTP/1.xと互換性があり、さらにバイナリフレーミングレイヤー、ヘッダー圧縮、多重化、サーバープッシュなどの機能が追加されています。

HTTP/2はウェブサイトにHTTPSの使用を強制しませんが、主要なブラウザのHTTP/2サポートはSSL/TLSに基づいて実装されています。現在、HTTP/2を使用しているウェブサイトはすべてHTTPSを有効にしています。

<span id="操作手順"></span>
## 操作手順


1. **HTTP/2**設定ペイジを開きます。操作手順については[ドメイン名設定](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_jp)をご参照ください。

2. **HTTP/2**の下で、**状態**を**有効**に設定します。

3. 設定が完了したら、**保存**をクリックします。


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_c9fa42621d4263ffd2d5241f85e7de5d.jpeg) </span>
