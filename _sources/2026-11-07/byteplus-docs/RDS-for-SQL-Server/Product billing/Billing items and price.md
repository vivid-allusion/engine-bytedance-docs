---
title: "Billing items and price"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/charge-items-and-price"
---

This topic describes billing items and price details related to RDS for SQL Server.

<span id="billing-items"></span>
## Billing items

RDS for SQL Server billing items include instance specification charges, storage space charges, backup space charges, extranet traffic charges.


|Billing item |Description |
|---|---|
|Node specification |The cost of the primary node specification, the secondary node specification, or the read\-only node specification. The billing methods include pay\-as\-you\-go and subscription. |
|Storage space |The cost of SQL Server instance storage space. The billing methods include pay\-as\-you\-go and subscription. |
|Backup space (optional) |The storage space occupied by the backup files does not incur any charges. |
|Public IP |SQL Server supports applying for a public address and accessing it using a public address. The public network address will be bound to the [public network IP](https://docs.byteplus.com/en/docs/eip/What-is-EIP) (Elastic IP Address, referred to as EIP), and the use of EIP will incur fees. For more information on public IP billing, see [Public IP Billing Overview](https://docs.byteplus.com/en/docs/eip/Billing-overview). |
|Cloud monitoring and billing |If a delivery channel for phone, SMS, or log services is selected when [Creating event rule, Cloud ](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/creating-event-rule)Monitor charges for those delivery channels. For more billing information, see [Product Billing](https://docs.byteplus.com/en/docs/cloudmonitor/What-is-Vitality-Cloud-Monitor). |


<div data-tips="true" data-tips-type="tip">tip</div>


<div data-tips="true" data-tips-type="tip">For information on billing types, see <a href="https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/price-overview">Overview</a>.</div>


<span id="instance-price"></span>
## Instance price

SQL Server instances support High availability edition, Single node edition, and Cluster edition, billed by node specification and storage space.

<span id="master-instance-node-specification"></span>
### Primary instance node specification & price

The pricing for each node specification of the SQL Server primary instance is listed in the table below.

**Standard Edition Specifications**


|**Instance type**<br><br> |**Specification type** |**Node specification**<br><br> |**vCPU**<br><br> |**Memory** |**Pay\-as\-you\-go (** USD **/Hour/Node)**  ||||Subscription (USD/Month/Node) ||||
|---|---|---|---|---|---|---|---|---|---|---|---|---|
||||||**China** ||**Overseas** ||**China** ||**Overseas** ||
||||||**Chinese mainland** |**Hong Kong** |**Jakarta** |**Johor**<br><br> |**Chinese mainland** |**Hong Kong** |**Jakarta** |**Johor** |
|**High availability** |**Exclusive Type II** |rds.mssql.3il.x8.medium.s2 |2 Cores |16GiB |0.89 |1.52 |1.61 |1.34 |429.23 |729.68 |773 |643.84 |
|||rds.mssql.3il.x8.large.s2 |4 Cores |32GiB |1.79 |3.04 |3.22 |2.68 |858.45 |1459.37 |1545 |1287.68 |
|||rds.mssql.3il.x8.xlarge.s2 |8 Cores |64GiB |3.58 |6.08 |6.44 |5.37 |1716.90 |2918.74 |3090 |2575.36 |
|||rds.mssql.3il.x8.2xlarge.s2 |16 Cores |128GiB |7.15 |12.16 |12.88 |10.73 |3433.81 |5837.47 |6181 |5150.71 |
|||rds.mssql.3il.x8.3xlarge.s2 |24 Cores |192GiB |10.73 |18.24 |32.19 |16.1 |5150.71 |8756.21 |15452 |7726.07 |
||**General Type II** |rds.mssql.3il.s2.medium.s2 |2 Cores |4GiB |0.29 |0.49 |0.78 |0.52 |138.67 |235.8 |374 |249.56 |
|||rds.mssql.3il.s2.large.s2 |4 Cores |8GiB |0.58 |0.98 |1.56 |1.04 |277.35 |471.46 |749 |499.25 |
|||rds.mssql.3il.s2.xlarge.s2 |8 Cores |16GiB |1.16 |1.96 |3.12 |2.08 |554.69 |942.92 |1498 |998.5 |
|||rds.mssql.3il.s2.2xlarge.s2 |16 Cores |32GiB |2.31 |3.93 |6.24 |4.16 |1109.38 |1885.98 |2995 |1996.86 |
|||rds.mssql.3il.s4.medium.s2 |2 Cores |8GiB |0.50 |0.84 |1.34 |0.89 |237.73 |404.19 |642 |427.85 |
|||rds.mssql.3il.s4.large.s2 |4 Cores |16GiB |0.99 |1.68 |2.67 |1.78 |475.45 |808.24 |1284 |855.84 |
|||rds.mssql.3il.s4.xlarge.s2 |8 Cores |32GiB |1.98 |3.37 |5.35 |3.57 |950.9 |1616.48 |2567 |1711.68 |
|||rds.mssql.3il.s4.2xlarge.s2 |16 Cores |64GiB |3.96 |6.74 |10.7 |7.13 |1901.8 |3233.09 |5135 |3423.21 |
|**Single node edition** |**Exclusive Type II** |rds.mssql.3il.x8.medium.s1 |2 Cores |16GiB |0.52 |0.88 |0.83 |0.77 |247.63 |420.97 |396 |371.45 |
|||rds.mssql.3il.x8.large.s1 |4 Cores |32GiB |1.03 |1.75 |1.65 |1.55 |495.26 |841.94 |792 |742.89 |
|||rds.mssql.3il.x8.xlarge.s1 |8 Cores |64GiB |2.06 |3.51 |3.3 |3.1 |990.52 |1683.89 |1585 |1485.78 |
|||rds.mssql.3il.x8.2xlarge.s1 |16 Cores |128GiB |4.13 |7.02 |6.6 |6.19 |1981.04 |3367.77 |3170 |2971.56 |
||**General Type II**<br><br> |rds.mssql.3il.s2.medium.s1 |2 Cores |4GB |0.17 |0.29 |0.46 |0.31 |82.54 |140.32 |223 |1981.04 |
|||rds.mssql.3il.s2.large.s1 |4 Cores |8GiB |0.34 |0.58 |0.93 |0.62 |165.09 |280.65 |446 |990.52 |
|||rds.mssql.3il.s2.xlarge.s1 |8 Cores |16GiB |0.69 |1.17 |1.86 |1.24 |330.17 |561.3 |891 |495.26 |
|||rds.mssql.3il.s2.2xlarge.s1 |16 Cores |32GiB |1.38 |2.34 |3.71 |2.48 |660.35 |1122.59 |1783 |247.63 |
|||rds.mssql.3il.s4.medium.s1 |2 Cores |8GiB |0.29 |0.49 |0.77 |0.52 |137.57 |233.87 |371 |1188.63 |
|||rds.mssql.3il.s4.large.s1 |4 Cores |16GiB |0.57 |0.97 |1.55 |1.03 |275.14 |467.75 |743 |594.31 |
|||rds.mssql.3il.s4.xlarge.s1 |8 Cores |32GiB |1.15 |1.95 |3.1 |2.06 |550.29 |935.49 |1486 |297.16 |
|||rds.mssql.3il.s4.2xlarge.s1 |16 Cores |64GiB |2.29 |3.9 |6.19 |4.13 |1100.58 |1870.98 |2972 |148.58 |


<span id="enterprise-edition-specifications"></span>
#### **Enterprise Edition Specifications**


|**Instance type**<br><br> |**Specification type**<br><br> |**Node specification** |**vCPU** |**Memory**<br><br> |**Pay\-as\-you\-go (** USD **/hour/Node)**  ||||Subscription (USD/Month/Node) ||||
|---|---|---|---|---|---|---|---|---|---|---|---|---|
||||||**China **  ||**Overseas **  ||**China **  ||**Overseas **  ||
||||||**Chinese mainland** |**Hong Kong** |Jakarta |**Johor**<br><br> |**Chinese mainland** |**Hong Kong** |Jakarta |**Johor** |
|**Cluster edition** |**Exclusive Type II** |rds.mssql.3il.x8.medium.e2 |2 Cores |16GiB |1.51 |2.57 |2.72 |2.72 |726.38 |1234.85 |1307 |1307.49 |
|||rds.mssql.3il.x8.large.e2 |4 Cores |32GiB |3.03 |5.15 |5.45 |5.45 |1452.76 |2469.7 |2615 |2614.98 |
|||rds.mssql.3il.x8.xlarge.e2 |8 Cores |64GiB |6.05 |10.29 |10.9 |10.9 |2905.53 |4939.4 |5230 |5229.95 |
|||rds.mssql.3il.x8.2xlarge.e2 |16 Cores |128GiB |12.11 |20.58 |21.79 |21.79 |5811.06 |9878.8 |10460 |10459.9 |
|||rds.mssql.3il.x8.4xlarge.e2 |32 Cores |256GiB |24.21 |41.16 |43.58 |43.58 |11622.12 |19757.6 |20920 |20919.81 |
|||rds.mssql.3il.x4.8xlarge.e2 |64 Cores |256GiB |44.02 |74.84 |79.24 |79.24 |21131.12 |35922.9 |38036 |38036.02 |
|**Single node edition** |**General Type II**<br><br> |rds.mssql.3il.s2.medium.e1 |2 Cores |4GiB |0.32 |0.54 |0.79 |0.47 |151.33 |257.26 |378 |226.99 |
|||rds.mssql.3il.s2.large.e1 |4 Cores |8GiB |0.63 |0.97 |1.43 |0.86 |302.66 |467.75 |688 |412.72 |
|||rds.mssql.3il.s2.xlarge.e1 |8 Cores |16GiB |1.26 |1.07 |1.58 |0.95 |605.32 |514.52 |757 |453.99 |
|||rds.mssql.3il.s2.2xlarge.e1 |16 Cores |32GiB |2.52 |1.95 |2.87 |1.72 |1210.64 |935.49 |1376 |825.43 |
|||rds.mssql.3il.s4.medium.e1 |2 Cores |8GiB |0.57 |2.14 |3.15 |1.89 |275.14 |1029.04 |1513 |907.98 |
|||rds.mssql.3il.s4.large.e1 |4 Cores |16GiB |1.15 |3.9 |5.73 |3.44 |550.29 |1870.98 |2751 |1650.87 |
|||rds.mssql.3il.s4.xlarge.e1 |8 Cores |32GiB |2.29 |4.29 |6.31 |3.78 |1100.58 |2058.08 |3027 |1815.96 |
|||rds.mssql.3il.s4.2xlarge.e1 |16 Cores |64GiB |4.59 |7.8 |11.46 |6.88 |2201.16 |3741.97 |5503 |3301.74 |


<span id="web-edition-specifications"></span>
#### **Web Edition Specifications**


|**Instance type** |**Specification type**<br><br> |**Node specification**<br><br> |**vCPU**<br><br> |**Memory**<br><br> |**Pay\-as\-you\-go (** USD **/Hour/Node)**  ||||Subscription (USD/Month/Node) ||||
|---|---|---|---|---|---|---|---|---|---|---|---|---|
||||||**China **  ||**Overseas **  ||**China **  ||**Overseas **  ||
||||||**Chinese mainland** |**Hong Kong** |Jakarta |**Johor**<br><br> |**Chinese mainland** |**Hong Kong** |Jakarta |**Johor** |
|**Single node edition** |**General Type II**<br><br> |rds.mssql.3il.s2.medium.w1 |2 Cores |4GiB |0.07 |0.07 |0.22 |0.07 |35.77 |35.77 |107 |35.77 |
|||rds.mssql.3il.s2.large.w1 |4 Cores |8GiB |0.15 |0.15 |0.45 |0.15 |71.54 |71.54 |215 |71.54 |
|||rds.mssql.3il.s2.xlarge.w1 |8 Cores |16GiB |0.30 |0.3 |0.89 |0.3 |143.08 |143.08 |429 |143.08 |
|||rds.mssql.3il.s2.2xlarge.w1 |16 Cores |32GiB |0.60 |0.6 |1.79 |0.6 |286.15 |286.15 |858 |286.15 |
|||rds.mssql.3il.s4.medium.w1 |2 Cores |8GiB |0.09 |0.09 |0.28 |0.09 |44.02 |44.02 |132 |44.02 |
|||rds.mssql.3il.s4.large.w1 |4 Cores |16GiB |0.18 |0.18 |0.55 |0.18 |88.05 |88.05 |264 |88.05 |
|||rds.mssql.3il.s4.xlarge.w1 |8 Cores |32GiB |0.37 |0.37 |1.1 |0.37 |176.09 |176.09 |528 |176.09 |
|||rds.mssql.3il.s4.2xlarge.w1 |16 Cores |64GiB |0.73 |0.73 |2.2 |0.73 |352.19 |352.19 |1057 |352.19 |


<span id="read-only-instance-specification"></span>
### Read\-only instance specification

The pricing for each node specification of the SQL Server read\-only instance is listed in the table below.


|**Instance type** |**Specification type** |**Node specification**<br><br> |**vCPU** |**Memory**<br><br> |**Pay\-as\-you\-go (** USD **/Hour/Node)**  ||||Subscription (USD/Month/Node) ||||
|---|---|---|---|---|---|---|---|---|---|---|---|---|
||||||**China** ||**Overseas **  ||**China **  ||**Overseas** ||
||||||**Chinese mainland** |**Hong Kong** |Jakarta |**Johor**<br><br> |**Chinese mainland** |**Hong Kong** |Jakarta |**Johor** |
|**Read\-only instance** |**Exclusive Type II** |rds.mssql.3il.x8.medium.ro |2 Cores |16GiB |1.29 |2.19 |1.29 |1.29 |619.08 |1052.43 |619 |619.08 |
|||rds.mssql.3il.x8.large.ro |4 Cores |32GiB |2.58 |4.39 |2.58 |2.58 |1238.15 |2104.86 |1238 |1238.15 |
|||rds.mssql.3il.x8.xlarge.ro |8 Cores |64GiB |5.16 |8.77 |5.16 |5.16 |2476.30 |4209.72 |2476 |2476.3 |
|||rds.mssql.3il.x8.2xlarge.ro |16 Cores |128GiB |9.74 |16.57 |9.74 |9.74 |4677.46 |7951.68 |4677 |4677.46 |
|||rds.mssql.3il.x8.4xlarge.ro |32 Cores |256GiB |19.49 |33.13 |19.49 |19.49 |9354.92 |15903.37 |9355 |9354.92 |
||**General Type II** |rds.mssql.3il.s2.medium.ro |2 Cores |4GiB |0.29 |0.49 |0.29 |0.52 |137.57 |233.87 |138 |247.63 |
|||rds.mssql.3il.s2.large.ro |4 Cores |8GiB |0.57 |0.78 |0.46 |0.83 |275.14 |374.2 |220 |396.21 |
|||rds.mssql.3il.s2.xlarge.ro |8 Cores |16GiB |1.15 |0.97 |0.57 |1.03 |550.29 |467.75 |275 |495.26 |
|||rds.mssql.3il.s2.2xlarge.ro |16 Cores |32GiB |2.29 |1.56 |0.92 |1.65 |1100.58 |748.39 |440 |792.42 |
|||rds.mssql.3il.s4.medium.ro |2 Cores |8GiB |0.46 |1.95 |1.15 |2.06 |220.12 |935.49 |550 |990.52 |
|||rds.mssql.3il.s4.large.ro |4 Cores |16GiB |0.92 |3.12 |1.83 |3.3 |440.23 |1496.79 |880 |1584.83 |
|||rds.mssql.3il.s4.xlarge.ro |8 Cores |32GiB |1.83 |3.9 |2.29 |4.13 |880.46 |1870.98 |1101 |1981.04 |
|||rds.mssql.3il.s4.2xlarge.ro |16 Cores |64GiB |3.67 |6.24 |3.67 |6.6 |1760.93 |2993.58 |1761 |3169.67 |
|||rds.mssql.3il.s4.4xlarge.ro |32 Cores |128GiB |7.34 |12.47 |7.34 |13.21 |3521.85 |5987.15 |3522 |6339.34 |


<span id="storage-space-price"></span>
## Storage space price

The prices of the storage space for SQL Server instances are as shown in the following table.


|Region |Instance type |Pay\-as\-you\-go price<br><br>(USD/GiB/Hour) |Subscripiton<br><br>(USD/GiB/Month) |
|---|---|---|---|
|* China (Beijing)<br><br>* China (Guangzhou)<br><br>* China (Shanghai) |High availability |0.0003 |0.1651 |
||Single node edition |0.0002 |0.0825 |
|* China(Hongkong)<br><br>* Asia Pacific (Johor)<br><br>* Asia Pacific (Jakarta) |High availability |0.0005 |0.2476 |
||Single node edition |0.0003 |0.1238 |


<span id="price-calculation-formula"></span>
## Price calculation formula


* **Subscripiton**


Total price (Yearly/Monthly) = (node specification unit price + storage space unit price × storage space size) × number of months


* **Pay\-as\-you\-go ** 


Per hour price = node specification unit price + storage space unit price × storage space size

<div data-tips="true" data-tips-type="tip">tip</div>


<div data-tips="true" data-tips-type="tip">The billing details will be supported to 6 decimal places. After being aggregated into the billing, 3rd and subsequent decimal places will be erased, and the actual deduction from the account will be deducted in 2 decimal places. For the billing issued before this, the details of the billing shall be subject to the value of 0.01 $ for less than 0.01 $. For more details, see <a href="https://docs.byteplus.com/en/docs/byteplus-platform/docs-having-an-overview-of-bills">Having an overview of bills</a>.</div>


<span id="purchase-example"></span>
## **Purchase example**


|Compatible version |Instance type |Billing type |Usage scenario |Payment due |
|---|---|---|---|---|
|Standard Edition Specifications |High availability |Subscription |Buy a new SQL Server instance with the following configuration:<br><br><br>* Region: China (Shanghai)<br><br>* storage space: 500GiB<br><br>* Specification code: rds.mssql.3il.x8.medium.s2(2 cores, 16 GiB)<br><br>* Duration of purchase: 1 month |429.23USD\*1 + 500GiB\*0.1651USD = 511.78 USD |
|||Pay\-as\-you\-go |Buy a new SQL Server instance with the following configuration:<br><br><br>* Region: China (Shanghai)<br><br>* storage space: 500GiB<br><br>* Specification code: rds.mssql.3il.x8.medium.s2(2 cores, 16 GiB)<br><br>* specification code: rds.mssql.3il.x8.medium.s2<br><br>* Duration of use: 720 hours (30 days) |(0.89USD/hour + 500GiB\*0.0003 USD/hour)\*720 = 748.8 USD |
