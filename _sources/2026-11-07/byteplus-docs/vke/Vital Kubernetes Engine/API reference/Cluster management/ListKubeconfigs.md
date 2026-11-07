---
title: "ListKubeconfigs"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/ListKubeconfigs"
---

Query the list of Kubeconfig details for clusters that meet the specified criteria.

<span id=".5L2_55So6K-05piO"></span>
## Usage instructions

The effect of querying cluster kubeconfig information varies depending on the permissions of the API caller:


* If the caller has BytePlus root user permissions, they can query kubeconfig information of their own account and their IAM users.

* If the caller has IAM user or role permissions, they can only query their own kubeconfig information.


<span id=".6K-35rGC6K-05piO"></span>
## Request description

VKE has deployed services in multiple regions globally to provide a stable and low\-latency access experience. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/vke/Service_addresses) topic and select the most suitable access point for your business region.


* Request method: POST

* Request URL: https://vke.cn\-beijing.byteplusapi.com.cn?Action=ListKubeconfigs&Version=2022\-05\-12


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=ListKubeconfigs&serviceCode=vke&version=2022-05-12&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table describes the API request parameters. You also need to provide public parameters when calling this API. See [Public parameters](https://docs.byteplus.com/en/docs/vke/Common-parameters) for details.


|Parameters |Type |Required |Sample value |Description |
|---|---|---|---|---|
|Action |String |Yes |ListKubeconfigs |The API name. The name of the current API is `ListKubeconfigs`. |
|Version |String |Yes |2022\-05\-12 |The API version. The current version of the API is `2022-05-12`. |
|PageNumber |Integer |No |1 |The starting page number when querying. The default number is 1. |
|PageSize |Integer |No |10 |The number of results per page:<br><br><br>* Minimum value: 1<br><br>* Maximum value: 100<br><br>* Default value: 10 |
|Filter |Object of [ListKubeconfigsFilter](https://docs.byteplus.com/en/docs/vke/ListKubeconfigs#listkubeconfigsfilter) |No |\- |Kubeconfig filter. |


<span id="listkubeconfigsfilter"></span>
### ListKubeconfigsFilter


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|ClusterIds |Array of String |No |["cc5silumrsf\*\*\*\*\*\*"] |Cluster ID.<br><br>Cluster IDs can be queried  by calling the [ListClusters](https://docs.byteplus.com/en/docs/vke/ListClusters) API.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">100 cluster IDs can be included at most in a single query.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If this parameter is an empty array, filtering is performed based on all clusters in the specified region within the account.</div><br> |
|Ids |Array of String |No |["kc9l74mvqtof\*\*\*\*\*\*"] |Kubeconfig ID.<br><br>To query the ID of the kubeconfig, click the name of the target cluster on the **Cluster** page of the [VKE console](https://console.byteplus.com/vke), and on the cluster **Overview** page that appears, go to the **Connection tab**. You can also view the KubeConfig ID returned after you call the [CreateKubeconfig](https://docs.byteplus.com/en/docs/vke/CreateKubeconfig) API. |
|UserIds |Array of Long |No |[2100\*\*\*\*\*\*] |User ID.<br><br>You can call the [GetUser](https://docs.byteplus.com/en/docs/byteplus-platform/reference-getuser) API to obtain the user ID.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">If no user ID is provided, the system checks the permissions of the caller and returns the corresponding kubeconfig information:</div><br><br><br>   * <div data-tips="true" data-tips-type="warning">If the caller has BytePlus root user permissions, the API returns all kubeconfig files of both the BytePlus root user and all its IAM users.</div><br><br><br>   * <div data-tips="true" data-tips-type="warning">If the caller has IAM user permissions, the API returns only the kubeconfigs of the IAM user.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">You can specify up to 20 user IDs per request.</div><br> |
|RoleIds |Array of Long |No |[7890\*\*\*\*\*\*] |Role ID.<br><br>You can call the [GetRole](https://docs.byteplus.com/en/docs/byteplus-platform/reference-getrole) API to obtain the role ID.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">If no role ID is provided, the system checks the permissions of the caller and returns the corresponding kubeconfig information:</div><br><br><br>   * <div data-tips="true" data-tips-type="warning">If the caller has BytePlus root user permissions, the API returns all kubeconfig files of both the BytePlus root user and all roles under it.</div><br><br><br>   * <div data-tips="true" data-tips-type="warning">If the caller has role permissions, the API returns only the kubeconfigs of the role.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">You can specify up to 20 role IDs per request.</div><br> |
|Types |Array of String |No |["Private"] |Type of the cluster Kubeconfig file. Valid values:<br><br><br>* **Private**: A kubeconfig file for private access.<br><br>* **Public**: A kubeconfig file for public access. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST /?Action=ListKubeconfigs&Version=2022-05-12 HTTP/1.1
Content-Type:application/json
{
    "PageNumber": 1,
    "PageSize": 10,
    "Filter": {
        "ClusterIds": ["cc5silumrsfeq****"],
        "Ids": ["kc9l74mvqtofjnoj5*****"],
        "UserIds": [210000*****],
        "Types": ["Private"]
    }
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following table contains the response parameters of this API. See [Response results](https://docs.byteplus.com/en/docs/vke/Response) for details about public response parameters.


|Parameters |Type |Sample value |Description |
|---|---|---|---|
|Items |Array of [KubeconfigResponse](https://docs.byteplus.com/en/docs/vke/ListKubeconfigs#kubeconfigresponse) |\- |A list of kubeconfig files. |
|PageNumber |Integer |1 |The current page number. |
|PageSize |Integer |10 |Number of kubeconfig items displayed per page. |
|TotalCount |Integer |11 |Total number of kubeconfig files that meet the query conditions. |


<span id="kubeconfigresponse"></span>
### KubeconfigResponse


|Parameters |Type |Sample value |Description |
|---|---|---|---|
|Id |String |kc9q8pbf\*\*\*\*\*\*\*\* |Kubeconfig ID. |
|UserId |Long |21000\*\*\*\*\* |User ID. |
|ClusterId |String |cc9q8pbf\*\*\*\*\*\*\*\* |Cluster ID. |
|Type |String |Private |Type of the cluster Kubeconfig file. Valid values:<br><br><br>* **Private**: A kubeconfig file for private access.<br><br>* **Public**: A kubeconfig file for public access. |
|CreateTime |String |2022\-05\-06T02:49:19Z |Kubeconfig generation time.<br><br>UTC+0 time in standard [RFC3339](https://tools.ietf.org/html/rfc3339) format. |
|ExpireTime |String |2022\-05\-06T02:49:19Z |Kubeconfig expiration time.<br><br>UTC+0 time in standard [RFC3339](https://tools.ietf.org/html/rfc3339) format. |
|Kubeconfig |String |YXBpVmVyc2\*\*\*\*\*\* |Kubeconfig text. The value is Base64\-encoded.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If <code>Type</code> is Public but the specified cluster in <code>ClusterIds</code> has <code>ClusterConfig.ApiServerPublicAccessEnabled</code> set to false, the value of this parameter is empty.</div><br> |
|RoleId |Long |13\*\*\*\*\*\* |Role ID. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```json
HTTP/1.1 200 OK
Content-Type:application/json
{
    "ResponseMetadata": {
        "RequestId": "20220515130014****",
        "Action": "ListKubeconfigs",
        "Version": "2022-05-12",
        "Service": "vke",
        "Region": "cn-beijing"
    },
    "Result": {
        "TotalCount": 1,
        "PageNumber": 1,
        "PageSize": 10,
        "Items": [
            {
                "Id": "kc9q8pbfqtofn8j****",
                "UserId": 210000****,
                "ClusterId": "cc9q8pbfqtofn8j****",
                "Type": "Private",
                "CreateTime": "2022-05-06T02:49:19Z",
                "ExpireTime": "2022-05-06T02:49:19Z",
                "Kubeconfig": "YXBpVmVyc2lvbjogdj*********MUzB0TFMxQ*********TMHRDazFKU1xDUVVSQlRrS*********"
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

There are no proprietary error codes for this API. See [Public error codes](https://docs.byteplus.com/en/docs/vke/Common-error-codes) for details.

&nbsp;
