---
title: "CreateImageCache"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/CreateImageCache"
---

Create an image cache.

<span id=".5L2_55So6K-05piO"></span>
## Usage instructions


* This is an asynchronous API. When this API returns a success message, it will return the ID of the image cache, and the image cache will enter the `{Creating, [Progressing]}` state, until it is successfully created and enters the {Ready, [Ok]} state. You can call the [ListImageCaches](https://docs.byteplus.com/en/docs/vke/ListImageCaches) API to obtain the current status of the image cache and check whether the image cache has been created.

* Before you create an image cache, you need to prepare the required container images. You can use images from BytePlus CR as well as images from third\-party container registries. For instructions on uploading images to CR, see [Pushing and pulling images](https://docs.byteplus.com/en/docs/cr/push-and-pull-images).

* Each BytePlus root user, including sub\-users, can have up to 20 image caches, excluding image caches that are being deleted (status: `[Deleting,*]`). If this upper limit is reached, new image caches cannot be created. You can delete image caches that are no longer used, or [submit a ticket](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000210) to apply for a quota increase.


<span id=".6K-35rGC6K-05piO"></span>
## Request description

VKE has deployed services in multiple regions globally to provide a stable and low\-latency access experience. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/vke/Service_addresses) topic and select the most suitable access point for your business region.


* Request method: POST

* Request URL: https://vke.cn\-beijing.byteplusapi.com.cn?Action=CreateImageCache&Version=2022\-05\-12


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table lists the API request parameters. You must also provide public parameters when calling this API. For details, see Public parameters.


|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |CreateImageCache |The API name. The name of the current API is `CreateImageCache`. |
|Version |String |Yes |2022\-05\-12 |The API version. The current version of the API is `2022-05-12`. |
|ImageCacheName |String |Yes |test\-imc |The image cache name.<br><br><br>* The image cache name must be unique in the same region.<br><br>* It can contain uppercase and lowercase letters, digits, and hyphens (\-) and is 1 to 64 characters in length. |
|SubnetIds |Array of String |Yes |["subnet\-3rf6vwbgkg\*\*\*\*"] |The ID of the subnet to which the image cache belongs.<br><br>You can call a [VPC API](https://docs.byteplus.com/en/docs/vpc/API-overview-1) to obtain the ID of the target subnet.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can enter up to five subnet IDs at a time.</div><br> |
|SecurityGroupIds |Array of String |Yes |["sg\-2byy13cnsczy\*\*\*\*"] |The IDs of the security groups to which the network of the image cache belongs.<br><br>You can call the [DescribeSecurityGroups](https://docs.byteplus.com/en/docs/vpc/DescribeSecurityGroups) API of VPC to obtain the security group IDs.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can enter up to five security group IDs at a time.</div><br> |
|Images |Array of String |Yes |["cr\-cn\-beijing.volces.com/vke\*\*\*\*/nginx:latest"] |The list of container images that are required to create the image cache. |
|ImageCacheSize |Integer |No |50 |The image cache capacity.<br><br><br>* Unit: GiB.<br><br>* Valid values: 40 to 500.<br><br>* Default value: 40. |
|ImageRegistryCredentials |Array of [ImageRegistryCredentials](https://docs.byteplus.com/en/docs/90/21142#imageregistrycredentials) |No |\- |The access credentials of CR. |
|AutoPrewarmConfig |Object of [AutoPrewarmConfig](https://docs.byteplus.com/en/docs/90/21142#autoprewarmconfig) |No |\- |The warm\-up policy configurations of the EBS snapshots that correspond to the image cache. |
|RetentionDays |Integer |No |15 |The retention duration of the image cache. After expiration, the image cache will be cleared.<br><br><br>* Unit: days.<br><br>* Valid values: 1 to 365. The value must be a positive integer.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div><br><br><br><div data-tips="true" data-tips-type="warning">If you do not specify this parameter in the request parameters, the image cache will expire after 15 days.</div><br> |
|RegistryHostnameResolvNameservers |Array of String |No |["10.xx.xx.xx", "10.xx.xx.xx"] |The IP addresses of DNS servers used for resolving hostnames.<br><br><br>* You can enter 0 to 3 IP addresses.<br><br>* Each IP address must be a valid IPv4 address. |
|BaseImageCacheId |String |No |imc\-3uqroqkx0i3j\*\*\*\* |Specify an existing image cache and enable incremental image cache creation. After you specify an existing image cache, the newly created image cache will reuse the image layer of the specified image cache, which accelerates the cache creation.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The image cache must be in the <strong>Ready</strong> state. You can call the <a href="https://docs.byteplus.com/en/docs/vke/ListImageCaches">ListImageCaches</a> API to obtain the current status of the image cache.</div><br> |


&nbsp;


|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |CreateImageCache |The API name. The name of the current API is `CreateImageCache`. |
|Version |String |Yes |2022\-05\-12 |The API version. The current version of the API is `2022-05-12`. |
|ImageCacheName |String |Yes |test\-imc |The image cache name.<br><br><br>* The image cache name must be unique in the same region.<br><br>* It can contain uppercase and lowercase letters, digits, and hyphens (\-) and is 1 to 64 characters in length. |
|SubnetIds |Array of String |Yes |["subnet\-3rf6vwbgkg\*\*\*\*"] |The ID of the subnet to which the image cache belongs.<br><br>You can call a [VPC API](https://docs.byteplus.com/en/docs/vpc/API-overview-1) to obtain the ID of the target subnet.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can enter up to five subnet IDs at a time.</div><br> |
|SecurityGroupIds |Array of String |Yes |["sg\-2byy13cnsczy\*\*\*\*"] |The IDs of the security groups to which the network of the image cache belongs.<br><br>You can call the [DescribeSecurityGroups](https://docs.byteplus.com/en/docs/vpc/DescribeSecurityGroups) API of VPC to obtain the security group IDs.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can enter up to five security group IDs at a time.</div><br> |
|Images |Array of String |Yes |["cr\-cn\-beijing.volces.com/vke\*\*\*\*/nginx:latest"] |The list of container images that are required to create the image cache. |
|ImageCacheSize |Integer |No |50 |The image cache capacity.<br><br><br>* Unit: GiB.<br><br>* Valid values: 40 to 500.<br><br>* Default value: 40. |
|ImageRegistryCredentials |Array of [ImageRegistryCredentials](https://docs.byteplus.com/en/docs/90/21142#imageregistrycredentials) |No |\- |The access credentials of CR. |
|AutoPrewarmConfig |Object of [AutoPrewarmConfig](https://docs.byteplus.com/en/docs/90/21142#autoprewarmconfig) |No |\- |The warm\-up policy configurations of the EBS snapshots that correspond to the image cache. |
|RetentionDays |Integer |No |15 |The retention duration of the image cache. After expiration, the image cache will be cleared.<br><br><br>* Unit: days.<br><br>* Valid values: 1 to 365. The value must be a positive integer.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div><br><br><br><div data-tips="true" data-tips-type="warning">If you do not specify this parameter in the request parameters, the image cache will expire after 15 days.</div><br> |
|RegistryHostnameResolvNameservers |Array of String |No |["10.xx.xx.xx", "10.xx.xx.xx"] |The IP addresses of DNS servers used for resolving hostnames.<br><br><br>* You can enter 0 to 3 IP addresses.<br><br>* Each IP address must be a valid IPv4 address. |
|BaseImageCacheId |String |No |imc\-3uqroqkx0i3j\*\*\*\* |Specify an existing image cache and enable incremental image cache creation. After you specify an existing image cache, the newly created image cache will reuse the image layer of the specified image cache, which accelerates the cache creation.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The image cache must be in the <strong>Ready</strong> state. You can call the <a href="https://docs.byteplus.com/en/docs/vke/ListImageCaches">ListImageCaches</a> API to obtain the current status of the image cache.</div><br> |


<span id="imageregistrycredentials"></span>
### ImageRegistryCredentials


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Server |String |Yes |cr\-cn\-beijing.volces.com |The domain name of the CR instance that does not start with `http://` or `https://`.<br><br>Obtain the domain name of the CR instance by using the [CR console](https://console.byteplus.com/cr) or by calling the [ListDomains](https://docs.byteplus.com/en/docs/cr/ListDomains) API of CR. |
|UserName |String |Yes |user_\*\*\*\*@21000\*\*\*\* |The username for accessing the CR instance.<br><br>Obtain the username for accessing the CR instance by using the [CR console](https://console.byteplus.com/cr) or by calling the [GetUser](https://docs.byteplus.com/en/docs/cr/setuser) API. |
|Password |String |Yes |dGhpcyBpcyBh\*\*\*\*\*\*\*\* |The password that corresponds to the username of the CR instance.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div><br><br><br><div data-tips="true" data-tips-type="warning">You need to Base64\-encode the password before passing it in. For more information about Base64 encoding, see <a href="https://docs.byteplus.com/en/docs/vke/FAQs-about-using-the-command-line-for-base64-encoding">FAQ</a>.</div><br><br><br>You can also obtain a temporary access key to access the CR instance. For detailed operations, see [GetAuthorizationToken](https://docs.byteplus.com/en/docs/cr/getauthorizationtoken). |


<span id="autoprewarmconfig"></span>
### AutoPrewarmConfig


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|ZoneIds |Array of String |No |["cn\-beijing\-b"] |The IDs of the availability zones for snapshots to be warmed up.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If you do not specify this parameter, the availability zones that correspond to the subnets specified during the creation of the image cache are used by default.</div><br> |
|PrewarmRetentionDays |Integer |No |90 |The warm\-up retention duration for the EBS snapshots that correspond to the image cache.<br><br><br>* Unit: days.<br><br>* Valid values: 1 to 180.<br><br>* Default value: 90. |


<span id="registriesconfig"></span>
## Sample requests

```json
POST /?Action= CreateImageCache&Version=2022-05-12 HTTP/1.1
Content-Type:application/json
{
    "ImageCacheName": "test-imc",
    "SubnetIds": [
        "subnet-3rf6vwbgkg****",
        "subnet-2d6kpn09********",
        "subnet-3rfcnoa********"
    ],
    "SecurityGroupIds": [
        "sg-2byy13cnsczy****"
    ],
    "Images": [
        "cr-cn-beijing.volces.com/vke****/nginx:latest",
        "cr-cn-beijing.volces.com/vke****/nginx:v1"
    ],
    "ImageRegistryCredentials": [
        {
            "UserName": "user_****@21000****",
            "Server": "cr-cn-beijing.volces.com",
            "Password": "dGhpcyBpcyBh********"
        }
    ],
    "ImageCacheSize": 50
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following table contains the response parameters of this API. See [Response results](https://docs.byteplus.com/en/docs/vke/Response) for details about public response parameters.


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|ImageCacheId |String |imc\-3uqroqkx0i3jabcdefgs |The ID of the image cache. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```json
{
    "ResponseMetadata": {
        "RequestId": "2023022020005173B********",
        "Action": "CreateImageCache",
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
|400 |LimitExceeded.ImageCacheSize |You have reached the limit of the size of image cache that you can create. |The size of the specified image cache exceeds the upper limit. Check the valid values of the **ImageCacheSize** parameter. |
|400 |VpcMismatch.{{Parameter}} |The specified {{resourceType}} {{resourceId}} and {{resourceType}} {{resourceId}} are not in the same vpc. |The specified subnet, security group, and other resources do not belong to the same VPC. Make sure that they are deployed in the same VPC. |
|400 |OutOfStorage.ImageCacheSize |The size of the specified image cache is too small. |The size of the specified image cache is too small. Check the valid values of the **ImageCacheSize** parameter. |
|400 |Conflict.Name |The specified name conflicts with existing {{resourceType}}. |An image cache with the same name already exists in the specified region. Update the image cache name and try again later. |
|400 |NotFound.BaseImageCacheId |The specified imageCache {{BaseImageCacheId}} not found |The specified base image cache for incremental creation of the image cache does not exist. Check the ID of the existing image cache and try again later. |
|400 |OperationDenied.ImageCacheStatus |The action has been denied due to wrong source image cache status {{Status}}. |The current status of the specified existing image cache does not support this operation. Check whether the status of the existing image cache specified by the BaseImageCacheId parameter is **Ready** and try again later. |
