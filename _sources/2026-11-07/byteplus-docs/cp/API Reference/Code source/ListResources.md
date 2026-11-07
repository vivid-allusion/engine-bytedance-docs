---
title: "ListResources"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/ListResources"
---

Code source list.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

To achieve low latency, it is recommended that you select the appropriate service address based on the region of your resources. For details, see [Service addresses](https://docs.byteplus.com/en/docs/cp/Service_Addresses).


* Request method: POST

* Request URL: https://cp.ap\-southeast\-1.byteplusapi.com.cn?Action=ListResources&Version=2023\-05\-01


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |ListResources |The API name. The current API is named `ListResources`. |
|Version |String |Yes |2023\-05\-01 |The API version. The current API version is `2023-05-01`. |
|WorkspaceId |String |Yes |000ce713ebd2487a9b4666c7ed81\*\*\*\* |Workspace ID. |
|PageNumber |Long |no |1 |The starting page number when querying. The default number is 1. |
|PageSize |Long |no |10 |The number of results per page:<br><br><br>* Minimum value: 1<br><br>* Maximum value: 100<br><br>* Default value: 10 |
|Filter |Object of [ResourceFilter](https://docs.byteplus.com/en/docs/292/73457#resourcefilter) |no |\- |Filter for the list of code sources to be queried. |


<span id="resourcefilter"></span>
### ResourceFilter


|**Parameter** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Types |Array of String |no |["Github"] |Code source type to query Possible values are:<br><br><br>* GitHub repository<br><br>* GitLab: GitLab code repository<br><br>* Gitee: Gitee code repository<br><br>* Gerrit: Gerrit code repository<br><br>* BitbucketCloud: BitbucketCloud code repository<br><br>* Git: General\-purpose Git\-based code repository<br><br>* Codeup: Codeup code repository |
|Name |String |no |github\-demo |Filter by code source name using fuzzy search. |
|Ids |Array of String |no |["1bfc821c23594ebbb7df1ae6b636\*\*\*\*"] |Filter by code source ID to perform an exact search. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST https://cp.ap-southeast-1.byteplusapi.com.cn?Action=ListResources&Version=2023-05-01 HTTP/1.1
Content-Type: application/json
{
    "WorkspaceId": "000ce713ebd2487a9b4666c7ed81****",
    "Filter": {
        "Types": [
            "Github"
        ],
        "Name": "github-demo",
        "Ids": [
            "1bfc821c23594ebbb7df1ae6b636****"
        ]
    }
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameter** |**Type** |**Sample Value** |**Description** |
|---|---|---|---|
|TotalCount |Long |10 |Total number of code sources. |
|Items |Array of [Resource](https://docs.byteplus.com/en/docs/292/73457#resource) |\- |Code source list. |
|PageNumber |Long |1 |The current page number. |
|PageSize |Long |10 |Number of single pages. |


<span id="resource"></span>
### Resource


|**Parameter** |**Type** |**Sample Value** |**Description** |
|---|---|---|---|
|Id |String |1bfc821c23594ebbb7df1ae6b636\*\*\*\* |Code source ID. |
|WorkspaceId |String |000ce713ebd2487a9b4666c7ed81\*\*\*\* |Workspace ID. |
|Name |String |test |The code source name. |
|Description |String |This is a description |A code source description. |
|Type |String |Gitee |The code source type. |
|Configuration |Object of [ResourceConfiguration](https://docs.byteplus.com/en/docs/292/73457#resourceconfiguration) |\- |Code source configuration information. |
|Creator |Object of [IAMUser](https://docs.byteplus.com/en/docs/292/73457#iamuser) |{<br><br>"AccountId": 24506499\*\*\*\*,<br><br>"UserId": 0<br><br>} |The code source creator. |
|CreateTime |String |2023\-05\-01T12:00:00+08:00 |The code source creation time. |
|UpdateTime |String |2023\-05\-01T12:02:00+08:00 |Last update time for code source. |


<span id="resourceconfiguration"></span>
### ResourceConfiguration


|**Parameter** |**Type** |**Sample Value** |**Description** |
|---|---|---|---|
|Git |Object of [GitConfiguration](https://docs.byteplus.com/en/docs/292/73457#gitconfiguration) |\- |Code source configuration information |


<span id="gitconfiguration"></span>
### GitConfiguration


|**Parameter** |**Type** |**Sample Value** |**Description** |
|---|---|---|---|
|Url |String |https://gitee.com/\*\*\*\* |Code repository URL. |
|UserToken |String |0f6832949f31ef77\*\*\*\* |User Token. |
|UserName |String |user |Username. |
|Password |String |pwd\*\*\*\* |Password. |
|CloneDepth |Long |0 |The default and minimum values for code clone depth are both 0. |
|AccessKey |String |qAfR\*\*\*\*\*\*\*\*\*\*\*\* |The AccessKey of the third\-party cloud. |
|SecretKey |String |Qtlc\*\*\*\*\*\*\*\*\*\*\*\* |Third\-party cloud SecretKey |


<span id="iamuser"></span>
### IAMUser


|**Parameter** |**Type** |**Sample Value** |**Description** |
|---|---|---|---|
|AccountId |Long |210048\*\*\*\* |account (main account) ID. |
|UserId |Long |28\*\*\*\* |IAM user ID |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
HTTP/1.1 200 OK
Content-Type: application/json
{
    "ResponseMetadata": {
        "RequestId": "20240402200758937550AAA43B9E05****",
        "Action": "ListResources",
        "Version": "2023-05-01",
        "Service": "cp",
        "Region": "ap-southeast-1",
    },
    "Result": {
        "Items": [
            {
                "Id": "1bfc821c23594ebbb7df1ae6b636****",
                "WorkspaceId": "000ce713ebd2487a9b4666c7ed81****",
                "Name": "test",
                "Type": "Gitee",
                "Configuration": {
                    "Git": {
                        "Url": "[https://gitee.com/](https://gitee.com/)****",
                        "UserToken": "0f6832949f31ef77****",
                        "CloneDepth": 0
                    }
                },
                "CreateTime": "2023-04-28T11:54:24+08:00",
                "UpdateTime": "2023-05-08T22:07:26+08:00",
                "Creator": {
                    "AccountId": 24506499****,
                    "UserId": 0
                }
            }
        ],
        "PageNumber": 1,
        "PageSize": 10,
        "TotalCount": 1
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

This API does not currently have dedicated error codes. If the API call returns an error, refer to [public error codes](https://docs.byteplus.com/en/docs/cp/Public_error_codes) to diagnose the issue.
