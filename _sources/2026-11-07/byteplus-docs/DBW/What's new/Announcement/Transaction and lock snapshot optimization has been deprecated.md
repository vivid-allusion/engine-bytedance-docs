---
title: "Transaction and lock snapshot optimization has been deprecated"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/transaction-and-lock-feature-have-been-deprecated"
---

To ensure secure and compliant use of Database Workshop (DBW) and to enhance feature stability and data security, DBW will remove the Transaction and Lock Snapshot entry point and simultaneously upgrade the Transaction and Lock Diagnostics functionality.

<span id="X9TfgoQx"></span>
## Discontinuation Time

This feature will be gradually phased out by region starting from March 16, 2026. Please refer to the actual console page for specific details.

<span id="6ddOi49V"></span>
## Feature optimization details

To continuously improve the operation experience, we have upgraded the transaction and lock diagnosis feature:


* **Mode adjustment**: The original active snapshot collection mode is adjusted to an on\-demand manual task\-based diagnosis (to avoid unnecessary data collection and improve resource efficiency).

* **Result retention**: Manually created analysis task results are retained for up to 30 days (from the task creation date) to facilitate review and collaborative analysis.


<span id="XDEP7RaY"></span>
## Discontinuation reason

The data collected by the transaction and lock snapshot feature comes from database kernel tables or views (such as `INNODB_TRX`, `pg_stat_activity`), including sensitive content like complete SQL statements and session information.

To comply with security requirements, reduce the risk of unintended information exposure, and ensure data privacy and operational security, we have decided to deactivate this entry.

<span id="w2hTGVvE"></span>
## Historical data processing

Historical snapshot data will be retained for 30 days (calculated from the deactivation date). To view historical snapshots, please [Submit ticket](https://console.byteplus.com/workorder/create/) to contact technical support within the retention period. After 30 days, historical data will be automatically cleared and no longer retained.

<span id="lLG6W2Xj"></span>
## Future support

This adjustment aims to provide you with a more secure, controllable, and reliable Database operation and maintenance service. For any questions, please consult via the DBW ticket system or official customer service channels.

Thank you for your understanding and support!
