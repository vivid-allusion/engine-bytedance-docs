---
title: "Querying slow logs"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/query-slow-log"
---

Document Database for MongoDB supports logs management, allowing you to view and export slow logs within a specified time range via MongoDB or DBW console, and optimize the database by analyzing these logs.

<span id=".5pON5L2c5q2l6aqk"></span>
## **Querying slow logs on MongoDB console**


1. Log in to the [MongoDB console](https://console.byteplus.com/db/mongodb).

2. In the upper\-left corner of the top menu bar, select the project and region for instance.

3. Select either **Replica set instances** or **Sharding instances** in the left navigation bar depending on the instance type.

4. On the target instance type list page, click the target instance name.

5. On the instance details page, click the **Logs** tab.

6. Under the **Slow log** sub\-tab, you can quickly filter slow logs that meet the criteria based on business needs through keywords, database names, components, and query time.

   You can view the specific log details of the target query request in the **Query statement** column of slow log list.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">MongoDB does not support using reserved keywords in log retrieval. For more details about reserved keywords, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/log-overview#.5pel5b-X5qOA57Si6aKE55WZ5YWz6ZSu6K-N">Reserved keywords for log search</a>.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can view the details of slow logs within the last 7 days. By default, details of slow logs within the last 1 day are displayed.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Requests with an execution duration exceeding the <code>operationProfiling.slowOpThresholdMs</code> parameter value (default value is 100 milliseconds) will be recorded in slow logs.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can export the slow log query results that meet the filtering criteria to a local device for management. For specific procedures, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/export-log">Exporting logs</a>.   </div>
   


<span id=".55u45YWz5paH5qGj"></span>
## **Querying slow logs on DBW console**

The slow log feature for Document Database for MongoDB is available on DBW with enhanced features. For specific usage, refer to [Slow log management](https://docs.byteplus.com/en/docs/DBW/slow-query-log-management).

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Database Workshop (DBW) is a unified cloud management platform for managing the lifecycle of multiple types of databases. DBW is a database SaaS product that integrates a graphical user interface (GUI), troubleshooting, and auditing. It provides web endpoint management capabilities such as comprehensive observation and analysis, intelligent risk checks, and autonomous operations. For more details, refer to <a href="https://docs.byteplus.com/en/docs/DBW/what-is-database-workbench">What is Database Workshop</a>.</div>


<span id="hKcVvfAO"></span>
## Relevant documents

[Troubleshooting manual for MongoDB high CPU utilization](https://docs.byteplus.com/en/docs/mongodb/troubleshooting-for-high-cpu-utilization)

<span id=".55u45YWzLWFwaQ=="></span>
## Relevant APIs


|API |Description |
|---|---|
|[DescribeSlowLogs](https://docs.byteplus.com/en/docs/mongodb/describeslowlogs) |Call the DescribeSlowLogs API to query the slow log information of the target MongoDB instance within the specified time. |
