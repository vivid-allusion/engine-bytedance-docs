---
title: "Implementing custom node scale-in behavior with lifecycle hooks"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Implementing_custom_node_scale-in_behavior_with_lifecycle_hooks"
---

VKE allows you to implement custom actions on nodes by using the lifecycle hook feature of autoscaling groups during node deletion. This topic describes the considerations and procedure for setting up lifecycle hooks for node pools.

<span id="F6xgq0xH"></span>
## Background

When you create a node pool in a VKE cluster, the system automatically creates a scaling group for the node pool. You can configure a custom lifecycle hook in the scaling group to perform defined operations during manual node deletion or automatic scale\-in. For example, you can implement cleanup behavior on nodes when deleting them. For details on lifecycle hooks, see [Lifecycle hook overview](https://docs.byteplus.com/en/docs/as/Overview-of-lifecycle-hooks).

<span id="9WZYEFDE"></span>
## Usage limits


* When using **lifecycle hooks** of scaling groups, consider the following information about billing types of nodes in the node pool:

   * **Pay\-as\-you\-go** instances are recommended.

   * **Subscription** instances are allowed. However, scaling in such instances usually triggers instance shutdown and system reinstallation, which may affect resource cleanup.

   * Changing the billing type of instances within their lifecycles may cause instance release failures and consequent resource idleness.

* A configured lifecycle hook of a node pool works only during node deletion. 


<span id="0V0SMjyb"></span>
## Prerequisites

A node pool has been created. For details, see [Creating node pools](https://docs.byteplus.com/en/docs/vke/Creating-a-managed-NodePool).

<span id="rNq5DNfO"></span>
## Procedure

<span id="hHICdU60"></span>
### Step 1: Create a command


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the left navigation bar, click **Maintenance & Monitoring** \> **Cloud Assistant**.

3. Click the **Custom command** tab. Click **Create custom command** to create a command to run during node deletion.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">This example uses a sleep command. Replace it with your desired command. For details on creating custom commands, see <a href="https://docs.byteplus.com/en/docs/ecs/Managing-Custom-Commands">Managing custom commands</a>.   </div>
   

5. Click **Confirm**.


&nbsp;

<span id="fDKNA0P8"></span>
### Step 2: Create a lifecycle hook


1. Log in to the [Auto Scaling console](https://console.byteplus.com/as).

2. In the left navigation bar, click **Scaling Group**.

3. In the scaling group list, click the name of the scaling group corresponding to the VKE cluster node pool. This opens the scaling group details page.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The scaling group automatically created for a VKE cluster follows the naming format of <code>vke-${Cluster-id}-${Nodepool-id}</code>. You can use the cluster ID or node pool ID to search for the target scaling group.   </div>
   

4. Click the **Lifecycle hook** tab. Click **Create lifecycle hook** to configure a custom lifecycle hook for this node pool. For details, see [Creating lifecycle hooks](https://docs.byteplus.com/en/docs/as/Creating-a-lifecycle-hook).

5. Click **Confirm**.


<span id="v2LnjZzy"></span>
## Validating results

After you configure a custom lifecycle hook for the node pool, manual node deletion or automatic scale\-in triggers that lifecycle hook. Node deletion is performed only after the hook performs the defined actions and ends.

&nbsp;
