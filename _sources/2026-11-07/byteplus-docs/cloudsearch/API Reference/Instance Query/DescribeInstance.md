---
title: "DescribeInstance"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/DescribeInstance"
---

Call DescribeInstance to query the configuration details of a specified instance.

<span id="0f7997ba"></span>
## Request Description


* Request method: POST

* Request URL: /?Action=DescribeInstance&Version=2023\-01\-01 HTTP/1.1


<span id="b7c23d7c"></span>
## Request parameters

<span id="d20615b2"></span>
### Query


|**Name** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |`DescribeInstance` |The action that you want to perform. Value: `DescribeInstance`. |
|Version |String |Yes |`2023-01-01` |The version of the API. Value: `2023-01-01`. |


<span id="b3210c10"></span>
### Body


|**Name** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |o\-00k\*\*\*\*o718 |The ID of the instance for which you want to query the configuration details. |


<span id="0ff2debc"></span>
## Response parameters


|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|InstanceInfo |Object of [ESInstanceInfoDTO](https://docs.byteplus.com/docs/cloudsearch/DescribeInstance#dd7f9798) | |The configuration details of the instance. |


<span id="dd7f9798"></span>
### ESInstanceInfoDTO


|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|ESEip |String |`180. *.* .*` |EIP bound to the instance. |
|Status |String |`Running` |The current status of the instance. For more information on instance status, refer to [Instance status](https://docs.byteplus.com/en/docs/cloudsearch/instance-details). |
|UserId |String |`210***34` |The user ID of the instance owner. |
|ESEipId |String |`eip-mij5ztefl98**` |The ID of the EIP bound to the instance. |
|ClusterId |String |`16a119e0d***41ae2627b0` |The ID of the cluster to which the instance belongs. |
|KibanaEip |String |`180. *.* .*` |EIP bound to the Kibana. |
|CreateTime |String |`2024-03-21T10:32:24+08:00` |The creation time of the instance. |
|ExpireDate |String |`2023-11-11T15:59:59.000+00:00` |The expiration time of the subscription instance. |
|InstanceId |String |`o-00k***o718` |Instance ID. |
|TotalNodes |Integer |`12` |The total number of nodes in the instance. |
|KibanaEipId |String |`eip-mij5ztefl98**` |The ID of the EIP bound to the Kibana. |
|KibanaConfig |Object of [ESKibanaConfig](https://docs.byteplus.com/docs/cloudsearch/DescribeInstance#7bcc067d) | |Kibana configuration parameters. |
|ResourceTags |Array of [TagInfo](https://docs.byteplus.com/docs/cloudsearch/DescribeInstance#d71f4792) | |Tag information for instance. |
|TransferInfo |Object of [TransferInfo](https://docs.byteplus.com/docs/cloudsearch/DescribeInstance#3946ef29) | |Data migration task information. |
|ChargeEnabled |Boolean |`true` |Whether the instance has billing enabled. Valid values:<br><br><br>* true: Billing is enabled.<br><br>* false: Billing is disabled. |
|CerebroEnabled |Boolean |`true` |Whether the instance has enabled cerebro.<br><br><br>* true: enabled<br><br>* false: disabled |
|MaintenanceDay |Array of String |`["MONDAY","TUESDAY","WEDNESDAY","THURSDAY","FRIDAY","SATURDAY","SUNDAY"]` |The maintenance days for instance. |
|MaintenanceTime |String |`03:00-06:00` |The maintenance window for instance. |
|ESPublicEndpoint |String |`https://elasticsearch-o-00k***o718..escloud.bytepluses.com:9200` |The public endpoint of the instance. |
|ESPrivateEndpoint |String |`https://elasticsearch-o-00k***o718.escloud.ibytepluses.com:9200` |The private endpoint of the instance. |
|DeletionProtection |Boolean |`true` |Whether the deletion protection feature is enabled for instance.<br><br><br>* true: Deletion protection is enabled.<br><br>* false: Deletion protection is not enabled.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Once deletion protection is enabled for an instance, the instance cannot be deleted using the API or through the console.</div><br><br><br><div data-tips="true" data-tips-type="tip">To disable deletion protection, call <a href="https://docs.byteplus.com/docs/cloudsearch/ModifyDeletionProtection">ModifyDeletionProtection</a>.</div><br> |
|KibanaPublicDomain |String |`https://visual-o-00**.escloud.bytepluses.com:5601` |The public endpoint of Kibana.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If it is a historical instance, the access address may start with <code>http(s)://kibana-***</code>.</div><br> |
|CerebroPublicDomain |String |`https://visual-o-00g**.escloud.bytepluses.com:9000/` |The public endpoint of Cerebro .<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Cerebro and Kibana share domain names. If it is a historical instance, the access address may start with <code>http(s)://kibana-***</code>.</div><br> |
|ESPublicIpWhitelist |String |`182. *.* .*` |The public IP Allowlist of instance.<br><br><br>* An IP allowlist can contain IP address entries in a single IP address format or in CIDR block notation, such as 192.168.0.1 or 192.168.0.0/24. Multiple IP address entries are separated with commas ( , ).<br><br>* An IP allowlist can contain up to 300 IP address entries. |
|KibanaPrivateDomain |String |`https://visual-o-00**.escloud.ibytepluses.com:5601` |The private endpoint of Kibana.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If it is a historical instance, the access address may start with <code>http(s)://kibana-***</code>.</div><br> |
|CerebroPrivateDomain |String |`https://visual-o-**.escloud.ibytepluses.com:5601` |The private endpoint of Cerebro.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Cerebro and Kibana share domain names. If it is a historical instance, the access address may start with <code>http(s)://kibana-***</code>.</div><br> |
|ESPrivateIpWhitelist |String |`192.168.1.1,192.168.1.2` |The private IP Allowlist of instance.<br><br><br>* An IP allowlist can contain IP address entries in a single IP address format or in CIDR block notation, such as 192.168.0.1 or 192.168.0.0/24. Multiple IP address entries are separated with commas ( , ).<br><br>* An IP allowlist can contain up to 300 IP address entries. |
|EnableESPublicNetwork |Boolean |`true` |Whether public network access is enabled for instance.<br><br><br>* true: public network access is enabled.<br><br>* false: public network access is not enabled. |
|InstanceConfiguration |Object of [EsInstanceConfigurationInfoDTO](https://docs.byteplus.com/docs/cloudsearch/DescribeInstance#380537fc) | |The configuration details of the instance. |
|EnableESPrivateNetwork |Boolean |`true` |Whether virtual private cloud (VPC) access is enabled for instance.<br><br><br>* true: VPC access is enabled. This is the default value.<br><br>* false: VPC access is not enabled. |
|KibanaPublicIpWhitelist |String |`182. *.* .*` |The public IP Allowlist of Kibana.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Cerebro and Kibana share an IPAllowlist</div><br> |
|KibanaPrivateIpWhitelist |String |`192.168.1.1,192.168.1.2` |The private IP Allowlist of Kibana.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Cerebro and Kibana share an IPAllowlist</div><br> |
|EnableKibanaPublicNetwork |Boolean |`true` |Whether Kibana enables public network access.<br><br><br>* true: Enable<br><br>* false: Disable |
|EnableKibanaPrivateNetwork |Boolean |`true` |Whether Kibana enables private network access.<br><br><br>* true: Enable<br><br>* false: Disable |
|EnableESPrivateDomainPublic |Boolean |`true` |Whether instance enables DNS Lookup.<br><br><br>* true: Enable<br><br>* false: Disable |
|EnableKibanaPrivateDomainPublic |Boolean |`true` |KWhether Kibana enables DNS Lookup.<br><br><br>* true: Enable<br><br>* false: Disable |


<span id="7bcc067d"></span>
### ESKibanaConfig


|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|SessionTTL |Long |`3600000` |The validity period of the session. The default value is 3600000 milliseconds, that is, 1 hour.<br><br>If you set **SessionKeepAlive** to **false**, once the logon time of a user reaches the specified session validity period, the user is automatically logged off. |
|RequestTimeout |Long |`30000` |The timeout period for API requests. The default value is 30000 milliseconds. Once no response is returned from the back end after 30 seconds, a `503 Request timed out` error is reported.<br><br>To receive responses as expected and reduce 503 errors, increase the value of this parameter. |
|SessionKeepAlive |Boolean |`true` |Whether to actively extend the session validity period.<br><br><br>* **true**: The system extends the session validity period for each page request. This is the default value.<br><br>* **false**: The system does not extend the session validity period. If this option is used, sessions can time out and expire. Once the logon time of a user reaches the value specified in **SessionTTL**, the user is automatically logged off. |


<span id="d71f4792"></span>
### TagInfo


|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|Type |String |`CUSTOM` |The type of tag.<br><br><br>* CUSTOM: Custom set tags<br><br>* SYSTEM: System tags |
|TagKvs |JSON Map |`user` |tag key. |
|TagKeys |Array of String |`tom` |tag value. |


<span id="3946ef29"></span>
### TransferInfo


|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|TransferStatus |String |`FINISH` |Data migration task status. |
|TransferTaskId |String |`88dbdf2431b44f36**` |Data migration task status. |
|ReduceSpecConfig |Object of [ResourceSpecs](https://docs.byteplus.com/docs/cloudsearch/DescribeInstance#9e37e1fc) | |Resource information. |
|TransferProgress |Double |`100` |Data migration task progress, percentage scale. |


<span id="380537fc"></span>
### EsInstanceConfigurationInfoDTO


|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|VPC |Object of [VpcInfo](https://docs.byteplus.com/docs/cloudsearch/DescribeInstance#26857c6f) | |VPC information for instance. |
|Subnet |Object of [SubnetInfo](https://docs.byteplus.com/docs/cloudsearch/DescribeInstance#480f456b) | |Subnet information for instance. |
|ZoneId |String |`ap-southeast-1a` |The availability zone of the instance. |
|Version |String |`V7_10` |The instance version.<br><br><br>* ES instance: supports versions `V6_7` and `V7_10`.<br><br>* OpenSearch instance: supports version `OPEN_SEARCH_2_9`. |
|RegionId |String |`ap-southeast-1` |The region of the instance. |
|ChargeType |String |`PostPaid` |The billing method of the instance.<br><br><br>* PostPaid: pay\-as\-you\-go.<br><br>* PrePaid: subscription. |
|MainZoneId |String |`ap-southeast-1a` |Primary Availability Zone. |
|ZoneNumber |Integer |`1` |The number of availability zones for instance. |
|EnableHttps |Boolean |`true` |Whether the instance has HTTPS enabled.<br><br><br>* true: HTTPS is enabled.<br><br>* false: HTTPS is not enabled, and HTTP is used instead.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Using HTTP allows access without security authentication, and the data is transmitted in plaintext. Make sure that the access environment is secure and the access interface is not exposed to the internet.</div><br> |
|ProjectName |String |`default` |The project the instance belongs to.<br><br>Instances belong to the default project by default, and the project to which the instance belongs can be adjusted. |
|InstanceName |String |`doc-test` |Instance name |
|AdminUserName |String |`admin` |Instance administrator account, fixed to admin. |
|HotNodeNumber |Integer |`3` |the number of Data nodes. |
|ColdNodeNumber |Integer |`3` |the number of Cold data nodes. |
|WarmNodeNumber |Integer |`3` |the number of Warm data nodes. |
|EnablePureMaster |Boolean |`true` |Whether the master node operates independently.<br><br><br>* true: The master node operates independently.<br><br>* false: The master node functions also as a data node, that is, it is declared as Hot. |
|KibanaNodeNumber |Integer |`1` |the number of Kibana nodes. |
|MasterNodeNumber |Integer |`3` |the number of Master nodes. |
|HotNodeStorageSpec |Object of [StorageSpecs](https://docs.byteplus.com/docs/cloudsearch/DescribeInstance#70437656) | |Storage specifications and configuration details of the Data node. |
|ColdNodeStorageSpec |Object of [StorageSpecs](https://docs.byteplus.com/docs/cloudsearch/DescribeInstance#70437656) | |Storage specifications and configuration details of the Cold data node. |
|HotNodeResourceSpec |Object of [ResourceSpecs](https://docs.byteplus.com/docs/cloudsearch/DescribeInstance#9e37e1fc) | |Node specification configuration details of the Data node. |
|WarmNodeStorageSpec |Object of [StorageSpecs](https://docs.byteplus.com/docs/cloudsearch/DescribeInstance#70437656) | |Storage specifications and configuration details of the Warm data node. |
|ColdNodeResourceSpec |Object of [ResourceSpecs](https://docs.byteplus.com/docs/cloudsearch/DescribeInstance#9e37e1fc) | |Node specification configuration details of the Cold data node. |
|WarmNodeResourceSpec |Object of [ResourceSpecs](https://docs.byteplus.com/docs/cloudsearch/DescribeInstance#9e37e1fc) | |Node specification configuration details of the Warm data node. |
|CoordinatorNodeNumber |Integer |`3` |the number of Coordinator nodes. |
|MasterNodeStorageSpec |Object of [StorageSpecs](https://docs.byteplus.com/docs/cloudsearch/DescribeInstance#70437656) | |Storage specifications and configuration details of the Master node. |
|KibanaNodeResourceSpec |Object of [ResourceSpecs](https://docs.byteplus.com/docs/cloudsearch/DescribeInstance#9e37e1fc) | |Node specification configuration details of the Kibana node. |
|MasterNodeResourceSpec |Object of [ResourceSpecs](https://docs.byteplus.com/docs/cloudsearch/DescribeInstance#9e37e1fc) | |Node specification configuration details of the Master node. |
|CoordinatorNodeStorageSpec |Object of [StorageSpecs](https://docs.byteplus.com/docs/cloudsearch/DescribeInstance#70437656) | |Storage specifications and configuration details of the Coordinator node. |
|CoordinatorNodeResourceSpec |Object of [ResourceSpecs](https://docs.byteplus.com/docs/cloudsearch/DescribeInstance#9e37e1fc) | |Node specification configuration details of the Coordinator node. |


<span id="492bee22"></span>
### ReduceSpecConfig


|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|ColdNodeNum |Integer |`0` |the number of Cold data nodes. |
|DataNodeNum |Integer |`3` |the number of Data nodes. |
|WarmNodeNum |Integer |`3` |the number of Warm data nodes. |
|MasterNodeNum |Integer |`3` |The number of Master nodes. |
|EnablePureMaster |Boolean |`false` |Whether the master node operates independently.<br><br><br>* true: The master node operates independently.<br><br>* false: The master node functions also as a data node, that is, it is declared as Hot. |


<span id="26857c6f"></span>
### VpcInfo


|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|VpcId |String |`vpc-274uhjap8u72****` |VPC ID |
|VpcName |String |`vpc_nameA` |VPC name |


<span id="480f456b"></span>
### SubnetInfo


|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|SubnetId |String |`subnet-1323sdda****` |Subnet ID |
|SubnetName |String |`subnet_nameA` |Subnet name |


<span id="70437656"></span>
### StorageSpecs


|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|Name |String |`es.volume.essd.pl0` |The name of the storage specification. Valid value:<br><br><br>* es.volume.essd.pl0: High Performance Cloud Storage\-pl0<br><br>* es.volume.essd.flexpl: High Performance Cloud Storage\-Flexpl |
|Size |Integer |`20` |The amount of available disk space configured. |
|MaxSize |Integer |`10000` |The maximum size defined by the storage specification. Unit: GiB. |
|MinSize |Integer |`20` |The minimum size defined by the storage specification. Unit: GiB. |
|Description |String |`High Performance Cloud Storage-pl0` |The description of the storage specification. |
|DisplayName |String |`ESSD-PL0` |The display name of the storage specification. |


<span id="9e37e1fc"></span>
### ResourceSpecs


|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|CPU |Integer |`2` |The CPU resources defined by the instance type. Unit: cores. |
|Name |String |`es.x2.medium` |The instance type of the node. For more information on the types and details of instance types, refer to [instance types](https://docs.byteplus.com/en/docs/cloudsearch/specifications). |
|Memory |Integer |`4` |The memory capacity defined by the instance type. Unit: GiB. |
|Description |String |Standard\-2Core4GiB Node |The description of the instance type. |
|DisplayName |String |`2Core4GiB` |The display name of the instance type. |


<span id="4209de2e"></span>
## Sample request

```HTTP
POST https://open.ap-southeast-1.byteplusapi.com?Action=DescribeInstance&Version=2023-01-01
Content-Type: application/json
X-Date: 20231003T104027Z
Authorization: HMAC-SHA256 
Credential=AKLTMjI2ODVlYzI3ZGY1NGU4ZjhjYWRjMTlmNTM5OTZ****/20231003/ap-southeast-1/ESCloud/request, SignedHeaders=content-type;host;x-date, Signature=88dd0a9ea555d8609ec83eb46054b52f6cd4f79b8d5094fa784c66fa3f2b****
{
    "InstanceId": "o-0080**iu98"
}
```


<span id="0301ce08"></span>
## Sample response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202310231023****F0BC33AAEA",
        "Action": "DescribeInstance",
        "Version": "2023-01-01",
        "Service": "ESCloud",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "InstanceInfo": {
            "ChargeEnabled": true,
            "CreateTime": "2023-10-19T09:21:21.000+00:00",
            "DeletionProtection": false,
            "EnableESPrivateNetwork": true,
            "EnableESPublicNetwork": false,
            "EnableKibanaPrivateNetwork": true,
            "EnableKibanaPublicNetwork": false,
            "EnableESPrivateDomainPublic": false,
            "EnableKibanaPrivateDomainPublic": false,
            "Encrypted": false,
            "InstanceConfiguration": {
                "AdminUserName": "admin",
                "ChargeType": "PostPaid",
                "ColdNodeNumber": 3,
                "ColdNodeResourceSpec": {
                    "Description": "Standard-2Core4GiB Node",
                    "DisplayName": "2Core4GiB",
                    "Memory": 4,
                    "Name": "es.x2.medium",
                    "CPU": 2
                },
                "ColdNodeStorageSpec": {
                    "Description": "High Performance Cloud Storage-PL0",
                    "DisplayName": "ESSD-PL0",
                    "MaxSize": 10000,
                    "MinSize": 20,
                    "Name": "es.volume.essd.pl0",
                    "Size": 100,
                    "Type": ""
                },
                "EnableHttps": true,
                "EnablePureMaster": true,
                "HotNodeNumber": 3,
                "HotNodeResourceSpec": {
                    "Description": "Standard-2Core4GiB Node",
                    "DisplayName": "2Core4GiB",
                    "Memory": 4,
                    "Name": "es.x2.medium",
                    "CPU": 2
                },
                "HotNodeStorageSpec": {
                    "Description": "High Performance Cloud Storage-PL0",
                    "DisplayName": "ESSD-PL0",
                    "MaxSize": 10000,
                    "MinSize": 20,
                    "Name": "es.volume.essd.pl0",
                    "Size": 20,
                    "Type": ""
                },
                "CoordinatorNodeNumber": 2,
                "CoordinatorNodeResourceSpec": {
                    "Description": "Standard-2Core4GiB Node",
                    "DisplayName": "2Core4GiB",
                    "Memory": 4,
                    "Name": "es.x2.medium",
                    "CPU": 2
                },
                "CoordinatorNodeStorageSpec": {
                    "Description": "High Performance Cloud Storage-PL0",
                    "DisplayName": "ESSD-PL0",
                    "MaxSize": 10000,
                    "MinSize": 20,
                    "Name": "es.volume.essd.pl0",
                    "Size": 20,
                    "Type": ""
                },
                "InstanceName": "doc-test",
                "KibanaNodeNumber": 1,
                "KibanaNodeResourceSpec": {
                    "Description": "Kibana-1Core2GiB Node",
                    "DisplayName": "1Core2GiB",
                    "Memory": 2,
                    "Name": "kibana.x2.small",
                    "CPU": 1
                },
                "MasterNodeNumber": 3,
                "MasterNodeResourceSpec": {
                    "Description": "Standard-2Core4GiB Node",
                    "DisplayName": "2Core4GiB",
                    "Memory": 4,
                    "Name": "es.x2.medium",
                    "CPU": 2
                },
                "MasterNodeStorageSpec": {
                    "Description": "High Performance Cloud Storage-PL0",
                    "DisplayName": "ESSD-PL0",
                    "MaxSize": 10000,
                    "MinSize": 20,
                    "Name": "es.volume.essd.pl0",
                    "Size": 20,
                    "Type": ""
                },
                "RegionId": "ap-southeast-1",
                "Subnet": {
                    "SubnetId": "subnet-rrzpagj****7r53lac",
                    "SubnetName": "wuch_A_sub"
                },
                "Version": "V7_10",
                "WarmNodeNumber": 0,
                "ZoneId": "ap-southeast-1a",
                "ZoneNumber": 1,
                "VPC": {
                    "VpcId": "vpc-13fsccv****u46g3mus",
                    "VpcName": "wuch_vpc0110"
                }
            },
            "InstanceId": "o-00k****718",
            "KibanaPrivateDomain": "https://kibana-o-00k***o718.escloud.ibytepluses.com:5601",
            "KibanaPublicDomain": "",
            "MaintenanceDay": [
                "MONDAY",
                "TUESDAY",
                "WEDNESDAY",
                "THURSDAY",
                "FRIDAY",
                "SATURDAY",
                "SUNDAY"
            ],
            "MaintenanceTime": "02:00-08:00",
            "Namespace": "o-00k****o718",
            "Status": "Running",
            "TransferInfo": {},
            "TotalNodes": 12,
            "UserId": "210******34",
            "ClusterId": "16a119e0d5d*****1ae2627b0",
            "ESInnerEndpoint": "",
            "ESPrivateDomain": "",
            "ESPrivateEndpoint": "https://elasticsearch-o-00k***o718.escloud.ibytepluses.com:9200",
            "ESPublicDomain": "",
            "ESPublicEndpoint": ""
        }
    }
}
```
