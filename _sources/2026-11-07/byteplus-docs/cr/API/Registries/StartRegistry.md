---
title: "StartRegistry"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/startregistry"
---

Start a Standard Edition instance of the Container Registry.

<span id=".5o6l5Y-j6K-05piO"></span>
## API description

Currently, this interface is only used to restore a Standard Edition instance that is in a pending reclaiming status (`{Stopped, [Released]}`). Before calling this API, call the [ListRegistries](https://docs.byteplus.com/en/docs/cr/listregistries) API to obtain the current status of the target Standard Edition instance.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

To achieve low latency, it is recommended that you select the corresponding service address based on the region where your resources are located. For details, refer to [service address](https://docs.byteplus.com/en/docs/cr/Service_address).


* Request method: POST

* Request URL: https://cr.cn\-beijing.byteplusapi.com.cn?Action=StartRegistry&Version=2022\-05\-12


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

When calling this API, in addition to the following request parameters, you also need to provide the public request parameters.  See [Public parameters](https://docs.byteplus.com/en/docs/cr/common-parameters) for details.


|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |StartRegistry |The API name. The current API's name is `StartRegistry`. |
|Version |String |Yes |2022\-05\-12 |The API version. The current version of the API is `2022-05-12`. |
|Name |String |Yes |example |The name of the Standard Edition instance to be started. On the [Container Registry console](https://console.byteplus.com/cr) **instance list** page, obtain the Standard Edition instance name. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST https://cr.cn-beijing.byteplusapi.com.cn?Action=StartRegistry&Version=2022-05-12
{
    "Name": "example"
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

None

<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```json
{
    "ResponseMetadata": {
        "RequestId": "540CFF28-407A-40B5-B6A5-74Bxxxxxxxxx",
        "Action": "StartRegistry",
        "Version": "2022-05-12",
        "Service": "cr",
        "Region": "cn-beijing"
    },
    "Result": {}
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

The error codes for this interface are shown in the table below. For public error codes, refer to [public error code](https://docs.byteplus.com/en/docs/cr/common-error-codes).


|**HTTP Status Code** |**Error code** |**Error Message** |**Descriptions** |
|---|---|---|---|
|400 |OperationDenied.Status |The action has been denied due to wrong status %s. |The specified operation is not allowed under the current access endpoint status. Please wait for the status transition to complete and try again. |
