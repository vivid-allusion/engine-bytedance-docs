---
title: "ListDomains"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/ListDomains"
---

Queries the domain names of a Container Registry instance.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

To achieve low latency, it is recommended that you select the corresponding service address based on the region where your resources are located. For details, refer to [service address](https://docs.byteplus.com/en/docs/cr/Service_address).


* Request method: POST

* Request address: https://cr.cn\-beijing.byteplusapi.com.cn?Action=ListDomains&Version=2022\-05\-12


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

When calling this API, in addition to the following request parameters, you also need to provide the public request parameters.  See [Public parameters](https://docs.byteplus.com/en/docs/cr/common-parameters) for details.


|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |ListDomains |The API name. The current API's name is `ListDomains`. |
|Version |String |Yes |2022\-05\-12 |The API version. The current version of the API is `2022-05-12`. |
|Registry |String |Yes |registrya |The name of the Container Registry instance for which domain names are to be queried. |
|PageSize |Long |no |10 |The number of domain name information items displayed per page. With a default value of 10, it takes integer values within the range [1, 100]. |
|PageNumber |Long |no |1 |The page number from which to start displaying the returned results. It starts from 1, with a default value of 1, and takes integer values within the range [1, 2147483647]. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST https://cr.cn-beijing.byteplusapi.com.cn?Action=ListDomains&Version=2022-05-12
{
    "Registry": "registrya"
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Registry |String |registrya |The name of the Container Registry instance. |
|TotalCount |Long |1 |The total number of domain names. |
|PageNumber |Long |1 |The current page number. |
|PageSize |Long |10 |The number of domain name information items displayed per page. |
|Items |Array of [Domain](https://docs.byteplus.com/en/docs/65/66443#domain) |[{"Domain": "aaa.com", "Type": "System", "CreateTime": "2022\-05\-20T13:00:55Z"}] |The list of domain names for the Container Registry instance. |


<span id="domain"></span>
### Domain


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Domain |String |helm\-cr\-cn\-beijing.cr.volces.com |The domain names of the Container Registry:<br><br><br>* Trial instance domain name:<br><br>   * For existing instances: `cr-cn-beijing.volces.com`<br><br>   * For upgraded instances: `[Instance Name]-[Region].cr.volces.com`<br><br>* For instances of other versions: `[Instance Name]-[Region].cr.volces.com` |
|Type |String |System |The type of the domain name:<br><br><br>* System: A domain name provided by the system.<br><br>* Volcengine: A BytePlus domain name.<br><br>* ThirdParty: A third\-party domain name. |
|CreateTime |String |2022\-05\-20T13:00:55Z |The time when the domain name was created, in RFC 3339 format. |
|Default |Boolean |true |Whether the domain name is the system domain name of the Container Registry.<br><br><br>* true: It is the default domain name.<br><br>* false: It is not the default domain name. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```json
{
    "ResponseMetadata": {
        "RequestId": "540CFF28-407A-40B5-B6A5-74Bxxxxxxxxx",
        "Action": "ListDomains",
        "Version": "2022-05-12",
        "Service": "cr",
        "Region": "cn-beijing"
    },
    "Result": {
        "TotalCount": 1,
        "PageSize": 10,
        "PageNumber": 1,
        "Registry": "registrya",
        "Items": [
            {
                "Domain": "xx.com",
                "Type": "System"
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

The error codes for this interface are shown in the following table. For public error codes, refer to [public error codes](https://docs.byteplus.com/en/docs/cr/common-error-codes).


|**HTTP Status Code** |**Error code** |**Error Message** |**Descriptions** |
|---|---|---|---|
|400 |OperationDenied.RegistryStatus |The action has been denied due to wrong status %s. |The specified operation is not allowed under the current instance status. Please wait for the status transition to complete and try again. |
