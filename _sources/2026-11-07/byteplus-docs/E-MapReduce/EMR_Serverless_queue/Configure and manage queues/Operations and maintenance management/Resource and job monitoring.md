---
title: "Resource and job monitoring"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Resource_and_job_monitoring"
---

EMR Serverless provides queue monitoring capabilities, supporting monitoring of multiple metrics for queues, compute groups, and jobs. After a queue is activated, you can select the corresponding queue in the resource queue list, enter the queue monitoring page from the queue details, and view monitoring data for the relevant metrics.

<span id="ee069281"></span>
# View monitoring metrics


1. After entering the queue monitoring page, you can view monitoring metrics across different dimensions.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b81f160586564793ba00caa223b35dac~tplv-goo7wpa0wc-image.image) </span>

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Among the monitoring metrics related to resource quantity, the core metric definitions include:   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">min_capacity: Resource quantity with fixed capacity.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">capacity: Resource quantity with fixed and elastic capacity.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">allocated: Allocated resource quantity.   </div>
   

   
   |Detailed dimensions |Core monitoring metrics |
   |---|---|
   |Queue |Supports queue\-level monitoring:<br><br><br>* CU resources: For example, CU/GPU/memory allocation, CU/GPU/memory allocation rate, CU/GPU/memory usage rate, and many other metrics.<br><br>* GPU resources: For example, GPU card allocation, GPU card allocation rate, and many other metrics.<br><br>* Job status: For example, number of jobs for the queue dimension, top 20 job CPU allocations, top 20 job memory allocations, and many other metrics. |
   |Compute group |Supports monitoring usage metrics for various compute groups:<br><br><br>* General computing group: CU/GPU/memory allocation amount, CU/GPU/memory allocation rate, CU/GPU/memory usage rate, MGPU\-related monitoring indicators, and more.<br><br>* Presto compute group: Presto Coordinator CPU Used, Presto Coordinator Memory Used, and many other metrics.<br><br>* Spark compute group: Spark Driver CPU usage, Spark Driver CPU usage rate, Spark Driver container memory usage, and many other metrics.<br><br>* Ray compute group: Number of failed tasks in Ray cluster, number of completed tasks in Ray cluster, number of tasks in Ray cluster, and many other metrics. |
   |Job |Supports monitoring queue and compute group metrics for the job dimension. |
   

2. You can set the time range for viewing monitoring metrics according to your monitoring needs. The monitoring pages for compute groups and jobs also support filtering by compute group and job.


<span id="9e5c6050"></span>
# Create monitoring alarms

You can also use cloud monitoring products to create monitoring alarm rules. When the corresponding monitoring alarm rules are triggered, an alarm will be sent to the designated recipient, enabling timely handling of high\-priority alarms. For guidance on configuring monitoring alarm rules, see [Creating an alarm strategy](https://docs.byteplus.com/en/docs/cloudmonitor/Creating-an-alarm-strategy).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ab59dae646fb437a9f6835874dd0140b~tplv-goo7wpa0wc-image.image) </span>
