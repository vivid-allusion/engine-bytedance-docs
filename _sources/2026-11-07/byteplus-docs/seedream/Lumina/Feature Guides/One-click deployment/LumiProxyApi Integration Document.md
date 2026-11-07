---
title: "LumiProxyApi Integration Document"
product: "Seedream"
product_code: "seedream"
source: "https://docs.byteplus.com/en/docs/seedream/LumiProxyApi-Integration-Document"
---

<span id="DI71RbED"></span>
## 1. Interface Overview

After publishing and accessing capabilities through Lumina, you can connect to the relevant API services via this document. This interface provides general access capabilities for enterprise\-level algorithm services, supporting core functions such as asynchronous task submission, synchronized processing requests, task result query, and task cancellation. It is suitable for business scenarios that require algorithmic processing of multimedia data such as images. 

<span id="I7vxL0vq"></span>
## 2. Basic Information

**Preparations before integration:** 

1. Your AccessKey and SecretKey can be created and obtained via [https://console.byteplus.com/iam/keymanage](https://console.byteplus.com/iam/keymanage)

2. Please integrate the BytePlus SDK in advance, obtain the signature key for requester identity verification, and include the signature information in the request. For the signature method, refer to: [https://docs.byteplus.com/en/docs/byteplus-platform/reference-how-to-calculate-a-signature](https://docs.byteplus.com/en/docs/byteplus-platform/reference-how-to-calculate-a-signature)

<span id="EL0cdorS"></span>
### 2.1 Request Domain Name

cv.byteplusapi.com

<span id="TgRNTBgm"></span>
### 2.2 Request Method


* **POST** (All interfaces use this method)


<span id="C5rCzTWv"></span>
## 3. Core Interface Description

<span id="9x34xhd0"></span>
### 3.1 Asynchronous Submission of Algorithm Task **LumiSync2AsyncSubmitTask**

<span id="byQr3kX3"></span>
#### 3.1.1 Functional Description

Submit an asynchronous processing task, supporting image Base64 or publicly accessible resource URLs, and return the task ID.

<span id="NZiNSJwn"></span>
#### 3.1.2 Request Parameters (SubmitTaskReq)


| |Parameter Name |Type |Required |Description |
|---|---|---|---|---|
|**Query** |Action |String |YES |Interface Name, Value:**LumiSync2AsyncSubmitTask** |
||Version |String |YES |Interface Version, Value:**2025\-06\-01** |
|**Header** |ServiceName |String |YES |cv |
||Region |String |YES |ap\-singapore\-1 |
||Authorization |String |YES |Signature Key, Signature Method Reference: https://docs.byteplus.com/en/docs/byteplus\-platform/reference\-how\-to\-calculate\-a\-signature |
||Content\-Type |String |YES |application/json |
|**Body**<br><br> |req_key |string |YES |Request Unique Identifier (Customized Capability Name for One\-Click Deployment) |
||res_quota_name |string |YES |Requested Resource Name <br><br><div style="text-align: center"><br><img src="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260416141609-737354580960.png" width="2490px" /></div><br> |
||binary_data |[]string<br><br> |No <br><br> |Base64 list of image files (if there are files, choose one of this and data_source, and at least one must be provided)<br><br>Base64 images are limited to a size of less than 8MB; if the size limit is exceeded, an error will occur: 400, Error when parsing request |
||req_json |json |YES |Business parameters in JSON format, reference for retrieval method:<br><br><div style="text-align: center"><br><img src="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260416141609-855243983919.png" width="2496px" /></div><br><br><br>&nbsp;<br><br>The parameters for slotting, which are the algorithm parameters that need to be passed when requesting Openapi, can be seen in the service details interface information. An example of req_json can be seen in the demo example <br><br> |
||expired_duration |\*int64 |No  |Task expiration time (milliseconds, optional, default handled according to service configuration) |
||data_source |[]\*common.DataSource |No  |Data source link list (supports HTTP/HTTPS links, images must be downloadable, otherwise a parameter error will be returned) |


DataSource Structure：


|Parameter Name |Type |Required |Description |
|---|---|---|---|
|data_source_type |int64 |YES |Default to 1 |
|value |string |YES |When the data source type is url, the value is a downloadable url; for the blocklist domain names of links, please refer to the specifications below.  |


<span id="oSxNZeWe"></span>
#### 3.1.3 Response Parameters (SubmitTaskResp)


|Parameter Name |Type |Description |
|---|---|---|
|task_id |string |Task ID (used for subsequent result query or task cancellation) |
|resp_json |string |Initial response results (may contain algorithm preprocessing information) |


<span id="E8WMUNQC"></span>
#### **Example**

&nbsp;

Submit an asynchronous task via binary_data:

```Shell
curl --location 'http://cv.byteplusapi.com?Action=LumiSync2AsyncSubmitTask&Version=2025-06-01' \
--header 'Authorization: YOURAuthorization' \
--header 'Region: ap-singapore-1' \
--header 'ServiceName: cv' \
--header 'Content-Type: application/json' \
--header 'get-svc: 1' \
--data '{
    "req_key": "hy_test_lumi_onedeploy_mingxinp_v1",
    "req_json":{
        "input_text": "HELLO",
        "seed": 1,
        "input_image": "uri://binary_data?index=0"
    },
    "binary_data": [
        "PIC1 base64"
    ]
}'
```


Submit an asynchronous task via the data_source method:

```Shell
curl --location 'http://cv.byteplusapi.com?Action=LumiSync2AsyncSubmitTask&Version=2025-06-01' \
--header 'Authorization: YOURAuthorization' \
--header 'Region: ap-singapore-1' \
--header 'ServiceName: cv' \
--header 'Content-Type: application/json' \
--header 'get-svc: 1' \
--data '{
    "req_key": "hy_test_lumi_onedeploy_mingxinp_v1",
    "req_json":{
        "input_text": "HELLO",
        "seed": 1,
        "input_image": "uri://binary_data?index=0"
    },
    "data_source": [
        {
            "data_source_type":1,
            "value":"Picture url"
        }
    ]
}'
```


After the command execution is completed, the following results are obtained: 

```JSON
{
    "code": 0,
    "message": "",
    "data": {
        "task_id": "14468076912309597066",
        "resp_json": ""
    },
    "request_id": "202506031700371C156D18803F25334BFC"
}
```


<span id="nf2Ajxz0"></span>
### 3.2 Synchronize Processing Request **LumiProcess**

<span id="NvV0708S"></span>
#### 3.2.1 Functional Description

Synchronous call algorithm processing (suitable for lightweight tasks, the response directly returns the result, with a default timeout of 30 seconds; tasks exceeding 30 seconds will return a failure. Please evaluate your own resource situation when choosing to call, and it is recommended to choose the asynchronous request method). 

<span id="nDzd9a6I"></span>
#### 3.2.2 Request Parameters (ProcessReq)


| |Parameter Name |Type |Required |Description |
|---|---|---|---|---|
|**Query**<br><br> |Action |String |YES |Interface Name, Value:**LumiProcess** |
||Version |String |YES |Interface Version, Value:**2025\-06\-01** |
|**Header** |ServiceName |String |YES |cv |
||Region |String |YES |ap\-singapore\-1 |
||Authorization<br><br> |String |YES |Signature Key, Signature Method Reference: https://docs.byteplus.com/en/docs/byteplus\-platform/reference\-how\-to\-calculate\-a\-signature |
||Content\-Type |String |YES |application/json |
|**Body**<br><br> |req_key |string |YES |Request Unique Identifier |
||res_quota_name |string |YES |Requested Resource Name <br><br><div style="text-align: center"><br><img src="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260416141609-197113996962.png" width="2490px" /></div><br><br><br> |
||binary_data |[]string<br><br> |No  |Image Base64 list (choose one with data_source, at least one must be provided) |
||req_json |json |YES |Business parameters in JSON format, reference for retrieval method:<br><br><div style="text-align: center"><br><img src="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260416141609-155461336684.png" width="3050px" /></div><br><br><br>&nbsp;<br><br>The parameters for slotting, which are the algorithm parameters that need to be passed when requesting Openapi, can be seen in the service details interface information. An example of req_json can be seen in the demo example <br><br> |
||data_source |[]\*common.DataSource |No  |Data source link list |


DataSource structure：


|Parameter Name |Type |Required |Description |
|---|---|---|---|
|data_source_type |int64 |YES |Default to 1 |
|value |string |YES |When the data source type is url, the value is a downloadable url; see the specifications below for the blocklist domain names of links.  |


<span id="Uu4BiJqA"></span>
#### 3.2.3 Response Parameters (AlgoResp)


|Parameter Name |Type |Description |
|---|---|---|
|binary_data |[][]byte |Binary results (such as files after image processing) |
|resp_json |string |Algorithm results in JSON format (core business data) |


<span id="dPAEzQjn"></span>
#### **Example**

Submit an asynchronous task via binary_data:

```Shell
curl --location 'http://cv.byteplusapi.com?Action=LumiProcess&Version=2025-06-01' \
--header 'Authorization: YOURAuthorization' \
--header 'Region: ap-singapore-1' \
--header 'ServiceName: cv' \
--header 'Content-Type: application/json' \
--header 'get-svc: 1' \
--data '{
    "req_key": "hy_test_lumi_onedeploy_mingxinp_v1",
    "req_json":{
        "input_text": "HELLO",
        "seed": 1,
        "input_image": "uri://binary_data?index=0"
    },
    "binary_data": [
        "PIC1 base64"
    ]
}'
```


Submit asynchronous tasks via data_source:

```Shell
curl --location 'http://cv.byteplusapi.com?Action=LumiProcess&Version=2025-06-01' \
--header 'Authorization: YOURAuthorization' \
--header 'Region: ap-singapore-1' \
--header 'ServiceName: cv' \
--header 'Content-Type: application/json' \
--header 'get-svc: 1' \
--data '{
    "req_key": "hy_test_lumi_onedeploy_mingxinp_v1",
    "req_json":{
        "input_text": "HELLO",
        "seed": 1,
        "input_image": "uri://binary_data?index=0"
    },
    "data_source": [
        {
            "data_source_type":1,
            "value":"Picture url"
        }
    ]
}'
```


After the command execution is completed, the following results are obtained: 

```JSON
{
        "code": 0,
        "message": "",
        "request_id": "2025060316510263209B2543B40032B4A0",
        "data": {
                "binary_data": ["return PIC1base64","return PIC2base64",],
                "resp_json": "{\"output_image\": [\"uri://binary_data?index=0\"], \"comfyui_cost\": 0}"
        }
}
```


&nbsp;

<span id="DpWYFQOG"></span>
### 3.3 Batch Obtain Task Results**LumiSync2AsyncBatchGetResults**

<span id="lY5EUy5j"></span>
####  3.3.1 Functional Description

&nbsp;

Batch query the status and results of asynchronous tasks by task ID.

<span id="nY4u1Ac2"></span>
#### 3.3.2 Request Parameters (GetResultReq)


| |Parameter Name |Type |Required |Description |
|---|---|---|---|---|
|**Query** |Action |String |YES |value:**LumiSync2AsyncBatchGetResults** |
||Version |String |YES |Interface Version, Value:**2025\-06\-01** |
|**Header** |ServiceName |String |YES |cv |
||Region |String |YES |ap\-singapore\-1 |
||Authorization |String |YES |Signature Key, Signature Method Reference: https://docs.byteplus.com/en/docs/byteplus\-platform/reference\-how\-to\-calculate\-a\-signature |
||Content\-Type |String |YES |application/json |
|**Body** |task_ids |[]string |YES |List of task IDs to be queried |


<span id="KsIQbcV8"></span>
#### 3.3.3 Response Parameters (BatchGetResultResp)


|Parameter Name |Type |Description |
|---|---|---|
|results |[]\*GetResultRespV2 |Task result list (corresponding to task ID) |


GetResultRespV2 Field Description:


|Parameter Name |Type |Description |
|---|---|---|
|task_id |string |Task ID |
|status |string |Task Status Enumeration:<br><br>in_queue: Task has been submitted<br><br>generating: The task has been consumed and is being processed<br><br>done: Processing completed. Note: Only when the processing is completed, should you check the specific results based on algo_status_code!!! Otherwise, StatusCode is invalid!!!<br><br>not_found: Task not found, possible reasons include the task does not exist or has expired (24 hours)<br><br>expired: The task has reached the set expiration time<br><br>Canceled: The task has been canceled<br><br>over_max_retries: Maximum number of retries has been reached |
|progress |int64 |Task progress (0\-100, only returned by asynchronous tasks) |
|req_json |string |Original business parameters when submitting the task |
|submit_timestamp_ms<br><br> |int64 |Task submission time (millisecond\-level timestamp) |
|process_start_timestamp_ms |int64 |Task start processing time (millisecond\-level timestamp) |
|process_end_timestamp_ms |int64 |Task end time (millisecond\-level timestamp, only returned after task completion) |
|algo_status_code |int32 |Algorithm Status Code |
|algo_status_message |string |Algorithm error message (returned when failed) |
|status_code |int32 |Error code (0 indicates success, non\-0 requires reference to the error code documentation)  |
|status_message |string |Status Information |


<span id="5pGH9oTk"></span>
#### Example

Query by task_id:

```Shell
curl --location 'http://cv.byteplusapi.com?Action=LumiSync2AsyncBatchGetResults&Version=2025-06-01' \
--header 'Authorization: YOURAuthorization' \
--header 'Region: ap-singapore-1' \
--header 'ServiceName: cv' \
--header 'Content-Type: application/json' \
--header 'get-svc: 1' \
--data '{
    "task_ids": ["14468076912309597066"]
}'
```


After the command execution is completed, the following results are obtained: 

```JSON
{
    "code": 0,
    "message": "",
    "data": {
        "results": [
            {
                "binary_data": [],
                "resp_json": "{\"output_image\": [\"uri://binary_data?index=0\"], \"comfyui_cost\": 133}",
                "status": "done",
                "callback_args": "",
                "progress": 0,
                "req_json": "{\"input_image\":\"uri://binary_data?index=0\",\"input_text\":\"HELLO\",\"seed\":13}",
                "task_id": "14468076912309597066",
                "submit_timestamp_ms": 1748941238332,
                "process_start_timestamp_ms": 1748941238388,
                "process_end_timestamp_ms": 1748941252489,
                "req_key": "hy_test_lumi_onedeploy_mingxinp_v1",
                "algo_status_code": 0,
                "algo_status_message": " <- [返回]消息=Success:Success",
                "status_code": 0
            }
        ]
    },
    "request_id": "202506031700531C156D18803F2533520C"
}
```


<span id="RixbOlEm"></span>
### 3.4 Batch Cancel Tasks**LumiSync2AsyncBatchCancelTasks**

<span id="ykwjU5jL"></span>
#### 3.4.1 Functional Description

Batch cancel unstarted asynchronous tasks.

<span id="R9BtTKAm"></span>
#### 3.4.2 Request Parameters (CancelTaskReq)


| |Parameter Name |Type |Required |Description |
|---|---|---|---|---|
|**Query** |Action |String |YES |Interface Name, Value:**LumiSync2AsyncBatchCancelTasks** |
||Version |String |YES |Interface Version, Value:**2025\-06\-01** |
|**Header**<br><br> |ServiceName |String |YES |cv |
||Region |String |YES |ap\-singapore\-1 |
||Authorization |String |YES |Signature Key, Signature Method Reference: https://docs.byteplus.com/en/docs/byteplus\-platform/reference\-how\-to\-calculate\-a\-signature |
||Content\-Type |String |YES |application/json |
|**Body** |task_ids |[]string |YES |List of task IDs to be cancelled |


<span id="DuetDA7p"></span>
#### 3.4.3 Response Parameters (BatchCancelTaskResp)


|Parameter Name |Type |Description |
|---|---|---|
|failed_task_ids |[]string |Cancel the list of failed task IDs (usually caused by the task already being in progress) |


<span id="KyIc30Ey"></span>
#### Example

Query by task_id:

```Shell
curl --location 'http://cv.byteplusapi.com?Action=LumiSync2AsyncBatchCancelTasks&Version=2025-06-01' \
--header 'Authorization: YOURAuthorization' \
--header 'Region: ap-singapore-1' \
--header 'ServiceName: cv' \
--header 'Content-Type: application/json' \
--header 'get-svc: 1' \
--data '{
    "task_ids": ["14468076912309597066"]
}'
```


After the command execution is completed, the following results are obtained: 

```JSON
{
    "code": 0,
    "message": "",
    "data": {
        "failed_task_ids": []
    },
    "request_id": "202506031713241DA91B56FDF0AA32030D"
}
```


<span id="ycZxdyzc"></span>
## 4. Request Specification

<span id="HKvR5Gr6"></span>
### 4.1 Data Format


* **Request Body**: Use JSON format, and the parameters must be consistent with the interface definition (note that the case of fields should be consistent with the documentation, such asreq_keyinstead ofReqKey).

* **File Transfer**: The Base64 encoding of images must ensure correct encoding (excluding the data:image/... prefix), and the data source link must be publicly accessible on the Internet.


<span id="bXVWQFUT"></span>
### 4.2 Error Code Explanation

<span id="Ubv8pc2B"></span>
#### Success 


|StatusCode  |StatusMessage  |Instructions  |
|---|---|---|
|0  |Success  |Success  |


<span id="xk78COeY"></span>
#### Internal Error


* Algorithm\-specific error codes are returned viacode.



|StatusCode  |StatusMessage  |Instructions  |
|---|---|---|
|10000  |Internal Error  |Abnormal internal error, mainly caused by the error reported by the gateway when calling the algorithm service, commonly due to timeout  |
|10001  |RPC Internal Error  |Downstream algorithm service abnormal internal error, such as algorithm service calling its sub\-service timeout, service crash, etc.  |
|10002  |Downstream RPC Service No Targets Found Error  |Error caused by the gateway failing to discover downstream instances. Please check if your res_quota_name is filled in correctly. <br><br>If the request comes from PPE, it will only discover downstream algorithm instances in the same data center; if the request comes from non\-PPE, it will only discover downstream algorithm instances in the prod environment.  |
|10003  |ECRetryInternal <br><br> |Abnormal internal error. The gateway has set up retries. After the request reaches the algorithm, the connection is successful, but it ultimately fails and reports an error due to reasons such as timeout.  |
|10004 | |Missing req_key： "message": "input validate failed: Key: 'SubmitTaskReq.ReqKey' Error:Field validation for 'ReqKey' failed on the 'required' tag"<br><br>Missing req_json："input validate failed: Key: 'SubmitTaskReq.ReqJson' Error:Field validation for 'ReqJson' failed on the 'required' tag" |
|30402 |ErrCodeBizError |Service is abnormal, please contact colleagues for troubleshooting |


<span id="sTRo368I"></span>
#### Rate limit error


|StatusCode  |StatusMessage  |Instructions  |
|---|---|---|
|11000  |Req over limit  |The request triggers gateway rate limiting, usually because of insufficient algorithm resources, so rate limiting is set to ensure service stability.  |
|11001  |ECReqConFailed  |Single instance BACKLOG rate limiting error in the algorithm. After the gateway sets retry and the algorithm service sets single instance BACKLOG, the connection fails (connection errors such as 1115). <br><br>Generally, rate limiting is set due to insufficient algorithm resources to ensure service stability. |


 &nbsp;

<span id="roGrzcJI"></span>
#### Input error 


|StatusCode  |StatusMessage  |Instructions  |
|---|---|---|
|20000  |RPC Process Error: {err_msg}, rpc service err_code={rpc_err_code}  |Non\-universal input error identified by the algorithm service |
|21000<br><br>30432<br><br>30400 |Invalid Param <br><br> |Parameter error  |
|30404 |FeatNotFound |Capability does not exist |
|21001<br><br>30431 |Image Decode Error  |Image decoding error  |
|21002  |Image Empty  |The input image is empty  |
|21003  |Invalid Image  |The incoming image cannot be processed by the algorithm  |
|22000  |No Face Detected  |No face was detected in the image  |
|22001  |No Man Detected  | No person was detected in the picture  |


<span id="jDOVHeF3"></span>
#### Moderation Error


|StatusCode  |StatusMessage  |Instructions  |
|---|---|---|
|23001  |Pre Img Risk Not Pass  |Moderation failed before inputting the image |
|23002  |Post Img Risk Not Pass  | After the image is output, moderation fails  |
|23003  |Text Risk Not Pass  |Moderation failed before inputting text  |
|23004  |Post Text Risk Not Pass  |The output text failed moderation after being generated  |
|23005  |Post Text Risk Not Pass  | Keyword service interception (generally used for copyright word moderation) |
|23006  |Pre Video Risk Not Pass  |Pre\-input video moderation failed |
|23007  |Post Video Risk Not Pass  |The output video failed moderation after being released  |
|23008  |Pre Audio Risk Not Pass  |Pre\-input audio moderation failed |
|23009  |Post Audio Risk Not Pass  |Moderation failed after audio output  |
|23010  |Pre Image Copyright Not Pass  |Moderation failed before inputting copyrighted image |
|23011  |Post Image Copyright Not Pass  |Moderation failed after outputting the copyright image  |
|23100  |ECRiskInternal  |Moderation service is abnormal  |
|23101  |ECAntidirtInternal  |Copyright term service is abnormal |
|23102  |ECImgCopyrightInternal  |Copyright image service is abnormal |


<span id="tbmzGbef"></span>
####  Authentication error


|StatusCode  |StatusMessage  |Instructions  |
|---|---|---|
|24000 |Ability Auth failed  |Competency level certification failed  |
|30403 |NoFeatAuth |has no permission |
|24001  |Application Auth failed  |General authentication failed |
|24002  |Sign Auth failed  |Signature error |
|24003  |Authorization failed  |Access authorization failed  |
|24004  |SignAuth Time Expired  |Signature verification timestamp has expired |


<span id="3t1cwqST"></span>
### 4.3 Correspondence between attachments such as images and the order of req_json

The value uri://binary_data?index=0 in the req_json request field represents the index in the binary_data list. If you choose to use data_source to pass a url as the value of a field in req_json, it will first be converted to binary_data internally, and then match the uri://binary_data?index=\* at the corresponding req_jso

&nbsp;

<span id="mt0thFK8"></span>
## 一、接口概述

通过Lumina发布并接入能力后，可通过本文档对接相关的api服务。本接口为企业级算法服务提供通用接入能力，支持异步任务提交、同步处理请求、任务结果查询、任务取消等核心功能。适用于需要对图片等多媒体数据进行算法处理的业务场景。

<span id="xuT4hqzJ"></span>
## 二、基础信息

**接入前准备：** 

1、你的AccessKey和你的SecretKey可通过[https://console.byteplus.com/iam/keymanage](https://console.byteplus.com/iam/keymanage)创建并获取。

2、请提前接入BytePlus sdk，并获取签名密钥进行请求者身份验证，在请求中携带签名信息，签名方法参考：[https://docs.byteplus.com/en/docs/byteplus-platform/reference-how-to-calculate-a-signature](https://docs.byteplus.com/en/docs/byteplus-platform/reference-how-to-calculate-a-signature)

<span id="gbLOM1YW"></span>
### 2.1 请求域名

cv.byteplusapi.com

<span id="8v449CMI"></span>
### 2.2 请求方法


* **POST**（所有接口均使用此方法）


<span id="MRSULtpj"></span>
## 三、核心接口说明

<span id="Pbgi46iA"></span>
### 3.1 异步提交算法任务 **LumiSync2AsyncSubmitTask**

<span id="zxKZDDp1"></span>
#### 3.1.1 功能描述

提交异步处理任务，支持图片Base64或公网可访问资源 url，返回任务ID。

<span id="B6wJjnnj"></span>
#### 3.1.2 请求参数（SubmitTaskReq）


| |参数名 |类型 |是否必填 |说明 |
|---|---|---|---|---|
|**Query** |Action |String |是 |接口名称，值：**LumiSync2AsyncSubmitTask** |
||Version |String |是 |接口版本，值：**2025\-06\-01** |
|**Header** |ServiceName |String |是 |cv |
||Region |String |是 |ap\-singapore\-1 |
||Authorization |String |是 |签名密钥，签名方法参考：[https://docs.byteplus.com/en/docs/byteplus-platform/reference-how-to-calculate-a-signature](https://docs.byteplus.com/en/docs/byteplus-platform/reference-how-to-calculate-a-signature) |
||Content\-Type |String |是 |application/json |
|**Body**<br><br> |req_key |string |是<br><br> |请求唯一标识（一键部署的自定义的能力名称） |
||res_quota_name |string |是 |请求资源名称<br><br><div style="text-align: center"><br><img src="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260416141923-801931877793.png" width="2490px" /></div><br> |
||binary_data |[]string<br><br> |否 |图片类文件Base64列表（如果有文件的情况下，与data_source二选一，至少传其一）<br><br>Base64图片限制大小为8M以内，超出大小限制，则会报错：400，Error when parsing request |
||req_json |json |是<br><br> |JSON格式的业务参数，获取方式参考：<br><br><div style="text-align: center"><br><img src="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260416141923-636352681526.png" width="2496px" /></div><br><br><br>&nbsp;<br><br>可以在服务详情接口信息看到开槽的参数，也就是请求 Openapi 需要传入的算法参数。可以在 demo 示例看到 req_json 的示例<br><br> |
||expired_duration |\*int64 |否 |任务过期时间（毫秒，可选，默认根据服务配置处理） |
||data_source |[]\*common.DataSource |否 |数据源链接列表（支持HTTP/HTTPS链接，图片需可下载，否则返回参数错误） |


DataSource结构：


|参数名 |类型 |是否必填 |说明 |
|---|---|---|---|
|data_source_type |int64 |是 |默认填1 |
|value |string |是 |数据来源类型为 url 时，value 为可下载 url；链接黑名单域名请见下方规范。 |


<span id="rHI7DVGN"></span>
#### 3.1.3 响应参数（SubmitTaskResp）


|参数名 |类型 |说明 |
|---|---|---|
|task_id |string |任务ID（用于后续结果查询或取消任务） |
|resp_json |string |初步响应结果（可能包含算法预处理信息） |


<span id="JX0KJ60r"></span>
#### **示例**

通过binary_data的方式提交异步任务：

```Shell
curl --location 'http://cv.byteplusapi.com?Action=LumiSync2AsyncSubmitTask&Version=2025-06-01' \
--header 'Authorization: 你的Authorization' \
--header 'Region: ap-singapore-1' \
--header 'ServiceName: cv' \
--header 'Content-Type: application/json' \
--header 'get-svc: 1' \
--data '{
    "req_key": "hy_test_lumi_onedeploy_mingxinp_v1",
    "req_json":{
        "input_text": "你好呀",
        "seed": 1,
        "input_image": "uri://binary_data?index=0"
    },
    "binary_data": [
        "图片1的base64"
    ]
}'
```


通过data_source的方式提交异步任务：

```Shell
curl --location 'http://cv.byteplusapi.com?Action=LumiSync2AsyncSubmitTask&Version=2025-06-01' \
--header 'Authorization: 你的Authorization' \
--header 'Region: ap-singapore-1' \
--header 'ServiceName: cv' \
--header 'Content-Type: application/json' \
--header 'get-svc: 1' \
--data '{
    "req_key": "hy_test_lumi_onedeploy_mingxinp_v1",
    "req_json":{
        "input_text": "你好呀",
        "seed": 1,
        "input_image": "uri://binary_data?index=0"
    },
    "data_source": [
        {
            "data_source_type":1,
            "value":"图片url"
        }
    ]
}'
```


命令执行完成后，获得以下结果： 

```JSON
{
    "code": 0,
    "message": "",
    "data": {
        "task_id": "14468076912309597066",
        "resp_json": ""
    },
    "request_id": "202506031700371C156D18803F25334BFC"
}
```


<span id="2C199wlp"></span>
### 3.2 同步处理请求 **LumiProcess**

<span id="iUcSFUeN"></span>
#### 3.2.1 功能描述

同步调用算法处理（适用于轻量级任务，响应直接返回结果，默认超时30s，超过30s的任务将会返回失败，请评估自身的资源情况选择调用，推荐选择异步请求的方式）。

<span id="Grknp6yp"></span>
#### 3.2.2 请求参数（ProcessReq）


| |参数名 |类型 |是否必填 |说明 |
|---|---|---|---|---|
|**Query**<br><br> |Action |String |是 |接口名称，值：**LumiProcess** |
||Version |String |是 |接口版本，值：**2025\-06\-01** |
|**Header** |ServiceName |String |是 |cv |
||Region |String |是 |ap\-singapore\-1 |
||Authorization<br><br> |String |是 |签名密钥，签名方法参考：[https://docs.byteplus.com/en/docs/byteplus-platform/reference-how-to-calculate-a-signature](https://docs.byteplus.com/en/docs/byteplus-platform/reference-how-to-calculate-a-signature) |
||Content\-Type |String |是 |application/json |
|**Body**<br><br> |req_key |string |是 |请求唯一标识 |
||res_quota_name |string |是 |请求资源名称<br><br><div style="text-align: center"><br><img src="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260416141923-491703005364.png" width="2490px" /></div><br><br><br> |
||binary_data |[]string<br><br> |否 |图片Base64列表（与data_source二选一，至少传其一） |
||req_json |json |是 |JSON格式的业务参数，获取方式参考：<br><br><div style="text-align: center"><br><img src="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260416141923-1614131022441.png" width="3050px" /></div><br><br><br>&nbsp;<br><br>可以在服务详情接口信息看到开槽的参数，也就是请求 Openapi 需要传入的算法参数。可以在 demo 示例看到 req_json 的示例 |
||data_source |[]\*common.DataSource |否 |数据源链接列表 |


DataSource结构：


|参数名 |类型 |是否必填 |说明 |
|---|---|---|---|
|data_source_type |int64 |是 |默认填1 |
|value |string |是 |数据来源类型为 url 时，value 为可下载 url；链接黑名单域名请见下方规范。 |


<span id="iyIy90xH"></span>
#### 3.2.3 响应参数（AlgoResp）


|参数名 |类型 |说明 |
|---|---|---|
|binary_data |[][]byte |二进制结果（如图像处理后的文件） |
|resp_json |string |JSON格式的算法结果（核心业务数据） |


<span id="wcoowwgn"></span>
#### **示例**

通过binary_data的方式提交异步任务：

```Shell
curl --location 'http://cv.byteplusapi.com?Action=LumiProcess&Version=2025-06-01' \
--header 'Authorization: 你的Authorization' \
--header 'Region: ap-singapore-1' \
--header 'ServiceName: cv' \
--header 'Content-Type: application/json' \
--header 'get-svc: 1' \
--data '{
    "req_key": "hy_test_lumi_onedeploy_mingxinp_v1",
    "req_json":{
        "input_text": "你好呀",
        "seed": 1,
        "input_image": "uri://binary_data?index=0"
    },
    "binary_data": [
        "图片1的base64"
    ]
}'
```


通过data_source的方式提交异步任务：

```Shell
curl --location 'http://cv.byteplusapi.com?Action=LumiProcess&Version=2025-06-01' \
--header 'Authorization: 你的Authorization' \
--header 'Region: ap-singapore-1' \
--header 'ServiceName: cv' \
--header 'Content-Type: application/json' \
--header 'get-svc: 1' \
--data '{
    "req_key": "hy_test_lumi_onedeploy_mingxinp_v1",
    "req_json":{
        "input_text": "你好呀",
        "seed": 1,
        "input_image": "uri://binary_data?index=0"
    },
    "data_source": [
        {
            "data_source_type":1,
            "value":"图片url"
        }
    ]
}'
```


命令执行完成后，获得以下结果： 

```JSON
{
        "code": 0,
        "message": "",
        "request_id": "2025060316510263209B2543B40032B4A0",
        "data": {
                "binary_data": ["返回的图片1base64","返回的图片2base64",],
                "resp_json": "{\"output_image\": [\"uri://binary_data?index=0\"], \"comfyui_cost\": 0}"
        }
}
```


&nbsp;

<span id="3CnJSoaz"></span>
### 3.3 批量获取任务结果 **LumiSync2AsyncBatchGetResults**

<span id="P3GPAnBI"></span>
#### 3.3.1 功能描述

通过任务ID批量查询异步任务状态及结果。

<span id="mgPhm2QO"></span>
#### 3.3.2 请求参数（GetResultReq）


| |参数名 |类型 |是否必填 |说明 |
|---|---|---|---|---|
|**Query** |Action |String |是 |接口名称，值：**LumiSync2AsyncBatchGetResults** |
||Version |String |是 |接口版本，值：**2025\-06\-01** |
|**Header** |ServiceName |String |是 |cv |
||Region |String |是 |ap\-singapore\-1 |
||Authorization |String |是 |签名密钥，签名方法参考：https://docs.byteplus.com/en/docs/byteplus\-platform/reference\-how\-to\-calculate\-a\-signature |
||Content\-Type |String |是 |application/json |
|**Body** |task_ids |[]string |是 |待查询的任务ID列表 |


<span id="vd1KNHyw"></span>
#### 3.3.3 响应参数（BatchGetResultResp）


|参数名 |类型 |说明 |
|---|---|---|
|results |[]\*GetResultRespV2 |任务结果列表（按任务ID对应） |


GetResultRespV2 字段说明：


|参数名 |类型 |说明 |
|---|---|---|
|task_id |string |任务ID |
|status |string |任务状态枚举：<br><br>in_queue：任务已提交 <br><br>generating：任务已被消费，处理中 <br><br>done：处理完成。注意：只有处理完成，才需要根据algo_status_code查看具体结果！！！否则StatusCode无效！！！<br><br>not_found：任务未找到，可能原因是无此任务或任务已过期(24小时) <br><br>expired：任务已达到设置的过期时间 <br><br>canceled：任务已被取消 <br><br>over_max_retries：已达到最大重试次数 |
|progress |int64 |任务进度（0\-100，仅异步任务返回） |
|req_json |string |提交任务时的原始业务参数 |
|submit_timestamp_ms<br><br> |int64 |任务提交时间（毫秒级时间戳） |
|process_start_timestamp_ms |int64 |任务开始处理时间（毫秒级时间戳） |
|process_end_timestamp_ms |int64 |任务结束时间（毫秒级时间戳，仅任务完成后返回） |
|algo_status_code |int32 |算法状态码 |
|algo_status_message |string |算法错误信息（失败时返回） |
|status_code |int32 |错误码（0为成功，非0需参考错误码文档） |
|status_message |string |状态信息 |


<span id="efzSPA09"></span>
#### 示例

通过task_id查询：

```Shell
curl --location 'http://cv.byteplusapi.com?Action=LumiSync2AsyncBatchGetResults&Version=2025-06-01' \
--header 'Authorization: 你的Authorization' \
--header 'Region: ap-singapore-1' \
--header 'ServiceName: cv' \
--header 'Content-Type: application/json' \
--header 'get-svc: 1' \
--data '{
    "task_ids": ["14468076912309597066"]
}'
```


命令执行完成后，获得以下结果： 

```JSON
{
    "code": 0,
    "message": "",
    "data": {
        "results": [
            {
                "binary_data": [],
                "resp_json": "{\"output_image\": [\"uri://binary_data?index=0\"], \"comfyui_cost\": 133}",
                "status": "done",
                "callback_args": "",
                "progress": 0,
                "req_json": "{\"input_image\":\"uri://binary_data?index=0\",\"input_text\":\"你好呀\",\"seed\":13}",
                "task_id": "14468076912309597066",
                "submit_timestamp_ms": 1748941238332,
                "process_start_timestamp_ms": 1748941238388,
                "process_end_timestamp_ms": 1748941252489,
                "req_key": "hy_test_lumi_onedeploy_mingxinp_v1",
                "algo_status_code": 0,
                "algo_status_message": " <- [返回]消息=Success:Success",
                "status_code": 0
            }
        ]
    },
    "request_id": "202506031700531C156D18803F2533520C"
}
```


<span id="lSpuO2Ux"></span>
### 3.4 批量取消任务 **LumiSync2AsyncBatchCancelTasks**

<span id="oFckKbAv"></span>
#### 3.4.1 功能描述

批量取消未开始处理的异步任务。

<span id="7KppgUy6"></span>
#### 3.4.2 请求参数（CancelTaskReq）


| |参数名 |类型 |是否必填 |说明 |
|---|---|---|---|---|
|**Query** |Action |String |是 |接口名称，值：**LumiSync2AsyncBatchCancelTasks** |
||Version |String |是 |接口版本，值：**2025\-06\-01** |
|**Header**<br><br> |ServiceName |String |是 |cv |
||Region |String |是 |ap\-singapore\-1 |
||Authorization |String |是 |签名密钥，签名方法参考：[https://docs.byteplus.com/en/docs/byteplus-platform/reference-how-to-calculate-a-signature](https://docs.byteplus.com/en/docs/byteplus-platform/reference-how-to-calculate-a-signature) |
||Content\-Type |String |是 |application/json |
|**Body** |task_ids |[]string |是 |待取消的任务ID列表 |


<span id="htZ8OzDS"></span>
#### 3.4.3 响应参数（BatchCancelTaskResp）


|参数名 |类型 |说明 |
|---|---|---|
|failed_task_ids |[]string |取消失败的任务ID列表（通常因任务已开始处理导致） |


<span id="GyhLl2XG"></span>
#### 示例

通过task_id查询：

```Shell
curl --location 'http://cv.byteplusapi.com?Action=LumiSync2AsyncBatchCancelTasks&Version=2025-06-01' \
--header 'Authorization: 你的Authorization' \
--header 'Region: ap-singapore-1' \
--header 'ServiceName: cv' \
--header 'Content-Type: application/json' \
--header 'get-svc: 1' \
--data '{
    "task_ids": ["14468076912309597066"]
}'
```


命令执行完成后，获得以下结果： 

```JSON
{
    "code": 0,
    "message": "",
    "data": {
        "failed_task_ids": []
    },
    "request_id": "202506031713241DA91B56FDF0AA32030D"
}
```


<span id="a2Qg4w5t"></span>
## 四、请求规范

<span id="tUKUK7EG"></span>
### 4.1 数据格式


* **请求体**：使用JSON格式，参数需与接口定义一致（注意字段大小写与文档保持一致，如req_key而非ReqKey）。

* **文件传输**：图片Base64需确保编码正确（不含data:image/...前缀），数据源链接需保证公网可访问。


<span id="F6wRYke3"></span>
### 4.2 错误码解释

<span id="IYtzUWan"></span>
#### 成功 


|StatusCode  |StatusMessage  |说明  |
|---|---|---|
|0  |Success  |成功  |


<span id="QaMt4ySm"></span>
#### 内部错误 


* 算法特定错误码通过code返回。



|StatusCode  |StatusMessage  |说明  |
|---|---|---|
|10000  |Internal Error  |异常内部错误，主要是网关调算法服务的报错，常见是超时  |
|10001  |RPC Internal Error  |下游算法服务异常内部错误，如算法服务调其子服务超时、服务崩溃等  |
|10002  |Downstream RPC Service No Targets Found Error  |网关未发现下游实例导致的报错。 请检查自己的res_quota_name是否填写正确。<br><br>若请求来自于PPE，则只会去发现同机房下游算法实例；若请求来自于非PPE，则只会发现prod环境下游算法实例。  |
|10003  |ECRetryInternal <br><br> |异常内部错误。网关设置了重试，请求打到算法后connect成功但最终因为超时等原因失败报错。  |
|10004 | |缺少req_key，报错： "message": "input validate failed: Key: 'SubmitTaskReq.ReqKey' Error:Field validation for 'ReqKey' failed on the 'required' tag"<br><br>缺少req_json，报错："input validate failed: Key: 'SubmitTaskReq.ReqJson' Error:Field validation for 'ReqJson' failed on the 'required' tag" |
|30402 |ErrCodeBizError |服务异常，请联系答疑同学排查问题 |


<span id="4aARhzFX"></span>
#### 限流错误 


|StatusCode  |StatusMessage  |说明  |
|---|---|---|
|11000  |Req over limit  |请求触发网关限流，一般是因为算法资源不足所以设置限流来保障服务稳定性。  |
|11001  |ECReqConFailed  |算法单实例BACKLOG限流错误。网关设置重试+算法服务设置单实例BACKLOG后，连接失败（1115等连接错误）。 <br><br>一般是因为算法资源不足所以设置限流来保障服务稳定性。  |


 &nbsp;

<span id="hi9e8vUW"></span>
#### 输入错误 


|StatusCode  |StatusMessage  |说明  |
|---|---|---|
|20000  |RPC Process Error: {err_msg}, rpc service err_code={rpc_err_code}  |算法服务识别到的非通用输入错误  |
|21000<br><br>30432<br><br>30400 |Invalid Param <br><br> |参数错误  |
|30404 |FeatNotFound |能力不存在 |
|21001<br><br>30431 |Image Decode Error  |图片解码错误  |
|21002  |Image Empty  |传入图片为空  |
|21003  |Invalid Image  |传入图片算法无法处理  |
|22000  |No Face Detected  |图片中没有检测到人脸  |
|22001  |No Man Detected  |图片中没有检测到人  |


<span id="3c9qdKTR"></span>
#### 审核错误 


|StatusCode  |StatusMessage  |说明  |
|---|---|---|
|23001  |Pre Img Risk Not Pass  |输入图片前审核未通过  |
|23002  |Post Img Risk Not Pass  |输出图片后审核未通过  |
|23003  |Text Risk Not Pass  |输入文本前审核未通过  |
|23004  |Post Text Risk Not Pass  |输出文本后审核未通过  |
|23005  |Post Text Risk Not Pass  |敏感词服务拦截（一般用于版权词审核）  |
|23006  |Pre Video Risk Not Pass  |输入视频前审核未通过  |
|23007  |Post Video Risk Not Pass  |输出视频后审核未通过  |
|23008  |Pre Audio Risk Not Pass  |输入音频前审核未通过  |
|23009  |Post Audio Risk Not Pass  |输出音频后审核未通过  |
|23010  |Pre Image Copyright Not Pass  |输入版权图前审核未通过  |
|23011  |Post Image Copyright Not Pass  |输出版权图后审核未通过  |
|23100  |ECRiskInternal  |审核服务异常  |
|23101  |ECAntidirtInternal  |版权词服务异常  |
|23102  |ECImgCopyrightInternal  |版权图服务异常  |


<span id="4UdJsqx8"></span>
#### 鉴权错误 


|StatusCode  |StatusMessage  |说明  |
|---|---|---|
|24000 |Ability Auth failed  |能力级别认证未通过  |
|30403 |NoFeatAuth |没有能力权限 |
|24001  |Application Auth failed  |通用认证未通过  |
|24002  |Sign Auth failed  |签名错误  |
|24003  |Authorization failed  |访问授权未通过  |
|24004  |SignAuth Time Expired  |验签时间戳过期  |


<span id="MDVYJ6jn"></span>
### 4.3 图片等附件与req_json的顺序对应关系

req_json请求字段中的值uri://binary_data?index=0代表binary_data列表中的索引。如果选择使用data_source传递url作为req_json中某个字段的值，在内部会先转化为binary_data，再匹配对应req_json位置的uri://binary_data?index=

&nbsp;
