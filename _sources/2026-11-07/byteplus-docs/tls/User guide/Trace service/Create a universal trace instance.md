---
title: "Create a universal trace instance"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/create_a_trace_instance"
---

Before accessing trace storage, you need to create a trace instance in TLS to manage collected trace data.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information

A trace instance is a trace data computing resource provided by TLS. It is used to manage collected trace data. You can view and analyze collected trace data from the dimension of trace instance in the TLS console.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Before using trace storage for the first time, you must authorize access to cloud resources. That is to say, you need to grant the ServiceRoleForTls role permission for TLS to access and write resources. If authorization has not yet been granted, TLS will guide you through the process when you create a trace instance in the console. We recommend that you use the Volcengine primary account for authorization. For details, see <a href="https://docs.byteplus.com/docs/tls/Authorizing_cross-service_access">Cross\-service access authorization</a>.</div>


* <div data-tips="true" data-tips-type="tip">After you create a trace instance, TLS automatically creates a corresponding topic for storing the relevant trace data. This log topic uses your Volcengine account quota. For the default configuration of this log topic, see <a href="https://docs.byteplus.com/docs/tls/trace_overview#.5rOo5oSP5LqL6aG5">Precautions</a>.</div>



<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [Torch log service console.](https://console.byteplus.com/tls)

2. Select the region where TLS is located from the top navigation bar.

3. On the left navigation bar, choose **Log application \>**   **Trace storage**.

4. On the **Trace storage** page, click **Create trace instance**.

5. In the **Create trace instance** dialog box, configure the following parameters, and then click **Create**.

   
   |Parameter |Description |
   |---|---|
   |File system name |It is the name of the trace instance. After creation, the instance name can not be modified. |
   |Instance description |Description of the trace instance The following requirements must be met:<br><br><br>* Does not support `<>`,`'`,`\`, `\\`, and all emoji icons.<br><br>* Length must be between 0 and 64 characters. |
   |Project |The project is used for storing data related to the trace instance.<br><br>If there is no suitable project, you can create a new one. For details, refer to [Project](https://docs.byteplus.com/docs/tls/Managing_projects). |
   |Advanced settings switch |When enabled, you can set up advanced configurations such as auto\-splitting and log storage period.<br><br><br>* Auto split:<br><br>   Once enabled, if data volume exceeds existing shard capacity for 5 consecutive minutes, shards split automatically to increase the number of shards.<br><br>   After enabling auto\-splitting, you need to set **maximum shards**. The supported shard number ranges from 1 to 256. If the maximum number of splits is less than or equal to the number of log shards, auto\-splitting is not available.<br><br>* Log storage time configuration:<br><br>   Set log storage period as you need. For log storage type and period requirements, refer to [Storage type](https://docs.byteplus.com/en/docs/tls/Storage_Type). |
   


<span id=".5ZCO57ut5pON5L2c"></span>
## Next steps

Based on your business needs, you can refer to [Access methods](https://docs.byteplus.com/docs/tls/trace_overview#.5o6l5YWl5pa55qGI) to select an appropriate method for accessing trace data.
