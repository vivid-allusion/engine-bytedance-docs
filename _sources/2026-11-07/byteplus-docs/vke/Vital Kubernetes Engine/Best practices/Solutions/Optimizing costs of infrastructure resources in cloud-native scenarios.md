---
title: "Optimizing costs of infrastructure resources in cloud-native scenarios"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Cost-optimization-solution-for-basic-cloud-resources-in-cloud-native-scenarios"
---

This article describes the main cost components involved in using BytePlus cloud\-native services, and provides reference solutions for cost management. These recommendations can help reduce costs while benefiting from the rapid business growth enabled by high\-quality cloud services, resulting in a higher return on investment.

<span id=".5oiQ5pys5p6E5oiQ"></span>
## Cost composition

Cloud\-native service costs fall into two categories: infrastructure resources and cloud\-native services. In general usage scenarios, the cost of infrastructure resources accounts for the majority of total costs and is the primary focus during cost optimization.


* Major cloud\-native services include VKE, CR, CP, and AMS.

* Major basic cloud resources include ECS, EIP, EBS, ALB, CLB, FileNAS, and TOS.


<span id=".5LqR5Z-656GA6LWE5rqQ6K6h6LS5"></span>
## Infrastructure resource billing

Use of cloud\-native services involves infrastructure resources, such as elastic computing, networking, storage, and security. These infrastructure resources incur fees based on applicable billing rules. Billing details are as follows:


|Cloud resource |Required |Resource description |Billing description |
|---|---|---|---|
|ECS |Required |Serves as nodes of VKE clusters. |[ECS billing](https://docs.byteplus.com/en/docs/ecs/Instance-type-billing) |
|VPC |Required |Provides cluster networking and routing rules for VKE clusters. |[VPC billing](https://docs.byteplus.com/en/docs/vpc/Billing) |
|Load balancer |Required |Provides load balancing resources for VKE clusters. |[CLB billing](https://docs.byteplus.com/en/docs/clb/Billing-01) |
|ALB |Optional |Provides ALB resources for VKE clusters. |[ALB billing](https://docs.byteplus.com/en/docs/clb/Billing-rules) |
|EIP |Optional |Enables public access over the Internet to a resource. |[EIP billing](https://docs.byteplus.com/en/docs/eip/Billing-overview) |
|NAT Gateway |Optional |Implements Internet communication for cluster nodes. |[NAT Gateway billing](https://docs.byteplus.com/en/docs/natgateway/Billing-overview) |
|CR |Recommended |Creates and manages cloud\-native artifacts throughout the entire lifecycle. |[CR billing](https://docs.byteplus.com/en/docs/cr/billing-overview) |
|VCI |Optional |Seamlessly integrates with VKE, providing Kubernetes orchestration capabilities. |[VCI billing](https://docs.byteplus.com/en/docs/vke/VCI-billing-overview) |
|TLS |Recommended |Collects container logs from clusters. |[TLS billing](https://docs.byteplus.com/en/docs/tls/Billing_items_based_on_pay-by-feature_mode) |
|TOS |Optional |Provides TOS volumes, which are mounted to a specific path within a container. |[TOS billing](https://docs.byteplus.com/en/docs/tos/docs-billing-overview) |
|FileNAS |Optional |Provides persistent storage for containers. Persistent storage is mounted on a container during workload creation. |[FileNAS billing](https://docs.byteplus.com/en/docs/nas/Billing-overview) |
|EBS |Required |Also known as cloud disks, EBS provides storage for operating system files, logs, and day\-to\-day data used by the cluster. |[EBS billing](https://docs.byteplus.com/en/docs/ecs/Volume-billing) |
|VMP |Optional |Monitors cluster resources. |[VMP billing](https://docs.byteplus.com/en/docs/vmp/billing-overview) |


<span id=".5oiQ5pys5LyY5YyW5bu66K6u"></span>
## Cost optimization recommendations

<span id=".5LqR5pyN5Yqh5Zmo"></span>
### ECS

ECS is one of the core infrastructure resources supporting cloud\-native services. You can select suitable ECS instance types, specifications, and billing methods based on specific workload requirements to achieve better service quality and have an optimal return on investment.


* **Type selection optimization**

   ECS provides multiple instance types. Different instance types offer different capabilities and support a wide range of business applications and service scenarios. For example:

   * The general\-purpose instance family offers balanced CPU and memory performance, making it suitable for most web applications.

   * The compute\-optimized series is suitable for websites or web servers with higher compute performance requirements.

   * The memory\-optimized series is designed for memory\-intensive workloads, such as data analysis, distributed caching, high\-performance databases, or in\-memory databases.

   You should choose the appropriate instance type that aligns with your business scenario to optimize costs. For example, if you build a portal website, selecting a general\-purpose or compute\-optimized specification as needed can reduce costs by 30% to 45% compared to a memory\-optimized instance. For more details on specifications and their use cases, see [ECS specifications](https://docs.byteplus.com/en/docs/ecs/Introduction-to-instance-types).

* **Instance specification optimization**

   You can reduce resource waste and lower costs by matching instance specifications to your workloads or releasing idle resources.

   * Properly plan nodes in cloud\-native scenarios. For details, see [Best practices for ECS instance selection](https://docs.byteplus.com/en/docs/vke/ECS-selection-best-practices).

   * Regularly monitor instance resource usage by using BytePlus Cloud Monitor and release idle resources.

   * Use [cluster autoscaling](https://docs.byteplus.com/en/docs/vke/Creating-a-Cluster-Autoscaler) or [VCI](https://docs.byteplus.com/en/docs/vke/What-is-Vital-Container-Instance) to elastically scale resources on demand. This ensures you only pay for what you need while meeting business requirements.

* **Billing method optimization**

   ECS supports two billing methods: pay\-as\-you\-go and subscription. You can choose one based on your usage patterns. The following table provides details about the billing methods.

   
   |Billing method |Description |Documentation |
   |---|---|---|
   |Pay\-as\-you\-go billing |A post\-payment method where resource usage precedes payment. You do not need to purchase a large amount of resources in advance. Instead, you can activate or release resources anytime. |[Pay-as-you-go billing](https://docs.byteplus.com/en/docs/ecs/Pay-as-you-go) |
   |Subscription |A pre\-payment method where payment is made before resource use. You can reserve resources in advance to enjoy greater discounts. This method is best for long\-term usage. |[Subscription](https://docs.byteplus.com/en/docs/ecs/Subscription) |
   

   Costs vary significantly by billing method and usage duration. For example, if the usage duration exceeds 1 year, a yearly subscription saves over 40% compared to pay\-as\-you\-go.

   Based on your business scenarios and usage duration, the following ECS purchase strategies are recommended:

   * If the usage duration is less than 20 days, for example, for short\-term testing, e\-commerce promotions, and short\-term computing projects, use pay\-as\-you\-go.

   * If the usage duration is greater than 20 days but less than 10 months, for example, for game launch testing and operations, use monthly subscriptions.

   * If the usage duration is greater than 10 months, for example, for portal websites and public services, use yearly subscriptions.


<span id=".5YWs572RLWlw"></span>
### EIP

In many cases, EIP costs account for a significant share of total spending and are one of the key infrastructure costs to watch when you use cloud\-native services on BytePlus.


* **Line type cost optimization**

   EIP offers multiple line types, including BGP multipath and carrier\-specific lines. Choose a line type based on your business scenario. For example, if you deploy an internal OA system on BytePlus and the outbound link uses China Telecom, choosing a China Telecom line on BytePlus can maintain the access experience while reducing costs by 64% compared with BGP multipath under the same bandwidth limit.

* **Billing method optimization**

   EIP bandwidth supports two billing methods: pay\-as\-you\-go and subscription. Pay\-as\-you\-go can be billed by bandwidth limit or by actual traffic. Choose a billing method based on your usage scenario and bandwidth utilization. For details on EIP billing, see [EIP billing](https://docs.byteplus.com/en/docs/eip/Billing-overview).

   Details on the billing methods are shown in the following table.

   
   |Billing type |Payment timing |Settlement cycle |Advantages |Recommended scenario |
   |---|---|---|---|---|
   |Pay\-as\-you\-go |Postpayment |Hourly (UTC+8) |You can activate or release resources anytime, without the need to purchase resources in advance. |Short\-term, spiky workloads, such as flash sales. |
   |Subscription |Prepayment |Non\-calendar month |The per\-unit cost is generally lower than pay\-as\-you\-go. |Long\-term, stable workloads. |
   

   Assume that a BGP line with 1 Mbps bandwidth is billed by bandwidth limit at `0.063 USD per hour`, or by actual traffic at `0.8 USD per GB`. The cost is calculated as follows:

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The billing rates above (<code>0.063 USD per hour</code> and <code>0.8 USD per GB</code>) are provided only as examples and do not represent any actual billing rule. For details on EIP, see <a href="https://docs.byteplus.com/en/docs/eip/Billing-overview">EIP billing</a>.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The following calculations are for reference only and may not apply to all scenarios.   </div>
   

    The monthly cost based on the bandwidth limit is calculated using the following formula:

   `0.063 (USD per hour) × 24 (hours) × 30 (days) = 45.36 USD`

   In actual traffic\-based billing, assume that bandwidth utilization is 100%. The monthly traffic for 1 Mbps bandwidth (1 bps = 1/8 Bps)  is calculated using the following formula:

   `1 (Mbps) ÷ 8 × 100% × 60 (seconds) × 60 (minutes) × 24 (hours) × 30 (days) = 324,000 MB. 324,000 ÷ 1024 = 316 GB`

   The monthly cost based on actual traffic billing is:

   `316 (GB) × 0.8 (USD per GB) = 252.8 USD`

   The calculations indicate that when bandwidth utilization exceeds 17.9%, actual traffic\-based billing becomes more expensive than bandwidth limit\-based billing.


<span id=".5by55oCn5Z2X5a2Y5YKo"></span>
### EBS


* **Type selection optimization**

   EBS provides several different types of volumes. For detailed performance differences among different volume specifications, see [EBS volume specifications](https://docs.byteplus.com/en/docs/ecs/Volume-specifications).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">VKE no longer supports creating StorageClasses, PersistentVolumes, or PersistentVolumeClaims for the Performance SSD (PTSSD) type. Existing PTSSD resources are not affected and can still be used until they are deleted.   </div>
   

   The performance of a single ESSD depends on its capacity. A larger capacity indicates higher performance. At low capacities, IOPS performance of ESSD is lower than that of Performance SSD, and there is an upper limit on IOPS.

   If your workload has low IOPS requirements but high capacity needs, we recommend using ESSD\-FlexPL. For the same capacity, it saves approximately 75% of the cost compared to Performance SSD.

* **EBS capacity optimization**

   We recommend that you regularly monitor volume capacity usage, scale storage as needed, and clean up idle volumes to keep EBS usage below 80% of total capacity.


<span id=".5a-56LGh5a2Y5YKo"></span>
### TOS


* **Type selection optimization**

   TOS provides standard storage and infrequent access storage. For more billing details, see [TOS billing](https://docs.byteplus.com/en/docs/tos/docs-billing-overview).

   If you use TOS to store infrequently accessed data that needs to be kept for at least 30 days, such as data backups, you can choose infrequent access storage, which can save about 20% of the capacity cost compared with standard storage with the same capacity.


<span id=".6LSf6L295Z2H6KGh"></span>
### CLB

CLB instances can be divided into private CLB instances and public CLB instances based on usage scenarios. The cost of a private CLB instance is mainly affected by its specification. To save costs, select the appropriate specification based on your needs. For details, see [CLB types and specifications](https://docs.byteplus.com/en/docs/clb/Product-Overview-02). The cost of a public CLB instance is affected by instance specification and public bandwidth fees.

The fees for different types of CLB instances vary. The relevant billing items are shown in the table below.


|Type |Instance fee |Specification fee |Public network fee |
|---|---|---|---|
|Public |✓ |✓ |✓ |
|Private |✓ |✓ |\- |


Compared with private CLB, public CLB includes an additional public network costs in its cost structure. For optimization of public network fees, see the EIP cost optimization section in this topic. This part focuses on cost optimization from the perspective of instance specifications.


* **Instance specification optimization**

   Different specifications have different performance limits. We recommend selecting a specification based on your business size. For detailed specification information, see [Service types and specifications](https://docs.byteplus.com/en/docs/clb/Product-Overview-02). Choosing the right instance specification can effectively reduce costs.

* **Billing method optimization**

   CLB supports two billing types: pay\-as\-you\-go and subscription. The unit price for the same specification varies depending on the billing method. For more CLB billing details, see [Pay-as-you-go](https://docs.byteplus.com/en/docs/clb/Billing-02) and [Subscription](https://docs.byteplus.com/en/docs/clb/Billing-04).

   You can select the appropriate billing method based on the usage duration and usage scenarios. The following recommendations are provided:

   * If the monthly usage duration is less than 540 hours (22.5 days), pay\-as\-you\-go is more cost\-effective.

   * If the monthly usage duration exceeds 540 hours (22.5 days), subscription billing is more cost\-effective than Pay\-as\-you\-go billing.

   * If the usage duration is greater than or equal to 10 months, a yearly subscription is more cost\-effective.
