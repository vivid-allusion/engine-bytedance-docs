---
title: "Manage Namespaces"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/doc-manage-namespace"
---

This article describes how to create, update, and delete namespaces through the console.

<span id="create-a-namespace"></span>
## Create a namespace

Follow these steps to create a namespace.


1. Open the [Edge KV](https://console.byteplus.com/cdn/edge-function/list) page.

2. On the **Edge KV** page, click **Create namespace**.

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_e7fec2fd871da96e5a489b8c0e00afd1.jpeg) </span>

3. In the **Create namespace** dialog box, set the following parameters, then click **Save**.

   
   |Parameter |Description |
   |---|---|
   |Name |The name of the namespace. The rules for the name are as follows:<br><br><br>* Can only contain English letters, numbers, hyphens (\-), and underscores (_).<br><br>* Length must be 2 to 64 characters. |
   |Description |A note for the namespace. Maximum length is 80 characters. |
   |Project |The project to which the namespace belongs. |
   

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_aca5aca74f92a7015196b477c9b75610.jpeg) </span>


<span id="update-a-namespace"></span>
## Update a namespace

Follow these steps to update the name and description of a namespace.

<div data-tips="true" data-tips-type="danger" data-tips-is-title="true">danger</div>


<div data-tips="true" data-tips-type="danger">Before modifying the name of a namespace, you need to ensure that the parameters of OpenAPI or runtime API accessing this namespace are updated synchronously. Otherwise, if OpenAPI or runtime API still accesses the old namespace name, the access will fail.</div>



1. Open the [Edge KV](https://console.byteplus.com/cdn/edge-function/list) page.

2. On the **Edge KV** page, find the namespace you want to update, then click **Edit** in the **Actions** column.

3. In the **Edit namespace** dialog box, enter the new space name and description, then click **Save** to complete the update.


<span id="delete-a-namespace"></span>
## Delete a namespace

You can delete namespaces that are no longer needed.

<div data-tips="true" data-tips-type="danger" data-tips-is-title="true">danger</div>


<div data-tips="true" data-tips-type="danger">When a namespace is deleted, all data in that namespace will also be deleted. This operation is irreversible. Before deleting, please make sure that no functions are using the data in this namespace.</div>



1. Open the [Edge KV](https://console.byteplus.com/cdn/edge-function/list) page.

2. On the **Edge KV** page, find the space you want to delete, then click **Delete** in the **Actions** column.

3. In the pop\-up dialog box, check **Confirmed**, then click **OK** to complete the deletion of the namespace.
