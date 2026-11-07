---
title: "Product specifications"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/product_specifications"
---

This topic presents the instance specifications of RDS for PostgreSQL, helping you understand the specifications of the RDS for PostgreSQL instance. You can refer to this topic to learn about the specific configurations of each specification.

PostgreSQL instances support a high\-availability architecture (one primary and one secondary node) and read\-only nodes. The supported node specifications are shown in the following table:


|Node specification |Cores |Memory size |Max connections |Storage space |
|---|---|---|---|---|
|rds.postgres.1c2g |1 core |2 GB |200 |20 GB\-3,000 GB |
|rds.postgres.2c4g |2 cores |4 GB |400 |20 GB\-3,000 GB |
|rds.postgres.2c8g |2 cores |8 GB |600 |20 GB\-3,000 GB |
|rds.postgres.2c16g |2 cores |16 GB |1600 |20 GB\-3,000 GB |
|rds.postgres.4c8g |4 cores |8 GB |800 |20 GB\-3,000 GB |
|rds.postgres.4c16g |4 cores |16 GB |1600 |20 GB\-3,000 GB |
|rds.postgres.4c32g |4 cores |32 GB |3200 |20 GB\-3,000 GB |
|rds.postgres.8c16g |8 cores |16 GB |1600 |20 GB\-6,000 GB |
|rds.postgres.8c32g |8 cores |32 GB |3200 |20 GB\-6,000 GB |
|rds.postgres.8c64g |8 cores |64 GB |6400 |20 GB\-6,000 GB |
|rds.postgres.16c32g |16 cores |32 GB |3200 |20 GB\-12,000 GB |
|rds.postgres.16c64g |16 cores |64 GB |6400 |20 GB\-12,000 GB |
|rds.postgres.16c128g |16 cores |128 GB |12800 |20 GB\-12,000 GB |
|rds.postgres.32c128g |32 cores |128 GB |12800 |20 GB\-12,000 GB |
|rds.postgres.32c256g |32 cores |256 GB |25600 |20 GB\-12,000 GB |


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">The maximum number of connections in the table represents the actual available connections for users (the connection capacity guaranteed for customers).</div>


* <div data-tips="true" data-tips-type="default">Since the backend management component reserves a portion of connections for O&M operations, the result returned by executing <code>show max_connections;</code> is slightly larger than the maximum number of connections shown in the table.</div>


* <div data-tips="true" data-tips-type="default">Storage space above 3000 GB is currently an allowlisted feature, available only in the China (Beijing), China (Shanghai), and China (Guangzhou) regions. If you need to use this feature, <a href="https://console.byteplus.com/workorder/create">submit a ticket</a> to contact us.</div>
