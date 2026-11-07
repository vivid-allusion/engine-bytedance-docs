---
title: "DeleteIpAddressPoolCidrBlock"
product: "Elastic IP Address"
product_code: "eip"
source: "https://docs.byteplus.com/en/docs/eip/DeleteIpAddressPoolCidrBlock"
---

Call the DeleteIpAddressPoolCidrBlock interface to delete a specified IP CIDR block from the IP address pool.

<span id="M4Lxb0j6"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=CreateIpAddressPool&data=%7B%7D&groupName=%E5%85%AC%E7%BD%91IP&query=%7B%7D&serviceCode=vpc&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request Parameters


|Parameter |Type |Required |Example Value |Description |
|---|---|---|---|---|
|Action |String |Yes |DeleteIpAddressPoolCidrBlock |The action that you want to perform. Value: **DeleteIpAddressPoolCidrBlock**. |
|Version |String |Yes |2020\-04\-01 |The version of the API request. The current version is 2020\-04\-01. |
|CidrBlock |String |Yes |101.0.XX.XX/24 |The specified CIDR block within the IP address pool.<br><br>You can call the [DescribeIpAddressPoolCidrBlocks](https://docs.byteplus.com/en/docs/eip/DescribeIpAddressPoolCidrBlocks) interface to query the IP address blocks within the IP address pool. |
|IpAddressPoolId |String |Yes |ippool\-fda83op\*\*\*\* |ID of the IP address pool.<br><br>You can call the [DescribeIpAddressPools](https://docs.byteplus.com/en/docs/eip/DescribeIpAddressPools) interface to query the ID of the IP address pool. |
|ClientToken |String |No |123e4567\-e89b\-12d3\-a456\-42665544\*\*\*\* |The client token that is used to ensure the idempotence of the request. You can use the client to generate the token, but you must make sure that the token is unique among different requests. This prevents repeated operations due to multiple client retries when the call of the API operation times out or an internal server error occurs. Valid range:<br><br><br>* It cannot exceed 64 ASCII characters in length. |


<span id=".6L-U5Zue5pWw5o2u"></span>
## Response parameters


|Parameter |Type |Example Value |Description |
|---|---|---|---|
|RequestId |String |2021062415303314515207C4\*\*\*\* |ID of the request. |


<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```Plain Text
GET /?Action=DeleteIpAddressPoolCidrBlock&Version=2020-04-01&CidrBlock=101.0.XX.XX/24&IpAddressPoolId=ippool-fda83op**** HTTP/1.1
Host: open.volcengineapi.com
Service: vpc
Region: cn-beijing
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response Example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20210624153033015207C4****",
        "Action": "DeleteIpAddressPoolCidrBlock",
        "Version": "2020-04-01",
        "Service": "vpc",
        "Region": "cn-beijing"
    },
    "Result":{
         "RequestId": "20210624153033015207C4****"
     }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

For more information on public error codes, refer to [Public error codes](https://docs.byteplus.com/en/docs/eip/Public-error-codes).


|HTTP Code |Error codes |Error Message |Description |
|---|---|---|---|
|400 |IdempotentParameterMismatch |Arguments on this idempotent request are inconsistent with arguments used in previous request(s). |The parameters in this idempotent request are inconsistent with those in the previous request. |
||InvalidCidr.Malformed |The specified cidr block is malformed. |The specified CIDR block is invalid. |
||InvalidIPPool.InvalidStatus |The specified IP address pool is not in the correct status for the request. |The current status of the specified IP address pool cannot respond to the request. |
||InvalidIPPoolCidrBlock.InUse |The specified CIDR block of IP address pool has dependent resource of an EIP. |The specified CIDR block of IP address pool has allocated EIP and cannot delete. |
||InvalidIPPoolCidrBlock.InvalidStatus |The specified CIDR block of IP address pool is not in the correct status for the request. |The specified IP address pool CIDR block is not in a status to respond to this request. |
||InvalidParameter.ClientTokenMalformed |The specified parameter ClientToken is malformed. |The specified client token is invalid and cannot exceed 64 ASCII characters in length. |
||QuotaExceeded.IPPoolIP |You've reached the limit on the number of IPs of all IP address pools that you can possess. |You have reached the maximum IP address count for all IP address pools. |
|404 |InvalidIPPool.NotFound |The specified IP address pool does not exist. |The specified IP address pool does not exist. |
||InvalidIPPoolCidrBlock.NotFound |The specified CIDR block of IP address pool does not exist. |The specified CIDR block of IP address pool does not exist. |
|412 |IdempotentProcessing |The request uses the same client token as previous one that is still in process. |The idempotent request is being processing. |
