---
title: "About hot and cold data separation"
product: "Table Storage for HBase"
product_code: "HBase"
source: "https://docs.byteplus.com/en/docs/HBase/About_hot_and_cold_data_separation"
---

Table Storage for HBase supports separate storage of hot and cold data, effectively reducing storage costs through different storage media.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background

With the iteration and widespread application of business, the amount of data in the table continues to increase, but as time goes by, the access frequency of many data will gradually decrease. For example, information such as bills and orders will generally only query data details within the past six months. Even for some monitoring data, when encountering problems, people usually only check the data within the past one or two days, and a large amount of historical data before that will be idle. Therefore, Table Storage for HBase provides different storage modes based on the hot and cold needs of data. The system will archive historical data in the table to cold storage based on the set hot and cold separation time boundary points, thereby reducing storage costs.

<span id=".5Y6f55CG5LuL57uN"></span>
## Principle introduction

HBase provides Capacity storage as a cold storage medium, supporting hot and cold separation of data in a table column family based on the data write time.

When creating an instance, you can choose whether to enable Capacity storage. After enabling it, you can set a cold/hot separation boundary (`COLD_BOUNDARY`) for the data in the table column family when creating a table. The system will judge the data based on the set boundary. Store newly written data in hot storage. As time passes, if the current time \- write time \> the `COLD_BOUNDARY` setting, the data will be archived to cold storage during background compaction. For more information, see [Configure hot and cold data separation](https://docs.byteplus.com/en/docs/HBase/Configure_hot_and_cold_data_separation).

At the same time, the hot and cold separation time boundary points can also be modified, and data can be transferred from hot storage to cold storage, or from cold storage to hot storage.

<span id="R2EKlr0X"></span>
## Billing instructions

Capacity storage is billed in the same manner as hot storage, based on the amount of stored data and storage duration. For pricing details, see [Billing items and prices](https://docs.byteplus.com/en/docs/HBase/Billing_items_and_prices).

<span id="oHWCVZOm"></span>
## How to operate


1. [Enabling Capacity storage](https://docs.byteplus.com/en/docs/HBase/Enabling_Capacity_storage)

2. [Configure hot and cold data separation](https://docs.byteplus.com/en/docs/HBase/Configure_hot_and_cold_data_separation)

3. [Changing the capacity of Capacity storage](https://docs.byteplus.com/en/docs/HBase/Changing_the_capacity_of_Capacity_storage)
