---
title: "Table statistics"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/table-statistics"
---

ByteHouse supports collecting statistical information on tables within the cluster, helping you to view and analyze table information in the cluster, allowing you to take optimization measures based on this information. This tutorial introduces how to configure collection strategies and view table statistics through visual methods.

<span id="620990a4"></span>
## Function Overview

Table statistics support the following functions.


|Function Items |Description |
|---|---|
|Collection information |The system will collect the following information:<br><br><br>* Data column<br><br>* Column type<br><br>* Column cardinality<br><br>* Number of null values<br><br>* Minimum and maximum values of this column<br><br>* Number of distinct values |
|Collection type |Supports all and sampling collection.<br><br><br>* All collection: Scan the entire table and collect real statistical values.<br><br>* Sampling collection: Uniformly extract N rows of data from each partition of the table to calculate statistical information. |
|Resource utilization |Collecting table statistics will occupy cluster performance. It is suggested to perform this operation during off\-peak hours to avoid impacting business operations. |


<span id="9657e9d3"></span>
## Create collection strategy


1. Log in to the ByteHouse Console, go through **Diagnostic** \>**Table statistics** path to enter the table statistics page, and under the collection strategy tab, click **Create collection strategy**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8c90c6307fc345f49e3f7c8647e0a2d5~tplv-goo7wpa0wc-image.image) </span>

2. On the Create collection strategy page, fill in the basic information for the strategy, select the collection target, and set the collection window.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9ffb9fa5e3094b8d964421a442bffc9f~tplv-goo7wpa0wc-image.image) </span>

   
   |Parameter |Parameter description |
   |---|---|
   |Strategy name |Supports custom strategy names. |
   |Cluster |Select the cluster for which you want to collect statistics. |
   |Collection type |Select total collection or sampling collection. |
   |Collection range |Select whether to collect statistics based on the table or the database. |
   |Database |Select the database for which you want to collect statistics. |
   |Table |Select the table for collecting statistical information. |
   |Collection window |Select the time frame for executing data collection.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">Data collection will occupy Cluster resources; it is advised to perform operations during off\-peak periods to avoid business impact.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">Only one data collection window is supported under the same cluster; the collection strategy will be activated at the next data collection window after editing is complete.</div><br> |
   

3. Click **OK**. The system automatically creates a collection strategy.

4. You can view created collection strategies in the collection strategy list. You can view specific strategies by selecting a cluster or entering a strategy name in the search box.


<span id="53076875"></span>
## Edit collection strategy


1. Log into ByteHouse Console, under the **Diagnostic** tab, go to the **Table statistics** page, click the **Collection strategy** tab, and click the **Edit** button in the actions column.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2700405c79f24cb6885c057c8836635f~tplv-goo7wpa0wc-image.image) </span>

2. On the edit collection strategy page, modify the collection type, object, and collection window.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0e599623803a4836a56e59ee8c0d21d2~tplv-goo7wpa0wc-image.image) </span>

3. Click **OK**. The system automatically updates the collection strategy.


<span id="ece4930d"></span>
## View information query


1. Log into ByteHouse Console, under the **Diagnostic** tab, enter the **Table statistics** page, and click the **Information query** tab.

2. In the search bar, select the cluster, database, and table you want to search for.

3. The system will show specific statistical information for the designated table based on specified information.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/09506bdb6e4d4bb68b5492b86f509f26~tplv-goo7wpa0wc-image.image) </span>
