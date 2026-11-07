---
title: "Server SDK overview"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-server-sdk-overview"
---

To simplify your integration with BytePlus VOD, this document provides a central resource for all available Server SDKs. It offers direct links to download, install, and use the SDKs for various programming languages, including Java, Python, Go, and PHP. The SDKs handle complex tasks like signature generation and API request management, allowing you to quickly implement VOD features in your application.


* Signature generation, which saves you from the complicated calculation process.

* Common OpenAPI operations, including sending requests and handling responses. Each SDK provides a corresponding code sample.


<span id="d9db79a2"></span>
## Prerequisites


* A BytePlus account or an IAM user. For more information, see [Signing up for a BytePlus account](https://docs.byteplus.com/en/byteplus-platform/docs/signing-up-your-account) or [Managing IAM users and roles](https://docs.byteplus.com/byteplus-livesaas/docs/managing-iam-users-and-roles).

* Obtain the AccessKey ID (AK) and Secret Access Key (SK) for authentication.

   * To obtain the AK and SK of a BytePlus account, go to [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/) \> User Profile \> **IAM** \> **Key management**.

   * To obtain the AK and SK of an IAM user, complete the following steps:

      1. Go to [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/) \> User Profile \> **IAM** \> **Identity management** \> **User**.

      2. Find the user and then click **View details**.

      3. On the **Access key** tab, click **Create new access key**.


<span id="5d966ab8"></span>
## SDK list

BytePlus offers two versions of its Server SDKs: V1.0 and V2.0. The V2.0 SDK is our next\-generation development kit, featuring a unified architecture and a standardized API design to streamline integration and maintenance. Note that V2.0 currently supports Java, Python, and Go only.

As BytePlus transitions all OpenAPIs to the V2.0 SDK, you may need to use both versions concurrently during this period. We recommend the following migration strategy:


1. Gradual adoption: Prioritize the use of V2.0 for supported OpenAPIs, while continuing to use V1.0 for those not yet available in the new version.

2. Version monitoring: Regularly check for updates as more OpenAPIs are added to the V2.0 SDK.

3. Full migration: Once the V2.0 SDK supports all the OpenAPIs required for your project, you can safely remove the V1.0 dependency.


<span id="b64cb39b"></span>
## Integration and usage

See the following table for instructions on integrating and using the Server SDKs. You can find code examples on our GitHub repository.


|**Language** |**V1.0** |||**V2.0** ||
|---|---|---|---|---|---|
||**Source code on GitHub** |**Sample code on GitHub** |**Documentation** |**Source code on GitHub** |**Documentation** |
|PHP SDK |[byteplus-sdk-php](https://github.com/byteplus-sdk/byteplus-sdk-php/tree/master/src/Service/Vod) |[PHP code examples](https://github.com/byteplus-sdk/byteplus-sdk-php/tree/master/examples/Vod) |[PHP SDK](https://docs.byteplus.com/docs/byteplus-vod/docs-php-sdk) |Not supported ||
|Python SDK |[byteplus-sdk-python](https://github.com/byteplus-sdk/byteplus-sdk-python/tree/master/byteplus_sdk/vod) |[Python code examples](https://github.com/byteplus-sdk/byteplus-sdk-python/tree/master/byteplus_sdk/example/vod) |[Python SDK](https://docs.byteplus.com/docs/byteplus-vod/docs-python-sdk) |[byteplus-python-sdk-v2](https://github.com/byteplus-sdk/byteplus-python-sdk-v2/tree/main/byteplussdkvod20250701) |* [Integrate the SDK](https://github.com/byteplus-sdk/byteplus-python-sdk-v2/blob/main/SDK_Integration.md)<br><br>* [Sample code](https://docs.byteplus.com/en/docs/byteplus-vod/docs-server-sdk-v2#python) |
|Go SDK |[byteplus-sdk-golang](https://github.com/byteplus-sdk/byteplus-sdk-golang/tree/master/service/vod) |[Go code examples](https://github.com/byteplus-sdk/byteplus-sdk-golang/tree/master/example/vod) |[Go SDK](https://docs.byteplus.com/docs/byteplus-vod/docs-go-sdk) |[byteplus-go-sdk-v2](https://github.com/byteplus-sdk/byteplus-go-sdk-v2/tree/main/service/vod20250701) |* [Integrate the SDK](https://github.com/byteplus-sdk/byteplus-go-sdk-v2/blob/main/SDK_Integration.md)<br><br>* [Sample code](https://docs.byteplus.com/en/docs/byteplus-vod/docs-server-sdk-v2#go) |
|Java SDK |[byteplus-sdk-java](https://github.com/byteplus-sdk/byteplus-sdk-java/tree/master/byteplus-sdk-java/src/main/java/com/byteplus/service/vod) |[Java SDK code examples](https://github.com/byteplus-sdk/byteplus-sdk-java/tree/master/example/src/main/java/com/byteplus/example/vod) |[Java SDK](https://docs.byteplus.com/docs/byteplus-vod/docs-java-sdk) |[byteplus-java-sdk-v2](https://github.com/byteplus-sdk/byteplus-java-sdk-v2/tree/main/byteplus-java-sdk-v2-vod20250701) |* [Integrate the SDK](https://github.com/byteplus-sdk/byteplus-java-sdk-v2/blob/main/SDK_Integration.md)<br><br>* [Sample code](https://docs.byteplus.com/en/docs/byteplus-vod/docs-server-sdk-v2#java) |
|Node.js SDK |Not available |Not available |[Node.js SDK](https://docs.byteplus.com/en/docs/byteplus-vod/docs-nodejs-sdk?type=preview) |Not supported ||
