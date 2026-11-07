---
title: "Managing bandwidth modes"
product: "FileNAS"
product_code: "nas"
source: "https://docs.byteplus.com/en/docs/nas/Managing_bandwidth_modes"
---

EFS offers two bandwidth modes: baseline and provisioned. This topic explains how to select or change the mode.

<span id="4syadaoG"></span>
## Background information


* The table below compares the two bandwidth modes.

   
   |Mode |**Use cases** |**Performance** |**Billing** |Features |
   |---|---|---|---|---|
   |Baseline Bandwidth |Suitable for the scenario where bandwidth needs to scale with storage capacity to meet basic workload performance needs. |Supports up to 30 GB/s of bandwidth and 900,000 IOPS. |The payment is billed by storage capacity. |It is a traditional performance delivery mode. The performance increases linearly with capacity. |
   |Provisioned Bandwidth |Suitable for the scenario where workloads are predictable. |Supports up to 2 TB/s of read bandwidth and 30 million read IOPS. |For provisioned bandwidth of custom file systems, the payment is billed based on the bandwidth that exceeds the baseline. |* Decoupled capacity and performance: Baseline bandwidth increases linearly with capacity, while provisioned bandwidth can be configured independently.<br><br>* Flexible and on\-demand configuration: Supports online enabling, upgrading, downgrading, and disabling bandwidth based on business needs. Bandwidth value can be adjusted flexibly to meet sudden or long\-term changes in performance demands.<br><br>* Transparent and controllable costs: Only the bandwidth that exceeds the baseline is billed. Storage expenses are reduced. |
   

* For pricing details on both bandwidth modes, see [Billing overview](https://docs.byteplus.com/en/docs/nas/Billing_overview).

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_febc9daf2ba38a154f3cc29b6804f1db.png) </span>



&nbsp;

* Provisioned bandwidth starts at 100 MB/s and can go up to 60,000 MB/s.


<span id="vTAWsQGn"></span>
## Notes

To ensure sustained high\-bandwidth performance and avoid the effects of burst traffic, wait at least one hour between reducing and disabling bandwidth operations. You can perform upgrade operations at any time.

<span id="xHawhhD5"></span>
## Selecting a bandwidth mode


<Tabs>
<Tab zoneid="K7SSiXjOGl" title="Provisioned bandwidth mode">
<TabTitle>Provisioned bandwidth mode</TabTitle>

1. Log in to the [EFS console](https://console.byteplus.com/efs).

2. In the top menu bar, select the region where you want to create the file system.

3. In the left navigation pane, click **File System**.

4. On the **File System** page, click **Create File System**.

5. On the **Create Elastic File System** page, in the **Bandwidth configuration** area, set **Bandwidth mode** to **Provisioned Bandwidth mode** and enter the desired **Provisioned Bandwidth** value. For more information, see [Creating file systems](https://docs.byteplus.com/en/docs/nas/efs_Creating_file_systems).

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">Note   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">After you enter a value for provisioned bandwidth, the corresponding read and write performance is displayed.   </div>
   

6. Click **Next step**.

7. Verify your configurations. Then, check the box that says **I have read and agree to** **The Terms of Storage Products and Service** **and** **Service Level Agreement for Elastic File Storage** **.** 

8. Click **Submit**.


</Tab>
<Tab zoneid="TI9ylObMX8" title="Baseline bandwidth mode">
<TabTitle>Baseline bandwidth mode</TabTitle>

1. Log in to the [EFS console](https://console.byteplus.com/efs).

2. In the top menu bar, select the region where you want to create the file system.

3. In the left navigation pane, click **File System**.

4. On the **File System** page, click **Create File System**.

5. On the **Create Elastic File System** page, in the **Bandwidth configuration** area, set **Bandwidth mode** to **Baseline Bandwidth mode**. For more information, see [Creating file systems](https://docs.byteplus.com/en/docs/nas/efs_Creating_file_systems).

6. Click **Next step**.

7. Verify your configurations. Then, check the box that says **I have read and agree to** **The Terms of Storage Products and Service** **and** **Service Level Agreement for Elastic File Storage** **.** 

8. Click **Submit**.


</Tab>
</Tabs>


<span id="iHcupIcf"></span>
## Viewing bandwidth information


1. Log in to the [EFS console](https://console.byteplus.com/efs).

2. In the top menu bar, select the region of the file system you want to manage.

3. In the left navigation pane, click **File System**.

4. On the File System page, click the file system you want to manage.

5. On the **Overview** page, find bandwidth\-related information, such as **Bandwidth mode**, **Baseline Bandwidth**, and **Provisioned Bandwidth**, in the **Bandwidth** area.


<span id="appe7V6s"></span>
## Changing the bandwidth mode


1. Log in to the [EFS console](https://console.byteplus.com/efs).

2. In the top menu bar, select the region of the file system you want to manage.

3. In the left navigation pane, click **File System**.

4. On the File System page, click the file system you want to manage.

5. On the **Overview** page, click the edit icon next to **Bandwidth mode** in the **Bandwidth** area **.** 

6. In the **Modify bandwidth mode** dialog, select a different **bandwidth mode**.

7. Click **OK**.


<span id="0dJWVKS1"></span>
## Modifying Provisioned Bandwidth


1. Log in to the [EFS console](https://console.byteplus.com/efs).

2. In the top menu bar, select the region of the file system you want to manage.

3. In the left navigation pane, click **File System**.

4. On the File System page, click the file system you want to manage.

5. On the **Overview** page, click the edit icon next to **Provisioned Bandwidth** in the **Bandwidth** area **.** 

6. In the **Modify provisioned bandwidth** dialog, enter the **Provisioned Bandwidth** value.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">Note   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">After you enter a value for provisioned bandwidth, the corresponding read and write performance is displayed.   </div>
   

7. Click **OK**.


&nbsp;
