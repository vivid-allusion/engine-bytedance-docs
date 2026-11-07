---
title: "CreateInstanceInOneStep"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/CreateInstanceInOneStep"
---

Call the CreateInstanceInOneStep API to create an instance directly in one step, supporting the creation of Elasticsearch instances and OpenSearch instances.

<span id=".6K-35rGC6K-05piO"></span>
## Request description


* Request method: **POST**

* Request URL:  **/?Action=CreateInstanceInOneStep&Version=2023\-01\-01 HTTP/1.1**


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the unique request parameters of this API and some common parameters are listed below. For more information, see [Public parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|j9iVu8">必选</span> `example value: CreateInstanceInOneStep`

The action to execute, value: CreateInstanceInOneStep.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|FKpjIT">必选</span> `Example value: 2023-01-01`

API version, value: 2023\-01\-01.



**Tags ** <span data-label="purple">object[] </span>`optional` `example: [{\"Key\": \"key1\", \"Value\": \"value1\"}]`

List of associated tags.


**Key ** <span data-label="purple">string </span><span data-api-tag="require|ZhefCr">必选</span>`Example value: KeyA`

Tag key.



**Value ** <span data-label="purple">string </span><span data-api-tag="require|ICAsYC">必选</span> `example value: ValueA`

Tag value.




**ClientToken ** <span data-label="purple">string </span>`optional` `example value: 123e4567-e89b-12d3-a456-426655440000`

Idempotent identifier to prevent duplicate operations during retries.



**InstanceConfiguration ** <span data-label="purple">object </span><span data-api-tag="require|vl46Ql">必选</span> `example value: --`

Instance configuration details.


**VPC ** <span data-label="purple">object</span><span data-api-tag="require|edO8Zy">必选</span>

Configure the private network VPC information of the instance.


**VpcId ** <span data-label="purple">string </span><span data-api-tag="require|rWUBeQ">必选</span> `Example: vpc-274uhjap8u72****`

VPC ID.



**VpcName ** <span data-label="purple">string </span><span data-api-tag="require|2oSIPv">必选</span> `example value: vpc_nameA`

VPC name.




**Period ** <span data-label="purple">integer </span>`optional` `example value: 1`

Set the purchase duration for subscription instances in months.



**Subnet ** <span data-label="purple">object</span><span data-api-tag="require|RFoSlA">必选</span>

Set the subnet information of the instance.


**SubnetId ** <span data-label="purple">string </span><span data-api-tag="require|IrWKZm">必选</span> `Example: subnet-1323sdda****`

Subnet ID.



**SubnetName ** <span data-label="purple">string </span><span data-api-tag="require|m2RjD6">必选</span> `Example value: subnet_nameA`

Subnet name.




**ZoneId ** <span data-label="purple">string </span><span data-api-tag="require|1dalHR">必选</span> `example value: cn-beijing-a`

The availability zone where the instance is located.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|CIyF59">必选</span> `Example: V7_10`

Instance version


* Supported versions when creating an Elasticsearch instance include `V6_7`, `V6_8`, and `V7_10`.

* Supported version `OPEN_SEARCH_2_9` when creating an OpenSearch instance.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Creating Elasticsearch 8.18 instances through OpenAPI or SDK is not recommended. To create one, <a href="https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000255">submit a ticket</a> for consultation.</div>




**RegionId ** <span data-label="purple">string </span><span data-api-tag="require|PVcLfQ">必选</span> `Example: cn-beijing`

Region where the instance is located.



**AutoRenew** <span data-label="purple">boolean</span> `optional` `example value: false`

Whether subscription instances are configured for automatic renewal.


* true: automatic renewal enabled. The system automatically renews the instance before each expiration.

* false: automatic renewal disabled. Manual renewal is required before the instance expires.

   For more information, refer to [Instance Renewal](https://docs.byteplus.com/en/docs/cloudsearch/renewal).



**ChargeType ** <span data-label="purple">string </span><span data-api-tag="require|xcbNDU">必选</span> `example value: PostPaid`

Instance billing type.


* PostPaid: Pay\-as\-you\-go.

* PrePaid: Subscription.



**EnableHttps ** <span data-label="purple">boolean </span><span data-api-tag="require|ERVRZP">必选</span> `example: true`

Whether to enable the HTTPS access protocol.


* true: enable HTTPS access.

* false: do not enable HTTPS, use HTTP access.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">If you choose HTTP access, the connection does not require authentication and transmits data as plain HTTP. You need to ensure the security of the access environment and avoid exposing the access interface to the public network environment.</div>


* <div data-tips="true" data-tips-type="tip">After creating the instance, you can modify the transport protocol based on business needs. For related documentation, see <a href="https://docs.byteplus.com/en/docs/cloudsearch/changing-transfer-protocol">Changing the transfer protocol of an instance</a>.</div>




**ProjectName ** <span data-label="purple">String </span>`Optional` `Example: default`

Set the project for the Cloud Search instance as needed to facilitate grouped management of cloud resources.

A project is a resource management method provided by Volcengine that helps maintain resource isolation and data security. You can view resource usage bills by project for easier cost calculation of cloud resources.



**InstanceName ** <span data-label="purple">string </span><span data-api-tag="require|I4GIRU">必选</span> `Example: doc-test`

Set the instance name.


* Can only include Chinese characters, letters, digits, hyphens (\-), and underscores (_). It cannot start or end with a digit or hyphen (\-).

* Length must be between 1 and 128 characters.



**AdminPassword ** <span data-label="purple">string </span><span data-api-tag="require|Qvofqx">必选</span> `Example: Password**`

Administrator password. Value selection rules:


* The password must include at least three of the following: uppercase letters, lowercase letters, numbers, and special characters, with a length of 8 to 32 characters.

* Supports special characters _#!@$%^&\*()+=\-; spaces and Chinese characters are not allowed.



**EnablePureMaster ** <span data-label="purple">boolean </span>`optional` `example: true`

Whether the master node is independent.


* true: The master node is independent.

* false: The Master node overlaps with the Data node, i.e., Hot declaration is used.



**NodeSpecsAssigns ** <span data-label="purple">object[]</span><span data-api-tag="require|lciemO">必选</span>

Quantity and specification configuration of various nodes in the instance.


**Type ** <span data-label="purple">string </span>`optional` `example: Hot`

Node type. Please understand the role of the node type first, then decide whether to create it based on your business needs. For details, see [product specifications](https://docs.byteplus.com/en/docs/cloudsearch/specifications).


* Master: Master node.

* Hot: Data node.

* Cold: Cold data node.

* Warm: Warm data node.

* Kibana: Kibana node.

* Coordinator: Coordinating node.



**Number ** <span data-label="purple">integer </span>`Optional` `Example: 2`

Number of nodes.


1. When configuring the number of data nodes under different deployment methods, consider the following information:

   * Single availability zone deployment: it is recommended to configure at least 3 data nodes for production environments. Configuring 2 nodes carries a risk of split brain.

   * Dual availability zone deployment with dedicated master node enabled by default: for production environments, configure at least 4 data nodes, two per availability zone.

   * Three availability zone deployment with dedicated master node enabled by default: for production environments, configure at least 6 data nodes, two per availability zone.

   * The number of data nodes can be set from 1 to 100; if more data nodes are needed, you can request an increase to 200.

2. Configure Master nodes the same way as data nodes.

3. Configure dedicated master nodes; if enabled, the default quantity is 3.

4. Configure Kibana nodes; the quantity is fixed at 1.

5. Configure coordinating nodes; if enabled, at least 2 coordinating nodes are recommended for production environments, with a range of 2 to 50.

6. Warm data nodes: if enabled, at least 3 warm data nodes are recommended for production environments, with a maximum of 100.



**StorageSize ** <span data-label="purple">integer </span>`optional` `example value: 100`

Storage capacity, measured in GiB.

The default value is 100 GiB, with step increments of 10 GiB.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Set the StorageSize of the Kibana node to 0, i.e., "StorageSize": 0.</div>




**StorageSpecName ** <span data-label="purple">string </span>`optional` `Example: es.volume.essd.pl0`

Storage specification names. The currently supported specifications are as follows:

es.volume.essd.pl0: standard edition \- high\-performance cloud disk \- pl0.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The StorageSpecName setting for the Kibana node is empty, i.e., "StorageSpecName": "" .</div>


For specification details, refer to [Product Specifications](https://docs.byteplus.com/en/docs/cloudsearch/specifications).



**ResourceSpecName ** <span data-label="purple">string </span>`optional` `example value: es.x4.medium`

Name of the compute resource specification. You can call the [DescribeNodeAvailableSpecs](https://docs.byteplus.com/en/docs/cloudsearch/DescribeNodeAvailableSpecs) API to get the list of available node specifications.

For specification details, refer to [product specifications](https://docs.byteplus.com/en/docs/cloudsearch/specifications).



**ExtraPerformance ** <span data-label="purple">object </span>`optional`

Disk extra performance package configuration.


**Throughput ** <span data-label="purple">integer </span><span data-api-tag="require|jbzq2S">必选</span>`example value: 100`

When the data node uses the FlexPL storage type and the storage specification is set to 500 GiB or above, you can purchase a bandwidth package to increase disk bandwidth.

Unit is MiB, adjustment step is 10 MiB.

Supported storage specifications and their corresponding maximum throughput for additional performance packages are as follows:


* es.volume.essd.flexpl\-standard: 650





**ConfigurationCode ** <span data-label="purple">string </span>`optional` `Example value: es.standard`

Billing configuration code, which can be obtained by calling the [DescribeNodeAvailableSpecs](https://docs.byteplus.com/en/docs/cloudsearch/DescribeNodeAvailableSpecs) API.



**DeletionProtection ** <span data-label="purple">boolean </span>`optional` `example value: true`

Enable instance deletion protection with the following value selection description:


* true: enable instance deletion protection.

* false: turn off instance deletion protection.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">After enabling instance deletion protection, you cannot delete the instance through the console or API.</div>




**NetworkSpecs** <span data-label="purple">object[]</span> `optional`

Instance public network specification configuration.


**Type ** <span data-label="purple">string </span><span data-api-tag="require|G6CnOn">必选</span> `Example value: Elasticsearch`

Public network application type.


* Elasticsearch: for Elasticsearch instance use.

* Kibana: for dashboard use.



**Bandwidth ** <span data-label="purple">integer </span><span data-api-tag="require|TWmadc">必选</span> `example: 1`

Public IP bandwidth limit, default is `1`, unit: Mbps.



**IsOpen ** <span data-label="purple">boolean </span><span data-api-tag="require|Ocpmmz">必选</span> `example value: true`

Enable or disable.



**SpecName ** <span data-label="purple">string </span><span data-api-tag="require|j1Eb2M">必选</span> `Example: es.eip.bgp_fixed_bandwidth`

The public network resource specification name of the instance. See [product specifications](https://docs.byteplus.com/en/docs/cloudsearch/specifications).





&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters unique to this API are listed below. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**Name ** <span data-label="purple">string </span>`Example value: o-008***iu98`

Created instance ID.



**InstanceId ** <span data-label="purple">string </span>`Example value: doc-test`

Instance name.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```text
POST /?Action=CreateInstanceInOneStep&Version=2023-01-01
Host: escloud.cn-beijing.byteplusapi.com.cn
Content-Type: application/json
X-Date: 20231003T104027Z
Authorization: HMAC-SHA256 
Credential=AKLTMjI2ODVlYzI3ZGY1NGU4ZjhjYWRjMTlmNTM5OTZ****/20231003/cn-beijing/ESCloud/request, SignedHeaders=content-type;host;x-date, Signature=88dd0a9ea555d8609ec83eb46054b52f6cd4f79b8d5094fa784c66fa3f2b****
{
        "InstanceConfiguration": {
                "NodeSpecsAssigns": [{
                        "Type": "Kibana",
                        "Number": 1,
                        "ResourceSpecName": "kibana.x2.small",
                        "StorageSpecName": "",
                        "StorageSize": 0
                }, {
                        "Type": "Master",
                        "Number": 3,
                        "ResourceSpecName": "es.x2.medium",
                        "StorageSpecName": "es.volume.essd.pl0",
                        "StorageSize": 20
                }, {
                        "Type": "Hot",
                        "Number": 3,
                        "ResourceSpecName": "es.x2.medium",
                        "StorageSpecName": "es.volume.essd.pl0",
                        "StorageSize": 30
                }, {
                        "Type": "Warm",
                        "Number": 3,
                        "ResourceSpecName": "es.x2.medium",
                        "StorageSpecName": "es.volume.essd.pl0",
                        "StorageSize": 20
                },{
                        "Type": "Coordinator",
                        "Number": 2,
                        "ResourceSpecName": "es.x2.medium",
                        "StorageSpecName": "es.volume.essd.pl0",
                        "StorageSize": 20
                }],
                "InstanceName": "doc-test",
                "Version": "V7_10",
                "RegionId": "cn-beijing",
                "ZoneId": "cn-beijing-b",
                "EnableHttps": true,
                "AdminUserName": "admin",
                "AdminPassword": "qaPwd*****",
                "EnablePureMaster": true,
                "ChargeType": "PostPaid",
                "ConfigurationCode": "es.standard",
                "ProjectName": "default",
                "DeletionProtection": false,
                "VPC": {
                        "VpcId": "vpc-13fs**6g3mus",
                        "VpcName": "wu**_vpc0110"
                },
                "Subnet": {
                        "SubnetId": "subnet-13f****pfdmug",
                        "SubnetName": "wu***_B_sub"
                } 
        }
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```text
{
    "ResponseMetadata": {
        "RequestId": "20240402143235C6321AF36AE68***",
        "Action": "CreateInstanceInOneStep",
        "Version": "2023-01-01",
        "Service": "ESCloud",
        "Region": "cn-beijing"
    },
    "Result": {
        "Name": "doc-test-2",
        "InstanceId": "o-0080w3***"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The following table lists error codes related to this API and business logic. For more information, see [Public error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|200 |Unauthorized |unauthorized error |User lacks permission to call the interface. |
|200 |IllegalParameter |illegal parameter |Invalid parameter. The reason may be a missing parameter or noncompliance with API requirements. |
|200 |InternalServerError |Internal server exception |The service exited due to an exception and cannot complete the interface request operation. |
