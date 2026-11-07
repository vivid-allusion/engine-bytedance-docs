---
title: "API overview"
product: "Server Migration Center"
product_code: "smc"
source: "https://docs.byteplus.com/en/docs/smc/smc_api_overview"
---

This topic provides an overview of all SMC APIs.​

<span id=".6L-B56e75rqQ"></span>
## Migration source


|API |Description |
|---|---|
|[DescribeMigrationSources](https://docs.byteplus.com/en/docs/smc/DescribeMigrationSources) |Query migration source information |
|[DeleteMigrationSource](https://docs.byteplus.com/en/docs/smc/DeleteMigrationSource) |Delete a migration source |
|[ModifyMigrationSourceAttribute](https://docs.byteplus.com/en/docs/smc/ModifyMigrationSourceAttribute) |Modify basic information of the migration source |


<span id=".6L-B56e75Lu75Yqh"></span>
## Migration task


|API |Description |
|---|---|
|[CreateMigrationJob](https://docs.byteplus.com/en/docs/smc/CreateMigrationJob) |Create a migration task |
|[ChangeMigrationJobAttribute](https://docs.byteplus.com/en/docs/smc/ModifyMigrationJobAttribute) |Modify the basic information of a migration task |
|[DeleteMigrationJob](https://docs.byteplus.com/en/docs/smc/DeleteMigrationJob) |Delete a migration task |
|[DescribeMigrationJobs](https://docs.byteplus.com/en/docs/smc/DescribeMigrationJobs) |Query migration task information |
|[DescribeMigrationLogs](https://docs.byteplus.com/en/docs/smc/DescribeMigrationLogs) |Query migration logs |
|[SetIncrementalSyncInterval](https://docs.byteplus.com/en/docs/smc/SetIncrementalSyncInterval) |Set automatic incremental synchronization |
|[TriggerLastIncrementalSync](https://docs.byteplus.com/en/docs/smc/TriggerLastIncrementalSync) |Perform the last automatic incremental synchronization |
|[DescribeMigrationSystemSupportTypes](https://docs.byteplus.com/en/docs/smc/DescribeMigrationSystemSupportTypes) |Query the target operating systems that the operating system of the source server supports for migration |


<span id=".5qCH562-"></span>
## Tag


|API |Description |
|---|---|
|[TagResources](https://docs.byteplus.com/en/docs/smc/TagResources) |Create and associate tags for the specified SMC migration source and migration task |
|[UnTagResources](https://docs.byteplus.com/en/docs/smc/UnTagResources) |Disassociate and delete tags for the specified SMC migration source and migration task |
