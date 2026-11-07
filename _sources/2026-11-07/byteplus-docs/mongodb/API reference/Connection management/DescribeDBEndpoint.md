---
title: "DescribeDBEndpoint"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/describedbendpoint"
---

Call the DescribeDBEndpoint API to query the address information under the target instance.

## Request type

Synchronous request.

## Precautions

When the DescribeDBEndpoint API is called to query the address information of an instance, the domain name and IP address information of the address will be returned. However, we do not recommend connecting to instances via the `IP:port` method, as the IP address will change after the subnet is switched, and the client will fail to connect to the instance if its code is not updated in time.

We recommend you access MongoDB instances via the `domain:port` method, so as to avoid the problem where the instance fails to connect due to IP address changes. For the specific steps for connecting to a MongoDB instance, refer to [Connecting to instance via Mongo Shell tool](https://docs.byteplus.com/en/docs/mongodb/connect-instance-via-mongo-shell).

## Request parameters

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |mongo\-replica\-617a883d5\*\*\*\* |Instance ID.<br><br>tip<br><br>You can call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/mongodb/describedbinstances) API to query the basic information about all the MongoDB instances in the target region, including the instance IDs. |

## Response parameters

|Name |Type |Example |Description |
|---|---|---|---|
|DBEndpoints |Object[] | |A list of address information. |
|DBAddresses |Object[] | |A list of address string information. |
|AddressDomain |String |mongoreplicae405f8e2c\*\*\*\*.mongodb.ibytepluses.com |The domain name of the address. |
|AddressIP |String |100.64.\*\*\*.\*\*\* |The IP corresponding to the address.<br><br>tip<br><br>We do not recommend connecting to instances via the `IP:port` method, as the IP address will change after the subnet is switched, and the client will fail to connect to the instance if its code is not updated in time. We recommend you access MongoDB instances via the `domain:port` method, so as to avoid the problem where the instance fails to connect due to IP address changes. For the specific steps for connecting to a MongoDB instance, refer to [Connecting to instance via Mongo Shell tool](https://docs.byteplus.com/en/docs/mongodb/connect-instance-via-mongo-shell). |
|AddressPort |String |3717 |The port number of the address. |
|AddressType |String |Primary |The address type of the node, with the following range of values:<br><br><br>* `Primary`： Address of primary node.<br><br>* `Secondary`： Address of secondary node.<br><br>* `Hidden`： Address of hidden node.<br><br><br>tip<br><br>The address information of the hidden nodes will be returned only when the address is a private address (i.e., the `NetworkType` value is `Private`). |
|EipId |String |eip\-2fef2qcfbfw8w5oxruw3w\*\*\*\*\*\* |The EIP ID to which the public address of the instance is bound.<br><br>tip<br><br>This parameter will be returned only when the address is a public address (i.e., the `NetworkType` value is `Public`). |
|NodeId |String |mongo\-shard\-9a554522\*\*\*\*\-1 |The node ID to which the address belongs. |
|EndpointId |String |Ak5BUhxJAkgSVR\*\*\*\* |Address ID. |
|EndpointStr |String |mongodb://:@mongoreplicae405f8e2c\*\*\*\*.mongodb.ibytepluses.com:3717,mongoreplicae405f8e2c\*\*\*\*.mongodb.ibytepluses.com:3717/?authSource=admin&replicaSet=rs\-mongo\-replica\-e405f8e2\*\*\*\*&retryWrites=true |String information for the address. |
|EndpointType |String |RelicaSet |The node type corresponding to the address. The value range is as follows:<br><br><br>* Replica set instances only support the `ReplicaSet` (i.e., Replica Set) address type.<br><br>* Sharding cluster instances support three address types: `Mongos` (Mongos nodes), `ConfigServer` (ConfigServer nodes), and `Shard` (Shard nodes). |
|NetworkType |String |Private |The network type of the address, with the following range of values:<br><br><br>* `Private`： Private address.<br><br>* `Public`： Public address. |
|ObjectId |String |mongo\-shard\-cd807041\*\*\*\* |The ID of the component to which the current address belongs. |
|SubnetId |String |subnet\-3rfc6bfv8lssg5zsk2h7z\*\*\*\*\*\* |The subnet ID to which the current instance belongs. |
|VpcId |String |vpc\-3tjjjskc6p4d2et2\*\*\*\*\*\* |The VPC ID to which the current instance belongs.<br><br>tip<br><br>This parameter will be returned only when the value of `EndpointType` is `Mongos`, `ConfigServer`, or `Shard`. |

## Sample request 1

Query the details of the connection address of the replica set instance.

```json
POST https://mongodb.ap-southeast-1.byteplusapi.com/?Action=DescribeDBEndpoint&Version=2022-01-01 HTTP/1.1
Host: mongodb.ap-southeast-1.byteplusapi.com
Content-Type: application/json; charset=utf-8
X-Date: 20201103T104027Z
Authorization: HMAC-SHA256 Credential=AK****/20201103/ap-southeast-1/mongodb/request,SignedHeaders=content-type;host;x-date,Signature=****
{
    "InstanceId": "mongo-replica-617a883d5****"
}
```

## Sample response 1

The return result of the replica set instance.

The following example only shows the connection address information of some nodes in the instance. The specific returned data shall be subject to the actual return result of the API call.

```json
{
    "ResponseMetadata": {
        "RequestId": "202205281742120102250821990282****",
        "Action": "DescribeDBEndpoint",
        "Version": "2022-01-01",
        "Service": "MongoDB",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "DBEndpoints": [
            {
                "DBAddress types": [
                    {
                        "AddressDomain": "mongoreplica617a883d5****.mongodb.ibytepluses.com",
                        "AddressIP": "192.168.***.***",
                        "AddressPort": "3717",
                        "AddressType": "Primary",
                        "EipId": "",
                        "NodeId": "mongo-replica-617a883d5****-0"
                    },
                    {
                        "AddressDomain": "mongoreplica617a883d5****.mongodb.ibytepluses.com",
                        "AddressIP": "192.168.***.***",
                        "AddressPort": "3717",
                        "AddressType": "Secondary",
                        "EipId": "",
                        "NodeId": "mongo-replica-617a883d5****-1"
                    },
                    {
                        "AddressDomain": "mongoreplica617a883d5****2.mongodb.ibytepluses.com",
                        "AddressIP": "192.168.***.***",
                        "AddressPort": "3717",
                        "AddressType": "Hidden",
                        "EipId": "",
                        "NodeId": "mongo-replica-617a883d5****-2"
                    }
                ],
                "EndpointId": "UUtGBkJJVB5EBE****",
                "EndpointStr": "mongodb://<user>:<password>@mongoreplica617a883d5****.mongodb.ibytepluses.com:3717,mongoreplica617a883d5****.mongodb.ibytepluses.com:3717/?authSource=admin&replicaSet=rs-mongo-replica-617a883d5****&retryWrites=true",
                "EndpointType": "ReplicaSet",
                "NetworkType": "Private",
                "SubnetId": "subnet-3rfc6bfv8lssg5zsk2h7z****",
                "VpcId": "vpc-2bzrc4aszyg3k2dx0eeic****"
            },
            {
                "DBAddress types": [
                    {
                        "AddressDomain": "mongoreplica617a883d5****.mongodb.bytepluses.com",
                        "AddressIP": "10.249.***.***",
                        "AddressPort": "3717",
                        "AddressType": "Primary",
                        "EipId": "eip-2d744t595x6o058ozfeht****",
                        "NodeId": "mongo-replica-617a883d5****-0"
                    },
                    {
                        "AddressDomain": "mongoreplica617a883d5****.mongodb.bytepluses.com",
                        "AddressIP": "10.249.***.***",
                        "AddressPort": "3717",
                        "AddressType": "Secondary",
                        "EipId": "eip-2d6v5hyyvu4g058ozfeai****",
                        "NodeId": "mongo-replica-617a883d5****-1"
                    }
                ],
                "EndpointId": "UUtGBkJJVB5EBE****",
                "EndpointStr": "mongodb://<user>:<password>@mongoreplica617a883d5****.mongodb.bytepluses.com:3717,mongoreplica617a883d5****.mongodb.bytepluses.com:3717/?authSource=admin&replicaSet=rs-mongo-replica-617a883d5****&retryWrites=true",
                "EndpointType": "ReplicaSet",
                "NetworkType": "Public",
                "SubnetId": "subnet-3rfc6bfv8lssg5zsk2h7z****",
                "VpcId": "vpc-2bzrc4aszyg3k2dx0eeic****"
            }
        ]
    }
}
```

## Sample request 2

Query the details of the connection address of the sharding cluster instance.

```json
POST https://mongodb.ap-southeast-1.byteplusapi.com/?Action=DescribeDBEndpoint&Version=2022-01-01 HTTP/1.1
Host: mongodb.ap-southeast-1.byteplusapi.com
Authorization: HMAC-SHA256 Credential=AKLTOGJhY2E1NTdkZGFmNDg0Yjk0ZDFiNjE5Y2NjZjI****/20230907/ap-southeast-1/mongodb/request, SignedHeaders=host;x-date;x-content-sha256;content-type, Signature=7f1119a75111535b1d6e7929700f22e1474af0fb4fe26c59f5ac5cdba0cc****
Content-Type: application/json; charset=utf-8
X-Content-Sha256: 567112abe45bd6a09504fd244237f14c0ba120491da0d35097afd54d87bd****
X-Date: 20230907T124910Z
{
    "InstanceId": "mongo-shard-bb7108c2****"
}
```

## Sample response 2

The return result of the sharding cluster instance.

The following example only shows the connection address information of some nodes in the instance. The specific returned data shall be subject to the actual return result of the API call.

```json
{
    "ResponseMetadata": {
        "RequestId": "202205281742120102250821990282****",
        "Action": "DescribeDBEndpoint",
        "Version": "2022-01-01",
        "Service": "MongoDB",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "DBEndpoints": [
            {
                "DBAddresses": [
                    {
                        "AddressDomain": "mongoshardbb7108c2****0.mongodb.ibytepluses.com",
                        "AddressIP": "192.168.***.***",
                        "AddressPort": "3717",
                        "AddressType": "Primary",
                        "EipId": "",
                        "NodeId": "mongo-shard-bb7108c2****-0"
                    }
                ],
                "EndpointId": "BRhGVkpJBEhEBB****",
                "EndpointStr": "mongodb://<user>:<password>@mongoshardbb7108c2****0.mongodb.ibytepluses.com:3717,mongoshardbb7108c2****1.mongodb.ibytepluses.com:3717/?authSource=admin&retryWrites=true",
                "EndpointType": "Mongos",
                "NetworkType": "Private",
                "ObjectId": "mongo-shard-bb7108c2****",
                "SubnetId": "subnet-22ixzr4pcvnk07r2qr0o0****",
                "VpcId": "vpc-22ixzq18qmk1s7r2qr0mr****"
            },
            {
                "DBAddresses": [
                    {
                        "AddressDomain": "mongoshardbb7108c2****0.mongodb.bytepluses.com",
                        "AddressIP": "14.103.***.***",
                        "AddressPort": "3717",
                        "AddressType": "Primary",
                        "EipId": "eip-5go9gekhuigw73inqlts****",
                        "NodeId": "mongo-shard-bb7108c2****-0"
                    }
                ],
                "EndpointId": "BRhGVkpJBEhEBB****",
                "EndpointStr": "mongodb://<user>:<password>@mongoshardbb7108c2****0.mongodb.bytepluses.com:3717/?authSource=admin&retryWrites=true",
                "EndpointType": "Mongos",
                "NetworkType": "Public",
                "ObjectId": "mongo-shard-bb7108c2****",
                "SubnetId": "subnet-22ixzr4pcvnk07r2qr0o0****",
                "VpcId": "vpc-22ixzq18qmk1s7r2qr0mr****"
            }
        ]
    }
}
```

## Error codes

For more information, refer to [Error codes](https://docs.byteplus.com/en/docs/mongodb/error-code).
