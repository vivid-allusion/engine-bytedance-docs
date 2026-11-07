---
title: "ListRepositories"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/listrepositories"
---

Queries one or more OCI artifact repositories under a specified Container Registry instance.

<span id=".5o6l5Y-j6K-05piO"></span>
## API description

When querying an OCI artifact repository, use the **Filter** parameter to control the filtering criteria for the OCI artifact repository.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

To achieve low latency, it is recommended that you select the corresponding service address based on the region where your resources are located. For more details, refer to [service address](https://docs.byteplus.com/en/docs/cr/Service_address).


* Request method: POST

* Request URL: https://cr.cn\-beijing.byteplusapi.com.cn?Action=ListRepositories&Version=2022\-05\-12


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

When calling this API, in addition to the following request parameters, you also need to provide the public request parameters.  See [Public parameters](https://docs.byteplus.com/en/docs/cr/common-parameters) for details.


|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |ListRepositories |The API name. The current API's name is `ListRepositories`. |
|Version |String |Yes |2022\-05\-12 |The API version. The current version of the API is `2022-05-12`. |
|Registry |String |Yes |registrya |The name of the specified Container Registry instance. On the [Container Registry console](https://console.byteplus.com/cr) **Instance list** page, obtain the instance name. |
|Filter |Object of [RepositoryFilter](https://docs.byteplus.com/en/docs/65/26079#repositoryfilter) |no | |The filtering conditions for querying OCI artifacts. |
|PageSize |Long |no |10 |The number of OCI artifact repositories displayed per page. The default is 10, and the value range is integers from [1,100]. |
|PageNumber |Long |no |1 |The page number from which to start displaying the returned results. It starts from 1, with a default value of 1, and takes integer values within the range [1, 2147483647]. |


<span id="repositoryfilter"></span>
### RepositoryFilter


|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Namespaces |Array of String |no |["ns1","ns2"] |The namespaces to which the specified OCI artifact repositories belong. On the **namespace** page of the target instance in the [Container Registry Console](https://console.byteplus.com/cr), obtain the namespace name. Supports both exact and fuzzy matchings. Fuzzy matching only supports using the asterisk (\*) as a wildcard. A maximum of 20 namespace names can be filled in at once. |
|Names |Array of String |no |["repo1","repo2"] |The names of the specified OCI artifact repositories. On the [Container Registry console](https://console.byteplus.com/cr) page for the target instance's **OCI artifact repository**, obtain the name of the OCI artifact repository. Supports both exact and fuzzy matchings. Fuzzy matching only supports using the asterisk (\*) as a wildcard. A maximum of 20 OCI artifact repository names can be specified in a single request. |
|AccessLevels |Array of String |no |Public |The access levels of the OCI artifact repositories, with the following values:<br><br><br>* **Private**: A private OCI artifact repository that can only be accessed by authorized users.<br><br>* **Public**: A public OCI artifact repository that can be accessed by all users. You can fill in one or more access levels at a time. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST https://cr.cn-beijing.byteplusapi.com.cn?Action=ListRepositories&Version=2022-05-12
{
    "Registry": "registrya",
    "PageSize": 20,
    "PageNumber": 3,
    "Filter": {
        "Namespaces": [
            "library"
        ],
        "Names": [
            "repositorya"
        ],
        "AccessLevels": [
            "Private"
        ]
    }
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Registry |String |registrya |Container Registry Instance |
|TotalCount |Long |1 |The total number of image instances. |
|Items |Array of [Repository](https://docs.byteplus.com/en/docs/65/26079#repository) | |The list of OCI artifact repositories. For more details, please refer to [Repository](https://docs.byteplus.com/en/docs/cr/data-structures-of-responses#repository). |
|PageSize |Long |10 |The number of OCI artifact repository information items displayed per page. |
|PageNumber |Long |1 |The current page number. |


<span id="repository"></span>
### Repository


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Namespace |String |ns1 |The name of the namespace. |
|Name |String |repo1 |The name of the OCI artifact repository. |
|AccessLevel |String |Private |The access level of the OCI artifact repository:<br><br><br>* **Private**: A private type OCI artifact repository that requires an access key for access.<br><br>* **Public**: A public OCI artifact repository that can be accessed directly via its URL. |
|Description |String |it is a description |The description of the Container Registry, with a length of 0 to 300 UTF\-8 characters. |
|CreateTime |String |2022\-05\-20T13:00:55Z |The time when the OCI artifact repository was created. UTC+0 time in [RFC3339](https://datatracker.ietf.org/doc/html/rfc3339) format. |
|UpdateTime |String |2022\-05\-20T13:00:55Z |The last time the OCI artifact repository was updated. UTC+0 time in [RFC3339](https://datatracker.ietf.org/doc/html/rfc3339) format. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```json
{
    "ResponseMetadata": {
        "RequestId": "540CFF28-407A-40B5-B6A5-74Bxxxxxxxxx",
        "Action": "ListRepositories",
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
                "Namespace": "library",
                "Name": "repositorya",
                "AccessLevel": "Private",
                "CreateTime": "2020-05-20T13:00:55Z",
                "UpdateTime": "2020-05-20T13:00:55Z"
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

The error codes for this interface are shown in the table below. For public error codes, please refer to [public error code](https://docs.byteplus.com/en/docs/cr/common-error-codes).


|**HTTP Status Code** |**Error code** |**Error Message** |**Descriptions** |
|---|---|---|---|
|400 |OperationDenied.RegistryStatus |The action has been denied due to wrong status %s. |The specified operation is not allowed under the current instance status. Please wait for the status transition to complete and try again. |
