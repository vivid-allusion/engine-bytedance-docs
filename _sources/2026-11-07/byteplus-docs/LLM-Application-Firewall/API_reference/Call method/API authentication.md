---
title: "API authentication"
product: "LLM Application Firewall"
product_code: "LLM-Application-Firewall"
source: "https://docs.byteplus.com/en/docs/LLM-Application-Firewall/API_authentication"
---

API signature is used to verify the requester's identity and prevent requests from being tampered with. To reduce integration costs, it is recommended to use the SDK sample provided by the LLM Application Firewall to skip the signature process, or refer to the BytePlus signature sample to make necessary modifications and complete the signature.

<span id="33cf970a"></span>
## Call the LLM Application Firewall SDK directly

LLM Application Firewall provides SDKs for common programming languages, allowing you to call product APIs directly. For more details, refer to [SDK overview](https://docs.byteplus.com/docs/LLM-Application-Firewall/SDK_overview).

<span id="f1370a9e"></span>
## Use signature examples

If the provided SDKs do not meet your requirements, you can refer to the BytePlus signature example to learn about the signature generation process and modify it as needed.


|Parameters |Description |Example |
|---|---|---|
|Service |The service name for the LLM Application Firewall. This value is always `llmshield`. |llmshield |
|Version |The version of the LLM Application Firewall API. This value is always `2025-08-31` |2025\-08\-31 |
|Action |The name of the LLM Application Firewall API. See the corresponding API documentation for details. |Moderate |
|Region |Region of the LLM Application Firewall instance.<br><br><br>* China (HongKong): cn\-hongkong<br><br>* Asia Pacific (Johor):  ap\-southeast\-1 |cn\-hongkong |
|Host |The external service domain name of the LLM Application Firewall. The format is `{region}.sdk.access-bp.llm-shield.omni-shield.ai`. Replace `{region}` with the region of your instance. |`cn-hongkong.sdk.access-bp.llm-shield.omni-shield.ai` |
|Path |The API request path, which specifies the operation or resource to access. This path excludes the query string. Refer to the corresponding API documentation for details. |/v2/moderate |
