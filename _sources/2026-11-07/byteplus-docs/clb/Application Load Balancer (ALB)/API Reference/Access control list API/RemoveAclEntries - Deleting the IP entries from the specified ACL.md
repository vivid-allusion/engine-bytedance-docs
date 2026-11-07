---
title: "RemoveAclEntries - Deleting the IP entries from the specified ACL"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/ALB-RemoveAclEntries"
---

Call the RemoveAclEntries API to delete IP entries from the specified ACL.

<span id=".5L2_55So6K-05piO"></span>
## Instructions


* The maximum number of IP entries that can be deleted in a single API call is 50.

* Submit up to 5 API requests per second.


<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=RemoveAclEntries&serviceCode=alb&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters



**Action ** <span data-label="purple">String</span> <span data-api-tag="require|JGyaHn">必选</span>`Example: RemoveAclEntries`

The interface name. The current API name is `RemoveAclEntries`.



**Version ** <span data-label="purple"> String  </span><span data-api-tag="require|suIPbc">必选</span> `Example: 2020-04-01`

The interface version. the current API version is `2020-04-01`.



**AclId ** <span data-label="purple"> String  </span><span data-api-tag="require|o0ylrm">必选</span> `Example: acl-3cj44nv0jhhxc6c6rrtet****`

ACL ID.



**Entries.N ** <span data-label="purple"> String[] </span><span data-api-tag="require|R5-DSV">必选</span>`Example: Entries.1=192.XX.XX.7/16& Entries.2=172.XX.XX.0/24`

The address range of the IP entry.


* Parameter \- N: Indicates the serial number of the IP entry, with a maximum of 50 entries.

* Separate multiple IP entries with ampersands (&).



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**RequestId ** <span data-label="purple"> String </span>`Example: Request ID.`

20210811152539010225146063030\*\*\*\*



<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```JSON
GET /?Action=RemoveAclEntries&AclId=acl-33txelibucdfk57uhwmviq46o&Entries.1=1.0.0.0/8&Version=2020-04-01 HTTP/1.1
Host: alb.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/alb/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```JSON
{
    "ResponseMetadata": {
        "RequestId": "2021081618465****225142142010A77B9",
        "Action": "RemoveAclEntries",
        "Version": "2020-04-01",
        "Service": "alb",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "202108161846****0225142142010A77B9"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

If the response body contains an Error field, it indicates the API request failed. This section displays only the error codes of the current API. For more error codes, see [Common error codes](https://docs.byteplus.com/en/docs/clb/Error-codes).


|**Status code** |**Error codes** |**Error message** |**Notes** |
|---|---|---|---|
|400 |LimitExceed.AclEntry |You've reached the limit on the number of ACL entries that you can operate at a time. |You have reached the maximum number of IP entries that can be operated on in a single request. |
|400 |InvalidAclEntries.Entry.Duplicated |The specified AclEntries.Entry is duplicated. |The specified AclEntries.Entry is duplicated. |
|400 |InvalidIndexOrder.Malformed |The specified index order is malformed. |The specified index order parameter format is invalid. |
|400 |InvalidAcl.InvalidStatus |The specified ACL is not in the correct status for the request. |The specified ACL is in a state that cannot respond to the request. |
|404 |InvalidAcl.NotFound |The specified ACL does not exist. |The specified ACL does not exist. |
|404 |InvalidAclEntry.NotFound |The specified AclEntry does not exist. |The specified IP entry does not exist. |
