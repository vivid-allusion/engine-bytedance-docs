---
title: "Managing an SQL review ticket"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/Manage_SQL_Review_Tickets"
---

This topic explains how to manage SQL review tickets on the DBW console.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

SQL review tickets have been created. For detailed steps, refer to [Creating an SQL review ticket](https://docs.byteplus.com/en/docs/DBW/Create_SQL_review_ticket).

<span id=".5p-l55yLLXNxbC3lrqHmoLjlt6XljZU="></span>
## View an SQL review ticket

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">DBW administrators can view all tickets, while DBW normal users can only view tickets they created or are assigned as approvers.</div>



1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the region.

3. On the left navigation bar, select **Data management** \> **Ticket list**.

4. On the **Ticket list** page, under the **All** tab, filter for the target ticket. The SQL audit information is detailed in the table below.

   * **Database Type** is **RDS for PostgreSQL**.

   * **Ticket type** is **SQL audit ticket**.

   
   |**information** |**Description** ||
   |---|---|---|
   |SQL review ticket list information |On the **Created by Me** and **All** sub\-tabs, you can view the **Ticket name**, **Ticket number**, **Ticket status**, **Database instance**, **Database type**, **Database name**, **Creator**, and **Creation time** of the ticket. ||
   |SQL review ticket details |Click the name of the target ticket to view ticket details, execute SQL statements, intelligent review results, operation logs, and manual review results on the **Ticket details** page. ||
   ||**Ticket details** |In the **Ticket information** area, you can view the ticket's **Creator**, **Remarks**, **Database type**, **Creation time**, **Instance ID**, **Last operation time**, **Database**, and other information. |
   ||**Execute SQL statement** |In the **Execute SQL statement** area, you can view SQL statements pending approval. |
   ||**Intelligent review results** |In the **Intelligent review** configuration wizard, you can view the following information.<br><br><br>* Specification review results: The specification review results include the number of red lines, warnings, and suggestions checked. You can click the count for any check level to view which security rules are triggered in the SQL statements.<br><br>* Index suggestions: Click the number after index recommendations to view SQL optimization suggestions and SQL templates in the **Index recommendation results** dialog box.<br><br>* SQL statement review results: View review details of SQL statements.<br><br>   * On the SQL statement list pane, click **Details** in the **Actions** column of the SQL statement. You can also query non\-standard SQL statements based on security rules. For more information on security rules, refer to [Security rule information](https://docs.byteplus.com/en/docs/DBW/security-rule-management_#.5Y-C6ICD5paH5qGj).<br><br>   * In the **Result details** control panel, view the **specification review**, **index suggestions**, and **SQL statements** of the SQL statement. |
   ||**Manual review results** |Since only approval\-free submission is currently supported, no approval workflow is set up in the **Manual approval** configuration wizard. |
