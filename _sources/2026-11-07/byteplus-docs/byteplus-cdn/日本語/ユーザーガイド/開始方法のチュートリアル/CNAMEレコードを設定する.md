---
title: "CNAMEレコードを設定する"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/create_cname_record"
---

このドキュメントでは、CNAMEレコードを設定してサイトをBytePlus CDNに接続する方法について説明します。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">このドキュメントは、<a href="https://docs.byteplus.com/en/docs/byteplus-cdn/quickstart-overview">チュートリアルの概要</a>で説明されているシナリオに基づいています。</div>


サイトをCDNに接続するには、DNSサービスプロバイダーでCNAMEレコードを設定する必要があります。レコード名は`www`で、レコード値は`www.example.com.bplslb.com`です。ドメイン名サービスプロバイダーによって設定インターフェースが異なります。以下では、主にBytePlus DNS SuiteとGoDaddyでの設定方法を紹介します。


* [BytePlus DNS Suite](https://docs.byteplus.com/en/docs/18/31759#byteplus-dns-suite)

* [GoDaddy](https://docs.byteplus.com/en/docs/18/31759#godaddy)


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">DNSサービスプロバイダーのインターフェースが変更される可能性があるため、実際のインターフェースを参照してください。</div>


* <div data-tips="true" data-tips-type="tip">CNAME設定完了後、<a href="https://docs.byteplus.com/en/docs/18/31759#cname-%E3%83%AC%E3%82%B3%E3%83%BC%E3%83%89%E3%81%8C%E6%9C%89%E5%8A%B9%E3%81%AB%E3%81%AA%E3%81%A3%E3%81%A6%E3%81%84%E3%82%8B%E3%81%8B%E7%A2%BA%E8%AA%8D%E3%81%99%E3%82%8B">CNAMEの設定が有効になっているか確認</a>してください。</div>



<span id="byteplus-dns-suite"></span>
## BytePlus DNS Suite


1. [BytePlus DNS Suite コンソール](https://console.byteplus.com/dns-suite/dns/publiczone/zones)にログインします。

2. **Domain management**ページのドメインリストで、`example.com`ドメインを見つけます。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3eab5b722afa4136b5f584c3e7d40b77~tplv-goo7wpa0wc-image.image) </span>

3. **Operation**列で、**Manage**をクリックします。

4. **Record management**タブで、**Create record set**をクリックします。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/de120a8606d544828808daf656dd3ef2~tplv-goo7wpa0wc-image.image) </span>

5. **Create record set**ページで、以下のスクリーンショットに従ってCNAMEレコードを設定します。

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_9493a59303e3414db75530f40e7cf34c.png) </span>

6. 設定が完了したら、**Submit**をクリックします。


<span id="godaddy"></span>
## GoDaddy


1. [GoDaddyサイトのMy Products ページ](https://account.godaddy.com/products)を開き、ログインします。

2. **Domains**の下で、**example.com**ドメインを見つけ、**DNS**をクリックします。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bfa5845daef0412e96267c778c27d023~tplv-goo7wpa0wc-image.image) </span>

3. **DNS Management**ページで、**Add New Record**をクリックします。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c5159b53e6844d1786fda6958d050c9d~tplv-goo7wpa0wc-image.image) </span>

4. 以下のスクリーンショットに従ってCNAMEレコードを設定します。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ebeda555ac1948d29dd0109c1a0092b1~tplv-goo7wpa0wc-image.image) </span>

5. 設定が完了したら、**Save**をクリックします。


<span id="cnameレコードが有効になっているか確認する"></span>
## CNAMEレコードが有効になっているか確認する

DNSサービスプロバイダーでCNAMEレコードを設定した後、3分待ってから、以下のいずれかの方法で設定したCNAMEレコードが有効になっているか確認してください。

<span id="方法1：cdnコンソールでcnameレコードのステータスを確認する"></span>
### 方法1：CDNコンソールでCNAMEレコードのステータスを確認する

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">DNSサービスプロバイダーが通信事業者の回線や地域などの次元に基づいてDNSレコードの設定をサポートしており、設定したCNAMEレコードが特定の次元に基づいている場合、方法1ではCNAMEレコードの実際のステータスを取得できない可能性があります。方法2を使用することをお勧めします。</div>


[ドメイン名](https://console.byteplus.com/cdn/cdn-bp/delivery-network/domain-access)ページを再度開くか更新します。CNAMEの前にオレンジ色の感嘆符がある場合、設定したCNAMEレコードはまだ有効になっていません。DNSサービスプロバイダーで設定したCNAMEレコードが正しいか確認してください。

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_042a56c5a25430c4de4bc1310e7e9afc.jpeg) </span>

CNAMEの前に緑色の感嘆符がある場合、設定したCNAMEレコードは有効になっています。

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_41dbcf30740a5f89ab5e3f06ca85d8b8.jpeg) </span>

<span id="方法2：コマンドラインツールを使用してcnameレコードのステータスを確認する"></span>
### 方法2：コマンドラインツールを使用してCNAMEレコードのステータスを確認する

使用しているオペレーティングシステムに応じて、以下の手順を参照してください。

<span id="macosとlinux"></span>
#### macOSとLinux


1. ターミナルウィンドウで、`dig www.example.com`コマンドを実行します。

2. **ANSWER SECTION**の下に以下の情報が表示される場合、設定したCNAMEが有効になっています。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/02ff456e965346898264764b51476c48~tplv-goo7wpa0wc-image.image) </span>


<span id="windows"></span>
#### Windows


1.  **コマンドプロンプト** ウィンドウで、`nslookup www.example.com`コマンドを実行します。

2. コマンドの下の情報に以下の情報が表示される場合、設定したCNAMEが有効になっています。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a5f3ec2e12c648efabe5969842cce83a~tplv-goo7wpa0wc-image.image) </span>
