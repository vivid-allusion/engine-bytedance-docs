---
title: "Why is the deadlock time and deadlock count collected on the Transactions and Locks page inconsistent with the performance monitoring collection?"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/can-i-export-execution-results-and-execution-records-after-executing-sql-statements"
---

Due to the following differences between InnoDB table current waiting for Row Locks, transaction holding locks, and deadlocks:


* **InnoDB table current waiting** **Row** **Locks (Row Locks Waiting)** : When a transaction attempts to acquire a lock on a row of data that has already been locked by another transaction, it will enter a waiting state before obtaining the lock. This type of lock is referred to as a waiting row lock. This is a concurrency control mechanism implemented by the database to ensure data consistency.

* **Holding Locks:**  After a transaction starts executing, it will lock the data it needs to access, thereby protecting this data from being modified by other transactions during its execution. This type of lock is referred to as a holding lock. A transaction can hold multiple locks, which can be row locks (locking a single record) or table locks (locking the entire table).

* **Deadlocks:**  A deadlock occurs when two or more transactions block each other during execution because they hold resources that the other transactions need. For example, Transaction A holds Resource 1 and waits to acquire Resource 2, while Transaction B holds Resource 2 and waits to acquire Resource 1, forming a deadlock. When a deadlock occurs, the database system typically resolves it by terminating and rolling back one of the transactions using mechanisms such as deadlock detection and timeout.
