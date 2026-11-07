---
title: "Use the debugging feature"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/Use_the_debugging_feature"
---

When data flows within Logstash, the data format is not intuitive, which may cause the data or format written to the destination to not meet expectations. The debugging process requires repeated modification, deployment, and data confirmation, increasing the workload. Therefore, Cloud Search Logstash provides a pipeline debugging feature. After the pipeline configuration is complete, you can directly view the data and its format in the Logs to reduce debugging costs. This topic describes how to use the debugging feature.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The debugging feature supports only standard pipelines, not metadata migration pipelines.</div>


<span id="HAUhTnKV"></span>
## Prerequisites

A Logstash instance has been created and is in the **Running** state. For specific operations, refer to [Create a Logstash instance](https://docs.byteplus.com/en/docs/cloudsearch/Create_a_Logstash_instance).

<span id="Cph09BVu"></span>
## Operation steps


1. Log in to the [Cloud Search console](https://console.byteplus.com/es).

2. In the left navigation pane, select **Data processing** \> **Logstash**.

3. In the Logstash Instances list, click the name of the target instance to go to the **Basic information** tab.

4. On the left, select the **Pipeline management** tab and click **Create pipeline**.

5. In the **Create pipeline** panel, configure the following parameters.

   
   |**Parameter** |**Note** |
   |---|---|
   |Pipeline type |Select **Standard pipeline**. |
   |Pipeline name |The unique identifier of the pipeline. The naming rules are as follows:<br><br><br>   * Must start with a letter.<br><br>   * The length is 1 to 128 characters.<br><br>   * Can contain only letters, digits, underscores (_), and hyphens (\-). |
   |Pipeline description |(Optional) A description of the pipeline. The length must be 1 to 256 characters. |
   |Config configuration |1. Click the **Reference template** button on the right, select the following templates in the pop\-up template list, and then click **confirm**.<br><br>   * Filter\-debug: converts the time to the current time zone to ensure that Logs are not displayed out of order.<br><br>   * Output\-debug_with_filter: outputs the converted time.<br><br>2. Modify the **Config configuration**, add an `input` plugin, and modify the `format` line of the `output` plugin to output all information. The code is as follows.<br><br>   ```Python```<br>```   input {```<br>```     generator {```<br>```       lines => ["logstash debug model usage example"]```<br>```       count =>1```<br>```     }```<br>```   }```<br>```   filter {```<br>```     ruby {```<br>```       code =>'```<br>```         require "time"```<br>```         local_time = Time.now.getlocal.strftime("%Y-%m-%dT%H:%M:%S.%3N")```<br>```   event.set("rfc3339_local", local_time) # rfc3339_local is the field name```<br>```       '```<br>```     }```<br>```   }```<br>```   output {```<br>```       file {```<br>```           path => "/logstash-logs/user-debug.log" # The path must be in the /logstash-logs/user-debug*.log format. The directory cannot be modified, and * can be replaced with other characters. Logs that do not conform to the format cannot be parsed correctly.```<br>```           codec => line {```<br>```               format => "[%{rfc3339_local}] %{event}"```<br>```           }```<br>```       }```<br>```   }```<br>```   ```<br>   <br><br> |
   

6. Click **Save and deploy**.

7. Wait for the Logstash instance status to become **Active** again, then in the left navigation pane, select **Observability**.  **\>**  **Log query**.

8. In the log type, select **Debug logs** to view the debug logs.
