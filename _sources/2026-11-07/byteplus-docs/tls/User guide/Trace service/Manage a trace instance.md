---
title: "Manage a trace instance"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/manage_trace_instances"
---

After you create a trace instance, you can view and manage the trace instance in the Torch Log Service (TLS) console.

<span id="查看-trace-实例信息"></span>
## View a trace instance

In the TLS console, view the list of trace instances and the details of a specific trace instance.


1. Log on to the [TLS console](https://console.byteplus.com/tls).

2. In the left\-side navigation pane, choose **Trace** \> **Tracing service**.

   The page displays the list of trace instances. You can view the instance status, description, project, topic, and creation time.

3. Click the name of the target instance, or click **View details** in the **Action** column. The page displays the basic information, integration method, and storage resource ID of the trace instance. The following table describes the instance status:

   
   |Status |Description |
   |---|---|
   |Creating |The trace instance is being created on the back\-end server. |
   |Running |The trace instance is running properly. The trace data can be integrated as expected. |
   |Deleting now |The trace instance is being deleted on the back\-end server. |
   


<span id="删除-trace-实例"></span>
## Delete a trace instance

If a trace instance is no longer needed, you can delete it.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When a trace instance is deleted, TLS deletes the corresponding topics and trace data.</div>



1. Log on to the [TLS console](https://console.byteplus.com/tls).

2. In the left\-side navigation pane, choose **Trace** \> **Tracing service**.

3. Find the target trace instance, then click **Delete** in the **Action** column.

4. In the dialog box, click **OK**.
