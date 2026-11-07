---
title: "Managing burst bandwidth"
product: "FileNAS"
product_code: "nas"
source: "https://docs.byteplus.com/en/docs/nas/efs_Managing_burst_bandwidth"
---

To handle increased workload demands, you can enable burst bandwidth for extra temporary bandwidth beyond the baseline and provisioned limits. This topic covers how to enable, view, change, and disable burst bandwidth.

<span id="IPGkQyc0"></span>
## Background information


* The default bandwidth for EFS is the greater of baseline bandwidth and provisioned bandwidth. If the default bandwidth is insufficient, you can obtain temporary burst bandwidth to satisfy business requirements.

* Burst bandwidth can be turned on or off at any time and is off by default. When on, you need to set an upper limit, which is the highest automatic burst bandwidth allowed.

* Please turn on burst bandwidth if the workload's performance peaks are unpredictable or the average throughput is 5% or less of the peak throughput.

* Burst bandwidth can be configured from 100 MB/s to 60,000 MB/s. [Submit a ticket](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000244) if you need more.


<span id="4NWsUfQp"></span>
## Notes

Burst bandwidth fees are based on the actual burst bandwidth used. For more information, see [Billing overview](https://docs.byteplus.com/en/docs/nas/Billing_overview).

<span id="3RMs6t3E"></span>
## Turning on Burst Bandwidth


<Tabs>
<Tab zoneid="1BwfcWL0" title="Turn on burst bandwidth for existing file systems">
<TabTitle>Turn on burst bandwidth for existing file systems</TabTitle>

1. Log in to the [EFS console](https://console.byteplus.com/efs).

2. In the top menu bar, select the region of the file system you want to manage.

3. In the left navigation pane, click **File System**.

4. On the **File System** page, click the file system you want to manage.

5. On the **Overview** page, click the edit icon next to **Burst** **Bandwidth limit** in the **Bandwidth** area.

6. In the **Modify Burst Bandwidth limit** dialog, toggle on the **Burst** **Bandwidth** switch and enter the value for **Burst Bandwidth limit**.

   * Burst bandwidth limit can be configured in increments of 100 MB/s from 100 MB/s to 60,000 MB/s.

   * After you enter a value for Burst bandwidth limit, the corresponding read and write performance is displayed.

7. Click **OK**.


</Tab>
<Tab zoneid="b4QJqmH7" title="Turn on burst bandwidth when creating a file system">
<TabTitle>Turn on burst bandwidth when creating a file system</TabTitle>

1. Log in to the [EFS console](https://console.byteplus.com/efs).

2. In the top menu bar, select the region where you want to create the file system.

3. In the left navigation pane, select **File System**.

4. On the **File System** page, click **Create File System**.

5. On the **Create Elastic File System** page, navigate to the **Bandwidth configuration** section. Then, toggle on the **Burst** **Bandwidth** switch, and enter the value for **Burst** **Bandwidth limit**. For more information, see [Creating file systems](https://docs.byteplus.com/en/docs/nas/efs_Creating_file_systems).

   * Burst bandwidth limit can be configured in increments of 100 MB/s from 100 MB/s to 60,000 MB/s.

   * After you enter a value for burst bandwidth limit, the corresponding read and write performance is displayed.

6. Click **Next step**.

7. Verify your configurations. Then, check the box that says **I have read and agree to** **The Terms of Storage Products and Service** **and** **Service Level Agreement for Elastic File Storage** **.** 

8. Click **Submit**.


</Tab>
</Tabs>


<span id="T5al8JIO"></span>
## Viewing Burst Bandwidth


1. Log in to the [EFS console](https://console.byteplus.com/efs).

2. In the top menu bar, select the region of the file system you want to manage.

3. In the left navigation pane, click **File System**.

4. On the **File System** page, click the file system you want to manage.

5. On the **Overview** page, view the **Burst** **Bandwidth limit** of the file system in the **Bandwidth** area.


<span id="R0Nc6ryY"></span>
## Modifying Burst Bandwidth


1. Log in to the [EFS console](https://console.byteplus.com/efs).

2. In the top menu bar, select the region of the file system you want to manage.

3. In the left navigation pane, click **File System**.

4. On the File System page, click the file system you want to manage.

5. On the **Overview** page, click the edit icon next to **Burst** **Bandwidth limit** in the **Bandwidth** area.

6. In the **Modify Burst** **Bandwidth limit** dialog, enter the value for **Burst** **Bandwidth limit**.

   * Burst bandwidth limit can be configured in increments of 100 MB/s from 100 MB/s to 60,000 MB/s.

   * After you enter a value for burst bandwidth limit, the corresponding read and write performance is displayed.

7. Click **OK**.


<span id="kcZhIf2Z"></span>
## Turning off Burst Bandwidth


1. Log in to the [EFS console](https://console.byteplus.com/efs).

2. In the top menu bar, select the region of the file system you want to manage.

3. In the left navigation pane, click **File System**.

4. On the **File System** page, click the file system you want to manage.

5. On the **Overview** page, click the edit icon next to **Burst** **Bandwidth limit** in the **Bandwidth** area.

6. In the **Modify Burst** **Bandwidth limit** dialog, toggle off the **Burst** **Bandwidth** switch.

7. Click **OK**.
