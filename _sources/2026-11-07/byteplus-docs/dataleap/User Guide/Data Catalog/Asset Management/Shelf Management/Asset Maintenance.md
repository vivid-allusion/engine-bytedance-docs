---
title: "Asset Maintenance"
product: "DataLeap"
product_code: "dataleap"
source: "https://docs.byteplus.com/en/docs/dataleap/Asset_Maintenance"
---

The asset maintenance feature allows you to view and manage all data assets belonging to the current business line. You can also register file assets online using the asset registration function. Asset maintenance includes two types: maintain assets and off\-shelf assets. The following sections explain the corresponding maintenance operations for each.

<span id="f3887b00"></span>
## Constraints

The business line administrator has all operational permissions, while the data classification administrator can only maintain assets under their managed data classifications and subcategories.

<span id="8abfde92"></span>
## Prerequisites

The business line has been created, and assets have been selected.

<span id="92f9193d"></span>
## Maintain Assets

This feature allows you to register assets and manage the listing and delisting of selected assets.


1. Log in to the DataLeap console.

2. Select **Overview \> Catalog \> Asset Management \> Shelf Management \> Asset Maintenance \> Maintain Assets** to go to the **Maintain Assets** page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ebadc75b7b0a422ba63adefccab43773~tplv-goo7wpa0wc-image.image) </span>

3. Select the business line to manage from the dropdown menu at the top right of the page.

4. You can perform the following actions:

   * Search assets

      After setting search conditions, you can view the list of assets that match the criteria.

   * Unpublished asset maintenance

      * List

         Click the **Launch** button in the **Action** column for the selected item, and confirm to complete the asset listing.

         <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="3">tip         </div>
         

         <div data-tips="true" data-tips-type="tip" data-wrapper-indent="3">Only assets linked to data classification can be listed.         </div>
         

      * Edit

         Click the **Edit** button in the **Action** column for the selected item to modify the asset information.

         
         |Parameters |Description |
         |---|---|
         |Data Categories |Asset classification. The dropdown allows selecting all categories under the current business line, supporting multiple selections. Refer to [Category Management](https://docs.byteplus.com/docs/dataleap/Category_Management) for the action of creating categories. |
         |Business Line Tags |Tag assets. The dropdown allows selecting all tags under the current business line, supporting multiple selections. Refer to [Label Management](https://docs.byteplus.com/docs/dataleap/Tag_Management) for the action of creating business line tags. |
         |Affiliated Albums |The album that the asset affiliated with. The dropdown allows selecting all albums under the current business line, supporting multiple selections. Refer to [Album Management](https://docs.byteplus.com/docs/dataleap/Album_Management) for the action of creating albums. |
         

      * Classification

         Click the **Classification** button in the **Action** column for an item, then set classification information in the popup window to classify the asset under the specified data classification.

         
         |Parameters |Description |
         |---|---|
         |\*Modify type |Modify the asset's type, supporting three methods: **change data classification**, **add data classification**, and **delete data classification**.<br><br><br>* Change data classification: directly modify the asset's classification.<br><br>* Add data classification: keep the asset's original classifications and add more.<br><br>* Delete data classification: remove classifications from the asset. |
         |\*Data classification |The classification of the asset. Select from the dropdown of created data classifications; multiple selections are allowed. |
         

      * Not listing

         Click the  **... \> Not on the shelves** button in the **Action** column for an item, then fill in the reason for not listing in the popup window to complete the operation. Unlisted assets cannot be searched in the **Asset Catalog**.

      * Remove

         Click the  **...**   **\> Remove** button in the **Action** column for an item, after confirmation, removes the asset from the current business line. After removal, the asset no longer belongs to the current business line, and any set business line and data classification information will be cleared.

   * Published Asset Maintenance

      Click the **Removal** button in the **Action** column for an item, and after confirmation, remove the asset.

   * Instructions

      Click the **Introduction** button in the **Action** column of an entry. In the pop\-out side panel, you can add a usage description for the asset and edit or delete it as needed.

   * Batch Operate

      After selecting one or more entries, click the batch operate button below the list to perform the corresponding batch operations.

      * Batch classification: batch classify the selected assets.

      * Batch maintenance: set data classification, business line tags, and attribution album for assets in batches.

         
         |Parameters |Description |
         |---|---|
         |Select batch maintenance content |Batch maintenance of asset business information, including **data classification**, **business line tags**, and **attribution album**. For specific instructions, please refer to the parameter descriptions for editing individual asset information above. |
         |**batch maintenance strategy** ||
         |Maintenance type |Maintenance types applied to batch maintenance content support the following three methods:<br><br><br>* add: add new maintenance content to the asset.<br><br>* modify: modify the existing maintenance content of the asset to the currently selected corresponding content.<br><br>* delete: delete existing maintenance content of the asset.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The corresponding maintenance type action takes effect only after selecting the appropriate batch maintenance content.</div><br> |
         |Content is empty do not execute |choose whether to execute when maintenance content is empty.<br><br><br>* yes: do not execute.<br><br>* No: Execute. |
         

      * Batch launch/not on the shelves: batch launch/not on the shelves the selected assets.

      * Batch removal: batch removal of selected assets.

      * Batch remove: batch remove the selected assets from the current business line.


<span id="d9ae702d"></span>
## Off\-shelf Asset Management

Off\-shelf assets are defined as assets with low liquidity value or non\-mandatory information completion, such as test tables, backup tables, and temporary tables. This feature enables centralized management of off\-shelf assets.


1. Log in to the DataLeap console.

2. Select **Overview \> Catalog \> Asset Management \> Shelf Management \> Asset Maintenance \> Off\-Shelf Assets** to enter the **Off\-Shelf Assets** page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ff818299657b4abb8d8aefa888e568a0~tplv-goo7wpa0wc-image.image) </span>

3. In the top\-right corner of the page, use the business line dropdown to select the business line to manage.

4. The following actions can be performed:

   * Search assets

      Set search criteria to view the list of off\-shelf assets that match the conditions.

   * View asset details

      Click on the **Asset Name** in any entry to view detailed data Search information for that asset.

   * Change asset status

      Click the **Change to pending maintenance** button in the **Action** column of a record, or select one or more records and click the **Change to pending maintenance** button below the list. After confirming, you can change the corresponding assets to pending maintenance status.

   * Remove

      Click the **Remove** button in the **Action** column of a record, or select one or more records and click the **Batch remove** button below the list. After confirming, you can remove the asset from the current business line. After removal, the asset will no longer belong to the current business line. If the asset has business line and data classification information set, these will also be cleared.


<span id="9c53fa1f"></span>
## Subsequent Actions


* After asset release, you can organize the data assets produced within the group using the **Asset Catalog** feature for categorized display. For related instructions, see [Asset Catalog](https://docs.byteplus.com/docs/dataleap/Asset_Catalog).

* After attributing an asset to an album, go to the **Asset Album** page to view the asset list under the album. For related operations, see [Asset Album](https://docs.byteplus.com/docs/dataleap/Asset_Album).
