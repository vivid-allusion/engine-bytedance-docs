---
title: "DisassociateVpcUserCidrBlock - Deleting a specified VPC user CIDR block"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/DisassociateVpcUserCidrBlock"
---

Call the DisassociateVpcUserCidrBlock API to delete the specified VPC user CIDR block.

<div data-tips="true" data-tips-type="default">Explain</div>


<div data-tips="true" data-tips-type="default">Adding User CIDR Block for VPCs is currently in Beta stage. If you need a trial, please contact your account manager.</div>


<span id=".5L2_55So6K-05piO"></span>
## Instructions

AssociateVpcUserCidrBlock an asynchronous API. When a request ID is returned, the system is still configuring in the background. You can call [DescribeVpcAttributes](https://docs.byteplus.com/en/docs/vpc/DescribeVpcAttributes) API to check the status of a VPC. Pending indicates the VPC is being configured, and Available indicates the configuration is complete.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DisassociateVpcUserCidrBlock&serviceCode=vpc&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. More information is available in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|GO3jdg">必选</span> `Example value: DisassociateVpcUserCidrBlock`

The interface name. The current API name is `DisassociateVpcUserCidrBlock`.



**Version ** <span data-label="purple"> String  </span><span data-api-tag="require|Zadflq">必选</span> `Example value: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**VpcId ** <span data-label="purple"> String  </span><span data-api-tag="require|PZwg1e">必选</span> `Example value: vpc-257gqcdfvx6n****`

VPC ID.

You can call the [DescribeVpcs](https://docs.byteplus.com/en/docs/vpc/DescribeVpcs) API to query the VPC ID.



**UserCidrBlock ** <span data-label="purple"> String  </span><span data-api-tag="require|Pn9V7r">必选</span> `Example value: 172.16.XX.0/24`

The user CIDR block is pending deletion.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**RequestId ** <span data-label="purple">String </span>`optional` `Example value: 2021062415303301022514515207C4****`

Request ID.



<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```JSON
GET /?Action=DisassociateVpcUserCidrBlock&Version=2020-04-01&VpcId=vpc-257gqcdfvx6n****&UserCidrBlock=172.16.XX.0/24 HTTP/1.1
Host: vpc.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/vpc/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```JSON
{
    "ResponseMetadata": {
        "RequestId": "2021062415303301022514515207C4****",
        "Action": "DisassociateVpcUserCidrBlock",
        "Version": "2020-04-01",
        "Service": "vpc",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "2021062415303301022514515207C4****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes


|**Status code** |**Error codes** |**Error message** |**Explain** |
|---|---|---|---|
|400 |DryRunOperation |Exception raised to indicate a successfully authorized action when the DryRun flag is set to true. |This request is set to DryRun. The action is authorized but not executed. |
|400 |InvalidCidr.Malformed |The specified cidr block is malformed. |The format of the specified CIDR block is invalid. |
|400 |InvalidUserCidrBlock.NotFound |The specified user CIDR block is not found. |The specified user CIDR block is not within the specified VPC. |
|400 |InvalidVpc.InvalidStatus |The specified VPC is not in the correct status for the request. |The specified VPC is in a state that cannot respond to this request. |
|400 |QuotaExceeded.VpcUserCidr |You've reached the limit on the number of user cidr blocks per VPC. |The maximum number of user CIDR blocks allowed for the VPC has been reached. |
|404 |InvalidVpc.NotFound |The specified VPC does not exist. |The specified VPC does not exist. |
