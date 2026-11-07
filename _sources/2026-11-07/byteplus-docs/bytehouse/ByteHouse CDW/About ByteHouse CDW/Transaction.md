---
title: "Transaction"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/docs-transaction"
---

In ByteHouse, every SQL statement is implicitly converted into a transaction and executed, providing Atomicity, Consistency, Isolation, and Durability (ACID) properties, aimed at ensuring data validity in case of errors, network failures, machine failures, and other accidents. All data written in a statement is atomic; no other statements will see partial data. For a write action, all data will be visible simultaneously and will be persisted after the successful write operation. Before this, any data written is invisible to other statements. If the write operation fails, ByteHouse will rollback the current transaction and automatically clean up the intermediate data written by the statement.

Currently, launching transactions by executing the BEGIN statement is not supported.

<span id="715c2171"></span>
## Isolation levels

Among the four isolation levels, ByteHouse currently only supports transactions at the READ COMMITTED level.


* Uncommitted Reads

* Read Committed

* Repeatable Read

* Serializable.



|Isolation Level |Dirty Write |Dirty Read |Fuzzy Read |Phantom |
|---|---|---|---|---|
|READ UNCOMMITTED |Not Possible |Possible |Possible |Possible |
|READ COMMITTED |Not Possible |Not possible |Possible |Possible |
|REPEATABLE READ |Not Possible |Not possible |Not possible |Possible |
|SERIALIZABLE |Not Possible |Not possible |Not possible |Not possible |


At the READ COMMITTED isolation level, a transaction must wait for another transaction to commit before it can read the data.

<span id="371eaf22"></span>
## Concurrency control

Concurrency control is used to ensure data correctness during concurrent updates. ByteHouse uses resource locks for concurrency control, which can be added to different resources such as databases, tables, and partitions. Locks prevent other transactions from modifying the same resources until the lock is released. If a transaction is blocked, the user running the transaction will receive a message displaying information about other transactions currently blocking it. The message will be displayed as "Current transaction conflicts with other txn (txn_id: xxx)." If you receive this message, it is advisable to wait for the transaction to release the lock before proceeding

ByteHouse utilizes MVCC (multi\-version concurrency control) to enhance performance in concurrent read and write operations, ensuring reads are not affected or blocked by other write operations on the same resource
