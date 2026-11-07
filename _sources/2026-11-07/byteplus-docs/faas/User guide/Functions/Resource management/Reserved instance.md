---
title: "Reserved instance"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/Reserved_instance"
---

This article introduces features related to reserved instances.

<span id=".5a6e5L6L57G75Z6L"></span>
## Instance type

Depending on the usage pattern, function instances can be classified as **elastic instances** and **reserved instances**.


* **Event function**, **Web applications**, **tasks**

   
   |Type |Elastic instance |Reserved instance |
   |---|---|---|
   |Features |* The allocation and release of instances are fully managed by the veFaaS system.<br><br>* veFaaS automatically scales instances based on the function's invocation volume, creating instances when calls increase and destroying instances when requests decrease.<br><br>* If an instance does not process requests for a period of time, it will be automatically destroyed.<br><br>* When initiating a call for the first time, the user needs to wait for the instance cold start. |* The allocation and release of instances are fully managed by the user.<br><br>* After starting reserved instances, these instances will remain resident until the user actively releases them.<br><br>* During actual business processing, function invocation requests are preferentially scheduled to reserved instances. When the concurrent requests for the function exceed the processing capacity of the reserved instances, the excess requests are handled by elastic instance that are provisioned on demand. |
   |Application scenarios |Meets regular business scenarios. |Reserved instances eliminate latency caused by cold start and on\-demand elasticity by starting the instance in advance. This is especially suitable for scenarios with high traffic and high response requirements, such as major e\-commerce promotions, live streaming events, and red envelope rain. |
   |Billing |Billing for elastic instances starts when the function request is made and ends when the request is completed. Charges are incurred only when a function call occurs. If there is no function call request, no instances are allocated and no charges are incurred. For specific product pricing and billing, see [product billing](https://docs.byteplus.com/en/docs/faas/Billing_overview). |The billing for reserved instances starts after the instance is successfully created and continues until the user actively releases it. Because the user is responsible for applying for and releasing reserved instances, the user needs to pay for reserved instances as long as they are not released, even if no requests are executed. For specific product pricing and billing, see [product billing](https://docs.byteplus.com/en/docs/faas/Billing_overview). |
   

* **Microservices applications**

   Microservices applications also support both reserved instances and elastic instances. Reserved instances remain resident, while elastic instances are launched as needed. The differences are as follows:

   * The number of reserved instances for microservices applications must be greater than or equal to 1, that is, at least one instance must remain resident.

   * The elastic scaling policy for microservices applications is user\-defined, and veFaaS performs elastic scaling according to the user\-configured policy.

   * Regardless of whether reserved instances or elastic instances are used, **microservices applications are charged according to reserved instance pricing**.


<span id="kRRsGBFP"></span>
## Configure static reserved instances

The configuration of static reserved instances can effectively prevent request latencies caused by the cold start of elastic instances during peak hours of function invocation.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For first\-time configuration of static reserved instances, go to <strong>Release \> Minimum instance count</strong> for configuration.</div>



1. Log in to [Function Service Console](https://console.byteplus.com/vefaas).

2. In the top navigation bar, select the region where your business is located.

3. In the function list, click the target function name to enter the basic information page for the current function.

4. Switch to the **Resource management** page, and in the **Resource limit** section in the **Instance count range**, modify the minimum instance count.

   veFaaS will maintain at least this number of instances for you, running continuously until you stop the application.


<span id=".6YWN572u5a6a5pe25Ly457yp5a6e5L6L5pWw562W55Wl"></span>
## Configure the scheduled scaling policy for instance numbers

When your function has clear periodic patterns or predictable traffic peaks, you can configure scheduled policies based on business characteristics to achieve dynamic scaling of instance counts, improve instance utilization, and solve resource waste problem.


1. Log in to [Function Service Console](https://console.byteplus.com/vefaas).

2. In the top navigation bar, select the region where your business is located.

3. In the function list, click the target function name to enter the basic information page for the current function.

4. Switch to the **Resource management** page, and click **Scheduled policy** area’s **Create**.

5. On the pop\-up page, click **Add scheduled policy** and configure the scheduled scaling instance count policy.

   Multiple scheduled policies are supported. Each function can create up to 10 policies.

   
   |**Parameter** |**Description** |
   |---|---|
   |Policy name |Customize the name of the timed scaling instance number policy.<br><br><br>* The scheduled policy name must be unique and have a length of 1 to 64 characters.<br><br>* The name can contain letters, numbers, hyphens (\-), and underscores (_), but cannot begin with a number, hyphen, or underscore. |
   |Number of reserved instances |Set the number of reserved instances for the function when this policy is triggered.<br><br>The number of reserved instances set cannot exceed the instance range, for example `[0,10]`. |
   |Policy cycle |Select the effective cycle of the scheduled policy.<br><br><br>* Daily: The scheduled policy takes effect during the specified time period each day.<br><br>* Weekly: Check the dates in the calendar week that need to take effect. The scheduled policy takes effect during the specified time period on the selected dates.<br><br>* Monthly: Check the dates in the calendar month that need to take effect. The scheduled policy takes effect during the specified time period on the selected dates. |
   |Start time |Set the start time for the policy from the dropdown time box. |
   |Duration |Set the duration after the timed policy takes effect. The unit is **minutes**. |
   |Policy validity period |Set the validity period of the policy. It is recommended that the validity periods of different scheduled policies do not overlap. |
   

6. View the policy effective time and reserved instance preview chart. After confirming, click **Save**.

7. (Optional) View the status of the scheduled scaling instance count policy.

   * After scheduled policy configuration, it is enabled by default. Subsequent actions such as edit, delete, and turn off are supported.

   * After the scheduled policy effective time is met, the instance count will scale according to the policy. The generated reserved instance names will carry the `reserved` identifier. For more information, see [Resource function statistics](https://docs.byteplus.com/en/docs/faas/Function_resource_statistics#.5a6a5pe2562W55Wl).


<span id="oeLHLdqf"></span>
## View the number of reserved instances

On the resource allocation page, you can view the reserved instance count for all functions in the current region.


1. Log in to [Function Service Console](https://console.byteplus.com/vefaas).

2. In the top navigation bar, select the region where your business is located.

3. In the left navigation bar, click **Function \> Resource allocation**.

4. In the **Allocation details** area, view the value of the target function’s **Instance count range**. The lower limit of the instance count range is the reserved instance count for the current function.


<span id="nqIaOKG8"></span>
## Increase the memory quota for reserved instances

If your function's memory is insufficient, go to the function’s resource management page and increase the instance count to improve memory.


1. Log in to [Function Service Console](https://console.byteplus.com/vefaas).

2. In the top navigation bar, select the region where your business is located.

3. In the function list, click the target function name to enter the basic information page for the current function.

4. Switch to the **Resource management** page. In the **Resource limit** area, at **Instance count range**, modify the upper limit of the instance count.

5. (Optional) If the number of instances to be added exceeds the **Configurable instance limit** on the page, you need to apply for more quota in the [Quota center](https://console.byteplus.com/quota/productList/ParameterList?ProviderCode=vefaas).

   1. Log in [Quota Center](https://console.byteplus.com/quota/productList/ParameterList?ProviderCode=vefaas).

   2. In **Quota Parameter**, select `AccountResource`, and select the region where the instance is located.

   3. Click **Apply** in the Actions column.

   4. Fill in the quota upper limit for the target instance and the reason for the application.

   5. Click **Submit** to complete the quota application.
