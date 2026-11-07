---
title: "API Description and Public Parameters"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/API_Description_and_Public_Parameters_Usage_Statistics"
---

<span id="7fcaba9f"></span>
# 1. Overview

This document provides application or group\-level, day\-to\-day or month\-to\-month event volume, DAU, and MAU usage statistics.

<span id="825ee9fc"></span>
# 2. API public parameters

**Context\-path**: /datafinder

**Body**:

```json
{
    "org_id": null,
    "app_ids": [164314],
    "start_time": 1643644800, # 2022.February.1st
    "end_time": 1645977600 # 2022.February.28th
}
```



|**Parameter** |**Type** |**Is it required?**  |**Sample value** |**Describe** |
|---|---|---|---|---|
|org_id |Int |org_id and app_ids must have a non\-empty |66 |Group ID |
|app_ids |Array of Int ||123456 |Application ID, support sending multiple |
|start_time |int |Yes |1643644800 |The timestamp of the start time in seconds |
|end_time |int |Yes |1645977600 |The timestamp of the end time, in seconds |


Support direct effect on the group level, such as getting org_id = 66 group level usage statistics:

```plaintext
{
    "org_id": 66,
    "app_ids": [],
    "start_time": 1643644800, # 2022.February.1st
    "end_time": 1645977600 # 2022.February.28th
}
```


**Response**:

```json
{
        "code": 200,
        "data": xxx,
        "message": "success"
}
```



* Code status code, 200 indicates success, other non\-failures

* Message Success or failure message

* Data result data, refer to the specific API description for the specific structure


<span id="8cb00ac6"></span>
# 3. API List


|API |Explain |
|---|---|
|[Monthly Granularity Usage Statistics](https://docs.byteplus.com/docs/DataFinder/Monthly_Granularity_Usage_Statistics) |monthly particle size usage statistics |
|[Daily Granularity Usage Statistics](https://docs.byteplus.com/docs/DataFinder/Daily_Granularity_Usage_Statistics) |Daily particle size usage statistics |
