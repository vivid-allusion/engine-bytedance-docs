---
title: "UpdateServiceConnection"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/UpdateServiceConnection"
---

Update service connection

<span id=".6K-35rGC6K-05piO"></span>
## Request description

To achieve low latency, it is recommended that you select the corresponding service address based on the region where your resources are located. For details, refer to [service address](https://docs.byteplus.com/en/docs/cp/Service_Addresses).


* Request method: POST

* Request URL: https://cp.cn\-beijing.byteplusapi.com.cn?Action=UpdateServiceConnection&Version=2023\-05\-01


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Action |String |Ye |UpdateServiceConnection |The API name. The name of the current API is `UpdateServiceConnection`. |
|Version |String |Ye |2023\-05\-01 |The API version. The current version of the API is `2023-05-01`. |
|Id |String |Ye |my_svc_\*\*\*\* |Service connection ID. |
|Name |String |Ye |my\-gitlab\-updated |Service connection name. |
|Description |String |None |My GitLab service \- update |Service connection description. |
|URL |String |None |https://gitlab.com |Address information for the service connection. |
|Credential |Object of [CredentialConf](https://docs.byteplus.com/en/docs/292/73437#credentialconf) |None | |Credential information for the service connection. |
|IsAllWsShared |Boolean |Ye |true |Is the service connection shared by all workspaces? |
|SharedWorkspaceIds |Array of String |None |["ws\-789"] |List of shared workspace IDs of the service connection. |
|DisableNetworkVerify |Boolean |None |false |Whether to ignore public network validation. |


<span id="credentialconf"></span>
### CredentialConf


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Token |String |None |glpat\*\*\* |Service connection credentials. |
|Password |String |None |password\*\*\* |The password of the service connection credential. |
|Username |String |None |test\-user |The username for the service connection credential. |
|AccessKey |String |None |AKIAIOS\*\*\* |AccessKey for service connection credentials. |
|SecretKey |String |None |wJalrXUtnFEMINGPxRfiCY\*\*\* |SecretKey of the service connection credential. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST https://cp.cn-beijing.byteplusapi.com.cn?Action=UpdateServiceConnection&Version=2023-05-01 HTTP/1.1
Content-Type: application/json
{
    "Id": "my_svc_****",
    "IsAllWsShared": true,
    "Name": "my-gitlab-new",
    "Credential": {
        "Token": "ghtsdjfk****",
        "Username": null,
        "Password": null,
        "AccessKey": null,
        "SecretKey": null
    }
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This API has no special response parameters.

<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```json
HTTP/1.1 200 OK
Content-Type: application/json
{
    "ResponseMetadata": {
        "RequestId": "20250916181442B5D71AE63B718DE9****",
        "Action": "UpdateServiceConnection",
        "Version": "2023-05-01",
        "Service": "cp",
        "Region": "cn-beijing"
    },
    "Result": {}
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

There are currently no independent error codes for this API. If an exception occurs during API invocation, refer to the [public error code](https://docs.byteplus.com/en/docs/cp/Public_error_codes) for troubleshooting.
