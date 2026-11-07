---
title: "DescribeInstances "
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/DescribeInstances"
---

Queries Cloud Search instance list and instance configuration details.

<span id=".6K-35rGC6K-05piO"></span>
## Request description


* Request method: **POST**

* Request URL:  **/?Action=DescribeInstance&Version=2023\-01\-01 HTTP/1.1**


<span id=".6LCD6K-V"></span>
## Request parameters

Only the unique request parameters of this API and some common parameters are listed below. For more information, see [Public parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|zp9fCM">必选</span> `Example: DescribeInstances`

Operation to execute: DescribeInstances.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|9BpNt4">必选</span> `Example: 2023-01-01`

API version, value: 2023\-01\-01.



**ProjectName ** <span data-label="purple">String </span>`Optional` `Example: default`

Enter the project name to filter by the instance's project.



**TagFilter ** <span data-label="purple">Object </span>`Optional` `Example: --`

Filter by instance tags


**Tags ** <span data-label="purple">Object[] </span>`Optional`

Array of tag filters.


**Key ** <span data-label="purple">string </span><span data-api-tag="require|KROfET">必选</span>`Example value: KeyA`

Tag filter key.



**Values ** <span data-label="purple">string[] </span><span data-api-tag="require|MeynyC">必选</span> `Example value: ValueA`

List of tag values.





**Filters ** <span data-label="purple">Object[] </span>`Optional` `Example value: --`

Filter criteria to return the list of instances that meet the requirements.


**Name ** <span data-label="purple">String </span>`Optional` `Example value: InstanceName`

Filter condition name. Supported query conditions are as follows:

InstanceId: Instance ID

InstanceName: Instance name

ZoneId: Availability zone ID

Status: Instance status

Version: Instance version

ChargeType: Billing type



**Values ** <span data-label="purple">String[] </span>`Optional` `Example: doc`

Filter condition values.




**PageSize ** <span data-label="purple">Integer </span>`Optional` `Example: 10`

Number of items displayed per page, default is 10.



**PageNumber ** <span data-label="purple">Integer </span>`Optional` `Example value: 1`

Page number, default is 1.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters unique to this API are listed below. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**Instances ** <span data-label="purple">Object[] </span>`Example value: --`

List and configuration information of instances.


**ESEip ** <span data-label="purple">String </span>`Example: 180.*.*.*`

EIP bound to the instance.



**Status ** <span data-label="purple">String </span>`Example:`Running

Current instance status.



**UserId ** <span data-label="purple">String </span>`Example value:` 210\*\*\*34``

User ID of the instance owner.



**ESEipId ** <span data-label="purple">String </span>`Example value: eip-mij5ztefl98**`

ID of the EIP associated with the instance.



**ClusterId ** <span data-label="purple">String </span>`Example:`16a119e0d\*\*\*41ae2627b0``

ID of the cluster to which the instance belongs.



**KibanaEip ** <span data-label="purple">String </span>`Example: 180.*.*.*`

The EIP associated with Kibana.



**CreateTime ** <span data-label="purple">String </span>`Example: 2024-03-21T10:32:24+08:00`

Instance creation time



**ExpireDate ** <span data-label="purple">string </span>`Example value:` 2023\-11\-11T15:59:59.000+00:00

Expiration time of the subscription instance.



**InstanceId ** <span data-label="purple">String </span>`Example value:` o\-00k\*\*\*o718``

Instance ID.



**MainZoneId ** <span data-label="purple">String </span>`Example: cn-beijing-a`

Main Availability Zone



**TotalNodes ** <span data-label="purple">Integer </span>`Example value:` 12

Total number of instance nodes.



**KibanaEipId ** <span data-label="purple">String </span>`Example value: eip-mij5ztefl98**`

The ID of the EIP associated with Kibana.



**KibanaConfig ** <span data-label="purple">Object </span>`Example: --`

Kibana parameter configuration.


**CookieTTL ** <span data-label="purple">Long </span>`Example value: 3600000`

Cookie duration.



**SessionTTL ** <span data-label="purple">Long </span>`Example value: 3600000`

Session duration.



**KibanaBasePath ** <span data-label="purple">String </span>`Example value:` /kibana/{psm}/{idc}

Kibana configuration item `server.basePath` value.



**RequestTimeout ** <span data-label="purple">Long </span>`Example: 30000`

Request timeout duration, default is 30,000 milliseconds.



**SessionKeepAlive ** <span data-label="purple">Boolean </span>`Example value: true`

Whether to extend the Session validity period, default is `true`.




**ResourceTags ** <span data-label="purple">Object[] </span>`Example value: --`

Tag information of the instance.


**Type ** <span data-label="purple">String </span>`Example value: CUSTOM`

tag type:


* CUSTOM: user\-defined tag.

* SYSTEM: system tag.



**TagKvs ** <span data-label="purple">Object </span>`Example value: user`

Tag key.



**TagKeys ** <span data-label="purple">String[] </span>`Example value: tom`

Tag value.




**SubInstances ** <span data-label="purple">Object[] </span>`Example value: --`

Enterprise\-level SQL analysis instance configuration information.


**SubInstanceStatus ** <span data-label="purple">String </span>`Example value: AVAILABLE`

Instance status.



**SubInstanceId ** <span data-label="purple">String </span>`Example value: k-00g0oh**`

Enterprise\-level SQL analysis instance ID.



**SubInstanceType ** <span data-label="purple">String </span>`Example value: sql`

Instance type.




**TransferInfo ** <span data-label="purple">Object </span>`Example value: --`

Data migration task information.


**ForbidStop ** <span data-label="purple">Boolean</span>

Whether stopping is forbidden.



**TransferStatus ** <span data-label="purple">String </span>`Example value: FINISH`

data migration task status.



**TransferTaskId ** <span data-label="purple">String </span>`Example value: 88dbdf2431b44f36**`

Data migration task ID.



**ReduceSpecConfig ** <span data-label="purple">Object</span>

Resource information.


**ColdNodeNum ** <span data-label="purple">Integer</span> `Example value: 0`.

Number of cold nodes.



**DataNodeNum** <span data-label="purple">Integer</span> `Example value: 3`

Number of data nodes



**WarmNodeNum ** <span data-label="purple">Integer </span>`Example value: 3`

Number of warm nodes.



**MasterNodeNum ** <span data-label="purple">integer </span>`Example value: 3`

Number of master nodes.



**EnablePureMaster ** <span data-label="purple">Boolean </span>`Example value: false`

Whether the master node is independent.


* true: The master node is independent.

* false: The master node overlaps with the data node, declared as Hot.




**TransferProgress ** <span data-label="purple">Double </span>`Example value: 100`

Data migration task progress, percentage scale.




**ChargeEnabled** <span data-label="purple">Boolean</span> `Example value:` true

Whether the instance has billing enabled. Value description: true means billing is enabled. false means billing is not enabled.



**CerebroEnabled ** <span data-label="purple">Boolean </span>`Example value:`true

Whether to turn on cerebro. true: cerebro turned on. false: do not turn on cerebro.



**MaintenanceDay ** <span data-label="purple">String[] </span>`Example values: [\"MONDAY\",\"TUESDAY\",\"WEDNESDAY\",\"THURSDAY\",\"FRIDAY\",\"SATURDAY\",\"SUNDAY\"]`

Maintanable days for the instance.



**MaintenanceTime ** <span data-label="purple">String </span>`Example:`03:00\-06:00

Instance maintenance time window.



**SupportColdNode ** <span data-label="purple">Boolean </span>`Example value: true`

Whether cold nodes are supported



**ESPublicEndpoint ** <span data-label="purple">String </span>`Example value:` https://elasticsearch\-o\-00k\*\*\*o718..escloud.volces.com:9200

Instance public network access address.



**ESPrivateEndpoint ** <span data-label="purple">String</span> `Example value:` https://elasticsearch\-o\-00k\*\*\*o718.escloud.ivolces.com:9200

Instance private network access address.



**DeletionProtection ** <span data-label="purple">Boolean </span>`Example value:`true

Whether deletion protection is enabled for the instance. true: instance deletion protection is enabled

false: instance deletion protection is not enabled

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">After enabling instance deletion protection, you cannot delete the instance through the console or API.</div>




**KibanaPublicDomain ** <span data-label="purple">String </span>`Example value: https://visual-o-00**.escloud.volces.com:5601`

Kibana public network access address.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For historical instances, the access address may start with <code>http(s)://kibana-***</code>.</div>




**CerebroPublicDomain ** <span data-label="purple">String </span>`Example value: https://visual-o-00g**.escloud.volces.com:9000/`

cerebro public network access address.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Cerebro and Kibana share the domain name. If it is a historical instance, the access address may start with <code>http(s)://kibana-***</code>.</div>




**ESPublicIpWhitelist ** <span data-label="purple">String </span>`Example: 182.*.*.*`

Instance public address whitelist.


* Supports single IP address or IP network segment format, such as 192.168.0.1 or 192.168.0.0/24. Separate multiple IP addresses with commas.

* Supports up to 300 IP addresses and network segments.



**KibanaPrivateDomain ** <span data-label="purple">String </span>`Example value: https://visual-o-00**.escloud.ivolces.com:5601`

Kibana private network access address.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If this is a historical instance, the access address might start with <code>http(s)://kibana-***</code>.</div>




**CerebroPrivateDomain ** <span data-label="purple">String </span>`Example:`https://visual\-o\-\*\*.escloud.ivolces.com:5601

Private network access address of Cerebro.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Cerebro and Kibana share the same domain name. If it is a historical instance, the access address may start with <code>http(s)://kibana-***</code>.</div>




**ESPrivateIpWhitelist ** <span data-label="purple">String </span>`Example value: 192.168.1.1,192.168.1.2`

Instance private network address access whitelist.


* Supports single IP addresses or IP ranges, formatted as 192.168.0.1 or 192.168.0.0/24. Separate multiple IP addresses with commas.

* Quantity up to 300 supported for IP addresses and ranges.



**EnableESPublicNetwork ** <span data-label="purple">Boolean </span>`Example: `true

Whether the instance has enabled public network access. true: Public network access is enabled. false: Public network access is not enabled.



**InstanceConfiguration ** <span data-label="purple">Object </span>`Example value: --`

Instance configuration details.


**VPC ** <span data-label="purple">Object </span>`Example value: --`

Configure the private network VPC information of the instance.


**VpcId ** <span data-label="purple">String </span>`Example value:` vpc\-274uhjap8u72\*\*\*\*

VPC ID。



**VpcName ** <span data-label="purple">String </span>`Example: `vpc_nameA

VPC name.




**Subnet ** <span data-label="purple">Object </span>`Example: --`

Set the subnet information of the instance.


**SubnetId ** <span data-label="purple">String </span>`Example value:` subnet\-1323sdda\*\*\*\*

Subnet ID。



**SubnetName ** <span data-label="purple">String </span>`Example value:` subnet_nameA

Subnet name.




**ZoneId ** <span data-label="purple">String </span>`Example value:` cn\-beijing\-a

The availability zone where the instance is located.



**Version ** <span data-label="purple">String </span>`Example: `V7_10

Instance version


* ES instance versions supported include V6_7 and V7_10

* Supported versions for OpenSearch instance OPEN_SEARCH_2_9



**RegionId ** <span data-label="purple">String </span>`Example value:` cn\-beijing

Region where the instance is located.



**ChargeType ** <span data-label="purple">String </span>`Example value:` PostPaid

Instance billing type. PostPaid: Pay\-as\-you\-go. PrePaid: Subscription.



**ZoneNumber ** <span data-label="purple">Integer </span>`Example value: 1`

Number of availability zones for the instance.



**EnableHttps ** <span data-label="purple">Boolean </span>`Example value:` true

Whether to enable the HTTPS access protocol. true: enable HTTPS access. false: do not enable HTTPS, use HTTP access.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If using HTTP access, it allows access without security authentication and transmits data in plain HTTP. You need to ensure the security of the access environment and avoid exposing the access interface to the public network environment.</div>




**ProjectName ** <span data-label="purple">String </span>`Example value:` default

Project to which the instance belongs.

The instance belongs to the default project by default; adjusting the instance's project is supported.



**InstanceName ** <span data-label="purple">String </span>`Example value: doc-test`

Instance name.



**AdminUserName ** <span data-label="purple">String </span>`Example value:` admin

Instance administrator account is fixed as **Admin**.



**HotNodeNumber ** <span data-label="purple">Integer </span>`Example value:` 3

Number of data nodes.



**ColdNodeNumber ** <span data-label="purple">Integer </span>`Example value:` 3

Number of cold data nodes.



**WarmNodeNumber ** <span data-label="purple">Integer </span>`Example value:` 3

Number of warm data nodes.



**EnablePureMaster ** <span data-label="purple">Boolean </span>`Example value:`true

Whether the Master node is standalone. true: The Master node is independent. false: The Master node overlaps with the Data node, i.e., Hot declaration is used.



**KibanaNodeNumber ** <span data-label="purple">Integer </span>`Example:` 1

Number of Kibana nodes.



**MasterNodeNumber ** <span data-label="purple">Integer </span>`Example value:` 3

Number of master nodes.



**HotNodeStorageSpec ** <span data-label="purple">Object </span>`Example value: --`

Storage specification configuration details for the data node.


**Name ** <span data-label="purple">string </span>`Example value:` es.volume.essd.pl0

Storage specifications. The currently supported specifications are as follows:


* es.volume.essd.pl0: standard version \- high\-performance cloud volumes \- pl0.

* es.volume.essd.flexpl\-standard: standard version \- high\-performance cloud volumes \- flexpl.



**Size ** <span data-label="purple">Integer </span>`Example: `20

Configured available disk space size.



**MaxSize ** <span data-label="purple">Integer </span>`Example value:` 10000

Maximum value of storage specifications, unit: GiB.



**MinSize ** <span data-label="purple">Integer </span>`Example value:` 20

Minimum storage specification value, unit: GiB.



**Description ** <span data-label="purple">String </span>`Example value:` Standard version\-high performance volume\-pl0

Description of the storage specification.



**DisplayName ** <span data-label="purple">String </span>`Example:` ESSD\-PL0

Display name of storage specifications.




**ColdNodeStorageSpec ** <span data-label="purple">Object </span>`Example value: --`

Storage specification configuration details for the cold node.


**Name ** <span data-label="purple">String </span>`Example value: es.volume.essd.pl0`

Storage specifications, the current specifications are as follows:

es.volume.essd.pl0: standard edition \- high\-performance cloud disk \- pl0.



**Size ** <span data-label="purple">Integer </span>`Example: 20`

Current storage specification value in GiB.



**MaxSize ** <span data-label="purple">Integer </span>`Example value: 10000`

Maximum value for storage specifications in GiB.



**MinSize ** <span data-label="purple">Integer </span>`Example: 20`

Minimum storage size in GiB.



**Description ** <span data-label="purple">String </span>`Example value: Standard Edition - High-Performance Cloud Volume - pl0`

Description of the storage specifications.



**DisplayName ** <span data-label="purple">String </span>`Example value: ESSD-PL0`

Display name of the storage specifications.




**HotNodeResourceSpec ** <span data-label="purple">Object </span>`Example value: --`

Node specification configuration details for the data node.


**CPU ** <span data-label="purple">Integer </span>`Example value:` 2

CPU resource of the node specification, unit Core.



**Name ** <span data-label="purple">String </span>`Example:` es.x2.medium

Node specification.



**Memory ** <span data-label="purple">Integer </span>`Example value:` 4

Memory capacity of the node specification, in GiB.



**Description ** <span data-label="purple">String </span>`Example value:` Standard version\-2C4G node

Description of the node specification.



**DisplayName ** <span data-label="purple">String </span>`Example value:` 2Core 4GiB

Display name of the node specification.




**WarmNodeStorageSpec ** <span data-label="purple">Object </span>`Example value: --`

Storage specification configuration details for warm nodes.


**Name ** <span data-label="purple">String </span>`Example value: es.volume.essd.pl0`

Storage specifications, the current specifications are as follows:

es.volume.essd.pl0: Standard Edition \- High\-Performance Cloud Disk \- pl0.



**Size ** <span data-label="purple">Integer </span>`Example value: 20`

The current storage specification value, in GiB.



**MaxSize ** <span data-label="purple">Integer </span>`Example value: 10000`

Maximum storage specification in GiB.



**MinSize ** <span data-label="purple">Integer </span>`Example value: 20`

Minimum storage specification, measured in GiB.



**Description ** <span data-label="purple">String </span>`Example value: Standard Edition - High-Performance Cloud Volume - pl0`

Description of the storage specifications.



**DisplayName ** <span data-label="purple">String </span>`Example value: ESSD-PL0`

Display name of the storage specification.




**ColdNodeResourceSpec ** <span data-label="purple">Object </span>`Example value: --`

Details of cold node specification configuration.


**CPU ** <span data-label="purple">Integer </span>`Example value: 2`

CPU resources of the node specification, unit: core (Core).



**Name ** <span data-label="purple">String </span>`Example: es.x2.medium`

Node specification. For information on node specification types and details.



**Memory ** <span data-label="purple">Integer </span>`Example value: 4`

Memory capacity of the node specification, unit GiB.



**Description ** <span data-label="purple">String </span>`Example value: Standard version-2C4G node`

Description of the node specification.



**DisplayName ** <span data-label="purple">String </span>`Example value: 2Core 4GiB`

Display name of the node specification.




**WarmNodeResourceSpec ** <span data-label="purple">Object </span>`Example value: --`

Node specification configuration details for the warm node.


**CPU ** <span data-label="purple">Integer </span>`Example value: 2`

CPU resource of the node specification, measured in cores.



**Name ** <span data-label="purple">String </span>`Example: es.x2.medium`

Node specification. For details on node specification types and information.



**Memory ** <span data-label="purple">Integer </span>`Example: 4`

Memory capacity of the node specification, in GiB.



**Description ** <span data-label="purple">String </span>`Example: Standard version-2C4G node`

Description information of the node specification.



**DisplayName ** <span data-label="purple">String </span>`Example: 2Core 4GiB`

Display name of the node specification




**Number of coordinating nodes** <span data-label="purple">integer</span> `Example value: 3`.

Number of coordinating nodes.



**MasterNodeStorageSpec ** <span data-label="purple">Object </span>`Example: --`

Storage specification configuration details for the master node.


**Name ** <span data-label="purple">String </span>`Example value: es.volume.essd.pl0`

Storage specifications, the current specifications are as follows:

es.volume.essd.pl0: standard edition \- high\-performance cloud disk \- pl0.



**Size ** <span data-label="purple">Integer </span>`Example value: 20`

Current storage specifications value, unit is GiB.



**MaxSize ** <span data-label="purple">Integer </span>`Example value: 10000`

Maximum storage specification in GiB.



**MinSize ** <span data-label="purple">Integer </span>`Example value: 20`

Minimum storage specification, unit GiB.



**Description ** <span data-label="purple">String </span>`Example value: Standard Edition - High-Performance Cloud Volume - pl0`

Description of storage specifications.



**DisplayName ** <span data-label="purple">String </span>`Example value: ESSD-PL0`

Display name of the storage specifications.




**KibanaNodeResourceSpec ** <span data-label="purple">Object </span>`Example: --`

Kibana node specification configuration details.


**CPU ** <span data-label="purple">Integer</span>. `Example value: 2`.

CPU resources of the node specification, unit is cores.



**Name ** <span data-label="purple">String </span>`Example: es.x2.medium`

Node specification. Check node specification types and details.



**Memory ** <span data-label="purple">Integer </span>`Example value: 4`

Memory capacity of the node specification, unit GiB.



**Description ** <span data-label="purple">String </span>`Example value: Standard version-2C4G node`

Description of the node specification.



**DisplayName ** <span data-label="purple">String </span>`Example value: 2Core 4GiB`

Display name of the node specification.




**MasterNodeResourceSpec ** <span data-label="purple">Object </span>`Example value: --`

Configuration details of the Master node specification.


**CPU ** <span data-label="purple">Integer </span>`Example: 2`

CPU resources of the node specification, unit is Core.



**Name ** <span data-label="purple">String </span>`Example value: es.x2.medium`

Node specification. See node specification types and details.



**Memory ** <span data-label="purple">Integer </span>`Example: 4`

Memory capacity of the node specification, in GiB.



**Description ** <span data-label="purple">String </span>`Example value: standard version-2C4G node`

Description of the node specification.



**DisplayName ** <span data-label="purple">String </span>`Example: 2Core 4GiB`

Display name of the node specification.




**CoordinatorNodeStorageSpec ** <span data-label="purple">Object </span>`Example value: --`

Storage specifications configuration details for the coordinating node.


**Name ** <span data-label="purple">String </span>`Example value: es.volume.essd.pl0`

Storage specifications, the current specifications are as follows:

es.volume.essd.pl0: Standard Edition \- High\-Performance Cloud Disk \- pl0.



**Size** <span data-label="purple">Integer</span> `Example value: 20`

Current storage specification value in GiB.



**MaxSize ** <span data-label="purple">Integer </span>`Example value: 10000`

The maximum value of the storage specification, in GiB.



**MinSize ** <span data-label="purple">Integer </span>`Example value: 20`

Minimum storage specification, unit: GiB.



**Description ** <span data-label="purple">String </span>`Example value: Standard Edition - High-Performance Cloud Volume - pl0`

Description of storage specifications.



**DisplayName ** <span data-label="purple">String </span>`Example: ESSD-PL0`

Display name of storage specifications.




**CoordinatorNodeResourceSpec ** <span data-label="purple">Object </span>`Example value: --`

Node specification configuration details for the coordinating node.


**CPU ** <span data-label="purple">Integer </span>`Example value: 2`

CPU resources of the node specification, unit: core



**Name ** <span data-label="purple">String </span>`Example: es.x2.medium`

Node specification. Refer to node specification types and details.



**Memory ** <span data-label="purple">Integer </span>`Example: 4`

Memory capacity of the node specification in GiB.



**Description ** <span data-label="purple">String </span>`Example value: Standard version-2C4G node`

Description of node specification.



**DisplayName ** <span data-label="purple">String </span>`Example: 2Core 4GiB`

Display name of the node specification.





**EnableESPrivateNetwork ** <span data-label="purple">Boolean </span>`Example value:`true

Whether the instance has turned on private network access. true: default, private network access turned on. false: private network access not enabled.



**KibanaPublicIpWhitelist ** <span data-label="purple">String </span>`Example value: 182.*.*.*`

Kibana public network IP whitelist. Only IP addresses added to the whitelist can access the visualization tool.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Cerebro and Kibana share the same whitelist</div>




**KibanaPrivateIpWhitelist ** <span data-label="purple">String </span>`Example: 192.168.1.1,192.168.1.2`

Kibana private network whitelist. Only IP addresses added to the whitelist can access the visualization tool.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Cerebro and Kibana share the same whitelist.</div>




**EnableKibanaPublicNetwork ** <span data-label="purple">Boolean </span>`Example value:`true

Enable public network access for Kibana. true: public network access is enabled. false: public network access is not enabled.



**EnableKibanaPrivateNetwork ** <span data-label="purple">Boolean </span>`Example:`true

Whether to enable private network access for Kibana. true: default value, private network access is enabled. false: private network access for Kibana is not enabled.



**EnableESPrivateDomainPublic** <span data-label="purple">Boolean</span> `Example value:` true

Whether the instance has enabled public network resolution. true: public network resolution enabled. false: public network resolution not enabled.



**EnableKibanaPrivateDomainPublic ** <span data-label="purple">Boolean </span>`Example value:`true

Whether Kibana enables public network resolution. true: public network resolution is enabled. false: public network resolution not enabled.



**KibanaPublicIpAllowList** <span data-label="purple">String</span> `Example value: 182.*.*.*`

Kibana public network whitelist. Only IP addresses added to the whitelist can access the visualization tool. Same as KibanaPublicIpWhitelist.



**KibanaPrivateIpAllowList ** <span data-label="purple">String </span>`Example value: 192.168.1.1,192.168.1.2`

Kibana private network whitelist. Only IP addresses added to the whitelist can access the visualization tool. Same as KibanaPrivateIpWhitelist.



**ESPublicIpAllowList ** <span data-label="purple">String </span>`Example: 182.*.*.*`

Whitelist for instance public IP address access. Same as ESPublicIpWhitelist.



**ESPrivateIpAllowList ** <span data-label="purple">String </span>`Example value: 192.168.1.1,192.168.1.2`

Instance private network address access whitelist. Same as ESPrivateIpWhitelist.



**SubInstanceEnable ** <span data-label="purple">String </span>`Example value: None`

Sub\-instance enable status.




**TotalCount ** <span data-label="purple">Long </span>`Example: 2`

Total number of instances returned.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```text
POST /?Action=DescribeInstances&Version=2023-01-01
Host: escloud.cn-beijing.byteplusapi.com.cn
Content-Type: application/json
X-Date: 20231003T104027Z
Authorization: HMAC-SHA256 
Credential=AKLTMjI2ODVlYzI3ZGY1NGU4ZjhjYWRjMTlmNTM5OTZ****/20231003/cn-beijing/ESCloud/request, SignedHeaders=content-type;host;x-date, Signature=88dd0a9ea555d8609ec83eb46054b52f6cd4f79b8d5094fa784c66fa3f2b****
{
    "Filters": [
        {
            "Name": "InstanceName",
            "Values": ["doc"]
        }
    ],
    "PageNumber": 1,
    "PageSize": 10
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```json
{
  "ResponseMetadata": {
    "RequestId": "2025033114421725011417324504B7B3",
    "Action": "DescribeInstances",
    "Version": "2023-01-01",
    "Service": "ESCloud",
    "Region": "cn-beijing"
  },
  "Result": {
    "Instances": [
      {
        "ESEip": "180.*.*.*",
        "Status": "Running",
        "UserId": "210***34",
        "ESEipId": "eip-mij5ztefl98**",
        "ClusterId": "16a119e0d***41ae2627b0",
        "KibanaEip": "180.*.*.*",
        "CreateTime": "2024-03-21T10:32:24+08:00",
        "ExpireDate": "2023-11-11T15:59:59.000+00:00",
        "InstanceId": "o-00k***o718",
        "MainZoneId": "cn-beijing-a",
        "TotalNodes": 0,
        "KibanaEipId": "eip-mij5ztefl98**",
        "KibanaConfig": {
          "CookieTTL": 3600000,
          "SessionTTL": 3600000,
          "KibanaBasePath": "/kibana/{psm}/{idc}",
          "RequestTimeout": 30000,
          "SessionKeepAlive": true
        },
        "ResourceTags": [
          {
            "Type": "CUSTOM",
            "TagKvs": {},
            "TagKeys": [
              "tom"
            ]
          }
        ],
        "SubInstances": [
          {
            "SubInstanceStatus": "AVAILABLE",
            "SubInstanceId": "k-00g0oh**",
            "SubInstanceType": "sql"
          }
        ],
        "TransferInfo": {
          "ForbidStop": true,
          "TransferStatus": "FINISH",
          "TransferTaskId": "88dbdf2431b44f36**",
          "ReduceSpecConfig": {
            "ColdNodeNum": 0,
            "DataNodeNum": 3,
            "WarmNodeNum": 3,
            "MasterNodeNum": 3,
            "EnablePureMaster": true
          },
          "TransferProgress": 100
        },
        "ChargeEnabled": true,
        "CerebroEnabled": true,
        "MaintenanceDay": [
          "[\"MONDAY\",\"TUESDAY\",\"WEDNESDAY\",\"THURSDAY\",\"FRIDAY\",\"SATURDAY\",\"SUNDAY\"]"
        ],
        "MaintenanceTime": "03:00-06:00",
        "SupportColdNode": true,
        "ESPublicEndpoint": "https://elasticsearch-o-00k***o718..escloud.volces.com:9200",
        "ESPrivateEndpoint": "https://elasticsearch-o-00k***o718.escloud.ivolces.com:9200",
        "DeletionProtection": true,
        "KibanaPublicDomain": "https://visual-o-00**.escloud.volces.com:5601",
        "CerebroPublicDomain": "https://visual-o-00g**.escloud.volces.com:9000/",
        "ESPublicIpWhitelist": "182.*.*.*",
        "KibanaPrivateDomain": "https://visual-o-00**.escloud.ivolces.com:5601",
        "CerebroPrivateDomain": "https://visual-o-**.escloud.ivolces.com:5601",
        "ESPrivateIpWhitelist": "192.168.1.1,192.168.1.2",
        "EnableESPublicNetwork": true,
        "InstanceConfiguration": {
          "VPC": {
            "VpcId": "vpc-274uhjap8u72****",
            "VpcName": "vpc_nameA"
          },
          "Subnet": {
            "SubnetId": "subnet-1323sdda****",
            "SubnetName": "subnet_nameA"
          },
          "ZoneId": "cn-beijing-a",
          "Version": "V7_10",
          "RegionId": "cn-beijing",
          "ChargeType": "PostPaid",
          "ZoneNumber": 0,
          "EnableHttps": true,
          "ProjectName": "default",
          "InstanceName": "doc-test",
          "AdminUserName": "admin",
          "HotNodeNumber": 0,
          "ColdNodeNumber": 0,
          "WarmNodeNumber": 0,
          "EnablePureMaster": true,
          "KibanaNodeNumber": 0,
          "MasterNodeNumber": 0,
          "HotNodeStorageSpec": {
            "Name": "es.volume.essd.pl0",
            "Size": 0,
            "MaxSize": 0,
            "MinSize": 0,
            "Description": "标准版-高性能云盘-pl0",
            "DisplayName": "ESSD-PL0"
          },
          "ColdNodeStorageSpec": {
            "Name": "es.volume.essd.pl0",
            "Size": 20,
            "MaxSize": 10000,
            "MinSize": 20,
            "Description": "标准版-高性能云盘-pl0",
            "DisplayName": "ESSD-PL0"
          },
          "HotNodeResourceSpec": {
            "CPU": 0,
            "Name": "es.x2.medium",
            "Memory": 0,
            "Description": "标准版-2C4G节点",
            "DisplayName": "2核4GiB"
          },
          "WarmNodeStorageSpec": {
            "Name": "es.volume.essd.pl0",
            "Size": 20,
            "MaxSize": 10000,
            "MinSize": 20,
            "Description": "标准版-高性能云盘-pl0",
            "DisplayName": "ESSD-PL0"
          },
          "ColdNodeResourceSpec": {
            "CPU": 2,
            "Name": "es.x2.medium",
            "Memory": 4,
            "Description": "标准版-2C4G节点",
            "DisplayName": "2核4GiB"
          },
          "WarmNodeResourceSpec": {
            "CPU": 2,
            "Name": "es.x2.medium",
            "Memory": 4,
            "Description": "标准版-2C4G节点",
            "DisplayName": "2核4GiB"
          },
          "CoordinatorNodeNumber": 0,
          "MasterNodeStorageSpec": {
            "Name": "es.volume.essd.pl0",
            "Size": 20,
            "MaxSize": 10000,
            "MinSize": 20,
            "Description": "标准版-高性能云盘-pl0",
            "DisplayName": "ESSD-PL0"
          },
          "KibanaNodeResourceSpec": {
            "CPU": 2,
            "Name": "es.x2.medium",
            "Memory": 4,
            "Description": "标准版-2C4G节点",
            "DisplayName": "2核4GiB"
          },
          "MasterNodeResourceSpec": {
            "CPU": 2,
            "Name": "es.x2.medium",
            "Memory": 4,
            "Description": "标准版-2C4G节点",
            "DisplayName": "2核4GiB"
          },
          "CoordinatorNodeStorageSpec": {
            "Name": "es.volume.essd.pl0",
            "Size": 20,
            "MaxSize": 10000,
            "MinSize": 20,
            "Description": "标准版-高性能云盘-pl0",
            "DisplayName": "ESSD-PL0"
          },
          "CoordinatorNodeResourceSpec": {
            "CPU": 2,
            "Name": "es.x2.medium",
            "Memory": 4,
            "Description": "标准版-2C4G节点",
            "DisplayName": "2核4GiB"
          }
        },
        "EnableESPrivateNetwork": true,
        "KibanaPublicIpWhitelist": "182.*.*.*",
        "KibanaPrivateIpWhitelist": "192.168.1.1,192.168.1.2",
        "EnableKibanaPublicNetwork": true,
        "EnableKibanaPrivateNetwork": true,
        "EnableESPrivateDomainPublic": true,
        "EnableKibanaPrivateDomainPublic": true,
        "KibanaPublicIpAllowList": "182.*.*.*",
        "KibanaPrivateIpAllowList": "192.168.1.1,192.168.1.2",
        "ESPublicIpAllowList": "182.*.*.*",
        "ESPrivateIpAllowList": "192.168.1.1,192.168.1.2",
        "SubInstanceEnable": "None"
      }
    ],
    "TotalCount": 2
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

The following table lists error codes related to this API and business logic. For more information, see [Public error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|200 |InternalServerError |Internal server exception |The service exited due to an exception and cannot complete the interface request operation. |
|200 |IllegalParameter |illegal parameter |Invalid parameter. The reason may be a missing parameter or noncompliance with API requirements. |
|200 |Unauthorized |unauthorized error |User lacks permission to call the interface. |
