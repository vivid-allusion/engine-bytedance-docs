---
title: "Expanding a file system"
product: "Parallel File Storage"
product_code: "pfs"
source: "https://docs.byteplus.com/en/docs/pfs/Expanding-a-file-system"
---

If the current storage capacity of the file system cannot meet your business requirements, you can choose to expand the file system to avoid issues such as inability to write data due to insufficient capacity. This topic introduces the precautions and steps for expanding the file system.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Note</div>



* <div data-tips="true" data-tips-type="warning">When the file system is at a high water level, there may be a high degree of file fragmentation, slow disk addressing, and other phenomena, which may result in reduced performance of the file system. It is recommended that you plan for capacity expansion before the file system reaches 90%.</div>


* <div data-tips="true" data-tips-type="warning">PFS currently does not support scaling down the file system.</div>



<span id=".5pWw5o2u5Z2H6KGh"></span>
## Data balancing

PFS supports the configuration data balance function during capacity expansion, but there are the following issues with data balance. It is recommended that you perform the operation during off\-peak hours of your business.


* The process of data balancing will consume the network and disk bandwidth of storage nodes, resulting in a decrease in the front\-end IO performance of the file system.

* The more existing data there is in the file system, the longer it takes to balance the data. Considering most businesses do not require automatic data balancing after capacity expansion, the existing data will still be stored on the original storage nodes and will not be automatically migrated to the newly expanded storage nodes.


<span id=".5pON5L2c5q2l6aqk"></span>
## **Procedure**


1. Log on to the [PFS console](https://console.byteplus.com/pfs).

2. In the top menu bar, select the region where the target file system is located.

3. Select **File System** \> **Instances** in the left navigation bar. on the Instance List page, click **Expand** in the **Actions** column of the target file system.

4. On the **File System Expansion** page, set the expansion parameters.

   
   |**Parameters** |**Description** |
   |---|---|
   |Billing type |Default display, no need to set. |
   |Current capacity |Default display, no need to set. |
   |New Capacity |Select the new capacity that needs to be expanded, and the expanded capacity must be greater than the original capacity. The expansion step and capacity limit of PFS file systems with different specifications are different. For detailed information, please refer to [Product specifications](https://docs.byteplus.com/docs/pfs/Product-specifications).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Tip</div><br><br><br><div data-tips="true" data-tips-type="tip">We recommend expanding the used capacity from 50% to 100%.</div><br> |
   |Data balance |Choose whether to enable data balancing function.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Note</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">After checking, data balancing will be immediately enabled after PFS capacity expansion.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">Due to the fact that the data balancing process consumes network and disk bandwidth of storage nodes, resulting in a performance decrease of the file system, it is recommended that you evaluate your business requirements and enable it cautiously.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">The time for data balancing is mainly affected by the amount of existing data. If you have a large amount of existing data, the time for balancing may be longer. We recommend that you perform the operation during off\-peak hours and be patient while waiting.</div><br> |
   

5. Click **Confirm order**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">Tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you have enabled the data balancing feature, after expanding the file system, you can view the status of data balancing on the instance overview page. For detailed instructions, please refer to <a href="https://docs.byteplus.com/docs/pfs/Data-balancing">Data balancing</a>.   </div>
   

6. On the **Details** page, confirm the file system parameters, read and check the **Storage Products and Services Terms**, and click **Buy now**.

7. After confirming that the information is correct, click **Next step**.
