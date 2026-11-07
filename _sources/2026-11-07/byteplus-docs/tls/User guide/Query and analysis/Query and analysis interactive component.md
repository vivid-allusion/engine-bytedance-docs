---
title: "Query and analysis interactive component"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Query-and-analysis-interactive-component"
---

Torch Log Service (TLS) has built\-in intuitive query and analysis interaction components to help you quickly build query and analysis statements. You only need to select the specific fields, operators, and other information, and the system will automatically generate corresponding query statements.

<span id="3f55fb9f"></span>
## Before you begin


* Create a project and a topic.

* Collect log data through LogCollector or other methods.

* Enable the index feature before you query logs. For information on how to enable the index feature, refer to [Configure indexes](https://docs.byteplus.com/docs/tls/Configure-indexes-2).


<span id="174c233b"></span>
## Operation steps


1. Log on to the [TLS console](https://console.byteplus.com/tls).

2. In the top navigation bar, select the region where TLS is located.

3. In the left navigation bar, select **Common functions** \> **Query and analysis**.

4. In the left list of the **Query and analysis** page, select the specified project and topic.

5. On the query and analysis page for the specified topic, set the time range for the log data.

6. Click **Switch to tap mode** icon.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b2b2993fdf9e466aa07741612a4fcfd4~tplv-goo7wpa0wc-image.image) </span>

7. Set the search criteria and click **OK** .

   * Click **full text**, and after selecting the judgment condition and entering the field value, the system will generate the full\-text query condition based on your settings.

   * Click a certain field, and after selecting the judgment condition and entering the field value, the system will generate the key\-value retrieval condition according to your settings.

   * Set the full\-text query or key\-value query conditions, and check **is it a phrase query**. Then, the system will generate the phrase query conditions according to your settings. For detailed explanations of phrase queries, refer to [Phrase search](https://docs.byteplus.com/docs/tls/Phrase-search-2).

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1b0ffb430d754640a330e20abf4fefa1~tplv-goo7wpa0wc-image.image) </span>

8. (Optional) Click **Add analysis statement** to add a `SELECT` statement.

9. After confirming that the search analysis criteria are correct, click **Search** .

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d562363e93d04eb3842bbb3375609da4~tplv-goo7wpa0wc-image.image) </span>

   After setting up the query and analysis conditions, click the **Switch to statement mode** icon to view the statements corresponding to the query and analysis conditions.


<span id="04bc4fb7"></span>
## Grammar description

<span id="37d7228b"></span>
### Logical connector


|Logical connector |Description |
|---|---|
|and |Corresponds to the `AND` operator in the query syntax. For detailed instructions, please refer to [Common query syntax](https://docs.byteplus.com/docs/tls/Log-query-syntax-2#57de8b6d). |
|or |Corresponds to the `OR` operator in the query syntax. For detailed instructions, please refer to [Common query syntax](https://docs.byteplus.com/docs/tls/Log-query-syntax-2#57de8b6d). |


<span id="a5fc5b71"></span>
### Operator

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When using the <strong>contain</strong> or <strong>no contain</strong> operator, you need to specify either a complete keyword or partial characters with wildcards <code>*</code> or <code>?</code>.</div>



* <div data-tips="true" data-tips-type="tip">Specify a complete keyword indicates an exact match.</div>


* <div data-tips="true" data-tips-type="tip">Specify partial characters and wildcards <code>*</code> or <code>?</code> indicate a fuzzy match. For example, <code>containcn *</code>.</div>


   <div data-tips="true" data-tips-type="tip">Wildcards must be added for fuzzy matches. For detailed instructions, please refer to <a href="https://docs.byteplus.com/docs/tls/Log-query-syntax-2#57d90d06">Accuracy</a>.   </div>
   



|Search method |Type |Operator |
|---|---|---|
|full\-text search |text |contain, No contain |
|key value retrieval |text |contain, No contain, exist, does not exist, the existence option belongs to, all options do not belong to |
||long |=, !=, \>=, \>, <=, <, in the specified range, not in the specified range, Exist, does not exist, The existence option belongs to, All options do not belong to |
||double |=, !=, \>=, \>, <=, <, in the specified range, not in the specified range, Exist, does not exist, The existence option belongs to, All options do not belong to |


<span id="abda031f"></span>
## Related operations


* After setting the query conditions, you can click on the following icon to quickly enable or disable the specified query condition.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0bddd3cc9cd141578a2f8f5e19155002~tplv-goo7wpa0wc-image.image) </span>

* After setting the query conditions, you can click the following icons to quickly set the inclusion or exclusion relationship for the query condition.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a01f15db1dde47e8a1be41b5bcb803fe~tplv-goo7wpa0wc-image.image) </span>


<span id="08ca165f"></span>
## Example

<span id="2e2d33be"></span>
### Example 1


* Scenario: Query logs containing **error** and **warning**.

* Interactive component configuration

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b2924f8cd61d46a696c92affa00af7ff~tplv-goo7wpa0wc-image.image) </span>

* Query statement

   ```SQL
   warning AND error
   ```
   

* Query result

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/90a919719b1845b5a7e44de5b5e3dc40~tplv-goo7wpa0wc-image.image) </span>


<span id="1580b1f5"></span>
### Example 2


* Scenario: Query the logs containing **PutLogs** in the value of the **URL** field.

* Interactive component configuration

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dba2faf8063b4c678579a98fff92a3d0~tplv-goo7wpa0wc-image.image) </span>

* Query statement

   ```SQL
   URL:PutLogs
   ```
   

* Query result

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0843cec6b6364d9abc35ea0f6741b1e8~tplv-goo7wpa0wc-image.image) </span>


<span id="cb96e3e3"></span>
### Example 3


* Scenario: Count the number of requests with the status of 200.

* Interactive component configuration

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7ad30d85132444aa9b65de8a137c75d0~tplv-goo7wpa0wc-image.image) </span>

* Query statement

   ```SQL
   status:200 | SELECT COUNT(*) 
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/65e7c946e46c4c97bb35fe707548ab20~tplv-goo7wpa0wc-image.image) </span>


<span id="51152c21"></span>
### Example 4


* Scenario: Query request IDs starting with **d581** .

* Interactive component configuration

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5b7f217a257a4e25b41143687dd05e1f~tplv-goo7wpa0wc-image.image) </span>

* Query statement

   ```SQL
   ReqID: d581* | SELECT DISTINCT ReqID
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/39e8f1ccbf344f37a8cb57c7268dc146~tplv-goo7wpa0wc-image.image) </span>
