---
title: "One-click repair for local disk failures"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/one_click_repair_for_local_disk_failures"
---

Volcano Engine EMR has optimized the maintenance operations for hard disk anomaly events that you may encounter when using ECS local disk instances (local SSD type, big data type). Complex local disk maintenance operations can be completed with a single click. To manually perform local disk failure recovery due to business requirements, refer to: [EMR local disk instance failure maintenance ](https://docs.byteplus.com/docs/E-MapReduce/105398)[EMR local disk instance failure maintenance](https://docs.byteplus.com/en/docs/E-MapReduce/One-click_repair_for_local_disk_failures).

<span id="cb4ddcaa"></span>
# Trigger scenarios

Hard disk anomaly events are received in the EMR Console Maintenance Center.

<span id="210dc54c"></span>
# Procedure


1. Log in to [E-MapReduce Console](https://console.byteplus.com/emr/region:emr_fe+ap-southeast-1/home?).

2. Click **Maintenance Center \>**  **Instance maintenance**, then select the appropriate maintenance operation based on your business requirements.

   
   |Business requirements |Recommended maintenance operations |
   |---|---|
   |The business and data stored on this node **are fault tolerant** (it is acceptable to release the node and lose the data on the local disk of this node), such as compute nodes in compute\-storage separation clusters, remote shuffle nodes, or nodes with configured elastic scaling rules, and all data stored on the local disk is **temporary data**. |Scale in the faulty node and scale out a node with the same configuration |
   |If the above conditions are met but **the node IP or instance ID needs to be retained** |Redeploy the faulty node |
   |The business running on this node has low fault tolerance (releasing the node will cause irreversible impact on the business), or this node is used to store persistent data, such as HDFS nodes or compute\-storage integrated nodes, and it is necessary to **retain the data on other non\-faulty local disks of the node**. |Isolate and replace the faulty disk |
   

3. Select the appropriate maintenance operation and confirm the risks. Click **Confirm** to enter the automated maintenance phase.

   
   |Maintenance operations |Risk warning |
   |---|---|
   |Scale in the faulty node and scale out a node with the same configuration |The **HDFS data on this node will be replicated after maintenance is completed**, **all other data will be lost. Please back up your data in advance** to prevent data loss, for example, by backing up to Elastic Block Storage (EBS) or Object Storage (TOS).<br><br>The ECS instance under maintenance is temporarily unavailable. Scaling operations for the node are expected to take 5 minutes. |
   |Redeploy the faulty node |The **HDFS data on this node will be replicated after maintenance is completed**, **all other data will be lost. Please back up your data in advance** to prevent data loss, for example, by backing up to Elastic Block Storage (EBS) or Object Storage (TOS).<br><br>The ECS instance under maintenance is temporarily unavailable. After redeployment, the IP address of this ECS instance will remain unchanged. Redeploying the instance is expected to take 5 minutes. |
   |Isolate and replace the faulty disk |The **HDFS data on the faulty disk will be replicated after maintenance is completed**, **all other data will be lost. Please back up your data in advance** to prevent data loss, for example, by backing up to Elastic Block Storage (EBS) or Object Storage (TOS).<br><br>When isolating the faulty disk, services on the node will be briefly stopped.<br><br>The local disk under maintenance is temporarily unavailable. This does not affect the operation of hardware, services, or processes on the ECS instance that are unrelated to this local disk. Replacing the faulty disk is expected to take 3 business days. |
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">To redeploy the faulty node or isolate and replace the faulty disk, after maintenance is completed, EMR will restore your services and you can continue to use the node as normal. To shrink the faulty node and expand a node with the same configuration, after maintenance is completed, you can continue to use the replacement node as normal.   </div>
   

4. During maintenance, you can click Maintenance Details to view the maintenance progress.
