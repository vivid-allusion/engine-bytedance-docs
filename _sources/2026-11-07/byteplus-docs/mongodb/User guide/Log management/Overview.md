---
title: "Overview"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/log-overview"
---

Document Database for MongoDB supports logs management, allowing you to view and export logs that match specified conditions via the console. This topic introduces the log categories that MongoDB supports for viewing and exporting.

<span id=".5pel5b-X57G75Yir"></span>
## Log category

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Slow logs, error logs, and running logs are exported in the same way. For specific procedures, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/export-log">Exporting logs</a>.</div>



|Log category |Description |
|---|---|
|Slow log |You can view and export slow logs within a specified time range via the console, and optimize the instance by analyzing these logs. For more details, refer to [Querying slow logs](https://docs.byteplus.com/en/docs/mongodb/query-slow-log). |
|Error log |You can view and export error log details for different nodes under different components via the console, which helps quickly identify problems. For more details, refer to [Querying error logs](https://docs.byteplus.com/en/docs/mongodb/query-error-log). |
|Running log |You can view and export instance running logs via the console to monitor instance's operational status. For more details, refer to [Querying running logs](https://docs.byteplus.com/en/docs/mongodb/query-running-log). |


<span id=".5pel5b-X5qOA57Si6aKE55WZ5YWz6ZSu6K-N"></span>
## Reserved keywords for log search

Document Database for MongoDB supports quick retrieval of log information that meets specified criteria by keyword, but the following reserved keywords cannot be used for retrieval:

`AND`, `OR`, `NOT`, `TO`, `"`, `:`, `*`, `?`, `(`, `)`, `>`, `<`, `=`, `[`, `]`, `{`, `}`, `\`.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The words in the reserved keywords mentioned above are case\-insensitive. For example, neither <code>AND</code> nor <code>and</code> is allowed.</div>
