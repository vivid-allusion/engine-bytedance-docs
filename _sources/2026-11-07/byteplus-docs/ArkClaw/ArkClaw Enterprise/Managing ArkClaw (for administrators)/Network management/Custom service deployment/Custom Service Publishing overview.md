---
title: "Custom Service Publishing overview"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Custom-service-deployment-Overview"
---

<span id="APM8zOXq"></span>
## Scenarios

By default, ArkClaw Spaces only serve employees through the internal workspace. To expose Claw instance capabilities (such as Web applications or APIs) to external users or other systems in the enterprise network, use Custom Service Publishing. This feature registers Claw instances as backend servers via Application Load Balancer (ALB) and publishes services through public or private ALB.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">ALB with ArkClaw capabilities are currently in invite\-only beta. To request a trial, please contact your account manager.</div>


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_61fd3fcbeb29502fef229dc94c974d46.png) </span>

<span id="72bioRyW"></span>
## Use limits


* ALBs with ArkClaw enabled support only IPv4.

* The network type cannot be changed for ALBs with ArkClaw enabled.

* The availability zone cannot be edited for ALBs with ArkClaw enabled. Two zones are fixed.


<span id="5Yt6Vpnq"></span>
## Procedure


* **Public network**

   1. [Create Public ALB (Enable ArkClaw)](https://docs.byteplus.com/en/docs/ArkClaw/Publishing-a-custom-service)

   2. [Create Claw server group](https://docs.byteplus.com/en/docs/ArkClaw/Publishing-a-custom-service)

   3. [Add Claw as backend server](https://docs.byteplus.com/en/docs/ArkClaw/Publishing-a-custom-service)

   4. [Create HTTP listener](https://docs.byteplus.com/en/docs/clb/Creating-HTTP-listener)

   5. [Configure enterprise custom domain](https://docs.byteplus.com/en/docs/ArkClaw/configuring-a-custom-enterprise-domain-old-version)

* **Private network**

   1. [Create Private ALB (Enable ArkClaw)](https://docs.byteplus.com/en/docs/ArkClaw/Publishing-a-custom-service)

   2. [Create Claw server group](https://docs.byteplus.com/en/docs/ArkClaw/Publishing-a-custom-service)

   3. [Add Claw as backend server](https://docs.byteplus.com/en/docs/ArkClaw/Publishing-a-custom-service)

   4. [Create HTTP listener](https://docs.byteplus.com/en/docs/clb/Creating-HTTP-listener)

   5. [Create endpoint service (with the ArkClaw-enabled ALB as the service resource)](https://docs.byteplus.com/en/docs/privatelink/Creating-endpoint-services)

   6. [Create endpoint](https://docs.byteplus.com/en/docs/privatelink/Endpoint-02)
