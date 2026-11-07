---
title: "Query Report Information in Dashboard"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Query_Report_Information_in_Dashboard"
---

<span id="d1badfc3"></span>
## Request description

**Path**: \*\*\*\* /openapi/v1/{app_id}/dashboards/{dashboard_id}/reports

**Method**: GET

**Content\-type**: application/json

<span id="a175c95f"></span>
## Request parameters

**Path\-parameters**:


|**Parameter** |**Type** |**Is it required?**  |**Sample value** |**Describe** |
|---|---|---|---|---|
|dashboard_id |string |Yes |7017737980265628173 |Dashboard ID |


<span id="22c5ff3a"></span>
## Return parameters

**Response**:

```json
{
    "code":200,
    "data":{
        "7017737980265628173":{
            "available":3,
            "denied":0,
            "layout":Array[3],
            "reports":[
                {
                    "app_id":"164314",
                    "creator":"",
                    "dsls":Array[1],
                    "is_preset":true,
                    "partner_info":{

                    },
                    "partners":[

                    ],
                    "report_id":"7017737978126696967",
                    "report_name":"\u6d3b\u8dc3vs\u65b0\u7528\u6237",
                    "report_type":"event_analysis"
                },
                Object{...},
                Object{...}
            ],
            "total":3
        }
    },
    "message":"success"
}
```


Field meaning description


|Parameter |Type |Sample value |Describe |
|---|---|---|---|
|reports |JSON object array |```JSON```<br>```"reports":[```<br>```                Object{...},```<br>```                Object{...},```<br>```                Object{...}```<br>```            ],```<br> |Multiple report information under Dashboard |
|reports[].dsls |JSON object array |Array[1] |DSL information for the report |
|reports[].report_id |string |7017737978126696967 |ID of the report |
|reports[].report_name |string |\u6d3b\u8dc3vs\u65b0\u7528\u6237 |Name of the report |
|reports[].report_type |string |event_analysis |Report type.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When the returned report_type is rich_text (rich text) or embedded (embedded), the report details are already included in the returned reports [] .dsls information, and there is no need to further query such report details through the report_id.</div><br> |


<span id="edd86e94"></span>
## Request example

`Bc`for the creation of RangersClient, its initialization please refer to [Instructions for use](https://docs.byteplus.com/docs/undefined/6a4ce4148a55b50525119a52#b9a8ccc7)the language SDK provides a similar interface

Call (Python):

```python
# for example, app_id= 164314 dashboard=6737549040994484743
res = bc. data_finder('/openapi/v1/164314/dashboards/6737549040994484743/reports', method='get')
print(res.content)
```


<span id="261ab7d0"></span>
## Back to example

Return result:

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_eab0d4a448e1a1f991ac999124139d8f.png) </span>
