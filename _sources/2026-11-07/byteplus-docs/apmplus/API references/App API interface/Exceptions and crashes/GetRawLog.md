---
title: "GetRawLog"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/GetRawLog"
---

Get raw data.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable access point based on your business location.


* Request method: GET

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=GetRawLog&Version=2025\-12\-01


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Before you call this API, specify the required public request parameters (such as <code>x-app-ids</code>). Otherwise, the call fails.</div>



|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |GetRawLog |The API name. The API name is `GetRawLog`. |
|Version |String |Yes |2025\-12\-01 |The API version. The API version is `2025-12-01`. |
|RawLogKey |String |Yes |example_raw_log_key |The identifier key of the raw file. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```JSON
GET https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=GetRawLog&Version=2025-12-01&RawLogKey=example_raw_log_key
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Stack |String |libsystem_platform.dylib__platform_memset (in libsystem_platform.dylib) |Raw stack trace information. |
|Custom |JSON Map |{"app_name":"tt"} |The custom data. |


Sample response

```JSON
{
    "ResponseMetadata": {
        "Action": "GetRawLog",
        "Region": "cn-north-1",
        "Service": "apmplus_openapi",
        "Version": "2025-12-01",
        "RequestId": "20230604110420****100232280022D31"
    },
    "Result": {
        "Stack": "libsystem_platform.dylib__platform_memset (in libsystem_platform.dylib)",
        "Custom": {
            "app_name": "tt"
        }
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

No error codes are specific to this API. If the API call returns an error code, refer to [Public error](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) codes for troubleshooting.
