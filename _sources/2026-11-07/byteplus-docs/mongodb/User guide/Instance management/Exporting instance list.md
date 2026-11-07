---
title: "Exporting instance list"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/download-instance-list"
---

Document Database for MongoDB allows you to export the instance list. You can filter out target instances based on service requirements and export relevant information about the instances (such as instance status, availability zone and instance type) to facilitate instance resource management offline.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [MongoDB console](https://console.byteplus.com/db/mongodb).

2. In the upper\-left corner of the top menu bar, select the project and region for instance.

3. Select either **Replica set instances** or **Sharding instances** in the left navigation bar depending on the instance type.

4. On the target instance type list page, click <span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_79fd9094eb01b1e0f325f9af1f38225b.jpg) </span> icon in the upper\-right corner of the page.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can first filter out target instances based on criteria such as <strong>Instance status</strong> and <strong>Tag</strong>in the instance list before exporting.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The private network address information of instances is not displayed by default on the instance list page. To view it, please click <img src="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0bcd2370f0fbd68a13767598ee94da7f.png" width="14px" /> icon in the upper right corner of the list and check <strong>Private network address</strong> in the field drop\-down list.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">On the instances list page, the <strong>Private network address</strong> column only displays private network address information that instances provide by default (for example, the private network address of replica set instances and Mongos in the sharding cluster instances). The private network addresses you applied for (for example, the private network address of Shard and ConfigServer in sharding cluster instances) will not be displayed.   </div>
   

5. In the pop\-up dialog box, set the following configurations.

   
   |Parameter |Description |
   |---|---|
   |Export range |Select the export range of the instance list. The following values are supported:<br><br><br>* **Export all data**: Export the specified field data of all instances **under the specified region and project of the current account**.<br><br>* **Export selected data**: Export the specified field data of the selected instances.<br><br>* **Export current search results**: Export the specified field data of the instances that meet the search criteria.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Selecting the <strong>Eexport range</strong> is only supported when exporting replica set instances.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">To select the export range as <strong>Export selected data</strong>, you must select at least one instance in the Instances list.</div><br> |
   |Exporting list fields |Check the instance information to be exported according to business needs, such as instance status, availability zone, private address and so on. |
   

6. click **OK**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After clicking <strong>OK</strong>, the instance list information will be exported as a CSV file and automatically downloaded to your local device via the browser. You can view the file using a text editor.   </div>
