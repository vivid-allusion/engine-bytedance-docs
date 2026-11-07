---
title: "ModifyDBInstanceSubnet"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/modifydbinstancesubnet"
---

Call the ModifyDBInstanceSubnet API to associate the target Redis instance to a specified subnet.

## Request type

Asynchronous request.

## Precautions

* Since May 17, 2022, customers who newly activate Redis and customers with existing instances must complete cross\-service access authorization. Complete the authorization as soon as possible, otherwise, calling interfaces such as [CreateDBInstance](https://docs.byteplus.com/en/docs/redis/createdbinstance), [ModifyDBInstanceSubnet](https://docs.byteplus.com/en/docs/redis/modifydbinstancesubnet), and [CreateDBEndpointPublicAddress](https://docs.byteplus.com/en/docs/redis/createdbendpointpublicaddress) will result in an error.

   For information on cross\-service access authorization, see [Cross-Service Access Authorization](https://docs.byteplus.com/en/docs/redis/cross-service-access-authorization).

## Operation impact

* During network configuration changes (including modifications to private networks or subnets), all connection addresses (such as private addresses, direct connect addresses, and public addresses) may experience 1\-2 temporary disconnections. Please proceed with caution. It is recommended to perform changes during off\-peak business hours and ensure the business has an automatic reconnection mechanism.

* Modifying the VPC and subnet does not change the domain name of the private endpoint or direct connection endpoint, but their corresponding IP addresses change. Make sure that your services connect by using domain names and that the network environment of your services can communicate with the newly configured network environment.

* Promptly clear the client cache, or else read/write exceptions may occur.

* Modifying the VPC and subnet temporarily affects the use of database ecosystem products such as DTS and DBW.

## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifyDBInstanceSubnet&serviceCode=Redis&version=2020-12-07&groupName=连接管理)

## Request parameters

|**Parameters** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |redis\-cn0212gzmh2xs1111 |Instance ID.<br><br>> **tip**<br><br><br>> Call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/redis/describedbinstances) API to query basic information about all Redis instances in the target region, including their instance IDs.<br> |
|VpcId |String |Yes |vpc\-1g15j0fvgmt4w8ibuxwjl1111 |Set the instance's Virtual Private Cloud ID.<br><br>> **tip**<br><br><br><br>* > If you enter the ID of the Virtual Private Cloud that the instance currently belongs to, it means you are not modifying the Virtual Private Cloud, but only the subnet.<br><br><br>* > We recommend that you connect Redis instances to ECS instances in the same VPC. Otherwise, they cannot achieve optimal communication performance. You can call the [CreateVpc](https://docs.byteplus.com/en/docs/vpc/CreateVpc) API to create a Virtual Private Cloud.<br><br><br>* > You can call the [DescribeVpcs](https://docs.byteplus.com/en/docs/vpc/DescribeVpcs) API to query Virtual Private Cloud information that matches specified conditions, including the Virtual Private Cloud ID.<br> |
|SubnetId |String |Yes |subnet\-1g15t8rj4uigw8ibuxxij1111 |Set the instance's subnet ID.<br><br>> **tip**<br><br><br><br>* > Subnets have availability zone attributes. You must select a subnet in the target Virtual Private Cloud that belongs to the same availability zone as the instance.<br><br><br>* > A subnet is an IP address block within a Virtual Private Cloud. All cloud resources in the Virtual Private Cloud must be deployed within a subnet. The subnet allocates private IP addresses to cloud resources. You can call the [CreateSubnet](https://docs.byteplus.com/en/docs/vpc/CreateSubnet) API to create a subnet.<br><br><br>* > You can call the [DescribeSubnets](https://docs.byteplus.com/en/docs/vpc/DescribeSubnets) API to query information about all subnets in a specified availability zone, including their subnet IDs.<br> |
|RetentionDays |Integer |No |0 |Set the release time for the old IP address. Valid values:<br><br><br>* `0`: Immediate release.<br><br>* `1` (default): Release after 1 day.<br><br>* `2`: Release after 2 days.<br><br>* `3`: Release after 3 days.<br><br>* `7`: Release after 7 days.<br><br><br>> **tip**<br><br><br>> Modifying VPCs and subnets does not change the domain names of VPC addresses or direct addresses. But their corresponding IP addresses will change. It is recommended to clear the client cache promptly before the old IP address is released; otherwise, read/write exceptions may occur. For more details, refer to [Modify VPC or subnet](https://docs.byteplus.com/en/docs/redis/modify-vpc-or-subnet).<br> |
|ClientToken |String |No |WbiAlPqJM6tMoSOYhT\*\*\*\* |To ensure the idempotence of requests and prevent duplicate submission of requests. The client generates the parameter values to ensure the uniqueness among different requests. Values are case\-sensitive, no more than 127 ASCII characters. |

## Response parameters

The current API has no specified response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/redis/response-structure).

## Example

## Request example

```JSON
POST https://redis.cn-beijing.byteplusapi.com.cn/?Action=ModifyDBInstanceSubnet&Version=2020-12-07 HTTP/1.1
Host: redis.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/cn-beijing/Redis/request,SignedHeaders=content-type;host;x-date,Signature=****
{
        "InstanceId": "redis-cn0212gzmh2xs1111",
        "VpcId": "vpc-1g15j0fvgmt4w8ibuxwjl1111",
        "SubnetId": "subnet-1g15t8rj4uigw8ibuxxij1111"
}
```

## Response example

```JSON
{
     "ResponseMetadata": {
          "RequestId": "2022042510294601022524308102C5****",
          "Action": "ModifyDBInstanceSubnet",
          "Version": "2020-12-07",
          "Service": "Redis",
          "Region": "cn-beijing"
     },
     "Result": null
}
```

## Error code

For more information, refer to [Error codes](https://docs.byteplus.com/en/docs/redis/error-code).
