---
title: "CreateInstance"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/CreateInstance"
---

Call the CreateInstance API to create an instance.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

Calling CreateInstance to create an instance returns the Volcengine order ID and instance ID. The instance remains in awaiting payment status. You must confirm the Volcengine order information in your browser for the instance creation to start. The access URL is: `https://console.byteplus.com/finance/order/pay/?preOrderNumbers={OrderID}`. Replace the variable in the URL with the OrderID from the response example. You can call the [CreateInstanceInOneStep](https://docs.byteplus.com/en/docs/cloudsearch/CreateInstanceInOneStep) API to create an instance in one step for convenience.

<span id=".6K-35rGC6K-05piO"></span>
## Request description


* Request method: **POST**

* Request URL:  **/?Action=CreateInstance&Version=2023\-01\-01 HTTP/1.1**


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the unique request parameters of this API and some common parameters are listed below. For more information, see [Public parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|M9vj9j">必选</span> `Example value: CreateInstance`

Operation to execute: CreateInstance.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|FT7RVY">必选</span> `Example value: 2023-01-01`

API version, value: 2023\-01\-01.



**Tags ** <span data-label="purple">object[] </span>`optional` `example: [{\"Key\": \"key1\", \"Value\": \"value1\"}]`

List of associated tags.


**Key ** <span data-label="purple">string </span><span data-api-tag="require|YyNAvS">必选</span> `Example value: test-tag`

Tag key.



**Value ** <span data-label="purple">string </span><span data-api-tag="require|PLvnGp">必选</span> `Example: test-value`

Tag value.




**ClientToken ** <span data-label="purple">string </span>`optional` `example: 123e4567-e89b-12d3-a456-426655440000`

Idempotent identifier to prevent duplicate operations during retries.



**InstanceConfiguration ** <span data-label="purple">object </span><span data-api-tag="require|tI6WQq">必选</span> `Example value: --`

Instance configuration details.


**VPC ** <span data-label="purple">object</span><span data-api-tag="require|SLxI0V">必选</span>

Configure the private network VPC information of the instance.


**VpcId ** <span data-label="purple">string </span><span data-api-tag="require|V0heXs">必选</span> `Example: vpc-274uhjap8u72****`

VPC ID.



**VpcName ** <span data-label="purple">string </span><span data-api-tag="require|2eU1LC">必选</span> `Example: vpc_nameA`

VPC name.




**Period ** <span data-label="purple">integer </span>`optional` `Example value: 1`

Set the purchase duration for subscription instances, in months.



**Subnet ** <span data-label="purple">object</span><span data-api-tag="require|1ZA10x">必选</span>

Set the subnet information of the instance.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The subnet must be in the main availability zone.</div>



**SubnetId ** <span data-label="purple">string </span><span data-api-tag="require|a88USS">必选</span> `Example: subnet-1323sdda****`

Subnet ID.



**SubnetName ** <span data-label="purple">string </span><span data-api-tag="require|1mVK5c">必选</span> `Example value: subnet_nameA`

Subnet name.




**ZoneId ** <span data-label="purple">string </span><span data-api-tag="require|Dr7rOX">必选</span> `Example value: cn-beijing-a`

The availability zone where the instance is located.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If deploying across multiple availability zones, enter multiple ZoneIds separated by commas, such as <code>cn-beijing-a,cn-beijing-c</code>. The leftmost <code>ZoneId</code> is the main availability zone; the others are backup availability zones.</div>




**Version ** <span data-label="purple">string </span><span data-api-tag="require|d9kvgv">必选</span> `example: V7_10`

Instance version


* When creating an Elasticsearch instance, supported versions include `V6_7`, `V6_8`, and `V7_10`.

* When creating an OpenSearch instance, the supported version is `OPEN_SEARCH_2_9`.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Not recommended to create Elasticsearch 8.18 version instances via OpenAPI or SDK. For creation, <a href="https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000255">submit a ticket</a> for consultation.</div>




**RegionId ** <span data-label="purple">string </span><span data-api-tag="require|e45LQh">必选</span> `Example value: cn-beijing`

Region where the instance is located.



**ChargeType ** <span data-label="purple">string </span><span data-api-tag="require|7WeBX6">必选</span> `Example: PostPaid`

Instance billing type.


* PostPaid: Pay\-as\-you\-go.

* PrePaid: Subscription.



**EnableHttps ** <span data-label="purple">boolean </span><span data-api-tag="require|8o4NKT">必选</span> `Example: true`

Whether to enable the HTTPS access protocol.


* true: enable HTTPS access.

* false: do not enable HTTPS, use HTTP access.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">If you choose HTTP access, it allows access without security authentication and transmits data in plain HTTP. You need to ensure the security of the access environment and avoid exposing the access interface to the public network environment.</div>


* <div data-tips="true" data-tips-type="tip">After creating the instance, you can modify the transport protocol based on business needs. For related documentation, see <a href="https://docs.byteplus.com/en/docs/cloudsearch/changing-transfer-protocol">Changing the transfer protocol of an instance</a>.</div>




**ProjectName ** <span data-label="purple">String </span>`Optional` `Example: default`

Set the project for the cloud search instance as needed to facilitate resource grouping management.

A project is a resource management method provided by Volcengine that helps maintain resource isolation and data security. You can view resource usage bills by project for easier cost calculation of cloud resources.



**InstanceName ** <span data-label="purple">string </span><span data-api-tag="require|gAjfm7">必选</span> `Example: doc-test`

Set the instance name.


* Can only include Chinese characters, letters, numbers, hyphens (\-), and underscores (_). It cannot start or end with numbers or hyphens (\-).

* Length must be between 1 and 128 characters.



**EnablePureMaster ** <span data-label="purple">boolean </span>`optional` `Example value: true`

Whether the master node is independent.


* true: The master node is independent.

* false: The Master node overlaps with the Data node, i.e., Hot declaration is used.



**NodeSpecsAssigns ** <span data-label="purple">object[]</span><span data-api-tag="require|bgAzeN">必选</span>

Quantity and specification configuration of various nodes in the instance.


**Type ** <span data-label="purple">string </span>`Optional` `Example: Hot`

Node type. Please understand the function of the node types first, then decide whether to create them based on your business needs. For details, see [product specifications](https://docs.byteplus.com/en/docs/cloudsearch/specifications).


* Master: master node.

* Hot: Data node.

* Cold: cold data node.

* Warm: warm data node.

* Kibana: Kibana node.

* Coordinator: coordinating node.



**Number ** <span data-label="purple">integer </span>`optional` `example: 2`

Number of nodes.


* When configuring the number of data nodes, note the following based on deployment methods:

   * Single availability zone deployment: it is recommended to configure at least 3 data nodes for production environments. Configuring 2 nodes carries a risk of split brain. If a dedicated master node is enabled, 2 data nodes will not cause split brain.

   * Dual availability zone deployment with dedicated master node enabled by default: for production environments, configure at least 4 data nodes, two per availability zone.

   * Three availability zone deployment with dedicated master node enabled by default: for production environments, configure at least 6 data nodes, two per availability zone.

   * The number of data nodes can be set from 1 to 100; if more data nodes are needed, you can request an increase to 200.

* Configure the master node: if dedicated master nodes are not enabled, the master node has the same configuration as the data node; otherwise, the master configuration is independent.

* Configure dedicated master nodes; the default quantity is 3 if enabled.

* Configure the Kibana node; the quantity is fixed at 1.

* Configure coordinating nodes; if enabled, at least 2 are recommended for production environments, with a range from 2 to 50.

* Warm data nodes: if enabled, at least 3 are recommended for production environments, with a maximum of 100.

* Cold data nodes: if enabled, at least 2 are recommended for production environments, with a maximum of 100.



**StorageSize ** <span data-label="purple">integer </span>`optional` `Example: 100`

Storage capacity, measured in GiB.

The default value is 100 GiB, adjustable in increments of 10 GiB.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Set the StorageSize of the Kibana node to 0, i.e., "StorageSize": 0.</div>


* <div data-tips="true" data-tips-type="tip">The default StorageSize for dedicated master nodes and coordinating nodes is 20.</div>




**StorageSpecName ** <span data-label="purple">string </span>`optional` `example: es.volume.essd.pl0`

Storage specifications name, currently supported specifications are as follows:


* es.volume.essd.pl0: standard version \- high\-performance cloud volumes \- pl0.

* es.volume.essd.flexpl\-standard: standard version \- high\-performance cloud volumes \- flexpl.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Set StorageSpecName of the Kibana node to empty, i.e., "StorageSpecName": "".</div>


For details, refer to the [product specifications](https://docs.byteplus.com/en/docs/cloudsearch/specifications).



**ResourceSpecName ** <span data-label="purple">string </span>`optional` `example value: es.x4.medium`

Name of the computing resource specification. You can get the list of available node specifications by calling the [DescribeNodeAvailableSpecs](https://docs.byteplus.com/en/docs/cloudsearch/DescribeNodeAvailableSpecs) API.

For details, see [product specifications](https://docs.byteplus.com/en/docs/cloudsearch/specifications).



**ExtraPerformance ** <span data-label="purple">object </span>`Optional`

Disk extra performance package configuration.


**Throughput ** <span data-label="purple">integer </span><span data-api-tag="require|2ODN9a">必选</span> `example value: 100`

When your data node uses the FlexPL storage type and storage specifications are set to 500 GiB or above, you can purchase a bandwidth package to increase disk bandwidth.

Unit is MiB, with adjustment steps of 10 MiB.

The currently supported storage specifications and their corresponding maximum extra performance package throughput are as follows:


* es.volume.essd.flexpl\-standard: 650





**ConfigurationCode ** <span data-label="purple">string </span>`optional` `Example value: es.standard`

Billing configuration code, which can be obtained by calling the [DescribeNodeAvailableSpecs](https://docs.byteplus.com/en/docs/cloudsearch/DescribeNodeAvailableSpecs) interface.



**DeletionProtection ** <span data-label="purple">boolean </span>`optional` `Example value: true`

Enable instance deletion protection with the following value selection description:


* true: enable instance deletion protection.

* false: turn off instance deletion protection.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">After enabling instance deletion protection, you cannot delete the instance through the console or API.</div>




**NetworkSpecs ** <span data-label="purple">object[] </span>`optional`

Instance public network specification configuration.


**Type ** <span data-label="purple">string </span><span data-api-tag="require|ZTY6pu">必选</span> `Example value: Elasticsearch`

Public network application type.


* Elasticsearch: Elasticsearch instance usage.

* Kibana: Dashboard usage.



**Bandwidth ** <span data-label="purple">integer </span><span data-api-tag="require|zB8S3i">必选</span> `Example value: 1`

The public network IP bandwidth limit, default is `1`, unit: Mbps.



**IsOpen ** <span data-label="purple">boolean </span><span data-api-tag="require|S7UA7P">必选</span> `Example value: true`

turn on/off.



**SpecName ** <span data-label="purple">string </span><span data-api-tag="require|N26EjK">必选</span> `Example: es.eip.bgp_fixed_bandwidth`

The instance public network resource specification name. See [product specifications](https://docs.byteplus.com/en/docs/cloudsearch/specifications).




**AdminPassword ** <span data-label="purple">string </span><span data-api-tag="require|dVy1P4">必选</span> `example value: Password**`

Administrator password.



**AutoRenew ** <span data-label="purple">boolean </span>`optional` `Example value: true`

Whether subscription instances are set to automatic renewal, default is true.


* true: automatic renewal. The system will automatically renew the instance before each expiration.

* false: automatic renewal is disabled. Manual renewal is required before the instance expires.

   For more information, see [instance renewal](https://docs.byteplus.com/en/docs/cloudsearch/renewal).




&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters unique to this API are listed below. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**OrderID ** <span data-label="purple">string </span>`Example value: BO729***08233255`

Order ID.



**OrderNO ** <span data-label="purple">string </span>`Example: BO729***08233255`

Order number.



**InstanceId ** <span data-label="purple">string </span>`Example: o-00***o718`

Instance ID.



**TradeEnabled ** <span data-label="purple">boolean </span>`Example: true`

Whether the instance created by the current request is billed.


* true: billed.

* false: unbilled.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```json
POST /?Action=CreateInstance&Version=2023-01-01
Host: escloud.cn-beijing.byteplusapi.com.cn
Content-Type: application/json
X-Date: 20231003T104027Z
Authorization: HMAC-SHA256 
Credential=AKLTMjI2ODVlYzI3ZGY1NGU4ZjhjYWRjMTlmNTM5OTZ****/20231003/cn-beijing/ESCloud/request, SignedHeaders=content-type;host;x-date, Signature=88dd0a9ea555d8609ec83eb46054b52f6cd4f79b8d5094fa784c66fa3f2b****
{
    "InstanceConfiguration": {
        "InstanceName": "doc-test-1",
        "RegionId": "cn-beijing",
        "ZoneId": "cn-beijing-a",
        "Version": "V7_10",
        "NodeSpecsAssigns": [
    {
      "Type": "Kibana",
      "Number": 1,
      "ResourceSpecName": "kibana.x2.small",
      "StorageSpecName": "",
      "StorageSize": 0
    },
    {
      "Type": "Master",
      "Number": 3,
      "ResourceSpecName": "es.x2.medium",
      "StorageSpecName": "es.volume.essd.pl0",
      "StorageSize": 20
    },
    {
      "Type": "Coordinator",
      "Number": 2,
      "ResourceSpecName": "es.x2.medium",
      "StorageSpecName": "es.volume.essd.pl0",
      "StorageSize": 20
    },
    {
      "Type": "Hot",
      "Number": 3,
      "ResourceSpecName": "es.x2.medium",
      "StorageSpecName": "es.volume.essd.pl0",
      "StorageSize": 20
    },
    {
      "Type": "Warm",
      "Number": 3,
      "ResourceSpecName": "es.x2.medium",
      "StorageSpecName": "es.volume.essd.pl0",
      "StorageSize": 100
    }
  ],
        "EnablePureMaster": true,
        "VPC": {
                "VpcId": "vpc-13fsc****3n6nu46g3mus",
                "VpcName": "wuch_vpc0110"
            },
        "Subnet": {
                "SubnetId": "subnet-rrzpa****7r53lac",
                "SubnetName": "wuch_A_sub"
            },
        "AdminUserName": "admin",
        "AdminPassword": "qaP****456",
        "EnableHttps": true,
        "DeletionProtection": true,
        "ConfigurationCode": "es.standard",
        "ChargeType": "PostPaid"
    }
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```json
{
    "ResponseMetadata": {
        "Action": "CreateInstance",
        "Region": "cn-beijing",
        "RequestId": "2023060411042001001002322***",
        "Service": "ESCloud",
        "Version": "2023-01-01"
    },
    "Result": {
        "OrderNO": "BO729***08233255",
        "OrderID": "BO729***08233255",
        "TradeEnabled": true,
        "InstanceId": "o-00***o718"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The following table lists error codes related to this API and business logic. For more information, see [Public error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|200 |IllegalParameter |illegal parameter |Invalid parameter. The reason may be a missing parameter or noncompliance with API requirements. |
|200 |InternalServerError |Internal server exception |The service exited due to an exception and cannot complete the interface request operation. |
|200 |Unauthorized |unauthorized error |User lacks permission to call the interface. |
