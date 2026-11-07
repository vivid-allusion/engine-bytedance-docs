---
title: "Sandbox instance warm pools"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/Sandbox_instance_warm_pools"
---

The sandbox instance warm pool automatically maintains a group of pre\-started sandbox instances for sandbox applications. This ensures that instances can be allocated within tens of milliseconds after requests to create sandbox instances are initiated. This eliminates cold start.

<span id="J855axbf"></span>
## Feature description

<span id="pwZklefQ"></span>
### Creation workflow

Through the warm pool, the system maintains a group of sandbox instances in the "Ready" state in the background. When you call the [CreateSandbox](https://docs.byteplus.com/en/docs/faas/CreateSandbox) API or create a sandbox instance in the console, the system preferentially allocates instances from the resource pool. This significantly reduces latencies.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_72701d125889755fecd74e11931670a9.png) </span>

<span id="Cxl1zoIp"></span>
### **Core features**


* **Quick allocation**: Instances in the warm pool can be pre\-started and can be used immediately after allocation.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Instances in the warm pool are pre\-started on the <strong>user side</strong>, which consumes resources and incurs corresponding fees. For specific billing details, see <a href="https://docs.byteplus.com/en/docs/faas/Pay-as-you-go#A3MAJE08">Pay\-as\-you\-go \- Cloud sandbox</a>.   </div>
   

* **Disaster recovery**: The warm pool maintains a certain number of pre\-started sandbox instances, which can be directly allocated in the event of extreme disasters.


<span id="bcY3HMJ7"></span>
### Resource pool replenishment logic

To keep the warm pool size at the expected level, the system automatically replenishes resources based on instance consumption. The resource pool replenishment logic of the platform is calculated by using the following formula: `QPS = Resource pool size/Sandbox instance creation time (s)`.

 
&nbsp;

* `Resource pool size`: The number of warm pools set by the user in **Resource quotas**.

* `Sandbox instance creation time`: The average instance creation time obtained through real\-time system monitoring.


The system dynamically adjusts the replenishment speed based on the calculated QPS rate to ensure the resource pool size remains stable.

<span id="50XIeRPK"></span>
## Considerations

After you enable the warm pool, some parameters cannot be modified during sandbox instance creation. Otherwise, the warm pool cannot be matched. For detailed parameters, see descriptions in **Procedure** \> **Step 2**.

<span id="2tqycSbn"></span>
## **Procedure**

<span id="t7hbgfD5"></span>
### **Step 1: Configure the warm pool size**


1. Log in to the [Function Service Console](https://console.byteplus.com/vefaas).

2. In the top navigation bar, select the target region.

3. In the left navigation pane, click **Cloud sandbox ** \> **Sandbox app**. Find the target sandbox application and click its name.

4. On the sandbox application details page, click the **Sandbox instance** tab.

5. In the **Resource quotas** section of the **Sandbox instance** tab, click **Settings** to specify the **Warm pool size** parameter.

6. Click **Confirm** to complete the configuration.

   After the configuration is complete, the system will start as many sandbox instances as specified, with their initial **Start type** set to **Pre\-warmed\-Idle**.


<span id="tL0RCuCF"></span>
### Step 2: Use the sandbox instance warm pool

On the **Sandbox instance** tab, click **Create sandbox instance**. For details, see [Creating sandbox instances](https://docs.byteplus.com/en/docs/faas/Sandbox_instances). At this point, veFaaS will preferentially allocate a **Warmed \- Idle** instance from the warm pool, and its status will change to **Warmed \- allocated**. In addition, the system will immediately start a new sandbox instance to replenish the warm pool to maintain the preset warm pool size.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Take note of the following items when you create a sandbox instance:</div>



* <div data-tips="true" data-tips-type="warning">If you change the <strong>Lifetime</strong> or <strong>Instance metadata</strong> parameters of instances, you can still allocate idle instances from the warm pool.</div>


* <div data-tips="true" data-tips-type="warning">If you modify parameters such as <strong>Instance specification</strong> and <strong>Execution timeout</strong>, idle instances cannot be allocated from the warm pool, and new instances will be created by default.</div>



<span id="23lkdEkK"></span>
## Resource monitoring

On the **Sandbox app** details page, click the **Monitoring** tab. Then, click **Cloud Sandbox Reserved Instance Pool Monitoring** to view the running status and instance allocation status of the warm pool. You can also perform the following operations:


* Click **View more metrics** to go to the Cloud Monitor console and view the monitoring dashboard for the current sandbox application.

* Click **Create alert strategy** to go to the Cloud Monitor console and configure an alert policy for the current sandbox application. When a metric meets the trigger condition for an alert, the system will send an alert notification through your specified method. This helps you promptly identify service exceptions. For specific operations, see [Creating alert policies](https://docs.byteplus.com/en/docs/cloudmonitor/Creating-an-alarm-strategy).
