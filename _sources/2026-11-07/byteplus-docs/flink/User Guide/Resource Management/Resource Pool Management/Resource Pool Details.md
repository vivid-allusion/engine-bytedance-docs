---
title: "Resource Pool Details"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/Resource_Pool_Details"
---

After the resource pool is created, you can view the resource pool information at any time.

<span id="1d973b33"></span>
## Operation Steps


1. Log in to [BytePlus Flink Console](https://console.volcengine.com/flink).

2. Select the target region from the top menu bar.

3. In the left sidebar, select **Project Management**, then search and click on the project block to enter the project.

4. In the project's left sidebar, select **Resource Management**, then click the **Resource Pool** tab.

5. On the resource pool list page, filter for the target resource pool, then click on the resource pool name.

6. View resource pool information.

   You can view information about the resource pool's status, computing resource utilization, type of resource pool, region, availability zone, network, storage, and billing.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/28914e7e92a04fd4b1f82409ee6f9069~tplv-goo7wpa0wc-image.image) </span>

<span id="1dc89434"></span>
## Add Subnet

During the runtime of the current Flink job, private network IP resources of the resource pool will be utilized. Each Flink job or Session cluster's JobManager and TaskManager will occupy one IP. If a Flink job occupies too many IPs from the resource pool's subnet, resulting in insufficient remaining IP numbers, you can perform the following operations


1. Log in to [BytePlus Flink console](https://console.volcengine.com/flink).

2. Select the target region from the top menu bar.

3. In the left navigation bar, select **Project Management**, then search and click on the project block to enter the project.

4. In the left navigation bar of the project, select **Resource Management**, then click **Resource Pool** tab.

5. On the resource pool list page, filter the target resource pool, then click on the resource pool name.

6. Click the edit button of the subnet in the network information.

7. At this moment, in the Add Subnet dialog, you can either select a new subnet or click the Create Subnet button to create a new one.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5c1a8efbc77e4a74b5130941d0cd5ac6~tplv-goo7wpa0wc-image.image) </span>

> Note: When scheduling Flink tasks, any subnet may be used randomly, so ensure that the security groups, upstream and downstream whitelists, and other settings of the two subnets are consistent.

> If partial network issues occur after submitting a Flink task, where some connections fail while others succeed. This could be due to different network configurations between subnets; please carefully check the network settings.


<span id="df263f12"></span>
## DNS Settings

If the services your Flink job depends on are specified by domain names, migrating to the BytePlus Flink service might result in an error stating that the domain name could not be resolved. At this point, you can use the DNS settings feature in the resource pool settings to manually add the domain name configuration.


1. Log into [BytePlus Flink console](https://console.volcengine.com/flink).

2. Select the target region from the top menu bar.

3. In the left navigation bar, select **Project Management**, then search and click the project block to enter the project.

4. In the project's left navigation bar, select **Resource Management**, then click on the **Resource Pool** tab.

5. On the resource pool list page, filter for the target resource pool, then click on the resource pool name.

6. Click on the **DNS Configuration \-\> Add Domain** button in the Network Information.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/92def09bbea740abbed0222ba747ff82~tplv-goo7wpa0wc-image.image) </span>


7. In the pop\-up Domain Information dialog, set the domain and IP information, then click the **OK** button to save.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a6781d49893442eba3ee27e9efb6c111~tplv-goo7wpa0wc-image.image) </span>


8. Note that after successful saving, if you need to access the configured domain, you must restart the existing BytePlus Flink tasks.
