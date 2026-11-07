---
title: "ModifyAclAttributes - Modifying the specified ACL"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/ALB-ModifyAclAttributes"
---

Call the ModifyAclAttributes API to modify the specified Access Control List (ACL).

<span id=".5L2_55So6K-05piO"></span>
## Instructions

Submit up to 10 API requests per second.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifyAclAttributes&serviceCode=alb&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters



**Action ** <span data-label="purple"> String  </span><span data-api-tag="require|Xq8bMJ">必选</span> `Example: ModifyAclAttributes`

The interface name. The current API name is `ModifyAclAttributes`.



**Version ** <span data-label="purple"> String  </span><span data-api-tag="require|j3oj33">必选</span> `Example: 2020-04-01`

The interface version. the current API version is `2020-04-01`.



**AclId ** <span data-label="purple"> String  </span><span data-api-tag="require|KpAdUG">必选</span> `Example: acl-3cj44nv0jhhxc6c6rrtet****`

ACL ID.



**AclName ** <span data-label="purple">String</span> `optional` `Example: myacl`

ACL name.



**Description ** <span data-label="purple"> String </span>`optional` `Example: This is a acl.`

ACL description.


* Cannot start with http:// or https://.

* Must start with a letter or Chinese character and may include numbers, half\-width commas (,), periods (.), underscores (_), spaces ( ), equal signs (=), hyphens (\-), full\-width commas (，), and full\-width periods (。).

* Must be 1 to 255 characters.

* If left blank, it defaults to the original Description.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**RequestId ** <span data-label="purple"> String  </span>`Example: 20210811152539010225146063030****`

Request ID.



<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```JSON
GET /?Action=ModifyAclAttributes&AclId=acl-33txelibucdfk57uhwmviq46o&AclName=myacl1&Description=yxl-test-2&Version=2020-04-01 HTTP/1.1
Host: alb.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/alb/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```JSON
{
    "ResponseMetadata": {
        "RequestId": "2021081613260****22524310001FAA1DB",
        "Action": "ModifyAclAttributes",
        "Version": "2020-04-01",
        "Service": "alb",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "2021081613260****22524310001FAA1DB"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

If the response body contains an Error field, it indicates the API request failed. This section displays only the error codes of the current API. For more error codes, see [Common error codes](https://docs.byteplus.com/en/docs/clb/Error-codes).


|**Status code** |**Error codes** |**Error message** |**Notes** |
|---|---|---|---|
|400 |InvalidAclName.Malformed |The specified AclName is malformed. |The specified AclName parameter format is invalid. |
|400 |InvalidDescription.Malformed |The specified Description is malformed. |The format specified for Description is invalid. |
|400 |InvalidAcl.InvalidStatus |The specified ACL is not in the correct status for the request. |The specified ACL is in a state that cannot respond to the request. |
|404 |InvalidAcl.NotFound |The specified ACL does not exist. |The specified ACL does not exist. |
