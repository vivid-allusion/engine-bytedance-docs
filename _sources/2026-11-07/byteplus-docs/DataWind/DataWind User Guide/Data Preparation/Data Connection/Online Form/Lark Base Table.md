---
title: "Lark Base Table"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Lark_Base_Table"
---

<span id="_1-概述"></span>
# 1. Overview

To enable the Lark dataset, you must first complete [Basic Configuration for Lark Integration](https://docs.byteplus.com/docs/undefined/69c349c050cba904c1f628d9) in “**2. Basic configuration**”.

[Lark Multi-dimensional Spreadsheet](https://www.feishu.cn/hc/en-US/articles/697278684206-get-started-with-base?from_lang=en-EN) is a business management tool based on spreadsheets, allowing you to manage projects from multiple dimensions and supporting various summary views. Therefore, in project management and business management scenarios, you may use Lark Multi\-dimensional Spreadsheet instead of Lark Spreadsheet for data recording. Currently, Lark Multi\-dimensional Spreadsheet supports connecting to datasets for data analysis.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/65716ba4960f4e5cb763f904c036f952~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-快速入门"></span>
# 2. Quick start

(1) In the dataset module under Data Preparation, click “New” \- “New dataset” above the dataset list on the left.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9656a5ed4ef44509dc16dd9163db39c~tplv-goo7wpa0wc-image.image) </span>

(2) Select to connect to “Lark Multi\-dimensional Spreadsheet”.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ff2c74dae5c140f38648b83707ee1b68~tplv-goo7wpa0wc-image.image" width="610px" /></div>


(3) Enter the Lark Multi\-dimensional Spreadsheet link and click “OK” to create the data connection.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b6cd91789a7c43ef837b206426a69e1c~tplv-goo7wpa0wc-image.image" width="610px" /></div>


(4) In Data Connections, find and click to select the Lark Multi\-dimensional Spreadsheet you just connected.

(5) Enter the dataset configuration interface to configure the settings.

For dataset configuration, refer to [Field Configuration](https://docs.byteplus.com/docs/DataWind/110003). After saving and creating the dataset, data synchronization will be performed according to the set synchronization frequency. In the Lark Multi\-dimensional Spreadsheet dataset, each synchronization retrieves all data from the corresponding model and writes it into the current partition.

<span id="_3-功能介绍"></span>
# 3. Feature introduction

<span id="_3-1-支持字段类型"></span>
## 3.1 Supported field types

Lark Multi\-dimensional Spreadsheet supports multiple field formats, including text, single select/multi select, date, person, attachment, and more. These field formats will be mapped when connecting to the dataset. Among them, attachment, association, lookup reference, and formula fields are not supported for dataset connection.


|Lark multi\-dimensional table field type |Dataset mapped field type |
|---|---|
|Multi\-line text |string (text) |
|Number |double (numeric) |
|Single select |string (text) |
|Multi\-select |array[string] (array) |
|Date |bigint (numeric; conversion is required if a date format is needed) |
|Checkbox |boolean (Boolean type, 1 means 'Yes', 0 means 'No') |
|Person |string (text) |
|Hyperlink |string (text) |
|Creation time |bigint (numeric) |
|Last updated time |bigint value |
|Creator |string text |
|Modifier |string text |


<span id="_3-2-日期-时间类型字段时区说明"></span>
## 3.2 Time zone description for date/time type fields

Date/time fields connected to the dataset retain the same timestamp as the date/time fields in Lark Multi\-dimensional Spreadsheet.

Specifically, in Lark Multi\-dimensional Spreadsheet, the local time is displayed according to the user's local time zone. However, after integrating with DataWind to generate a dataset, the corresponding time will be displayed based on the data center where the dataset is located. By default, the time is shown as UTC+8 (original time plus 8 hours), which typically means adding 8 hours to the default original time zone of Lark multi\-dimensional tables, displaying the time in a format consistent with the China time zone.

> Timestamp: Also known as Unix timestamp (Unix Timestamp), it is a way to represent dates and times as numbers.


**Format**: Convert a time or a text\-based time into a timestamp using toUnixTimestamp(xxx), that is, convert yyyy\-mm\-dd hh:mm:ss into a timestamp.

**Example**:


|Field A |toUnixTimestamp(Field A) |Extension: toDateTime(toUnixTimestamp(Field A)+28800) |
|---|---|---|
|2020\-12\-21 18:00:00 |1608544800 |2020\-12\-22 02:00:00 |


**Extension**: For the converted timestamp, add the 8\-hour timestamp offset of 28800 to complete the conversion from UTC+0 to UTC+8, and then use the toDateTime function to convert it into a more readable time format.

<span id="_3-3-注意事项"></span>
## 3.3 Notes

**Permissions and features description:** 


* The dataset owner needs to have read permissions for Lark multi\-dimensional tables.

* After a user enters a link to a Lark table, all data tables under that table will be imported.

* Table formulas are not supported at this time.

* Importing multiple sheets from a standard Lark table is not supported at this time.

* If there are empty rows, they will be counted in the row count ([null,null,null,null] format data will be included in the dataset).


**Naming conventions:** 


* When naming Lark documents or table files, please follow the naming conventions and try to avoid using the English period '.' in table and sheet names.

* Column names: When naming columns, please follow the naming conventions and use plain text as much as possible. Avoid using column names that are purely numeric, images, hyperlinks, or naming columns as p_date or containing $, `(backtick), ! and similar regular expression characters; since the column names captured during synchronization are those at the time of creation, do not modify them arbitrarily after creating the dataset. Column names must be unique.
