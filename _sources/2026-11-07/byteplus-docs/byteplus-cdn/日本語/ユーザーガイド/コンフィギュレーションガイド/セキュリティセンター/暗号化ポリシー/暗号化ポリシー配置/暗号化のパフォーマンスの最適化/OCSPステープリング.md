---
title: "OCSPステープリング"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/ocsp-staping-jp"
---

本ドキュメントでは、BytePlus CDNが提供する「OCSPステープリング」機能について説明します。

<span id="ocspステープリングとは"></span>
## OCSPステープリングとは

OCSPは、オンライン証明書状態プロトコル（Online Certificate Status Protocol）の略称です。TLSハンドシェイクの段階で、クライアントは証明書を取得した後、その証明書のCA機関に証明書の状態を問い合わせます。CA機関はクライアントにOCSPレスポンスを送信します。

クライアントが証明書を取得するとすぐにCA機関に証明書の状態を問い合わせるため、CA機関に大量の問い合わせリクエストが発生しやすくなります。CA機関の応答が遅い場合、TLSハンドシェイクの時間が増加します。この問題を回避するために、OCSPステープリングが生まれました。OCSPステープリングでは、サーバーが定期的にCA機関に証明書の状態を問い合わせ、その状態をサーバーにキャッシュすることができます。サーバーがクライアントに証明書を送信する際、その証明書のOCSPレスポンスも一緒に送信します。OCSPレスポンスはCA機関によって署名されているため、偽造が困難です。

<span id="ocspステープリングの長所と短所"></span>
## OCSPステープリングの長所と短所

OCSPステープリングは、クライアントからCA機関への問い合わせリクエストを大幅に減少させ、TLSハンドシェイクの時間も短縮します。短所としては、クライアントが取得する証明書の状態が最新でない可能性があることです。ただし、サーバーがCA機関に証明書を問い合わせる間隔を設定することで、この短所の影響を軽減することができます。

<span id="ocspステープリングの有効化"></span>
## OCSPステープリングの有効化

BytePlus CDNは「OCSPステープリング」機能を提供しており、TLSハンドシェイクの効率を向上させ、ユーザーエクスペリエンスを改善することができます。

<span id="前提条件"></span>
### 前提条件

この設定を有効にするには、ドメイン名がすでにHTTPS暗号化サービスを有効にしている必要があります。

<span id="操作手順"></span>
## 操作手順


1. **OCSPステープリング**  設定ペイジを開きます。操作手順については[ドメイン名設定](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_jp)をご参照ください。

2. **OCSPステープリング** の下で、**状態**を**有効**に設定します。

3. 設定が完了したら、**保存**をクリックします。


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_4fc34f910bfd16d9833d62731de6e418.jpeg) </span>
