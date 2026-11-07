---
title: "Manage Data"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-manage-data"
---

This article describes how to add, update, or delete data in a namespace.

<span id="prerequisites"></span>
## Prerequisites

You have a [namespace](https://docs.byteplus.com/docs/byteplus-cdn/doc-manage-namespace) under your BytePlus account.

<span id="add-data"></span>
## Add data


1. Open the [Edge KV](https://console.byteplus.com/cdn/edge-function/list) page.

2. Find the namespace where you want to add data, and click on the name of the namespace.

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_41694dc2598b6ba5bb4c8bf76d28f32e.png) </span>

3. Click **Add data**.

4. In the **Add data** dialog box that appears, set the relevant parameters for the data, then click **Save**.

   
   |Parameter |Description |
   |---|---|
   |Key |The key of the data. Can only contain English letters, numbers, hyphens (\-), and underscores (_). Not exceeding 512 bytes. |
   |Value |The value of the data. A single value should not exceed 128 KB. |
   |TTL |Optional. The expiration time of the data. You can set it to **Never expires**, or set it to **Customize** and then set the expiration time for the data. The data will not be accessible after it expires. |
   

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_977d137d8ce27027f700cadcf4815bd3.jpeg) </span>


<span id="update-data"></span>
## Update data

After adding data, you can modify the value of the data or its expiration time.


1. Open the [Edge KV](https://console.byteplus.com/cdn/edge-function/list) page.

2. Find the namespace where you want to update data, and click on the name of the namespace.

3. Find the data you want to update, and click **Modify** in the **Actions** column.

4. In the **Modify data** dialog box that appears, modify the **Value** or **TTL**, then click **Save** to complete the modification.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">After you update the data, the updated data will be synchronized to all edge nodes. You don't need to republish the function.</div>


<span id="delete-data"></span>
## Delete data

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Before deleting data, please make sure that no functions are using this data. This operation is irreversible.</div>



1. Open the [Edge KV](https://console.byteplus.com/cdn/edge-function/list) page.

2. Find the namespace where you want to delete data, and click on the name of the namespace.

3. You can delete a single data item or multiple data items:

   * To delete a single data item, find the data item you want to delete, and click **Delete** in the **Actions** column. In the dialog box that appears, click **Delete**.

   * To delete multiple data items, select the checkboxs preceding the key of each data item, and click **Batch delete**. In the dialog box that appears, click **OK**.
