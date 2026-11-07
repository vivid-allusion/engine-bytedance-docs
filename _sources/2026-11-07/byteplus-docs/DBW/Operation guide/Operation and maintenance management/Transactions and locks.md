---
title: "Transactions and locks"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/transactions-and-locks"
---

Database Workshop DBW provides the Transactions and Locks feature, which captures and analyzes real\-time database lock scenarios such as hold locks, deadlocks, and lock waits. When lock\-wait issues occur in the database, you can use the Transactions and Locks analysis feature to intuitively examine and visualize relevant locking information such as blocked sessions, holding transactions, and wait chains enabling rapid identification and resolution of the root cause. This helps ensure stable database operation and significantly reduces troubleshooting time.

<span id="ByQmrRtC"></span>
## Core Features


* View active transactions in real time: Displays current transaction IDs, start times, Execute SQL, and states.

* Identify lock wait relationships: Shows which transactions are waiting for which locks (row locks, table locks) and the lock holders.

* Pinpoint blocking sources: Quickly identifies transactions causing others to block (e.g., unsubmitted long transactions).

* Assist deadlock analysis: Reconstructs transaction and lock dependency graphs during deadlocks using deadlock logs.


<span id="VtONrkjj"></span>
## Precautions

While using the transaction and lock feature, avoid modifying instance configurations, as this may prevent normal display of transactions and locks.

<span id="Z1VxR2Fl"></span>
## Advantages

Transaction and lock features transform hidden, hard\-to\-trace, and time\-consuming lock issues into visible, manageable, and actionable operational events, thereby:


* Reducing business downtime.

* Lowering troubleshooting costs for database administrators.

* Encouraging developers to write more robust transaction code.


<span id="XfdGhcxa"></span>
## Applicable scenarios


* Application suddenly slows down/times out: Check for a large number of LOCK WAIT transactions and identify blocking transactions.

* Deadlock errors occur: Analyze the locking sequence of two transactions using snapshots and deadlock logs to optimize code logic.

* Connection pool exhausted: Check for long\-running uncommitted transactions occupying connections.

* High primary\-replica replication delay: Investigate if there are large uncommitted transactions on the primary database.

* Database administrator routine inspection: Periodically check for long\-running transactions (\>5 minutes) or lock accumulation.

* Local development debugging: Reproduce the stuck issue in the test environment and verify if it's caused by uncommitted transactions through snapshots.


<span id="OF2UVBHA"></span>
## Supported database types


* RDS for MySQL

* NDB for MySQL

* RDS for PostgreSQL


<span id="CXRqs0h8"></span>
## Related operation document


|**Database type** |**Actions document** |
|---|---|
|RDS for MySQL |[Transaction and lock management](https://docs.byteplus.com/en/docs/DBW/lock-analysis-management-for-mysql?lang=zh) |
|NDB for MySQL |[Transaction and lock management](https://docs.byteplus.com/en/docs/DBW/Transaction_and_lock_management?lang=zh) |
|RDS for PostgreSQL |[Transaction and lock management](https://docs.byteplus.com/en/docs/DBW/transaction-and-lock-management?lang=zh) |
