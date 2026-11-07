---
title: "CreateWorkspace"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/CreateWorkspace"
---

Create a workspace.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

To achieve low latency, it is recommended that you select the corresponding service address based on the Region where your resources are located. For details, see [Service Address](https://docs.byteplus.com/en/docs/cp/Service_Addresses).


* Request method: POST

* Request URL: https://cp.ap\-southeast\-1.byteplusapi.com.cn?Action=CreateWorkspace&Version=2023\-05\-01


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |CreateWorkspace |The API name. The current API is named `CreateWorkspace`. |
|Version |String |Yes |2023\-05\-01 |The API version. The current version of the API is `2023-05-01`. |
|Name |String |Yes |workspace\-demo |Workspace name.<br><br><br>* Any character is supported. The length must be between 2 and 50 characters.<br><br>* The name must be unique within the same account. |
|Description |String |no |Description |The workspace description can contain any characters, with a length limit of 0 to 256 characters. |
|Visibility |String |Yes |Specified |Workspace visibility options<br><br><br>* Account: Visible to all users<br><br>* Visible to specified users |
|VisibleUsers |Array of [IAMUser](https://docs.byteplus.com/en/docs/292/73441#iamuser) |no |[<br><br>{<br><br>"AccountId": 24506499\*\*\*\*,<br><br>"UserId": 0<br><br>}<br><br>] |Visible user list.<br><br>When workspace member visibility is set to Specified, you must further specify the visible users. A account (main account) is required. |


<span id="iamuser"></span>
### IAMUser


|**Parameter** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|AccountId |Long |no |210048\*\*\*\* |account (main account) ID. |
|UserId |Long |no |28\*\*\*\* |Sub\-user (IAM user) ID. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST https://cp.ap-southeast-1.byteplusapi.com.cn?Action=CreateWorkspace&Version=2023-05-01 HTTP/1.1
Content-Type: application/json
{
    "Name": "workspace-demo",
    "Description": "demo",
    "Visibility": "Specified",  
    "VisibleUsers": [
        {
            "AccountId": 24506499****,
            "UserId": 0
        }
    ]
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameter** |**Type** |**Sample Value** |**Description** |
|---|---|---|---|
|Id |String |2c7a85e4ac034eb790b096705694\*\*\*\* |Workspace ID. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
HTTP/1.1 200 OK
Content-Type: application/json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****10023228002****",
        "Action": "CreateWorkspace",
        "Version": "2023-05-01",
        "Service": "cp",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "Id": "2c7a85e4ac034eb790b096705694****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

The following table lists the error codes related to this interface and its business logic. For public error codes, see the [Public Error Codes](https://docs.byteplus.com/en/docs/cp/Public_error_codes) documentation.


|**HTTP Status Code** |**Error code** |**Error Message** |**Descriptions** |
|---|---|---|---|
|403 |Forbidden.{parameter} |The request is refused because it does not have access to Quota |Insufficient quota to create a workspace. Please purchase a package. |
