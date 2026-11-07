---
title: "GetServiceList"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/GetServiceList"
---

Get the service list.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable access point based on your business location.


* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=GetServiceList&Version=2022\-10\-12


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |GetServiceList |The API name. The current API name is `GetServiceList`. |
|Version |String |Yes |2022\-10\-12 |The API version. The current API version is `2022-10-12`. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```JSON
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=GetServiceList&Version=2022-10-12
{}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|error_msg |String |"" |Error message. It is empty if the request succeeds. |
|error_no |Integer |0 |Error code. 0 indicates success. |
|data |JSON Map |\- |Service list. The key is the unique service key. |


<span id="data"></span>
### Data


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|key |String |app_monitor |Application. |
|value |Object of [ApmService](https://docs.byteplus.com/en/docs/299/67861#apmservice) |\- |Application key. |


<span id="apmservice"></span>
### ApmService


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|id |Integer |123456 |Application ID. |
|pay |Boolean |true |Whether it is activated as a paid service. |
|demo |Boolean |true |Whether to display a demo. |
|name |String |App Monitoring |The service name. |
|doc_url |String |https://docs.byteplus.com/en/docs/6431/160093 |Documentation link. |
|demo_aid |Long |12345 |Demo application ID. |
|icon_url |String |www.example.com |Icon link. |
|sort_index |Integer |\- |Sort index. |
|description |String |test |Service description. |
|service_key |String |\- |Unique service key. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```JSON
{
    "error_msg": "",
    "data": {},
    "error_no": 0
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

No error codes are specific to this API. If the API call returns an error code, refer to [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) for troubleshooting.
