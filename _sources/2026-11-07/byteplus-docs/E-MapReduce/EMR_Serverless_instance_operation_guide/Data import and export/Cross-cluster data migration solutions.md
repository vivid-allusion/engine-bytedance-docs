---
title: "Cross-cluster data migration solutions"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Cross-cluster_data_migration_solutions"
---

This article introduces recommended data migration solutions for cross\-cluster migration in different scenarios.


|Specific scenarios |Recommended solutions |Reference documentation |
|---|---|---|
|Data migration between clusters of the same major version<br><br>(for example, migration from 3.3 to 3.3) |It is recommended to use the backup and restore capabilities of EMR Serverless instances (OLAP) to perform data migration between clusters of the same version. |* [StarRocks实例备份与恢复最佳实践](https://docs.byteplus.com/docs/undefined/68da347342e561058e056ca4)<br><br>* [Doris is the backup and restore reference documentation.](https://doris.apache.org/zh-CN/docs/3.x/admin-manual/data-admin/backup-restore/overview) |
|Data migration between clusters of different versions<br><br>(for example, migration from 3.2 to 3.3) |It is recommended to use the data import and export capabilities provided by EMR Serverless instances (OLAP) to export cluster data from the source cluster and then import it into the template cluster. Details:<br><br><br>* For export: it is recommended to use the Export method<br><br>* For import: it is recommended to use the BrokerLoad + TOS method |* Export: [Data export](https://docs.byteplus.com/docs/E-MapReduce/109119)<br><br>* Import: [Broker Load](https://docs.byteplus.com/docs/E-MapReduce/109121) |
