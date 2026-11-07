---
title: "Operation logs"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Operation_log"
---

EMR Serverless queues provide the operation log feature, allowing you to view detailed operation logs for queues and compute groups within queues on this page. This helps you trace operation history and perform operation auditing.

<span id="ba1a0b21"></span>
# Context

Currently, in EMR Serverless:


* EMR Serverless public queues: Operation logs cannot be viewed. Since public queues cannot be directly modified, operation logs are not required for public queues.

* EMR Serverless Subscription dedicated queues: Operation logs can be viewed, including operations for queues and compute groups.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This document introduces the operation log feature for EMR Serverless queues. EMR Serverless instances support the operation auditing feature, which differs from the operation log feature described in this document.</div>


The list of supported operation events is as follows.


|Detailed operation object types |List of supported operation events |
|---|---|
|Queue |* Create order<br><br>* Create resource<br><br>* Resource renewal<br><br>* Resource configuration change (records configuration change details)<br><br>* Resource shutdown<br><br>* Expiration release/manual unsubscribe: When the operator is the system, it is expiration release; when the operator is a user name, it is manual unsubscribe.<br><br>* Configuration changes: availability zone, network connection, and storage mount. |
|Compute group |* Create compute group<br><br>* Stop compute group<br><br>* Start compute group<br><br>* Update compute group: including editing various configuration items of the compute group<br><br>* Save compute group: Save image<br><br>* Delete compute group<br><br>* Update, delete queue, VEPFS, and related operations: |


<span id="afeac640"></span>
# View operation log details


1. After logging in to the EMR console, in EMR Serverless queues, click the name of an EMR Serverless Subscription dedicated queue to enter the queue details page.

2. On the left side of the queue details page, click “Operation logs” to enter the operation log page. On this page, you can view the list of operations for the current queue or compute group.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a7b482fea71b476591703c8c1d0a5484~tplv-goo7wpa0wc-image.image) </span>

   * You can quickly filter operation events by operation start time range, compute group name, or operator.

   * You can view summary information for each operation in the operation event list, such as operator, operation start/end time, operation status (whether completed), and more.

   * For completed operations, click “Procedure details” after the operation event to view the detailed procedure list involved in the operation. Click the corresponding sub\-procedure to view the detailed log for that procedure.
