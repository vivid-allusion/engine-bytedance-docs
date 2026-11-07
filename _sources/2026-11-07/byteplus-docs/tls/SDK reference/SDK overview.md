---
title: "SDK overview"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/sdk_overview"
---

This topic introduces Torch Log Service (TLS) SDKs for various languages.

<span id="日志服务-sdk"></span>
## TLS SDKs

TLS offers SDKs for mainstream languages such as Go and Node.js. The SDKs encapsulate TLS API actions to implement features such as managing resources, collecting logs, and querying logs. The SDK implementation varies depending on the language. For more information, refer to the documents of each specific SDK.


* TLS SDKs implement the signature logic of server\-side API actions. When using an SDK to call an API action, you do not need to be concerned with the compute logic of the API signature, making it easy to use.

* When you use a TLS SDK to upload logs, the log data is encapsulated in Protobuf format.

* When you use a TLS SDK to upload logs, the log data is compressed automatically. Therefore, you do not need to be concerned with the compression method and logic.


<span id="使用限制"></span>
## Limits


* Each SDK calls server\-side API actions using synchronous requests.

* When you use an SDK to send a request to the server for interaction, the request goes through the security authentication of Identity and Access Management (IAM). For this reason, you must specify an AccessKey pair that is enabled. We recommend that you use the AccessKey pair of an IAM user. Make sure that the IAM user has relevant permissions.

* After TLS query features are upgraded in the back end, we recommend that you use the latest version of a TLS SDK. The latest version of each SDK supports SearchLogsV2. The X\-Tls\-Apiversion in the request header is fixed to 0.3.0. You can use the latest SQL functions and syntax after query features such as estimation functions are upgraded.


<span id="sdk-列表"></span>
## SDKs


|SDK |Download URL |Sample Project |Reference |
|---|---|---|---|
|Go SDK |[Go SDK download URL](https://github.com/volcengine/volc-sdk-golang) |[Go SDK sample project](https://github.com/volcengine/volc-sdk-golang/tree/main/example/tls) |[SDK for Go overview](https://docs.byteplus.com/docs/tls/go_sdk_overview) |
|Java SDK |[Java SDK download URL](https://github.com/volcengine/volc-sdk-java) |[Java SDK sample project](https://github.com/volcengine/volc-sdk-java/tree/main/example/src/main/java/com/volcengine/example/tls/demo) |[SDK for Java overview](https://docs.byteplus.com/docs/tls/tls_sdk_for_java_overview) |
|Python SDK |[Python SDK download URL](https://github.com/volcengine/volc-sdk-python) |[Python SDK sample project](https://github.com/volcengine/volc-sdk-python/tree/main/volcengine/example/tls) |[SDK for Python overview](https://docs.byteplus.com/docs/tls/tls_sdk_for_python_overview) |
|Android SDK |[Android SDK download URL](https://github.com/volcengine/volc-sdk-java) |[Android SDK sample project](https://github.com/volcengine/volc-sdk-java/tree/main/android-example/src/main/java/com/volcengine/example/tls/android-demo) |[SDK for Android overview](https://docs.byteplus.com/docs/tls/tls_sdk_for_android_overview) |
|iOS SDK |[iOS SDK download URL](https://github.com/volcengine/ve-tls-ios-sdk) |[iOS SDK sample project](https://github.com/volcengine/ve-tls-ios-sdk/blob/master/VeTLSiOSSDK-Example/VeTLSiOSSDK-Example/main.m) |[SDK for iOS overview](https://docs.byteplus.com/docs/tls/tls_sdk_for_ios_overview) |
|C++ SDK |[C++ SDK download URL](https://github.com/volcengine/ve-tls-cpp-sdk) |[C++ SDK sample project](https://github.com/volcengine/ve-tls-cpp-sdk/blob/master/demo/main.cc) |[SDK for C++ Overview](https://docs.byteplus.com/docs/tls/tls_sdk_for_c_overview) |
|Node.js SDK |[Node.js SDK download URL](https://github.com/volcengine/volc-sdk-nodejs) |[Node.js SDK sample project](https://github.com/volcengine/volc-sdk-nodejs/tree/main/src/services/tls/example) |[SDK for Node.js overview](https://docs.byteplus.com/docs/tls/tls_sdk_for_nodejs_overview) |
|Browser JavaScript SDK |[Browser JavaScript SDK download URL](https://github.com/volcengine/tls-js-sdk) |[JavaScript SDK sample project](https://github.com/volcengine/tls-js-sdk) |[Browser JavaScript SDK](https://docs.byteplus.com/docs/tls/browser_javascript_sdk) |
