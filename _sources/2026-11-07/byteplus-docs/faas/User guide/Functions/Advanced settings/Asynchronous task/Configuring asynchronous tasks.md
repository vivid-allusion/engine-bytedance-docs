---
title: "Configuring asynchronous tasks"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/Configuring_async_tasks"
---

The asynchronous task mode is primarily applied to long\-running and compute\-intensive tasks. BytePlus Function Service (veFaaS) provides the asynchronous task mode in both **webserver mode** and **non\-webserver mode**. The primary difference between the two modes lies in whether a webserver is required to process requests in business scenarios. No significant differences exist in business scenarios. This topic describes how to enable the asynchronous task mode in these two modes.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

Code has been locally developed. For details, refer to [Native runtime](https://docs.byteplus.com/en/docs/faas/Native_runtime). For the webserver mode, refer to [Development methods (Web applications)](https://docs.byteplus.com/en/docs/faas/Native_runtime_Development_methods_Web_applications). For the non\-webserver mode, refer to [Development methods (Task)](https://docs.byteplus.com/en/docs/faas/Native_runtime_Development_methods_Task).

<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limits


* Switching between synchronous and asynchronous modes is not supported. You can select whether to enable the asynchronous task mode only during function creation. After the function is created, this configuration cannot be modified or updated.

* Switching between webserver and non\-webserver modes for asynchronous tasks is not supported.

* If the QPS of your task is high, we recommend that you enable the**multiple concurrent requests per instance** feature, or increase the **maximum number of instances** for the current function.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">In non\-webServer mode, a single instance can run only one task at a time (exclusive mode) by default and cannot process multiple concurrent requests.   </div>
   

* Retries are automatically performed only for system errors. User\-initiated tasks cannot be retried.

* The task execution duration can be from 10 seconds to 3 hours. Specify an appropriate timeout duration based on your business requirements.

* When a task times out or a user terminates a task, the response of veFaaS varies slightly based on the following scenarios:

   * For **Webserver mode**:

      * If the multiple concurrent requests per instance feature is disabled, veFaaS will terminate requests and restart the webserver process.

      * If the multiple concurrent requests per instance feature is enabled, veFaaS will only cancel the corresponding requests.

         <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="3">warning         </div>
         

         <div data-tips="true" data-tips-type="warning" data-wrapper-indent="3">Make sure that cancellation signals are handled as expected in the business logic. For example, listen to Context cancellation signals and terminate business logic execution. Otherwise, your business logic may continue to be executed after requests are canceled. As a result, resources will be wasted, or the tasks will not be stopped as expected.         </div>
         

   * In non\-webserver mode, veFaaS will terminate the corresponding task process.

* For completed tasks, the records of execution status can be retained for up to 30 days, or up to 1,000 records of execution status can be retained. The 1000\-record limit and the 30\-day limit are in the **OR** relationship.

* Supported event trigger types include the APIG trigger and the timer trigger.

* The maximum payload of an asynchronous task can be up to 128 KB.


<span id=".5byA5ZCv5byC5q2l5Lu75Yqh"></span>
## Enable the asynchronous task mode

You can perform the following steps to enable the asynchronous task mode:


1. Enable asynchronous tasks when you create a function.

   * **Webserver mode**

      When you create a function, select [Create「Event function」](https://docs.byteplus.com/en/docs/faas/Creating_event_functions) or [Create「Web applications」](https://docs.byteplus.com/en/docs/faas/Creating_Web_applications), and enable asynchronous tasks in the **Advanced settings** section.

   * **Non\-webserver mode**

      When you create a function, select [Create「Task」](https://docs.byteplus.com/en/docs/faas/Creating_tasks). As a result, asynchronous tasks will be automatically enabled.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">We recommend that you enable the <strong>logging feature</strong>. Otherwise, you will not be able to query the execution logs of historical tasks.   </div>
   

2. After you enable the asynchronous task mode, you can specify the **Retries of async task** parameter. The value can be set to 0 to 3. The default value is 0, which indicates that an asynchronous task will not be retried after failure.

3. Click [Release](https://docs.byteplus.com/en/docs/faas/Release_function) to release the function online.


<span id=".5byC5q2l5Lu75Yqh57uT5p6c5Zue6LCD"></span>
## Asynchronous task result callback

After receiving an asynchronous invocation request, veFaaS persists the request and immediately returns a response without waiting for the request execution to complete. If you want to notify downstream services of function asynchronous execution failures, you can configure the result callback feature. After you configure a destination service, veFaaS automatically calls back the service based on the execution result after an asynchronous invocation request is executed.

<span id=".5Zy65pmv5LuL57uN"></span>
### Scenario introduction

Asynchronous task result callbacks apply to the following scenarios:


* Save events that would otherwise be discarded for subsequent use.

   When an asynchronous task fails and still fails after being retried based on the specified policy, you may need to be promptly notified of the task failure and handle it based on your business requirements. In this case, you can configure an asynchronous task result callback to push the failure event to the target service. You can also specify the target service as another function. veFaaS will automatically push the context of failure events to this function and execute your custom error handling logic.

* Automatically notify downstream services of execution results

   After an asynchronous task is executed, you can configure the asynchronous task result callback feature to automatically notify downstream services of the result. These services will perform subsequent operations accordingly. For example, if you have configured veFaaS to automatically decompress ZIP files that are uploaded to BytePlus Torch Object Storage (TOS) and you want to receive notifications after a ZIP file is decompressed, you can configure the asynchronous task result callback feature for the target service.


<span id=".5L2_55So6ZmQ5Yi2"></span>
### Limits


* Only **HTTP\- or HTTPS\-type webhooks** can be specified as the target services for asynchronous invocation.

* Only one target service can be configured.

* Do not call back the function itself to avoid circular calls.

* The payload returned by an asynchronous task in webserver mode can be up to 64 KiB in size. If the upper limit is exceeded, the payload will be truncated in the callback message.


<span id=".5Zue6LCD5raI5oGv5qC85byP"></span>
### Callback message format

The following sample code shows the format of a callback message and the description of each parameter.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">The callback request is in JSON format.</div>


* <div data-tips="true" data-tips-type="default">The <code>requestPayload</code>/<code>responsePayload</code> fields are Base64\-encoded strings, used for compatibility with binary or non\-UTF\-8 payloads.</div>



```json
{
    "version": "1.0", // The callback message version. Fixed value: 1.0.
    "timestamp": 1733998143975, // The time when the callback is initiated, which is a timestamp that is accurate to milliseconds.
    "requestContext": { // The context of the request.
        "requestId": "e4b46cbf-b738-xmpl-8880-********", // The request ID of the asynchronous task.
        "functionName": "my-function", // The function name.
        "condition": "RetriesExhausted", // The invocation error code.
        "approximateInvokeCount": 3 // The number of times that the asynchronous task is executed. When the value is greater than 1, it indicates that veFaaS has retried your task.
    },
    "requestPayload": "eyJ0b3NfYnVja2V0IjoibXktYnVja2V0****", // The original request payload for submitting the task (a Base64-encoded string; the raw bytes of the HTTP Request Body before encoding). If the request body is empty, this field may not exist.
    "responseContext": { // The context of the response.
        "statusCode": 200, // The status code returned by the function in webserver mode. The exit code of the task in non-webserver mode.
        "revisionNumber": 1, // The function revision.
        "functionError": "Unhandled" // The task execution failure information.
    },
    "responsePayload": "ZXJyb3IgZXhlY3V0aW5nIGNvbW1hbmQgYGV4aXQgMWA6IGV4aXQgc3RhdHVzIDEsIHBsZWFzZSBjaGVjayB0aGUgbG9ncyBmb3IgbW9yZSBkZXRh****", // In Webserver mode, indicates the original payload returned by the function (a Base64-encoded string; the raw bytes of the function response Body before encoding); in non-Webserver mode, this field is empty or does not exist.
}
```


<span id=".6YWN572u5byC5q2l5Zue6LCD55uu5qCH5pyN5Yqh"></span>
### Configure target services for asynchronous callbacks


1. Log in to [Function Service Console](https://console.byteplus.com/vefaas).

2. In the left navigation bar, click **Function**. Find the function for which the asynchronous task mode is enabled and click the function name.

3. On the **Function configuration** tab of the function details page, configure the asynchronous task mode.

4. In the **Edit configuration information** panel of the asynchronous task mode, configure target services for asynchronous callbacks.

   
   |Parameter |Description |
   |---|---|
   |Retries of async task |The number of retries for failed asynchronous tasks. Valid values: 0 to 3. |
   |Asynchronous target configuration |Configure target services for asynchronous callbacks.<br><br><br>* **Called on success**: After the asynchronous task is executed, the target service is invoked.<br><br>* **Called on failure**: After the asynchronous task fails to be executed, the target service is invoked.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">Only <strong>HTTP\- or HTTPS\-type webhooks</strong> can be specified as the target services.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">Make sure that the configured <strong>target services</strong> can be accessed over the Virtual Private Cloud (VPC) or the public network.</div><br> |
   

5. Click **Save** to save the configuration.


<span id=".5ZCO57ut5pON5L2c"></span>
## What to do next

Submit the task and invoke the function in asynchronous mode. For details on submitting and terminating tasks, refer to [Task management](https://docs.byteplus.com/en/docs/faas/Async_task_management).
