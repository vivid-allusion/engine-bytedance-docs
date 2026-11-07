---
title: "Billable items"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/billing-items"
---

This topic introduces the details of the Cloud Search service billable items.

<span id="p3mttmrv"></span>
## Billable item


|**Billable item** |**Description** |
|---|---|
|Instance node specification cost |Provide different performance computing specifications based on supported peak business traffic. Billing type is Subscription or Pay\-as\-you\-go. |
|Kibana node specification cost |Besides the free Kibana node with 1 core and 2 GiB provided in the instance, custom Kibana node specifications are supported. Billing will be based on the new specification and the billing type will be Subscription or Pay\-as\-you\-go. |
|Storage capacity fee |Cloud Search service instance storage space fee. Billing type is subscription or pay\-as\-you\-go. |
|FlexPL bandwidth package fee |When the data node uses the FlexPL storage type and the storage specifications are set to 500 GiB or above, you can purchase bandwidth packages to increase disk bandwidth.<br><br>Turning on bandwidth packages incurs additional fees, with billing types as subscription or pay\-as\-you\-go. |
|TL0 bandwidth package fee |When the data node uses TL0 storage type with storage specifications of 100 GiB or above, you can purchase bandwidth packages to increase disk bandwidth.<br><br>Turning on bandwidth packages incurs additional charges, billed by subscription or pay\-as\-you\-go. |
|Public network bandwidth fee |Enable public network access for instances and visualization tools. The system automatically allocates dedicated bandwidth for public network access based on your configured bandwidth.<br><br>The billing type for public network bandwidth is Subscription or Pay\-as\-you\-go. |
|System default bucket |The system automatically creates a TOS Bucket for storing snapshots and Snapshots can be searched when creating the first snapshot in an instance or transferring snapshots from TOS. The system default Bucket charges based on actual usage. |
|Logstash instance node specification cost |Billing is based on the node specification used to create your Logstash instance. Billing type includes Subscription or Pay\-as\-you\-go. |


<span id="ip3b0i5z"></span>
### Instance specification fees

The billing formula and prices for instance specification fees are as follows.


* **Pay\-as\-you\-go**: instance specification fee = node specification pay\-as\-you\-go unit price × number of nodes × usage duration

* **Subscription**: instance specification fee = node specification subscription unit price × number of nodes × usage duration



|**Specification type** |**vCPU** |**Memory** |* **China (Beijing)** <br><br>* **China (Shanghai)** <br><br>* **China (Guangzhou)**  ||* **China (Hong Kong)** <br><br>* **Asia Pacific (Johor)**  ||<div style="text-align: center"><br><strong>Asia Pacific (Jakarta)</strong></div><br> ||
|---|---|---|---|---|---|---|---|---|
||||**Pay\-as\-you\-go (USD/hour/node)**  |**Monthly subscription (USD/month/node)**  |**Pay\-as\-you\-go (USD/hour/node)**  |**Monthly subscription (USD/month/node)**  |**Pay\-as\-you\-go (USD/hour/node)**  |**Monthly subscription (USD/month/node)**  |
|es.x4.small<br><br>(for testing only, disabled in production) |1 core |4 GiB |0.65 |182.43 |0.51 |242.91 |0.51 |220.05 |
|es.x2.medium |2 cores |4 GiB |0.87 |243.18 |0.67 |323.82 |0.77 |367.21 |
|es.x4.medium |2 cores |8 GiB |1.31 |364.86 |1.01 |485.82 |0.99 |440.11 |
|es.x8.medium |2 cores |16 GiB |1.41 |392.22 |1.27 |590.22 |1.26 |588.61 |
|es.x2.large |4 cores |8 GiB |1.74 |486.36 |1.34 |647.64 |1.54 |768.61 |
|es.x4.large |4 cores |16 GiB |2.61 |729.72 |2.01 |971.64 |2.01 |880.21 |
|es.x8.large |4 cores |32 GiB |2.82 |784.44 |2.54 |1180.44 |2.47 |1134.91 |
|es.x2.xlarge |8 cores |16 GiB |3.48 |972.72 |2.69 |1295.28 |3.02 |1494.91 |
|es.x4.xlarge |8 cores |32 GiB |5.22 |1459.44 |4.03 |1943.28 |3.97 |1723.51 |
|es.x8.xlarge |8 cores |64 GiB |5.64 |1568.88 |5.08 |2360.88 |4.86 |2224.81 |
|es.x1.2xlarge |16 cores |16 GiB |5.23 |1458.72 |5.33 |2535 |5.59 |2615.41 |
|es.x2.2xlarge |16 cores |32 GiB |6.96 |1945.44 |5.38 |2590.56 |6.26 |2970.91 |
|es.x4.2xlarge |16 cores |64 GiB |10.45 |2918.88 |8.06 |3886.56 |7.88 |3409.21 |
|es.x8.2xlarge |16 cores |128 GiB |11.28 |3137.76 |10.16 |4721.76 |9.72 |4449.61 |
|es.x2.2.5xlarge |24 cores |48 GiB |10.44 |2918.16 |8.07 |3885.84 |9.23 |4611.61 |
|es.x4.2.5xlarge |24 cores |96 GiB |15.68 |4378.32 |12.09 |5829.84 |12.04 |5281.21 |
|es.x8.2.5xlarge |24 cores |192 GiB |16.92 |4706.64 |15.24 |7082.64 |14.81 |6809.41 |
|es.x1.3xlarge |32 cores |32 GiB |10.46 |2917.44 |10.68 |5070 |11.18 |5230.81 |
|es.x2.3xlarge |32 cores |64 GiB |13.93 |3890.88 |10.76 |5181.12 |12.47 |5904.91 |
|es.x4.3xlarge |32 cores |128 GiB |20.90 |5837.76 |16.12 |7773.12 |15.75 |6818.41 |
|es.x8.3xlarge |32 cores |256 GiB |22.56 |6275.52 |20.32 |9443.52 |19.44 |8899.21 |
|es.x2.5xlarge |48 cores |96 GiB |20.88 |5836.32 |16.14 |7771.68 |18.78 |8912.73 |
|es.x4.5xlarge |48 cores |192 GiB |31.35 |8756.64 |24.18 |11659.68 |23.64 |10227.63 |
|es.x1.6xlarge |64 cores |64 GiB |20.92 |5834.88 |21.32 |10140 |22.36 |10461.64 |


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">es.x2.5xlarge and es.x4.5xlarge specifications currently support only the North China 2 (Beijing) region.</div>


<span id="U92EMwOB"></span>
### Kibana node billing

In an instance, besides the free 1 core 2 GiB Kibana node, you can customize the Kibana node specifications. Billing will follow the new specifications, based on Subscription or Pay\-as\-you\-go billing types.


* **Pay\-as\-you\-go**: Kibana node fee = node specification pay\-as\-you\-go unit price × number of nodes × usage duration

* **Subscription**: Kibana node fee = node specification monthly unit price × number of nodes × usage duration



|**Specification type** |**vCPU** |**Memory** |* **China (Beijing)** <br><br>* **China (Shanghai)** <br><br>* **China (Guangzhou)**  ||* **China (Hong Kong)** <br><br>* **Asia Pacific (Johor)**  ||<div style="text-align: center"><br><strong>Asia Pacific (Jakarta)</strong></div><br> ||
|---|---|---|---|---|---|---|---|---|
||||**Pay\-as\-you\-go (USD/hour/node)**  |**Monthly subscription (USD/month/node)**  |**Pay\-as\-you\-go (USD/hour/node)**  |**Monthly subscription (USD/month/node)**  |**Pay\-as\-you\-go (USD/hour/node)**  |**Monthly subscription (USD/month/node)**  |
|kibana.x2.small |1 core |2 GiB |Free |Free |Free |Free |Free |Free |
|kibana.x2.medium |2 cores |4 GiB |0.87 |243.18 |0.67 |323.82 |0.77 |367.21 |
|kibana.x4.medium |2 cores |8 GiB |1.31 |364.86 |1.01 |485.82 |0.99 |440.11 |
|kibana.x2.large |4 cores |8 GiB |1.74 |486.36 |1.34 |647.64 |1.54 |768.61 |
|kibana.x4.large |4 cores |16 GiB |2.61 |729.72 |2.01 |971.64 |2.01 |880.21 |
|kibana.x2.xlarge |8 cores |16 GiB |3.48 |972.72 |2.69 |1295.28 |3.02 |1494.91 |
|kibana.x4.xlarge |8 cores |32 GiB |5.22 |1459.44 |4.03 |1943.28 |3.97 |1723.51 |
|kibana.x2.2xlarge |16 cores |32 GiB |6.96 |1945.44 |5.38 |2590.56 |6.26 |2970.91 |
|kibana.x4.2xlarge |16 cores |64 GiB |10.45 |2918.88 |8.06 |3886.56 |7.88 |3409.21 |
|kibana.x2.3xlarge |32 cores |64 GiB |13.93 |3890.88 |10.76 |5181.12 |12.47 |5904.91 |
|kibana.x4.3xlarge |32 cores |128 GiB |20.90 |5837.76 |16.12 |7773.12 |15.75 |6818.41 |


<span id="q09rfaqc"></span>
### Storage capacity fee

The calculation formula and prices for storage capacity fees are as follows.


* **Pay\-as\-you\-go**: storage capacity fee = single node storage capacity × storage capacity pay\-as\-you\-go unit price × number of nodes × usage duration

* **Subscription**: storage capacity fee = single node storage capacity × storage capacity monthly unit price × number of nodes × usage duration



|**Disk type**<br><br><div style="text-align: center"><br> </div><br> |* **China (Beijing)** <br><br>* **China (Shanghai)** <br><br>* **China (Guangzhou)**  ||* **China (Hong Kong)** <br><br>* **Asia Pacific (Johor)**  ||<div style="text-align: center"><br><strong>Asia Pacific (Jakarta)</strong></div><br> ||
|---|---|---|---|---|---|---|
||**Pay\-as\-you\-go (USD/GiB/hour/node)**  |**Subscription (USD/GiB/month/piece)**  |**Pay\-as\-you\-go (USD/GiB/hour/node)**  |**Subscription (USD/GiB/month/piece)**  |**Pay\-as\-you\-go (USD/GiB/hour/node)**  |**Subscription (USD/GiB/month/piece)**  |
|es.volume.essd.pl0 |0.00105 |0.5 |0.00158 |0.75 |0.00149 |0.69 |
|es.volume.essd.flexpl\-standard |0.0021 |1 |0.00315 |1.5 |0.0033 |1.52 |
|es.volume.essd.tl0\-standard |0.00146 |0.7 |0.0022 |1.05 |0.00161 |0.76 |


Storage capacity is calculated in binary, for example, 1 GiB = 1024 MiB.

<span id="WFm0JnLR"></span>
### FlexPL bandwidth package fees

When a data node uses the FlexPL storage type and the storage specification is set to 500 GiB or above, you can purchase a bandwidth package to increase disk bandwidth.

Enabling a bandwidth package incurs additional fees, detailed as follows:


|**Billable item** |* **China (Beijing)** <br><br>* **China (Shanghai)** <br><br>* **China (Guangzhou)**  ||* **China (Hong Kong)** <br><br>* **Asia Pacific (Johor)**  ||**Asia Pacific (Jakarta)**  ||
|---|---|---|---|---|---|---|
||**Pay\-as\-you\-go (USD/MBps/hour)**  |**Subscription (USD/MBps/month)**  |**Pay\-as\-you\-go (USD/MBps/hour)**  |**Subscription (USD/MBps/month)**  |**Pay\-as\-you\-go (USD/MBps/hour)**  |**Subscription (USD/MBps/month)**  |
|es.volume.essd.flexpl\-bandwidth |0.00348 |2.50 |0.00522 |3.75 |0.00547 |3.8 |


<span id="P1h6MDVw"></span>
### TL0 bandwidth package fees

When a data node uses the TL0 storage type and the storage specification is set to 100 GiB or above, you can purchase a bandwidth package to increase disk bandwidth.

Enabling a bandwidth package incurs additional fees, detailed as follows:


|**Billable item** |* **China (Beijing)** <br><br>* **China (Shanghai)** <br><br>* **China (Guangzhou)**  ||* **China (Hong Kong)** <br><br>* **Asia Pacific (Johor)**  ||**Asia Pacific (Jakarta)**  ||
|---|---|---|---|---|---|---|
||**Pay\-as\-you\-go (USD/MBps/hour)**  |**Subscription (USD/MBps/month)**  |**Pay\-as\-you\-go (USD/MBps/hour)**  |**Subscription (USD/MBps/month)**  |**Pay\-as\-you\-go (USD/MBps/hour)**  |**Subscription (USD/MBps/month)**  |
|es.volume.essd.tl0\-bandwidth |0.00244 |1.75 |0.00365 |2.625 |0.00264 |1.89 |


<span id="LZMRZMo6"></span>
### Public network bandwidth fee

Enable public network access for instances and visualization tools. The system automatically allocates dedicated bandwidth for public network access based on your configured bandwidth.

The billing type for public network bandwidth is subscription or pay\-as\-you\-go.

The current public network bandwidth limits for instances are [1, 500] Mbps, and for Kibana/Dashboards are [1, 200] Mbps. If you require higher bandwidth, please [submit a ticket](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000255) to apply.


|**Billable item** |* **China (Beijing)** <br><br>* **China (Shanghai)** <br><br>* **China (Guangzhou)**  ||* **China (Hong Kong)** <br><br>* **Asia Pacific (Johor)**  ||
|---|---|---|---|---|
||**Pay\-as\-you\-go (USD/Mbps/hour)**  |**Subscription (yuan/Mbps/month)**  |**Pay\-as\-you\-go (USD/Mbps/hour)**  |**Subscription (yuan/Mbps/month)**  |
|es.eip.bgp_fixed_bandwidth |* [1, 5] Mbps: 0.063<br><br>* (5, +∞) Mbps: 0.25 |* [1, 2] Mbps: 23<br><br>* (2, 5] Mbps: 25<br><br>* (5, +∞) Mbps: 100 |* [1, 5] Mbps: 0.04<br><br>* (5, +∞) Mbps: 0.14 |* [1, 5] Mbps: 20<br><br>* (5, +∞) Mbps: 80 |


<span id="MmfqjsCX"></span>
### System default bucket fee

When you create a snapshot in an instance for the first time or transfer snapshots from TOS, the system automatically creates a TOS Bucket to store snapshots and searchable snapshots. The system default Bucket charges based on actual usage.


|**Billable item** |* **China (Beijing)** <br><br>* **China (Shanghai)** <br><br>* **China (Guangzhou)**  |* **China (Hong Kong)** <br><br>* **Asia Pacific (Johor)**  |
|---|---|---|
||**Pay\-as\-you\-go (USD/GiB/hour)**  ||
|es.volume.tos.standard |0.000138 |0.000189 |


<span id="gtQJg3oN"></span>
### Logstash instance node specification fees

The billing formula and prices for Logstash instance specifications are as follows.


* **Pay\-as\-you\-go**: Logstash instance specification fee = pay\-as\-you\-go unit price per Logstash node specification × number of nodes × usage duration

* **Subscription**: Instance specification fee = node specification monthly unit price × number of nodes × usage duration



|**Specification type** |**vCPU** |**Memory** |* **China (Beijing)** <br><br>* **China (Shanghai)** <br><br>* **China (Guangzhou)**  ||* **China (Hong Kong)** <br><br>* **Asia Pacific (Johor)**  ||<div style="text-align: center"><br><strong>Asia Pacific (Jakarta)</strong></div><br> ||
|---|---|---|---|---|---|---|---|---|
||||**Pay\-as\-you\-go (USD/hour/node)**  |**Monthly subscription (USD/month/node)**  |**Pay\-as\-you\-go (USD/hour/node)**  |**Monthly subscription (USD/month/node)**  |**Pay\-as\-you\-go (USD/hour/node)**  |**Monthly subscription (USD/month/node)**  |
|ls.x2.medium |2 cores |4 GiB |0.72 |198.20 |0.65 |272.80 |0.71 |337.19 |
|ls.x4.medium |2 cores |8 GiB |1.08 |297.37 |0.97 |409.20 |0.91 |386.26 |
|ls.x8.medium |2 cores |16 GiB |1.27 |353.00 |1.23 |497.23 |0.98 |444.86 |
|ls.x2.large |4 cores |8 GiB |1.44 |396.39 |1.3 |545.60 |1.42 |674.37 |
|ls.x4.large |4 cores |16 GiB |2.15 |594.73 |1.95 |818.40 |1.79 |772.52 |
|ls.x8.large |4 cores |32 GiB |2.54 |706.00 |2.46 |994.46 |1.96 |889.71 |
|ls.x1.xlarge |8 cores |8 GiB |2.36 |656.43 |2.59 |1077.38 |2.25 |1047.72 |
|ls.x2.xlarge |8 cores |16 GiB |2.87 |792.77 |2.6 |1091.2 |2.84 |1348.74 |
|ls.x4.xlarge |8 cores |32 GiB |4.31 |1189.45 |3.9 |1636.8 |3.58 |1545.05 |
|ls.x8.xlarge |8 cores |64 GiB |5.08 |1412 |4.92 |1988.92 |3.92 |1778.49 |
|ls.x1.1.5xlarge |12 cores |12 GiB |3.54 |984.64 |3.89 |1616.07 |3.38 |1572.52 |
|ls.x2.1.5xlarge |12 cores |24 GiB |4.32 |1189.17 |3.9 |1636.8 |4.27 |2023.11 |
|ls.x4.1.5xlarge |12 cores |48 GiB |6.45 |1784.19 |5.85 |2455.2 |5.37 |2317.55 |
|ls.x8.1.5xlarge |12 cores |96 GiB |7.62 |2118 |7.38 |2983.38 |5.89 |2669.14 |
|ls.x1.2xlarge |16 cores |16 GiB |4.71 |1312.85 |5.18 |2154.76 |4.51 |2096.38 |
|ls.x2.2xlarge |16 cores |32 GiB |5.74 |1585.54 |5.21 |2182.4 |5.69 |2689.03 |
|ls.x4.2xlarge |16 cores |64 GiB |8.61 |2378.89 |7.8 |3273.6 |7.17 |3090.19 |
|ls.x8.2xlarge |16 cores |128 GiB |10.16 |2823.99 |9.84 |3977.84 |7.83 |3556.98 |
|ls.x1.2.5xlarge |24 cores |24 GiB |7.07 |1312.85 |7.77 |2154.76 |6.75 |2096.38 |
|ls.x2.2.5xlarge |24 cores |48 GiB |8.61 |1585.54 |7.81 |2182.4 |8.53 |2689.03 |
|ls.x4.2.5xlarge |24 cores |96 GiB |12.92 |2378.89 |11.7 |3273.6 |10.75 |3090.19 |
|ls.x8.2.5xlarge |24 cores |192 GiB |15.23 |2823.99 |14.76 |3977.84 |11.77 |3556.98 |
|ls.x1.3xlarge |32 cores |32 GiB |9.42 |2625.7 |10.36 |4309.52 |9.02 |4192.76 |
|ls.x2.3xlarge |32 cores |64 GiB |11.48 |3171.07 |10.41 |4364.8 |11.38 |5378.06 |
|ls.x4.3xlarge |32 cores |128 GiB |17.22 |4757.78 |15.6 |6547.2 |14.35 |6180.37 |
|ls.x8.3xlarge |32 cores |256 GiB |20.32 |5647.98 |19.68 |7955.68 |15.66 |7113.96 |


<span id="ELS1DvYB"></span>
## Price calculation explanation


* **Pay\-as\-you\-go**

   Instance total fee = instance specification fee + storage capacity fee + Kibana node fee = (node specification hourly unit price + single node storage capacity × capacity hourly unit price) × number of nodes × usage duration + Kibana node specification hourly unit price × usage duration

* **Subscription**

   Instance total fee = instance specification fee + storage capacity fee + Kibana node fee = (node specification monthly unit price + single node storage capacity × capacity monthly unit price) × number of nodes × usage duration + Kibana node specification monthly unit price × usage duration

   If the purchase duration is 1 year or longer, you have a discount. The specific discount is subject to the actual order page in the console.


<span id="Uw0syqyR"></span>
## Billing example

The example prices in this chapter are for reference only. Please refer to the console for the latest prices.

For example, you purchase an Elasticsearch instance in the North China 2 (Beijing) region, with the following instance specifications:


* Node specifications: 3 data nodes, each with 2 cores and 8 GiB memory.

* Kibana node fee: the custom\-configured Kibana node has 2 cores and 4 GiB memory.

* Storage capacity: each node has 100 GiB of storage.


The prices under different billing modes are as follows:


* **Pay\-as\-you\-go**

   If your usage is 1 day, the following fees apply:

   * Node specification fee: 1.31 USD/hour/node × 3 nodes × 24 hours = 94.32 USD

   * Kibana node fee: 0.87 USD/hour/node × 1 node × 24 hours = 20.88 USD

   * Storage capacity fee: 100 GiB × 0.00105 USD/GiB/hour × 3 nodes × 24 hours = 7.56 USD

   * Total cost = node specification fee + Kibana node fee + storage capacity fee = 94.32 USD + 20.88 USD + 7.56 USD = 122.76 USD

* **Subscription**

   If your purchase duration is 1 month, you need to pay the following fees:

   * Node specification fee: 364.86 USD/month/node × 3 nodes × 1 month = 1094.58 USD

   * Kibana node fee: 243.18 USD/month/node × 1 node × 1 month = 243.18 USD

   * Storage capacity fee: 100 GiB × 0.5000 USD/GiB/month × 3 nodes × 1 month = 150 USD

   * Total cost = node specification fee + Kibana node fee + storage capacity fee = 1094.58 USD + 243.18 USD + 150 USD = 1487.76 USD
