---
title: "Get Results Based on Query ID"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Get_Results_Based_on_Query_ID"
---

<span id="ed9699d1"></span>
# Request description

**Path**:/openapi/v1/{app_id}/user_analysis/queries/<query_id\>

**Method**: GET

**Content\-type**: application/json

<span id="4cf79549"></span>
## Request parameters

without

<span id="b79c3a5d"></span>
## Return parameters

**Response**:

```json
{
    "code": 200,
    "message": "success",
    "data": {
        "query_result": {
            "profiles": [
                {
                    "user_id_type": "user_unique_id",
                    "show_user_id": "278145",
                    "stat_standard_id": "95a3de81-61ce-454e-90f0-7b7b1144c148",
                    "user_id": "278145",
                    "device_id": "9223372036854775807",
                    "web_id": "7049540563264423427",

                }
            ],
            "total": 323,
            "result_length": 323,
            "page": 0,
            "page_size": 1000
        },
        "show_option": {
            "query_type": "analysis",
            "profile_names": [
            ],
            "profile_sort": [],
            "limit": 1000,
            "id_types": [
                "ssid",
                "user_unique_id",
                "device_id",
                "web_id"
            ],
            "analysis": {
                "dsl": {omit}
            }
        }
    }
}
```



|**Field** |**Type** |**Description** |
|---|---|---|
|query_result |object |Query ID of user list |
|query_result.total |int |Total number of user lists |
|query_result.result_length |int |The total number of results for this query is related to the limit, and the maximum is 1000 when the limit is 1000. |
|query_result.profiles |list |The details of the user list, each element in the list represents a user, and returns fields such as user id information and user properties |
|page |int |Page number, default is 0 |
|page_size |int |The number of paginated pages, the default is 20, cannot exceed the query limit, up to 1000 |
|show_option |object |Returns the basic information when the query_id was created |


<span id="26d472c6"></span>
## Request example

`Bc`for the creation of RangersClient, its initialization please refer to [Instructions for use](https://docs.byteplus.com/docs/undefined/6a4ce4148a55b50525119a52#b9a8ccc7) the language SDK provides a similar interface.

Call (Python):

```python
res = bc.data_finder('/openapi/v1/12345/user_analysis/queries/za9fa417b308a1c8e01')
print(res.content)
```


<span id="75fc2f36"></span>
## Back to example

Return result:

```json
{
    "code": 200,
    "message": "success",
    "data": {
        "query_result": {
            "profiles": [
                {
                    "user_id_type": "user_unique_id",
                    "show_user_id": "278145",
                    "stat_standard_id": "95a3de81-61ce-454e-90f0-7b7b1144c148",
                    "user_id": "278145",
                    "device_id": "9223372036854775807",
                    "web_id": "7049540563264423427",

                }
            ],
            "total": 323,
            "result_length": 323,
            "page": 0,
            "page_size": 1000
        },
        "show_option": {
            "query_type": "analysis",
            "profile_names": [
            ],
            "profile_sort": [],
            "limit": 1000,
            "id_types": [
                "ssid",
                "user_unique_id",
                "device_id",
                "web_id"
            ],
            "analysis": {
                "dsl": {omit}
            }
        }
    }
}
```
