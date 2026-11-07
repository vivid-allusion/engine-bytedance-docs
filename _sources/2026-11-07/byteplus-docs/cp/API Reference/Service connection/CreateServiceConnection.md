---
title: "CreateServiceConnection"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/CreateServiceConnection"
---

Create service connection

<span id=".6K-35rGC6K-05piO"></span>
## Request description

To achieve low latency, it is recommended that you select the corresponding service address based on the region where your resources are located. For details, refer to [service address](https://docs.byteplus.com/en/docs/cp/Service_Addresses).


* Request method: POST

* Request URL: https://cp.ap\-southeast\-1.byteplusapi.com.cn?Action=CreateServiceConnection&Version=2023\-05\-01


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Action |String |Ye |CreateServiceConnection |The API name. The name of the current API is `CreateServiceConnection`. |
|Version |String |Ye |2023\-05\-01 |The API version. The current version of the API is `2023-05-01`. |
|Id |String |Ye |my_svc_con\*\*\*\* |Service connection ID. |
|Name |String |Ye |my\-gitlab |Service connection name. |
|Description |String |None |My GitLab service |Service connection description. |
|Type |String |Ye |Gitlab |Type of Service connection: supported values are as follows.<br><br><br>* `DockerRegistry`<br><br>* `ArtifactRegistry`<br><br>* `Github`<br><br>* `Gitlab`<br><br>* `Gitee`<br><br>* `BitbucketCloud`<br><br>* `Codeup`<br><br>* `PrivateGitLab`<br><br>* `BitbucketServer`<br><br>* `Gerrit`<br><br>* `Git`<br><br>* `Perforce`<br><br>* `Codebase`<br><br>* `Coding`<br><br>* `GitCode` |
|URL |String |None |https://gitlab.com |Address information for the service connection. |
|Credential |Object of [CredentialConf](https://docs.byteplus.com/en/docs/292/73440#credentialconf) |Ye | |Credential information for the service connection. |
|IsAllWsShared |Boolean |Ye |false |Is the service connection shared across all workspaces? |
|SharedWorkspaceIds |Array of String |None |["ws\-123", "ws\-456"] |List of shared workspace IDs for the service connection. |
|DisableNetworkVerify |Boolean |None |false |Whether to ignore public network verification. |


<span id="credentialconf"></span>
### CredentialConf


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Token |String |None |glpat\*\*\* |Service connection credentials. |
|Password |String |None |password\*\*\* |Password for the service connection credential. |
|Username |String |None |test\-user |Username of the service connection credential. |
|AccessKey |String |None |AKIAIOS\*\*\* |AccessKey for the service connection credential. |
|SecretKey |String |None |wJalrXUtnFEMINGPxRfiCY\*\*\* |SecretKey of the service connection credential. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST https://cp.ap-southeast-1.byteplusapi.com.cn?Action=CreateServiceConnection&Version=2023-05-01 HTTP/1.1
Content-Type: application/json
{
    "Type": "Gitlab",
    "Id": "svc-connect****",
    "IsAllWsShared": true,
    "Name": "my-gitlab",
    "Credential": {
        "Token": "glpat***"
    }
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|Id |String |svc\-connect\*\*\*\* |Service connection ID |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```json
HTTP/1.1 200 OK
Content-Type: application/json
{
    "ResponseMetadata": {
        "RequestId": "20250916172852F58BD2C7CA225D28****",
        "Action": "CreateServiceConnection",
        "Version": "2023-05-01",
        "Service": "cp",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "Id": "svc-connect****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

There are currently no dedicated error codes for this API. If an exception occurs during an API call, you can refer to the [public error code](https://docs.byteplus.com/en/docs/cp/Public_error_codes) for troubleshooting.
