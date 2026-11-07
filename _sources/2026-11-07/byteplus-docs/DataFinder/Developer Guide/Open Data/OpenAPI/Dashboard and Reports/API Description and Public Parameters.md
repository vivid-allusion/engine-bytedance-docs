---
title: "API Description and Public Parameters"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/API_Description_and_Public_Parameters_Dashboard_Reports"
---

<span id="7343f302"></span>
# 1. Overview

This document provides instructions for exporting statistics from BytePlus Growth Analysis.

Exportable statistics include:


* List of user Dashboard boards, all Dashboard boards that users can see, including public and private Dashboard boards.

* Specify the report information in Dashboard;

* Specifies the data for the report.


<span id="d224dd45"></span>
# 2. API public parameters

**Context\-path**: /datafinder

**Path\-parameters**:


|**Parameter** |**Type** |**Is it required?**  |**Sample value** |**Describe** |
|---|---|---|---|---|
|app_id |int |Yes |123456 |App ID |


**Response**:

```json
{
        "code": 200,
        "message": "success"
        "data": xxx
}
```



* Code status code, 200 indicates success, other non\-failures

* Message Success or failure message

* Data result data, refer to the specific API description for the specific structure


<span id="446896a0"></span>
# 3. API List


|API |Explain |
|---|---|
|[Query User Dashboard List](https://docs.byteplus.com/docs/DataFinder/Query_User_Dashboard_List) |Query user dashboard list |
|[Query Dashboard Information](https://docs.byteplus.com/docs/DataFinder/Query_Dashboard_Information) |Query Dashboard information |
|[Query Report Information in Dashboard](https://docs.byteplus.com/docs/DataFinder/Query_Report_Information_in_Dashboard) |Query report information in Dashboard |
|[Query Report Information and Data](https://docs.byteplus.com/docs/DataFinder/Query_Report_Information_and_Data) |Query report information and data |
