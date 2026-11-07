---
title: "View LAS Catalog Tables"
product: "DataLeap"
product_code: "dataleap"
source: "https://docs.byteplus.com/en/docs/dataleap/View_LAS_Catalog_Tables"
---

This article explains how to view and manage the data details of LAS Catalog tables.

<span id="_1-前提条件"></span>
## **Prerequisites**

Before searching, create a new collector on the **Catalog \> Metadata Ingestion** page to collect the cluster's metadata into the Data Catalog. Refer to the [Metadata Ingestion](https://docs.byteplus.com/docs/dataleap/Metadata_Ingestion) operating instructions for related operations.

<span id="_2-检索数据"></span>
## **View Data Details**


1. Log in to the DataLeap console.

2. Select **Overview \> Catalog \> Search** to enter the **Search** page.

3. After searching data, enter the data details page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/66c5f901d48a4b88ba192f181b944127~tplv-goo7wpa0wc-image.image) </span>

4. You can view data details and manage data.

   * Summary information at the top of the page

      * You can view the table name, metadata completion, and other information. The completion is calculated as: owner 20%, table description 20%, field description 30% (based on field fill rate), business domain 15%, hierarchy 15%.

      * You can see the number of likes and favorites, and click the respective icons to like or favorite the table.

      * Click the **SQL query** button to display the generated SQL query statement in the pop\-up window.

      * You can quickly check whether the logged\-in account has operation permissions for the table. If not, the page shows the **permission application** button, which you can click to apply for permission. For related operations of permission application, see [Apply Permission](https://docs.byteplus.com/docs/dataleap/Apply_Permission).

         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c349285115e444c9b1e883663ff9544f~tplv-goo7wpa0wc-image.image) </span>

   * Table schema details, including detailed information, usage instructions, lineage, and other feature information.

   * The right sidebar shows basic information about the table, including basic info, business info, security info, and technical info.


<span id="_4-管理表结构信息"></span>
## Manage Table Schema Information

<span id="_4-1-明细信息"></span>
### Detailed Information


1. Log in to the DataLeap console.

2. Select **Overview \> Catalog \> Search** to enter the **Search** page.

3. After searching the data table, enter the table details page.

4. Click the **Detailed Information** tab to enter the table overview page.

5. You can view the table's field information, partition info, and change log, and perform the following operations:

   * Field Info

      * Enter the field name or description keyword in the search box, then click the search icon on the right to view matching information.

      * Click the **Edit** button to modify field info. Click the **Save** button, check the prompt in the confirmation dialog, then click **OK** to complete the modification.

         The following table explains the parameters related to the LAS Formation table. Parameters marked with \* are required; those without \* are optional.

         
         |Parameter |Description |
         |---|---|
         |Primary Key |The primary key is one or more fields in the table whose value uniquely identifies a record in the table.<br><br>You can choose whether to set a field as the primary key. If it is a composite primary key, select multiple columns |
         |\*English Name |The English name of the field, supporting only lowercase English letters, numbers, and underscores. |
         |\*Field Type |Fill in according to the actual situation. Multiple type options are available from the dropdown. |
         |\*Field Description |Explanation of the field for later management. |
         |Custom Label |Tags set for fields support the following two methods:<br><br><br>* Select existing tags from the dropdown, with keyword search to quickly choose.<br><br>* Set tags manually: Enter tags manually, then select the tag from the dropdown list. |
         |Business line tags |Set business line tags for fields. Select multiple tags from those created under the associated business line in the dropdown.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Choose the corresponding created tags only after selecting <strong>Business line</strong>.</div><br> |
         

         <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="3">tip         </div>
         

         * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="3">Before modifying field names or types, check downstream affected tasks through <strong>Lineage</strong> and notify the relevant task owners to make necessary changes to prevent errors in generated tasks and downstream dependencies caused by modifications.         </div>
         

         * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="3">After modifying fields, you can reactivate the task.         </div>
         

      * Click the **Show DDL** button to view the table’s SQL definition statement.

   * Partition Information

      * Enter the keyword for the partition field in the search box and click the search icon on the right side of the box to view matching partition info.

      * Select the partition creation time to view partition info within the corresponding time period.

      * In the partition info list, some parameters support ascending and descending sorting.


<span id="2dc47679"></span>
### Preview Profiling


1. Log in to the DataLeap console.

2. Select **Overview \> Data Catalog \> Search** to enter the **Search** page.

3. After searching the table, enter the table details page.

4. Click the **Preview & Exploration** tab to enter the profiling page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e47f20f7aef44e139962ead7a641656b~tplv-goo7wpa0wc-image.image) </span>

5. You can view several data entries of the table and profiling results, and perform the following actions:

   * Data preview

      You can preview the current table's data and perform the following actions:

      * Select a queue from the queue dropdown list, then click the refresh icon next to it to query using the currently selected queue.

         <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="3">tip         </div>
         

         <div data-tips="true" data-tips-type="tip" data-wrapper-indent="3">When previewing data, the system automatically selects the default queue. If there is no default queue, manually select a queue with permission to query.         </div>
         

      * Click **Hidden column** to hide or show the field list. When a field is checked, it is displayed in the worksheet; when unchecked, it is hidden.

      * Click **Search**, enter the keyword in the search box that appears, and press Enter to search for the corresponding information.

   * Dynamic Probe

      Probe results can be sampled, filtered, grouped by, columns deleted, and reordered as needed. For detailed operating instructions, see [Dynamic Probe](https://docs.byteplus.com/docs/dataleap/Dynamic_Probe).

   * Full exploration

      Click the Probe button on the Full exploration page to directly jump to the **Create Probe** page for this table, create a probe, and generate a probe report. For detailed operating instructions, see [Full Probe](https://docs.byteplus.com/docs/dataleap/Full_probe).

      * If data has not been probed, the probe report cannot be viewed here. Click the **Go to explore** button to create a probe.

      * If data has been probed, you can view the probe report and click the **I want to probe** button to create a new probe.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">If you lack read permission for a table, opening the table’s <strong>Profiling</strong> page will show a no\-permission notice. You must apply for access before viewing.</div>


<span id="_4-2-预览探查"></span>
### Usage Instructions

This feature allows you to write the usage instructions document for a data table, usually authored by the Table owner. The related operation steps are as follows:


1. Log in to the DataLeap console.

2. Select **Overview \> Catalog \> Search** to enter the **Search** page.

3. After searching the table, enter the table details page.

4. Click the **Usage Instructions** tab to go to the add instructions for use page.

5. Click the **Click Add** button, and in the pop\-up side window, after setting the instructions content, click the **Save** button to add the first description category content. After completion, the Add button changes to the **Add instructions for use** button, allowing you to add more classifications.

   
   |Parameters |Description |
   |---|---|
   |Description category name |Classification titles for the description can be added multiple times to set up multiple classifications. |
   |Editing tools |The editing tools used for the configuration description support two options: **Text editor** and **Configure hyperlink**, which are selectable from a dropdown. |
   |Content |Enter a description.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When <strong>Editing tools</strong> is set to <strong>Text editor</strong>, this parameter needs to be set.</div><br> |
   |\*Link |Enter the link for the description content to be set.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When <strong>Editing tools</strong> is set to <strong>Configure hyperlink</strong>, you need to set this parameter.</div><br> |
   

6. You can also edit and delete added content.

   * Click the  **︙ \> Edit** button for a description classification to edit the information for that classification.

   * Click the  **︙ \> Delete** button for a description classification. After a second confirmation, you can delete the information for that classification.


<span id="_4-4-生产信息"></span>
### Production Information


1. Log in to the DataLeap console.

2. Select **Overview \> Catalog \> Search** to enter the **Search** page.

3. After searching for a data table, enter the table details page.

4. Click the **Production information** tab to enter the production information page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8524ae7be0eb45d6bfcd6103cca7f693~tplv-goo7wpa0wc-image.image) </span>

5. You can view this table's operation and script information and perform the following actions:

   * Operation information

      * Select a task from the dropdown list and set the operation time range to view the task status within that period.

      * Click the task name in the operation list or the **task** button in the **action** column to jump to the Data Development task configuration page.

      * Click the **log** button in the **action** column of a record in the operation list to jump to the instance log page and view instance information.

   * Script information

      * Click the **view task details** icon after the task to jump to the Data Development task configuration page.

      * Click to expand the task to view its script information.


<span id="_4-5-血缘关系"></span>
### Lineage

This is used to see which tables contribute data to this table, representing its upstream lineage, and which tables are generated using this table's data, representing its downstream lineage, and to manage them accordingly. Lineage is displayed in two ways: table view and visual chart.

<span id="_4-5-1-表格视图"></span>
#### Table View


1. Log in to the DataLeap console.

2. Select **Overview \> Catalog \> Search** to enter the **Search** page.

3. After searching for a table, enter the table details page.

4. Select the **Lineage Relationship \> Table view** tab to enter the table view of the lineage page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/345ae831e9d34e0a9318afcf68d4b111~tplv-goo7wpa0wc-image.image) </span>

5. The following operations are available:

   * Set viewing conditions to see data that meets the criteria, including data asset nodes, fields, lineage levels, node owners, task names, and mandate holders.

      * Filtering granularity: includes tables, columns, and partitions.

      * View scope: includes view all, upstream only, and downstream only.

      * Levels: 1 to 5 levels.

      * Search: enter table name, task name, etc., to find specific objects.

      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div>
      

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">Lineage is updated in real time, meaning new dependencies are updated immediately in the lineage relationships.      </div>
      

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">If lineage cannot be parsed automatically or the parsing is inaccurate, supplement it by manually registering on the <strong>Data Development \> Task Development \> Schedule Settings</strong> page.      </div>
      

   * Click the **Download Info** button on the right to save node data from the list locally in CSV format for browsing.

   * Set quick notification

      1. Select one or more node data entries from the list and click the **Quick notification** button on the right to open the **Quick notification** window.

      2. Configure notification details and click the **Notify** button to open the confirmation dialog.

      3. Click the **Confirm** button to complete the setup. When upstream or downstream node tables change, the system sends notifications to the registered email addresses of target users.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Only the table owner can set up quick notifications, which currently support only the “Email” notification method.      </div>
      

<span id="_4-5-2-可视化图表"></span>
#### Visual Graph

Visual charts display in three modes: table view, column view, and partition view.


1. Log in to the DataLeap console.

2. Select **Overview \> Catalog \> Search** to enter the **Search** page.

3. After searching the Table, enter the Table Detail page.

4. Select the **Lineage \> Visual Graph** tab to enter the visual chart page for Lineage.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a0cfa50b6471490e8de77414e2ac9f7f~tplv-goo7wpa0wc-image.image) </span>

5. The following query operations are available:

   * **Table view**

      * Range x levels: You can select the node range, including hierarchy (1 level to 5 levels) and upstream and downstream node information, to display all selected levels of upstream and downstream in the chart.

      * Group: Node information can be displayed in groups, and group results will be shown in the chart.

      * Filter: You can filter one or multiple data types to display corresponding node information, narrowing the node search range.

      * Property display: You can select one or more properties to display in the list. You can display up to 3 properties simultaneously.

      * The three icon buttons in the upper right corner are full screen, reset, and download CSV.

      * Clicking a node highlights the path from that node to the primary node, while other nodes will be dimmed; clicking the blank area in the graph interaction zone again cancels the highlight.

      * You can click the table name to view the node and task information in the information panel on the right. The node information panel also allows the following operations:

         * Click the **view table details** button to navigate to the data search page and see the detailed information of the table.

         * Click the **switch to primary node** button to change a non\-primary node table to the primary node for display.

   * **Column view**

      * Primary node fields: display the lineage of one or more primary node fields. You can display up to five fields simultaneously.

      * Range x levels: select the node range, including hierarchy (1 to 5 levels) and upstream/downstream node information, to display all selected upstream and downstream levels in the graph.

      * The three icon buttons at the top right are Full Screen, Reset, and Download CSV.

      * Clicking a field node highlights the path from that node to the primary node, while other nodes dim; clicking the blank area in the graph interaction zone again cancels the highlight.

      * Click the table name to view the node and task information in the information panel on the right. The node information panel also supports the following actions:

         * Click the **View table details** button to jump to the data search page to see detailed information of the table.

         * Click the **Switch to primary node** button to display a non\-primary node table as the primary node.

   * **Partition view**

      * You can select the range (show all, show only upstream, or show only downstream) and hierarchy (1 to 5 levels) to display all upstream and downstream nodes of the selected levels in the graph. The four buttons below the hierarchy range are Centered, Zoom In, Zoom Out, and Full Screen/Exit Full Screen.

      * Enter keyword tags to facilitate searching for key information.

      * Category aggregation: Filter by category conditions to display the same type of information in the corresponding label tooltip.

      * Click a node to highlight the node and its upstream and downstream, while other nodes will be dimmed; click the node again to cancel the highlight. You can also hold down on the blank area of the interactive graph and move the mouse to pan the graph accordingly.

      * Click the table name to view the node and task information of the table in the right information panel.


<span id="738fa268"></span>
### Comments and Q&A

This feature supports viewing the comments and Q&A information for the table, and also allows posting comments and questions.


1. Log in to the DataLeap console.

2. Select **Overview \> Catalog \> Search** to enter the **Search** page.

3. After searching for a data table, enter the table detail page.

4. Click the **Comments and Q&A** tab to open the comments and Q&A page.

5. You can perform the following operations:

   * In the search box, search for a comment subject, then click the subject to view the table’s comments and Q&A information by category.

   * Click the **comment** button to fill in the comment information.

   * Click the **I have a question** button to ask the owner a question.

   * Edit or delete comments and Q&A you created.

      Hover over an item and click the displayed icon button to edit or delete the item.


<span id="_5-管理表信息"></span>
## **Manage Table Basic Information**


1. Log in to the DataLeap console.

2. Select **Overview \> Catalog \> Search** to enter the **Search** page.

3. After searching for a table, go to the table details page.

4. You can view the table's basic information, business information, and other details and perform the following management operations:

   * Hover over a parameter, click the displayed edit icon, modify the parameter information, then click the confirm icon to complete the change.

   * Click the on/off icon button of **Is Hidden** to decide whether to hide the table’s security information.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When hovering the mouse, only parameters that show an edit icon can be edited.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Only accounts with read and write permissions on a LAS Catalog table can edit its information. Accounts without permission can request it via the <strong>Permission application</strong> button shown at the top right of the page. For related operations on requesting permissions, see <a href="https://docs.byteplus.com/docs/dataleap/Apply_Permission">Apply Permission</a>.   </div>
   


The following table explains the parameters related to table information.


|Parameters |Description |
|---|---|
|**Summary information at the top of the page** ||
|Data type |show the type of this data. |
|data classification |show the business line classification of this table. In "Asset Directory", specify the file directory name under the business line for asset portal construction. |
|business line tags |show the business line tags of this table. |
|**basic information** ||
|Chinese name |the Chinese name of the data table, editable. |
|description |Description of metadata, editable. |
|Owner |The owner of this metadata, not editable. |
|Manage business line |The business line this metadata belongs to, editable. Select from the dropdown of created business lines. |
|Data layer |The layer where the data table is located, editable. Supports the following options, selectable from dropdown. Supports quick selection by searching layer name keywords.<br><br><br>* Operational Data Store (ODS)<br><br>* Data Integration Layer (DWI)<br><br>* Basic Dimensions<br><br>* Detailed data layer<br><br>* Intermediate data layer<br><br>* Data Warehouse Service<br><br>* Data warehouse application layer<br><br>* Data Market Layer<br><br>* Application Service Layer<br><br>* Application layer |
|Modeling specification category |Show the modeling specification category used by this metadata; editable. The dropdown allows selection of model specification categories created under the business line. |
|Project |The project to which the data table belongs, editable with a dropdown of created projects. |
|Is Core Asset |show whether the table is core; editable. |
|View Count |show the number of visits to the table in the last 30 days, updated in real time. |
|**Business information** ||
|Business Lines |The asset portal business line to which the table belongs. |
|Business domain |business domain to which the metadata belongs; editable, with a dropdown to select from created business domains.<br><br>supports quick selection by searching business domain name keywords. |
|Product line |The product line to which the metadata belongs; editable with a dropdown to select from created product lines.<br><br>Support quick selection by searching product line name keywords. |
|Theme |The theme to which the metadata belongs; editable with a dropdown to select from created themes.<br><br>Support quick selection by searching theme name keywords. |
|Custom label |Labels set for the metadata; editable and supports the following two methods:<br><br><br>* Select existing labels from the dropdown, supporting quick selection by searching label keywords.<br><br>* Set labels manually: after typing the label, select it from the dropdown list. |
|Business glossary |The business glossary associated with metadata is editable, with a dropdown to select from created business glossaries.<br><br>Supports quick selection by searching business glossary name keywords. |
|**Security Information** ||
|Confidentiality Level |The table's confidentiality level is editable, with four selectable options: L1, L2, L3, and L4. Different confidentiality levels correspond to different approval processes.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The table's classification cannot exceed that of the DB it belongs to.</div><br> |
|Authority Owner |The person responsible for the table's data security permissions is editable and supports assigning multiple owners.<br><br>This authority owner only displays the table authority owner. For row/column authority owners, go to **Security \> Authorization Management \> Authority Settings** to view, change, and other operations. |
|Database authority owner |The authority owner of the database to which this table belongs, not editable. |
|My Permissions |The current account’s operation permissions on this table, not editable.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Only accounts with read and write permissions can edit metadata. The main account has default access rights to all data.</div><br> |
|Is Hidden |Indicates whether this table is hidden, editable.<br><br>After the table is hidden, if you are not the database manager or table owner and do not have read and write permissions on this table, you cannot view its detailed information on the **Search** page. |
|**Technical Information** ||
|LAS Catalog Name |Display the name of the LAS Catalog data directory to which the table belongs. |
|Database name |Name of the database to which the table belongs. Click the database name to access its details page and view more information. |
|Is Partitioned |Shows whether the data table is partitioned. |
|LAS Catalog table type |Displays the type of table. You can participate in the operation to set the table type [Manage LAS Catalog Tables](https://docs.byteplus.com/docs/dataleap/Manage_LAS_Catalog_Tables). |
|Creation time |Show the table's creation time. |
