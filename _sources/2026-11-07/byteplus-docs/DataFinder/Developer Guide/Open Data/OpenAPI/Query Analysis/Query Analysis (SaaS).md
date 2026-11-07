---
title: "Query Analysis (SaaS)"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Query_Analysis_SaaS"
---

<span id="8b0be8ba"></span>
## Request description


* **Context\-Path**: /datafinder

* **Path**：/openapi/v1/analysis

* **Method**: POST

* **Content\-type**: application/json


<span id="f909c3a8"></span>
## Request parameters


* **Body**:

   * Request parameters are described in query DSL, see [4. DSL structure description](https://docs.byteplus.com/docs/DataFinder/API_Description_and_Public_Parameters_Query_Analysis#8af6aa94).

      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div>
      

      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">The DSL cannot be empty, otherwise this interface cannot be called normally.      </div>
      

   * Data is encoded in UTF\-8.


<span id="06b737e4"></span>
## Return parameters


* **Response**:

   Structure description:

   ```json
   {
       "code": 200, # return code, 200 represents query returned correctly，for non-200, please refer to message in return mesages
       "data": [
           {
               "error_message": null, # wrong messages
               "region_info_map": {}, # mapping of region id during region query
               "trace_id": "6bcbc580ab144afd8b8a792349ed9a5a", # link tracing identifier
               "query_id": "a00:p00:c00:q00", # Sub-query identifier
               "result_status": "SUCCESS", # Sub-query status
               "execute_time": 0, # Sub-query execution time
               "data_item_list": [ # Sub-query return data
                   {
                       "filter_label": null, # filter label
                       "group_by_key": "__all", # group key
                       "data": [ # metric data
                           142099,
                           145940,
                           139035,
                           148457,
                           154313
                       ],
                       "sum_value_square": 106673323444, # Sum of squared indicators
                       "composed_item_key": null,
                       "item_key": "a00:p00:c00:q00:f00_0",
                       "show_name": "active user amount",
                       "sum": 729844, # Sum value of indicators
                       "event_params": {},
                       "filter_value": null,
                       "event_name_alias": "",
                       "prefix_key": "active_user",
                       "avg": 145968.8, # Average value of indicators
                       "result_type_unit": null,
                       "event_show_name": "应用启动", //App start
                       "event_indicator_params": {},
                       "composed_label": null,
                       "show_label": "active_user",
                       "suffix_key": "__all",
                       "origin_profile_params": {},
                       "result_type": "event_users",
                       "attr_value_name": "",
                       "result_type_label": "active user amount",
                       "is_disabled": null,
                       "profile_params": {},
                       "event_label": "active_user",
                       "origin_key": "__all",
                       "event_id": null,
                       "is_compute": null,
                       "name": "active_user, __all",
                       "event_name": "app_launch",
                       "group_by_type": "user_attr"
                   }
               ],
               "error_code": null,
               "date_index_list": [ # The data time index value corresponds one-to-one with the data
                   "20200606",
                   "20200607",
                   "20200608",
                   "20200609",
                   "20200610"
               ]
           }
       ],
       "message": "success" # wrong messages
   }
   ```
   


<span id="3ef80f89"></span>
## Request example

`Bc`for the creation of RangersClient, its initialization please refer to [Instructions for use](https://docs.byteplus.com/docs/undefined/6a4ce4148a55b50525119a52#b9a8ccc7) the language SDK provides a similar interface.

Call (Python):

```python
dsl = {
    "version": 3,
    "app_ids": [164***],
    "use_app_cloud_id": True,
    "periods": [
        {
            "granularity": "day",
            "type": "last",
            "last": {
                "amount": 5,
                "unit": "day"
            },
            "timezone": "Asia/Shanghai"
        }
    ],
    "content": {
            "query_type": "event",
            "profile_groups_v2": [],
            "profile_filters": [],
            "queries": [
                [
                    {
                        "event_type": "origin",
                        "show_name": "active user amount",
                        "event_name": "app_launch",
                        "groups_v2": [],
                        "filters": [],
                        "show_label": "active_user",
                        "event_indicator": "event_users"
                    }
                ]
            ],
            "option": {
                "skip_cache": False
            }
        }
}

# SaaS logic
resp = bc.data_finder("/openapi/v1/analysis", body=dsl)
print(resp.content)
```
