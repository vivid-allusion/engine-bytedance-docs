---
title: "CreateAcl - Creating an ACL"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/CreateAcl"
---

Call the CreateAcl API to create an ACL.

<span id=".5L2_55So6K-05piO"></span>
## Instructions

Under one account, up to 200 policy groups can be created per region.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=CreateAcl&serviceCode=clb&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters



**Action ** <span data-label="purple">String </span><span data-api-tag="require|HbIUiL">必选</span>`Example: CreateAcl`

Action to execute. Set the value to **CreateAcl**.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|h1YZva">必选</span> `Example: 2020-04-01`

API version. The current version is **2020\-04\-01**.



**AclName ** <span data-label="purple">String </span>`optional` `Example: myacl`

ACL name.


* Must start with a letter, number, or Chinese character. May include letters, numbers, Chinese characters, periods (.), underscores (_), and hyphens (\-).

* Must be 1 to 128 characters.

* If left blank, it defaults to the ACL ID.



**Description ** <span data-label="purple">String </span>`optional` `Example: This is an acl.`

ACL description.


* Must start with a letter, number, or Chinese character. May include letters, numbers, Chinese characters, and the following symbols: commas (,), periods (.), underscores (_), spaces ( ), equal signs (=), hyphens (\-), full\-width commas ( ， ), and full\-width periods ( 。 ).

* Must be 0 to 255 characters.

* If left blank, it defaults to an empty string.



**ProjectName ** <span data-label="purple">String </span>`optional` `Example: default`

The name of the project to which ACL belongs. If left blank, it defaults to default.



**Tags.N.Key ** <span data-label="purple">String </span>`optional` `Example: key1`

The tag key of the custom tag.


* N represents the sequence number of a tag key. Valid range: 1 to 20.

* Separate multiple tag keys with &.

* Must not start with `volc:` or `sys:` in any case form.

* Must be 1 to 128 characters. May include characters (any language), numbers, spaces ( ), underscores (_), periods (.), half\-width colons (:), slashes (/), equal signs (=), plus signs (+), hyphens (\-), and at signs (@).

* If a tag key contains leading or trailing spaces, the system will automatically delete them.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Duplicate tag keys are not allowed for the same resource.</div>




**Tags.N.Value ** <span data-label="purple">String </span>`optional` `Example: value1`

The tag value of the custom tag.


* N represents the sequence number of a tag value. Valid range: 1–20.

* Separate multiple tag values with ampersands (&).

* Must be 0 to 256 characters. If left blank, this parameter defaults to an empty string.

* The following characters are allowed: characters from all languages, numbers, spaces ( ), underscores (_), periods (.), colons (:), forward slashes (/), equal signs (=), plus signs (+), hyphens (\-), and the at symbol (@).

* Case\-sensitive.

* If a tag value starts or ends with a space, the system will automatically delete it.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To pass in this parameter, pass in <code>Tags.N.Key</code> first.</div>




&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**RequestId ** <span data-label="purple">String </span>`Example: 20210811152539010225146063030****`

Request ID.



**AclId ** <span data-label="purple">String </span>`Example: acl-3cj44nv0jhhxc6c6rrtet****`

ACL ID.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=CreateAcl&Version=2020-04-01&AclName=myacl&Description=This is an acl.&ProjectName=default&Tags.1.Key=key1&Tags.1.Value=value1
Host: clb.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/clb/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "CreateAcl",
        "Version": "2020-04-01",
        "Service": "clb",
        "Region": "cn-beijing"
    },
    "Result": {
        "AclId": "acl-3cj44nv0jhhxc6c6rrtet****",
        "RequestId": "20210811152539010225146063030****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

This section displays only the error codes of the current API. For more error codes, see [Common error codes](https://docs.byteplus.com/en/docs/clb/Public-error-codes).


|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |InvalidDescription.Malformed |The specified Description is malformed. |The format specified for Description is invalid. |
|400 |InvalidIncorrectOrder.Malformed |The specified index order is malformed. |The specified index order parameter format is invalid. |
|400 |InvalidName.Malformed |The specified Name is malformed. |The specified Name parameter format is invalid. |
|400 |InvalidProject.Malformed |The specified Project is malformed. |The format of the specified Project is invalid. |
|400 |InvalidQuotaCode.Malformed |The specified QuotaCode is malformed. |The specified QuotaCode parameter format is invalid. |
|400 |InvalidTagKey.Malformed |The specified TagKey is malformed. |The specified TagKey is invalid. |
|400 |InvalidTagValue.Malformed |The specified TagValue is malformed. |The specified TagValue parameter format is invalid. |
|400 |LimitExceeded.ServiceManagedTag |You've reached the limit on the number of service managed tags that you can create. |You have reached the limit for the number of managed resource tag key\-value pairs that can be created in a single request. |
|400 |LimitExceeded.TagOperation |You've reached the limit on the number of tags that you can operate at a time. |You have reached the maximum number of tag entries that can be operated on in a single request. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the ''. |This request is missing a required parameter. Ensure the request includes all required parameters, such as . |
|400 |QuotaExceed.AclNumber |You've reached the limit on the number of ACL that you can create. |The quota limit for the number of ACLs that can be created has been reached. |
|403 |Forbidden |You are not authorized to perform operations on the service managed tag. |No permission to tag the specified resource with managed tags. |
|403 |Forbidden |You are not authorized to perform operations on the system tag. |No permission to tag the specified resource with a system tag. |
|404 |InvalidProject.NotFound |The specified Project does not exist. |The specified project does not exist. |
|409 |InvalidAclName.Conflict |The specified ACL Name already exits. |The specified ACL name already exists. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. |
