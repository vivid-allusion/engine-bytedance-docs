---
title: "UpdateTask"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/UpdateTask"
---

Update a task in the VKE cluster.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

VKE has deployed services in multiple regions globally to provide a stable and low\-latency access experience. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/vke/Service_addresses) topic and select the most suitable access point based on the region where your business is located.


* Request method: POST

* Request URL: https://vke.cn\-beijing.byteplusapi.com.cn?Action=UpdateTask&Version=2022\-05\-12


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=UpdateTask&serviceCode=vke&version=2022-05-12&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameter

The following table describes the API request parameters. You also need to provide public parameters when calling this API. For details about public request parameters, see [Public parameters](https://docs.byteplus.com/en/docs/vke/Common-parameters).


|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |UpdateTask |The API name. The current API name is `UpdateTask`. |
|Version |String |Yes |2022\-05\-12 |The API version. The current version of the API is `2022-05-12`. |
|Id |String |Yes |tcax\*\*\*\*\*\* |Task ID.<br><br>You can call [ListTasks](https://docs.byteplus.com/en/docs/vke/ListTasks) to get the task ID. |
|Status |String |No |Running |Task status. Valid values:<br><br><br>* **Running**: It is running.<br><br>* **Succeeded**: Succeeded<br><br>* **Failed**: Failed<br><br>* **Aborted**: Aborted<br><br>* **Paused**: Paused<br><br>* **Pending**: Pending<br><br>* **Approving**: Approving<br><br>* **Waiting**: Waiting to be executed |
|Operation |String |No |Pause |Task control operations. Valid values:<br><br><br>* **Pause**: Pause the task<br><br>* **Resume**: Resume the task<br><br>* **Abort**: Abort the task |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```JSON
POST https://vke.cn-beijing.byteplusapi.com.cn?Action=UpdateTask&Version=2022-05-12
Content-Type: application/json
{
    "Id": "tcax******",
    "Status": "Running",
    "Operation": "Pause"
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter

The following table contains the response parameters of this API. See [Response results](https://docs.byteplus.com/en/docs/vke/Response) for details about public response parameters.


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Id |String |tcax\*\*\*\*\*\* |Task ID. |
|Status |String |Running |Task status. Valid values:<br><br><br>* **Running**: It is running.<br><br>* **Succeeded**: Succeeded<br><br>* **Failed**: Failed<br><br>* **Aborted**: Aborted<br><br>* **Paused**: Paused<br><br>* **Pending**: Pending<br><br>* **Approving**: Approving<br><br>* **Waiting**: Waiting to be executed |
|Operation |String |Pause |Task control operations. Valid values:<br><br><br>* **Pause**: Pause the task<br><br>* **Resume**: Resume the task<br><br>* **Abort**: Abort the task |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420**********",
        "Action": "UpdateTask",
        "Version": "2022-05-12",
        "Service": "vke",
        "Region": "cn-beijing"
    },
    "Result": {
        "Id": "tcax******",
        "Status": "Running",
        "Operation": "Pause"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

There are no proprietary error codes for this API. See [Public error codes](https://docs.byteplus.com/en/docs/vke/Common-error-codes) for details about public error codes.
