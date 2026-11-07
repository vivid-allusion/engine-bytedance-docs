---
title: "GrantPermission"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/GrantPermission"
---

Granting RBAC access permission to an IAM user or role.

<span id=".5o6l5Y-j6K-05piO"></span>
## API description

By default, users who did not create the VKE cluster have no RBAC (Role\-Based Access Control) permission within it. You can call the GrantPermission API to grant RBAC access permissions to IAM users or roles, including accessible resources, scope of permission, and built\-in role type, to better manage the security and access control of the cluster.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

VKE has deployed services in multiple regions globally to provide a stable and low\-latency access experience. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/vke/Service_addresses) topic and select the most suitable access point for your business region.


* Request method: POST

* Request URL: https://vke.cn\-beijing.byteplusapi.com.cn?Action=GrantPermission&Version=2022\-05\-12


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=GrantPermission&serviceCode=vke&version=2022-05-12&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table describes the API request parameters. You also need to provide public parameters when calling this API. See [Public parameters](https://docs.byteplus.com/en/docs/vke/Common-parameters) for details.


|Parameters |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Action |String |Yes |GrantPermission |The API name. The API name is `GrantPermission `. |
|Version |String |Yes |2022\-05\-12 |The API version. The current version of the API is `2022-05-12`. |
|RoleDomain |String |no |cluster |The permission type granted to an IAM user or role:<br><br><br>* **Namespace ** : Grants permission at the namespace level.<br><br>* **Cluster ** : Grants permission at the cluster level.<br><br>* **all_clusters ** : Grants all the permissions available at the cluster level under the current account. |
|ClusterId |String |no |ccog93v\*\*\*\*\*\*\* |The cluster ID that an IAM user or role can access. Cluster IDs can be obtained by calling the [ListClusters](https://docs.byteplus.com/en/docs/vke/ListClusters) API.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div><br><br><br><div data-tips="true" data-tips-type="warning">This parameter is required if the <code>roleDomain</code> is set to <code>namespace</code> or <code>cluster </code>.</div><br> |
|Namespace |String |no |default |The namespace that an IAM user or role can access. You can log in to the [VKE console ](https://console.byteplus.com/vke) to view namespace names.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">This parameter is required if the <code>RoleDomain </code>is set to <code>namespace </code>.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">This parameter does not take effect if <code>roleDomain</code> is not set to <code>namespace</code>.</div><br> |
|RoleName |String |no |vke:admin |The name of RBAC role that can be granted. The available RBAC permissions include:<br><br><br>* Customization of role name: You can customize a role name without any restrictions on the format and string composition on VKE side, as long as it meets Kubernetes specifications.<br><br>* System built\-in role name: For the built\-in RBAC role names, see [Description of RBAC permission role  ](https://docs.byteplus.com/en/docs/vke/RBAC-roles).<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">This parameter is required.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">A custom role name is not allowed if <code>roleDomain </code>is set to <code>all_clusters</code>.</div><br> |
|IsCustomRole |Boolean |no |false |Whether it is a custom RBAC role:<br><br><br>* **True**: Custom role.<br><br>* **False**: (Default) A built\-in role of the system. |
|GranteeId |Long |no |153\*\*\*\*\*\* |The ID of the authorized target. It can be an IAM user ID or an IAM role ID. IDs can be fetched by calling [ListUsers](https://docs.byteplus.com/en/docs/byteplus-platform/reference-listusers) or [ListRoles](https://docs.byteplus.com/en/docs/byteplus-platform/reference-listroles) API.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div><br><br><br><div data-tips="true" data-tips-type="warning">This parameter is required.</div><br> |
|GranteeType |String |no |User |The types of targets to be authorized:<br><br><br>* **User**: IAM user.<br><br>* **Role**: IAM role. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST /?Action=GrantPermission&Version=2022-05-12 HTTP/1.1
Content-Type: application/json
{
    "RoleDomain": "cluster",
    "ClusterId": "ccog93v*******",
    "Namespace": "default",
    "RoleName": "vke:admin",
    "IsCustomRole": true,
    "GranteeId": 1**,
    "GranteeType": "User"
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following table contains the response parameters of this API. See [Response results](https://docs.byteplus.com/en/docs/vke/Response) for details about public response parameters.


|Parameters |Type |Sample value |Description |
|---|---|---|---|
|Id |String |ap\*\*\*\*\*\*\*\* |The ID of the RBAC policy.<br><br>It will be wise to keep a copy of the ID for later use, e.g., making queries or changes to RBAC access policies. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420********",
        "Action": "GrantPermission",
        "Version": "2022-05-12",
        "Service": "vke",
        "Region": "cn-beijing"
    },
    "Result": {
        "Id": "ap********"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

There are no error codes proprietary to this API. See [Public error codes](https://docs.byteplus.com/en/docs/vke/Common-error-codes) for details.

&nbsp;
