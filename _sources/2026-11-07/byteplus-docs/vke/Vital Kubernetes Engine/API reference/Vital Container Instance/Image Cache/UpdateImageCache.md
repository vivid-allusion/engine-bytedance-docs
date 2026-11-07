---
title: "UpdateImageCache"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/UpdateImageCache"
---

Update an image cache.

<span id=".5L2_55So6K-05piO"></span>
## Usage instructions

This is an asynchronous API. When this API returns a success message, it will return the ID of the image cache, and the image cache will enter the `{Updating, [Progressing]}` state. After the image cache is updated, it will enter the `{Ready, [Ok]}` state. You can call the [ListImageCaches](https://docs.byteplus.com/en/docs/vke/ListImageCaches) API to obtain the current status of the image cache and check whether the image cache has been updated.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

VKE has deployed services in multiple regions globally to provide a stable and low\-latency access experience. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/vke/Service_addresses) topic and select the most suitable access point for your business region.


* Request method: POST

* Request URL: https://vke.cn\-beijing.byteplusapi.com.cn?Action=UpdateImageCache&Version=2022\-05\-12


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table contains the request parameters for the API. You also need to provide public parameters when calling this API. See [Public parameters](https://docs.byteplus.com/en/docs/vke/Common-parameters) for details.


|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |UpdateImageCache |The API name. The name of the current API is `UpdateImageCache`. |
|Version |String |Yes |2022\-05\-12 |The API version. The current version of the API is `2022-05-12`. |
|ImageCacheId |String |Yes |imc\-3uqro\*\*\*\*\*\* |The ID of the image cache to be updated.<br><br>You can call the [ListImageCaches](https://docs.byteplus.com/en/docs/vke/ListImageCaches) API to obtain the image cache ID.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">The image cache must be in the <strong>Ready</strong> state. You can call the <a href="https://docs.byteplus.com/en/docs/vke/ListImageCaches">ListImageCaches</a> API to obtain the current status of the image cache.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">If you only specify this parameter and do not specify other parameters, the image cache will not be updated.</div><br> |
|AutoPrewarmConfig |Object of [AutoPrewarmConfig](https://docs.byteplus.com/en/docs/90/21145#autoprewarmconfig) |no |\- |The warm\-up policy configurations of the EBS snapshots that correspond to the image cache. |
|Images |Array of String |no |["cr\-cn\-beijing.volces.com/vke\*\*\*\*/nginx:latest"] |The list of container images that correspond to the image cache to be updated.<br><br><br>* If you enter a new container image, a new snapshot will be re\-created, and the control plane will map this new snapshot to the current image cache (The image cache ID remains unchanged).<br><br>* If you do not specify this parameter, it indicates that the container images that correspond to the image cache will not be updated.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div><br><br><br><div data-tips="true" data-tips-type="warning">If you do not update the container images that correspond to the image cache, the <strong>ImageCacheSize</strong>, <strong>ImageRegistryCredentials</strong>, <strong>SubnetIds</strong>, and <strong>SecurityGroupIds</strong> parameters cannot be updated. Otherwise, an error will be reported when you call the API.</div><br> |
|SubnetIds |Array of String |no |["subnet\-3rf6v\*\*\*\*"] |The ID of the subnet to which the image cache belongs.<br><br>You can call a [VPC API](https://docs.byteplus.com/en/docs/vpc/API-overview-1) to obtain the ID of the target subnet.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">If you do not update container images (<strong>Images</strong>), you cannot update the subnet ID.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">You can enter up to five subnet IDs at a time.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">When you update container images (<strong>Images</strong>), you cannot leave this parameter empty and need to provide the ID of the target subnet.</div><br> |
|SecurityGroupIds |Array of String |no |["sg\-2byy13c\*\*\*\*"] |The IDs of the security groups to which the image cache belongs.<br><br>You can call the [DescribeSecurityGroups](https://docs.byteplus.com/en/docs/vpc/DescribeSecurityGroups) API of VPC to obtain the security group IDs.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">If you do not update container images (<strong>Images</strong>), you cannot update the security group IDs.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">When you update container images (<strong>Images</strong>), you cannot leave this parameter empty and need to provide the IDs of the target security groups.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">You can enter up to five security group IDs at a time.</div><br> |
|ImageCacheSize |Integer |no |50 |The image cache capacity.<br><br><br>* Unit: GiB.<br><br>* Valid values: 40 to 500.<br><br>* Default value: 40.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">If you do not update container images (<strong>Images</strong>), you cannot update the image cache size.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">When you update the image cache size, the size must be <strong>greater than or equal to</strong> the original size of the image cache.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">If you do not specify this parameter, the image cache size remains unchanged.</div><br> |
|ImageRegistryCredentials |Array of [ImageRegistryCredentials](https://docs.byteplus.com/en/docs/90/21145#imageregistrycredentials) |no |\- |The access credentials of CR.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">If you do not update container images (<strong>Images</strong>), you cannot update the access credentials of CR.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">If you update container images (<strong>Images</strong>), you can provide the access credentials of CR. If you leave this parameter empty, the system will assume that no access credentials are required for pulling the updated container images.</div><br> |
|RegistryHostnameResolvNameservers |String |no |["10.xx.xx.xx", "10.xx.xx.xx"] |The IP addresses of DNS servers used for resolving hostnames.<br><br><br>* You can enter 0 to 3 IP addresses.<br><br>* Each IP address must be a valid IPv4 address. |


<span id="autoprewarmconfig"></span>
### AutoPrewarmConfig


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|ZoneIDs |Array of String |no |["cn\-beijing\-b"] |The IDs of the availability zones for snapshots to be warmed up.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">If you do not specify this parameter, the availability zones that correspond to the subnets specified during the creation of the image cache are used by default.</div><br> |
|PrewarmRetentionDays |Integer |no |90 |The warm\-up retention duration for the EBS snapshots that correspond to the image cache.<br><br><br>* Unit: days.<br><br>* Valid values: 1 to 180.<br><br>* Default value: 90. |


<span id="imageregistrycredentials"></span>
### ImageRegistryCredentials


|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Server |String |Yes |cr\-cn\-beijing.volces.com |The domain name of the CR instance that does not start with `http://` or `https://`.<br><br>Obtain the domain name of the CR instance by using the [CR console](https://console.byteplus.com/cr) or by calling the [ListDomains](https://docs.byteplus.com/en/docs/cr/ListDomains) API of CR. |
|UserName |String |Yes |user_\*\*\*\*@21\*\*\*\*\*\* |The username for accessing the CR instance.<br><br>Obtain the username for accessing the CR instance by using the [CR console](https://console.byteplus.com/cr) or by calling the [GetUser](https://docs.byteplus.com/en/docs/cr/setuser) API. |
|Password |String |Yes |dGhpcy\*\*\*\*\*\*\*\* |The password that corresponds to the username of the CR instance.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div><br><br><br><div data-tips="true" data-tips-type="warning">You need to Base64\-encode the password before passing it in. For more information about Base64 encoding, see <a href="https://docs.byteplus.com/en/docs/vke/FAQs-about-using-the-command-line-for-base64-encoding">FAQ</a>.</div><br><br><br>You can also obtain a temporary access key to access the CR instance. For detailed operations, see [GetAuthorizationToken](https://docs.byteplus.com/en/docs/cr/getauthorizationtoken). |


<span id="registriesconfig"></span>
## Sample requests

```json
POST /?Action=UpdateImageCache&Version=2022-05-12 HTTP/1.1
Content-Type: application/json
{
    "ImageCacheId": "imc-3uqro****",
    "AutoPrewarmConfig": {
        "ZoneIDs": [
            "cn-beijing-b"
        ],
        "PrewarmRetentionDays": 90
    },
    "Images": [
        "cr-cn-beijing.volces.com/vke****/nginx:latest"
    ],
    "SubnetIds": [
        "subnet-3rf6vwbgkg****"
    ],
    "SecurityGroupIds": [
        "sg-2byy13cnsczy****"
    ],
    "ImageCacheSize": 50,
    "ImageRegistryCredentials": [
        {
            "Server": "cr-cn-beijing.volces.com",
            "UserName": "user_****@21000****",
            "Password": "dGhpc********"
        }
    ]
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following table contains the response parameters of this API. See [Response results](https://docs.byteplus.com/en/docs/vke/Response) for details about public response parameters.


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|ImageCacheId |String |imc\-3uqroqk\*\*\*\*\*\* |The ID of the image cache. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```json
{
    "ResponseMetadata": {
        "RequestId": "2023022020005173B********",
        "Action": "UpdateImageCache",
        "Version": "2022-05-12",
        "Service": "vke",
        "Region": "cn-beijing"
    },
    "Result": {
        "ImageCacheId": "imc-3uqroqkx********"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

The error codes for this API are listed in the table below. Refer to the [Public error codes](https://docs.byteplus.com/en/docs/vke/Common-error-codes) topic for public error codes.


|**HTTP status code** |**Error code** |**Error message** |**Description** |
|---|---|---|---|
|400 |OperationDenied.Stauts |The action has been forbidden due to wrong status {{Status.State}} and {{Status.StateConditions,...}} |The current status of the specified image cache does not support this operation. Please confirm the required image cache status for this API and try again later. |
|400 |OperationDenied.ImageCacheStatus |* Non\-Ready and Failed status:<br><br>   The action has been forbidden due to the image cache's status is not Ready or Failed.<br><br>* Failed status:<br><br>   You can not update a Failed image cache without giving parameter Images.<br><br>* Ready status:<br><br>   You can not update the image cache without any changing. |* You cannot update image caches that are not in the Ready or Failed state.<br><br>* For image caches in the Failed state, you need to specify the **Images** parameter to perform the update.<br><br>* To perform an image cache update, you need to update at least one of the following fields:<br><br>   * **Images**<br><br>   * **PrewarmRetentionDays** |
|400 |UnchangedImages |You can not update a Ready image cache with a non\-null but unchanged parameter Images. |When the image cache is in the Ready state, you cannot provide a non\-null value for the **Images** parameter that is the same as the current value. Update the parameter value and try again. |
|400 |Immutable.SubnetIds |You can not update the subnet without updating container images. |If you do not update container images (**Images**), you cannot update the IDs of subnets to which the image cache belongs (**SubnetIds**). Update the request parameters and try again. |
|400 |Immutable.SecurityGroupIds |You can not update the security group without updating container images. |If you do not update container images (**Images**), you cannot update the IDs of security groups to which the image cache belongs (**SecurityGroupIds**). Update the request parameters and try again. |
|400 |Immutable.ImageCacheSize |You can not update the image cache size without updating container images. |If you do not update container images (**Images**), you cannot update the image cache size (**ImageCacheSize**). Update the request parameters and try again. |
|400 |Immutable.ImageRegistryCredentials |You can not update the image registry credentials without updating container images. |If you do not update container images (**Images**), you cannot update the access credentials of CR (**ImageRegistryCredentials**). Update the request parameters and try again. |
