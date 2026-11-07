---
title: "Query Report Information and Data"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Query_Report_Information_and_Data"
---

<span id="9f62b8e6"></span>
## Request description

**Path**：/openapi/v1/{app_id}/reports/{report_id}

**Method**: GET / POST

**Content\-type**: application/json

<span id="c42b8ff9"></span>
## Request parameters

**Path\-parameters**:


|**Parameter** |**Type** |**Is it required?**  |**Sample value** |**Describe** |
|---|---|---|---|---|
|report_id |string |Yes |6761676584756707854 |Report ID |


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">SaaS environments support <strong>SQL custom query</strong> results.</div>


* <div data-tips="true" data-tips-type="warning">When the report type is rich_text (rich text) or embedded (embedded), the report details are already included in reports [] .dsls, and there is no need to use report_id to query the report information and data.</div>



**Query\-parameters**:


|**Parameter** |**Type** |**Is it required?**  |**Sample value** |**Describe** |
|---|---|---|---|---|
|count |int |No |30 |Quantity is limited, maximum support 1000. |
|filter_id |int |No |without |Global filter id, if used this id will ignore global_filter nodes in the body (supported after privatization 4.4) |


**Body:** 

When the Http Method is **POST** , you can use the **body** parameter.

```json
{
    "global_filter": {
        "param_filters": {},
        "profile_filters": [],
        "period": {},
        "property_logic": "and",
        "replace_info": null
    }
}
```


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">When using the report API interface, if the filter param_filters contains a date range, the date range is passed in. However, if "granularity": "month" is set, the data for the current month is automatically completed, for example, the time filter is set to 2024\-01\-01 to 2024\-03\-05, and "granularity": "month" returns data 2024\-01\-01 to 2024\-03\-31.</div>


* <div data-tips="true" data-tips-type="warning">If you want to obtain day\-level data results, you need to use "granularity": "day" with filters to limit the date range.</div>



<span id="058ab9ed"></span>
## Return parameters

**Response**:

```json
{
        "code": 200,
        "message": "success"
        "data":  {
            "dsls": [{
                 "data": [{}],
                 "mp_scene": {},
                 "qr_codes": []
                }
            ],
        }
}
```


Field meaning description


|Parameter |Type |Sample value |Describe |
|---|---|---|---|
|data.dsls[].data |JSON object array |See the return example below. |Information in the report |
|data.dsls[].mp_scene |JSON object |See the return example below. |scene information |
|data.dsls[].qr_codes |array |See the return example below. |QR code information |


<span id="f448fd5b"></span>
## Request example

`Bc`for the creation of RangersClient, its initialization please refer to [Instructions for use](https://docs.byteplus.com/docs/undefined/6a4ce4148a55b50525119a52#b9a8ccc7)the language SDK provides a similar interface

Call (Python):

```python
# for example, app_id= 165108 report_id= 6761676584756707854
res = bc.data_finder('/openapi/v1/165108/reports/{}'.format('6761676584756707854'), method='get', params={"count":30})
print(res.content)
```


<span id="dc1b175e"></span>
## Back to example

Return result:

Data.dsls [] .data is the data in the report

Data.dsls []. mp_scene for scene information

Data.dsls []. qr_codes QR code information

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5f223283556cfd8581c2c7aa8f1edbde.png) </span>

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_69d4d13327450e6432624cb1b7dd62ca.png) </span>

<span id="0081db8f"></span>
## Reference: Get global filter configuration from front\-end configuration

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_406fb3d0b1560bca170f2b4c041e3d56.png) </span>

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_57b9a3a130d1b3c11dabaf1241ce0d2d.png) </span>
