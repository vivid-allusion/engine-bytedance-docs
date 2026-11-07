---
title: "AddAclEntries - Adding the ACL entries"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/AddAclEntries"
---

Call the AddAclEntries API to add IP entries to a specified ACL.

<span id=".5L2_55So6K-05piO"></span>
## Instructions

Each ACL can contain up to 300 IP entries.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=AddAclEntries&serviceCode=clb&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters



**Action ** <span data-label="purple">String </span><span data-api-tag="require|AnUH17">必选</span> `Example: AddAclEntries`

Action to execute. Set the value to **AddAclEntries**.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|HTp4mS">必选</span> `Example: 2020-04-01`

API version. The current version is **2020\-04\-01**.



**AclId ** <span data-label="purple">String </span><span data-api-tag="require|33ZjlE">必选</span> `Example: acl-3cj44nv0jhhxc6c6rrtet****`

ACL ID. You can call the [DescribeAcls](https://docs.byteplus.com/en/docs/clb/DescribeAcls) API to get the ACL ID.



**AclEntries.N.Entry ** <span data-label="purple">String </span><span data-api-tag="require|KmxZh0">必选</span> `Example: 192.168.1.7/32`

The address range of the IP entry. Only CIDR addresses are supported.


* Parameter \- N: Indicates the serial number of the IP entry, ranging from 1 to 50.

* IPv4 and IPv6 entries can be passed simultaneously.

* Separate multiple IP entries with ampersands ( & ).

* The IP address/address range cannot be `0.0.0.0, 0.0.0.0/x` or `::/x`.

* The IP address range must be in **standard format**, with the **IP and mask matching**. For example, `192.168.0.0/16` is correct, while `192.168.1.0/16` is incorrect.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">If the CLB instance to which the listener belongs is of IPv4 type, then after ACL is associated with the listener, the added IPv6 entries will not take effect.</div>


* <div data-tips="true" data-tips-type="tip">The dual\-stack load balancer is in beta stage. Currently, only accounts that have completed enterprise verification can apply for a trial. To request a trial, please contact your account manager.</div>




**AclEntries.N.Description ** <span data-label="purple">String </span>`optional` `Example: entry1`

The description of the IP entry. The default value is an empty string.


* Parameter \- N: Indicates the serial number of the IP entry, ranging from 1 to 50.

* Separate multiple IP entries with ampersands ( & ).

* The requirements are as follows:

   * Must start with a letter, number, or Chinese character. May include letters, numbers, Chinese characters, and the following symbols: commas (,), periods (.), underscores (_), spaces ( ), equal signs (=), hyphens (\-), full\-width commas ( ， ), and full\-width periods ( 。 ).

   * The length limit is 0 to 255 characters.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**RequestId ** <span data-label="purple">String </span>`Example: 20210811152539010225146063030****`

Request ID



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=AddAclEntries&Version=2020-04-01&AclId=acl-3cj44nv0jhhxc6c6rrtet****&AclEntries.1.Entry=192.168.1.7/32&AclEntries.1.Description=entry1
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
        "Action": "AddAclEntries",
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
|400 |InvalidAcl.InvalidStatus |The specified ACL is not in the correct status for the request. |The specified ACL is in a state that cannot respond to the request. |
|400 |InvalidCIDR.Malformed |The specified CIDR is malformed. |The format specified for CIDR is invalid. |
|400 |InvalidDescription.Malformed |The specified Description is malformed. |The format specified for Description is invalid. |
|400 |InvalidIncorrectOrder.Malformed |The specified index order is malformed. |The specified index order parameter format is invalid. |
|400 |LimitExceeded.IPOperation |You've reached the limit on the number of IP that you can operate at a time. |You have reached the maximum number of IP entries that can be operated on in a single request. |
|400 |LimitExceeded.IPTotal |You've reached the limit on the total number of IP that you can create in an ACL. |The maximum number of IP addresses that can be added has been reached. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the 'AclId'. |This request does not contain required parameters. Please ensure the request includes all required parameters, such as AclId. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the ''. |This request is missing a required parameter. Ensure the request includes all required parameters, such as . |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request; for example, the 'AclEntries'. |This request is missing a required parameter. Please ensure the request includes all required parameters, such as AclEntries. |
|403 |InvalidResourceType.ServcieManaged |The specified ResourceType is managed by a service. |The specified resource is a service\-managed resource. |
|404 |InvalidAcl.NotFound |The specified ACL does not exist. |The specified ACL does not exist. |
|409 |InvalidEntry.Conflict |The specified ACL Entry already exits. |The specified IP entry of ACL already exists. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. |
