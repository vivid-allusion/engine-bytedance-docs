---
title: "署名付きURL認証の概要"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/signed-url-authentication-jp"
---

このドキュメントでは、BytePlus CDNでURLの認証を設定する方法について説明します。

<span id="背景"></span>
## 背景

CDNは、ユーザーリクエストをフィルタリングするために「Referer制限」、「Origin制限」、および「IP制限」を提供しています。しかし、場合によってはReferer、Origin、およびIPが偽装される可能性があり、サイトのコンテンツの悪用につながる可能性があります。サイトのコンテンツに高いセキュリティ要件がある場合は、URL認証を使用できます。

<span id="動作原理"></span>
## 動作原理

ユーザーがサーバーにリクエストを送信する際、設定した認証ルールに従って署名を計算し、この署名をリクエストに含めます。サーバーはリクエストを受信すると、署名を検証します。検証が成功した場合にのみ、ユーザーからのリクエストが許可されます。

このドキュメントでは、[サンプルコード](https://docs.byteplus.com/en/docs/18/32310#%E7%BD%B2%E5%90%8D%E8%A8%88%E7%AE%97%E3%81%AE%E3%82%B5%E3%83%B3%E3%83%97%E3%83%AB%E3%82%B3%E3%83%BC%E3%83%89)を通じてユーザー側の署名ロジックの実装を示します。また、CDNでリクエスト認証ロジックを設定する方法についても説明します。

<span id="認証プロセス"></span>
### 認証プロセス


1. CDNコンソールでドメイン名のURL認証ルールを設定します。CDNは、選択および設定可能な複数の認証タイプを提供しています。各認証タイプは異なる署名アルゴリズムを提供します。

2. ユーザーが署名付きリクエストをドメイン名に送信します。

3. 設定されたURL認証ルールに従って、CDNは以下の検証を行います：

   * CDNが計算した署名がユーザーからのリクエストに含まれる署名と一致するかどうかを検証します。この検証に使用されるロジックは以下の通りです：

      * 小文字のMD5値を比較します。

   * リクエストが期限切れでないかを検証します。リクエストが以下の条件を満たす場合、期限切れではありません：

      * CDNがリクエストを受信した時間 <= リクエストに含まれるタイムスタンプ + 署名の有効期間

4. 検証が成功した場合、CDNはリクエストを許可します。失敗した場合、リクエストは拒否され、403のレスポンスステータスコードが返されます。


URL認証は、悪意のあるユーザーがコンテンツを不正に使用することを効果的に防ぐことができます。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">URL認証はCDNによって実行されるため、サイトの設定を変更する必要はありません。</div>


* <div data-tips="true" data-tips-type="tip">URL認証を有効にすると、すべてのユーザーリクエストに署名が含まれている必要があります。そうでない場合、リクエストは失敗します。</div>


* <div data-tips="true" data-tips-type="tip">認証タイプがEタイプの場合、CDNはオリジンリクエストにユーザーからのリクエストの署名を含めます。</div>


* <div data-tips="true" data-tips-type="tip">認証タイプがEタイプでない場合、CDNはオリジンリクエストに署名を含めません。オリジンサーバーでもURL認証が有効になっている場合、オリジンリクエストは失敗します。オリジンサーバー上のURL認証を無効にする必要があります。</div>



<span id="操作手順"></span>
## 操作手順


1. **署名付きURL認証**設定ペイジを開きます。操作手順については[ドメイン名設定](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_jp)をご参照ください。

2. **署名付きURL認証**で、**状態**を**有効**に設定します。

3. 認証タイプを選択し、対応する設定を行います。

   * [タイプA](https://docs.byteplus.com/en/docs/byteplus-cdn/Type-A-jp)

   * [タイプB](https://docs.byteplus.com/en/docs/byteplus-cdn/Type-B-jp)

   * [タイプC](https://docs.byteplus.com/en/docs/byteplus-cdn/Type-C-jp)

   * [タイプD](https://docs.byteplus.com/en/docs/byteplus-cdn/Type-D-jp)

   * [タイプE](https://docs.byteplus.com/en/docs/byteplus-cdn/Type-E-jp)

   * [タイプF](https://docs.byteplus.com/en/docs/byteplus-cdn/typef_jp)

4. 設定後、**保存**をクリックします。


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_0670b4807d8520c2d99a638961d1330f.png) </span>

<span id="署名計算のサンプルコード"></span>
## 署名計算のサンプルコード

ユーザーリクエストに含まれる署名は、独立した署名サーバーから提供することも、ユーザーで生成することもできます。以下のサンプルコードに示される署名アルゴリズムを参考にして、ユーザーまたは署名サーバーで適切なプログラミング言語を使用して署名計算ロジックを実装することができます。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Pythonのサンプルコードは、Python 3.0が必要です。</div>


<Attachment link="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_764b0d07610e99ad909f897f2c2b4789.txt" name="URL-Auth-for-PHP.txt">URL-Auth-for-PHP.txt</Attachment>


<Attachment link="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_f4de2bc0c6c583787678290aa04fb025.txt" name="URL-Auth-for-Go.txt">URL-Auth-for-Go.txt</Attachment>


<Attachment link="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_17238c7e88c379eca0ff1708ce4fbb68.txt" name="URL-Auth-for-Python.txt">URL-Auth-for-Python.txt</Attachment>


<Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/68b02630a2a34e6b862915dec9f1845f~tplv-goo7wpa0wc-image.image" name="URL-Auth-for-Java.txt">URL-Auth-for-Java.txt</Attachment>
