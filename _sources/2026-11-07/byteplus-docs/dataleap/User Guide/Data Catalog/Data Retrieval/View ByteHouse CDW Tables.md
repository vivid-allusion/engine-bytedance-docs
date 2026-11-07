---
title: "View ByteHouse CDW Tables"
product: "DataLeap"
product_code: "dataleap"
source: "https://docs.byteplus.com/en/docs/dataleap/View_ByteHouse_CDW_Tables"
---

This article introduces how to view and manage the data details of ByteHouse CDW tables.

<span id="_1-前提条件"></span>
## **Prerequisites**

Before searching, create a collector on the **Catalog \> Metadata Ingestion** page to collect cluster metadata into the data catalog. Refer to [Metadata Ingestion](https://docs.byteplus.com/docs/dataleap/Metadata_Ingestion) for related operation instructions.

<span id="_2-检索数据"></span>
## **View Data Details**


1. Log in to the DataLeap console.

2. Select **Overview \> Catalog \> Search** to enter the **Search** page.

3. After searching data, go to the data details page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/97e34a4e5bc64ffeb144b6b02dfe7f51~tplv-goo7wpa0wc-image.image) </span>

4. View data details and perform data management.

   * summary information located at the top of the page

      * View the table name, metadata completion, and other information. The completion calculation is: owner 20%, table description 20%, field description 30% (calculated by field fill rate), business domain 15%, levels 15%.

      * View likes and number of favorites; click the corresponding icon to like or favorite the table.

      * Click the **SQL query** button to display the generated SQL query statement in the popup window.

      * Click the **Copy table** icon button to copy the table information and open the create table page to create a new data table as needed. Refer to [Manage ByteHouse CDW Tables](https://docs.byteplus.com/docs/dataleap/Manage_ByteHouse_CDW_Tables) for related instructions on table creation operations.

      * You can quickly check whether the logged\-in account has permission to operate on this table. If not, the page displays an **Apply permission** button, which can be clicked to request access. Refer to [Apply Permission](https://docs.byteplus.com/docs/dataleap/Apply_Permission) for related operations on requesting permissions.

   * Details of the table schema information, including detailed table info, introduction, lineage, and other feature information.

   * The basic information of the data table in the right info panel includes basic information, business info, and technical info.


<span id="_4-管理表结构信息"></span>
## Manage Table Schema Information

<span id="_4-1-明细信息"></span>
### Detailed Information


1. Log in to the DataLeap console.

2. Select **Overview \> Catalog \> Search** to enter the **Search** page.

3. After searching the table, enter the table details page.

4. Click the **Details** tab to view the detailed information page of the table.

5. You can view the field information and change log of the table.

   * Field Info

      * Enter a keyword in the search box for the field name or description, and click the search icon on the right side of the search box to view matching information.

      * Click the **Edit** button to modify the field information, then click the **Save** button and confirm to complete the modification.

         
         |Parameter |Description |
         |---|---|
         |\*English Name |The field's English name. It must start with a letter or underscore and can include letters, numbers, and underscores. |
         |\*Field Type |Fill in according to actual conditions. Multiple types are supported and selectable from a dropdown. |
         |\*Field Description |A description of the field for subsequent management. This is a required field. |
         |Default value |Set the default value of the field yourself.<br><br>The default value can be an expression or a constant. For constant values of String or Time type, please enclose the input value in single quotes, such as 'Hello Word' and '1970\-01\-01'. |
         |Can be empty |You can choose whether this field can be empty. |
         

         <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="3">tip         </div>
         

         * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="3">Primary key fields and partition fields cannot be deleted and only support modifying the field description.         </div>
         

         * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="3">You can add new fields, and please note:         </div>
         

            * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="3">Before changing the field name or type, check the downstream affected tasks via <strong>Lineage</strong> and notify the responsible persons to make corresponding adjustments to avoid generation task and downstream dependency errors caused by the change.         </div>
         

            * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="3">After changing the field name or type, you can reactivate the task.         </div>
         

      * Click the **comment** or **Q&A** button in the **Comments and Q&A** column for a field in the list. On the corresponding comments and Q&A page, you can add comments or raise questions, then click the **submit** button to post. The page displays the latest published information, which you can edit or delete.

   * Partition info

      Set search criteria to view partition info that matches the conditions.


<span id="_4-2-预览探查"></span>
### Preview Profiling


1. Log in to DataLeap console.

2. Select **Overview \> Catalog \> Search** to enter the **Search** page.

3. After searching for a table, enter the table detail page.

4. Click the **Preview & Exploration** tab to enter the profiling page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7cdbeccda8404de4a9efbdf7633287ee~tplv-goo7wpa0wc-image.image) </span>

5. You can view some data from the table and profiling results, and perform the following actions:

   * Data preview

      You can preview the current table's data and perform the following actions:

      * Click **Hide column** to hide or show the field list. When a field is checked, it shows in the worksheet; when unchecked, it hides in the worksheet.

      * Click **Search**, enter the keyword in the search box that appears, and press Enter to find the corresponding information.

   * Full exploration

      Click the explore button on the full exploration page to jump directly to the **Create Probe** page for the table, create a probe, and generate a report. See [Full Probe](https://docs.byteplus.com/docs/dataleap/Full_probe) for detailed operating instructions.

      * If the data has not been profiled, the report cannot be viewed here. Click the **Go to explore** button to create a probe.

      * If the data has been profiled, you can view the report and click the **I want to probe** button to create a new probe.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">If you do not have read permission for a data table, opening the <strong>Profiling</strong> page of that table will notify you of no permission. You need to apply for permission to view it.</div>


<span id="b000357c"></span>
### Usage Instructions

This feature allows you to write usage documentation for data tables, usually authored by the table owner. The related steps are as follows:


1. Log in to the DataLeap console.

2. Select **Overview \> Catalog \> Search** to enter the **Search** page.

3. After searching for a table, enter the table details page.

4. Click the **Introduction** tab to add usage instructions.

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


<span id="_4-5-血缘关系"></span>
### Production Information


1. Log in to the DataLeap console.

2. Select **Overview \> Catalog \> Search** to enter the **Search** page.

3. After searching for a table, enter the table details page.

4. Click the **Production information** tab to open the page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8524ae7be0eb45d6bfcd6103cca7f693~tplv-goo7wpa0wc-image.image) </span>

5. You can view the table's operation information and script information and perform the following actions:

   * operation information

      * Select a task from the dropdown list and set the run time period to view the task’s operation status within that period.

      * Click the **task** button in the **Action** column of the run list to go to the Data Development task configuration page.

      * Click the **log** button in the **Action** column of the run list to go to the instance log page and view instance information.

   * script information

      * Click the **view task details** icon after the task to go to the Data Development task configuration page.

      * Click to expand the task to view its script information.


<span id="bcc62cff"></span>
### Lineage

Use this to see which tables contribute data to this table, i.e., the table’s upstream lineage, and which tables are generated from this table’s data, i.e., the table’s downstream lineage, and manage them accordingly. Lineage is displayed in two ways: table view and visual chart.

<span id="_4-5-1-表格视图"></span>
#### Table View


1. Log in to the DataLeap console.

2. Select **Overview \> Catalog \> Search** to enter the **Search** page.

3. After searching for the table, enter the table details page.

4. Select the **Lineage Relationship \> Table view** tab to enter the table view of lineage.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7c1987d2674c4aae97866f5aa9152e96~tplv-goo7wpa0wc-image.image) </span>

5. You can perform the following actions:

   * Set viewing conditions to see data that meets the criteria, including data asset nodes, fields, lineage levels, node owners, task names, and task owners.

      * Filter granularity: includes table, field, partition.

      * View range: includes view all, upstream only, downstream only.

      * Levels: 1 to 5 levels.

      * Search: enter table name, task name, etc., to find specific objects.

      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div>
      

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">The lineage updates in real time, meaning new dependencies are immediately reflected in the lineage.      </div>
      

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">If lineage cannot be automatically parsed or is inaccurate, you can supplement it manually on the <strong>Data Development \> Task Development \> Schedule Settings</strong> page.      </div>
      

   * Click the **Download Info** button on the right to save the node data in the list as a CSV file for local browsing.

   * Set quick notification

      1. Select one or more node data items in the list, then click the **Quick notification** button on the right to open the **Quick notification** window.

      2. Configure the notification information, then click the **Notification** button to open the notification confirmation dialog.

      3. Click the **Confirm** button to complete the setup. When upstream or downstream node table change information occurs, the system will send the notification to the email registered by the target user.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Only the table owner can set quick notifications, which currently support email only.      </div>
      

<span id="_4-5-2-可视化图表"></span>
#### Visual Graph

Visual charts display in three modes: table view, column view, and partition view.


1. Log in to the DataLeap Console.

2. Select **Overview \> Catalog \> Search** to enter the **Search** page.

3. After searching the table, enter the table details page.

4. Select the **Lineage Relationship \> Visual Graph** tab to enter the visual chart page of lineage.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/10b1a77489a949b78de4d7b1f2e5ca79~tplv-goo7wpa0wc-image.image) </span>

5. You can perform the following query operations:

   * **Table view**

      * Range x levels: You can select the node range, including levels (1 level to 5 levels) and upstream and downstream node information, to display all selected levels' upstream and downstream in the chart.

      * Grouping: You can group node information, and the grouping results will appear in the chart.

      * Filtering: You can filter one or more data types to show corresponding node information, narrowing the search scope of nodes.

      * Property display: You can select one or more properties to show in the list. Up to three properties can be displayed simultaneously.

      * The three icon buttons in the upper right corner are Full Screen, Reset, and Download CSV.

      * Clicking a node highlights the path from that node to the primary node, while other nodes fade; clicking the blank area in the graph interaction zone again cancels the highlight.

      * You can click the table name to view the node information and task info in the information panel on the right. The following operations are available in the node information panel:

         * Click the **View table details** button to jump to the data search page and view the table overview.

         * Click the **Switch to primary node** button to display a non\-primary node table as the primary node.

   * **Column view**

      * Primary node fields: displays the lineage relationship of one or more primary node fields. A maximum of 5 can be displayed simultaneously.

      * Range x levels: select the node range, including levels (1 level to 5 levels) and upstream and downstream node information, to display all selected levels’ upstream and downstream in the graph.

      * The three icon buttons at the top right are Full Screen, Reset, and Download CSV.

      * Click a field node to highlight the path from that node to the primary node, while dimming others; click the empty area in the graph interaction zone again to cancel the highlight.

      * Click the table name to view the table's node information and task info in the information panel on the right. The node information panel also supports the following operations:

         * Click the **View table details** button to navigate to the data search page and see the table's overview.

         * Click the **Switch to primary node** button to display a non\-primary node table as the primary node.

   * **Partition view**

      * You can select range (show all, upstream only, or downstream only) and hierarchy (1 level to 5 levels) to display all upstream and downstream nodes within the selected levels in the graph. The four buttons below the hierarchy range are Centered, Zoom In, Zoom Out, and Full Screen/Exit Full Screen.

      * You can enter keyword tags to facilitate searching for key information.

      * Classification aggregation: Filter by classification conditions to display similar information in the corresponding tag's tooltip.

      * Click a node to highlight it along with its upstream and downstream nodes; other nodes will be dimmed. Click the node again to cancel the highlight. You can also click and hold the blank area in the interaction graph, then move the mouse to pan the graph.

      * Click the table name to view the node and task information in the right sidebar.


<span id="767ca40e"></span>
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

3. After searching the data table, go to the table detail page.

4. You can view the table's basic information, business information, and other details. Hover over a parameter, click the displayed edit icon, modify the parameter information, then click the confirm icon to complete the change.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When hovering the mouse, only parameters that show an edit icon can be edited.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Only the owner of ByteHouse CDW tables can edit the tables they are responsible for.   </div>
   

   The table below explains the parameters related to data table information.

   
   |Parameter |Description |
   |---|---|
   |**Summary information at the top of the page** ||
   |Data type |Shows the type of this data. |
   |Data Categories |Show the business line classification this table belongs to. In "Asset Directory," specify the file directory name under the business line for asset portal construction. |
   |Business line tags |Show the business line tags for this table. |
   |**Basic information** ||
   |Chinese name |The editable Chinese name of this metadata. |
   |Description |The description of metadata, not editable. |
   |Owner |The owner of this metadata, not editable. |
   |Managing Business Line |The business line this metadata belongs to, editable. Choose from created business lines in the dropdown. |
   |Data Layer |The layer of the data table, editable, supports the following options, selectable from the dropdown. Supports quick selection by searching for hierarchy name keywords.<br><br><br>* Operational Data Store (ods)<br><br>* Data Integration Layer (dwi)<br><br>* Basic Dimensions Layer (dim)<br><br>* detailed data layer (dwd)<br><br>* intermediate data layer (dwm)<br><br>* data warehouse service layer (dws)<br><br>* data warehouse application layer (dwa)<br><br>* data market layer (dm)<br><br>* application service layer (ads)<br><br>* application layer (app) |
   |Modeling specification categories |display the modeling specification category used by this metadata; editable, with a dropdown to select from the model specification category types created under the business line |
   |Project |The project to which the table belongs, editable, selectable from the created projects dropdown. |
   |Is Core Asset |Show whether the table is core, editable. |
   |**Business Information** ||
   |Business Lines |The asset portal business line to which the table belongs. |
   |Business domain |The business domain of the metadata, editable, dropdown allows selecting created business domains.<br><br>Supports quick selection by searching business domain name keywords. |
   |Product line |The product line to which the metadata belongs, editable, with a dropdown to select from created product lines.<br><br>Supports quick selection by searching product line name keywords. |
   |Theme |The theme to which the metadata belongs, editable, with a dropdown to select from created themes.<br><br>Supports quick selection by searching theme name keywords. |
   |Custom label |Labels set for the metadata, editable, supporting the following two settings:<br><br><br>* Dropdown to select existing labels, supporting quick selection by searching label keywords.<br><br>* Set labels manually: after manually entering a label, select it from the dropdown list. |
   |Business glossary |The business glossary associated with the metadata is editable, with a dropdown to select created business glossary terms.<br><br>Supports quickly selecting by searching business glossary term name keywords. |
   |**Security Information** ||
   |Confidentiality Level |The table's confidentiality level is editable, with four options: L1, L2, L3, and L4. Different confidentiality levels correspond to different approval processes.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">the classification level of the table cannot exceed that of its database</div><br> |
   |Authority Owner |The table's data security authority owner is editable, supporting multiple settings.<br><br>This authority owner only shows the table authority owner. Row/column authority owners can be viewed and changed by going to **Security \> Authorization Management \> Authority Settings**. |
   |Database authority owner |The owner of the database this table belongs to, not editable. |
   |My Permissions |The current login account’s permissions for this table, not editable.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">only accounts with read\-write permissions can edit metadata; the main account has access to all data by default</div><br> |
   |**Technical Information** (view only) ||
   |Database name |Displays the name of the database this table belongs to. |
   |Primary Key |The primary key is one or more fields in the table whose values uniquely identify a record in the table. This field is configured when creating the table and cannot be edited here. |
   |Is partitioned |Indicates whether the data table is partitioned. |
   |Partition key |Displays the partition key of the data table. |
   |Unique key |Displays the unique key of the data table. |
   |Logical table size |show the size of the corresponding logical table |
   |Creation time |show the table creation time |
   |Update time |show the table's most recent update time, which updates automatically after editing other data source information |
