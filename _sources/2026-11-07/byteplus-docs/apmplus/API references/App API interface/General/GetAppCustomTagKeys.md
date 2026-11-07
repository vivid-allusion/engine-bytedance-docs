---
title: "GetAppCustomTagKeys"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/GetAppCustomTagKeys"
---

Get custom dimension keys.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable access point based on your business location.


* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=GetAppCustomTagKeys&Version=2022\-10\-12


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |GetAppCustomTagKeys |The API name. The current API name is `GetAppCustomTagKeys`. |
|Version |String |Yes |2022\-10\-12 |The API version. The current API version is `2022-10-12`. |
|aid |Integer |No |123456 |Application ID. |
|start_time |Integer |Yes |1665417600 |Start time. |
|end_time |Integer |Yes |1665504000 |The end time. |
|biz_type |String |Yes |crash |Metric type.<br><br><br>* crash: Crash<br><br>* crash_defend: Crash protection<br><br>* lag: Lag<br><br>* custom_exception: Custom exception<br><br>* battery: Battery metric<br><br>* battery_summary: Power consumption factors<br><br>* battery_trace: Anomaly trend |
|limit |Integer |No |100 |Number of data entries returned. Default: 100. |
|filters |Object of [Condition](https://docs.byteplus.com/en/docs/299/67867#condition) |No |\- |The filter condition. You can specify multiple key‑value pairs to filter data. |


<span id="condition"></span>
### Condition


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|op |String |No |in |The operator.<br><br><br>* gt: greater than<br><br>* gte: greater than or equal to<br><br>* lt: less than<br><br>* lte: less than or equal to<br><br>* eq: equal to<br><br>* neq: not equal to<br><br>* in: contains<br><br>* not_in: does not contain<br><br>* lk: Matches data that fits a specific pattern.<br><br>* nlk: Excludes data that fits a specific pattern. |
|type |String |No |expression |The type of the filter condition.<br><br><br>* expression: The current condition is an expression.<br><br>* and: The current condition is a compound expression, and multiple sub\-conditions are in an AND logical relationship.<br><br>* or: The current condition is a compound expression, and multiple sub\-conditions are in an OR logical relationship.<br><br>* map: The current condition is of map type. |
|value |String |No |123456 |The filter value. |
|values |Array of String |No |[123456] |The filter value. Multiple filter values are supported. |
|map_key |String |No |key_1 |The key of the map type. It is required when the type is set to map. |
|dimension |String |No |aid |The name of the condition. |
|sub_conditions |Array of [Condition](https://docs.byteplus.com/en/docs/299/67867#condition) |No |\- |The sub\-condition. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```JSON
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=GetAppCustomTagKeys&Version=2022-10-12
{
  "aid": 12345,
  "biz_type": "crash",
  "limit": 100,
  "start_time": 1721012400,
  "end_time": 1721098907,
  "filters": {
    "type": "and",
    "sub_conditions": [
      {
        "dimension": "os",
        "op": "in",
        "type": "expression",
        "values": [
          "Android"
        ]
      }
    ]
  }
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|data |Array of [TagKey](https://docs.byteplus.com/en/docs/299/67867#tagkey) |[{"label":"third_id", "value":"3ffffs"}] |Returned key data, at most 100 entries. |
|error_msg |String |success |Error message. |
|error_no |Integer |0 |Error code. 0 indicates success. |


<span id="tagkey"></span>
### TagKey


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|label |String |third_id |The field value. |
|value |String |3ffffs |The display name of the field value. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```JSON
{
  "err_detail": "",
  "data": [
    {
      "label": "HarmonyOS",
      "value": "is_harmony_os"
    },
    {
      "label": "ANR Attribution",
      "value": "anr_key"
    },
    {
      "label": "FD Quantity Greater Than 1000",
      "value": "fd_leak"
    },
    {
      "label": "Successfully Captured logcat",
      "value": "has_logcat"
    },
    {
      "label": "Remaining System Storage Space",
      "value": "inner_free"
    },
    {
      "label": "Remaining Internal Storage Space",
      "value": "inner_free_real"
    },
    {
      "label": "Remaining sdcard Storage Space",
      "value": "sdcard_free"
    },
    {
      "label": "Whether It Is a 64-bit Device",
      "value": "is_64_devices"
    },
    {
      "label": "Whether It Is a 64-bit APK",
      "value": "is_64_runtime"
    },
    {
      "label": "Whether It Is a Rooted Device",
      "value": "is_root"
    },
    {
      "label": "Whether It Is an x86 Device",
      "value": "is_x86_devices"
    },
    {
      "label": "Excessive Java Heap Memory Usage (Greater Than 95%)",
      "value": "java_heap_leak"
    },
    {
      "label": "The Last Activity in onResume State",
      "value": "last_resume_activity"
    },
    {
      "label": "The Thread with the Highest STM Usage",
      "value": "max_stm_thread"
    },
    {
      "label": "The Thread with the Highest UTM Usage",
      "value": "max_utm_thread"
    },
    {
      "label": "Excessive Virtual Memory Usage (2.8G for 32-bit / 3.8G for 64-bit)",
      "value": "memory_leak"
    },
    {
      "label": "Excessive Native Heap Memory Usage (Greater Than 200M)",
      "value": "native_heap_leak"
    },
    {
      "label": "Successfully Captured the FD List",
      "value": "has_fds_file"
    },
    {
      "label": "Successfully Captured the Thread Status List",
      "value": "has_threads_file"
    },
    {
      "label": "Successfully Captured the Process Status",
      "value": "has_meminfo_file"
    },
    {
      "label": "ANR reason",
      "value": "anr_reason"
    },
    {
      "label": "ANR tag",
      "value": "anr_tag"
    },
    {
      "label": "anr_cmsg_wall",
      "value": "anr_cmsg_wall"
    },
    {
      "label": "anr_replace_mainstack",
      "value": "anr_replace_mainstack"
    },
    {
      "label": "anr_step",
      "value": "anr_step"
    },
    {
      "label": "app_tag",
      "value": "app_tag"
    },
    {
      "label": "first_update_launch",
      "value": "first_update_launch"
    },
    {
      "label": "has_envinfo_file",
      "value": "has_envinfo_file"
    },
    {
      "label": "has_malloc_file",
      "value": "has_malloc_file"
    },
    {
      "label": "has_native_stack",
      "value": "has_native_stack"
    },
    {
      "label": "has_pthread_key_file",
      "value": "has_pthread_key_file"
    },
    {
      "label": "has_pthread_key_map_file",
      "value": "has_pthread_key_map_file"
    },
    {
      "label": "has_pthreads_file",
      "value": "has_pthreads_file"
    },
    {
      "label": "has_signal",
      "value": "has_signal"
    },
    {
      "label": "has_view_tree",
      "value": "has_view_tree"
    },
    {
      "label": "input_timeout_type",
      "value": "input_timeout_type"
    },
    {
      "label": "is_current_process",
      "value": "is_current_process"
    },
    {
      "label": "is_hm_os",
      "value": "is_hm_os"
    },
    {
      "label": "kernel_version",
      "value": "kernel_version"
    },
    {
      "label": "key",
      "value": "key"
    },
    {
      "label": "load_0",
      "value": "load_0"
    },
    {
      "label": "load_1",
      "value": "load_1"
    },
    {
      "label": "load_2",
      "value": "load_2"
    },
    {
      "label": "logcat_type",
      "value": "logcat_type"
    },
    {
      "label": "success_end_anrinfo",
      "value": "success_end_anrinfo"
    },
    {
      "label": "version_get_time",
      "value": "version_get_time"
    }
  ],
  "error_msg": "",
  "error_no": 0
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

No error codes are specific to this API. If the API call returns an error code, refer to [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) for troubleshooting.
