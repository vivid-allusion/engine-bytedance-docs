---
title: "Product billing"
product: "Milvus for VectorDB"
product_code: "Milvus_for_VectorDB"
source: "https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Product_billing"
---

Milvus for VectorDB has been officially available for sale since November 25, 2025, UTC+8. This topic describes the product billing details of Milvus for VectorDB.

## Billable items

**Dedicated instance**

|Billable item |Billing type |Description |
|---|---|---|
|Service nodes |* Pay\-as\-you\-go<br><br>* Subscription |Charges are based on the node type, node specifications, billing type, and purchase or usage duration selected when you create the Milvus instance. For information about how to create an instance, see [Create an instance](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Create_an_instance). |
|Index node |* Pay\-as\-you\-go<br><br>* Subscription ||
|Compute nodes |* Pay\-as\-you\-go<br><br>* Subscription ||
|Storage space |Pay\-as\-you\-go |After you create an instance, the system automatically creates a TOS bucket to store data and charges hourly based on the actual storage usage. |
|Backup |Pay\-as\-you\-go |After creating a backup, the system charges by the hour based on the actual TOS storage used by the backup; the backup feature itself is free of charge. |

**Serverless instance**

|Billable item |Billing type |Description |
|---|---|---|
|Write vCU |Pay\-as\-you\-go |You are charged hourly for the number of write vCUs used by your Serverless instance. |
|Read vCU ||Charges are calculated hourly based on the number of read vCUs used in the Serverless instance. |
|Storage space ||After you create an instance, the system automatically creates a TOS bucket to store data and charges hourly based on the actual storage usage. |
|Backup ||After creating a backup, the system charges by the hour based on the actual TOS storage used by the backup; the backup feature itself is free of charge. |

**On-Demand instance**

|Billable item |Billing type |Description |
|---|---|---|
|Query CU |Pay\-as\-you\-go |Query CU is billed by the hour based on your use of the On\-Demand edition instance. |
|Index CU ||Currently free of charge. |
|Storage space ||After you create an instance, the system automatically creates a TOS bucket to store data and charges hourly based on the actual storage usage. |

## Billing rules

### Node billing rules

**Dedicated instance**

#### Pricing table

|Mode |Billable item |Specification |Region |Pay\-as\-you\-go (USD/hour/CU) |Subscription (USD/month/CU) |
|---|---|---|---|---|---|
|Default |* Service nodes<br><br>* Index node (Capacity)<br><br>* Compute node (Performance) |1C1G |Asia Pacific (Johor) |0.04872 |23.39 |
|||1C2G ||0.05675 |27.24 |
|||1C4G ||0.0728 |34.94 |
|||1C8G ||0.08971 |43.06 |
||Compute node (Capacity) |1C1G ||0.04786 |22.97 |
|||1C2G ||0.05589 |26.83 |
|||1C4G ||0.07165 |34.39 |
|||1C8G ||0.08828 |42.37 |
|Pooling<br><br>> **tip**<br><br><br>> For pooling function details, see [Index node pooling function introduction](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Introduction_to_index_node_pooling).<br> |* Index node (Capacity)<br><br>* Index node (Performance)<br><br>* Data node (Capacity)<br><br>* Data node (Performance) |\- ||0.1456 |\- |

#### Fee calculation formula

* Node fee in default mode = unit price × CU × number of nodes × usage duration

* Node fee in pooling mode = unit price × cumulative CU × usage duration

> **tip**

* > CU represents the node specification unit. For example, a node with 1 core and 4 GiB has a CU of 1, and a node with 2 cores and 8 GiB has a CU of 2, and so on.

* > Cumulative CU represents the average CU usage weighted by time within the statistical period.

   > For example, within a 1\-hour statistical period:

   * > The CU used from 00:00 to 00:20 is 1

   * > The CU used from 00:20 to 00:40 is 2

   * > The CU used from 00:40 to 01:00 is 3

   > The cumulative CU for this hour is: `1 * 20 / 60 + 2 * 20 / 60 + 3 * 20 / 60 = 2`. You can view the cumulative CU of index node pooling in the **Index pooling usage** metric of instance monitoring. For detailed steps, see [View instance monitoring information](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/View_instance_monitoring_information).

**Serverless instance**

#### Pricing table

|Billable item |Region |Pay\-as\-you\-go (USD/hour/vCU) |
|---|---|---|
|Write vCU |Asia Pacific (Johor) |0.0000038 |
|Read vCU ||0.0000038 |

#### Fee calculation formula

Node fee payable = vCU unit price × vCU consumption for actions

* Write vCU consumption is as follows:

   * Insert: inserting 4 KB data consumes 1 vCU

   * Delete: deleting 1 entity consumes 1 vCU

   * Upsert: equals the vCU consumed by one delete + one insert action

* Read vCU consumption is as follows:

   * The more search or query requests, the higher the vCU consumption

   * The larger the volume of data scanned in a single search or query request, the higher the vCU consumption

   * Amount of data returned in a single search or query request: the larger the amount of data returned, the higher the vCU consumption

   * Each read operation consumes at least 6 vCU

**On-Demand instance**

Pricing table

|Billable item |Region |Pay\-as\-you\-go (USD/hour/CU) |
|---|---|---|
|Query CU |Asia Pacific (Johor) |0.07165 |
|Index CU ||\- |

#### Fee calculation formula

Node fee payable = vCU unit price × vCU consumption for actions

### Storage space billing rules

**Dedicated instance**

**Pricing table**

|Region |Pay\-as\-you\-go (USD/hour/GiB) |
|---|---|
|Asia Pacific (Johor) |0.0000357 |

#### Fee calculation formula

Storage space fee = unit price × instance storage space × usage duration

**Serverless instance**

#### Pricing table

|Region |Pay\-as\-you\-go (USD/hour/GiB) |
|---|---|
|Asia Pacific (Johor) |0.0000357 |

#### Fee calculation formula

Storage space fee = unit price × instance storage space × usage duration

**On-Demand instance**

#### Pricing table

|Region |Pay\-as\-you\-go (USD/hour/GiB) |
|---|---|
|Asia Pacific (Johor) |0.0000357 |

#### Fee calculation formula

Storage space fee = unit price × instance storage space × usage duration

### Backup billing rules

**Dedicated instance**

#### Pricing table

|Region |Pay\-as\-you\-go (USD/hour/GiB) |
|---|---|
|Asia Pacific (Johor) |0.0000357 |

#### Fee calculation formula

Backup fee = unit price × backup Storage space × usage hours

**Serverless instance**

#### Pricing table

|Region |Pay\-as\-you\-go (USD/hour/GiB) |
|---|---|
|Asia Pacific (Johor) |0.0000357 |

#### Fee calculation formula

Backup fee = unit price × backup Storage space × usage hours

**On-Demand instance**

Not applicable.
