---
title: "UpdateWorkspace"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/UpdateWorkspace"
---

Update the workspace.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

To achieve low latency, it is recommended that you select the corresponding service address based on the Region where your resources are located. For details, see [Service address](https://docs.byteplus.com/en/docs/cp/Service_Addresses).


* Request method: POST

* Request URL: https://cp.ap\-southeast\-1.byteplusapi.com.cn?Action=UpdateWorkspace&Version=2023\-05\-01


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |UpdateWorkspace |The API name. The name of the current API is `UpdateWorkspace`. |
|Version |String |Yes |2023\-05\-01 |The API version. The current version of the API is `2023-05-01`. |
|Id |String |Yes |18be9d623fba45a1aca409f5e19c\*\*\*\* |Workspace ID. |
|Name |String |no |workspace\-demo |The workspace name.<br><br><br>* Any character is supported. Length is limited to 2–50 characters.<br><br>* The name must be unique within the same account. |
|Description |String |no |This is a description. |Workspace description. Supports any characters, with a length limit of 0 to 256 characters. |
|Visibility |String |no |Account |Workspace member visibility<br><br><br>* Account: Visible to all users<br><br>* Specified: Visible to specified users |
|VisibleUsers |Array of [IAMUser](https://docs.byteplus.com/en/docs/292/73459#iamuser) |no |[<br><br>{<br><br>"AccountId": 24506499\*\*\*\*,<br><br>"UserId": 0<br><br>}<br><br>] |Visible to users. When the workspace visibility for members is set to "Specified", you must specify which users are visible. A account (main account) is required. |


<span id="iamuser"></span>
### IAMUser


|**Parameter** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|AccountId |Long |no |210048\*\*\*\* |account (main account) ID. |
|UserId |Long |no |28\*\*\*\* |Sub\-user (IAM user) ID. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST https://cp.ap-southeast-1.byteplusapi.com.cn?Action=UpdateWorkspace&Version=2023-05-01 HTTP/1.1
Content-Type: application/json
{
    "Id": "2c7a85e4ac034eb790b096705694****",
    "Name": "workspace-demo",
    "Description": "test",
    "Visibility": "Account"
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This interface does not have any unique return parameters.

<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
HTTP/1.1 200 OK
Content-Type: application/json
{
    "ResponseMetadata": {
        "RequestId": "202404031138595E5D8BD124299EB9****",
        "Action": "UpdateWorkspace",
        "Version": "2023-05-01",
        "Service": "cp",
        "Region": "ap-southeast-1"
    },
    "Result": {}
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

This API does not currently have independent error codes. If an exception occurs during API calls, refer to [the public error codes](https://docs.byteplus.com/en/docs/cp/Public_error_codes) for troubleshooting.
