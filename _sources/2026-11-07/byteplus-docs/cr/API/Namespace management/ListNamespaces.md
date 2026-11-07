---
title: "ListNamespaces"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/listnamespaces"
---

Query one or more namespaces under a specified Container Registry instance.

<span id=".5o6l5Y-j6K-05piO"></span>
## API description

Supports controlling namespace filtering criteria through the **Filter** parameter.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

To achieve low latency, it is recommended that you select the corresponding service address based on the region where your resources are located. For details, refer to [service address](https://docs.byteplus.com/en/docs/cr/Service_address).


* Request method: POST

* Request URL: https://cr.cn\-beijing.byteplusapi.com.cn?Action=ListNamespaces&Version=2022\-05\-12


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

When calling this API, in addition to the following request parameters, you also need to provide the public request parameters.  See [Public parameters](https://docs.byteplus.com/en/docs/cr/common-parameters) for details.


|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |ListNamespaces |The API name. The current API's name is `ListNamespaces`. |
|Version |String |Yes |2022\-05\-12 |The API version. The current version of the API is `2022-05-12`. |
|Registry |String |Yes |registrya |The name of the specified Container Registry instance. On the **instance list** page of the [Container Registry console](https://console.byteplus.com/cr), obtain the instance name. |
|Filter |Object of [NamespaceFilter](https://docs.byteplus.com/en/docs/65/26074#namespacefilter) |no | |The filtering conditions for the namespace to be queried. |
|PageSize |Long |no |10 |The number of namespaces displayed per page. With a default value of 10, it takes integer values within the range [1, 100]. |
|PageNumber |Long |no |1 |The page number from which to start displaying the returned results. It starts from 1, with a default value of 1, and takes integer values within the range [1, 2147483647]. |


<span id="namespacefilter"></span>
### NamespaceFilter


|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Names |Array of String |no |["ns1","ns2"] |The name of the specified namespace. On the [Container Registry Console](https://console.byteplus.com/cr) target instance's **namespace** page, obtain the namespace name. Supports both exact and fuzzy matchings. Fuzzy matching only supports using the asterisk (\*) as a wildcard. A maximum of 20 namespace names can be filled in at once. |
|Projects |Array of String |no |["projecta","projectb"] |Filters the projects to which the users belong. This parameter is read for filtering when inProject is set to true. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST https://cr.cn-beijing.byteplusapi.com.cn?Action=ListNamespaces&Version=2022-05-12
{
    "Registry": "registrya",
    "PageNumber": 1,
    "PageSize": 20,
    "Filter": {
        "Names": [
            "namespacea"
        ]
    }
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Registry |String |registrya |The name of the specified Container Registry instance. |
|TotalCount |Long |1 |The number of namespaces queried. |
|PageNumber |Long |1 |The current page number. |
|PageSize |Long |10 |The number of namespace information entries displayed per page. |
|Items |Array of [Namespace](https://docs.byteplus.com/en/docs/65/26074#namespace) | |The list of namespaces. For details, please refer to [Namespace](https://docs.byteplus.com/en/docs/cr/data-structures-of-responses#namespace). |


<span id="namespace"></span>
### Namespace


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Name |String |namespacea |The name of the namespace. |
|Project |String |projecta |The name of the project to which the namespace belongs. If this parameter is left blank, it indicates that the created Namespace does not belong to any project. |
|CreateTime |String |2022\-05\-20T13:00:55Z |The time when the namespace was created. UTC+0 time in [RFC3339](https://datatracker.ietf.org/doc/html/rfc3339) format. |
|RepositoryDefaultAccessLevel |String |Private |The default public access level of the OCI artifact repository under the namespace.<br><br><br>* Public: Public, accessible directly without an access key.<br><br>* Private: Private, accessible only after entering an access key. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```json
{
    "ResponseMetadata": {
        "RequestId": "540CFF28-407A-40B5-B6A5-74Bxxxxxxxxx",
        "Action": "ListNamespaces",
        "Version": "2022-05-12",
        "Service": "cr",
        "Region": "cn-beijing"
    },
    "Result": {
        "TotalCount": 1,
        "Registry": "registrya",
        "PageSize": 10,
        "PageNumber": 1,
        "Items": [
            {
                "Name": "namespacea",
                "CreateTime": "2020-05-20T13:00:55Z",
                "Project": ""
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

The error codes for this interface are shown in the table below. For public error codes, refer to [public error code](https://docs.byteplus.com/en/docs/cr/common-error-codes).


|**HTTP Status Code** |**Error code** |**Error Message** |**Descriptions** |
|---|---|---|---|
|400 |OperationDenied.RegistryStatus |The action has been denied due to wrong status %s. |The specified operation is not allowed under the current instance status. Please wait for the status transition to complete and try again. |
