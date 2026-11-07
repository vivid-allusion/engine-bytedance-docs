---
title: "DeleteRegistry"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/deleteregistry"
---

Delete a Standard Edition instance of the Container Registry.

<span id=".5o6l5Y-j6K-05piO"></span>
## API description

When deleting a Standard Edition instance, the cost\-related description is as follows:


* If **DeleteImmediately** is configured in the request parameters and its value is **true**, billing will stop when the interface returns a successful call result.

* If **DeleteImmediately** is not configured in the request parameters or its value is **false**, the instance will enter a pending reclaiming status (`{Stopped, [Released]}`) and billing will continue when the interface returns a successful call result. In the pending reclaiming status, the instance will be reclaimed and billing will stop after seven days.


<span id=".6K-35rGC6K-05piO"></span>
## Request description

To achieve low latency, it is recommended that you select the corresponding service address based on the region where your resources are located. For more information, refer to [service address](https://docs.byteplus.com/en/docs/cr/Service_address).


* Request method: POST

* Request URL: https://cr.cn\-beijing.byteplusapi.com.cn?Action=DeleteRegistry&Version=2022\-05\-12


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

When calling this API, in addition to the following request parameters, you also need to provide the public request parameters.  See [Public parameters](https://docs.byteplus.com/en/docs/cr/common-parameters) for details.


|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |DeleteRegistry |The API name. The current API's name is `DeleteRegistry`. |
|Version |String |Yes |2022\-05\-12 |The API version. The current version of the API is `2022-05-12`. |
|Name |String |Yes |example |The name of the Standard Edition instance to be deleted. On the **Instance List** page of the [Container Registry Console](https://console.byteplus.com/cr), get the Standard Edition instance name. |
|DeleteImmediately |Boolean |no |false |Indicates whether to immediately delete the Standard Edition instance:<br><br><br>* **false**: The instance enters a pending reclamation state `{Stopped, [Released]}`. It will be automatically and completely deleted after 7 days. Within these 7 days, it can be restored to the `{Running, [*]}` status by calling the [StartRegistry](https://docs.byteplus.com/en/docs/cr/startregistry) interface.<br><br>* **true**: The instance will be immediately and completely deleted, with no possibility of recovery. Default value **false**. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST https://cr.cn-beijing.byteplusapi.com.cn?Action=DeleteRegistry&Version=2022-05-12
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
        "Action": "DeleteRegistry",
        "Version": "2022-05-12",
        "Service": "cr",
        "Region": "cn-beijing"
    },
    "Result": {}
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

The error codes for this API are shown in the following table. For public error codes, refer to [public error codes](https://docs.byteplus.com/en/docs/cr/common-error-codes).


|**HTTP Status Code** |**Error code** |**Error Message** |**Descriptions** |
|---|---|---|---|
|400 |OperationDenied.Status |The action has been denied due to wrong status %s. |The specified operation is not allowed under the current access endpoint status. Please wait for the status transition to complete and try again. |
