---
title: "ModifyAclAttributes - Modifying the ACL attributes"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/ModifyAclAttributes"
---

Call the ModifyAclAttributes API to modify the specified ACL.

<span id=".5L2_55So6K-05piO"></span>
## Instructions

When calling this API, if an optional parameter is not configured, its existing configuration remains unchanged.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifyAclAttributes&serviceCode=clb&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters



**Action ** <span data-label="purple">String </span><span data-api-tag="require|iOSA8t">必选</span> `Example: ModifyAclAttributes`

Action to execute. Set the value to **ModifyAclAttributes**.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|znehPw">必选</span> `Example: 2020-04-01`

API version. The current version is **2020\-04\-01**.



**AclId ** <span data-label="purple">String </span><span data-api-tag="require|XzjI3a">必选</span> `Example: acl-3cj44nv0jhhxc6c6rrtet****`

ACL ID.

You can call the [DescribeAcls](https://docs.byteplus.com/en/docs/clb/DescribeAcls) API to query the ACL ID.



**AclName ** <span data-label="purple">String </span>`optional` `Example: myacl`

ACL name.


* Must start with a letter, number, or Chinese character. May include letters, numbers, Chinese characters, periods (.), underscores (_), and hyphens (\-).

* Length limit is 1 to 128 characters.



**Description ** <span data-label="purple">String </span>`optional` `Example: This is an acl.`

ACL description.


* Must start with a letter, number, or Chinese character. May include letters, numbers, Chinese characters, and the following symbols: commas (,), periods (.), underscores (_), spaces ( ), equal signs (=), hyphens (\-), full\-width commas ( ， ), and full\-width periods ( 。 ).

* The length limit is 0 to 255 characters.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**RequestId ** <span data-label="purple">String </span>`Example: 20210811152539010225146063030****`

Request ID.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=ModifyAclAttributes&Version=2020-04-01&AclId=acl-3cj44nv0jhhxc6c6rrtet****&AclName=myacl&Description=This is an acl.
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
        "Action": "ModifyAclAttributes",
        "Version": "2020-04-01",
        "Service": "clb",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "20210811152539010225146063030****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

This section displays only the error codes of the current API. For more error codes, see [Common error codes](https://docs.byteplus.com/en/docs/clb/Public-error-codes).


|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |InvalidAcl.InvalidStatus |The specified ACL is not in the correct status for the request. |The specified ACL is in a state that cannot respond to this request. |
|400 |InvalidDescription.Malformed |The specified Description is malformed. |The format specified for Description is invalid. |
|400 |InvalidName.Malformed |The specified Name is malformed. |The format specified for Name is invalid. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the 'AclId'. |This request does not contain required parameters. Please ensure the request includes all required parameters, such as AclId. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the ''. |This request is missing a required parameter. Ensure the request includes all required parameters, such as . |
|403 |InvalidResourceType.ServcieManaged |The specified ResourceType is managed by a service. |The specified resource is a service\-managed resource. |
|404 |InvalidAcl.NotFound |The specified ACL does not exist. |The specified ACL does not exist. |
|409 |InvalidAclName.Conflict |The specified ACL Name already exits. |The specified ACL name already exists. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. |
