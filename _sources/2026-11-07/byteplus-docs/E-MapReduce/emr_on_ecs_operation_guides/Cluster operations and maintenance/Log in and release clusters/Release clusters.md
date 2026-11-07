---
title: "Release clusters"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Release_clusters"
---

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">After the cluster is released, data cannot be recovered. Please operate with caution.</div>


<span id="前置条件"></span>
## prerequisites

Please ensure that the cluster is a Pay\-As\-You\-Go cluster and is in the running, abnormal, or stopped state. Subscription clusters cannot be released.

<span id="操作步骤"></span>
## procedure


1. Log in to [E-MapReduce Console](https://console.byteplus.com/emr/region:emr_fe+ap-southeast-1/home?)

2. In the top menu bar, select the region as appropriate.

3. Click \*\*Resources \> on ECS \*\* to view the cluster list.

4. On the right side of the cluster to be released, click the directory under **operation**, then click **Release cluster.** 

5. In the pop\-up dialog box, select **I am aware of the risks of this operation**, and then click **Confirm.** 


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can also click <strong>Cluster operations \> Release cluster</strong> in the upper right corner of the cluster details page, select <strong>I am aware of the risks of this operation</strong>, and then click <strong>Confirm</strong>.</div>


<span id="释放流程"></span>
## Release process


1. Force termination of all jobs on the cluster.

2. Terminate and release cluster\-related resources, including all ECS instances, cloud disks, and public IP addresses.
