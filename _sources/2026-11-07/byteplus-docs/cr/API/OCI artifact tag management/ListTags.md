---
title: "ListTags"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/listtags"
---

Queries one or more OCI artifact (image, Helm Chart) versions within a specified OCI artifact repository.

<span id=".5o6l5Y-j6K-05piO"></span>
## API description

When querying OCI artifact versions, use the **Filter** parameter to control the filtering criteria for OCI artifact versions.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

To achieve low latency, it is recommended that you select the corresponding service address based on the region where your resources are located. For details, refer to [service address](https://docs.byteplus.com/en/docs/cr/Service_address).


* Request method: POST

* Request URL: https://cr.cn\-beijing.byteplusapi.com.cn?Action=ListTags&Version=2022\-05\-12


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

When calling this API, in addition to the following request parameters, you also need to provide the public request parameters.  See [Public parameters](https://docs.byteplus.com/en/docs/cr/common-parameters) for details.


|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |ListTags |The API name. The current API's name is `ListTags`. |
|Version |String |Yes |2022\-05\-12 |The API version. The current version of the API is `2022-05-12`. |
|Registry |String |Yes |registrya |The name of the Container Registry instance to which the specified OCI artifact repository belongs. On the **instance list** page of the [Container Registry console](https://console.byteplus.com/cr), find the instance name. |
|Namespace |String |Yes |library |The name of the namespace to which the specified OCI artifact repository belongs. On the **namespace** page of the target instance in the [Container Registry Console](https://console.byteplus.com/cr), obtain the namespace name. |
|Repository |String |Yes |repositorya |The names of the specified OCI artifact repositories. On the [Container Registry console](https://console.byteplus.com/cr) page for the target instance's **OCI artifact repository**, obtain the OCI artifact repository name. |
|Filter |Object of [TagFilter](https://docs.byteplus.com/en/docs/65/26082#tagfilter) |no | |The filtering conditions for querying OCI artifact versions. |
|PageSize |Long |no |10 |The number of OCI artifact versions displayed per page. With a default value of 10, it takes integer values within the range [1,100]. |
|PageNumber |Long |no |1 |The page number from which to start displaying the response results. It starts from 1, with a default value of 1. The value range is an integer from [1,2147483647]. |


<span id="tagfilter"></span>
### TagFilter


|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Names |Array of String |no |["tag"] |Specifies the Tags to filter by, supporting both exact and fuzzy matching. Fuzzy matching only supports using the asterisk (\*) as a wildcard, with a maximum of 20. |
|Types |Array of String |no |["Image"] |The types of OCI artifact tags. Available values:<br><br><br>* Image: this tag represents a container image.<br><br>* Chart: this tag represents a Helm chart. You can fill in one or more Tag types at a time. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST https://cr.cn-beijing.byteplusapi.com.cn?Action=ListTags&Version=2022-05-12
{
    "Registry": "registrya",
    "Namespace": "library",
    "Repository": "repositorya",
    "PageSize": 2,
    "PageNumber": 1,
    "Filter": {
        "Names": [
            "taga"
        ],
        "Types": [
            "Image"
        ]
    }
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Registry |String |registrya |The name of the Container Registry instance to which the specified OCI artifact repository belongs. |
|TotalCount |Long |1 |The total number of OCI artifact versions found. |
|Namespace |String |library |The name of the namespace to which the specified OCI artifact repository belongs. |
|Repository |String |repositorya |The names of the specified OCI artifact repositories. |
|Items |Array of [Tag](https://docs.byteplus.com/en/docs/65/26082#tag) | |The list of OCI artifact versions. For more details, please refer to [Tag](https://docs.byteplus.com/en/docs/cr/data-structures-of-responses#tag). |
|PageNumber |Long |1 |The current page number. |
|PageSize |Long |10 |The number of OCI artifact version information items displayed per page. |


<span id="tag"></span>
### Tag


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Name |String |v2 |The name of the OCI artifact version (Tag). |
|Type |String |Image |The type of the OCI artifact Tag:<br><br><br>* Image: this tag represents a container image.<br><br>* Chart: this tag represents a Helm chart. |
|Digest |String |sha256:dd97a3eb42\*\*\*\*\*\*\*\* |The digest of the OCI artifact, represented as a SHA256 value. |
|PushTime |String |2022\-05\-03T12:08:01Z |The time of the last push of the OCI artifact. UTC+0 time in [RFC3339](https://datatracker.ietf.org/doc/html/rfc3339) format. |
|Size |Long |10061844 |The size of an OCI artifact, measured in bytes. |
|ImageAttributes |Array of [ImageAttribute](https://docs.byteplus.com/en/docs/65/26082#imageattribute) | |The relevant attributes when the Tag type is Image. |
|ChartAttribute |Object of [ChartAttribute](https://docs.byteplus.com/en/docs/65/26082#chartattribute) | |The relevant attributes when the Tag type is Chart. |


<span id="imageattribute"></span>
### ImageAttribute


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Author |String |user@test.com |The creator of the image, i.e., the BytePlus root user that uploads the image to the Container Registry. |
|Architecture |String |amd64 |The architecture of the image. |
|Os |String |linux |The operating system supported by the image. |
|Digest |String |sha256:dd97a3eb42\*\*\*\*\*\*\*\* |The digest of the image, represented as a SHA256 value. |
|Size |Long |213587000 |The size of the image. |


<span id="chartattribute"></span>
### ChartAttribute


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|ApiVersion |String |v2 |The Helm version. |
|Name |String |helm1 |The name of the Helm Chart. |
|Version |String |8.6.1 |The version of the Helm Chart. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```json
{
    "ResponseMetadata": {
        "RequestId": "540CFF28-407A-40B5-B6A5-74Bxxxxxxxxx",
        "Action": "ListTags",
        "Version": "2022-05-12",
        "Service": "cr",
        "Region": "cn-beijing"
    },
    "Result": {
        "Registry": "registrya",
        "Namespace": "library",
        "Repository": "repositorya",
        "TotalCount": 1,
        "PageSize": 10,
        "PageNumber": 1,
        "Items": [
            {
                "Digest": "sha256:318693f46bd015fa7e1652cff99728ab91403d0922af1183a8ad15ee********",
                "Type": "Image",
                "PushTime": "2021-08-26T06:04:29Z",
                "Size": 4389,
                "Name": "0.0.2",
                "ImageAttributes": [
                    {
                        "Author": "",
                        "Architecture": "amd64",
                        "Os": "linux",
                        "Digest": "xxxxxx"
                    }
                ]
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

The error codes for this interface are listed in the table below. For public error codes, refer to [public error codes](https://docs.byteplus.com/en/docs/cr/common-error-codes).


|**HTTP Status Code** |**Error code** |**Error Message** |**Descriptions** |
|---|---|---|---|
|400 |OperationDenied.RegistryStatus |The action has been denied due to wrong status %s. |The specified operation is not allowed under the current instance status. Please wait for the status transition to complete and try again. |
