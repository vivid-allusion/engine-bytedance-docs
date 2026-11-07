---
title: "Managing provisioned bandwidth"
product: "FileNAS"
product_code: "nas"
source: "https://docs.byteplus.com/en/docs/nas/Managing_provisioned_bandwidth"
---

With provisioned bandwidth, you can increase the bandwidth of your file system without expanding your storage capacity. This enables you to scale capacity and performance independently. This topic covers how to enable, view, change, and disable provisioned bandwidth.

<span id="a3459a13"></span>
## Background information

By default, DataFlow uses up to 30% of the FileNAS file system bandwidth. Therefore, enabling provisioned bandwidth increases the bandwidth of both the file system and DataFlow. The calculation formula is as follows:


* File system bandwidth = Max (Reference bandwidth, provisioned bandwidth)

* DataFlow bandwidth = Max (Reference bandwidth, provisioned bandwidth) × 0.3


Provisioned bandwidth affects billable storage capacity. For each 1 MB/s of bandwidth provisioned, billable storage capacity is reduced by 5 GiB. The calculation formula is as follows:


* Billable capacity reduction = (Min (Reference bandwidth, provisioned bandwidth) – 600) × 5 GiB

* Billable capacity after reduction = Current billable capacity – Billable capacity reduction


If the min (reference bandwidth, provisioned bandwidth) is less than 600, there will be no change to the billable storage capacity.

<span id="8cb93b0f"></span>
## Notes


* The provisioned bandwidth feature is available only on Cache FileNAS.

* Provisioned bandwidth fees are based on the actual bandwidth used. For details, see [Billing overview](https://docs.byteplus.com/en/docs/nas/Billing-overview).


<span id="18a4d36d"></span>
## Enabling provisioned bandwidth


<Tabs>
<Tab zoneid="bZZevuOu4t" title="Turn on provisioned bandwidth for existing file systems">
<TabTitle>Turn on provisioned bandwidth for existing file systems</TabTitle>

1. Log in to the [FileNAS console](https://console.byteplus.com/filenas/).

2. In the top menu bar, select the region where the target file system is located.

3. In the left navigation pane, click **File** **System** \> **File** **System** **list**.

4. On the **File System list** page, click **Change** in the **Actions** column of the target file system.

5. On the **Change** page, enable **Provisioned bandwidth** and enter a value.

   The provisioned bandwidth ranges from 700 to 60,000 MB/s in increments of 100 MB/s. The maximum bandwidth must be based on the available capacity of the cluster.

   After configuring the provisioned bandwidth, you can view the provisioned bandwidth, DataFlow bandwidth, billable capacity reduction, and billable capacity after reduction in the **Changed configuration** section of the **Change** page.

6. After completing the settings, click **Confirm order**.

7. On the details page, read and check **The Terms of Storage Products and Services**, and click **Buy now**.


</Tab>
<Tab zoneid="fbBiNdQxvi" title="Turn on provisioned bandwidth when creating a file system">
<TabTitle>Turn on provisioned bandwidth when creating a file system</TabTitle>

1. Log in to the [FileNAS console](https://console.byteplus.com/filenas/).

2. In the top menu bar, select the region where you want to create the file system.

3. In the left navigation pane, select **File System** \> **File System list**, then click **Create File System**.

4. On the **Create File System** page, set the **File System type** to **Cache FileNAS**, topple the **Provisioned Bandwidth** switch, and set the upper limit. For description of other parameters, see [Creating file systems](https://docs.byteplus.com/en/docs/nas/Creating_file_systems).

   The provisioned bandwidth ranges from 700 to 60,000 MB/s in increments of 100 MB/s. The maximum bandwidth must be based on the available capacity of the cluster.

5. After completing the settings, click **Confirm order**.

6. On the details page, read and check **The Terms of Storage Products and Services**, and click **Buy now**.


</Tab>
</Tabs>


<span id="9e765df6"></span>
## Viewing provisioned bandwidth


1. Log in to the [FileNAS console](https://console.byteplus.com/filenas/).

2. In the top menu bar, select the region where the target file system is located.

3. In the left navigation pane, click **File System** \> **File System list**.

4. On the **File System list** page, click the target file system and navigate to the **Overview** tab to see the **Performance information** section, where you can view reference bandwidth, DataFlow bandwidth, and provisioned bandwidth.


<span id="279d31ad"></span>
## Changing provisioned bandwidth

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">To ensure sustained high\-bandwidth performance, wait at least one hour between bandwidth reduction and disable operations. Upgrade operations can be done at any time without restrictions.</div>



1. Log in to the [FileNAS console](https://console.byteplus.com/filenas/).

2. In the top menu bar, select the region where the target file system is located.

3. In the left navigation pane, click **File System** \> **File System list**.

4. On the **File System list** page, click **Change** in the **Actions** column of the target file system.

5. On the **Change** page, modify the provisioned bandwidth value.

6. After completing the settings, click **Confirm order**.

7. On the details page, read and check **The Terms of Storage Products and Services**, and click **Buy now**.


<span id="9335d698"></span>
## Disabling provisioned bandwidth


1. Log in to the [FileNAS console](https://console.byteplus.com/filenas/).

2. In the top menu bar, select the region where the target file system is located.

3. In the left navigation pane, click **File System** \> **File System list**.

4. On the **File System list** page, click **Change** in the **Actions** column of the target file system.

5. On the **Change** page, topple the provisioned bandwidth switch to disable it.

6. After completing the settings, click **Confirm order**.

7. On the details page, read and check **The Terms of Storage Products and Services**, and click **Buy now**.
