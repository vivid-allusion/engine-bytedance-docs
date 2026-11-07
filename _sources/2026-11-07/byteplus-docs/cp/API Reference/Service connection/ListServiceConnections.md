---
title: "ListServiceConnections"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/ListServiceConnections"
---

Query the service connection list

<span id=".6K-35rGC6K-05piO"></span>
## Request description

To achieve low latency, it is recommended that you select the corresponding service address based on the region where your resources are located. For details, refer to [service address](https://docs.byteplus.com/en/docs/cp/Service_Addresses).


* Request method: POST

* Request URL: https://cp.ap\-southeast\-1.byteplusapi.com.cn?Action=ListServiceConnections&Version=2023\-05\-01


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Action |String |Ye |ListServiceConnections |The API name. The name of the current API is `ListServiceConnections`. |
|Version |String |Ye |2023\-05\-01 |The API version. The current version of the API is `2023-05-01`. |
|PageNumber |Long |None |1 |The current page number. |
|PageSize |Long |None |10 |Number of single pages. |
|Filter |Object of [SCFilter](https://docs.byteplus.com/en/docs/292/73429#scfilter) |None | |Filtering parameters for service connection. |


<span id="scfilter"></span>
### SCFilter


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Ids |Array of String |None |["svc\-connect\-\*\*\*"] |List of service connection IDs. |
|Name |String |None |my |The name of the service connection supports fuzzy matching. |
|TypeInfo |Object of [FilterTypeInfo](https://docs.byteplus.com/en/docs/292/73429#filtertypeinfo) |None | |Type information for the service connection. |
|WorkspaceId |String |None |ws\*\*\*\* |The shared workspace ID of the service connection. |


<span id="filtertypeinfo"></span>
### FilterTypeInfo


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Type |String |None |Gitlab |Supported values for Service connection type are as follows.<br><br><br>* `DockerRegistry`<br><br>* `ArtifactRegistry`<br><br>* `Github`<br><br>* `Gitlab`<br><br>* `Gitee`<br><br>* `BitbucketCloud`<br><br>* `Codeup`<br><br>* `PrivateGitLab`<br><br>* `BitbucketServer`<br><br>* `Gerrit`<br><br>* `Git`<br><br>* `Perforce`<br><br>* `Codebase`<br><br>* `Coding`<br><br>* `GitCode` |
|Category |String |None |CodeRepo |Service connection categories:<br><br><br>* Registry: Artifact repository category.<br><br>* CodeRepo: Code source category. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST https://cp.ap-southeast-1.byteplusapi.com.cn?Action=ListServiceConnections&Version=2023-05-01 HTTP/1.1
Content-Type: application/json
{
    "PageNumber": 1,
    "PageSize": 10,
    "Filter": {
        "Name": "my"
    }
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Total |Long |100 |Total number of service connections. |
|PageNumber |Long |1 |The current page number. |
|PageSize |Long |10 |Number of pages. |
|Items |Array of [ServiceConnection](https://docs.byteplus.com/en/docs/292/73429#serviceconnection) | |Service connection list. |


<span id="serviceconnection"></span>
### ServiceConnection


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Id |String |svc\-connect\*\*\*\* |Service connection ID. |
|URL |String |https://gitlab.com |Address information for the service connection. |
|Name |String |my\-gitlab |Address information for the service connection. |
|Type |String |Gitlab |The type of Service connection and the supported values are as follows.<br><br><br>* `DockerRegistry`<br><br>* `ArtifactRegistry`<br><br>* `Github`<br><br>* `Gitlab`<br><br>* `Gitee`<br><br>* `BitbucketCloud`<br><br>* `Codeup`<br><br>* `PrivateGitLab`<br><br>* `BitbucketServer`<br><br>* `Gerrit`<br><br>* `Git`<br><br>* `Perforce`<br><br>* `Codebase`<br><br>* `Coding`<br><br>* `GitCode` |
|Creator |Object of [IAMUser](https://docs.byteplus.com/en/docs/292/73429#iamuser) | |Service connection creator. |
|Category |String |CodeRepo |Service connection categories:<br><br><br>* Registry: Artifact repository category.<br><br>* CodeRepo: Code source category. |
|CreateTime |String |2024\-01\-01T00:00:00+08:00 |Service connection creation time. |
|Credential |Object of [CredentialConf](https://docs.byteplus.com/en/docs/292/73429#credentialconf) | |Service connection credential information. |
|UpdateTime |String |2024\-01\-01T00:00:00+08:00 |The service connection update time. |
|Description |String |My GitLab service |Service connection description. |
|IsAllWsShared |Boolean |false |Is the service connection shared across all workspaces? |
|PipelineBinding |Boolean |false |Is the service connection bound to the pipeline? |
|SharedWorkspaceIds |Array of String |["ws\-123", "ws\-456"] |List of shared workspace IDs for service connection. |


<span id="iamuser"></span>
### IAMUser


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|AccountId |Long |210048\*\*\*\* |BytePlus root user ID. |
|UserId |Long |28\*\*\*\* |IAM user (IAM user) ID. |


<span id="credentialconf"></span>
### CredentialConf


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Token |String |glpat\*\*\* |Service connection credential. |
|Password |String |password\*\*\* |Password for the service connection credential. |
|Username |String |test\-user |Username for service connection credentials. |
|AccessKey |String |AKIAIOS\*\*\* |AccessKey for the service connection credential. |
|SecretKey |String |wJalrXUtnFEMINGPxRfiCY\*\*\* |SecretKey of the service connection credential. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```json
HTTP/1.1 200 OK
Content-Type: application/json
{
    "ResponseMetadata": {
        "RequestId": "202509161802522086048CF4D6121C****",
        "Action": "ListServiceConnections",
        "Version": "2023-05-01",
        "Service": "cp",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "Total": 1,
        "PageNumber": 1,
        "PageSize": 10,
        "Items": [
            {
                "Id": "my_svc_****",
                "Name": "my-gitlab",
                "Description": null,
                "Category": "CodeRepo",
                "Type": "Gitlab",
                "Credential": {},
                "IsAllWsShared": true,
                "Creator": {
                    "AccountId": 210048****,
                    "UserId": ****
                },
                "CreateTime": "2025-09-16T17:28:57+08:00",
                "UpdateTime": "2025-09-16T17:28:57+08:00"
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

There are currently no independent error codes for this interface. If an exception occurs when calling the interface, you can refer to the [public error codes](https://docs.byteplus.com/en/docs/cp/Public_error_codes) for troubleshooting.
