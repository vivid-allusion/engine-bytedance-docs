---
title: "Rename a collection"
product: "Milvus for VectorDB"
product_code: "Milvus_for_VectorDB"
source: "https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Rename_a_collection"
---

After creating a collection, you can rename it as needed. This topic describes how to rename a collection.

<span id="HbZXv2Iu"></span>
## Prerequisites


* Created a Milvus for VectorDB instance and completed authorization. For more information, see [Create an instance](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Create_an_instance) and [Authorize to use an instance](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Authorize_to_use_an_instance).

* Collection has been created. For detailed steps, see [Create a collection](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Create_a_collection).


<span id="w6OTInqZ"></span>
## Precautions

Only Dedicated instances support renaming collections.

<span id="w6OTInqZ"></span>
## Procedure


1. Log on to the [Milvus for VectorDB console](https://console.byteplus.com/milvus).

2. In the top navigation bar, select the project and region for collections management.

3. Select **Collections** in the left navigation bar.

4. On the **Collections** page, choose the **Dedicated** tab, select the authorized instance, then click **View**.

5. On the **Collections** page, expand the database containing the target Collection, then select  **... \> Rename** on the right of the target Collection.

6. In the Rename Collection dialog, enter the new Collection name, then click **OK.** 

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The Collection naming rules are as follows:   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Cannot start with a number or underscore (_).   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The length must be between 1 and 64 characters.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Can only contain letters, digits, and underscores (_).   </div>
