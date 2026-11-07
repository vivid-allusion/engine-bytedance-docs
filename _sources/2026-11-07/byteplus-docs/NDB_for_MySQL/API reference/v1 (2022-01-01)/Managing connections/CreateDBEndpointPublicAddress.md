---
title: "CreateDBEndpointPublicAddress"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/CreateDBEndpointPublicAddress"
---

Call the CreateDBEndpointPublicAddress to enable public network access for instance.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Asynchronous request.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* The [AllocateEipAddress](https://docs.byteplus.com/en/docs/eip/AllocateEipAddress) API has been called to request a public IP address.

* A public address is associated with an Elastic IP Address (EIP). Using an EIP incurs charges at EIP billing rates. For more information about public IP address billing, refer to [Billing overview](https://docs.byteplus.com/en/docs/eip/Billing-overview).


<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=CreateDBEndpointPublicAddress&serviceCode=vedbm&version=2022-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Name** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |vedbm\-ca12cbqv\*\*\*\* |Instance ID.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can call the <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeDBInstances">DescribeDBInstances</a> API to query the basic information of all instances in the target region, including their instance IDs.</div><br> |
|EndpointId |String |Yes |vedbm\-h5u625wj\*\*\*\*\-Primary |Instance endpoint ID.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can call the <a href="https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeDBInstanceDetail">DescribeDBInstanceDetail</a> interface to query the details of the instance, including the instance endpoint ID.</div><br> |
|EipId |String |Yes |eip\-2fef2qcfbfw8w5oxruw3w\*\*\*\* |The EIP ID to bind to the instance.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can call the <a href="https://docs.byteplus.com/en/docs/eip/DescribeEipAddressAttributes">DescribeEipAddresses</a> interface to query the details of created EIPs, including the EIP ID.</div><br> |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter

null

<span id=".56S65L6L"></span>
## Example

<span id=".6K-35rGC56S65L6L"></span>
### Request example

```JSON
POST /?Action=CreateDBEndpointPublicAddress&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host:vedbm.cn-beijing.byteplusapi.com.cn
X-Date: 20220101T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20220101/cn-beijing/vedbm/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c645****
{
    "InstanceId": "vedbm-h5u625wj****",
    "EndpointId": "vedbm-h5u625wj****-Primary",
    "EipId": "eip-3rfb9a0cyyg3k5zsk2ili****"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Response example

```JSON
{
     "ResponseMetadata": {
          "RequestId": "2022042511062201022509900802EB****",
          "Action": "CreateDBEndpointPublicAddress",
          "Version": "2022-01-01",
          "Service": "vedbm",
          "Region": "cn-beijing",
     },
     "Result": null
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

For details, refer to [Error codes](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Error_codes).
