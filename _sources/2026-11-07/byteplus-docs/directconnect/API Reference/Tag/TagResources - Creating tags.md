---
title: "TagResources - Creating tags"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/TagResources"
---

Call the TagResources API to add custom tags to Direct Connect (DC) resources.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=TagResources&serviceCode=directconnect&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple"> String  </span><span data-api-tag="require|yrdc20">必选</span> `Example: TagResources`

The interface name. The current API name is `TagResources`.



**Version ** <span data-label="purple"> String  </span><span data-api-tag="require|LDEwxa">必选</span> `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**ResourceType ** <span data-label="purple"> String  </span><span data-api-tag="require|S-bgHC">必选</span> `Example: directconnectconnection`

The type of the resource to be tagged. Values:


* directconnectconnection: Direct Connect Connection

* directconnectgateway: Direct Connect Gateway

* directconnectvirtualinterface: Direct Connect Virtual Interface



**ResourceIds.N ** <span data-label="purple"> String </span><span data-api-tag="require|bHl4dr">必选</span> `Example: dcc-lhn2cx0an18****`

The ID of the resource to be tagged.


* N represents the sequence number of a DC resource. You can specify a maximum of 50 IDs per call.

* Separate multiple IDs with ampersands (&).



**Tags.N.Key ** <span data-label="purple"> String </span><span data-api-tag="require|HTb6hW">必选</span> `Example: v1`

The tag key of the resource.


* N represents the sequence number of a tag key. Valid range: 1 to 20.

* Separate multiple tag keys with ampersands (&).

* Must not start with volc: or sys: in any case form.

* Must be 1 to 128 characters. May include characters (any language), numbers, spaces ( ), underscores (_), periods (.), half\-width colons (:), slashes (/), equal signs (=), plus signs (+), hyphens (\-), and at signs (@).

* If a tag key contains leading or trailing spaces, the system will automatically delete them.


> Duplicate tag keys are not allowed for the same resource.



**Tags.N.Value ** <span data-label="purple"> String </span>`optional` `Example: k1`

The tag value of the resource.


* N represents the sequence number of a tag value. Valid range: 1–20.

* Separate multiple tag values with ampersands (&).

* Must be 0 to 256 characters. If left blank, this parameter defaults to an empty string.

* The following characters are allowed: characters from all languages, numbers, spaces ( ), underscores (_), periods (.), colons (:), forward slashes (/), equal signs (=), plus signs (+), hyphens (\-), and the at symbol (@).

* Case\-sensitive.

* If a tag value starts or ends with a space, the system will automatically delete them.


> To pass in this parameter, pass in Tags.N.Key first.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This API does not have specific response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```JSON
GET /?Action=TagResources&Version=2020-04-01&ResourceType=directconnectconnection&ResourceIds.1=dcc-lhn2cx0an18****&Tags.1.Key=v1&Tags.1.Value=k1 HTTP/1.1
Host: directconnect.cn-beijing.byteplusapi.com.cn
X-Date: 20250804T033538Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20250804/cn-beijing/directconnect/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "TagResources",
        "Version": "2020-04-01",
        "Service": "directconnect",
        "Region": "cn-north-1"
    },
"Result": {
        "RequestId": "2021062415303301022514515207C4****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

For more information, see [Common error codes](https://docs.byteplus.com/en/docs/directconnect/Public-error-codes).
