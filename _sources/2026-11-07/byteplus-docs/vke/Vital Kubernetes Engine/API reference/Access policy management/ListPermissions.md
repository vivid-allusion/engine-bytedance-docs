---
title: "ListPermissions"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/ListPermissions"
---

Making queries to find RBAC access policy resources that meet the conditions.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

VKE has deployed services in multiple regions globally to provide a stable and low\-latency access experience. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/vke/Service_addresses) topic and select the most suitable access point for your business region.


* Request method: POST

* Request URL: https://vke.cn\-beijing.byteplusapi.com.cn?Action=ListPermissions&Version=2022\-05\-12


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=ListPermissions&serviceCode=vke&version=2022-05-12&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table contains the API request parameters. You also need to provide public parameters when calling this API. See [Public parameters](https://docs.byteplus.com/en/docs/vke/Common-parameters) for details.


|Parameters |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Action |String |Yes |ListPermissions |The API name. The API name is `ListPermissions `. |
|Version |String |Yes |2022\-05\-12 |The API version. The current version of the API is `2022-05-12`. |
|Filter |Object of [ListPermissionsFilter](https://docs.byteplus.com/en/docs/vke/ListPermissions#listpermissionsfilter) |no |\- |The filter conditions for policy resources. |
|PageNumber |Integer |no |1 |The starting page number when querying. The default number is 1. |
|PageSize |Integer |no |10 |The number of results per page:<br><br><br>* Minimum value: 1<br><br>* Maximum value: 100<br><br>* Default value: 10 |


&nbsp;


|Parameters |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Action |String |Yes |ListPermissions |The API name. The API name is `ListPermissions `. |
|Version |String |Yes |2022\-05\-12 |The API version. The current version of the API is `2022-05-12`. |
|Filter |Object of [ListPermissionsFilter](https://docs.byteplus.com/en/docs/vke/ListPermissions#listpermissionsfilter) |no |\- |The filter conditions for policy resources. |
|PageNumber |Integer |no |1 |The starting page number when querying. The default number is 1. |
|PageSize |Integer |no |10 |The number of results per page:<br><br><br>* Minimum value: 1<br><br>* Maximum value: 100<br><br>* Default value: 10 |


<span id="listpermissionsfilter"></span>
### ListPermissionsFilter


|Parameters |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Ids |Array of String |no |["ap\*\*\*\*\*\*12"] |A list of the IDs for the RBAC permission policy resources. The IDs of the RBAC policies can be fetched by calling the [GrantPermission](https://docs.byteplus.com/en/docs/vke/GrantPermission) API.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">100 resource IDs can be included at most in a single query.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Leaving it empty indicates all the RBAC permission policy resources under the account.</div><br> |
|Status |String |no |Success |The status of the RBAC permission policy resource.<br><br><br>* **Success**: Applied successfully.<br><br>* **Failed ** : Failed to apply.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The logic OR is applied to represent relations among multiple statuses.</div><br> |
|RoleNames |Array of String |no |["vke:admin"] |A list of RBAC role names given to the authorized targets:<br><br><br>* Custom role name: A custom role name.<br><br>* System built\-in role name: For the built\-in RBAC role names, see[ Description of RBAC permission role](https://docs.byteplus.com/en/docs/vke/RBAC-roles).<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Up to 100 RBAC role names can be included in a single query.</div><br> |
|ClusterIds |Array of String |no |[ccog93v\*\*\*\*\*\*\*] |A list of cluster IDs with which the RBAC permission policy resource is bound. Cluster IDs can be fetched by calling [ListClusters](https://docs.byteplus.com/en/docs/vke/ListClusters) API.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">100 cluster IDs can be included at most in a single query.</div><br> |
|GranteeIds |Array of Long |no |[153\*\*\*\*\*\*] |The ID of the authorized target. It is an IAM user ID by default. You can also use an IAM role ID. |
|Namespaces |Array of String |no |["default"] |A list of namespaces with which the RBAC permission policy resource is bound. You can log in to the [VKE console ](https://console.byteplus.com/vke)and view namespace names. |
|GranteeType |String |no |User |The types of targets to be authorized:<br><br><br>* **User**: IAM user.<br><br>* **Role**: IAM role. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST /?Action=ListPermissions&Version=2022-05-12 HTTP/1.1
Content-Type: application/json
{
    "Filter": {
        "Ids": [
            "ap******12"
        ],
        "Status": "Success",
        "RoleNames": [
            "vke: admin"
        ],
        "Namespaces": [
            "default"
        ],
        "GranteeType": "User"
    },
    "PageNumber": 1,
    "PageSize": 10
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following table contains the response parameters of this API. See [Response results](https://docs.byteplus.com/en/docs/vke/Response) for details about public response parameters.


|Parameters |Type |Sample value |Description |
|---|---|---|---|
|Items |Array of [AccessPolicy](https://docs.byteplus.com/en/docs/vke/ListPermissions#accesspolicy) |\- |A list of the RBAC access policy resources. |
|TotalCount |Integer |1 |Total number of the RBAC permission policy resources that meet the query conditions. |
|PageSize |Integer |10 |The number of RBAC permission policy resources displayed per page. |
|PageNumber |Integer |1 |The current page number. |


<span id="accesspolicy"></span>
### AccessPolicy


|Parameters |Type |Sample value |Description |
|---|---|---|---|
|Id |String |ap\*\*\*\*\*\*\*\* |The ID of the RBAC permission policy resource. |
|Status |String |Succeeded |The status of the RBAC permission policy resource. Valid values:<br><br><br>* **Success**: Applied.<br><br>* **Failed**: Failed to apply. |
|Message |String |AccessDenied In Cluster A |Details of authorization. |
|RoleName |String |vke:admin |The RBAC role name given to the authorized target. For the built\-in RBAC role names, see [Description of RBAC permission role](https://docs.byteplus.com/en/docs/vke/RBAC-roles). |
|ClusterId |String |ccog93v\*\*\*\*\*\*\* |The cluster ID with which the RBAC permission policy resource is bound. Setting the parameter to `all_clusters ` means all clusters under the current account. |
|GrantedAt |String |2022\-05\-06T02:49:19Z |The time when the RBAC permission policy resource was created.<br><br>UTC+0 time in standard [RFC3339](https://tools.ietf.org/html/rfc3339) format. |
|GranteeId |Long |15\*\*\*\*\*\* |The ID of the authorized target (IAM user or role). |
|Namespace |String |default |The namespace with which the RBAC permission policy resource is bound. Leaving it empty for the parameter indicates authorization at the cluster level. |
|RevokedAt |String |2022\-05\-06T02:49:19Z |The time when permissions are revoked.<br><br>UTC+0 time in standard RFC 3339 format. |
|GranteeType |String |Role |The target type authorized:<br><br><br>* **User:**  IAM user.<br><br>* **Role**: IAM role. |
|AuthorizedAt |String |2022\-05\-06T02:49:19Z |The time when the RBAC permission policy resource was applied.<br><br>UTC+0 time in standard [RFC3339](https://tools.ietf.org/html/rfc3339) format. |
|AuthorizerId |Long |21\*\*\*\*\*\* |The ID of the authorizer. |
|IsCustomRole |Boolean |true |Whether it is a custom RBAC role:<br><br><br>* **True ** : a custom role.<br><br>* **False ** : a built\-in role of the system. |
|AuthorizerName |String |John |The name of the authorizer. |
|AuthorizerType |String |Account |The type of the authorizer:<br><br><br>* **Account**: BytePlus root user.<br><br>* **User**: IAM user.<br><br>* **Role**: IAM role. |
|KubeRoleBindingName |String |1\-vke\-admin\-cluster\-binding |The object name of the RBAC permission policy resource in Kubernetes. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420********",
        "Action": "ListPermissions",
        "Version": "2022-05-12",
        "Service": "vke",
        "Region": "cn-beijing"
    },
    "Result": {
        "Items": [
            {
                "Id": "ap********",
                "Status": "Succeeded",
                "Message": "AccessDenied In Cluster A",
                "RoleName": "vke:admin",
                "ClusterId": "ccog93v*******",
                "GrantedAt": "2022-05-06T02:49:19Z",
                "GranteeId": 1*,
                "Namespace": "default",
                "RevokedAt": "2022-05-06T02:49:19Z",
                "GranteeType": "Role",
                "AuthorizedAt": "2022-05-06T02:49:19Z",
                "AuthorizerId": 2*,
                "IsCustomRole": true,
                "AuthorizerName": "John",
                "AuthorizerType": "",
                "KubeRoleBindingName": "1-vke-admin-cluster-binding"
            }
        ],
        "TotalCount": 1,
        "PageSize": 10,
        "PageNumber": 1
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

There are no error codes proprietary to this API. See [Public error codes](https://docs.byteplus.com/en/docs/vke/Common-error-codes) for details.

&nbsp;
