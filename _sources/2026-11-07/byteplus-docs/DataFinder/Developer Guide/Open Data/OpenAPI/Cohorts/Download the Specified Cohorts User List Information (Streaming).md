---
title: "Download the Specified Cohorts User List Information (Streaming)"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Download_the_Specified_Cohorts_User_List_Information_Streaming"
---

<span id="b36d7b47"></span>
## Request description

**Path**:/openapi/v1/{app_id}/cohorts/{cohort_id}/download

**Method**: GET

**Content\-type**: application/json

<span id="c3b48f6e"></span>
## Request parameters

**Path\-parameters**:


|**Parameter** |**Type** |**Is it required?**  |**Sample value** |**Describe** |
|---|---|---|---|---|
|cohort_id |int |true |1001076 |cluster ID |


<span id="271f1a56"></span>
## Return parameters

**Response**:

Attention:


1. Response content/type is text/csv; charset = utf\-8

2. Response via streaming


```plain
[cohort name]:{cohort name}
[editor]:{editor name}
[cohort user quantity]:{cohort quantity}
user ID,stat_standard_id,device_id,web_id
{},{},{},{}
{},{},{},{}
{},{},{},{}
```


Field meaning description


|**Field** |**Type** |**Description** |
|---|---|---|
|User IDs |string |user ID |
|stat_standard_id |string |Statistical criteria ID |
|device_id |string |Device ID |
|web_id |string |Web ID |


<span id="f903e74d"></span>
## Request example

`Bc`for the creation of RangersClient, its initialization please refer to [Instructions for use](https://docs.byteplus.com/docs/undefined/6a4ce4148a55b50525119a52#b9a8ccc7) the language SDK provides a similar interface.

Call (Python):

```python
# for example, app_id= 164314 cohort id= 1001076

# According to streaming reading, the following operations can be taken:
resp = bc.data_finder("/openapi/v1/164314/cohorts/1001076/download")
for content in resp.iter_lines():
    print(content.decode("utf-8"))
```


<span id="68393c0c"></span>
## Back to example

Return result:

```plain
[cohort name]:cohort_name
[editor]:datarangers
[cohort user quantity]:1064
user ID,stat_standard_id,device_id,web_id
7039603993451071012,ce4f5339-b261-4567-ac87-b9e560ce5f71,0,7039603993451071012
256065,5c188cbd-9066-4c3f-817b-3656ed2d32eb,0,6981656913172432419
270159,619619ce-788e-4058-acf4-82063ca81374,0,7040148471437133327
...
...
...
204677,aa67d722-6af4-41f1-9b0c-e478553a0d4e,0,6981289846937978399
243118,58e53ded-b220-4978-99ac-ee7137210b23,0,6970956560466134558
```
