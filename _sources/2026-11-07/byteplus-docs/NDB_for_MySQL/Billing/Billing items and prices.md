---
title: "Billing items and prices"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Billing_items_and_prices"
---

This article describes the billing items and pricing details for NDB for MySQL.

<span id="GkVfJAhf"></span>
## Billing Items


|Billing item |Description |Billing type |
|---|---|---|
|Node specifications |* The cost of the instance computing node specification. Compute nodes include master nodes and read\-only nodes.<br><br>* The cost of computing nodes depends on the node type and usage duration. |* Pay\-as\-you\-go<br><br>* Yearly or monthly subscription |
|Storage space |* The fees for the storage space used by the instance include database table files, index files, log files (undo log, redo log, binlog, slowlog, etc.) and a small amount of system files.<br><br>* The cost of storage space is related to the amount of data and the duration of usage. |* Pay\-as\-you\-go<br><br>* Yearly or monthly subscription |
|Backup space |* The cost of the space occupied by the backup files. Currently, the backup space is free and no fees are charged.<br><br>* The backup space fee is related to the usage and storage duration. |none |


<span id="qM51ykmh"></span>
## Price

<span id="hkKEv0nm"></span>
### Node specifications


|**Specification type** |**Specification code** |vCPU |Memory |Pay\-as\-you\-go（USD/node/hour） |||Subscription (USD/Node/Month) |||
|---|---|---|---|---|---|---|---|---|---|
|||||**China (Hong Kong)**  |**Asia Pacific (Johor)**  |**Asia Pacific (Jakarta)**  |**China (Hong Kong)**  |**Asia Pacific (Johor)**  |**Asia Pacific (Jakarta)**  |
|**Exclusive type** |vedb.mysql.x4.medium |2C |8GiB |0.1545 |0.152 |0.13905 |72.2 |72.2 |70.3 |
||vedb.mysql.x4.large |4C |16GiB |0.53 |0.589 |0.477 |280.25 |280.25 |265.5 |
||vedb.mysql.x8.large |4C |32GiB |0.997 |0.94715 |0.8973 |454.1 |454.1 |430.2 |
||vedb.mysql.x4.xlarge |8C |32GiB |1.063 |1.1685 |0.9567 |559.55 |559.55 |530.1 |
||vedb.mysql.x8.xlarge |8C |64GiB |1.342 |1.4725 |1.2078 |705.85 |705.85 |668.7 |
||vedb.mysql.x4.2xlarge |16C |64GiB |2.451 |2.32845 |2.2059 |1117.2 |1117.2 |1058.4 |
||vedb.mysql.x8.2xlarge |16C |128GiB |2.684 |2.945 |2.4156 |1411.7 |1411.7 |1337.4 |
||vedb.mysql.x4.4xlarge |32C |128GiB |4.903 |4.65785 |4.4127 |2235.35 |2235.35 |2117.7 |
||vedb.mysql.x8.4xlarge |32C |256GiB |5.376 |5.89 |4.8384 |2823.4 |2823.4 |2674.8 |
||vedb.mysql.x8.6xlarge |48C |384GiB |8.5504 |8.835 |7.69536 |4235.1 |4235.1 |4279.68 |
||vedb.mysql.x4.8xlarge |64C |256GiB |9.329 |9.3157 |8.3961 |4470.7 |4470.7 |3510.288 |
||vedb.mysql.x8.8xlarge |64C |512GiB |12.384 |11.7705 |11.1456 |5646.8 |5646.8 |5349.6 |
|**General type** |vedb.mysql.g2.medium |2C |4GiB |0.135 |0.11685 |0.1215 |56.05 |56.05 |58.5 |
||vedb.mysql.g4.medium |2C |8GiB |0.14 |0.1501 |0.126 |72.2 |72.2 |70.3 |
||vedb.mysql.g4.large |4C |16GiB |0.521 |0.53295 |0.4689 |237.5 |274.55 |218.5 |
||vedb.mysql.g4.xlarge |8C |32GiB |1.042 |1.06305 |0.9378 |475 |548.15 |437.95 |
||vedb.mysql.g4.2xlarge |16C |64GiB |2.084 |2.1261 |1.8756 |950 |1096.3 |899.64 |
||vedb.mysql.g8.2xlarge |16C |128GiB |3.185 |3.02575 |2.8665 |1242.296 |1242.296 |1176.912 |
||vedb.mysql.g4.4xlarge |32C |128GiB |4.168 |4.2522 |3.7512 |1900 |2192.6 |1799.28 |


<span id="29oIjhpG"></span>
### Storage space


|**Type** |**Pay\-as\-you\-go (** USD **/GiB/hour)**  |||**Subscription (** USD **/GiB/month)**  |||
|---|---|---|---|---|---|---|
||**China (Hong Kong)**  |**Asia Pacific (Johor)**  |**Asia Pacific (Jakarta)**  |**China (Hong Kong)**  |**Asia Pacific (Johor)**  |**Asia Pacific (Jakarta)**  |
|IOOptimizedStorage |0.00077 |||0.30972067 |||
|IntelligentCompressedStorage |0.0005082 |||0.204415642 |||


<span id="0rdjJjIp"></span>
### Price calculation formula


* **Pay\-as\-you\-go (computing pay\-as\-you\-go + storage pay\-as\-you\-go)** 

   Hourly postpaid price = node specification unit price × number of nodes + storage space unit price × storage space size

* **Yearly or monthly subscription**

   * **Computing yearly or monthly subscription + storage pay\-as\-you\-go**

      Calculate one\-time prepaid price + postpaid storage price = (node specification unit price × number of nodes × number of months) + (storage space unit price × storage space size × total storage usage time (hours))

   * **Computing yearly or monthly subscription + storage yearly or monthly subscription + storage overage pay\-as\-you\-go ** 

      One\-time prepaid price + price for overage storage = ((node specification unit price × number of nodes + storage space unit price × storage space size) × number of months) + (storage Space unit price × overage storage space × total storage usage time (hours))


&nbsp;
