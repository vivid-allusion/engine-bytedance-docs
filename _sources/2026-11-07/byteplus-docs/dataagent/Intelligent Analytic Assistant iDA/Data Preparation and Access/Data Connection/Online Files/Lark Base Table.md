---
title: "Lark Base Table"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Lark_Base_Table__"
---

<span id="2272eedd"></span>
# 1. Overview

To open the Feishu dataset, you need to complete [Lark Integration](https://docs.byteplus.com/docs/dataagent/Lark_Integration_) the "**2. basic configuration**" first.

[Base ](https://www.feishu.cn/hc/en-US/articles/697278684206-get-started-with-base?from_lang=us-EN)is a table\-based business management tool that manages projects from multiple dimensions while also supporting multiple summary views. Therefore, in project management and business management scenarios, you may use Base instead of Feishu tables for data recording. Currently, Base already supports accessing datasets for data analytics.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a19a68f6105e413c9bf6d325be970144~tplv-goo7wpa0wc-image.image) </span>

<span id="64ee3e6b"></span>
# 2. Quick start

(1) In the Dataset module in Data Preparation, click "New" \- "New Dataset" at the top of the dataset list on the left.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b2700dc012b148d59c714846a310b3cc~tplv-goo7wpa0wc-image.image) </span>

(2) Select Connect "Base table".

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/72816033a9644c75afe3ad2818402690~tplv-goo7wpa0wc-image.image" width="600px" /></div>


(3) Enter the Base link and click "Confirm" to create a data connection.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a3c1ef6ccaf64f95a2ce38a41372a554~tplv-goo7wpa0wc-image.image" width="600px" /></div>


(4) In the data connection, find and click to select the Feishu Base that you just connected to.

(5) Enter the dataset configuration interface and configure.

Data set configuration can be referred to [Field Configuration](https://docs.byteplus.com/docs/dataagent/Field_Configuration_). After the dataset is saved and created, the data will be synchronized according to the set synchronization frequency. In the Base dataset, each synchronization fetches the full amount of data in the corresponding model and writes it to the current partition.

<span id="d3ff6886"></span>
# 3. Function introduction

<span id="c878a510"></span>
## 3.1 Supported field types

Base supports a variety of field formats, including text, radio/multi\-select, date, person, attachment, and more. These field formats will be mapped when accessing the dataset. Among them, the attachment, association, lookup reference, and formula fields do not support access to the dataset.


|Base field type |Dataset mapping field type |
|---|---|
|multiline text |String text |
|number |Double value |
|radio |String text |
|multiple choice |Array [string] array |
|date |Bigint value (if you need to convert to date format, you need to convert it) |
|check box |Boolean Boolean type, 1 for'yes', 0 for'no' |
|personnel |String text |
|hyperlinke |String text |
|creation time |BIGINT value |
|Last update time |BIGINT value |
|founder |String text |
|Modifier |String text |


<span id="debd68c3"></span>
## 3.2 Date/Time Type Field Time Zone Description

The date/time field that accesses the dataset is consistent with the timestamp of the date/time field in Base.

Specifically, in Base, the local time will be displayed according to the user's local time zone. However, after accessing Datawind to generate a dataset, the corresponding time will be displayed according to the data set in the computer room, and the default display is UTC + 8 (original time + 8 hours), usually for the default original time zone of Base plus 8 hours, which is displayed as a time format in line with the Chinese time zone.

> Timestamp: Also known as Unix timestamp (Unix Timestamp), it is a way to represent dates and times as numbers.


**Format** : Converts time or text type to timestamp toUnixTimestamp (xxx), i.e. yyy\-mm\-dd hh: mm: ss to timestamp.

**Example** :


|Field A |toUnixTimestamp (field A) |Extension: toDateTime (toUnixTimestamp (field A) + 28800) |
|---|---|---|
|2020\-12\-21 18:00:00 |1608544800 |2020\-12\-22 02:00:00 |


**Extension** : For the converted timestamp, add the timestamp difference of 28800 corresponding to 8 hours to complete the conversion from UTC + 0 to UTC + 8, and then convert it to a more readable time format through the toDateTime function.

<span id="911499fe"></span>
## 3.3 Precautions

**Permissions and function descriptions:** 


* The dataset owner needs to have Base read access.

* After the user fills in a link to a Feishu form, all data tables under that form are imported.

* Table formulas are not currently supported.

* Multiple sheet access in normal Feishu tables is not supported.

* If there are empty rows, they will be included in the row count ([null, null, null, null] format data will be added to the dataset).


**Naming convention:** 


* When naming Feishu documents and table files, please pay attention to the naming convention and try to avoid the English dot '.' in the table name and sheet name.

* Column names: When naming column names, please pay attention to the naming convention, try to be ordinary text, avoid pure numbers, pictures, hyperlinkes and other column names, avoid naming p_date or containing $, ' (backquotes),! Regular expression; since the column name at the time of creation is captured during synchronization, please do not modify it casually after creating the dataset. Column names should be unique values.
