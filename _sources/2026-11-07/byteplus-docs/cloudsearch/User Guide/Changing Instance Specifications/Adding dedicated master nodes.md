---
title: "Adding dedicated master nodes"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/adding-master-nodes"
---

If you have not bought dedicated master nodes during instance creation, you can add them later by modifying the instance configurations to meet your service requirements.

<span id="9af3ae70"></span>
## Precautions


* You can only add dedicated master nodes to an instance that is in the **Running** state (indicated by green) and currently does not have existing dedicated master nodes.

* When you attempt to add dedicated master nodes, the system automatically assesses the situation and displays a window that guides you through the next steps:

   * If combined master and data nodes contain residual data that cannot be migrated to the remaining data nodes, you must add 3 data nodes and transfer the data to those new nodes before adding dedicated master nodes.

   * If combined master and data nodes contain residual data that can be migrated to the remaining data nodes, you must migrate the data before adding dedicated master nodes.

   * If combined master and data nodes do not contain any residual data, you can directly add dedicated master nodes.

      Adding data nodes or dedicated master nodes incurs charges. For more information, refer to [Billing overview](https://docs.byteplus.com/en/docs/cloudsearch/billing-overview).


<span id="2b95e09d"></span>
## Procedure


1. Log into the [BytePlus Cloud Search console](https://console.byteplus.com/es).

2. In the top menu bar, select the Project and Region where the desired instance resides.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c11209b6da4c40859894dea23a18eaf7~tplv-goo7wpa0wc-image.image) </span>

3. On the **Instances** page, find the desired instance, click `...` in the **Actions** column, and then choose **Add dedicated masternode**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d0ebb6a112614b3abf9eb4cb78afd8ad~tplv-goo7wpa0wc-image.image) </span>

4. Follow the on\-screen prompts.


<span id="743b1daa"></span>
### Adding data nodes

If there is data left over on the combined master node and it cannot be migrated to the remaining data nodes, you must first add data nodes


1. If prompted to add a data node before data migration, click **Immediately add**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/48658a20cf694240801d8dd46c5a7ad7~tplv-goo7wpa0wc-image.image) </span>

2. In the **Increase the number of data nodes** dialog box, confirm the new node number and associated charges, click **Confirm**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f2172b5ea8c24a508163deb1f530cf0a~tplv-goo7wpa0wc-image.image) </span>

3. On the **Data node expansion** page, confirm change details, read and agree to Terms of Service, and then click **Submit**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f3d6123bf0bc48a6a8b444a8f1d89bb7~tplv-goo7wpa0wc-image.image) </span>

4. Return to the **Instances** page and wait for the operation to complete.

   If the instance status is **Changing**, the operation is in progress. If the instance status is **Running**, the operation succeeds, indicating that new data nodes have been added.


<span id="8947cf2c"></span>
### Migrating data

If there is data left over on the combined master node, but the data can be directly migrated to the remaining data nodes, data migration will be required first.


1. To initiate data migration, click **Migrate now**, and then click **OK** next to the estimated migration time.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/502329bd843f4f368f39394aa3d1bc5b~tplv-goo7wpa0wc-image.image) </span>

2. Wait for the migration to complete, click **Confirm to change**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/14be00b76f664aec9f4679d79e706eb1~tplv-goo7wpa0wc-image.image) </span>

   On the displayed page, add dedicated master nodes as required.


<span id="509d8a66"></span>
### Adding dedicated master nodes

If combined master and data nodes do not contain any residual data, you can directly add dedicated master nodes.


1. On the **Add dedicated masternode** page, select node specifications, click **Confirm order**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Select node specifications based on your specific scenarios. For more information, refer to <a href="https://docs.byteplus.com/en/docs/cloudsearch/specifications">Specifications</a>.   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7cd99fcc78cd40cab20de7e3c2dde83a~tplv-goo7wpa0wc-image.image) </span>

2. Confirm change details, read and agree to Legal Resources, then click **Buy now**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Adding dedicated master nodes involves converting combined master and data nodes into dedicated master nodes, rather than introducing three entirely new nodes.   </div>
   

3. Return to the **Instances** page and wait for the operation to complete.

   If the instance status is **Changing**, the operation is in progress. If the instance status is **Running**, the operation succeeds, indicating that dedicated master nodes have been added.


<span id="89205b92"></span>
## Result verification

After confirming that dedicated master nodes are added, navigate to the instance details page. In the **Configuration diagram** pane, view information about the dedicated master nodes.
