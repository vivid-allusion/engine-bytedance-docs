---
title: "AddAclEntries - Adding the IP entries to a specified ACL"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/ALB-AddAclEntries"
---

Call the AddAclEntries API to add IP entries to a specified ACL.

<span id=".5L2_55So6K-05piO"></span>
## Instructions


* Each ACL can contain up to 300 IP entries.

* The maximum number of IP entries that can be added in a single API call is 50.

* Submit up to 5 API requests per second.


<span id=".6K-35rGC6K-05piO"></span>
## Request description


* Method: **GET**

* URL:  **/?Action=AddAclEntries&Version=2020\-04\-01**


<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=AddAclEntries&groupName=%E8%AE%BF%E9%97%AE%E6%8E%A7%E5%88%B6&serviceCode=alb&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. More information can be found in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|T3Yz4d">必选</span> `Example: AddAclEntries`

Action to execute. Set the value to AddAclEntries.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|6QGaFx">必选</span> `Example: 2020-04-01`

The API version. Value: 2020\-04\-01.



**AclEntries.N.Entry ** <span data-label="purple">string[] </span><span data-api-tag="require|s4bbGy">必选</span> `Example: AclEntries.1.Entry=1.0.0.0/8&AclEntries.2.Entry=192.1.0.0/16`

The address range of the IP entry. Only CIDR addresses are supported.


* Parameter \- N: Indicates the serial number of the IP entry, with a maximum of 50 entries.

* Separate multiple IP entries with ampersands (&). When adding entries, duplicate IP entries or existing IP entries are automatically ignored.



**AclEntries.N.Description ** <span data-label="purple">string[] </span>`optional` `Example: AclEntries.1.Description=entry1&AclEntries.2.Description=entry2`

Description of the IP entry.


* Cannot start with http:// or https://.

* Must start with a letter or Chinese character and may include numbers, half\-width commas (,), periods (.), underscores (_), spaces ( ), equal signs (=), hyphens (\-), full\-width commas (，), and full\-width periods (。).

* Must be 1 to 255 characters.

* If left blank, this parameter defaults to an empty string.



**AclId ** <span data-label="purple">string </span><span data-api-tag="require|5RMS1y">必选</span> `Example: acl-3cj44nv0jhhxc6c6rrtet****`

The ID of the ACL to which ACL rules are to be added.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this API are listed below. More information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**RequestId ** <span data-label="purple">string </span>`Example: 20210811152539010225146063030****`

Request ID.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```text
GET /?Action=AddAclEntries&AclId=acl-33txelibucdfk57uhwmviq46o&AclEntries.1.Entry=1.0.0.0/8&AclEntries.1.Description=acl-rule-1&AclEntries.2.Entry=12.1.0.0/16&AclEntries.2.Description=acl-rule-2&Version=2020-04-01 HTTP/1.1
Host: alb.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/alb/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```text
{
    "ResponseMetadata": {
        "RequestId": "20210816184245010****46063050B4001",
        "Action": "AddAclEntries",
        "Version": "2020-04-01",
        "Service": "alb",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "20210816184245****25146063050B4001"
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
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, 'AclEntries'. |This request does not contain required parameters. Please ensure the request includes all required parameters, such as AclEntries. |
|400 |LimitExceed.AclEntry |You've reached the limit on the number of ACL entries that you can operate at a time. |You have reached the maximum number of IP entries that can be operated on in a single request. |
|400 |InvalidIndexOrder.Malformed |The specified index order is malformed. |The specified index order parameter format is invalid. |
|400 |InvalidAclEntries.Entry.Malformed |The specified AclEntries.Entry is malformed. |The specified AclEntries.Entry parameter format is invalid. |
|400 |InvalidAclEntries.Entry.Duplicated |The specified AclEntries.Entry is duplicated. |The specified AclEntries.Entry is duplicated. |
|400 |InvalidAclEntries.Description.Malformed |The specified AclEntries.Description is malformed. |The specified AclEntries.Description parameter format is invalid. |
|400 |InvalidAcl.InvalidStatus |The specified ACL is not in the correct status for the request. |The specified ACL is in a state that cannot respond to the request. |
|400 |QuotaExceed.IPPerAcl |You've reached the limit on the number of IPs per ACL you can add in, resource xxx, usage xx/xx. |The maximum number of IP entries that can be added to each ACL has been reached. The resource is xxx. Used: xxx. Quota: xxx |
|400 |QuotaExceed.AclEntriesPerInstance |You've reached the limit on the number of ACL entries per instance you can associate with, resource xxx, usage xx/xx. |The maximum number of ACL entries that can be associated with a single instance has been reached. The resource is xxx. Used: xxx. Quota: xxx |
|404 |InvalidAcl.NotFound |The specified ACL does not exist. |The specified ACL does not exist. |
|409 |InvalidAclEntries.Entry.Conflict |The specified AclEntries.Entry already exists. |The specified IP entry already exists. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Please try again later or contact an engineer for further consultation. |
