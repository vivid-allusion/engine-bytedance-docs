---
title: "Impala uses Proton"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Impala_uses_Proton"
---

<span id="c52a4f1b"></span>
## 1 Note

EMR has supported the Proton SDK since EMR\-3.1.1 (corresponding to Hadoop 3.x). This document describes how to use the Proton SDK in Volcano Engine EMR's Impala to read and write TOS data.

<span id="476fa3b1"></span>
## 2 Authentication configuration

For authentication configuration, refer to: [Documentation for using Proton with Hadoop](https://docs.byteplus.com/docs/E-MapReduce/109384#_1-1-%E8%AE%A4%E8%AF%81%E9%85%8D%E7%BD%AE)

<span id="c8b73629"></span>
## 3 Using TOS

<span id="e521f51e"></span>
### 3.1 Create a TOS table in Impala

When creating an Impala table, set the value of the location field to the TOS address to analyze TOS data. For example:

```SQL
CREATE TABLE `impala_tos_table`(
`id` STRING COMMENT '',
`brand` STRING COMMENT '',
`channel` STRING COMMENT '')
PARTITIONED BY (dt String)
LOCATION
'tos://您的bucket/impala_tos_table/';
```


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e0ea5c6fbc17469b887898f27b6d13e3~tplv-goo7wpa0wc-image.image" width="2302px" /></div>


<span id="90041aa5"></span>
### 3.2 Write to a TOS table in Impala

```SQL
insert into impala_tos_table partition(dt='20240512') values('0', 'brand0', 'channel0');
```


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f6deba7bc3b5413da4ca1b8cade8b4d6~tplv-goo7wpa0wc-image.image" width="3378px" /></div>


<span id="986347aa"></span>
### 3.3 Read from a TOS table in Impala

```SQL
select * from impala_tos_table;
```


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b81b1720d08247bbab6a7dbcf526f5d2~tplv-goo7wpa0wc-image.image" width="2730px" /></div>
