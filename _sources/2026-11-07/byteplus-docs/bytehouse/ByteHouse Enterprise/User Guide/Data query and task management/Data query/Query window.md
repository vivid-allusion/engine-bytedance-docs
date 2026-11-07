---
title: "Query window"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/query-window"
---

When data is imported, if you need to quickly verify the data. You can perform a quick query through the console.

<span id="e52b34c5"></span>
## Send query

How to use:


1. Enter the console, visit the **Quick Query** window.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4388e0eab44241bf8fd8e4c0baacc5e4~tplv-goo7wpa0wc-image.image) </span>

2. Select the cluster in the drop\-down menu on the interface.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e626bca7ce6e46f99a38872e4bf8af0f~tplv-goo7wpa0wc-image.image) </span>

3. In the worksheet window of the interface, input SQL statements.

4. Click “Run” below to proceed with the query.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a545bcdff32f4850b8142d7e746706cc~tplv-goo7wpa0wc-image.image) </span>


<span id="60f6d2e4"></span>
## Sending mode

Above the editor, you can select one of three node distribution modes:


* Send to Automatic Assignment Node: [Default] Pass the gateway and select a node to send the query.

* Send to All Nodes: Send the query to all nodes under the cluster, can be used in place of `on cluster` syntax to send DML commands. It can also be used for troubleshooting.

* Send to a Single Node: Send the query to a designated node. Usually used for error investigation.


<span id="d1d28446"></span>
## Save worksheet

The worksheet can be saved in the cloud, log in on other browsers with your BytePlus Account, and you will see the saved worksheet. Steps as follows:


1. Click "Save" at the bottom right corner.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cc93640313854e2a99a61048a201991b~tplv-goo7wpa0wc-image.image) </span>

2. And input the name of the worksheet.

3. Complete the cloud saving of the worksheet.

4. In the "Worksheet" Tab on the left side of the interface, you can see all the worksheets saved under the current account and current cluster.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The search window and cluster are correlated one\-to\-one; the search window of each cluster is not visible in other clusters.</div>


<span id="e4c3cbd4"></span>
## Export results

For successfully searched results, you can download the query results as a CSV file to your local environment for further analysis and usage by clicking **Query results** page's **Download** button.
