---
title: "API overview"
product: "BytePlus Messaging"
product_code: "byteplus-sms"
source: "https://docs.byteplus.com/en/docs/byteplus-sms/docs-overview"
---

This section guides you on how to call BytePlus Messaging APIs. Currently, BytePlus Messaging offers the APIs included in BytePlus Messaging SDKs and OpenAPIs.


|**Access method** |**Safety** |**Complexity** |**Template ID** |**Support channels** |
|---|---|---|---|---|
|Openapi 2.0 (Recommend) |Low |Low |The content can be directly sent out. |SMS, WhatsApp, Voice |
|Openapi |Low |Low |The content can be directly sent out. |SMS |
|Apis |High |High |Template ID must be used (prior reporting is required). |SMS |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Byteplus APIs & OpenAPI distinction</div>



1. <div data-tips="true" data-tips-type="tip">Authentication Complexity & Access Difficulty</div>


   1. <div data-tips="true" data-tips-type="tip">APIs：The SDK needs to be integrated to complete the more complex authentication process and provide a higher level of security</div>


   2. <div data-tips="true" data-tips-type="tip">OpenAPI：The certification process is relatively simple, allowing for quick integration and testing</div>


2. <div data-tips="true" data-tips-type="tip">Template use</div>


   1. <div data-tips="true" data-tips-type="tip">APIs: The template ID must be passed as a parameter to ensure consistency and compliance of the message content</div>


   2. <div data-tips="true" data-tips-type="tip">OpenAPI: Does not need to pass in the template ID, allowing for more active message content</div>


3. <div data-tips="true" data-tips-type="tip">Reason of difference</div>


   1. <div data-tips="true" data-tips-type="tip">Security considerations: The complex authentication mechanism of APIs provides higher security and is suitable for handling sensitive information or sending at large scale.</div>


   2. <div data-tips="true" data-tips-type="tip">Compliance management: Using template ID ensures that all messages sent are pre\-reviewed and comply with relevant regulatory requirements,</div>


   3. <div data-tips="true" data-tips-type="tip">Functionality and exposure :APIs provide more control and more functionality, while OpenAPI provides more flexibility and ease of use</div>



<div data-tips="true" data-tips-type="tip">You can select an access mode that suits you.</div>


<div data-tips="true" data-tips-type="tip">PS：Non\-SMS channels currently only support OpenAPI 2.0 integration.<strong>OpenAPIs only support sending SMS.</strong></div>


For how to integrate a SDK, refer to [SDK integration overview](https://docs.byteplus.com/en/byteplus-sms/docs/sdk-integration_1).

BytePlus OpenAPIs are also applicable for BytePlus Messaging. For details, refer to [BytePlus OpenAPI Overview](https://docs.byteplus.com/byteplus-platform/reference/overview-1).
