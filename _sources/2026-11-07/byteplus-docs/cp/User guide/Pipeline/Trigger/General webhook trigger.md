---
title: "General webhook trigger"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/General_webhook_trigger"
---

The generic Webhook trigger is used to trigger pipeline runs from third\-party tools or proprietary systems, other than the code source. A pipeline supports configuring multiple general Webhook triggers. This article introduces how to configure general Webhook trigger rules.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

The pipeline has been created. For specific operations, refer to [Create a pipeline](https://docs.byteplus.com/en/docs/cp/Create_pipelines).

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Use any of the following methods to access the add trigger panel.

   * Edit a pipeline

      1. In the pipeline list, select the target pipeline, and click  **`...`**   **\> edit**, go to the Process orchestration tab of the current pipeline.

      2. In the code source & trigger panel, click **Add \> General Webhook Trigger**.

   * Trigger shortcut

      1. In the pipeline list, click the name of the target pipeline. This opens the Run Records tab for the selected pipeline.

      2. Click **trigger** to switch to the trigger tab.

      3. Click **Add trigger \> General Webhook trigger**.

2. Configure general Webhook trigger rules.

   
   |Configuration Item |Descriptions |
   |---|---|
   |Trigger types |This scenario is **a general Webhook trigger**. |
   |Trigger name |The name of the custom Webhook trigger. Webhook trigger names within the same pipeline must be unique. |
   |URL |Display the Webhook URL for the current pipeline. The pipeline receives Webhook trigger messages through this URL. |
   |Dynamic Parameter |Optional configuration. Dynamic Parameter is used to configure the runtime value of dynamic variables when a Webhook triggers pipeline execution. If no configuration is set, dynamic variables will use the default value entered in **Process orchestration \> Variable management**.<br><br>The runtime value of a dynamic variable can be set to a static value or assigned dynamically via parameters.<br><br><br>* Static value: for example, 10.<br><br>* Dynamic parameter passing: Extract the relevant content from the Hook message to dynamically assign values to variables. Supports JsonPath format and standard format. Refer to the following for details.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Variable precedence: passing parameters to dynamic variables \> static runtime value of dynamic variables \> default value of dynamic variables (the default value configured when creating the variable)</div><br> |
   |Description |Enter remarks for the current trigger. This field can be left blank. |
   |Runtime branch |When a pipeline has a code source, you can configure the code branch used at runtime.<br><br><br>* Turn on: Select the code branch to use when the pipeline is triggered by a Webhook. To use a non\-default branch when the Webhook is triggered, configure this parameter. For example: In a pipeline, the default branch of the code source is the "main" branch. However, if you want the Webhook to trigger a specific branch, you can achieve this by configuring this parameter.<br><br>* Turn off: When a webhook triggers the pipeline, the default branch specified in the code source configuration will be used. |
   

3. Click **Confirm** to complete the Webhook trigger configuration.

4. If you enter from the edit pipeline entry point, click **Save** in the bottom right to save the pipeline configuration.


<span id=".5ZCO57ut5pON5L2c"></span>
## What to do next

Configure the pipeline's URL on your platform to ensure that the pipeline can properly receive webhook trigger messages. You can also use the following commands to directly trigger the pipeline to run.

```bash
curl --location 'https://cp.volces.com/v2/webhook/your-webhook' \
--header 'Content-Type: application/json' \
--data-raw '{
  "xx": "xx",
  "xx": "xx"
}'
```


When triggering a pipeline, you can extract messages from a Hook using either the JsonPath format or a standard format, and use the extracted values to pass parameters to dynamic variables. The following will introduce these two methods separately.

<span id=".6YCa6L-HLWpzb25wYXRoLeagvOW8j-WKqOaAgeS8oOWPgg=="></span>
## Dynamically pass parameters using the JsonPath format

JsonPath is primarily used to locate and extract data from specific parts of a JSON structure. It provides a concise and powerful method for specifying which elements or attributes to select, making it suitable for handling complex nested data structures. This article uses a store's JSON text as an example to show you how to extract the authors of all books in the store using `$.store.book[*].author`.


1. In the pipeline's **Process orchestration \> Variable management**, configure the dynamic variables and default values you want to pass. The example is as follows:

2. Turn on the generic Webhook trigger. In **Dynamic Parameter**, select the dynamic variable configured in Step 1, and configure the runtime value using [JsonPath format](https://github.com/oliveagle/jsonpath). The example is as follows:

3. Call and use data\-raw information to pass trigger parameters and modify the value of the Dynamic Parameter. The example is as follows:

   ```bash
   curl --location 'https://cp.volces.com/v2/webhook/your-webhook' \
   --header 'Content-Type: application/json' \
   --data-raw '{ "store": {
       "book": [ 
         { "category": "reference",
           "author": "Nigel Rees",
           "title": "Sayings of the Century",
           "price": 8.95
         },
         { "category": "fiction",
           "author": "Evelyn Waugh",
           "title": "Sword of Honour",
           "price": 12.99
         },
         { "category": "fiction",
           "author": "Herman Melville",
           "title": "Moby Dick",
           "isbn": "0-553-21311-3",
           "price": 8.99
         },
         { "category": "fiction",
           "author": "J. R. R. Tolkien",
           "title": "The Lord of the Rings",
           "isbn": "0-395-19395-8",
           "price": 22.99
         }
       ],
       "bicycle": {
         "color": "red",
         "price": 19.95
       }
     }
   }'
   ```
   

4. As shown, the initial value of the variable `user` in the example is `xiaoming`, and after being triggered, it changes to `[Nigel Rees, Evelyn Waugh, Herman Melville, J. R. R. Tolkien]`.


<span id=".6YCa6L-H5pmu6YCa5qC85byP5Yqo5oCB5Lyg5Y-C"></span>
## Pass parameters dynamically using a standard format

The normal format is simple to use and does not require learning JsonPath syntax. It is suitable for extracting a single value or simple data types. This article uses a simple example to demonstrate how to use the ordinary format for dynamic parameter passing.


1. In the pipeline's **Process orchestration \> Variable management**, configure the dynamic variables with the same name and their default values that you want to pass. The example is as follows:

2. Turn on the generic Webhook trigger, and in **Dynamic Parameter**, select the dynamic variable configured in Step 1. The example is as follows:

3. Invoke and use data\-raw information to pass trigger parameters, and modify dynamic parameter values. The example is as follows:

   ```bash
   curl --location 'https://cp.volces.com/v2/webhook/your-webhook' \
   --header 'Content-Type: application/json' \
   --data-raw '{"name": "b"}'
   ```
   

4. As can be seen, the initial value of the variable `name` in the example is`a`, changes after triggering are intended for`b`.
