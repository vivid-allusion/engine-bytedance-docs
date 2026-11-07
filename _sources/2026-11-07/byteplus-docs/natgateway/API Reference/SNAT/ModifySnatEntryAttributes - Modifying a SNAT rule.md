---
title: "ModifySnatEntryAttributes - Modifying a SNAT rule"
product: "NAT Gateway"
product_code: "natgateway"
source: "https://docs.byteplus.com/en/docs/natgateway/ModifySnatEntryAttributes"
---

Call the ModifySnatEntryAttributes API to modify the name and associated elastic IP addresses (EIPs) of a SNAT entry.

<span id=".5L2_55So6K-05piO"></span>
## Instructions

Modifying the EIP in an SNAT rule will cause existing SNAT connections to terminate. The Elastic Compute Service (ECS) instances need to re\-initiate requests to establish new connections. Proceed with caution.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=ModifySnatEntryAttributes&groupName=SNAT%E8%A7%84%E5%88%99&serviceCode=natgateway&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|Cj1Cvz">必选</span> `Example: ModifySnatEntryAttributes`

The action that you want to perform. Value: ModifySnatEntryAttributes.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|uVxuVx">必选</span> `Example: 2020-04-01`

The API version. Value: 2020\-04\-01.



**SnatEntryName ** <span data-label="purple">string </span>`optional` `Example: test-another-name`

Name of the SNAT rule.


* Must start with a letter, Chinese character, or number. May include periods (.), underscores (_), and hyphens (\-).

* Must be 1 to 128 characters. If not provided, the original configuration remains.



**EipId ** <span data-label="purple">string </span>`optional` `Example: EipId=eip-2feaac9wtccn459gp67qe****`

The ID of the EIP associated with the Internet NAT gateway. Separate multiple EIP IDs with commas (,).

You can call [DescribeEipAddresses](https://docs.byteplus.com/en/docs/eip/DescribeEipAddressAttributes) to query the EIP ID.


* If a single EIP is specified, the SNAT rule will be associated with that IP. All business connections will then access the public Internet through this specific IP address.

* If multiple EIPs are specified, the SNAT rule will be associated with all of them. Business connections are distributed across these IPs based on a hash of their five\-tuple​.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When a SNAT rule is associated with multiple EIPs, we recommend adding the EIPs to a Bandwidth Package to prevent any traffic packet loss caused by any one EIP reaching its bandwidth cap.​​</div>




**NatIpId ** <span data-label="purple">string </span>`optional` `Example: vpcnatip-gw8y7q3cpk3fggs8****`

The ID of the NAT IP address used by the VPC NAT gateway.



**SnatEntryId ** <span data-label="purple">string </span><span data-api-tag="require|FJNr4I">必选</span> `Example: snat-2fedi096gdiww59gp680r****`

ID of the SNAT rule.

You can call the [DescribeSnatEntries](https://docs.byteplus.com/en/docs/natgateway/DescribeSnatEntries) API to query the SNAT rule ID.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**RequestId ** <span data-label="purple">string </span>`Example: 2021062415303301022514515207C4****`

Request ID.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```text
GET /?Action=ModifySnatEntryAttributes&Version=2020-04-01&SnatEntryId=snat-2fedi096gdiww59gp680r****&EipId=eip-2feaac9wtccn459gp67qe**** HTTP/1.1
Host: natgateway.cn-beijing.byteplusapi.com.cn
Service: natgateway
Region: cn-beijing
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "2021062415303301022514515207C4****",
        "Action": "ModifySnatEntryAttributes",
        "Version": "2020-04-01",
        "Service": "natgateway",
        "Region": "cn-beijing"
    },
    "Result":{
        "RequestId": "2021062415303301022514515207C4****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below describes the error codes for this API that are associated with business logic. For details, see [Common error codes](https://docs.byteplus.com/en/docs/natgateway/Public-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |MissingParameter |The request is missing a required parameter. |This request does not contain required parameters. |
|400 |InvalidEip.InstanceMismatch |The specified elastic ip and instance mismatch. |The specified EIP does not match the instance. |
|400 |InvalidNatGateway.InvalidStatus |The specified NAT gateway is not in the correct status for the request. |The specified NAT gateway cannot respond to this request due to its status. |
|400 |LimitExceeded.EipsPerSnatEntry |You've reached the limit on the number of EIPs per snat entry. |You have reached the maximum numebr of EIPs that can be associated per SNAT rule. |
|400 |InvalidSnatEntry.EipNotSupported |Can not create or modify SNAT entry with eip on the specified NAT gateway. |You cannot create or modify a SNAT rule that uses an EIP in the specified NAT gateway. |
|400 |InvalidSnatEntry.NatIpConflict |The specified nat ip and eip conflict. |The specified NAT IP conflicts with the EIP parameter. |
|400 |InvalidSnatEntry.NatIpNotSupported |Can not create or modify SNAT entry with nat ip on the specified NAT gateway. |You cannot create or modify a SNAT rule that uses a NAT IP in the specified NAT gateway. |
|400 |InvalidEip.InUse |The specified eip has been used by dnat entry of ip mapping. |The specified EIP is already used by a DNAT rule for IP mapping. |
|400 |InvalidEip.InvalidStatus |The specified elastic ip is not in the correct status for the request. The specified elastic ip is in freeze. |The specified EIP or VPC cannot respond to this request due to its status. The current EIP is frozen. |
|400 |InvalidName.Malformed |The specified name is malformed.Ensure the maximum length of name is 128. |The format of specified name is invalid. A name must not exceed 128 characters in length. |
|400 |InvalidName.Malformed |The specified name is malformed. |The format of the specified name is invalid. Correct the name format and retry. |
|400 |InvalidSnatEntry.InvalidStatus |The specified snat entry is not in the correct status for the request. |The specified SNAT rule cannot respond to this request due to its status. |
|404 |InvalidSnatEntry.NotFound |The specified snat entry does not exist. |The specified SNAT rule does not exist. |
|404 |InvalidEip.NotFound |The specified EIP does not exist. |The specified EIP does not exist. |
|404 |InvalidNatIp.NotFound |The specified nat ip does not exist. |The specified NAT IP does not exist. |
|409 |InvalidSnatEntry.EipConflict |The specified EIP conflicts with that of another EIP in the snat entry. |The EIP in the SNAT rule conflicted. |
|412 |InvalidNatGateway.Expired |The specified NatGateway has expired. |The specified NAT gateway is expired. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. |
