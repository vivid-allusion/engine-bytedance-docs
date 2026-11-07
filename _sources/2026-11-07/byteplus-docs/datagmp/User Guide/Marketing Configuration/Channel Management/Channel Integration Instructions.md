---
title: "Channel Integration Instructions"
product: "Byteplus GMP"
product_code: "datagmp"
source: "https://docs.byteplus.com/en/docs/datagmp/Channel_Integration_Instructions"
---

**The configuration/integration instructions for marketing channels are as follows:** 


|**Marketing Touchpoint/Channel** |**Configuration/Integration Instructions** |
|---|---|
|Webhook |Webhook is an API concept that allows you to call your own sending channel interfaces to deliver messages, such as invoking your own SMS, push, WeChat, email, or outbound call interfaces to send messages. |
|SMS |* If you already have an SMS service provider and the provider is Jiguang, Montnets, Yunpian, Alibaba Cloud, or Tencent Cloud, you can directly configure your account in GMP for integration.<br><br>* If you do not have a partnered SMS service provider, you can purchase BytePlus Cloud Communication SMS services. |
|WeChat Public Account |Integration is possible via developer mode or third\-party authorization mode; currently under development. |
|APP push |Using GMP's own push service: GMP integrates vendor channels and third\-party channels to maximize push delivery rates. GMP also collects complete end\-to\-end data and enables copy A/B testing strategies based on real\-time data feedback (requires client integration of GMP push SDK). |
|H5 Pop\-up |Requires integration of GMP's JS SDK. |
|Client Pop\-up |Requires integration of GMP's client SDK. |
|Placement |Requires integration of GMP's Placement SDK. |


Taking webhook as an example, only simple configuration is required to connect with existing enterprise capabilities. For documentation on integrating the webhook channel, please refer to [【历史 GMP v3.11.0 】Webhook通道接入](https://docs.byteplus.com/docs/6315/66392).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b68261cdc1d743b79e1dbeb3d82d53dd~tplv-goo7wpa0wc-image.image) </span>
