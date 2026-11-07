---
title: "ModifyPlacementGroup - Modify placement group"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Modifyplacementgroup"
---

Use ModifyPlacementGroup to change the name and description of a storage placement group.

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=ModifyPlacementGroup&groupName=%E5%AD%98%E5%82%A8%E6%94%BE%E7%BD%AE%E7%BB%84&serviceCode=storage_ebs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## request parameters

Only specific request parameters for this API and some common parameters are listed below. For more information, see [Common Parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|4Z1Ch2">必选</span> `Example value: ModifyPlacementGroup`

Operation to perform: ModifyPlacementGroup.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|4MoURY">必选</span> `Example: 2020-04-01`

The version of the API is: 2020\-04\-01.



**Id ** <span data-label="purple">string </span><span data-api-tag="require|yfonV3">必选</span> `Example: pg-bp67acfmxazb4ph****`

Storage placement group ID.



**Name ** <span data-label="purple">string </span>`Optional` `Example: test-pg`

Storage placement group name; see details below:


* The first character can only be a Chinese character, letter, or underscore (_).

* It can contain Chinese characters, letters, numbers, underscores (_), hyphens (\-), or periods (.).

* Length must be between 1 and 128 characters.



**Description ** <span data-label="purple">string </span>`Optional` `Example value: testDescription`

The description for the storage placement group; defaults to empty. Description as follows:


* The first character can only be a Chinese character, letter, or underscore (_).

* Can contain Chinese characters, letters, numbers, underscores (_), hyphens (\-), or periods (.).

* Length limit is 1 to 128 characters.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response Parameters

This API does not have specific response parameters. For more information, see [Response Structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```text
POST /?Action=ModifyPlacementGroup&Version=2020-04-01 HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com
Content-Type: application/json; charset=UTF-8
X-Date: 20250730T085716Z
X-Content-Sha256: 287e874e******d653b44d21e
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20250730/ap-southeast-1/storage_ebs/request, SignedHeaders=host;x-content-sha256;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f

{
  "Id": "pg-bp67acfmxazb4ph****",
  "Name": "test-pg"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Back to example

```text
{
  "ResponseMetadata": {
    "RequestId": "20240829152008176165188230AC****",
    "Action": "ModifyPlacementGroup",
    "Version": "2020-04-01",
    "Service": "storage_ebs",
    "Region": "ap-southeast-1"
  },
  "Result": {}
}
```


<span id=".6ZSZ6K-v56CB"></span>
## error code

The table below lists error codes related to this interface and business logic. For public error codes, see the [Public Error Code](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes) documentation.


|Status Code |error code |error message |Create Volume |
|---|---|---|---|
|404 |InvalidPlacementGroup.NotFound |placement group not found |Anti\-affinity group does not exist. |
