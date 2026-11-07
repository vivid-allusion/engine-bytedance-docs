---
title: "Integrate with LAS"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Integrate_with_LAS"
---

<span id="_1-las-formation-介绍"></span>
## LAS overview

LAS is a BytePlus platform service that provides unified metadata and permission management for lakehouse engines, supporting fully managed, semi\-managed, and other forms of big data analytics systems. It is recommended to use LAS as the default metadata management service for EMR Serverless queues.

<span id="_2-las-formation开通"></span>
## LAS activation

<span id="_2-1-las-formation入口"></span>
### LAS entry point


1. You can access the LAS activation entry from the Serverless public queue creation interface by selecting **Metadata configuration \> LAS** and using the quick link "**Go to activate**" provided at the location.

2. You can also use the BytePlus navigation entry to log in to the [LAS console](https://console.byteplus.com/las/region:las+ap-southeast-1/next/home?) and access the LAS entry point.


<span id="_3-las-formation开通"></span>
## LAS activation

<span id="_3-1-针对las新用户"></span>
### For new LAS users

Follow the prompts to enter the product activation page.

<span id="_3-2-针对las老用户"></span>
### For existing LAS users

If you are already using the integrated lakehouse service provided by LAS, contact your administrator to activate it for you.

<span id="_4-服务授权"></span>
## Service authorization

LAS requires users to grant permissions to access user resources, such as TOS, AssumeRole, and more.

<span id="_5-完善默认数据目录"></span>
## Complete the default data catalog

**What is a data catalog?** 

LAS metadata management for data lake construction uses a three\-layer entity structure: Catalog/Database/Table (View, UDF). Each tenant can have multiple catalogs, each catalog can contain multiple databases, and each database can have multiple tables.

**Data catalog use cases?** 

Data catalogs are mainly suitable for scenarios requiring metadata isolation, such as different clusters, business units, or organizational teams. Different catalogs can be bound, and metadata in different catalogs is not visible to each other.

**LAS support for data catalogs?** 

LAS supports both default data catalogs and custom\-created data catalogs.

**LAS default data catalog**

To use LAS, users must first complete the default data catalog and fill in the path information.
