---
title: "Configure data flow bandwidth"
product: "Parallel File Storage"
product_code: "pfs"
source: "https://docs.byteplus.com/en/docs/pfs/Configure_data_flow_bandwidth"
---

Data Flow bandwidth defines the maximum throughput capacity for data transfers between PFS and TOS. This parameter must be configured before creating any Data Flow task. This topic shows how to configure Data Flow bandwidth.

<span id="41ef80f9"></span>
## Prerequisites


* The file system has been created. For detailed steps, see [Creating a file system](https://docs.byteplus.com/en/docs/pfs/Creating-a-file-system).

* The TOS bucket has been created. For more information, see [Creating a Bucket](https://docs.byteplus.com/en/docs/tos/docs-create-a-bucket).


<span id="acc720d7"></span>
## Notice


* Setting the Data Flow bandwidth to 0 disables the bandwidth and stops all running Data Flow tasks. However, the tasks will not be deleted. After reconfiguration, you need to manually create a new Data Flow task.

* Data Flow bandwidth is limited by the TOS intranet upload and download bandwidth. For region\-specific master account bandwidth ceilings, see [Restrictions](https://docs.byteplus.com/en/docs/tos/docs-restrictions). Adjust your Data Flow bandwidth according to both TOS performance characteristics and your specific workload requirements. Contact your account manager if you need higher Data Flow bandwidth.


<span id="ab6db57b"></span>
## Steps


1. Log in to the [PFS console](https://console.byteplus.com/pfs).

2. In the top menu bar, select the region of the file system you want to manage.

3. In the left navigation pane, click **File** **System** \> **File** **System** **List**.

4. On the File System page, click the file system you want to manage.

5. On the **Overview** page, click the **Data flow** tab.

6. Click on the **Bandwidth** **configuration** in the corresponding **Actions** column of the **Data** **Flow** **bandwidth** **configuration**.

7. In the **Data Flow bandwidth configuration** dialog, set the **Bandwidth** value.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The configurable range is [500 MB/s, Min (20 GB/s, Maximum write bandwidth of PFS file system)], with increments of 500 MB/s.   </div>
   

8. Click **OK** to save your choices.
