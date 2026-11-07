---
title: "API Key Usage Instructions"
product: "Vision AI"
product_code: "byteplus-vision"
source: "https://docs.byteplus.com/en/docs/byteplus-vision/api-key-usage-instructions"
---

API Key Usage Instructions

<span id="iv5avfLr"></span>
## Prerequisites (Must Read)


1. Go to ** ** [Access Key Management ](https://console.byteplus.com/iam/keymanage)to create an API Key and obtain the API Key Secret, which is used to construct the Authorization Header parameter.

2. Check the **Action** field under **Query Parameters** in the API documentation. Retrieve the corresponding request path based on the Action value. Refer to the Request Path Specification for the mapping between Action and request paths.

3. Check the **Body Parameters** and **request examples** in the API documentation. Construct the Body parameters following the parameter descriptions.


<span id="hfo7yPhh"></span>
## Request Instructions


|Name |Value |
|---|---|
|Interface address |**https://openapi.cv.bytepluses.com** |
|HTTP Method |**POST** |


<span id="slfHJnhx"></span>
### Request Path Mapping


|Action |Request Path |Description |
|---|---|---|
|CVSync2AsyncSubmitTask |/api/common/v3/submit_task_v2 |Submit sync\-to\-async task |
|CVSync2AsyncGetResult |/api/common/v3/get_result_v2 |Query sync\-to\-async task |
|CVSubmitTask |/api/common/v3/submit_task |Submit async task |
|CVGetResult |/api/common/v3/get_result |Query async task |
|CVProcess |/api/common/v3/process |Synchronous task |
|CVCancelTask |/api/common/v3/cancel_task |Cancel task |


<span id="4WdaEeYP"></span>
### Header Parameters


|Parameter Name |Value |
|---|---|
|Authorization |Bearer $API_KEY |
|Content\-Type |application/json |


<span id="02lHAJoe"></span>
## Examples

<span id="tPRZsP4d"></span>
### Sync\-to\-Async: Submit Task

```Bash
curl --location --request POST 'https://openapi.cv.bytepluses.com/api/common/v3/submit_task_v2' \
--header 'Authorization: Bearer $API_key' \
--header 'Content-Type: application/json' \
--data-raw '{
 "req_key": "REQUEST_REQ_KEY",
 "prompt": "Thousands of troops and horses"
}'
```


<span id="vfbUcmh5"></span>
### Sync\-to\-Async: Query Task

```Bash
curl --location --request POST 'https://openapi.cv.bytepluses.com/api/common/v3/get_result_v2' \
--header 'Authorization: Bearer $API_key' \
--header 'Content-Type: application/json' \
--data-raw '{
 "req_key": "REQUEST_REQ_KEY",
 "task_id": "task_id returned by the task submission API"
}'
```


<span id="KKCljP2R"></span>
### Async: Submit Task

```Bash
curl --location --request POST 'https://openapi.cv.bytepluses.com/api/common/v3/submit_task' \
--header 'Authorization: Bearer $API_key' \
--header 'Content-Type: application/json' \
--data-raw '{
 "req_key": "REQUEST_REQ_KEY",
 "prompt": "Thousands of troops and horses"
}'
```


<span id="k4ZbKpSG"></span>
### Async: Query Task

```Bash
curl --location --request POST 'https://openapi.cv.bytepluses.com/api/common/v3/get_result' \
--header 'Authorization: Bearer $API_key' \
--header 'Content-Type: application/json' \
--data-raw '{
 "req_key": "REQUEST_REQ_KEY",
 "task_id": "task_id returned by the task submission API"
}'
```


<span id="Y8Paa172"></span>
### Synchronous Task

```Bash
curl --location --request POST 'https://openapi.cv.bytepluses.com/api/common/v3/process' \
--header 'Authorization: Bearer $API_Key' \
--header 'Content-Type: application/json' \
--data-raw '{
 "req_key": "REQUEST_REQ_KEY",
 "prompt": "Thousands of troops and horses"
}'
```


<span id="hKi8nYqe"></span>
### Cancel Task

```Bash
curl --location --request POST 'https://openapi.cv.bytepluses.com/api/common/v3/cancel_task' \
--header 'Authorization: Bearer $API_key' \
--header 'Content-Type: application/json' \
--data-raw '{
 "req_key": "REQUEST_REQ_KEY",
 "task_id": "task_id returned by the task submission API"
}'
```
