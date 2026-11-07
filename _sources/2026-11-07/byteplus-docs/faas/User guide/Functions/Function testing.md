---
title: "Function testing"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/Function_testing"
---

After the function is released, you can initiate a function test in the console. The FaaS will simulate sending a request from the specified trigger to your live function and display the test results, verifying whether the function's behavior meets expectations.

<span id="background-information"></span>
## Background Information

Currently, FaaS supports both synchronous calls and async tasks. If the async task feature is not enabled, the default call method is synchronous.

<span id="prerequisites"></span>
## Prerequisites

The function has been successfully released. For specific operations, refer to [Release function](https://docs.byteplus.com/en/docs/faas/Release_function).

<span id="usage-limit"></span>
## Usage limit


* Only supports online testing for released function revisions. If you wish to test the updated function code, the updated code needs to be released online first.

* Trigger test requests must be in JSON format.

* When there are canary revisions of the function, the test requests will be sent randomly to new and old versions based on the traffic proportion.

* For synchronous calls, online testing is not supported for functions with execution times exceeding 30 seconds, and an execution timeout error will be returned.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The function service currently supports synchronous calls and async tasks. Functions without active async tasks default to synchronous call methods.   </div>
   

* In APIG trigger test requests, the method must be in uppercase.


<span id="procedure-steps"></span>
## Procedure steps


1. Log in to the [Function Service console](https://console.byteplus.com/vefaas).

2. On the top navigation bar, select the target region.

3. On the **Function** page, select the function you need to test and click on the function name.

4. On the function detail page, click **Test** in the upper right corner.

5. In the **Function test** panel, select the trigger type for testing.

6. (Optional) Modify the default test request as needed. Changes must comply with JSON format.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Reset: Resets the test request to the default.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Format: Formats multiple JSON data on the same line in an organized manner.   </div>
   

7. Click **Test** to start the function test.


<span id="operation-result"></span>
## Operation result


* **Function test succeeded**

   * For functions without async tasks enabled, the default is synchronous calling. The console will display an execution summary (including CPU usage during the request, function memory usage, and function execution duration) and the function's response result.

   * For functions with async tasks enabled, the console will return a RequestID. Click **View details** to jump to the async task list and view the current task's execution details.

* **Function test failed**

   The console will display the execution log, making it easier to diagnose the cause of the failure.
