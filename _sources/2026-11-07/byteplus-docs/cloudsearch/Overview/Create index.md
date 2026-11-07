---
title: "Create index"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/Create_index"
---

This article explains how to create an index.

<span id="NXqeEbIW"></span>
## Prerequisites


* Created an OpenSearch 2.9.0 or later instance. For more information, see [Create an instance](https://docs.byteplus.com/en/docs/cloudsearch/creating-instance).

* Created AI search. For detailed steps, see [Create AI search](https://docs.byteplus.com/en/docs/cloudsearch/Create_an_AI_search_service).


<span id="3102e6f7"></span>
## Procedure


1. Log on to the[Cloud Search console](https://console.byteplus.com/es).

2. In the top navigation bar, select the target project and region.

3. Select **AI search** in the left navigation bar, then find and click the target service name.

4. Select **Index management** in the left navigation bar, then click **Create index**.

5. In the **Create index** panel, configure the following parameters, then click **Next step**.

   
   |**Parameter** |**Description** |
   |---|---|
   |Index name |Name of the index. Limits are as follows:<br><br><br>* Cannot start with a number or underscore (_).<br><br>* Length must be between 1 and 128 characters.<br><br>* Can only contain lowercase letters, numbers, underscores (_), and hyphens (\-). |
   |Number of active shards |The number of active primary shards in the index. |
   |Replicas |Number of Replicas for the index, value range 1 to 10. |
   |Translog |Select **Asynchronous flush** or **Synchronous flush**. |
   |Compression method |Select **Speed priority**, **Compression ratio priority**, or **ZSTD**. |
   |ANN Search |Select **Enable** or **Close**. |
   |Index settings (optional) |Set index details. |
   

6. In the index field area, choose **Visual editing** or **JSON editing**, then configure accordingly.

   
   <Tabs>
   <Tab zoneid="KlyXqyrMxj" title="visual editor">
   <TabTitle>visual editor</TabTitle>
   
   Configure scalar fields and vector fields as needed.
   
   
      * Scalar fields: specify **scalar type**, then select **retrievable** and **aggregatable** options as required.
   
      * Vector fields: specify **Dector type**, **Dimension**, and **Metric type**.
   
   
   <div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>
   
   
   
   * <div data-tips="true" data-tips-type="default">Click <strong>add a row</strong> to configure multiple fields.</div>
   
   
   * <div data-tips="true" data-tips-type="default">When configuring scalar fields, if the scalar type is text, also enter the tokenizer.</div>
   
   
   
   </Tab>
   <Tab zoneid="w1wiz75hkp" title="JSON editor">
   <TabTitle>JSON editor</TabTitle>
   
   Enter field content in JSON format within the code box.
   
   
   </Tab>
   </Tabs>
   

7. In the **Other configurations** area, configure the following parameters, then click **OK**.

   
   |**Parameter** |**Description** |
   |---|---|
   |Add dynamic columns |select **True**, **False**, or **Strict**. |
   |Routing |routing switch; enable as needed.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">this setting cannot be changed once the index is created. confirm before submitting.</div><br> |
   


<span id="xhADzG1F"></span>
#
