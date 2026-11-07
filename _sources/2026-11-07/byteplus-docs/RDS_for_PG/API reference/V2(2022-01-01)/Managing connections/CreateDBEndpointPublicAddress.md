---
title: "CreateDBEndpointPublicAddress"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/deletedbendpoint"
---

Call the CreateDBEndpointPublicAddress API to create a public address.

<span id=".6K-35rGC57G75Z6L"></span>
## Request type

Synchronous request.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* The public network address is associated with an [Elastic IP Address (EIP)](https://docs.byteplus.com/en/docs/eip/What-is-EIP) . Using an EIP is billed according to EIP billing standards. For more billing information about public network IPs, refer to [Elastic IP Address](https://docs.byteplus.com/en/docs/eip/Billing-overview).

* A pay\-as\-you\-go EIP enters the **Closed** status after it falls into arrears for two hours and is automatically disassociated from resources. If your PostgreSQL instance is associated with a pay\-as\-you\-go EIP, you are recommended to pay close attention to the account balance and top it up in good time to avoid unavailability of the instance public address due to arrears. For more information about public IP address billing, refer to [Elastic IP Address](https://docs.byteplus.com/en/docs/eip/Arrears).

* An instance enters the shut\-down status when the account is in arrears for 2 hours. During this period, after you top up your account, settle the overdue bills, and have an available balance greater than 0, the instance status will automatically restore to **Running**. However, released EIPs will not be re\-associated with the instance. You need to manually enable public access and bind a new EIP to the instance.


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Required?**  |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |postgres\-ca7b7019\*\*\*\* |Instance ID. |
|EndpointId |String |No |postgres\-ca7b7019\*\*\*\*\-custom\-f07b |Instance connection endpoint ID. If not set, the default endpoint is selected. |
|EipId |String |Yes |eip\-3jhjud2zgy1og3pncmeh7\*\*\*\* |ID of the EIP. Use the [DescribeEipAddressAttributes](https://docs.byteplus.com/en/docs/eip/DescribeEipAddresses) API to query the basic information of the EIP. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter

null

<span id=".56S65L6L"></span>
## Sample

<span id=".6K-35rGC56S65L6L"></span>
### Sample request

```json
POST /?Action=CreateDBEndpointPublicAddress&Version=2022-01-01 HTTP/1.1
Content-Type: application/json
Host: rds-postgresql.cn-beijing.byteplusapi.com.cn
X-Date: 20231002T101010Z
Authorization: HMAC-SHA256 Credential=AKLTN2I0MmFiNzMxNWE5NDgzMzk4MmVjMTVkODlkZTZ****/20211202/cn-beijing/rds_postgresql/request,SignedHeaders=x-date, Signature=71d31fc7bcf990142851c9833c5656391486cda0ae2e0b8ada733b7c6458****
{
    "InstanceId": "postgres-ca7b7019****",
    "EndpointId": "postgres-ca7b7019****-custom-f07b",
    "EipId": "eip-3jhjud2zgy1og3pncmeh7****"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202308021632037746FBCF122026EECAB5",
        "Action": "CreateDBEndpointPublicAddress",
        "Version": "2022-01-01",
        "Service": "rds_postgresql",
        "Region": "cn-beijing"
    },
    "Result": null
}
```
