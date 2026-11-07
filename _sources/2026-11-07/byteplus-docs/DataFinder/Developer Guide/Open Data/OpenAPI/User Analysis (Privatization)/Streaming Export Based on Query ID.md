---
title: "Streaming Export Based on Query ID"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Streaming_Export_Based_on_Query_ID"
---

<span id="59252eca"></span>
# Request description

**Path**:/openapi/v1/{app_id}/user_analysis/files/<query_id\>

**Method**: GET

**Content\-type**: application/json

<span id="b69cb8d9"></span>
## Request parameters

without

<span id="bef059f3"></span>
## Return parameters

**Response**:

Attention:


1. Response content/type is text/csv; charset = utf\-8

2. Response via streaming


When query_id corresponding query_type is cohort, the response is:

```plain
[cohorts name]:{cohorts name}
[editor]:{editor name}
[cohorts user quantity]:{cohorts quantity}
user ID,stat_standard_id,device_id,web_id
{},{},{},{}
{},{},{},{}
{},{},{},{}
```


When query_id corresponding query_type is analysis, the response is:

```plain
user ID,stat_standard_id,device_id,web_id
{},{},{},{}
{},{},{},{}
{},{},{},{}
```


<span id="e420109d"></span>
## Request example

`Bc`for the creation of RangersClient, its initialization please refer to [Instructions for use](https://docs.byteplus.com/docs/undefined/6a4ce4148a55b50525119a52#b9a8ccc7) the language SDK provides a similar interface.

Call (Python):

```python
res = bc.data_finder('/openapi/v1/12345/user_analysis/files/za9fa417b308a1c8e01')
for content in res.iter_lines():
    print(content.decode("utf-8"))
```


<span id="62710b23"></span>
## Back to example

Return result:

```plain
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
