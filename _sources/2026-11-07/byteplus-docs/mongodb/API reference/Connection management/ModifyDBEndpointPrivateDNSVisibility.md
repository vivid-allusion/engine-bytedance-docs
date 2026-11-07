---
title: "ModifyDBEndpointPrivateDNSVisibility"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/modifydbendpointprivatednsvisibility"
---

Call the ModifyDBEndpointPrivateDNSVisibility interface to enable or disable the public network resolution function for the target MongoDB instance.

## Request type

Asynchronous request.

## Precautions

* The complex Internet cannot ensure the accuracy and timeliness of domain name resolution. Therefore, Public Network Resolution is available only for non\-production environments. We recommend using DNS Forward in a production environment, where you configure Forward in local Domain Name System (DNS) servers to the BytePlus DNS servers. `100.96.0.2` and `100.96.0.3` are the IP addresses of the DNS servers used by BytePlus to implement domain name resolution in a private network.

* After enabling Public Network Resolution for sharding cluster instances, if you add Mongos nodes, you need to disable and then enable Public Network Resolution after instance specification modification is completed. Otherwise, the private domain names corresponding to the new Mongos nodes cannot be resolved to private addresses. For more details, refer to [Enabling or disabling public network resolution](https://docs.byteplus.com/en/docs/mongodb/set-public-network-resolution).

* Only the private addresses of the following instances or nodes support the function of enabling or disabling public network resolution:

   * The private address of the replica set instance.

   * The private address of the Mongos node in the sharding cluster.

## Request parameters

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|InstanceId |String |Yes |mongo\-replica\-e405f8e2\*\*\*\* |Instance ID.<br><br>tip<br><br>You can call the [DescribeDBInstances](https://docs.byteplus.com/en/docs/mongodb/describedbinstances) interface to query the basic information of all MongoDB instances in the target Region, including instance ID. |
|PrivateDNSVisibility |Boolean |Yes |true |Enable or disable the public network resolution function of the instance. The value range is as follows:<br><br><br>* `true`: Enable public network resolution.<br><br>* `false`: Disable public network resolution. |

## Response parameters

The current API has no specified response parameters. For more information, refer to [Response structure](https://docs.byteplus.com/en/docs/mongodb/response-structure).

## Sample request

```json
POST https://mongodb.ap-southeast-1.byteplusapi.com/?Action=ModifyDBEndpointPrivateDNSVisibility&Version=2022-01-01 HTTP/1.1
Host: mongodb.ap-southeast-1.byteplusapi.com
Authorization: HMAC-SHA256 Credential=AKLTOGJhY2E1NTdkZGFmNDg0Yjk0ZDFiNjE5Y2NjZjI****/20230907/ap-southeast-1/mongodb/request, SignedHeaders=host;x-date;x-content-sha256;content-type, Signature=7f1119a75111535b1d6e7929700f22e1474af0fb4fe26c59f5ac5cdba0cc****
Content-Type: application/json; charset=utf-8
X-Content-Sha256: 567112abe45bd6a09504fd244237f14c0ba120491da0d35097afd54d87bd****
X-Date: 20230907T124910Z
{
    "InstanceId": "mongo-replica-e405f8e2****",
    "PrivateDNSVisibility": true
}
```

## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420100232280022D31****",
        "Action": "ModifyDBEndpointPrivateDNSVisibility",
        "Version": "2022-01-01",
        "Service": "mongodb",
        "Region": "ap-southeast-1"
    },
    "Result": null
}
```

## Error codes

For more information, refer to [Error codes](https://docs.byteplus.com/en/docs/mongodb/error-code).
