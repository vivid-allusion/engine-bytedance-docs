---
title: "Querrying error logs"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/query-error-log"
---

Document Database for MongoDB supports logs management, allowing you to view and export error log details for different nodes under different components via the console, which helps quickly identify problems.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [MongoDB console](https://console.byteplus.com/db/mongodb).

2. In the upper\-left corner of the top menu bar, select the project and region for instance.

3. Select either **Replica set instances** or **Sharding instances** in the left navigation bar depending on the instance type.

4. On the target instance type list page, click the target instance name.

5. On the instance details page, click the **Logs** tab.

6. Click **Error log** sub\-tab, and you can quickly filter error logs that meet the criteria based on business needs through keywords, components, and query time.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">MongoDB does not support using reserved keywords in log retrieval. For more details about reserved keywords, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/log-overview#%E6%97%A5%E5%BF%97%E6%A3%80%E7%B4%A2%E9%A2%84%E7%95%99%E5%85%B3%E9%94%AE%E8%AF%8D">Reserved keywords for log search</a>.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can view the details of error logs within the last 7 days. By default, details of error logs within the last 1 day are displayed.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can export the error log query results that meet the filtering criteria to a local device for management. For specific procedures, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/export-log">Exporting logs</a>.   </div>
   


<span id=".55u45YWzLWFwaQ=="></span>
## Relevant APIs


|API |Description |
|---|---|
|[DescribeNormalLogs](https://docs.byteplus.com/en/docs/mongodb/describenormallogs) |Call the DescribeNormalLogs API to query the running log or error log information of the target MongoDB instance within the specified time period. |
