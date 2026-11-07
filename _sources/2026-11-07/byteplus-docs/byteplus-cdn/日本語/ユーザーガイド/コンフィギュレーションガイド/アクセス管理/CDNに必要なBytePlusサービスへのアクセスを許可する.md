---
title: "CDNに必要なBytePlusサービスへのアクセスを許可する"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/allow-cdn-access-to-byteplus-service-jp"
---

BytePlus CDNで以下の操作を実行する場合、CDNに対応するBytePlusサービスへのアクセスを許可する必要があります：


* BytePlus オブジェクトストレージ（TOS）内の名前空間をオリジンサーバーとして指定する場合：CDNにTOSサービスへのアクセスを許可する必要があります。

* 証明書をアップロードするか、BytePlus証明書センター内の証明書を関連付ける場合：CDNに証明書センターサービスへのアクセスを許可する必要があります。

* エッジ関数を作成する場合：CDNにエッジ関数サービスへのアクセスを許可する必要があります。


上記の操作を実行する際に、あなたやIAMユーザーが権限の問題に遭遇するのを避けるため、事前にCDNにこれらのサービスへのアクセス権限を付与することをお勧めします。

<span id="操作手順"></span>
## 操作手順

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">以下の手順はプライマリアカウントで操作することを強くお勧めします。以下の手順が完了すると、プライマリアカウントとIAMユーザーがCDNで証明書の操作、エッジ関数の管理、TOS名前空間をオリジンサーバーとして設定する際に、これらの手順を再度実行する必要はなく、サービス認可の問題にも遭遇しません。</div>


<div data-tips="true" data-tips-type="warning">IAMユーザーの場合、IAMFullAccessシステムポリシーが付与されていない限り、CDNに他のBytePlusサービスへのアクセスを許可する権限がありません。したがって、IAMFullAccessポリシーが付与されていないIAMユーザーが以下の手順を操作すると、認可は失敗します。同時に、IAMユーザーにIAMFullAccessポリシーを付与することはお勧めしません。このポリシーの権限範囲が広すぎるためです。</div>



1. [このリンク](https://console.byteplus.com/iam/service/attach_role/?ServiceName=CDN)を開きます。

2. **今すぐ承認**をクリックします。


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_71448eec895692e6beed03cbe65f6d58.jpeg) </span>
