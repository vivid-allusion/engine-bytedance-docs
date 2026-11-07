---
title: "DescribeAclAttributes - Querying the details of the specified ACL"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/ALB-DescribeAclAttributes"
---

Call the DescribeAclAttributes API to view the details of the specified Access Control List (ACL).

<span id=".5L2_55So6K-05piO"></span>
## Instructions

Submit up to 200 API requests per second.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=DescribeAclAttributes&groupName=%E8%AE%BF%E9%97%AE%E6%8E%A7%E5%88%B6&serviceCode=alb&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. More information can be found in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|eGcVQ5">必选</span> `Example: DescribeAclAttributes`

Action to execute. Set the value to DescribeAclAttributes.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|f9yRr6">必选</span> `Example: 2020-04-01`

The API version. Value: 2020\-04\-01.



**AclId ** <span data-label="purple">string </span><span data-api-tag="require|kbZPgF">必选</span> `Example: acl-3cj44nv0jhhxc6c6rrtet****`

ACL ID.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this API are listed below. More information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**RequestId ** <span data-label="purple">string </span>`Example: 20210811152539010225146063030****`

Request ID.



**AclId ** <span data-label="purple">string </span>`Example: acl-3cj44nv0jhhxc6c6rrtet****`

ACL ID.



**AclName ** <span data-label="purple">string </span>`Example: myacl`

ACL name.



**CreateTime ** <span data-label="purple">string </span>`Example: 2021-08-11T16:37:37Z`

Creation time of ACL.



**UpdateTime ** <span data-label="purple">string </span>`Example: 2021-08-11T16:37:37Z`

Last operation time of ACL.



**AclEntries ** <span data-label="purple">object[] </span>`Example: --`

IP entry list in ACL.


**Description ** <span data-label="purple">string </span>`Example: entry1`

Description of the IP entry.



**Entry ** <span data-label="purple">string </span>`Example: 192.XX.XX.7/16`

The address range of the IP entry.




**Listeners ** <span data-label="purple">object[] </span>`Example: --`

List of listeners associated with ACL.


**AclType ** <span data-label="purple">string </span>`Example: white`

The control method of the listener over this ACL.


* white: Allowlist method. Indicates that the listener forwards requests only from the IP addresses or CIDR blocks set in the selected access control policy group. If no IPs are added to the selected policy group, the listener does not forward any requests.

* black: Denylist method. Indicates that the listener denies requests only from the IP addresses or CIDR blocks set in the selected access control policy group. If no IPs are added to the selected policy group, the listener forwards all requests.



**ListenerId ** <span data-label="purple">string </span>`Example: lsn-2fek3rgsxhrsw5oxruwec****`

Listener ID.



**ListenerName ** <span data-label="purple">string </span>`Example: mylistener`

Listener name.



**Port ** <span data-label="purple">integer </span>`Example: 88`

Listener port.



**Protocol ** <span data-label="purple">string </span>`Example: HTTP`

Listener protocol.




**Description ** <span data-label="purple">string </span>`Example: test`

ACL description.



**ProjectName ** <span data-label="purple">string </span>`Example: default`

The name of the project to which ACL belongs.



**Tags ** <span data-label="purple">object[] </span>`Example: --`

Tags attached to ACL.


**Key ** <span data-label="purple">string </span>`Example: key`

The tag key of the custom tag.



**Value ** <span data-label="purple">string </span>`Example: value`

The tag value of the custom tag.




**Status ** <span data-label="purple">string </span>`Example: Active`

ACL status.


* Creating

* Active

* Deleting

* Configuring



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```text
GET /?Action=DescribeAclAttributes&AclId=acl-33txelibucdfk57uhwmviq46o&Version=2020-04-01 HTTP/1.1
Host: alb.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/alb/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```text
{
    "ResponseMetadata": {
        "RequestId": "d9e8b282-d9a0-4d58-84f7-91f482960b6b",
        "Action": "DescribeAclAttributes",
        "Version": "2020-04-01",
        "Service": "alb",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "d9e8b282-d9a0-4d58-84f7-91f482960b6b",
        "CreateTime": "2022-02-22T08:34:34Z",
        "UpdateTime": "2022-02-23T06:21:31Z",
        "AclId": "acl-33txelibucdfk57uhwmviq46o",
        "AclName": "yxl-test",
        "Description": "yxl-test",
        "AclEntries": [
            {
                "Entry": "1.0.0.0/8",
                "Description": "acl-rule-1"
            },
            {
                "Entry": "12.1.0.0/16",
                "Description": "acl-rule-2"
            }
        ],
        "Listeners": null
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
|404 |InvalidAcl.NotFound |The specified ACL does not exist. |The specified ACL does not exist. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Please try again later or contact an engineer for further consultation. |
