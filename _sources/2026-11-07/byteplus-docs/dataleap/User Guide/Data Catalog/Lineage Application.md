---
title: "Lineage Application"
product: "DataLeap"
product_code: "dataleap"
source: "https://docs.byteplus.com/en/docs/dataleap/Lineage_Application"
---

The Lineage Application helps you analyze upstream and downstream relationships of data objects, identify impact levels and task dependency scheduling, and quickly trace and understand the effects of changes on other objects.

This feature supports viewing the data lineage graph in real time through visual charts. You can switch between Table view, Column view, and Partition view. The Table view shows the upstream and downstream lineage of tables. The Column view shows the upstream and downstream of fields within a table. The Partition view shows the upstream and downstream lineage of tables over time periods.

<span id="081dec85"></span>
## Prerequisites

Corresponding metadata types have been collected. For related operation instructions, see [Metadata Ingestion](https://docs.byteplus.com/docs/dataleap/Metadata_Ingestion).

<span id="_2-操作步骤"></span>
## **Operation Steps**


1. log in to the DataLeap console.

2. Select **Overview \> Catalog \> Lineage Application** to enter the **Lineage Application** page.

3. Enter the table name keyword in the data type search box, then select the desired table from the dropdown list to display the lineage graph for that table.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Currently supports lineage queries for multiple data types including BMQ Topic, RocketMQ, LAS table, EMR Hive table, ByteHouse CDW table, EMR StarRocks table, EMR Doris table, EMR Serverless StarRocks table, and LAS Catalog table. You can also quickly find types by selecting from the <strong>All types</strong> dropdown.   </div>
   

4. You can perform the following actions:

   * Click the **table view** button to view the table data lineage.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/58ae6997bc6541c7bc7f3f9e8f18b11a~tplv-goo7wpa0wc-image.image) </span>

      * Range x levels: choose the node range, including hierarchy (1 to 5 levels) and upstream/downstream node information, to display all upstream and downstream nodes within the selected levels in the graph.

      * Group: display node information in groups; nodes will be further classified into combination label tooltips based on the selected criteria.

      * Filter: filter one or more data types to show corresponding node information and narrow the node search scope.

      * Property display: select one or more properties to show in the list. Up to 3 properties can be displayed simultaneously.

      * The three icon buttons at the top right are Full Screen, Reset, and Download CSV.

      * Click a node to highlight the path from that node to the primary node; other nodes will be dimmed. Click the blank area in the graph interaction zone again to remove the highlight.

      * Click a node to view its node information and task info in the information panel on the right. The node information page also allows the following actions:

         * Click the **View table details** button to go to the Search page and view detailed information for that table.

         * Click the **Switch to primary node** button to change a non\-primary node table to a primary node for display.

   * Click the **Column view** button to see the column data lineage.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f0e8f6106d5c4d69a1d6d2e5743b69a2~tplv-goo7wpa0wc-image.image) </span>

      * Primary node field: Allows displaying the lineage of one or multiple primary node fields. Up to 5 can be displayed simultaneously.

      * range x hierarchy: You can select the node range, including hierarchy levels (1 to 5) and upstream/downstream node information, to display all selected levels' upstream and downstream in the graph.

         <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="3">tip         </div>
         

         <div data-tips="true" data-tips-type="tip" data-wrapper-indent="3">Each node displays up to 20 direct upstream and downstream nodes.         </div>
         

      * The three icon buttons at the top right are full screen, reset, and download CSV.

      * Click a field node to highlight the link from that node to the primary node while dimming others; click the blank area in the graph interaction area again to cancel the highlight of that node.

      * Click a node to view its node information and task info in the right information panel.

   * Click the **Partition view** button to see the lineage relationship of partition data.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1913fdac2917426d83de4699dc69851e~tplv-goo7wpa0wc-image.image) </span>

      * Partition filter: Filter based on partition conditions to display corresponding information.

      * You can view the range (show all, just look upstream, or just look downstream) and hierarchy levels (1 to 5) to display all the upstream and downstream nodes of the selected levels in the graph. The four buttons below the hierarchy range are center display, zoom in, zoom out, and full screen/exit full screen.

      * You can enter keyword tags to search for key information.

      * Classification aggregation: Filter by classification conditions to display the same type of information in the corresponding tag tooltip.

      * Click a node to highlight it along with its upstream and downstream nodes; other nodes will be dimmed. Click the same node again to cancel the highlight. You can also click and hold on an empty area in the interaction zone, then move the mouse to pan the interaction graph.

      * Click a node to view the node information and task info of that table in the right information panel.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The lineage updates in real time, meaning new dependencies are immediately reflected in the lineage application.</div>


* <div data-tips="true" data-tips-type="tip">Regarding the lineage parsing of EMR StarRocks type data, note the following two points:</div>


   * <div data-tips="true" data-tips-type="tip">Table lineage does not always include field lineage because table lineage can be parsed through task upstream and downstream dependencies; field lineage relies on user\-written SQL parsing, so if the SQL parsing fails, field lineage information will not appear.</div>


   * <div data-tips="true" data-tips-type="tip">Currently, only ordinary SQL statements support field lineage parsing; SQL involving external catalogs is not supported yet.</div>
