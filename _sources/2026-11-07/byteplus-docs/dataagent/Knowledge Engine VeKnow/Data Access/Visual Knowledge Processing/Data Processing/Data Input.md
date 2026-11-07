---
title: "Data Input"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Data_Input_"
---

<span id="74a9da9e"></span>
# Feature Overview

Data input is the beginning of the user's task of visual knowledge processing. It is necessary to select a certain data connection to obtain data input from the data source, and then you can choose a data cleaning operator or other processing methods.

<span id="e5f99497"></span>
# Operation steps


1. **data entry processing**


Take the data input of a MySQL data connection as an example, push the input dataset into the canvas, and click on the input operator. You can see the data source information, and set the extraction method to filter partitioned and non\-partitioned fields. At present, non\-partitioned field filtering already supports "and" and "or" filtering logic, and users can further freely filter data based on the data source. In addition, you can also set extraction parameters, set the amount of data to preview, and so on.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3f30563a2c984a88a205c60a06f4e627~tplv-goo7wpa0wc-image.image) </span>

After completing the above basic data input processing, users can further choose operators such as data cleaning or feature engineering to achieve a variety of data processing and processing.


2. **Custom SQL**


Visual knowledge processing supports custom SQL for most offline stored data inputs to achieve basic data processing. In the data connection part of the task creation, if the user selects a dataset, it will be displayed in the left canvas: custom SQL (available for offline tasks), visual modeling dataset, Datawind dataset, customer data platform dataset (if the product is purchased and deployed simultaneously). The introduction to custom SQL is as follows:


* **Hive** / **ClickHouse** custom SQL:

   * Hive: Visualize the modeling output and store the data as a Hive type dataset, you can write SQL and meet the Hive syntax

   * ClickHouse: Visualize the modeling output and store the data as a Clickhouse dataset, you can write SQL and meet ClickHouse syntax

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/26de2e80169042ed8dcf26962c0a1239~tplv-goo7wpa0wc-image.image) </span>

   1. **Configuration interface** , visual knowledge processing custom SQL, users can rename, add description, copy and delete operations. Usually when used as the first sub\-node, "execute this node", "execute here", etc. are not supported.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/eaf6820cfd034a839a38d4f095aa5fb5~tplv-goo7wpa0wc-image.image) </span>

   2. (Optional) In the editing area, common function libraries are prepared for you, including function usage instructions, command formats, examples, and more.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f1cd99d982e94af79fdd169e60de65f7~tplv-goo7wpa0wc-image.image) </span>

   3. If the editing has been completed, the user can click on the **preview** to view. Support for setting the number of previews to help users quickly verify SQL logic and improve the accuracy and efficiency of data processing.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6738185a4cda46669299846b9658c1cf~tplv-goo7wpa0wc-image.image) </span>
