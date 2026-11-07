---
title: "GetServiceConnection"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/GetServiceConnection"
---

Query service connection details

<span id=".6K-35rGC6K-05piO"></span>
## Request description

To achieve low latency, it is recommended that you select the corresponding service address based on the region where your resources are located. For details, refer to [service address](https://docs.byteplus.com/en/docs/cp/Service_Addresses).


* Request method: POST

* Request URL: https://cp.ap\-southeast\-1.byteplusapi.com.cn?Action=GetServiceConnection&Version=2023\-05\-01


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Action |String |Ye |GetServiceConnection |The API name. The name of the current API is `GetServiceConnection`. |
|Version |String |Ye |2023\-05\-01 |The API version. The current version of the API is `2023-05-01`. |
|Id |String |Ye |my_svc_\*\*\*\* |Service connection ID. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST https://cp.ap-southeast-1.byteplusapi.com.cn?Action=GetServiceConnection&Version=2023-05-01 HTTP/1.1
Content-Type: application/json
{
    "Id": "my_svc_****"
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Id |String |svc\-connect\*\*\*\* |Service connection ID. |
|Name |String |my\-gitlab |Service connection name. |
|Description |String |My GitLab service |Service connection description. |
|Category |String |CodeRepo |Service connection category:<br><br><br>* Registry: Artifact repository category.<br><br>* CodeRepo: Code source category. |
|Type |String |Gitlab |Type of service connection: supported values are as follows.<br><br><br>* `DockerRegistry`<br><br>* `ArtifactRegistry`<br><br>* `Github`<br><br>* `Gitlab`<br><br>* `Gitee`<br><br>* `BitbucketCloud`<br><br>* `Codeup`<br><br>* `PrivateGitLab`<br><br>* `BitbucketServer`<br><br>* `Gerrit`<br><br>* `Git`<br><br>* `Perforce`<br><br>* `Codebase`<br><br>* `Coding`<br><br>* `GitCode` |
|URL |String |https://gitlab.com |Address information for the service connection. |
|Credential |Object of [CredentialConf](https://docs.byteplus.com/en/docs/292/73438#credentialconf) | |Credential information for the service connection. |
|IsAllWsShared |Boolean |false |Is the service connection shared across all workspaces? |
|SharedWorkspaceIds |Array of String |["ws\-123", "ws\-456"] |List of shared workspace IDs for service connection. |
|Creator |Object of [IAMUser](https://docs.byteplus.com/en/docs/292/73438#iamuser) | |Service connection creator. |
|CreateTime |String |2024\-01\-01T00:00:00+08:00 |Service connection creation time. |
|UpdateTime |String |2024\-01\-01T00:00:00+08:00 |Service connection update time. |
|PipelineBinding |Boolean |false |Whether the service connection is bound to the pipeline. |


<span id="credentialconf"></span>
### CredentialConf


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Token |String |glpat\*\*\* |Service connection credentials. |
|Password |String |password\*\*\* |Password for the service connection credential. |
|Username |String |test\-user |Username for the service connection credential. |
|AccessKey |String |AKIAIOS\*\*\* |AccessKey for the service connection credential. |
|SecretKey |String |wJalrXUtnFEMINGPxRfiCY\*\*\* |SecretKey of the service connection credential. |


<span id="iamuser"></span>
### IAMUser


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|AccountId |Long |210048\*\*\*\* |BytePlus account (root user) ID. |
|UserId |Long |28\*\*\*\* |IAM user (IAM user) ID. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```json
HTTP/1.1 200 OK
Content-Type: application/json
{
    "ResponseMetadata": {
        "RequestId": "2025091618070703C4D63B357BB082****",
        "Action": "GetServiceConnection",
        "Version": "2023-05-01",
        "Service": "cp",
        "Region": "ap-southeast-1"
    },
    "Result": {
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
        "UpdateTime": "2025-09-16T17:28:57+08:00",
        "PipelineBinding": false
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

This interface currently does not have independent error codes. If an exception occurs when calling the interface, you can refer to the [public error codes](https://docs.byteplus.com/en/docs/cp/Public_error_codes) for troubleshooting.
