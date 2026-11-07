---
title: "CreateRegistry"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/createregistry"
---

Create a Standard Edition instance of the Container Registry.

<span id=".5o6l5Y-j6K-05piO"></span>
## API description

This interface is an asynchronous one. After successfully calling the interface and receiving a positive response, you need to call the [ListRegistries](https://docs.byteplus.com/en/docs/cr/listregistries) interface to obtain the current status of the Standard Edition instance. When the status of the Standard Edition instance changes to `{Running, [*]}`, billing will start. For billing details, please refer to [Product billing](https://docs.byteplus.com/en/docs/cr/billing-overview). 

<span id=".6K-35rGC6K-05piO"></span>
## Request description

For low latency, it is recommended that you select the corresponding service address based on the region where your resources are located. For details, refer to [service address](https://docs.byteplus.com/en/docs/cr/Service_address).


* Request method: POST

* Request URL: https://cr.cn\-beijing.byteplusapi.com.cn?Action=CreateRegistry&Version=2022\-05\-12


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

When calling this API, in addition to the following request parameters, you also need to provide the public request parameters.  See [Public parameters](https://docs.byteplus.com/en/docs/cr/common-parameters) for details.


|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |CreateRegistry |The API name. The current API's name is `CreateRegistry`. |
|Version |String |Yes |2022\-05\-12 |The API version. The current version of the API is `2022-05-12`. |
|Name |String |Yes |exampleregistry |The name of the Standard Edition instance, which must be unique within the same region. It supports lowercase English letters, numbers, and hyphens (\-), but numbers can not appear at the beginning, and hyphens (\-) can not appear at the beginning or end. The length limit is 3 to 30 characters. |
|Type |String |no |Enterprise |If not filled in, a Standard Edition instance will be created by default.<br><br><br>* Enterprise: the Standard Edition<br><br>* Micro: the Micro Edition |
|Project |String |no |default |The project to which the instance needs to be associated. Each instance supports association with only one project. |
|ResourceTags |Array of [ResourceTag](https://docs.byteplus.com/en/docs/65/22268#resourcetag) |no |Refer to the general data structure |Allow customizing instance labels using key\-value pairs.  |
|ClientToken |String |no |BC028527\-33B9\-4990\-A633\-84E9F9\*\*\*\*\*\* |A string used to ensure the idempotency of the request. This string is passed in by the caller and must be unique across different requests. ClientToken is case\-sensitive and can consist of 64 ASCII characters at most. |
|ProxyCacheEnabled |Boolean |no |true |Indicates whether it is a proxy cache registry. |
|ProxyCache |Object of [ProxyCacheSpec](https://docs.byteplus.com/en/docs/65/22268#proxycachespec) |no |{<br><br>"Type": "Dockerhub",<br><br>"Username": "",<br><br>"Password": ""<br><br>} |The configuration for the proxy cache registry. It is required when creating a proxy cache registry. |


<span id="resourcetag"></span>
### ResourceTag


|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Key |String |Yes |key1 |The Key value of the label. |
|Value |String |Yes |val1 |The list of values for the label. |


<span id="proxycachespec"></span>
### ProxyCacheSpec


|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Type |String |Yes |DockerHub |The type supported by the proxy cache registry.<br><br><br>* DockerHub: A proxy cache registry of the Docker Hub type, which supports pulling images from Docker Hub in the mainland region.<br><br>* DockerRegistry: A general\-purpose proxy cache registry, which supports the requirements for primary and secondary registries in multi\-cloud scenarios. |
|Endpoint |String |no |https://a.b.c.com |The access address of the source image.<br><br><br>* DockerHub type: The access address is fixed as `https://hub.docker.com`.<br><br>* For types other than DockerHub: A specific access address needs to be specified. |
|Password |String |no |5pWw5o2u5a6J5YWoCg== |The username or SecretAccessKey required to access the source image. |
|Username |String |no |username\-1 |The password or AccessKeyID required to access the source image. |
|SkipSSLVerify |Boolean |no |true |Indicates whether to ignore SSL certificate verification. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST https://cr.cn-beijing.byteplusapi.com.cn?Action=CreateRegistry&Version=2022-05-12
{
    "Name": "exampleregistry"
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

None

<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```json
{
    "ResponseMetadata": {
        "RequestId": "540CFF28-407A-40B5-B6A5-74Bxxxxxxxxx",
        "Action": "CreateRegistry",
        "Version": "2022-05-12",
        "Service": "cr",
        "Region": "cn-beijing"
    },
    "Result": {}
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

The error codes for this interface are listed in the table below. For public error codes, refer to [public error codes](https://docs.byteplus.com/en/docs/cr/common-error-codes).


|**HTTP Status Code** |**Error code** |**Error Message** |**Descriptions** |
|---|---|---|---|
|400 |QuotaExceeded.Registry |The quota of cr registry is exceeded. |The number of Standard Edition instances has reached the quota limit. For product limit descriptions, please refer to the [Limit](https://docs.byteplus.com/en/docs/cr/limits) documentation. If you are sure that you need to increase the quota, you can [submit a ticket](https://console.byteplus.com/ticket/createTicketV2/?step=2&Service=cr) to apply. |
