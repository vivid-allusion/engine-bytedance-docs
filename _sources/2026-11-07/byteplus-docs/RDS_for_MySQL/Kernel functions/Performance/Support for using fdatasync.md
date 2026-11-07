---
title: "Support for using fdatasync"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/Support_for_fdatasync"
---

This topic provides information about the fdatasync call for MySQL 5.7 instances in RDS for MySQL.

<span id="alPeO3yu"></span>
## Background

InnoDB's redo log/doublewrite buffer currently uses the fsync system call to flush data to disk, an operation that includes flushing both file metadata and file data. In write scenarios with fixed\-size files, such as the redo log/doublewrite buffer, refreshing file metadata like the last modification time is unnecessary. The fdatasync system call can avoid constantly flushing file metadata to the storage device, thereby reducing write overhead.

MySQL 8.0 introduced support for using the fdatasync system call instead of fsync for flushing data to disk, and this optimization is enabled by default in version 8.4 and later. RDS for MySQL has backported this optimization from MySQL 8.0 to MySQL 5.7.

<span id="Fpmt2sLa"></span>
## Supported version

MySQL 5.7, kernel version MySQL 5.7 20250615 or later.

<span id="USILPfCh"></span>
## Use cases

Suitable for scenarios with high write pressure that require frequent synchronous flushing of redo logs and the doublewrite buffer.

<span id="RXKksL2C"></span>
## Performance data

In sysbench\-write\-only high\-concurrency continuous write scenarios, QPS performance can be improved by about 5%.

<span id="xqqkGSFa"></span>
## Instructions

In the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql), set the loose_innodb_use_fdatasync parameter to `on` to enable the fdatasync disk flushing optimization for the instance. For more information about modifying parameters, see [Modifying parameters](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifying_parameters).


|Parameter name |Default value |Does it need instance restart to take effect? |Value range |Scope |Parameter description |
|---|---|---|---|---|---|
|loose_innodb_use_fdatasync |OFF |No |[ON\|OFF] |Global |Specifies whether to use the fdatasync system call to flush data to disk. |
