---
title: "Modifiable parameters list (PostgreSQL engine)"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/Modifiable_parameters_list"
---

AI Native BaaS for Supabase provides the following modifiable parameters in workspaces using the PostgreSQL engine. Modifying these parameters allows you to adjust and configure the workspace's running status.

&nbsp;


|Parameter name |Default value |Need restart? |Value range |Description |
|---|---|---|---|---|
|max_connections |Null |Yes |[20\-4000] |Determines the maximum concurrent connects allowed by the database server This parameter can only be configured during server startup Dynamically adjusted according to the compute specifications, limited to the range 20~4000 For details, refer to [Modifying the maximum number of connections](https://docs.byteplus.com/en/docs/aidap/Modifying_maximum_connections). |
|pg_partman_bgw.dbname |Null |No |The database must exist in the workspace. |Specify which databases need to be run automatically by the background process `run_maintenance()`, supporting multiple databases separated by commas. |
|pg_partman_bgw.role |Null |No |The account must exist in the workspace. |The backend process executes `run_maintenance()` under which role (user) identity. It must be a single role, used for all target databases. Therefore, it must exist and have sufficient privileges in every database:<br><br><br>* `partman.run_maintenance()` `EXECUTE` privilege;<br><br>* Read and write access to metadata tables part_config and part_config_sub;<br><br>* `SELECT` and DDL (`CREATE`/`ALTER`/`DROP` child tables) privileges on managed partition tables. |
|pg_partman_bgw.interval |3600 |No |[1\-2147483647] |Execution interval of background processes: how often the main loop wakes up To execute `run_maintenance()` Unit is second. |


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">You can call the <a href="https://docs.byteplus.com/en/docs/aidap/ModifyComputeParameters">ModifyComputeParameters</a> API to modify the above parameters.</div>
