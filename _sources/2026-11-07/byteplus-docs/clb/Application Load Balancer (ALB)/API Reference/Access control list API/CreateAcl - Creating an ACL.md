---
title: "CreateAcl - Creating an ACL"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/ALB-CreateAcl"
---

Call the CreateAcl API to create an ACL.

<span id=".5L2_55So6K-05piO"></span>
## Instructions


* The maximum number of policy groups that can be created per account per region is 50.

* Submit up to 10 API requests per second.


<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=CreateAcl&groupName=%E8%AE%BF%E9%97%AE%E6%8E%A7%E5%88%B6&serviceCode=alb&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. More information can be found in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|DGcT25">必选</span> `Example: CreateAcl`

Action to execute. Set the value to CreateAcl.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|q9uiqI">必选</span> `Example: 2020-04-01`

The API version. Value: 2020\-04\-01.



**AclName ** <span data-label="purple">string </span>`optional` `Example: myacl`

ACL name.


* Cannot start with http:// or https://.

* Must start with a letter or Chinese character. May include numbers, periods (.), underscores (_), and hyphens (\-).

* Length limit is 1 to 128 characters.

* If left blank, it defaults to the ACL ID.



**Description ** <span data-label="purple">string </span>`optional` `Example: This is a acl.`

ACL description.


* Cannot start with http:// or https://.

* Must start with a letter or Chinese character and may include numbers, half\-width commas (,), periods (.), underscores (_), spaces ( ), equal signs (=), hyphens (\-), full\-width commas (，), and full\-width periods (。).

* Must be 1 to 255 characters.

* If left blank, this parameter defaults to an empty string.



**Tags.N.Value ** <span data-label="purple">string[] </span>`optional` `Example: Tags.1.Value=v1&Tags.2.Value=v2`

The tag value of the custom tag. To provide this parameter, provide Tags.N.Key first. The specific rules are as follows:


* The length limit is 0 to 256 characters.

* Case\-sensitive.

* Must not start or end with a space.

* May include characters (any language), numbers, spaces ( ), underscores (_), periods (.), half\-width colons (:), slashes (/), equal signs (=), plus signs (+), minus signs (\-) and at signs (@).



**Tags.N.Key ** <span data-label="purple">string[] </span>`optional` `Example: Tags.1.Key=k1&Tags.2.Key=k2`

The tag key of the custom tag. The specific rules are as follows:


* Must be 1 to 128 characters.

* Case\-sensitive.

* Cannot start with any case‑insensitive combination of volc: or sys:.

* Must not start or end with a space.

* May include characters (any language), numbers, spaces ( ), underscores (_), periods (.), half\-width colons (:), slashes (/), equal signs (=), plus signs (+), minus signs (\-) and at signs (@).

* Duplicate tag keys are not allowed for the same resource.



**ProjectName ** <span data-label="purple">string </span>`optional` `Example: default`

The name of the project to which ACL belongs.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this API are listed below. More information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**RequestId ** <span data-label="purple">string </span>`Example: 20210811152539010225146063030****`

Request ID.



**AclId ** <span data-label="purple">string </span>`Example: acl-3cj44nv0jhhxc6c6rrtet****`

ACL ID.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```text
GET /?Action=CreateAcl&AclName=yxl-test&Description=yxl-test&ProjectName=default&Version=2020-04-01 HTTP/1.1
Host: alb.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/alb/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```text
{
    "ResponseMetadata": {
        "RequestId": "916800fc-fc38-47dd-8e7f-71a16f325cc4",
        "Action": "CreateAcl",
        "Version": "2020-04-01",
        "Service": "alb",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "916800fc-fc38-47dd-8e7f-71a16f325cc4",
        "AclId": "acl-33txelibucdfk57uhwmviq46o"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The following table lists the error codes related to the business logic for this API. For details, see [Common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).


|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |Invalid%s.Malformed |MismatchThe specified %s is malformed. |The specified %s parameter format is invalid. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, '%s'. |This request is missing a required parameter. Please ensure the request includes all required parameters, such as: %s. |
|400 |InvalidParameter |Data unmarshal failed. |Failed to parse the request. |
|400 |InvalidAclName.Malformed |The specified AclName is malformed. |The specified AclName parameter format is invalid. |
|400 |InvalidDescription.Malformed |The specified Description is malformed. |The format specified for Description is invalid. |
|400 |OperationFailed.QueryProject |The request on the specified resource failed due to the query on project failed. |The request to operate on this resource failed because the project query failed. |
|400 |QuotaExceed.AclPerRegion |You've reached the limit on the number of ACLs the current region you can create in, usage xx/xx. |The maximum number of ACLs that can be created in the current region has been reached. Used: xxx. Quota: xxx |
|400 |OperationFailed.AddIntoProjectFailed |The request on the specified resource failed due to adding it into the project failed. |The request to operate on this resource failed because adding the resource to the project failed. |
|400 |InvalidTags.Key.Malformed |The specified Tags.Key is malformed. |The specified Tags.Key parameter format is invalid. |
|400 |InvalidTags.Value.Malformed |The specified Tags.Value is malformed. |The specified Tags.Value parameter format is invalid. |
|400 |InvalidTags.Key.Duplicated |The specified Tags.Key is duplicated. |The specified Tags.Key is duplicated. |
|404 |InvalidProject.NotFound |The specified Project does not exist. |The specified project does not exist. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Please try again later or contact an engineer for further consultation. |
