---
title: "AI Effects Template - OpenAPI"
product: "BytePlus Kickart"
product_code: "kickart"
source: "https://docs.byteplus.com/en/docs/kickart/OpenAPI"
---

1. # Overview <span id="GnCqy2Mh"></span>


This document serves as the official access guide for the Byteplus\-Kickart\-AI effects Template consumption OpenAPI. It aims to assist developers in quickly and efficiently integrating and using the AI effects capabilities provided by the platform, such as stylized image\-to\-image and image\-to\-video, through API interfaces. 


2. # Quick Start <span id="CqgHSZ7m"></span>


You can complete your first API call in just two steps: 


1. **Apply for API Key**: Obtain the API Key for OpenAPI requests in the [BytePlus-Kickart Console](https://console.byteplus.com/kickart/setting/api-key).

2. **Invoke the API**: Follow the instructions in this document to construct an HTTP request, authenticate using the API Key, and initiate the API call.

3. # Domain Name <span id="J7LGaTb5"></span>


**Domain Name: ** [https://kickart.bytepluses.com](https://kickart.bytepluses.com)


4. # API Key Application <span id="n68T26SD"></span>

1. Please log in to[ the BytePlus-Kickart homepage ](https://console.byteplus.com/kickart). 

2. Navigate to the [kickart-apikey Application Page](http://console.byteplus.com/kickart/settings). 



|<div style="text-align: center"><br><img src="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260330143044-900033040642.png" width="210px" /></div><br><br><br><div style="text-align: center"><br>Create ApiKey</div><br> |<div style="text-align: center"><br><img src="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260330143118-1590178532082.png" width="312px" /></div><br><br><br><div style="text-align: center"><br>View and manage ApiKey</div><br> |
|---|---|



3. Select the  **「API Key」**  module in the left menu bar, then click the  **「+New」**  button.

4. After entering the API Key name, click the  **「Create」**  button to complete the creation. 

5. After successful creation, you will receive an API Key. Please keep this key safe, as it will serve as the sole credential for all your API calls.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Permission Instructions: Before calling the API, please ensure that your account has been granted access permissions for the relevant services. If you encounter permission issues during the call, please contact your enterprise administrator or BytePlus business representative.</div>



* ## **Authentication Method** <span id="n3HRC1KX"></span>


All API interfaces adopt the Bearer Token authentication scheme based on HTTP Header. You need to include the `Authorization` and `Content-Type` fields in the Header of each request.


|**Header** |**Description** |
|---|---|
|`Authorization` |Authentication credentials. The format must be `Bearer {API_KEY}`, where `{API_KEY}` needs to be replaced with the actual API Key you obtained from the BytePlus\-Kickart platform.<br><br>**Example**: `Bearer 1jkdislxdsldjgeouqllsj8ko8gssccx` |
|`Content-Type` |Content type of the request body. The fixed value is application/json.  |



---




5. # **Interface Description** <span id="sdxgcYnz"></span>

1. ### **Submit an asynchronous task** <span id="9A3XdxkD"></span>


This interface is used to submit an asynchronous processing task for an AI Effects Template. After a successful call, a task ID (`task_id`) will be immediately returned, which you can use to query the execution status and final result of the task. 


* **Request Method:**  `POST`

* **Request Path: ** `/openapi/ai_effect/submit`


<span id="0fvrozCf"></span>
### **Request Parameters**


|**Field Name** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|`template_id` |`string` |Yes |`"1001"`<br><br> |Template ID to be used. Please obtain it from the response of the "Get Template List" API. |
|`payload` |`json`<br><br> |Yes  |Please refer to the example below<br><br> |**JSON Object**: A data structure used to transmit the specific parameters required for template rendering. The structure is described below." |
|`callback_url`<br><br> |`string`<br><br> |No  |Public network callback address for task results. <br><br> |When the task is completed (whether successfully or unsuccessfully), the system will send a POST request to this URL to notify you of the result.<br><br>&nbsp;<br><br>The callback result is the response parameter of the query. |


<span id="JdYN4d6s"></span>
### **`payload`** ** Structure ** 


|**Field Name** |**Type** |**Required** |**Description** |
|---|---|---|---|
|`resource_list` |`array<string>`<br><br> |&nbsp;<br><br>No  |List of original media asset URLs to be processed. Supports publicly accessible image URLs or Base64 Data URIs of images. To ensure the stability and speed of requests, it is strongly recommended to use **Data URI** format. |
|`resolution` |`string`<br><br> |&nbsp;<br><br>No <br><br> |Specify the resolution of the output work, for example `"480p" "720p" "1080p"`For supported values, please refer to the `resolutions` field returned by the "Get Template List" API. If left blank, the default resolution of the template will be used.<br><br>**Note:**  Some templates (template_id) only support fixed resolutions. Please check the template details page for more information." |


<span id="dZISF0qj"></span>
### **Response Parameter**


|**Field Name** |**Type** |**Description** |
|---|---|---|
|`code` |`int32` |Status code.`0` indicates that the task has been successfully submitted. A non\-`0` value indicates submission failure, with the reason provided in the `message` field. |
|`message` |`string` |Status description information. |
|`request_id` |`string` |The Unique Identifier of this request, which can be used for troubleshooting issues.  |
|`data` |`object` |A data object containing the task ID. The structure is  **`{"task_id": "..."}`**  |


<span id="kQv9maPY"></span>
### **Example of cURL Request**

```Bash
curl --location 'https://kickart.bytepluses.com/openapi/ai_effect/submit' \
--header 'Authorization: Bearer {API_KEY}' \
--header 'Content-Type: application/json' \
--data '{
    "template_id": "1690784258",
    "callback_url": "https://{YOUR_PUBLIC_DOMAIN}/{PATH_CAN_RESPONSE_POST_REQUEST}",
    "payload": {
        "resolution": "1080p",
        "resource_list": [
            "https://lf-iccloud-muse.volcmusecdn.com/obj/labcv-tob/gmy_test/AI.jpg"
        ]
    }
}'
```


<span id="8UNYbdvA"></span>
### **Response Example (Success)** 

```JSON
{
    "code": 0,
    "data": {
        "task_id": "7621886649043206198" //It serves as an input parameter for query tasks and can also wait for a callback.
    },
    "message": "success",
    "request_id": "20260330132131910C619A3D2F5FF87656"
}
```


<span id="0tu3y0Ou"></span>
### **Response Example (Failure)** 

```JSON
{
    "code": 1410, // Please refer to Section 5.3 General Error Codes.
    "data": {},
    "message": "template_id not exist",
    "request_id": "202603301322133EB7BAD7D1B156F75CF7"
}
```


<span id="CMFQbl4A"></span>
### **Code Example**


|python |node |golang |
|---|---|---|
|```Python```<br>```import requests```<br>```import json```<br>``````<br>```API_KEY = "your_api_key_here"```<br>```TEMPLATE_ID = "your_template_id_here"```<br>```RESOURCE_LIST = ["your_resource_url_1", "your_resource_url_2"]```<br>```CALLBACK_URL = None```<br>```RESOLUTION = None```<br>``````<br>```BASE_URL = "https://kickart.bytepluses.com"```<br>``````<br>```headers = {```<br>```    "Authorization": f"Bearer {API_KEY}",```<br>```    "Content-Type": "application/json"```<br>```}```<br>``````<br>```url = f"{BASE_URL}/openapi/ai_effect/submit"```<br>``````<br>```payload = {```<br>```    "resource_list": RESOURCE_LIST```<br>```}```<br>```if RESOLUTION:```<br>```    payload["resolution"] = RESOLUTION```<br>``````<br>```data = {```<br>```    "template_id": TEMPLATE_ID,```<br>```    "payload": payload```<br>```}```<br>```if CALLBACK_URL:```<br>```    data["callback_url"] = CALLBACK_URL```<br>``````<br>```try:```<br>```    response = requests.post(url, headers=headers, data=json.dumps(data))```<br>```    response.raise_for_status()```<br>```    result = response.json()```<br>```    ```<br>```    if result.get("code") == 0 and result.get("data"):```<br>```        task_id = result["data"]["task_id"]```<br>```    else:```<br>```        print(f"submit task failed: {result.get('message', 'Unknown error')}")```<br>``````<br>```except requests.exceptions.RequestException as e:```<br>```    print(f"error: {e}")```<br>```except Exception as e:```<br>```    print(f"error: {e}")```<br>```    ```<br> |```JavaScript```<br>```const BASE_URL = 'https://kickart.bytepluses.com';```<br>``````<br>```const API_KEY = 'YOUR_API_KEY';```<br>```const TEMPLATE_ID = 'YOUR_TEMPLATE_ID';```<br>```const RESOURCE_LIST = ['resource_url_1', 'resource_url_2'];```<br>```const RESOLUTION = '1080p';```<br>```const CALLBACK_URL = 'https://your-domain.com/callback';```<br>``````<br>```async function submitTask() {```<br>```  const url = `${BASE_URL}/openapi/ai_effect/submit`;```<br>```  ```<br>```  const requestBody = {```<br>```    template_id: TEMPLATE_ID,```<br>```    payload: {```<br>```      resource_list: RESOURCE_LIST,```<br>```      resolution: RESOLUTION```<br>```    },```<br>```    callback_url: CALLBACK_URL```<br>```  };```<br>``````<br>```  try {```<br>```    const response = await fetch(url, {```<br>```      method: 'POST',```<br>```      headers: {```<br>```        'Authorization': `Bearer ${API_KEY}`,```<br>```        'Content-Type': 'application/json'```<br>```      },```<br>```      body: JSON.stringify(requestBody)```<br>```    });```<br>``````<br>```    if (!response.ok) {```<br>```      throw new Error(`HTTP error! status: ${response.status}`);```<br>```    }```<br>``````<br>```    const result = await response.json();```<br>```    ```<br>```    return result;```<br>```  } catch (error) {```<br>```    console.error('error:', error);```<br>```    throw error;```<br>```  }```<br>```}```<br>``````<br>```submitTask();```<br>``````<br> |```Go```<br>```package main```<br>``````<br>```import (```<br>```        "bytes"```<br>```        "encoding/json"```<br>```        "fmt"```<br>```        "io"```<br>```        "net/http"```<br>```        "time"```<br>```)```<br>``````<br>```func SubmitTask() {```<br>```        const (```<br>```                apiKey      = "YOUR_API_KEY"```<br>```                templateID  = "YOUR_TEMPLATE_ID"```<br>```                callbackURL = "YOUR_CALLBACK_URL"```<br>```                resolution  = "1080p"```<br>```        )```<br>``````<br>```        resourceList := []string{"resource_url_1", "resource_url_2"}```<br>``````<br>```        requestBody := map[string]interface{}{```<br>```                "template_id": templateID,```<br>```                "payload": map[string]interface{}{```<br>```                        "resource_list": resourceList,```<br>```                        "resolution":    resolution,```<br>```                },```<br>```                "callback_url": callbackURL,```<br>```        }```<br>``````<br>```        body, err := json.Marshal(requestBody)```<br>```        if err != nil {```<br>```                return```<br>```        }```<br>``````<br>```        url := "https://kickart.bytepluses.com/openapi/ai_effect/submit"```<br>```        req, err := http.NewRequest("POST", url, bytes.NewReader(body))```<br>```        if err != nil {```<br>```                return```<br>```        }```<br>``````<br>```        req.Header.Set("Authorization", "Bearer "+apiKey)```<br>```        req.Header.Set("Content-Type", "application/json")```<br>``````<br>```        client := &http.Client{```<br>```                Timeout: 30 * time.Second,```<br>```        }```<br>``````<br>```        resp, err := client.Do(req)```<br>```        if err != nil {```<br>```                return```<br>```        }```<br>```        defer resp.Body.Close()```<br>``````<br>```        respBody, err := io.ReadAll(resp.Body)```<br>```        if err != nil {```<br>```                return```<br>```        }```<br>``````<br>```        var response map[string]interface{}```<br>```        if err := json.Unmarshal(respBody, &response); err != nil {```<br>```                return```<br>```        }```<br>``````<br>```        if data, ok := response["data"].(map[string]interface{}); ok {```<br>```                fmt.Printf("task_id: %s\n", data["task_id"])```<br>```        }```<br>```        fmt.Printf("response: %s\n", string(respBody))```<br>```}```<br>``````<br> |


```JSON
{
  "code": 0,
  "message": "success",
  "request_id": "2024031211223301017205503512345678",
  "data": {
    "task_id": "7573967600885514303"
  }
}

```



2. ### **Query task results** <span id="VzFGhSDU"></span>


After submitting an asynchronous task, you can use this interface and task_id to poll the task's execution status, processing progress, and final results (such as the generated image or video URL).


* **Request Method**: `POST`

* **Request Path**: `/openapi/ai_effect/query`

* **Timeout**: 3600 seconds


<span id="Cl4qBptc"></span>
### **Request Parameter**


|**Field Name** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|`task_id` |`string` |Yes  |`"7573967600885514303"` |The task ID to be queried, which is sourced from the successful response of the "Submit Asynchronous Task" interface.  |


<span id="Cf4IcPSs"></span>
### **Response Parameter**

The  `code`  field in the response body indicates the current status of the task. You need to rely on this field to determine whether the task is still in progress, has succeeded, or has failed. 


|**Field Name** |**Type** |**Description** |
|---|---|---|
|`code`<br><br> |`i32`<br><br> |Task status code. Key values include:<br><br><br>* `0`: Task execution succeeded.<br><br>* `1000`: The task is still running.<br><br><br>Other non\-zero values indicate task failure. For specific meanings, please refer to the "Error Code Explanation" section.  |
|`message` |`string` |Text description of the task status. For example "`Success`" or `"AsyncTaskRunning"`. |
|`request_id` |`string` |The Unique Identifier for this request.  |
|`data` |`object` |Object containing task details, see below `QueryData` structure. |


<span id="srvImmWu"></span>
### **queryData**


|**Field Name** |**Type** |**Description** |
|---|---|---|
|`task_id` |`string` |Unique ID of the task |
|`usage` |`double` |The number of creation points consumed in this task, and it is only valid when the task is successful  |
|`payload` |`json` |Task Details |


<span id="qtMEOMHS"></span>
### **payload**

Task result details. Result fields may vary for different task types; the following fields are common to all results.


|**Field Name** |**Type** |**Description** |
|---|---|---|
|`result_url` |`string` |`Task Result URL` |


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true"><strong>Regarding the validity period of </strong><strong><code>result_url</code></strong></div>


<div data-tips="true" data-tips-type="warning"><strong>Please note that the </strong><code>result_url</code> returned in the response has a validity period, and we guarantee its availability within <strong>24 hours</strong>. To avoid resource expiration, please download the required files as soon as possible after obtaining the URL.</div>


<span id="5eTC8XTI"></span>
### **cURL Request Example**

```Bash
curl --location 'https://kickart.bytepluses.com/openapi/ai_effect/query' \
--header 'Authorization: Bearer {API_KEY}' \
--header 'Content-Type: application/json' \
--data '{
    "task_id": "7620360162389278779"
}'
```


<span id="Y69Zxgz9"></span>
### **Response Example (Task Success)** 

```JSON
{
     "code": 0,
     "data": {
          "payload": {
               "result_url": "https://lf16-river-service-sign.creative-agent-cdn.com/obj/river-service-asiasebd/tmp/7865e9bf-35a5-4775-89cd-f323499efa54.mp4?x-expires=1773802681&x-signature=WqtrjGoK3IE6i6G1a6t0ChToEUw%3D",
               "produce_id": "xx",
               "any_key": "value1"
          },
          "task_id": "7617833350455099399",
          "usage": 0.36
     },
     "message": "success",
     "request_id": "202603171105302BE4CA2F5B03C331AEBD"
}
```


<span id="vjrjFh2Q"></span>
### **Response Example (Task in Progress)** 

```JSON
{
    "code": 1000,
    "data": {
        "task_id": "7618132941507395592"
    },
    "message": "running",
    "request_id": "20260317183056FA38F2B3914E1A517D02"
}
```


<span id="bOkZaUX3"></span>
### **Response Example (Task Fail)** 

```JSON
{
    "code": 1413,
    "data": {
        "task_id": "7618132941507395594"
    },
    "message": "ResourceDownloaderError:Failed to get resource, status: 404",
    "request_id": "202603171842504BE68774F527685BBBC0"
}
```


<span id="XAXecj9g"></span>
### **Code Example**


|python |node |golang |
|---|---|---|
|```Python```<br>``` import requests```<br>```import json```<br>``````<br>```BASE_URL = "https://kickart.bytepluses.com"```<br>```API_KEY = "YOUR_API_KEY"```<br>```TASK_ID = "YOUR_TASK_ID"```<br>``````<br>```def query_task():```<br>```    url = f"{BASE_URL}/openapi/ai_effect/query"```<br>```    ```<br>```    headers = {```<br>```        "Authorization": f"Bearer {API_KEY}",```<br>```        "Content-Type": "application/json"```<br>```    }```<br>```    ```<br>```    data = {```<br>```        "task_id": TASK_ID```<br>```    }```<br>```    ```<br>```    try:```<br>```        response = requests.post(url, headers=headers, data=json.dumps(data))```<br>```        response.raise_for_status()```<br>```        ```<br>```        result = response.json()```<br>```        print(json.dumps(result, indent=2, ensure_ascii=False))```<br>```        ```<br>```        if result.get("code") == 0:```<br>```            print(f"task id: {result.get('data', {}).get('task_id')}")```<br>```            if result.get('data', {}).get('usage') is not None:```<br>```                print(f"usage: {result['data']['usage']:.2f}")```<br>```            if result.get('data', {}).get('payload'):```<br>```                print("result payload:")```<br>```                print(json.dumps(result['data']['payload'], indent=2, ensure_ascii=False))```<br>```        else:```<br>```            print(f"\nquery failed: {result.get('message')}")```<br>```            ```<br>```    except requests.exceptions.RequestException as e:```<br>```        print(f"error: {e}")```<br>```    except Exception as e:```<br>```        print(f"error: {e}")```<br>``````<br>```if __name__ == "__main__":```<br>```    query_task()```<br>```    ```<br>```     ```<br> |```JavaScript```<br>```const BASE_URL = 'https://kickart.bytepluses.com';```<br>```const API_KEY = 'YOUR_API_KEY';```<br>```const TASK_ID = 'YOUR_TASK_ID';```<br>``````<br>```async function queryTask() {```<br>```  const url = `${BASE_URL}/openapi/ai_effect/query`;```<br>```  const requestBody = {```<br>```    task_id: TASK_ID```<br>```  };```<br>``````<br>```  try {```<br>```    const response = await fetch(url, {```<br>```      method: 'POST',```<br>```      headers: {```<br>```        'Authorization': `Bearer ${API_KEY}`,```<br>```        'Content-Type': 'application/json'```<br>```      },```<br>```      body: JSON.stringify(requestBody)```<br>```    });```<br>``````<br>```    if (!response.ok) {```<br>```      throw new Error(`HTTP error! status: ${response.status}`);```<br>```    }```<br>``````<br>```    const data = await response.json();```<br>``````<br>```    if (data.code === 0) {```<br>```      console.log(`task id: ${data.data.task_id}`);```<br>```      if (data.data.usage) {```<br>```        console.log(`usage: ${data.data.usage.toFixed(2)}`);```<br>```      }```<br>```      if (data.data.payload) {```<br>``````<br>```        console.log(JSON.stringify(data.data.payload, null, 2));```<br>```      }```<br>```    } else {```<br>```      console.log('\nquery task failed:', data.message);```<br>```    }```<br>```  } catch (error) {```<br>```    console.error('query task failed:', error);```<br>```  }```<br>```}```<br>``````<br>```queryTask();```<br>``````<br> |```Go```<br>```package main```<br>``````<br>```import (```<br>```        "bytes"```<br>```        "encoding/json"```<br>```        "fmt"```<br>```        "io"```<br>```        "net/http"```<br>```        "time"```<br>```)```<br>``````<br>```func QueryTask() {```<br>```        const (```<br>```                apiKey = "YOUR_API_KEY"```<br>```                taskID = "YOUR_TASK_ID"```<br>```        )```<br>``````<br>```        requestBody := map[string]interface{}{```<br>```                "task_id": taskID,```<br>```        }```<br>``````<br>```        body, err := json.Marshal(requestBody)```<br>```        if err != nil {```<br>``````<br>```                return```<br>```        }```<br>``````<br>```        url := "https://kickart.bytepluses.com/openapi/ai_effect/query"```<br>```        req, err := http.NewRequest("POST", url, bytes.NewReader(body))```<br>```        if err != nil {```<br>```            ```<br>```                return```<br>```        }```<br>``````<br>```        req.Header.Set("Authorization", "Bearer "+apiKey)```<br>```        req.Header.Set("Content-Type", "application/json")```<br>``````<br>```        client := &http.Client{```<br>```                Timeout: 30 * time.Second,```<br>```        }```<br>``````<br>```        resp, err := client.Do(req)```<br>```        if err != nil {```<br>```                return```<br>```        }```<br>```        defer resp.Body.Close()```<br>``````<br>```        respBody, err := io.ReadAll(resp.Body)```<br>```        if err != nil {```<br>```                return```<br>```        }```<br>``````<br>```        var response map[string]interface{}```<br>```        if err := json.Unmarshal(respBody, &response); err != nil {```<br>```                return```<br>```        }```<br>``````<br>```        if data, ok := response["data"].(map[string]interface{}); ok {```<br>```                fmt.Printf("task_id: %s\n", data["task_id"])```<br>```                if usage, ok := data["usage"]; ok {```<br>```                        fmt.Printf("usage: %.2f\n", usage)```<br>```                }```<br>```                if payload, ok := data["payload"]; ok {```<br>```                        fmt.Printf("task result: %v\n", payload)```<br>```                }```<br>```        }```<br>```        fmt.Printf("response: %s\n", string(respBody))```<br>```}```<br>``````<br> |



3. ### **Error Code Description **  <span id="zqGroH8L"></span>


The response bodies of all interfaces contain  `code`  and  `message`  fields, which are used to indicate the processing result of the request. When  `code`  is  `0` , it indicates that the business processing was successful. A value other than  `0`  indicates that an exception occurred. 

<span id="1vOTJolF"></span>
### **General Error Code**


|Error Code |Error Type (for marking only, will not be returned) |Description and Handling Suggestions |
|---|---|---|
|1300 |`AuthFailed` |**Authentication failed**: The API Key is invalid, expired, or inactive. Please check if your API Key is correct, or confirm its status in the Volcano Engine Console. |
|1400 |`ParamErr`<br><br> |**Parameter Error**: The request contains invalid or missing parameters. Please check the request body structure, field types, and required fields against the documentation. |
|1401 |`ConcurrentErr`<br><br> |**Concurrent limit exceeded**: The number of your current concurrent requests has exceeded the agreed\-upon limit. Please reduce the request frequency or contact your business representative to adjust the concurrent quota. |
|1403 |`QuotaErr` |**No Permission **  : Your account does not have permission to call this API. Please contact the enterprise administrator to grant you access to the relevant services.  |
|1402<br><br> |`InsufficientPoints`<br><br> |**Insufficient Creation Points**: Account balance is insufficient to cover the consumption of this task. Please recharge in a timely manner. |
|1500 |`InternalErr` |**Internal Error**: An unknown error occurred on the server. Please record request_id and contact technical support. |


<span id="edbfvA4r"></span>
### **Interface\-specific error code**

 **`/openapi/ai_effect/submit`** ** & **  **`/openapi/ai_effect/query`**


|Error Code |Error Type (for marking only, will not be returned) |Description and Handling Suggestions |
|---|---|---|
|0 |`Success` |**Task Succeeded**: Task processing completed, and results have been generated. |
|1000 |`AsyncTaskRunning`<br><br> |**Task is running**: The task is being processed. Please poll the results later via the `AITemplateAsyncTaskQuery` interface. |
|1410 |`TemplateIdNotExist`<br><br> |**Template does not exist**: The requested `template_id` is invalid or the corresponding template has not been launched. Please obtain the list of available templates through the `ListTemplateInfo` interface. |
|1411 |`InputResolutionErr` |**Resolution Error**: The requested `Resolution` is not in the list of supported `resolutions` by the template. |
|1412<br><br> |`ImageFormatErr`<br><br> |**Image format error**: The input image format is unsupported or the file is corrupted. It is recommended to use common `JPEG` or `PNG` formats. |
|1413 |`InvalidMediaUrlErr`<br><br> |**Media URL is invalid**: `URL in ResourceList` is inaccessible. Please ensure the URL is publicly accessible and has not expired. |
|1414 |`MediaSensitiveErr`<br><br> |**Content Safety Issue**: The input content has triggered the platform's safety moderation policy. Please replace the content and try again. |
|1600 |`AsyncTaskNotExist` |**Task does not exist**: The queried `task_id` is invalid. Please check whether `task_id` is the value successfully returned by the `AITemplateAsyncTaskSubmit` interface. |
|1601 |`AsyncTaskTimeoutErr` |**Task timeout**: Task execution exceeded the maximum processing time set by the system (currently 1 hour). |
|2000 |`AsyncTaskFailed` |**Task Failed**: An unclassifiable failure occurred during task execution. |
|3000 |`TaskCallbackFailed` |**Callback failed**: Failed to send the result to the callback address you configured. |
|5000 |`RiverWorkflowFailed` |**Workflow failed**: Underlying AI workflow execution failed, usually serving as a fallback for more specific errors (e.g., 1412\-1414). |



---



&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;
