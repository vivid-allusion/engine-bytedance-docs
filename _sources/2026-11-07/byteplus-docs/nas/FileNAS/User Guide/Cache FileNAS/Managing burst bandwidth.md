---
title: "Managing burst bandwidth"
product: "FileNAS"
product_code: "nas"
source: "https://docs.byteplus.com/en/docs/nas/Managing_burst_bandwidth"
---

To handle increased workload demands, you can enable burst bandwidth for extra temporary bandwidth beyond the baseline and pre\-allocated limits. This topic covers how to enable, view, change, and disable burst bandwidth.

<span id="Gepb1C8F"></span>
## Background information

The default bandwidth for Cache FileNAS is the greater of reference bandwidth and provisioned bandwidth. If the default bandwidth is insufficient, you can obtain temporary burst bandwidth to satisfy business requirements. Burst bandwidth can be turned on or off at any time and is off by default. When on, you need to set an upper limit, which is the highest automatic burst bandwidth allowed. Please turn on burst bandwidth if the workload's performance peaks are unpredictable or the average throughput is 5% or less of the peak throughput.

<span id="B1PDNnv6"></span>
## Notes


* The burst bandwidth feature is available only on Cache FileNAS.

* Burst bandwidth fees are based on the actual burst bandwidth used. For details, see [Billing overview](https://docs.byteplus.com/en/docs/nas/Billing-overview).


<span id="4FdRbwJW"></span>
## Turning on burst bandwidth


<Tabs>
<Tab zoneid="pdCeEWD4D1" title="Turn on burst bandwidth for existing file systems">
<TabTitle>Turn on burst bandwidth for existing file systems</TabTitle>

1. Log in to the [FileNAS console](https://console.byteplus.com/filenas/).

2. In the top menu bar, select the region where the target file system is located.

3. In the left navigation pane, click **File System** \> **File System list**.

4. On the **File System list** page, click the target file system **.** 

5. In the **Performance information** section under the **Overview** tab, click the edit icon next to burst bandwidth to **turn it on** and set the upper limit.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Burst bandwidth starts at 700 MB/s, with a maximum of 60 GB/s and increments of 100 MB/s. When provisioned bandwidth is turned on, burst bandwidth should be at least equal to it.   </div>
   

6. After completing the settings, click **OK**.


</Tab>
<Tab zoneid="h3negTjJ5f" title="Turn on burst bandwidth when creating a file system">
<TabTitle>Turn on burst bandwidth when creating a file system</TabTitle>

1. Log in to the [FileNAS console](https://console.byteplus.com/filenas/).

2. In the top menu bar, select the region where you want to create the file system.

3. In the left navigation pane, select **File System \> File System list**, then click **Create File System**.

4. On the **Create File System** page, set the **File System type** to **Cache FileNAS**, topple the burst bandwidth switch, and set the upper limit. For description of other parameters, see [Creating file systems](https://docs.byteplus.com/en/docs/nas/Creating_file_systems).

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Burst bandwidth starts at 700 MB/s, with a maximum of 60 GB/s and increments of 100 MB/s. When provisioned bandwidth is turned on, burst bandwidth should be at least equal to it.   </div>
   

5. After completing the settings, click **Confirm order**.

6. On the details page, read and check **The Terms of Storage Products and Services**, and click **Buy now**.


</Tab>
</Tabs>


<span id="7hBaXJ0Y"></span>
## Viewing burst bandwidth


1. Log in to the [FileNAS console](https://console.byteplus.com/filenas/).

2. In the top menu bar, select the region where the target file system is located.

3. In the left navigation pane, click **File System** \> **File System list**.

4. On the **File System list page**, click the target file system and navigate to the **Overview** tab to see the **Performance information** section, where you can view reference bandwidth, DataFlow bandwidth, provisioned bandwidth, and burst bandwidth.


<span id="PZhyVaMK"></span>
## Modifying burst bandwidth


1. Log in to the [FileNAS console](https://console.byteplus.com/filenas/).

2. In the top menu bar, select the region where the target file system is located.

3. In the left navigation pane, click **File System** \> **File System list**.

4. On the **File System list** page, click the target file system **.** 

5. In the **Performance information** section under the **Overview** tab, click the edit icon next to burst bandwidth to set its upper limit.

6. After completing the settings, click **OK**.


<span id="mxcx4HtB"></span>
## Turning off burst bandwidth


1. Log in to the [FileNAS console](https://console.byteplus.com/filenas/).

2. In the top menu bar, select the region where the target file system is located.

3. In the left navigation pane, click **File System** \> **File System list**.

4. On the **File System list** page, click the target file system **.** 

5. In the **Performance information** section under the **Overview** tab, click the edit icon next to burst bandwidth to turn it off.

6. After completing the settings, click **OK**.
