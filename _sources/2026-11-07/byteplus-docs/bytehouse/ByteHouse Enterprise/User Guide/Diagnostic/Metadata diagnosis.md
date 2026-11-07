---
title: "Metadata diagnosis"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/metadata-diagnosis"
---

Metadata diagnosis is used to detect the consistency of table metadata in the current cluster, with diagnostic results updated weekly. You can perform repairs according to the solutions provided by ByteHouse for metadata issues to improve the availability and stability of the cluster. This feature is applicable to scenarios such as troubleshooting the causes of table unavailability, repairing metadata anomalies, and regularly checking instance health. This tutorial describes the issues, impacts, and solutions related to diagnostics supported by meta information diagnostics, as well as how to use meta information diagnostics.

<span id="0371298f"></span>
# Function overview

ByteHouse currently supports diagnosis of the following metadata issues and supports filtering metadata issues of specified clusters and tables.


|**Issue** |**Impact** |**Remediation plan** |**Caution** |
|---|---|---|---|
|The local table and distributed table structures are inconsistent |If not fixed, it may affect the normal query of data. |Rebuild the table. |It is recommended to perform changes during off\-peak business hours. |
|The distributed table does not have a shard key |If not repaired, it will affect write and query performance. |Rebuild the table. |It is recommended to perform changes during off\-peak business hours. |
|UNIQUE KEY contains many fields and does not use hash functions |If not repaired, it will affect write and query performance. |Rebuild the table. |It is recommended to perform changes during off\-peak business hours. |
|The number of indexes in table settings does not match the metadata |If not repaired, an error will occur when querying. |Rebuild the table. |It is recommended to perform changes during off\-peak business hours. |
|The table settings' index property does not match the metadata |If not repaired, an error will occur when querying. |Rebuild the table. |It is recommended to perform changes during off\-peak business hours. |
|The number of fields in the table does not match the metadata |If not repaired, an error will occur when querying. |Rebuild the table. |It is recommended to perform changes during off\-peak business hours. |
|Table name does not match the metadata |If not repaired, an error will occur when querying. |Rebuild the table. |It is recommended to perform changes during off\-peak business hours. |
|Nullable property of table fields does not match the metadata |If not repaired, an error will occur when querying. |Rebuild the table. |It is recommended to perform changes during off\-peak business hours. |


<span id="78aded97"></span>
# Use metadata for diagnostics


1. Log in to the ByteHouse Enterprise console, click the top **Diagnostic** tab, click **Metadata Diag**, and go to the feature page.

2. Select a cluster from the dropdown list, click **Diagnosis**, and the system will automatically analyze and display the diagnostic status of the metadata for all tables in the current cluster.

   Various diagnostic items can be used to assist in diagnosing whether there are anomalies in table metadata within the cluster. They also provide information about the degree of impact of such anomalies, solutions for remediation, and notes for remediation.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/72240dcf913c4ab78bf7160c66402805~tplv-goo7wpa0wc-image.image) </span>

   To view the diagnostic information for a table, enter the table name and click **Diagnosis**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0c7fa01ec8054dff965dc10dfd3a7020~tplv-goo7wpa0wc-image.image) </span>
