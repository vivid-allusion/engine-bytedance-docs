---
title: "View LAS Schema DB"
product: "DataLeap"
product_code: "dataleap"
source: "https://docs.byteplus.com/en/docs/dataleap/View_LAS_Schema_Library"
---

This article introduces how to view and manage the data details of the LAS Catalog DB.

<span id="_1-前提条件"></span>
## **Prerequisites**

Before searching, create a collector on the **Catalog \> Metadata Ingestion** page to collect cluster metadata into the Data Catalog. For related instructions, see [Metadata Ingestion](https://docs.byteplus.com/docs/dataleap/Metadata_Ingestion).

<span id="_2-检索数据"></span>
## **View Data Details**


1. Log in to the DataLeap console.

2. Select **Overview \> Catalog \> Search** to enter the **Search** page.

3. After searching data, enter the data details page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d7deea5b64d744f2989fe51f63b27d44~tplv-goo7wpa0wc-image.image) </span>

4. You can view data details and manage data.

   * Summary information located at the top of the page

      * You can view the database name, data type, and more.

      * You can view the number of likes and favorites, and click the corresponding icons to like or favorite the database.

   * Database details

   * Basic database information in the right sidebar, including basic info and technical info.


<span id="_4-管理表结构信息"></span>
## Manage Overview


1. Log in to the DataLeap Console.

2. Select **Overview \> Catalog \> Search** to enter the **Search** page.

3. After searching the database, enter the data details page.

4. Click the **Detail Info** tab to enter the database details page.

5. You can view the database details and perform the following actions:

   * Enter the table name or Chinese name keyword in the search box to view matching information.

   * Click the table name in any record to jump to the table details page.


<span id="_5-管理表信息"></span>
## **Manage Basic Database Information**


1. Log in to the DataLeap console.

2. Select **Overview \> Catalog \> Search** to enter the **Search** page.

3. Search for a database and enter the data details page.

4. You can view the basic information of the database. Hover over a parameter, click the displayed edit icon to modify the parameter information, then click the confirm icon to complete the modification.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Only parameters that display the edit icon can be edited when the mouse hovers over them.   </div>
   

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Only the person in charge of the LAS Catalog DB can edit the tables they manage.   </div>
   

   The table below describes the related database information parameters.

   
   |Parameters |Description |
   |---|---|
   |**Basic information** ||
   |Description |The metadata description is editable. |
   |Owners |The person in charge of this metadata, with a development role, is responsible for the daily operation of the database and can edit it. |
   |DB Usage |Show the usage of this database, editable. |
   |**Security Information** ||
   |Authority Admins |The person in charge of the database permissions, not editable.<br><br>The database authority owner, from a business perspective, can determine whether the data can be used openly and is the approver for the final step of permission approval. |
   |Privilege Status |The current logged\-in account's access rights to this database cannot be edited.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The main account has default access rights to all data.</div><br> |
   |**Tech Information** ||
   |LAS Catalog Name |Show the name of the LAS Catalog to which this database belongs. |
   |Cluster ID |Show the ID of the cluster to which this database belongs. |
   |Database size |Show the size of this database. |
   |Creation time |Show the creation time of this database. |
