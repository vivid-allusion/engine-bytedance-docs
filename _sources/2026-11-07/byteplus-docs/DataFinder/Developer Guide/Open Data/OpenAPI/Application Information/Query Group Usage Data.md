---
title: "Query Group Usage Data"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Query_Group_Usage_Data"
---

<span id="c46204f8"></span>
# Request description

**Path**:`v1/openapi/org/{org_id}/usage`

**Method**：GET

**Content\-type**:application/json

<span id="70fc5fd7"></span>
# Precautions


* Currently, only SaaS\-non\-cloud native supports the use of this OpenAPI.

* When calling this OpenAPI, you need to use the group administrator account AK/SK to call it.


<span id="2762cdc3"></span>
# Call instructions

When using the current interface, if you use the SDK provided by DataFinder to make calls, you need to use

`Bc.data_rangers ("${path}",...)`interface, see more about the API call instructions [Call Method](https://docs.byteplus.com/docs/undefined/6a4ce4148a55b50525119a52). The call example is as follows.

```JSON
res = bc.data_rangers('/openapi/v1/org/**/usage', method='get', params=params, headers=headers)
print(res.content)
```


<span id="3caccbd9"></span>
# Request parameters


* **Path\-parameters**

   
   |**Parameter** |**Type** |**Is it required?**  |**Sample value** |**Describe** |
   |---|---|---|---|---|
   |org_id |int |Yes |12345 |Group ID (Group Number).<br><br><br>* You can use the group administrator account to enter the Group Settings \> Group Information page of the DataFinder console to obtain the group ID.<br><br>* After setting the group ID, you can then use the current interface to query the usage data of all applications under the group. |
   

* **Params**

   
   |**Parameter** |**Type** |**Is it required?**  |**Sample value** |**Describe** |
   |---|---|---|---|---|
   |with_monthly_detail |int |No |1 |Do you need to add monthly details to the usage data of the configuration query?<br><br><br>* 0 (default): does not include month\-level details.<br><br>* 1: With monthly level detailed data. |
   |product_name_list |string |Yes |DataFinder |Configure the product range covered by the usage data of the query, and only support queries:<br><br><br>* DataFinder: Usage data for other DataFinders other than ad monitoring.<br><br>* DataTracer: Usage data for ad monitoring.<br><br><br>Supports simultaneous querying of DataFinder and DataTracer, separated by commas: `DataFinder, DataTracer`. |
   


<span id="4167f1c7"></span>
# Return parameters


|**Parameter name** |**Type** |**Explain** |
|---|---|---|
|code |int |Interface returns status, 200 is successful |
|message |string |The interface returns information, and the default is success when successful. |
|data |object |For details of usage for all applications within the group, please refer to the details of the parameters in the data below. |


Data parameter details are as follows.


|**Parameter name** |**Type** |**Explain** |
|---|---|---|
|product_name |string |The range of products covered by the usage data queried. |
|started_at |string |Contract start time. |
|expired_at |string |Contract end time. |
|data_limit_desc |string |The billing item for the amount used in the contract.<br><br><br>* EVENTS_NUM: effective event volume<br><br>* MTU: Users who have valid events according to SSID caliber statistics.<br><br>* DAU: The number of DAUs. This method is no longer used for billing. This method may exist for a small number of historical users. |
|data_limit |int |The usage limit in the contract. |
|total_amount |int |Cumulative usage of billed items in the current contract. |
|this_amount |int |During the inquiry time, the usage of the billing item in the current month. |
|last_amount |int |During the inquiry time, the usage of the billing item in the previous month. |
|current_time |string |Current time. |
|statistics_time |string |The deadline for statistical data. |
|monthly_detail |object |Monthly usage details, which will show you the usage details of each application on a monthly basis. The usage details include:<br><br><br>* app_id: App ID.<br><br>* app_name: Application name.<br><br>* Amount: The usage data of this app in the current month. |


<span id="d63696bd"></span>
# Request example

```JSON
{
    "with_monthly_detail": 1 
}
```


<span id="611cef6f"></span>
# Back to example

```JSON
{
    "code": 200,
    "message": "success",
    "data": [
        {
            "product_name": "DataFinder",
            "started_at": "2025-06-04",
            "expired_at": "2026-06-04",
            "data_limit_desc": "EVENTS_NUM",
            "data_limit": 200000000,
            "total_amount": 383983760,
            "this_amount": 221001113,
            "last_amount": 162982647,
            "current_time": "2025-08-19 22:47:15",
            "statistics_time": "2025-08-18",
            "monthly_detail": {
                "2025-07": [
                    {
                        "app_id": ****,
                        "app_name": "** Finder",
                        "amount": 82576533
                    },
                    {
                        "app_id": ****,
                        "app_name": "** Ranger",
                        "amount": 5949092
                    }
                ],
                "2025-08": [
                    ...
                ]
            }
        }
    ]
}
```
