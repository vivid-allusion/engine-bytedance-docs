---
title: "Lark Base Tables"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Lark_Base_Tables"
---

<span id="_1-概述"></span>
# 1. Overview

To enable the Lark dataset, you must first complete "**2. Basic configuration**" in [Lark Integration](https://docs.byteplus.com/docs/dataagent/Lark_Integration_).

[Lark Base Table](https://www.feishu.cn/hc/en-US/articles/697278684206-get-started-with-base?from_lang=us-EN) is a business management tool based on spreadsheets that enables project management from multiple dimensions and supports various summary views. Therefore, in project management and business management scenarios, you may use Lark base tables instead of Lark Spreadsheet for data recording. Currently, Lark base tables supports integration with datasets for data analysis.

<span id="_2-快速入门"></span>
# 2. Quick start

(1) In the dataset module under data preparation, click "New" \- "New dataset" above the dataset list on the left.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d786b4485e084e408ab79370e7c7c2f9~tplv-goo7wpa0wc-image.image) </span>

(2) Select to connect to "Lark base tables".

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f4a97f8ec2a2444fb850ac9e2a1d3499~tplv-goo7wpa0wc-image.image) </span>

(3) Enter the Lark base tables link and click "OK" to create the data connection.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/14ed4ec55d64444fb0cf3c672d9d944c~tplv-goo7wpa0wc-image.image" width="610px" /></div>


(4) In data connections, locate and click to select the Lark base tables you just connected.

(5) Enter the dataset configuration interface to configure the settings.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/93141a3e43ca402cadd09af1a6744ca0~tplv-goo7wpa0wc-image.image) </span>

For dataset configuration, refer to [Field Configuration](https://docs.byteplus.com/docs/dataagent/Field_Configuration). After saving and creating the dataset, data synchronization will be performed according to the set synchronization frequency. In the Lark base tables dataset, each synchronization will retrieve all data from the corresponding model and write it to the current partition.

<span id="_3-功能介绍"></span>
# 3. Feature introduction

<span id="_3-1-支持字段类型"></span>
## 3.1 Supported field types

Lark base tables supports multiple field formats, including text, single choice, multiple choice, date, person, attachment, and more. These field formats will be mapped when integrating with datasets. Among these, attachment, association, lookup reference, and formula fields are not supported for dataset integration.


|Lark multidimensional table field types |Dataset mapped field types |
|---|---|
|Multiline text |string text |
|Number |double value |
|Single choice |string text |
|Multiple choice |array of strings |
|Date |bigint value (if you need to convert to date format, conversion is required) |
|Checkbox |boolean type, 1 represents 'yes', 0 represents 'no' |
|Person |string text |
|Hyperlink |string text |
|Creation time |bigint value |
|Last updated time |bigint value |
|Created by |string text |
|Modified by |string text |


<span id="_3-2-日期-时间类型字段时区说明"></span>
## 3.2 Time zone instructions for date/time type fields

Date/time fields integrated into datasets remain consistent with the timestamps of date/time fields in Lark base tables.

Specifically, in Lark base tables, the local time is displayed according to the user's local time zone. However, after integrating intelligent data insights to generate a dataset, the corresponding time will be displayed based on the data center where the dataset is located. By default, the time is shown as UTC+8 (original time plus 8 hours), which is typically the default original time zone for Lark multidimensional tables, plus 8 hours, resulting in a time format that matches the China time zone.

> Timestamp: Also known as Unix Timestamp, it is a way to represent date and time as a number.


**Format**: Convert time or text\-type time to a timestamp using toUnixTimestamp(xxx), that is, convert yyyy\-mm\-dd hh:mm:ss to a timestamp.

**Example**:


|Field A |toUnixTimestamp(Field A) |Extension: toDateTime(toUnixTimestamp(Field A)+28800) |
|---|---|---|
|2020\-12\-21 18:00:00 |1608544800 |2020\-12\-22 02:00:00 |


**Extension**: For the converted timestamp, add the timestamp difference of 28800 corresponding to 8 hours to complete the conversion from UTC+0 to UTC+8, then use the toDateTime function to convert it to a more readable time format.

<span id="_3-3-注意事项"></span>
## 3.3 Caution

**Permission and functionality description:** 


* The dataset owner needs to have read permission for Lark multidimensional tables.

* After the user enters a link to a Lark table, all data tables under that table will be imported.

* Table formulas are currently not supported.

* Multiple sheets in a regular Lark table are currently not supported for integration.

* If there are empty rows, they will be counted in the row statistics ([null,null,null,null] format data will be added to the dataset).


**Naming conventions:** 


* When naming Lark documents or table files, please pay attention to naming conventions and try to avoid using the period ('.') in table names and sheet names.

* Column names: When naming column names, please follow naming conventions and use plain text as much as possible. Avoid column names that are purely numeric, images, hyperlinks, and similar types. Avoid naming columns as p_date or including $, `(backtick), ! and other regular expressions. Since the column names captured during synchronization are the column names as originally created, please do not modify them arbitrarily after creating the dataset. Column names must be unique.
