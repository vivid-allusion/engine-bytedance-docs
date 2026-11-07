---
title: "Common Request Parameters"
product: "Vision AI"
product_code: "byteplus-vision"
source: "https://docs.byteplus.com/en/docs/byteplus-vision/docs-common-request-parameters"
---

To successfully call BytePlus Vision openAPIs, you must include several public parameters in every request for authentication and routing. This document lists these necessary parameters, such as `Authorization` and `Region`. For the complete list of all public parameters, see [Common parameters](https://docs.byteplus.com/byteplus-platform/reference/common-parameters)


|**Name** |**Type** |**Must/Optional** |**Example value** |**Description** |
|---|---|---|---|---|
|X\-Date |String |Must |20201103T104027Z |Time in UTC with second\-level precision, formatted as YYYYMMDD'T'HHMMSS'Z' |
|Region |String |Must |ap\-singapore\-1 |The geography parameter, which identifies which geographic region you wish to operate on, takes a fixed value of `ap-singapore-1`. |
|Service |String |Must |cv |The type of service used, with a fixed value of `cv`. |
|Authorization |String |Must |HMAC\-SHA256 Credential={AccessKeyId}/{ShortDate}/{Region}/{Service}/request, SignedHeaders={SignedHeaders}, Signature= |HMAC\-SHA256: signature method<br><br>Credential: signature credentials, where,<br><br>AccessKeyId is the access key ID, more details at [Calculating a signature](https://docs.byteplus.com/byteplus-platform/reference/how-to-calculate-a-signature)<br><br>ShortDate is<br><br>Region defaults to `ap-singapore-1`.<br><br>Service defaults to `cv`<br><br>SignedHeaders is the header information involved in the signature calculation, content\-type and host are mandatory headers;<br><br>Signature is the signature, available in [Calculating a signature](https://docs.byteplus.com/byteplus-platform/reference/how-to-calculate-a-signature).<br><br>Note: We provide SDK and signature examples to help you quickly integrate the service; please refer to [Quick Integration via SDK](https://docs.byteplus.com/byteplus-vision/docs/quick-integration-via-sdk) |
|X\-Security\-Token |String |Optional |None |It refers to the SessionToken in the temporary security credentials issued by Security Token Service (STS):<br><br><br>1. The user/service can use AK/SK to access their own resources directly (long\-term Token) without filling in the parameter.<br><br>2. A user or service must use STS when calling the interface by assuming a role. The process is to first call AssumeRole to get a short\-term token, and then include that token in this parameter to request the target interface. |
|Content\-Type |String |Must |application/x\-www\-form\-urlencoded |Encoding format |
