---
title: "Category Management"
product: "DataLeap"
product_code: "dataleap"
source: "https://docs.byteplus.com/en/docs/dataleap/Category_Management"
---

Category management is used for building the Data Services Portal and includes data classification and album classification. Data classification displays the directory of data assets, while album classification shows the directory of asset albums.

<span id="3dc858be"></span>
## Constraints


* Business line administrators can create directories under their business lines to display data assets and albums as needed.

* Category administrators can only edit, sort, or delete categories they manage and their subcategories.


<span id="d08ccb74"></span>
## Prerequisites

A business line has been created.

<span id="617e7b68"></span>
## Operation Steps


1. Log in to the DataLeap console.

2. Select **Overview \> Catalog \> Asset Management \> Basic Management \> Category Management** to enter the **Category Management** page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0262ae658b98480b986182083a3e5255~tplv-goo7wpa0wc-image.image) </span>

3. Click the **Data Classification** tab or the **Album Category** tab to perform the following management operations respectively:

   * Add category

      Click the **New Category** button, set category information in the pop\-up window, then click **OK** to complete the addition.

      
      |Parameters |Description |
      |---|---|
      |\*Category Type |The type of this category supports three options: **comprehensive category**, **custom category**, and **model specification category**, selectable from a dropdown.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">This parameter is supported only when <strong>data classification</strong> is set.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Only one primary model specification category is allowed under a single business line.</div><br> |
      |Superior classification |The parent category of this category, selectable from a dropdown.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If the superior classification is empty, the current creation will be a first\-level category.</div><br> |
      |* Specify asset type |The specified asset types under this category, supporting multiple current options, selectable from a dropdown, with multi\-selection available.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter must be set only when <strong>category type</strong> is <strong>custom category</strong>.</div><br> |
      |* Category name |The category name, which must be unique among sibling categories.<br><br>Supports Chinese characters, letters, numbers, underscore "_", hyphen "\-", and spaces, and must start with a Chinese character, letter, or number. |
      |English name |English name of the category.<br><br>Only supports English letters, numbers, and underscores. |
      |\*English abbreviation |English abbreviation of the category name, unique within the same level.<br><br>Only supports English letters, numbers, and underscores.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Supported only when setting <strong>data classification</strong>.</div><br> |
      |Description |Description of the category, optional. |
      |\*Category administrator |Category administrators can enter account keywords to select from the dropdown and set multiple accounts. |
      |Business Owner |Business leader for the applicant or provider. This parameter takes effect only after integration with the approval flow.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Supported only when setting <strong>data classification</strong>.</div><br> |
      |Category Approver |Approver for listing assets in this category's asset catalog. This parameter takes effect only after integration with the approval flow.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Supported only when setting <strong>data classification</strong>.</div><br> |
      |\*Whether to force table naming |You can choose whether to force table naming.<br><br>If **Yes** is selected, when creating a table on the **Table Management** page, after selecting the corresponding category, the table name will automatically include the category's **English abbreviation**.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">This parameter only needs to be set when the <strong>Category Type</strong> is <strong>Model specification category</strong>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip"><strong>First\-level model specification category</strong> is the theme name, and only one is allowed under one business line. If it is a first\-level model specification category, this parameter is recommended to set as <strong>No</strong>.</div><br> |
      |\*Whether first\-level data warehouse domain |You can choose whether this category is a first\-level data warehouse domain.<br><br>This parameter is for attribute description only and serves as a marker.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter only needs to be set when the <strong>Category Type</strong> is <strong>Model specification category</strong>.</div><br> |
      |\*Linked Data Layer |The table data hierarchy linked to business line data classification supports the following options. Multiple selections are allowed from the dropdown.<br><br><br>* Operational Data Store (ods)<br><br>* Data Integration Layer (dwi)<br><br>* Basic Dimensions (dim)<br><br>* Detailed data layer (dwd)<br><br>* Intermediate data layer (dwm)<br><br>* Data Warehouse Service (dws)<br><br>* data warehouse application layer (dwa)<br><br>* Data Market Layer (dm)<br><br>* Application Service Layer (ads)<br><br>* application layer<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">This parameter is required only when the <strong>category type</strong> is <strong>model specification category</strong>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If there is a multi\-level category directory and <strong>whether to force table naming</strong> is all <strong>Yes</strong>, the table prefix will be concatenated according to the hierarchy.</div><br> |
      |\*Whether to enable |You can choose whether to enable this category.<br><br>This parameter is supported only when setting **data classification**. |
      

   * Edit category

      Click the **Edit** button in the **Action** column of a category to modify its configuration information.

   * Category sorting

      Click the **Category Sorting** button, and in the pop\-up window, adjust the display order of categories within the same level. After adjustment, its subcategories will also be adjusted accordingly.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Adjusting data classification changes its display order on the <strong>Asset Catalog</strong> page; adjusting album classification changes its order on the <strong>Asset Album</strong> page.      </div>
      

   * Delete category

      Click the **Delete** button in the **Action** column of a category entry, and after confirmation, the entry can be deleted.

   * Add category introduction

      Click the **New category introduction** button to enter the new introduction page. After setting the relevant information, click **Save** to complete adding.

      
      |Parameters |Description |
      |---|---|
      |**Basic Information** ||
      |\*Data Classification |To set the introduction information for the data classification, select from the created data classifications in the dropdown. |
      |\*Creation method |The creation method for category introduction supports **creat locally** and **existing link address** options. |
      |\*Link |When **Creation method** is set to **existing link address**, enter the correct link here. |
      |\*Effective Status |You can choose whether this introduction is valid. It is enabled by default.<br><br>Once enabled, the Category introduction button will only appear under the corresponding data classification in the **Asset Catalog**. |
      |\*Default display |You can choose to enable default display. The default setting is off.<br><br>This setting determines whether the category introduction side panel appears when entering the **Asset Catalog**.<br><br><br>* If enabled, the corresponding data classification side panel of the **Asset Catalog** will open automatically showing the **category introduction**.<br><br>* If disabled, only the category introduction button will appear when entering the corresponding classification in the **Asset Catalog**, with the panel collapsed by default. |
      |**Content editing** ||
      |Content |Detailed content of the asset overview introduction. |
      

   * Edit category introduction

      Click the **Introduce** button in the **Action** column of a category entry to modify its configuration information.

   * Enable/disable category

      Click the **Enable/Disable** icon in the **Enabled State** column of a category entry, and after confirmation, you can disable or enable the category.

      * After a category is disabled, its assets will be changed to uncategorized.

      * After enabling the category, assets already listed under this category can be searched in the Asset Catalog.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Data classification and album classification are not interchangeable and require separate creation and management.</div>


* <div data-tips="true" data-tips-type="tip">Only categories without attached assets can be deleted.</div>


* <div data-tips="true" data-tips-type="tip">Only <strong>data classification</strong> supports the <strong>category introduction</strong> feature.</div>



<span id="b6589ec3"></span>
## Subsequent Operations


* After creating a data classification, manage and publish assets by category as needed. For related instructions, see [Asset Circling](https://docs.byteplus.com/docs/dataleap/Asset_Circling). After publishing, the asset will appear under the corresponding data classification on the **Asset Catalog** page.

* After creating an album category, you can manage albums. For related instructions, see [Album Management](https://docs.byteplus.com/docs/dataleap/Album_Management). After publishing, the album will appear under the corresponding album category on the **Asset Album** page.
