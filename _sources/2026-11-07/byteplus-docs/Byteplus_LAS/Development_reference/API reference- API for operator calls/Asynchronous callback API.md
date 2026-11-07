---
title: "Asynchronous callback API"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Asynchronous_callback_API"
---

LAS operators provide asynchronous callback capabilities via asynchronous interfaces. You can set the callback parameter `callback.url` when initiating an operator task. When the task status changes, LAS will send an HTTP POST notification to this URL.

<span id="d2710b61"></span>
# Caution


* The asynchronous callback capability applies to operators with asynchronous tasks. Typically, asynchronous task operators submit tasks through the submit interface and poll the task processing status via the poll interface. Using the callback capability reduces polling frequency and allows you to receive timely updates on task status through proactive notifications from LAS.

* Currently, callback functionality is being gradually enabled for asynchronous task operators. Supported operators include: las_asr_pro, las_video_super_resolution, las_video_seedance_replace, las_viral_clip_gen, las_video_scene_seg, las_video_translate.

* The callback mechanism is a best\-effort notification mechanism and does not provide strict reliability, exactly\-once delivery, or strict ordering guarantees. In certain scenarios, such as network issues, the receiving end may not properly obtain the task status. LAS implements a retry mechanism for sending messages, but success cannot be guaranteed. Therefore, when using the callback feature, it is recommended to supplement with fallback logic using the poll interface.


<span id="e96dd886"></span>
# Usage instructions

<span id="7ce66cbb"></span>
## Invocation process


1. The user calls `/api/v1/submit` to submit an asynchronous task and passes in `callback.url`.

2. LAS returns `task_id`, and the user saves this `task_id`.

3. After the task status changes, LAS sends a POST notification to the `callback.url` configured by the user.

4. Upon receiving the callback, the user processes it idempotently based on `task_id`.

5. If the callback is not received, the user should still use `/api/v1/poll` to query the task status.


<span id="035ff1bb"></span>
## `callback.url` configuration requirements


|Rules |Note |
|---|---|
|Protocol |By default, only `https://` is allowed. |
|Host |A valid host must be present. |
|Userinfo |Userinfo is not allowed in the URL, for example, `https://user:pass@example.com/cb`. |
|Localhost |`localhost` or `. localhost` are not allowed. |
|Address accessibility |The URL must be a public address accessible by the LAS service. |
|Redirect |LAS does not follow HTTP redirects. The callback URL must be able to directly receive POST requests. |
|Response time |It is recommended that the user service returns a 2xx response within 5 seconds. |


<span id="7ec24341"></span>
## Callback message format and fields

LAS will send an HTTP POST to the `callback.url` provided by the user.

<span id="757d04db"></span>
### Request headers

```Plain
Content-Type: application/json; charset=utf-8
```


The user side should process idempotently based on `metadata.task_id`.

<span id="efdf68d3"></span>
### Body fields


|Field |Type |Note |
|---|---|---|
|`metadata.task_id` |string |Asynchronous task ID. It is recommended that users use this as the idempotency key. |
|`metadata.task_status` |string |Final status of the task. Possible values include:<br><br><br>* `PENDING`: The task has been submitted and is waiting to be executed.<br><br>* `RUNNING`: The task is in progress.<br><br>* `COMPLETED`: The task completed successfully. The response usually contains `data`.<br><br>* `FAILED`: The task failed. Error information is provided in `metadata.business_code` and `metadata.error_msg`. |
|`metadata.business_code` |string |Business error code. Success is usually `0`. |
|`metadata.error_msg` |string |Error message. The error message is an empty string when the task is successful. |
|`data` |object |Required. Included only when the task is successful and the server\-side policy enables `include_data`. The content depends on the specific operator result. |


<span id="2c89975e"></span>
### Callback message handling recommendations


1. Parse the JSON body.

2. Verify that `metadata.task_id` is not empty.

3. Check locally whether `task_id` has already been processed.

4. If already processed, return `2xx` directly.

5. If not processed, record the complete callback body in the database.

6. Update the local task status based on `task_status`.

7. Return `2xx` promptly. For longer processing chains, it is recommended to place them in your own asynchronous queue.


<span id="c46494b7"></span>
## Examples

<span id="90b2ff36"></span>
### Submit task example

```JSON
{
  "operator_id": "las_xxx",
  "operator_version": "v1",
  "data": {
    "input": "..."
  },
  "callback": {
    "url": "https://example.com/las/callback"
  }
}
```


<span id="902d346f"></span>
### Callback request example

LAS will send an HTTP POST to the URL provided by the user.

<span id="d1e3eed1"></span>
#### Successful task example

```JSON
{
  "metadata": {
    "task_id": "task_xxx",
    "task_status": "COMPLETED",
    "business_code": "0",
    "error_msg": ""
  },
  "data": {
    "result": "..."
  }
}
```


<span id="51412b35"></span>
#### Failed task example

```JSON
{
  "metadata": {
    "task_id": "task_xxx",
    "task_status": "FAILED",
    "business_code": "Server.InternalError",
    "error_msg": "..."
  }
}
```


<span id="4e52102c"></span>
# Complete demo

The following provides code skeletons for building a callback receiving service in mainstream programming languages. You can directly download the corresponding demo and use it as a foundation for integrating and developing your callback receiving service.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For programming languages without a provided demo, you can adapt the code based on the documentation, examples, and existing language demo samples.</div>



* **Java：** 

   <Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6fda22fc4e3d499498f6f45306feeec9~tplv-goo7wpa0wc-image.image" name="las-user-callback-example-java.zip">las-user-callback-example-java.zip</Attachment>
   

* **Python：** 

   <Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/44c5bcd3ce40448c8cbcf6f97cc1cb05~tplv-goo7wpa0wc-image.image" name="las-user-callback-example-python.zip">las-user-callback-example-python.zip</Attachment>
   

* **Golang：** 

   <Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a17e7415e6b54993ad620ff9ddfed312~tplv-goo7wpa0wc-image.image" name="las-user-callback-example-go.zip">las-user-callback-example-go.zip</Attachment>
   


<span id="61fe260e"></span>
# Common failure issues


|Issue |Symptoms |Recommended solution |
|---|---|---|
|The operator does not currently support callback |Submit returns `Parameter.Invalid`, indicating that callback is not enabled. |The current operator does not support the callback capability. It is recommended to use the poll interface to periodically check the task status and obtain the operator's processing results. |
|URL is not HTTPS |Submit returns `Url.Invalid` or `Parameter.Invalid`. |Please use a URL in HTTPS format. URLs in HTTP format pose security risks and are not recommended. If HTTP is required, you need to [submit a ticket](https://console.byteplus.com/workorder/create?ref=L2xhcy9yZWdpb246bGFzK2FwLXNvdXRoZWFzdC0xL25leHQvaG9tZQ%3D%3D) to apply for inclusion in the allowlist, so that the LAS server\-side policy can be relaxed. |
|URL points to localhost or an internal network address |Submit or sending is rejected. |Use a publicly accessible HTTPS address. |
|User service returns 4xx |LAS does not retry. |Correct the authentication, path, and request body parsing logic of the user callback interface. |
|User service processing exceeds 5 seconds |LAS may time out and retry. |The interface should quickly write to the database and return a response, and handle time\-consuming logic asynchronously. |
|The task is completed but the callback was not received |No notification. |Use `/poll` as a fallback query; troubleshoot URL reachability and user service logs. |
|Duplicate callback received |The same `task_id` is received multiple times. |Process requests idempotently based on `task_id`; return 2xx for duplicate requests. |
