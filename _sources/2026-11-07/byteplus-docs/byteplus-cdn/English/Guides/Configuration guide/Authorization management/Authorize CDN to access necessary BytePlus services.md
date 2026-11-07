---
title: "Authorize CDN to access necessary BytePlus services"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-authorize-byteplus-cdn-to-access-byteplus-certificate-center"
---

To prevent permission errors when using BytePlus CDN features that interact with other services like TOS, Certificate Center, or Edge Functions, you must grant CDN the necessary access permissions. This guide shows you how to complete this one\-time authorization to ensure smooth operations for both primary and IAM users.


* Specify a bucket in BytePlus Tinder Object Storage (TOS) as an origin: You need to authorize CDN to access the TOS service.

* Upload a certificate or associate a certificate from BytePlus Certificate Center: You need to authorize CDN to access the Certificate Center service.

* Create an edge function: You need to authorize CDN to access the Edge Functions service.


To avoid permission issues for you and your IAM users when performing the above operations, we recommend that you grant CDN permissions to access these services in advance.

<span id="steps"></span>
## Steps

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">We highly recommend using the primary account for these steps. After this one\-time setup is complete, neither the primary account nor IAM users will need to repeat the authorization when managing certificates, using edge functions, or setting TOS buckets as origin servers. This also prevents service authorization issues.</div>


<div data-tips="true" data-tips-type="tip">IAM users do not have permission to grant CDN access to other BytePlus services unless they are granted the IAMFullAccess system policy. Therefore, if an IAM user without the IAMFullAccess policy performs the following steps, the authorization will fail. Additionally, we do not recommend granting IAM users the IAMFullAccess policy because its permission scope is too broad.</div>



1. Open the [Service authorization](https://console.byteplus.com/iam/service/attach_role/?ServiceName=CDN) page.

2. Click **Authorize Now**.


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_5652ebf1824cd0ed90d371e437850f51.png) </span>
