---
title: "How to customize uploading a symbol table"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/How_to_customize_uploading_a_symbol_table"
---

The domain name and interface for uploading symbol tables have been encapsulated in the SDK. By default, the SDK supports two methods for uploading symbol tables: [manual upload and automatic upload](https://docs.byteplus.com/en/docs/apmplus/Integrate_the_Android_SDK_into_the_application#49dce7df). If you want to upload symbol tables using a custom method, please refer to this document.

<span id="GqZhwgEo"></span>
## Usage Limits

The request address for uploading symbol tables varies by region. For detailed information, refer to the symbol table request address listed under [server-launching region](https://docs.byteplus.com/en/docs/apmplus/server-launching_region).

<span id="43d42ae3"></span>
## Upload a custom symbol table

The request headers are as follows:

```HTTP
"Content-Type":"multipart/form-data; boundary=" + "---" + System.currentTimeMillis() + "---"

long currentTime = System.currentTimeMillis();
MessageDigest digest = MessageDigest.getInstance("MD5")
digest.update("${currentTime}${project.apminsightConfig.api_token}".getBytes())

"X-OpenApi-Timestamp": currentTime
"X-OpenApi-Token": new BigInteger(1, digest.digest()).toString(16)
"X-OpenApi-AppID": project.apminsightConfig.api_key
"X-App-Ids": aid
```


To obtain the `api_token` and `api_key` information, please follow the method below:


1. Enter the application and select **All features \> File management \> Symbol table management**.

2. On the **Symbol Table Management** page, select the **Android** system, then obtain the **API Key** and **API Token**.


Sample request:

```HTTP
curl https://open.apmplus.cn-beijing.volces.com/apmplus_api/eue/guest/app/mapping/upload \
-F "type=Java" \
-F "os=Android" \
-F "aid=187277" \
-F "update_version_code=12345" \
-F "fileSize=819337" \
-F "file=@/Users/bytedance/code/Npth_toB/Npth/app/build/outputs/mapping/cnNoasanTob/release/mapping.txt" \
-H "X-OpenApi-Timestamp: 1656569613656" \
-H "X-OpenApi-Token: c42c7bfbebc6980eb0f19715***" \
-H "X-OpenApi-AppID: 4" -H "X-App-Ids: 187***" \
-H "Content-Type: multipart/form-data" \
-w %{http_code} -v
```
