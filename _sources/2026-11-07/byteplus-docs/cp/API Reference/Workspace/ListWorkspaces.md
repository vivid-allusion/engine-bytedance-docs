---
title: "ListWorkspaces"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/ListWorkspaces"
---

Query workspaces

<span id=".6K-35rGC6K-05piO"></span>
## Request description

For low latency, select the service address that corresponds to the Region where your resources are located. For details, see [Service addresses](https://docs.byteplus.com/en/docs/cp/Service_Addresses).


* Request method: POST

* Request URL: https://cp.ap\-southeast\-1.byteplusapi.com.cn?Action=ListWorkspaces&Version=2023\-05\-01


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |ListWorkspaces |The API name. The name of the current API is `ListWorkspaces`. |
|Version |String |Yes |2023\-05\-01 |The API version. The current version of the API is `2023-05-01`. |
|PageNumber |Long |no |1 |The starting page number when querying. The default number is 1. |
|PageSize |Long |no |10 |The number of results per page:<br><br><br>* Minimum value: 1<br><br>* Maximum value: 100<br><br>* Default value: 10 |
|Filter |Object of [WorkspaceFilter](https://docs.byteplus.com/en/docs/292/73451#workspacefilter) |no |\- |Filter criteria for the workspace being queried. |


<span id="workspacefilter"></span>
### WorkspaceFilter


|**Parameter** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Name |String |no |work |Filter workspace names using fuzzy search. |
|Ids |Array of String |no |["2c7a85e4ac034eb790b096705694\*\*\*\*"] |Filter by workspace ID to perform an exact search. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST https://cp.ap-southeast-1.byteplusapi.com.cn?Action=ListWorkspaces&Version=2023-05-01 HTTP/1.1
Content-Type: application/json
{
    "PageNumber": 1,
    "PageSize": 10,
    "Filter": {
        "Name": "work",
        "Ids": [
            "2c7a85e4ac034eb790b096705694****"
        ]
    }
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameter** |**Type** |**Sample Value** |**Description** |
|---|---|---|---|
|TotalCount |Long |20 |Total number of workspaces. |
|Items |Array of [Workspace](https://docs.byteplus.com/en/docs/292/73451#workspace) |\- |Workspace list. |
|PageNumber |Long |1 |The current page number. |
|PageSize |Long |10 |Number of single pages. |


<span id="workspace"></span>
### Workspace


|**Parameter** |**Type** |**Sample Value** |**Description** |
|---|---|---|---|
|Id |String |18be9d623fba45a1aca409f5e19c\*\*\*\* |Workspace ID. |
|Name |String |workspace\-test |The workspace name. |
|Description |String |A description |The workspace description. |
|Creator |Object of [IAMUser](https://docs.byteplus.com/en/docs/292/73451#iamuser) |{<br><br>"AccountId": 24506499\*\*\*\*,<br><br>"UserId": 0<br><br>} |The workspace creator. |
|Visibility |String |Specified |Workspace visibility for members<br><br><br>* Account: Visible to all users<br><br>* Specified: Visible to designated users |
|VisibleUsers |Array of [IAMUser](https://docs.byteplus.com/en/docs/292/73451#iamuser) |[<br><br>{<br><br>"AccountId": 24506499\*\*\*\*,<br><br>"UserId": 0<br><br>},<br><br>{<br><br>"AccountId": 24506499\*\*\*\*,<br><br>"UserId": 1454\*\*\*<br><br>}<br><br>] |When the "Visible to members" setting for the workspace is set to "Specified", the list of visible users will then be displayed. |
|CreateTime |String |2023\-05\-10T14:11:28+08:00 |Workspace creation time. |
|UpdateTime |String |2023\-05\-10T14:11:28+08:00 |The workspace update time. |


<span id="iamuser"></span>
### IAMUser


|**Parameter** |**Type** |**Sample Value** |**Description** |
|---|---|---|---|
|AccountId |Long |210048\*\*\*\* |account (main account) ID. |
|UserId |Long |28\*\*\*\* |Sub\-user (IAM user) ID. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
HTTP/1.1 200 OK
Content-Type: application/json
{
    "ResponseMetadata": {
        "RequestId": "202404031430323BAEA57387980A0B****",
        "Action": "ListWorkspaces",
        "Version": "2023-05-01",
        "Service": "cp",
        "Region": "ap-southeast-1",
    },
    "Result": {
        "TotalCount": 1,
        "PageNumber": 1,
        "PageSize": 10,
        "Items": [
            {
                "Id": "18be9d623fba45a1aca409f5e19c****",
                "Name": "workspace-test",
                "CreateTime": "2023-05-10T14:11:28+08:00",
                "UpdateTime": "2023-05-10T14:11:28+08:00",
                "Creator": {
                    "AccountId": 24506499****,
                    "UserId": 0
                },
                "Visiblity": "Specified",
                "VisibleUsers": [
                    {
                        "AccountId": 24506499****,
                        "UserId": 0
                    },
                    {
                        "AccountId": 24506499****,
                        "UserId": 1454***
                    }
                ]
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

This API does not currently have independent error codes. If an exception is returned when calling the API, you can refer to [public error codes](https://docs.byteplus.com/en/docs/cp/Public_error_codes) for troubleshooting.
