---
title: "Storage type introduction"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/storage-type-introduction"
---

RDS for SQL Server offers two storage types: Extremely Fast SSD PL1 Cloud Drive and Extremely Fast SSD PL2 Cloud Drive. This article introduces the relevant information of the extremely fast SSD PL1 cloud disk and the extremely fast SSD PL2 cloud disk for your reference.

<span id="storage-type-introduction"></span>
## Storage Type Introduction


|**storage type** |**Extremely fast SSD PL2 cloud disk** |**Extremely fast SSD PL1 cloud disk** |
|---|---|---|
|**performance description** |The cloud disk has high concurrency limit I/O and stable read and write latency. It provides excellent read and write performance, providing you with fast response times and shorter data read times.<br><br>Due to its high performance, the cloud disk is relatively expensive. |The concurrency limit I/O performance of the cloud disk is moderate, and the read and write latency is relatively stable. If your demand for read and write speed is not particularly high, you can choose the PL1 cloud disk.<br><br>The performance of the PL1 cloud disk is slightly lower than that of the PL2 cloud disk, but the price is lower. |
|**Maximum I/O performance per disk** |100000 |50000 |
|**Single disk I/O performance calculation formula** |Min |Min |
|**Maximum throughput per disk ( MB/s)**  |1000 |350 |
|**Single disk throughput performance calculation formula** |Min |Min |
|**Single random write average delay (Block Size = 4KB) (ms)**  |0.3~0.5 |0.3~0.5 |
|**Single disk maximum capacity (GiB)**  |500~4000 |20~4000 |
|**Promise data reliability** |99.9999999% |99.9999999% |
|**applicable scenario** |Based on the high read and write performance of the cloud disk, the cloud disk is suitable for medium\-scale application scenarios that require high I/O or high throughput. For example:<br><br><br>* Database applications: Scenarios that require a large number of read and write operations.<br><br>* High\-performance computing: Scenarios that require high\-speed data reading and writing to ensure computational efficiency, such as in computationally intensive applications such as AI or big data analytics.<br><br>* Financial transactions: Scenarios that require quick responses to avoid trading mistakes, such as securities trading systems. |The cloud disk is suitable for application scenarios that do not require high\-throughput small and medium\-sized conventional services. For example:<br><br><br>* Web server: Scenarios that require higher stability rather than extremely high throughput performance, such as servers serving websites or web applications.<br><br>* Development and testing environment: Scenarios where reading and writing data is relatively low, such as for development testing of applications.<br><br>* Lightweight applications: Scenarios that require a stable storage environment and do not have high requirements for read and write operations. |
