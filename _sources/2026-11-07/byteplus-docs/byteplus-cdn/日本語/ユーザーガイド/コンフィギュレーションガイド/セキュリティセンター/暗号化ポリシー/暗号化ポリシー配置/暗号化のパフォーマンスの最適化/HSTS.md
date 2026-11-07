---
title: "HSTS"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/HSTS-jp"
---

本ドキュメントでは、BytePlus CDNでドメインにHSTSを有効にする方法について説明します。

<span id="hstsの概要"></span>
## HSTSの概要

HSTSは、HTTP Strict Transport Securityの略称で、ネットワークセキュリティのポリシーメカニズムです。HSTSの目的は、ユーザーがHTTPSサイトにアクセスする際にダウングレード攻撃やクッキーハイジャックから保護することです。サイトでHSTSを有効にすると、サイトのレスポンスに`Strict-Transport-Security`レスポンスヘッダーが含まれます。`Strict-Transport-Security`レスポンスヘッダーは、ブラウザにサイトへのすべてのリクエストがHTTPSプロトコルを使用しなければならないことを通知します。

`Strict-Transport-Security`レスポンスヘッダーには2つのパラメータも含まれています。これらのパラメータについての説明は、[設定説明](https://docs.byteplus.com/en/docs/18/32190#734701ec)を参照してください。

<span id="hstsと「httpからhttpsへのリダイレクト」"></span>
## HSTSと「HTTPからHTTPSへのリダイレクト」

CDN が提供する「HTTPとHTTPS間のリダイレクト」機能には、「HTTPからHTTPSへのリダイレクト」という設定（以下「HTTPSへのリダイレクト」と呼びます）があります。この設定の目的は、CDN が受信したHTTPリクエストをHTTPSリクエストにリダイレクトすることです。

HSTSについてさらに説明する前に、HSTSと「HTTPSへのリダイレクト」の違いを説明する必要があります。

HTTPは安全でないプロトコルです。ユーザーがブラウザでHTTPプロトコルを指定してサイトにリクエストを送信すると、そのリクエストが傍受され、悪意のあるサイトにリダイレクトされる可能性があります。HTTPリクエストがドメイン名にアクセスするのを避けるために、CDNは以下の2つの設定を提供しています：


* 「HTTPとHTTPS間のリダイレクト」：「HTTPとHTTPS間のリダイレクト」を有効にした後、 **ポリシー** を**HTTPからHTTPSへのリダイレクト** に設定する必要があります。

* HSTS。


<span id="httpsへのリダイレクトの制限"></span>
### HTTPSへのリダイレクトの制限

HTTPSへのリダイレクトを設定した後、ブラウザがCDNにHTTPリクエストを送信した場合、CDNは301または302レスポンスステータスコードを返し、ブラウザにHTTPリクエストをHTTPSリクエストにリダイレクトするよう通知します。HTTPSへのリダイレクトの詳細については、[HTTPとHTTPS間のリダイレクト](https://docs.byteplus.com/en/docs/byteplus-cdn/protocol-redirect-jp)を参照してください。

ただし、HTTPSへのリダイレクトを設定しても、ユーザーはブラウザでHTTPプロトコルを指定してCDNにHTTPリクエストを送信することができます。HTTPSリクエストにリダイレクトされますが、これらのHTTPリクエストはCDNに到達する前に傍受されるリスクがあります。

<span id="hstsの利点"></span>
### HSTSの利点

HTTPSへのリダイレクトと比較して、HSTSはより安全なソリューションを提供します。ドメイン名でHSTSを有効にすると、CDNのレスポンスに`Strict-Transport-Security`レスポンスヘッダーが含まれます。ブラウザがHTTPSプロトコルを使用してCDNに1回リクエストを送信することに成功すると、ブラウザはそのレスポンスヘッダーをキャッシュします。その後、ユーザーがブラウザでHTTPプロトコルを指定してCDNにアクセスしようとしても、リクエストを送信する前に、ブラウザがHTTPをHTTPSに変換します。この変換プロセスがブラウザ側で行われるため、ブラウザからCDNに送信されるHTTPリクエストの数を大幅に減少させることができます。同時に、HTTPリクエストが傍受されるリスクも低減されます。

<span id="hstsレスポンスヘッダーが機能するための前提条件"></span>
#### HSTSレスポンスヘッダーが機能するための前提条件

HSTSソリューションはより安全ですが、ブラウザが`Strict-Transport-Security`レスポンスヘッダーに従ってHTTPをHTTPSに変換するためには、以下の条件が満たされている必要があります：


* ブラウザが`Strict-Transport-Security`レスポンスヘッダーをキャッシュしていること。

* キャッシュされたレスポンスヘッダーが期限切れでないこと。`Strict-Transport-Security`レスポンスヘッダーのキャッシュ有効期間については、[設定説明](https://docs.byteplus.com/en/docs/18/32190#%E8%A8%AD%E5%AE%9A%E8%AA%AC%E6%98%8E)を参照してください。


ドメイン名でHSTSを有効にすると、CDNはすべてのリクエストに対して`Strict-Transport-Security`レスポンスヘッダーを返します。ただし、ブラウザがこのレスポンスヘッダーをキャッシュするためには、ブラウザがHTTPSプロトコルを使用してCDNに1回リクエストを送信することに成功している必要があります。したがって、HSTSを有効にする際は、「HTTPとHTTPS間のリダイレクト」も有効にし、 **リダイレクトの種類**を**HTTPからHTTPSへリダイレクト** に設定することをお勧めします。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">CDNコンソールでHSTSを有効にすると、CDNはHTTPSへのリダイレクトの設定を有効にする必要があるかどうかを提案します。<a href="https://docs.byteplus.com/en/docs/18/32190#%E6%93%8D%E4%BD%9C%E6%89%8B%E9%A0%86">操作手順</a>を参照してください。</div>


<span id="ブラウザとcdnの相互作用プロセス"></span>
#### ブラウザとCDNの相互作用プロセス

HSTSとHTTPSへのリダイレクトを有効にした後、ユーザーがブラウザを使用してCDNにHTTPリクエストを送信した場合、ブラウザとCDNの相互作用プロセスは以下のようになります：


1. ブラウザは、キャッシュされた`Strict-Transport-Security`レスポンスヘッダーが存在するかどうかをチェックします。

2. ブラウザのキャッシュにこのレスポンスヘッダーが存在しないため、ブラウザはCDNにそのHTTPリクエストを送信します。

3. CDNがこのリクエストを受信すると、HTTPSへのリダイレクトの設定により、CDNのレスポンスステータスコードは301または302になります。同時に、HSTSの設定により、レスポンスには`Strict-Transport-Security`レスポンスヘッダーが含まれます。この時点では、まだHTTPSプロトコルを使用してCDNに1回リクエストを送信することに成功していないため、ブラウザはこのレスポンスヘッダーをキャッシュしません。

4. 301または302レスポンスステータスコードにより、ブラウザはCDNにHTTPSリクエストを送信します。レスポンスでは、CDNは同様に`Strict-Transport-Security`レスポンスヘッダーを含めます。このレスポンスヘッダーの有効期間が10分であると仮定し、このHTTPSリクエストが要求されたファイルの取得に成功したとします。

5. HTTPSリクエストが成功したため、ブラウザは`Strict-Transport-Security`レスポンスヘッダーをキャッシュします。


10分以内に、同じユーザーがブラウザを使用してCDNに再度HTTPリクエストを送信したとします。この時、ブラウザとCDNの相互作用プロセスは以下のようになります：


1. ブラウザは、キャッシュされた`Strict-Transport-Security`レスポンスヘッダーが存在するかどうかをチェックします。

2. ブラウザのキャッシュにこのレスポンスヘッダーが存在するため、ブラウザはこのレスポンスヘッダーが期限切れかどうかをチェックします。

3. このレスポンスヘッダーが期限切れでないため、ブラウザはHTTPをHTTPSに変換し、そのリクエストをCDNに送信します。


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">キャッシュされた<code>Strict-Transport-Security</code>レスポンスヘッダーが期限切れの場合、そのユーザーがCDNにHTTPリクエストを送信すると、<a href="https://docs.byteplus.com/en/docs/18/32190#%E3%83%96%E3%83%A9%E3%82%A6%E3%82%B6%E3%81%A8CDN%E3%81%AE%E7%9B%B8%E4%BA%92%E4%BD%9C%E7%94%A8%E3%83%97%E3%83%AD%E3%82%BB%E3%82%B9">ブラウザとCDNの相互作用プロセス</a>で説明されたステップが繰り返されます。</div>


* <div data-tips="true" data-tips-type="warning">注意すべき点は、HSTSとHTTPSへのリダイレクトを有効にしても、CDNが受信するHTTPリクエストを完全に排除することはできないということです。以下のいずれかの状況では、ブラウザはHTTPをHTTPSに変換しません：</div>


   * <div data-tips="true" data-tips-type="warning">ブラウザのキャッシュに<code>Strict-Transport-Security</code>レスポンスヘッダーが存在しない場合。</div>


   * <div data-tips="true" data-tips-type="warning">ブラウザのキャッシュにある<code>Strict-Transport-Security</code>レスポンスヘッダーが期限切れの場合。</div>



<span id="前提条件"></span>
### 前提条件

この設定を有効にするには、ドメイン名がすでにHTTPS暗号化サービスを有効にしている必要があります。

<span id="操作手順"></span>
## 操作手順


1. **HSTS** 設定ペイジを開きます。操作手順については[ドメイン名設定](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_jp)をご参照ください。

2. **HSTS**の下で、**状態**を**有効**に設定します。

   この時点で、まだ「HTTPとHTTPS間のリダイレクト」を有効にしていない場合、または既に「HTTPとHTTPS間のリダイレクト」を有効にしているものの、 **ポリシー** が**HTTPからHTTPSへのリダイレクト** になっていない場合、CDNはHTTPSへのリダイレクトを設定するかどうかを確認します。その理由については、「HSTS応答ヘッダーが機能するための前提条件」を参照してください。

   * **確認**をクリックすると、CDNはHTTPSへのリダイレクトを設定します。**確認**をクリックする前に、HTTPSへのリダイレクトの設定があなたのビジネスに与える影響を十分に評価してください。

   *  **キャンセル** をクリックすると、CDNは現在の「HTTPとHTTPS間のリダイレクト」の設定を維持します。

3. 以下の設定説明を参照してください。


<span id="設定説明"></span>
### 設定説明


|**設定** |**説明** |
|---|---|
|有効期間 |`Strict-Transport-Security`レスポンスヘッダーがクライアントブラウザでキャッシュされる有効期間を表します。この設定は`Strict-Transport-Security`レスポンスヘッダーの`max-age`パラメータに対応します。HTTPリクエストを送信する前に、ブラウザはキャッシュされた`Strict-Transport-Security`レスポンスヘッダーが期限切れかどうかをチェックします。このレスポンスヘッダーが期限切れの場合、ブラウザはHTTPをHTTPSに変換しません。<br><br>設定できる最長時間は31,536,000秒で、365日を表します。有効期間を`0`に設定すると、HSTSを無効にするのと同じ効果があります。<br><br>&nbsp;<br><br>注意すべき点は、ブラウザが受信する各レスポンスについて、レスポンスに`Strict-Transport-Security`レスポンスヘッダーが含まれている場合、ブラウザは受信したレスポンスヘッダーの有効期間を使用して、キャッシュされたレスポンスヘッダーの有効期間を置き換えることです。 |
|サブドメイン |HSTS設定がサブドメインサイトに適用されるかどうかを表します。この設定には以下のオプションがあります：<br><br><br>*  **いいえ** ：HSTS設定がサブドメインサイトに適用されないことを表します。<br><br>*  **はい** ：HSTS設定がサブドメインサイトに適用されることを表します。この場合、レスポンスヘッダーに`includeSubDomains`パラメータが含まれます。<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning"><strong>サブドメインを含めますか</strong>を<strong>はい</strong>に設定すると、CDNが返すレスポンスヘッダーは、ブラウザにすべてのサブドメインへのリクエストもHTTPSプロトコルを使用しなければならないことを通知します。この場合、サブドメインサイトがHTTPSプロトコルでアクセス可能であることを確認してください。また、サブドメインにもサブドメインのHTTPリクエストをHTTPSリクエストに「HTTPからHTTPSへのリダイレクト」する同様の設定が必要です。</div><br> |


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_46beb707af9555545ff1d7687e5f1493.jpeg) </span>

**例**


* 例1：有効期間を6秒に指定し、サブドメインを含む場合。この場合、CDNが実際に返すレスポンスヘッダーは以下のようになります：

   * `Strict-Transport-Security: max-age=6;includeSubDomains`

* 例2：有効期間を1日に指定し、サブドメインを含まない場合。この場合、CDNが実際に返すレスポンスヘッダーは以下のようになります：

   * `Strict-Transport-Security: max-age=86400`


<span id="追加情報"></span>
## 追加情報

<span id="ブラウザでhsts設定を管理する方法"></span>
### ブラウザでHSTS設定を管理する方法

以下では、Google ChromeとMicrosoft Edgeを例に、ブラウザでHSTS設定を管理する方法を説明します。

ChromeまたはEdgeで、以下のURLにアクセスします：


* `chrome://net-internals/#hsts`


開いたページで、以下のことができます：


* ドメインをブラウザのHSTSキャッシュに追加する。

* ブラウザのHSTSキャッシュから指定したドメインを削除する。

* ドメインがブラウザのHSTSキャッシュに存在するかどうかを確認する。

   * そのドメインが存在しない場合、クエリ結果は`Not found`となります。

   * そのドメインが存在する場合、クエリ結果にはそのドメインのHSTS設定情報が表示されます。設定情報の中で、`dynamic_sts_observed`はブラウザがそのドメインをキャッシュした時間を表し、時間形式はUnixタイムスタンプです。`dynamic_sts_expiry`はそのドメインがHSTSキャッシュで期限切れになる時間を表します。


ドメインを確認する際、結果データに1分程度の遅延が生じる可能性があります。

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_bceca7d3f4666d763c878521f8ae8164.png) </span>
