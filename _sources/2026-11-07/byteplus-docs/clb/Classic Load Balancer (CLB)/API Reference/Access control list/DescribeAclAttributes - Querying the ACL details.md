---
title: "DescribeAclAttributes - Querying the ACL details"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/DescribeAclAttributes"
---

Call the DescribeAclAttributes API to view details of the specified ACL.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeAclAttributes&serviceCode=clb&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters



**Action ** <span data-label="purple">String </span><span data-api-tag="require|n455Vz">必选</span> `Example: DescribeAclAttributes`

Action to execute. Set the value to **DescribeAclAttributes**.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|5kvHwG">必选</span> `Example: 2020-04-01`

API version. The current version is **2020\-04\-01**.



**AclId ** <span data-label="purple">String </span><span data-api-tag="require|BmEo3m">必选</span> `Example: acl-3cj44nv0jhhxc6c6rrtet****`

ACL ID.

You can call the [DescribeAcls](https://docs.byteplus.com/en/docs/clb/DescribeAcls) API to query the ACL ID.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**RequestId ** <span data-label="purple">String </span>`Example: 20210811152539010225146063030****`

Request ID.



**AclId ** <span data-label="purple">String </span>`Example: acl-3cj44nv0jhhxc6c6rrtet****`

ACL ID.



**AclName ** <span data-label="purple">String </span>`Example: myacl`

ACL name.



**Description ** <span data-label="purple">String </span>`Example: test`

ACL description.



**AclEntries ** <span data-label="purple">Object[] </span>`Example: -`

Details of the IP entries in the ACL.


**Entry ** <span data-label="purple">String </span>`Example: 192.XX.XX.7/16`

The address range of the IP entry.



**Description ** <span data-label="purple">String </span>`Example: entry1`

Description of the IP entry.




**Listener** <span data-label="purple">Object[]</span> `Example: -`

Details of listeners associated with ACL.


**ListenerId ** <span data-label="purple">String </span>`Example: lsn-2fek3rgsxhrsw5oxruwec****`

Listener ID.



**ListenerName ** <span data-label="purple">String </span>`Example: mylistener`

Listener name.



**Protocol ** <span data-label="purple">String </span>`Example: TCP`

The protocol of the listener.


* TCP

* UDP

* HTTP

* HTTPS



**Port ** <span data-label="purple">Integer </span>`Example: 88`

Port of the listener.



**AclType ** <span data-label="purple">String </span>`Example: white`

The control method of the listener over this ACL.


* white: Allowlist. When the listener listens to the traffic of the CLB, the CLB only forwards requests from IP addresses that are in the ACL associated with its allowlist.

* black: Denylist. When the listener listens to the traffic of the CLB, the CLB refuses to forward requests from IP addresses that are in the ACL associated with its allowlist.




**ServiceManaged ** <span data-label="purple">Boolean </span>`Example: false`

It is a managed resource.


* true: Yes

* false: No.



**Status ** <span data-label="purple">String </span>`Example: Active`

ACL status.


* Creating

* Active: Available

* Configuring

* Deleting



**ProjectName ** <span data-label="purple">String </span>`Example: default`

The name of the project to which ACL belongs.



**Tags ** <span data-label="purple">Object[] </span>`Example: -`

Details of ACL tags.


**Key ** <span data-label="purple">String </span>`Example: k1`

The tag key.



**Value ** <span data-label="purple">String </span>`Example: v1`

The tag value.




**CreateTime ** <span data-label="purple">String </span>`Example: 2021-08-11T16:37:37Z`

Creation time of ACL.



**UpdateTime ** <span data-label="purple">String </span>`Example: 2021-08-11T16:37:37Z`

Last operation time of ACL.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=DescribeAclAttributes&Version=2020-04-01&AclId=acl-3cj44nv0jhhxc6c6rrtet****
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
        "Action": "DescribeAclAttributes",
        "Version": "2020-04-01",
        "Service": "clb",
        "Region": "cn-beijing"
    },
    "Result": {
        "AclEntries": [
            {
                "Entry": "192.XX.XX.7/16",
                "Description": "entry1"
            }
        ],
        "AclId": "acl-3cj44nv0jhhxc6c6rrtet****",
        "AclName": "myacl",
        "CreateTime": "2021-08-11T16:37:37Z",
        "Description": "test",
        "Listeners": [
            {
                "Port": 88,
                "AclType": "white",
                "Protocol": "TCP",
                "ListenerId": "lsn-2fek3rgsxhrsw5oxruwec****",
                "ListenerName": "mylistener"
            }
        ],
        "ProjectName": "default",
        "RequestId": "20210811152539010225146063030****",
        "ServiceManaged": true,
        "Status": "Active",
        "Tags": [
            {
                "Key": "k1",
                "Value": "v1"
            }
        ],
        "UpdateTime": "2021-08-11T16:37:37Z"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

This section displays only the error codes of the current API. For more error codes, see [Common error codes](https://docs.byteplus.com/en/docs/clb/Public-error-codes).


|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the 'AclId'. |This request is missing a required parameter. Please ensure the request includes all required parameters, such as AclId. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the ''. |This request does not contain required parameters. Ensure the request includes all required parameters, such as . |
|404 |InvalidAcl.NotFound |The specified ACL does not exist. |The specified ACL does not exist. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. |
