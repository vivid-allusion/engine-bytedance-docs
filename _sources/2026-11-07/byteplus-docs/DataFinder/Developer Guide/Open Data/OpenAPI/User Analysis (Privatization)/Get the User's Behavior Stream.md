---
title: "Get the User's Behavior Stream"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Get_the_Users_Behavior_Stream"
---

<span id="5c467223"></span>
## Request description

**Path**:/openapi/v1/{app_id}/behaviors/flows

**Method**: POST

**Content\-type**: application/json

<span id="08aad187"></span>
## Request parameters

**Body**:


|**Parameter** |**Type** |**Is it required?**  |**Sample value** |**Describe** |
|---|---|---|---|---|
|query_type |string |Yes |user_unique_id |query aperture type |
|query_id |string |Yes |test_1 |Query ID |
|orientation |string |Yes |earlier |Forward or backward query according to timestamp, optional earlier, later |
|timestamp |int |Yes |1674889321177 |13\-Bit millisecond timestamp to query |
|count |int |Yes |1000 |How many actions are queried at a time, the recommended value is 1000, and the maximum support is 5000; |
|current_earliest_timestamp |int |No |null |The timestamp of the earliest known action<br><br><br>* If the parameter is not passed or passed to 0, when searching forward according to timestamp and finding no behavior, it will automatically locate the earliest behavior that the user can query |


<span id="b93212b0"></span>
## Return parameters

**Response**:

```json
{
    "code": 200,
    "message": "success",
    "data": {
        "flow": [
            {
                "server_time": 1674889013,
                "time": 1674889013,
                "event_date": "2023-01-28",
                "event": "event_1",
                "app_name": "bytefinder",
                "app_id": 2174,
                "user": {
                    "user_unique_id": "test_1",
                    "web_id": "",
                    "ssid": "172020d7-2261-47d8-ae0d-5721d4445f79",
                    ...
                },
                "params": {
                    "$is_login": "already logged in",
                    ...
                },
                "items": {},
                "local_time_ms": 1674889013000,
                "event_name": "event_1",
                "repetition_cnt": 1
            }],
        "is_reorientation": false,
        "is_earliest": false,
        "is_latest": false,
        "general_preset_params": [
            "$data_validation_test",
            ...
        ],
        "platform_types": "web"
    }
}
```



|**Field** |**Type** |**Description** |
|---|---|---|
|flow |list |behavioral flow |
|is_reorientation |bool |Whether to automatically redirect to the earliest behavior |
|is_latest |bool |Is it already the latest behavior? |
|is_earliest |bool |Is that the first act? |
|general_preset_params |list |A list of preset properties in the event properties contained in the behavior flow |
|platform_types |str |The terminal type to which the app belongs |


<span id="c45f38c0"></span>
## Request example

`Bc`for the creation of RangersClient, its initialization please refer to [Instructions for use](https://docs.byteplus.com/docs/undefined/6a4ce4148a55b50525119a52#b9a8ccc7) the language SDK provides a similar interface.

Call (Python):

```python
body={
    "query_id": "test_1",
    "query_type": "user_unique_id",
    "count": 1000,
    "orientation": "earlier",
    "timestamp": 1674889321177,
    "current_earliest_timestamp": null
}
res = bc.data_finder('/openapi/v1/12345/behaviors/flow', body=body)
print(res.content)
```


<span id="30f7728c"></span>
## Back to example

Return result:

```python
{
    "code": 200,
    "message": "success",
    "data": {
        "flow": [
            {
                "server_time": 1674889013,
                "time": 1674889013,
                "event_date": "2023-01-28",
                "event": "event_1",
                "app_name": "bytefinder",
                "app_id": 12345,
                "user": {
                    "user_unique_id": "test_1",
                    "web_id": "",
                    "ssid": "172020d7-2261-47d8-ae0d-5721d4445f79",
                    "app_channel": "unknown",
                    "user_register_ts": 1670315402,
                    "device_model": "unknown",
                    "ab_version": [],
                    "network_carrier": "unknown",
                    "app_version": "unknown",
                    "network_type": "unknown",
                    "os_version": "unknown",
                    "os_name": "unknown",
                    "package": "unknown",
                    "loc_province_id": "Hebei",
                    "browser": "unknown",
                    "loc_city_id": Zhangjiakou",
                    "language": "unknown",
                    "resolution": "unknown",
                    "app_language": "unknown",
                    "loc_country_id": "China",
                    "browser_version": "unknown",
                    "user_id": "test_1",
                    "bd_did": "",
                    "brand": "unknown"
                },
                "params": {
                    "$is_login": "already logged in",
                    "error_param_code": 0,
                    "error_count": 128,
                    "error_event_code": 1010006,
                    "error_platform": "Android",
                    "error_param_name": "",
                    "error_sdk_version": "6090690",
                    "error_app_id": 168436,
                    "error_event_name": "bav2b_click"
                },
                "items": {},
                "local_time_ms": 1674889013000,
                "event_name": "data_quality_error_statistics",
                "repetition_cnt": 1
            }],
        "is_reorientation": false,
        "is_earliest": false,
        "is_latest": false,
        "general_preset_params": [
            "$data_validation_test",
            "$event_name",
            "$event_time",
            "$is_first_day",
            "$is_login",
            "$latest_referrer",
            "$latest_referrer_host",
            "$latest_search_keyword",
            "$latest_traffic_source_type",
            "$tr_web_ssid",
            "$user_register_time",
            "__sdk_platform",
            "bddid",
            "event_date",
            "server_time",
            "user_register_ts",
            "user_unique_id",
            "web_id",
            "wechat_unionid",
            "$extra",
            "referer_full_domain",
            "$app_channel",
            "$deeplink_url",
            "$source_platform",
            "app_name",
            "referer_site_name",
            "referer_type",
            "scene",
            "session_duration",
            "title",
            "url",
            "url_full_domain",
            "url_path",
            "visit_from_outside",
            "$is_first_time",
            "$page_duration",
            "$app_version",
            "$cpu",
            "$crash_process",
            "$crash_thread",
            "$detailed_stack",
            "$device_model",
            "$is_backstage",
            "$os_version",
            "$resolution",
            "$rom",
            "$session_duration",
            "$link_type",
            "ssid",
            "error_app_id",
            "error_count",
            "error_event_code",
            "error_event_name",
            "error_param_code",
            "error_param_name",
            "error_platform",
            "error_sdk_version",
            "event_type",
            "message_id",
            "description",
            "message_type",
            "media_id",
            "pic_url",
            "latitude",
            "longitude",
            "precision",
            "location_x",
            "location_y",
            "scale",
            "key",
            "thumb_media_id",
            "content",
            "$inactive",
            "$inline",
            "$source_uuid",
            "$url_query",
            "currency_amount",
            "session_no",
            "session_start_time",
            "$task_unit_id",
            "$target_uuid_list"
        ],
        "platform_types": "web"
    }
}
```
