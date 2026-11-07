---
title: "TLSバージョン"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/tls-version-jp"
---

本ドキュメントでは、BytePlus CDNでドメイン名のTLSバージョンサポートを設定する方法について説明します。

ユーザーがブラウザを使用してHTTPS加速が有効になっているドメインにアクセスする際、CDNはブラウザのTLSバージョンサポート状況とドメイン名がサポートするTLSバージョンに基づいて、一致する最高のTLSバージョンを選択してデータ転送を行います。CDNが一致するTLSバージョンを見つけられない場合、TLSハンドシェイクが失敗し、接続の確立に失敗します。

<span id="tlsバージョン"></span>
## TLSバージョン

古いバージョンのTLSは互換性が高い一方でセキュリティは低くなります。最新バージョンのTLSは最高のセキュリティを提供しますが、比較的互換性は低くなります。ただし、現在ほとんどのブラウザがTLS 1.3をサポートしています。TLS 1.0とTLS 1.1は古いバージョンであり、セキュリティの脆弱性リスクがあります。

CDNはすべてのTLSバージョンをサポートしています。ただし、互換性とセキュリティのバランスを取るため、ドメインのHTTPS暗号化サービスを有効にする際、CDNはデフォルトでTLS 1.1、TLS 1.2、TLS 1.3のサポートを有効にします。必要に応じて、TLS 1.0のCDNサポートを手動で有効にすることができます。

CDNがサポートするTLS暗号スイートについては、[暗号スイート](https://docs.byteplus.com/en/docs/18/32191#CDN%E3%81%8C%E3%82%B5%E3%83%9D%E3%83%BC%E3%83%88%E3%81%99%E3%82%8BTLS%E6%9A%97%E5%8F%B7%E3%82%B9%E3%82%A4%E3%83%BC%E3%83%88)を参照してください。

<span id="ブラウザがサポートするtlsバージョン"></span>
## ブラウザがサポートするTLSバージョン

TLSバージョンとブラウザのサポート状況は以下の表の通りです。


|**TLSバージョン**  | **サポートするブラウザ**  |**備考** |
|---|---|---|
|TLS 1.0 |* Microsoft Internet Explorer 6+<br><br>* Google Chrome 1+<br><br>* Mozilla Firefox 2+ |TLS 1.0とTLS 1.1のサポートは以下のバージョンのブラウザで削除されました：<br><br><br>* Google Chrome 84+<br><br>* Microsoft Edge 84+<br><br>* Mozilla Firefox 78+<br><br>* Safari 14+ |
|TLS 1.1 |* Microsoft Internet Explorer 11+<br><br>* Google Chrome 22+<br><br>* Microsoft Edge 12+<br><br>* Mozilla Firefox 24+<br><br>* Apple Safari 7+<br><br>* Opera 12.1+ ||
|TLS 1.2 |* Microsoft Internet Explorer 11+<br><br>* Google Chrome 30+<br><br>* Microsoft Edge 12+<br><br>* Mozilla Firefox 27+<br><br>* Apple Safari 7+<br><br>* Opera 16+ | |
|TLS 1.3 |* Google Chrome 70+<br><br>* Microsoft Edge 79+<br><br>* Mozilla Firefox 63+<br><br>* Apple Safari 14+<br><br>* Opera 57+ | |


<span id="前提条件"></span>
## 前提条件

この設定を有効にするには、ドメイン名がすでにHTTPS暗号化サービスを有効にしている必要があります。

<span id="操作手順"></span>
## 操作手順


1. **TLSバージョン**  設定ペイジを開きます。操作手順については[ドメイン名設定](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_jp)をご参照ください。

2. **TLSバージョン** の下で、有効にする必要があるTLSバージョンにチェックを入れます。

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">少なくとも1つのTLSバージョンにチェックを入れる必要があります。   </div>
   

3. 設定が完了したら、**保存**をクリックします。


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_3b17148abe1c16e700c69a087a4efa1a.jpeg) </span>

<span id="追加情報"></span>
## 追加情報

<span id="cdnがサポートするtls暗号スイート"></span>
### CDNがサポートするTLS暗号スイート

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">CDNはサーバー上で設定されたスイートの優先順位に基づいて最適なスイートを選択します。</div>



|**TLSバージョン**  | **サポートする暗号スイート**  |
|---|---|
|TLS 1.1 |* ECDHE\-RSA\-AES256\-SHA<br><br>* ECDHE\-ECDSA\-AES256\-SHA<br><br>* AES256\-SHA<br><br>* CAMELLIA256\-SHA<br><br>* ECDHE\-RSA\-AES128\-SHA<br><br>* ECDHE\-ECDSA\-AES128\-SHA<br><br>* AES128\-SHA<br><br>* CAMELLIA128\-SHA |
|TLS1.2 |* ECDHE\-RSA\-AES256\-GCM\-SHA384<br><br>* ECDHE\-ECDSA\-AES256\-GCM\-SHA384<br><br>* ECDHE\-RSA\-AES256\-SHA384<br><br>* ECDHE\-ECDSA\-AES256\-SHA384<br><br>* ECDHE\-RSA\-AES256\-SHA<br><br>* ECDHE\-ECDSA\-AES256\-SHA<br><br>* ECDHE\-ECDSA\-CHACHA20\-POLY1305<br><br>* ECDHE\-RSA\-CHACHA20\-POLY1305<br><br>* ECDHE\-ECDSA\-AES256\-CCM8<br><br>* ECDHE\-ECDSA\-AES256\-CCM<br><br>* ECDHE\-RSA\-CAMELLIA256\-SHA384<br><br>* ECDHE\-ECDSA\-CAMELLIA256\-SHA384<br><br>* AES256\-GCM\-SHA384<br><br>* AES256\-CCM8<br><br>* AES256\-CCM<br><br>* AES256\-SHA256<br><br>* AES256\-SHA<br><br>* CAMELLIA256\-SHA256<br><br>* CAMELLIA256\-SHA<br><br>* ARIA256\-GCM\-SHA384<br><br>* ECDHE\-ECDSA\-ARIA256\-GCM\-SHA384<br><br>* ECDHE\-ARIA256\-GCM\-SHA384<br><br>* ECDHE\-RSA\-AES128\-GCM\-SHA256<br><br>* ECDHE\-ECDSA\-AES128\-GCM\-SHA256<br><br>* ECDHE\-RSA\-AES128\-SHA256<br><br>* ECDHE\-ECDSA\-AES128\-SHA256<br><br>* ECDHE\-RSA\-AES128\-SHA<br><br>* ECDHE\-ECDSA\-AES128\-SHA<br><br>* ECDHE\-ECDSA\-AES128\-CCM8<br><br>* ECDHE\-ECDSA\-AES128\-CCM<br><br>* AES128\-CCM8<br><br>* AES128\-CCM<br><br>* ECDHE\-RSA\-CAMELLIA128\-SHA256<br><br>* ECDHE\-ECDSA\-CAMELLIA128\-SHA256<br><br>* AES128\-GCM\-SHA256<br><br>* AES128\-SHA256<br><br>* AES128\-SHA<br><br>* CAMELLIA128\-SHA256<br><br>* CAMELLIA128\-SHA<br><br>* ARIA128\-GCM\-SHA256<br><br>* ECDHE\-ECDSA\-ARIA128\-GCM\-SHA256<br><br>* ECDHE\-ARIA128\-GCM\-SHA256 |
|TLS1.3 |* TLS_AES_256_GCM_SHA384<br><br>* TLS_CHACHA20_POLY1305_SHA256<br><br>* TLS_AES_128_GCM_SHA256 |


<span id="ブラウザリクエストで使用されているtlsバージョンを確認する方法"></span>
### ブラウザリクエストで使用されているTLSバージョンを確認する方法


1. ブラウザで特定のサイトを開きます。例えば、最新バージョンのGoogle Chromeで[BytePlus公式ウェブサイト](https://www.byteplus.com/en)を開きます。

2. F12キーを押して開発者ツール（DevTools）を開きます。

3.  **セキュリティ** タブをクリックします。

4.  **セキュリティ** タブで、赤枠内の内容に注目します。


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/23dd1e4fba6a4badb124a07bce3ce2b7~tplv-goo7wpa0wc-image.image) </span>
