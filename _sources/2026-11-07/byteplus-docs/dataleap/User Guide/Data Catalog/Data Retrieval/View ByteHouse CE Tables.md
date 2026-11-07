---
title: "View ByteHouse CE Tables"
product: "DataLeap"
product_code: "dataleap"
source: "https://docs.byteplus.com/en/docs/dataleap/View_ByteHouse_CE_Table"
---

This article introduces how to view and manage ByteHouse CE table data details.

<span id="_1-前提条件"></span>
## **Prerequisites**

Before searching, create a collector on the **Catalog \> Metadata Ingestion** page to ingest the cluster's metadata into the Data Catalog. Refer to [Metadata Ingestion](https://docs.byteplus.com/docs/dataleap/Metadata_Ingestion) for related operation instructions.

<span id="_2-检索数据"></span>
## **View Data Details**


1. Log in to the DataLeap console.

2. Select **Overview \> Catalog \> Search** to enter the **Search** page.

3. After searching data, enter the data details page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/05328f07772b49229db4b6c8f004e7a9~tplv-goo7wpa0wc-image.image) </span>

4. You can view data details and manage data.

   * Summary information at the top of the page

      * You can view table name, metadata completion, and other information. The completion calculation is: owner 20%, table description 20%, field description 30% (calculated by field fill rate), business domain 15%, hierarchy 15%.

      * You can view likes and number of favorites, and click the respective icons to like or favorite the table.

      * Click the **SQL query** button to display the generated SQL query in the popup window.

      * Click the **Copy table** icon button to copy the table information and open the create table page to create a new data table as needed. For related instructions on creating table operations, see [Manage ByteHouse CE Tables](https://docs.byteplus.com/docs/dataleap/Manage_ByteHouse_CE_Tables).

      * You can quickly check whether the logged\-in account has operation permission for this table. If not, the page shows the **Permission Application** button, which you can click to apply for permission. For related operations on applying for permission, see [Apply Permission](https://docs.byteplus.com/docs/dataleap/Apply_Permission).

   * Details of the table schema, including detailed information, usage instructions, lineage, and other functional information.

   * Basic information section on the right, including basic info, business info, security information, and technical info.


<span id="_4-管理表结构信息"></span>
## Manage Table Schema Information

<span id="_4-1-明细信息"></span>
### Detailed Information


1. Log in to the DataLeap console.

2. Select **Overview \> Catalog \> Search** to enter the **Search** page.

3. After searching the table, enter the table details page.

4. Click the **Details** tab to access the table details page.

5. You can view the field information and change log for the table.

   * Field Information

      * Enter field name or description keywords in the search box, then click the search icon on the right to view matching information.

      * Click the **Edit** button to modify the field information, then click the **Save** button and confirm to complete the modification.

         
         |Parameters |Description |
         |---|---|
         |\*English Name |The English name of the field, supporting only letters, underscores at the start, and combinations of letters, numbers, and underscores. |
         |\*Field Type |Fill in according to the actual situation, supporting multiple types with a dropdown selection. |
         |\*Field Description |Description of the field for subsequent management; this is a required field. |
         |Default Value |Set the default value for the field as needed.<br><br>The default value can be an expression or a constant. For String or Time type constants, enclose the input value in single quotes, such as 'Hello Word' and '1970\-01\-01'. |
         |Can be empty |You can choose whether this field can be empty. |
         

         <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="3">tip         </div>
         

         * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="3">Primary key fields and partition fields cannot be deleted, and only their descriptions can be modified.         </div>
         

         * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="3">You can add new fields, with the following considerations:         </div>
         

            * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="3">Before modifying the field name or type, check the downstream impact tasks through <strong>lineage</strong> and notify the corresponding task owners to make necessary adjustments to prevent errors caused by the changes in generated tasks and downstream dependencies.         </div>
         

            * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="3">After modifying the field name or type, you can redeploy the task.         </div>
         

      * Click the **Comment** or **Q&A** button in the **Comments and Q&A** column for any field in the list. On the corresponding comment or Q&A page, you can submit comments or questions by clicking the **Submit** button. The page displays the latest published information, which you can edit or delete.

      * Click the **Configuration** button in the **Security tag** column for any field in the list to jump to the **Data Security \> Security tag \> Discovery Result** path for that table’s detail page, where you can edit the field’s current tags. After configuring tags, the **Field Info** page displays the security tags of the field. For detailed instructions on configuring security tags, see [Discovery Result Management](https://www.volcengine.com/docs/6260/1188000).

   * Partition info

      Set search criteria to view partition info that meet the conditions.

   * Change Log

      * Enter keywords in the search box and click the search icon on the right to view matching change records.

      * Click the **Show diff** button in the **Change content** column of an item in the list to see a detailed comparison of changes in the pop\-up window.


<span id="_4-2-预览探查"></span>
### Preview Profiling


1. Log in to the DataLeap console.

2. Select **Overview \> Catalog \> Search** to enter the **Search** page.

3. After searching for the table, enter the table details page.

4. Click the **Profiling** tab to enter the profiling page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/859015d70e98496d9c486aa0cdbd07cc~tplv-goo7wpa0wc-image.image) </span>

5. You can view several data entries and profiling results of the table and perform the following operations:

   * Data preview

      * Click **hide columns** to toggle the field list display. When a field is checked, it appears in the worksheet; when unchecked, it is hidden.

      * Click **search**, enter keywords in the search box that appears, and press Enter to search for matching information.

   * Dynamic Probe

      You can sample data, filter, group by, delete columns, sort columns, and more on the profiling results. See the [Dynamic Probe](https://docs.byteplus.com/docs/dataleap/Dynamic_Probe) for detailed instructions.

   * Full exploration

      Click the probe button on the full exploration page to directly jump to the **create probe** page for this table, create a probe, and generate a probe report. For detailed instructions, see [Full Probe](https://docs.byteplus.com/docs/dataleap/Full_probe).

      * If data has not been probed, the probe report cannot be viewed here. Click the **go to explore** button to create a probe.

      * If data has been probed, you can view the probe report and click the **i want to probe** button to create a new probe.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">If you do not have read permission for a data table, opening its <strong>profiling</strong> page will prompt a no\-permission message; you must apply for access to view it.</div>


<span id="8f0bbae3"></span>
### Usage Instructions

This feature is used to write documentation for data table usage, generally prepared by the table owner. The related operation steps are as follows:


1. Log in to the DataLeap console.

2. Select **overview \> Catalog \> search** to enter the **search** page.

3. After searching for a data table, enter the data table details page.

4. Click the **Introduction** tab to enter the add instructions page.

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


<span id="28cc45a6"></span>
### Production Information


1. Log in to the DataLeap console.

2. Select **Overview \> Catalog \> Search** to enter the **Search** page.

3. After searching for a table, enter the table details page.

4. Click the **Production information** tab to access the production information page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8524ae7be0eb45d6bfcd6103cca7f693~tplv-goo7wpa0wc-image.image) </span>

5. You can view the table's operation and script information and perform the following actions:

   * Operation information

      * Select a task from the dropdown and set the run time period to view the task's operation status during that period.

      * Click the task name in the operation list or the **Action** column's **Task** button to jump to the Data Development task configuration page.

      * Click the **log** button in the **Action** column of an item in the run list to jump to the instance log page and view instance information.

   * Script information

      * Click the **view task details** icon after a task to jump to the task configuration page in Data Development.

      * Click to expand the task to view the script information of the task.


<span id="_4-5-血缘关系"></span>
### Lineage

Used to view which tables the data in this table is calculated from, that is, the upstream lineage of this table, and which tables this table’s data is used to calculate, that is, the downstream lineage of this table, and to manage them accordingly. Lineage can be displayed in either table view or visual chart.

<span id="_4-5-1-表格视图"></span>
#### Table View


1. Log in to the DataLeap console.

2. Select **Overview \> Catalog \> Search** to enter the **Search** page.

3. After searching the data table, enter the data table details page.

4. Select the **Lineage \> Table view** tab to enter the table view page of the lineage.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/12ee629082e14fea8c15a04bee0698fc~tplv-goo7wpa0wc-image.image) </span>

5. The following operations are available:

   * Set viewing conditions to see data that meets the criteria, including data asset nodes, fields, lineage levels, node owners, task names, and task owners.

      * Filter granularity: includes tables, fields, and partitions.

      * View range: includes view all, upstream only, downstream only.

      * Levels: 1 to 5 levels.

      * Search: enter table name, task name, etc., to find specific objects.

      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div>
      

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">The lineage updates in real time, meaning new dependencies are immediately reflected in the lineage.      </div>
      

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">If lineage cannot be automatically parsed or is inaccurate, supplement it by manually registering on the <strong>Data Development \> Task Development \> Schedule Settings</strong> page.      </div>
      

   * Click the **Download Info** button on the right to save the node data in the list as a CSV file for local viewing.

   * Set Quick notification

      1. Select one or more nodes from the list, click the **Quick notification** button on the right, and the **Quick notification** window will appear.

      2. Configure the notification message, then click the **Notify** button to open the notification confirmation dialog.

      3. Click the **Confirm** button to complete the setup. When upstream or downstream node table information changes, the system sends a notification to the target user's registered email.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Only the table owner can set quick notifications, currently supporting only "Email" notifications.      </div>
      

<span id="_4-5-2-可视化图表"></span>
#### Visual Chart

The visual chart offers three display modes: table view, column view, and Partition view.


1. Log in to the DataLeap console.

2. Select **Overview \> Catalog \> Search** to enter the **Search** page.

3. After searching for a data table, enter the data table details page.

4. Select the **Lineage \> Visual chart** tab to access the visual chart page for lineage.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/23af36351dc944d389b52f80e4f082f2~tplv-goo7wpa0wc-image.image) </span>

5. Supports the following query operations:

   * **Table view**

      * Range x levels: Select the node range, including hierarchy (1 to 5 levels) and upstream and downstream node information, to display all selected levels' upstream and downstream in the graph.

      * Group: Display node information by group, with grouping results shown in the graph.

      * Filtering: Filter one or more data types to show corresponding node information, narrowing the search range.

      * Property display: Select one or more attributes to show in the list. Up to 3 attributes can be displayed simultaneously.

      * The three icon buttons at the top right are full screen, reset, and download CSV.

      * Clicking a node highlights the path from that node to the primary node, graying out others; clicking empty space in the graph clears the highlight.

      * Click the table name to view node and task information in the right info panel. In the node information panel, you can also perform the following operations:

         * Click the **View table details** button to go to the Search page and view the detailed information of the table.

         * Click the **Switch to primary node** button to change a non\-primary table node to a primary node for display.

   * **Column view**

      * Primary node field: displays the lineage of one or more primary node fields. You can display up to 5 simultaneously.

      * Range x levels: select the node range, including levels (1 level to 5 levels) and upstream/downstream nodes, to display all selected levels of upstream and downstream in the graph.

      * The three icon buttons in the upper right corner are Full Screen, Reset, and Download CSV.

      * Click a field node to highlight the path from that node to the primary node, while other nodes will fade; click the blank area in the graph interaction zone again to remove the highlight from that node.

      * You can click the table name to view the node information and task information of the table in the right information panel. In the node information panel, you can also perform the following operations:

         * Click the **View table details** button to go to the data search page and see detailed information about the table.

         * Click the **Switch to primary node** button to display the table as the primary node instead of a non\-primary node.

   * **Partition view**

      * You can select the range (show all, just upstream, or just downstream) and levels (1 to 5 levels) to display all upstream and downstream nodes within the selected levels in the graph. The four buttons below the level range are centered display, zoom in, zoom out, and full screen/exit full screen.

      * You can enter keyword tags to search for and locate key information.

      * Classification aggregation: filter by classification criteria to display the same type of information in the corresponding tag’s tooltip.

      * Click a node to highlight it and its upstream and downstream nodes; other nodes will be dimmed. Clicking the node again cancels the highlight. You can also click and hold on a blank area in the interaction graph and move the mouse to pan the graph along with the cursor.

      * Click the table name to view the node information and task info for that table in the information panel on the right.


<span id="_4-6-质量信息"></span>
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

3. After searching for a table, enter the table detail page.

4. You can view the table’s basic info, business info, and perform the following management operations:

   * Hover over a parameter, click the displayed edit icon, modify the parameter info, then click the confirm icon to save changes.

   * Click the on/off icon button for **Is Hidden** to decide whether to hide the table’s security information.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Only parameters that show an edit icon when hovered over are editable.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Only accounts with read and write permissions on a ByteHouse CE table can edit its information. Accounts without permission can request access via the <strong>Permission Application</strong> button displayed at the top right of the page. For related operations, see <a href="https://docs.byteplus.com/docs/dataleap/Apply_Permission">Apply Permission</a>.   </div>
   

   Parameter descriptions for data table information are shown in the table below.

   
   |Parameters |Description |
   |---|---|
   |**Summary information at the top of the page** ||
   |Data type |Displays the type of this data. |
   |Data Classification |Show the business line classification to which this table belongs. In "Asset Catalog", specify the file directory name under the business line for asset portal construction. |
   |Business Line Tags |Show the business line tags of this table. |
   |**Basic Information** ||
   |Chinese name |The editable Chinese name of this metadata. |
   |Description |The editable description of the metadata. |
   |Owner |The owner of this metadata, displayed by default as the primary account and cannot be edited. |
   |Managing Business Line |The business line to which this metadata belongs. Editable with a dropdown to select from created business lines. |
   |Data Layer |The layer where the table is located. Editable, supports the following options with a dropdown selection. Supports keyword search by layer name for quick selection.<br><br><br>* Operational Data Store (ods)<br><br>* Data Integration Layer (dwi)<br><br>* Basic Dimensions Layer (dim)<br><br>* Detailed data layer (dwd)<br><br>* Intermediate data layer (dwm)<br><br>* Data warehouse service layer (dws)<br><br>* Data warehouse application layer (dwa)<br><br>* Data market layer (dm)<br><br>* Application service layer (ads)<br><br>* Application layer (app) |
   |Modeling specification categories |Display the modeling specification category used by this metadata; editable and selectable from model specification category types created under the business line in the dropdown. |
   |Project |The project the data table belongs to, editable, with a dropdown of created projects. |
   |Is Core Asset |Show whether the table is core or not, editable. |
   |**Business Information** ||
   |Business Lines |The asset portal business line to which the table belongs. |
   |Business domain |Metadata’s business domain, editable. Select from created business domains via dropdown.<br><br>Supports quick selection by searching business domain name keywords. |
   |Product line |Metadata’s product line, editable. Select from created product lines via dropdown.<br><br>Supports quick selection by searching product line name keywords. |
   |Theme |The theme to which the metadata belongs. Editable, selectable from existing themes in the dropdown.<br><br>Supports quick selection by searching theme name keywords. |
   |Custom Label |Labels set for the metadata. Editable, supports the following two methods:<br><br><br>* Select from existing labels in the dropdown. Supports quick selection by searching label keywords.<br><br>* Set labels manually: enter the label manually, then select it from the dropdown list. |
   |Business glossary |The business glossary associated with the metadata. Editable, selectable from existing business glossaries in the dropdown.<br><br>Supports quick selection by searching business glossary name keywords. |
   |**Security Information** ||
   |Confidentiality Level |The table's confidentiality level is editable, with four options: L1, L2, L3, and L4. Different confidentiality levels correspond to different approval processes.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The table's classification cannot exceed that of the database.</div><br> |
   |Authority Owner |The table's data security authority owner is editable and supports multiple settings.<br><br>This authority owner only shows the table authority owner. Row/column authority owners can be viewed and changed in **Security \> Authorization Management \> Authority Settings**. |
   |Database authority owner |The database authority owner for the database to which this table belongs; not editable. |
   |My Permissions |The current login account's permissions for this table are not editable.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Only accounts with read\-write permissions can edit metadata; the main account has Default access rights to all data.</div><br> |
   |Is Hidden |Indicates whether the table is hidden and can be edited.<br><br>After the table is hidden, if you are not the database authority owner or table owner and do not have read and write permissions for the table, you cannot view its detailed information on the **Search** page. |
   |**Technical Information** (view only) ||
   |Cluster ID |Displays the ID of the cluster this table belongs to. |
   |Database name |Display the name of the database to which the table belongs. |
   |Primary Key |The primary key is one or more fields in the table whose values uniquely identify a record in the table. This field is configured when the table is created and cannot be edited here. |
   |Is Partitioned |Indicates whether the data table is partitioned. |
   |Partition key |Displays the partition key of the data table. |
   |TTL (Time to Live) |The lifecycle of the metadata. |
   |Order By key |Show the table's order by key. Order by keys determine the physical storage order of data in the database. |
   |Shard Key |Show the shard key of the table. |
   |Sample field |Show the sampling key of the table. |
   |Unique key |Show the unique key of the data table. |
   |Logical table size |Show the size of the corresponding logical table. |
   |Engine |Show the table's Engine. |
   |Creation time |Show the creation time of the table. |
   |Update time |Show the latest update time of the table, automatically updated after editing other data source information. |
