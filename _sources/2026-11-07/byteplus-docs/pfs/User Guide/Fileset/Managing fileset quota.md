---
title: "Managing fileset quota"
product: "Parallel File Storage"
product_code: "pfs"
source: "https://docs.byteplus.com/en/docs/pfs/Managing-fileset-quota"
---

PFS supports setting quotas for the required capacity, file count, IOPS, and bandwidth for Filesets, in order to prevent a single Fileset from occupying excessive resources. This topic introduces the prerequisites and steps for setting Fileset quotas and QoS.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisite

Fileset has been created. For specific steps, please refer to [Create Fileset](https://docs.byteplus.com/docs/pfs/Managing-fileset#%E5%88%9B%E5%BB%BA-fileset).

<span id="e13f2f4f"></span>
## Note


* When the usage capacity reaches the quota threshold, the increment write will be intercepted and the write will be prohibited; when the usage performance reaches the QoS threshold, it will trigger traffic control and ensure that the business performance is within the QoS threshold; To avoid the above scenarios and ensure the business performance of Fileset, it is recommended that you configure Fileset alarm strategies based on the quota threshold. When capacity, number of files, IOPS QoS, and bandwidth QoS are close to the quota threshold, alarm messages should be sent.

* When setting fileset quota, you can click on the [Alarm configuration](https://console.byteplus.com/cloud-monitor/alert/strategy/create?namespace=VCM_vePFS) link in the prompt message to enter the **Create alarm strategy** page, and create a fileset alert policy. For details on the relevant parameters, please refer to [Configuring alarm rules](https://docs.byteplus.com/docs/pfs/Configuring-alarm-rules).


<span id=".5pON5L2c5q2l6aqk"></span>
## **Procedure**


1. Log on to the [PFS console](https://console.byteplus.com/pfs).

2. In the top menu bar, select the region where the target file system is located.

3. Select **File System** \> **Instances** in the left navigation bar. On the Instance List page, click the target file system name.

4. On the instance details page, click **Fileset** tab.

5. On the **Fileset** tab, click the name of the Fileset that needs to be configured with quotas or QoS.

6. In the pop\-up panel, set the following parameters as needed.

   
   |Type |Parameters |Description |
   |---|---|---|
   |Basic information |name |Fileset name, automatically filled.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If you want to modify the Fileset name, please refer to <a href="https://docs.byteplus.com/docs/pfs/Managing-fileset#%E5%85%B6%E4%BB%96%E6%93%8D%E4%BD%9C">Other operations</a>.</div><br> |
   ||Directory path |Fileset directory path, automatically filled, cannot be modified. |
   ||ID |Fileset ID, automatically filled in and cannot be modified. |
   ||inode limit |Inode limit, auto\-fill. |
   |Quota information |Capacity quota |1. Click **Modify** button next to the **Capacity quota**.<br><br>2. In the pop\-up dialog box for editing capacity quota, check the option to enable capacity quota.<br><br>3. Enter the quota data that needs to be set in the **Capacity quota**, and then click **OK**.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="warning">The capacity quota cannot exceed the total capacity of the file system.</div><br> |
   ||File quota |1. Click **Modify** button next to the **File quota**.<br><br>2. In the popped\-up **Edit File Quota** dialog box, check the box to enable **File quota**.<br><br>3. Enter the desired quota data in the file quota, then click **OK**.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="warning">The file quota cannot exceed the iNode limit. If you need a higher file quota, please submit a ticket for application.</div><br> |
   |QoS information |IOPS |1. Click **Modify** next to the **IOPS QoS**.<br><br>2. In the popped\-up **Edit IOPS QoS** dialog box, check the box to enable **IOPS QoS**.<br><br>3. Enter the desired number in the IOPS QoS, then click on **OK**. |
   ||Bandwidth QoS |1. Click **Modify** next to the **Bandwidth QoS**.<br><br>2. In the popped\-up **Edit Bandwidth QoS** dialog box, check the box to enable **Bandwidth QoS**.<br><br>3. Enter the desired number in the Bandwidth QoS , then click on **OK**. |
