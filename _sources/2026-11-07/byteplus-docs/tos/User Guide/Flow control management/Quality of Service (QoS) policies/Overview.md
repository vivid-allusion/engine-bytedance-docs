---
title: "Overview"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Qos-policy-overview"
---

A Quality of Service (QoS) policy controls traffic to and from TOS resources. It allows you to manage throttling for resource groups shared by multiple workloads as needed. This ensures that workloads sharing the same resources operate efficiently without disrupting each other.

<span id="0277580b"></span>
## Use cases

<span id="OIUuLrY5"></span>
### Threshold‑based throttling

Threshold\-based throttling allows you to control traffic to and from TOS resource groups based on account, user, or role. These policies can be applied at various levels, such as to all TOS buckets, to specific buckets, or even to individual objects, to isolate traffic between workloads and prevent resource contention across different business activities. This feature is ideal for multi\-tenant setups, multi\-department organizations, and scenarios in which multiple workloads share the same TOS resources.

<span id="cetoO9V5"></span>
### Priority\-based throttling

To manage complex online workloads, it is necessary to both isolate and manage traffic using granular, tiered QoS policies. In addition to preventing aggressive contention, different workloads require guaranteed minimum resources and preemption capability.


* Ensuring business\-critical workloads: Critical workloads with high priorities, such as online transactions and critical data uploads, require guaranteed bandwidth. These workloads should not experience performance degradation or resource shortages due to contention, even under high system loads.

* Maximizing resource utilization: When the system is not heavily loaded, non\-critical workloads, such as offline analysis and log backhaul, can temporarily "borrow" idle bandwidth to improve overall resource utilization. Once traffic from higher\-priority workloads increases again, the system should automatically reclaim the "borrowed" quota to prevent critical workloads from being affected.


Thus, priority\-based throttling adds multiple priority levels and guaranteed quotas to threshold\-based throttling. The two schemes complement each other to build a QoS system that ensures the stable operation of core services while maximizing resource utilization.

<span id="2CquExF7"></span>
## Effective rules

<span id="4wX3CsaX"></span>
### Threshold‑based throttling

When multiple limits of the same type are in effect simultaneously, the actual quota is the lowest value among all active rules. For example, if a request matches multiple QoS policies, all of the policies take effect. If the policies have the same type of throttling limit, the smallest quota is used.

<span id="fTsPbv2N"></span>
### Priority\-based throttling


* **Guaranteed quota**

   * Each priority level is assigned a guaranteed quota. No matter how busy the system is, that priority level receives at least its guaranteed bandwidth or QPS. This ensures the stable operation of core services.

   * The sum of the guaranteed quotas for all priority levels is less than or equal to the total resource quota.

* **Rule matching**

   * In the same QoS policy, priority\-based and threshold\-based throttling cannot be used together.

   * When a request matches the conditions of multiple priority levels, the system applies the highest priority rule. For example, if a request matches both priority 3 and priority 2, it is treated as priority 3.

* **Quota preemption**

   * Higher\-priority workloads can preempt any portion of the total resources that exceeds the sum of the guaranteed quotas. Workloads with a higher priority have preemption priority over those with a lower priority.

   * Lower\-priority workloads may use idle guaranteed quotas from higher\-priority workloads, but higher\-priority workloads take precedence when needed.


<span id="DpsiTchT"></span>
## Common configuration scenarios

Suppose a QoS policy has a total bandwidth limit of 100 Gbps and three priority levels (1–3), with higher numbers indicating higher priority.

**Scenario 1: Higher\-priority workloads preempt any portion of the total resources that exceeds the sum of the guaranteed quotas.** 


|**Priority** |**Guaranteed quota** |**Demand** |**Allocation** |**Description** |
|---|---|---|---|---|
|Priority 3<br><br> |20 Gbps<br><br> |80 Gbps<br><br> |70Gbps<br><br> |Receives 20 Gbps of guaranteed quota + 10 Gbps of idle time from Priority\-1 workloads + 40 Gbps from the pool (after deducting all guaranteed quotas from the total resources). |
|Priority 2 |20 Gbps |30 Gbps |20 Gbps |Receives 20 Gbps of guaranteed quota. The additional 10 Gbps it requires is preempted by Priority\-3 workloads. |
|Priority 1 |20 Gbps |10 Gbps |10 Gbps |Receives the demanded 10 Gbps from the guaranteed quota, with remaining 10 Gbps being preempted by Priority\-3 workloads. |


**Scenario 2: Workloads with a higher priority have preemption priority over those with a lower priority.** 


|**Priority** |**Guaranteed quota** |**Demand** |**Allocation** |**Description** |
|---|---|---|---|---|
|Priority 3 |25 Gbps |60 Gbps |60 Gbps |Receives 25 Gbps of guaranteed quota + 35 Gbps preempted as the top priority. |
|Priority 2 |25 Gbps |40 Gbps |35Gbps |Receives 25 Gbps of guaranteed quota + 10 Gbps preempted as the second highest priority. |
|Priority 1 |25 Gbps |5 Gbps |5 Gbps |Receives 5 Gbps as the demand is less than the guaranteed quota. |


**Scenario 3: The sum of the guaranteed quotas is less than the total bandwidth.** 


|**Priority** |**Guaranteed quota** |**Demand** |**Allocation** |**Description** |
|---|---|---|---|---|
|Priority 3 |10 Gbps |30 Gbps |30 Gbps |Demand fully satisfied as the highest priority. |
|Priority 2 |10 Gbps |50 Gbps |50 Gbps |Demand fully satisfied as the second highest priority. |
|Priority 1 |10 Gbps |50 Gbps |20 Gbps |Receives 10 Gbps of guaranteed quote + 10 Gbps from the pool. |


<span id="dBMgvLV2"></span>
## Parameters

A statement serves as a container for the main policy elements. A single policy may include multiple statements, each of which contains the following parameters:


|Parameter |Required |Description |Example |
|---|---|---|---|
|Sid |No |A unique identifier for the policy statement. The statement names must:<br><br><br>* Be unique.<br><br>* Contain only uppercase and lowercase letters, numbers, hyphens (\-), underscores (_), periods (.), colons (:) and percent signs (%).<br><br>* Be between 1 and 255 characters long.<br><br><br>If this parameter is not specified, TOS will automatically generate a statement name. |```Plain```<br>```{"Sid":"Test"}```<br> |
|Quota |Yes |The throttling limits for the QoS policy. Options:<br><br><br>* `WritesQps`: The QPS limit for write requests. Enter a positive integer.<br><br>* `ReadsQps`: The QPS limit for read requests. Enter a positive integer.<br><br>* `ListQps`: The QPS limit for list requests. Enter a positive integer.<br><br>* `WritesRate`: The upload bandwidth limit in Mbps. Enter a positive integer.<br><br>* `ReadsRate`: The download bandwidth limit in Mbps. Enter a positive integer.<br><br>* `FetchQps`: The QPS limit for synchronous fetches. Enter a positive integer.<br><br>* `FetchRate`: The bandwidth limit for synchronous fetches in Mbps. Enter a positive integer.<br><br>* `AsyncFetchQps`: The QPS limit for asynchronous fetches. Enter a positive integer.<br><br>* `AsyncFetchRate`: The bandwidth limit for asynchronous fetches in Mbps. Enter a positive integer. |```Plain```<br>```"Quota": {```<br>```  "WritesQps": "100",```<br>```  "ReadsQps": "100",```<br>```  "ListQps": "100",```<br>```  "WritesRate": "10",```<br>```  "ReadsRate": "10",```<br>```  "FetchQps": "100",```<br>```  "FetchRate": "10",```<br>```  "AsyncFetchQps": "100",```<br>```  "AsyncFetchRate": "10"```<br>```}```<br> |
|Priority |No<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter is required for priority\-based throttling.</div><br> |The priority of the QoS policy defines the order in which different workloads compete for resources. A higher\-priority workload can take resources away from a lower\-priority one. |```Plain Text```<br>```"Priority": [```<br>```        {```<br>```          "PriorityLevel": 2,```<br>```          "GuaranteedQuota": {```<br>```            "WritesRate": "1000"```<br>```          },```<br>```          "Principal": [```<br>```            "trn:iam::200000:user/core-service"```<br>```          ],```<br>```          "Resource": "trn:tos:::critical-bucket2/*"```<br>```        },```<br>```        {```<br>```          "PriorityLevel": 1,```<br>```          "GuaranteedQuota": {```<br>```            "WritesRate": "1000"```<br>```          },```<br>```          "Principal": [```<br>```            "trn:iam::200000:user/core-service"```<br>```          ],```<br>```          "Resource": "trn:tos:::critical-bucket1/*"```<br>```        }```<br>```      ]```<br><br><br> |
|PriorityLevel |No<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter is required for priority\-based throttling.</div><br> |The QoS policy's priority level follows these rules:<br><br><br>* It takes natural numbers starting from 1, and they must be consecutive and unique. For example, 1/2 and 1/2/3 are supported, but 1/3 is not.<br><br>* At least 2 and at most 3 priority levels must be configured. A higher number indicates a higher priority. |```Plain Text```<br>```{"PriorityLevel": 3}```<br><br><br> |
|GuaranteedQuota |No<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter is required for priority\-based throttling.</div><br> |The minimum amount of resources reserved for a specific priority level. Even when the system is fully loaded, this level is guaranteed to receive this amount or more. This value follows the same rules as the `Quota` parameter.<br><br>Each priority level must be assigned a guaranteed quota greater than 0. In other words, a guaranteed quota must be assigned to each additional priority level. The sum of the guaranteed quotas for all priority levels must be less than or equal to the total quota. |```Plain Text```<br>```"GuaranteedQuota": {```<br>```   "WritesRate": "3000"```<br>```}```<br><br><br> |
|Resource |No<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When configuring a QoS policy, you must specify the target resources using either the <code>Resource</code> or <code>NotResource</code> parameter.</div><br> |The resources that are subject to throttling.<br><br><br>* The value must be a case\-insensitive string in the format of `"Resource": ["trn:tos:::{BucketName}/{Object}"]`.<br><br>* Wildcards (`*`) are allowed. Specifically:<br><br>   * At the bucket level, `*` matches all buckets (e.g., `"trn:tos:::*"`).<br><br>   * At the object level, `*` matches all resources within a bucket (e.g., `"trn:tos:::bucketname/*"`).<br><br>   * \* after an object prefix matches all objects with that prefix (e.g., `"trn:tos:::bucketname/objectPrefix*"`). |```Plain```<br>```"Resource":[```<br>```  // Apply the QoS policy to all buckets.```<br>```  "trn:tos:::*",```<br>```  // Apply the QoS policy to all objects within the "bucketname" bucket.```<br>```  "trn:tos:::bucketname/*",```<br>```  // Apply the QoS policy to objects with the "objectPrefix" prefix in the "bucketname" bucket.```<br>```  "trn:tos:::bucketname/objectPrefix*"```<br>```]```<br> |
|NotResource |No<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When configuring a QoS policy, you must specify the target resources using either the <code>Resource</code> or <code>NotResource</code> parameter.</div><br> |The resources that are not subject to throttling.<br><br><br>* The value must be a case\-insensitive string in the format of `"NotResource": ["trn:tos:::{BucketName}/{Object}"]`.<br><br>* Wildcards (`*`) are allowed. Specifically:<br><br>   * At the object level, `*` matches all resources within a bucket (e.g., `"trn:tos:::bucketname/*"`).<br><br>   * \* after an object prefix matches all objects with that prefix (e.g., `"trn:tos:::bucketname/objectPrefix*"`).<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><code>NotResource</code> does not support the use of <code>*</code> at the bucket level (e.g., <code>"NotResource":["trn:tos:::*"]</code>).   </div><br>    |```Plain```<br>```"NotResource":[```<br>```  // Apply the QoS policy to all buckets except the "bucketname" bucket.```<br>```  "trn:tos:::bucketname/*",```<br>```  // Apply the QoS policy to all objects in the "bucketname" bucket, except objects with the "objectPrefix" prefix.```<br>```  "trn:tos:::bucketname/objectPrefix*"```<br>```]```<br> |
|Principal |No<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When configuring a QoS policy, you must specify the target account using either the <code>Principal</code> or <code>NotPrincipal</code> parameter.</div><br> |The accounts, IAM users, or roles that are subject to throttling. |```Plain```<br>```"Principal": [```<br>```  // Apply the QoS policy to the role 'tos_role' under account 200000****.```<br>```  "trn:iam::200000****:role/tos_role",```<br>```  // Apply the QoS policy to the user 'tos_user' under account 200000****.```<br>```  "trn:iam::200000****:user/tos_user",```<br>```  // Apply the QoS policy to account 200001****.```<br>```   "trn:iam::200001****:root",```<br>```  // Apply the QoS policy to all users under account 200000****.```<br>```   "*"```<br>``` ]```<br> |
|NotPrincipal |No<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When configuring a QoS policy, you must specify the target account using either the <code>Principal</code> or <code>NotPrincipal</code> parameter.</div><br> |The accounts, IAM users, or roles that are not subject to throttling.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Using a wildcard (<code>*</code>) with <code>NotPrincipal</code> is not supported. In other words, <code>"NotPrincipal":["*"]</code> is not permitted.</div><br> |```Plain```<br>``` "NotPrincipal": [```<br>```   // Apply the QoS policy to all roles except 'tos_role' under account 200000****.```<br>```   "trn:iam::200000****:role/tos_role",```<br>```   // Apply the QoS policy to all users except 'tos_user' under account 200000****.```<br>```   "trn:iam::200000****:user/tos_user",```<br>```   // Apply the QoS policy to all accounts except account 200000****.```<br>```   "trn:iam::200001****:root"```<br>```  ]```<br> |
|Condition |No |The conditions for the statement to take effect. For more information, see [Conditions](https://docs.byteplus.com/en/docs/tos/Qos-policy-overview#aNd3FkmH). |```Plain```<br>```"Condition": {```<br>```        "IpAddress": {```<br>```                "SourceIp": [```<br>```                        "192.168.0.1",```<br>```                        "192.168.0.3"```<br>```                ]```<br>```        }```<br>```}```<br> |


<span id="aNd3FkmH"></span>
## Conditions

The conditions determine when a QoS policy takes effect. A QoS policy is applied only when its condition expressions match the values in the request. Each condition consists of a condition operator, a key, and a value. The conditions supported by QoS policies are listed below.

<span id="3b8288d2"></span>
### Supported conditions


|**Key** |**Condition operator type** |**Key description** |**Value description** |
|---|---|---|---|
|CurrentTime |Date |The time when the server receives a request, in the UTC time format yyyy\-MM\-ddTHH:mmZ, according to ISO 8601. |Enter a date in ISO 8601 format.<br><br>For example, if the QoS policy condition is set to `CurrentTime is greater than 2023-10-13T15:00:00Z`, the time at which an authorized account performs the corresponding action must be after 2023\-10\-13T15:00:00Z. Otherwise, the QoS policy will not take effect. |
|EpochTime |Numeric |The number of seconds that have elapsed since midnight on January 1, 1970, UTC/GMT, excluding leap seconds. |Enter the number of seconds.<br><br>For example, if the QoS policy condition is set to `EpochTime is greater than 1697187692`, the time at which an authorized account performs the corresponding action must be after 1697187692. Otherwise, the QoS policy will not take effect. |
|SourceIp |String |The source IP of the request. |Enter IP addresses or ranges. Use commas to separate multiple IP addresses.<br><br>For example, if the QoS policy condition is set to `SourceIp is equal to 192.168.0.1`, the source IP address must be "192.168.0.1" when an authorized account performs the corresponding action. Otherwise, the QoS policy will not take effect. |
|SourceVpc |String |The VPC from which the request has been initiated. |Enter a VPC ID.<br><br>For example, if the QoS policy condition is set to `SourceVpc is equal to vpc-2d****ez0n`, an authorized account must make the request from the `vpc-2d****ez0n` VPC when performing the corresponding action. Otherwise, the QoS policy will not take effect. |
|UserAgent |String |The user agent of the request. |Enter the information of the agent and a wildcard (\*), where applicable.<br><br>For example, if the QoS policy condition is set to `UserAgent is equal to tos go sdk v2.6.0`, the user agent must be "tos go sdk v2.6.0" when an authorized account performs the corresponding action. Otherwise, the QoS policy will not take effect. |
|Referer |String |The URL from which the resource has been requested. |Enter a URL.<br><br>For example, if the QoS policy condition is set to `Referer is equal to http://console.volcengine.com`, the request header must be `http://console.volcengine.com` when an authorized account performs the corresponding action. Otherwise, the QoS policy will not take effect. |
|Host |String |The domain name accessed by the request. |Enter a domain name.<br><br>For example, if the QoS policy condition is set to `Host is equal to bucketname.tos-cn-beijing.volces.com`, an authorized account must perform the corresponding action via the `bucketname.tos-cn-beijing.volces.com` domain name. Otherwise, the QoS policy will not take effect. |
|NetPlane |String |The layer of network architecture from which the request has been initiated. |The value is fixed as `public`, indicating the request should come from the public network.<br><br>For example, if the QoS policy condition is set to `NetPlane is equal to public`, an authorized account must make the request from the public network when performing the corresponding action. Otherwise, the QoS policy will not take effect. |
|ProjectName |String |The project to which the requested resources belong. |Enter the project to which the requested resources belong.<br><br>For example, if the QoS policy condition is set to ProjectName is equal to `test`, the requested resources must belong to the `test` project when an authorized account performs the corresponding action. Otherwise, the QoS policy will not take effect. |
|DataAccessPointTrn |String |Controls traffic sent to and from the specified access point. |Enter an access point `TRN`.<br><br>For example, if the QoS policy condition is set to `DataAccessPointTrn is equal to` <br><br>`trn:tos:cn-beijing:214748****:accesspoint/bbb`, the QoS policy will only apply when the principal accesses the bucket through the `trn:tos:cn-beijing:214748****:accesspoint/bbb` access point.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Use the DataAccessPointTrn condition only when you want to control traffic based on access points.</div><br> |
|DataAccessPointAccount |String |Controls traffic sent to and from access points within a specific account. |Enter an account ID.<br><br>For example, if the QoS policy condition is set to `DataAccessPointAccount is equal to 214748****`, the QoS policy will only apply when the principal uses access points of the account `214748****` to access the bucket.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Use the DataAccessPointAccount condition only when you want to control traffic based on access points.</div><br> |
|AccessPointNetworkOrigin |String |Controls traffic sent to and from access points with the specified network origin. |Enter VPC or Internet.<br><br><br>* VPC: Controls traffic through access points whose network origin is **VPC**.<br><br>* Internet: Controls traffic through access points whose network origin is **Internet**.<br><br><br>For example, if the QoS policy condition is set to `AccessPointNetworkOrigin is equal to VPC`, the QoS policy will only apply when the principal uses access points with a **VPC** network origin to access the bucket.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Use the AccessPointNetworkOrigin condition only when you want to control traffic based on access points.</div><br> |


<span id="f65abf44"></span>
### Condition operators

In QoS policies, condition keys and condition operators are matched as follows.


|**Condition key** |**Condition operator** |
|---|---|
|* UserAgent<br><br>* Referer<br><br>* SourceVPC<br><br>* Host<br><br>* ProjectName<br><br>* DataAccessPointTrn<br><br>* DataAccessPointAccount<br><br>* AccessPointNetworkOrigin |* **Equal To**: Exact matching.<br><br>* **Not Equal To**: Negated matching.<br><br>* **Equal To (Case\-Insensitive)** : Exact matching, ignoring case.<br><br>* **Not Equal To (Case\-Insensitive)** : Negated matching, ignoring case.<br><br>* **Like**: Case\-sensitive matching. Values can include a multi\-character match wildcard (\*). For example, `Like abc*` matches all strings that start with `abc`.<br><br>* **Not Like**: Negated case\-sensitive matching. Values can include a multi\-character match wildcard (\*). For example, `Not Like abc*` excludes all strings that start with `abc`. |
|* CurrentTime<br><br>* EpochTime |* **Equal To**: Exact matching.<br><br>* **Not Equal To**: Negated matching.<br><br>* **Less Than**: "Less than" matching.<br><br>* **Less Than or Equal To**: "Less than or equals" matching.<br><br>* **Greater Than**: "Greater than" matching.<br><br>* **Greater Than or Equal To**: "Greater than or equals" matching. |
|* SourceIp<br><br>* NetPlane |* **Equal To**: Exact matching.<br><br>* **Not Equal To**: Negated matching. |


<span id="446f82ad"></span>
## Configuration methods

There are two configuration methods for QoS policies. Refer to the following documentation to choose the appropriate method:


* [Creating a QoS policy in visual view](https://docs.byteplus.com/en/docs/tos/Create-a-qos-policy#a5380bf5)

* [Creating a QoS policy in JSON view](https://docs.byteplus.com/en/docs/tos/Create-a-qos-policy#94ae834d)
