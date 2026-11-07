---
title: "HTTP/3 (QUIC)"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/quic-jp"
---

本ドキュメントでは、BytePlus CDNのHTTP/3およびQUICプロトコルのサポートについて説明します。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">プロトコルのメカニズムが異なるため、HTTP/3（QUIC）と WebSocket を同時に有効にすることはできません。</div>


<span id="概要"></span>
## 概要

CDNがサポートするQUICプロトコルには以下が含まれます：


* Google QUIC (gQUIC)：サポートされるgQUICのバージョンはQ043、Q046、Q050です。

* IETF QUIC：IETF QUICはHTTP/3が使用する転送層プロトコルです。


以上より、CDNはHTTP/3および特定バージョンのgQUICをサポートしています。

CDNでは、"HTTP/3 (QUIC)"機能を有効にすることができます。この機能を有効にすると、CDNは上記のプロトコルを使用するユーザーからのリクエストを処理できるようになります。

<span id="http-3の紹介"></span>
## HTTP/3の紹介

HTTP/3はIETF QUICに基づいており、HTTPプロトコルの最新バージョンです。以下の利点があります：


* **低遅延**：QUICは鍵交換とサポートされるプロトコルを初期ハンドシェイクプロセスの一部としています。サーバーがクライアントの接続に応答する際、応答パケットにはデータ暗号化に必要なデータが含まれています。クライアントはこのデータを使用して、送信するパケットを暗号化するための鍵を生成できます。HTTPS接続を確立する際、クライアントとサーバーはまずTCPハンドシェイクを行い、その後TLSハンドシェイクを行って安全な接続を確立する必要があります。

*  **ネットワーク切り替え時のパフォーマンスが優れている** ：QUICにはコネクション識別子が含まれています。この識別子は、クライアントとサーバー間の接続を一意に識別します。クライアントのIPアドレスが変更された場合でも、クライアントはこのIDを含むパケットを送信するだけでサーバーとの接続を確立できます。TCPの場合、クライアントのIPアドレスが変更されると、既存のTCP接続はタイムアウトします。その後、クライアントはサーバーとの接続を再確立するために冗長なプロセスを経なければなりません。

*  **ネットワークの通信速度が遅い場合のパフォーマンスが良好**：QUICはUDPベースです。パケットロスやネットワーク遅延が深刻な状況でも、QUICはサービスの可用性を確保できます。


<span id="前提条件"></span>
## 前提条件

この設定を有効にするには、ドメイン名ですでにHTTPS暗号化サービスが有効になっていることが必要です。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">注意すべき点として、プロトコルのメカニズムが異なるため、ドメイン名ですでにWebsocketが有効になっている場合、そのドメイン名で"HTTP/3 (QUIC)"を有効にすることはできません。</div>


<span id="操作手順"></span>
### 操作手順


1. **HTTP/3 (QUIC)**  設定ペイジを開きます。操作手順については[ドメイン名設定](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_jp)をご参照ください。

2. **HTTP/3 (QUIC)**  の下で、**状態**を**有効**に設定します。

3. 設定が完了したら、**保存**をクリックします。

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_da64e62fd0b1dd629de1616d36f106b1.png) </span>
