---
title: "Migrating to Volcano Engine Supabase"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/migrating-to-supabase-connected-over-public-network"
---

This topic describes how to create a task for migrating Supabase connected over public network to BytePlus Supabase in the Database Transmission Service (DTS) console.

## Prerequisites

* If the source end are PostgreSQL databases on [Supabase.com](https://supabase.com/) and the instances connect via public network self\-hosting or private network, log in to the Supabase console, open the **Connect to your project** page in the target project, select the **Direct (Connection string)**  tab, and choose the connection method according to the network environment. Set **Type** to URI, then copy the PostgreSQL connection string generated on the page. When configuring source database information in the Database Transmission Service (DTS) later, refer to this connection string to fill in the address, port, database name, account number, and password.

* When the access method of the database instance is self\-managed over the Internet and access restrictions are enabled, add the DTS server IP addresses to the allowlist or security group of the database instance before creating the database transmission task. DTS server IP addresses vary by region, as detailed below:

   * DTS server IP addresses in China (Guangzhou), China (Shanghai), and China (Beijing) are `221.194.189.0/27,157.148.90.32/27,180.184.132.64/27,61.129.54.64/27,220.196.172.32/27,117.135.143.32/27,220.196.168.32/27,116.132.250.32/27,111.45.13.32/27,125.88.248.32/27,180.153.35.32/27,220.181.65.32/27,220.181.65.64/27`.

   * DTS server IP addresses in Asia Pacific (Johor) are `101.47.0.32/27,220.181.65.32/27,220.181.65.64/27,101.47.65.192/27,101.47.65.32/27`.

   * DTS server IP addresses in Asia Pacific (Jakarta) are `221.194.189.0/27,157.148.90.32/27`.

   * DTS server IP addresses in China (Hong Kong) are `101.47.0.32/27,220.181.65.32/27,220.181.65.64/27,101.47.65.192/27,101.47.65.32/27`.

      For more information on the CIDR block of DTS servers, refer to [Adding the CIDR block of the DTS server](https://docs.byteplus.com/en/docs/DTS/Adding_the_CIDR_block_of_the_DTS_server).

* AIDAP\-managed Supabase engine instance:

   * Create workspace. For detailed steps, refer to [Create workspace](https://docs.byteplus.com/en/docs/aidap/Supabase-Creating_a_workspace?lang=en).

   * Create database branch. For detailed steps, refer to [Creating branch](https://docs.byteplus.com/en/docs/aidap/Supabase-Creating_a_branch?lang=en).

   * Obtain the connection information required by DTS, such as host address, port, account number, and password. refer to [Obtaining the connection information of computing power](https://docs.byteplus.com/en/docs/aidap/Supabase-Getting_compute_connection_information?lang=en) for detailed steps.

* The network connectivity and service availability of the source and destination have been confirmed.

## Precautions

* Migration configuration and object selection

   * DDL operation restrictions: During the table structure migration and full migration stages, DDL operations that change the database or table structure are strictly prohibited; otherwise, the task will fail.

   * Pre\-check alarm: if the alarm is ignored during pre\-check and the task is started, it may cause data inconsistency and business risks.

   * Migration object restrictions: currently only your business tables are migrated, and Supabase's own system database tables are not migrated.

* Performance and resource impact

   * Storage space inflation: Full migration performs concurrent INSERT operations, resulting in fragmentation in the target database. The target database storage is usually larger than the source database after migration.

   * Load impact: Migration consumes certain read and write resources. It is recommended to perform it during off\-peak hours and assess the performance of the source and target databases in advance.

   * Network resources: When creating a dedicated network migration task, the system will by default create several network interfaces (named in the format `dts_shuttle_********`) within the virtual private cloud subnet you select.

* Operation stability and permissions

   * Special attention for self\-built PostgreSQL:

      * Primary switch: if the source end switches to the primary during migration, the migration task will fail.

      * Restart operation: restarting the source end will temporarily interrupt the task and automatically attempt to recover. if recovery takes long, [Submit tickets](https://console.byteplus.com/workorder/create).

   * Permission retention: during migration, do not modify the database account access permissions on created objects (such as triggers, functions, internal tables, etc.) in the source database.

   * Task independence: data migration and storage object migration are independent and do not affect each other.

## Limits

|**Type** |**Description** |
|---|---|
|Source database basic requirements<br><br> |* Version compatibility: it is recommended that the PostgreSQL versions of the source database and the target database remain consistent or migrate from a lower version to a higher version. Migrating from a higher version to a lower version may involve compatibility or data loss risks.<br><br>* Bandwidth requirements: the source end server must have sufficient outbound bandwidth; otherwise, the migration speed will be affected.<br><br>* Table structure and naming:<br><br>   * Tables to be migrated must have a primary key or a unique non\-null constraint, and their fields must be unique. Otherwise, data inconsistency may occur.<br><br>   * The database or table name of the object to be migrated can not contain question marks (?). Otherwise, the task will fail.<br><br>* Migration granularity and quantity:<br><br>   * A single migration task only supports migrating one database. To migrate multiple databases, configure multiple tasks.<br><br>   * Select the migration object granularity as database or table. If only tables are selected, views, triggers, functions, stored procedures, and other objects will not be migrated.<br><br>   * It is recommended that a single task does not exceed 20,000 tables or 50 databases. When migrating a large number of databases and tables, splitting tasks is recommended.<br><br>* Data scale: the current version is recommended for migrating storage objects with about 100,000 items. If the scale is exceeded, it is recommended to conduct a separate evaluation before execution.<br><br>* Change control: It is not recommended to make any Bucket or Object changes (including additions, updates, deletions, and renaming) on the source end during migration. Migration is recommended during off\-peak hours, with write operations to Buckets within the migration scope paused as much as possible. |
|Target database basic requirements |* Capacity and limits: Confirm that the destination Supabase Storage limits cover the source data:<br><br>   * The destination allows creating the corresponding bucket.<br><br>   * The destination's single file size limit must be greater than or equal to the source's maximum single file size.<br><br>   * The total capacity or project quota on the destination can accommodate this migration's data.<br><br>   * The destination supports resumable upload / TUS shard upload<br><br>   * The destination API rate limiting strategy withstands concurrency pressure during migration.<br><br>* Conflict resolution: Confirm the conflict resolution strategy in advance if the destination already contains a Bucket or Object with the same name. |
|Other limits |* Beta: This feature is currently in beta. You can [Submit tickets](https://console.byteplus.com/workorder/create) to contact technical support for data migration.<br><br>* Only primary database: Only data from the primary database supports migration. Data from the secondary database is not supported.<br><br>* Network connectivity: Confirm that the migration execution environment can access the Supabase Storage API addresses of the source end and destination, as well as the source end PostgreSQL database addresses. Check firewall, allowlist, security groups, proxy, and SSL connection policies. Open these in advance if requirements are not met.<br><br>* Migration object range:<br><br>   * The current web interface supports selecting all or specific buckets but does not support manual entry of wildcards, prefix\-based, or custom filter rules to migrate partial objects.<br><br>   * Current migration tasks use source end object snapshots as the baseline and do not support automatic inclusion of objects added after task initiation.<br><br>* WAL logs must be retained for at least 24 hours, and a retention period of more than seven days is recommended. otherwise, the dts task may fail because it can not obtain the logs, potentially leading to data loss. |

## Minimum database permission policy

|**Database** |**Permission description** |
|---|---|
|**Source** |Ensure that the provided source end credentials (it is recommended to use a `service role key` with full management capability instead of a restricted `anon key`) have the following permissions:<br><br><br>* Storage: can list Buckets, read Bucket configurations and Object metadata, and download Object content.<br><br>* PostgreSQL: Can connect to the source database, and read the `storage.buckets` and `storage.objects` tables.<br><br>* Metadata reading: Has permission to read index metadata related to `storage.objects` so the system can automatically check whether the required indexes for scanning (`bucket_id`, `name COLLATE "C"`) exist. |
|**Target** |Ensure the provided destination credentials (using `service role key` is recommended) have storage permissions to list and create buckets, read bucket configurations and object metadata, write objects, and support large file shard uploads. |

## Procedure

1. Log on to the [DTS console](https://console.byteplus.com/dts).

2. On the top menu bar, select the project and region.

3. In the left navigation bar, click **Data migration**.

4. On the **Migration task list** page, click **Create task**.

5. On the **Create migration task** page, locate the **Configure source and target database** wizard, and configure the following parameters.

|**Type** |**Name** |**Description** |
|---|---|---|
|**Basic information** |**Task name** |Optional. Customize the task name. The length must be within 256 characters.<br><br>> **tip**<br><br><br>> If not set, the system generates a task named with `dts-` by default.<br> |
||**Link specification** |Select the link specification for the migration task. **Compact**, **Medium** and **Standard** are supported.<br><br>> **tip**<br><br><br>> The link specification can not be modified after the task is successfully created. For details on the link specifications, refer to [Product specifications](https://docs.byteplus.com/en/docs/DTS/product_specifications?lang=en).<br> |
|**Source database configuration** |**Select an existing data source** |You can choose whether to use an existing instance as needed:<br><br><br>* Use existing instances: Click **Select an existing data source**, then in the **Select data source** control panel, choose the target region from the **Region** drop\-down list, and select the target data source. Supports selecting data sources by data source name and ID. For methods to create data sources, refer to Data source management.<br><br>* Do not use existing instances: If not using an existing instance, you need to configure the following database instance information. |
||**Instance type** |Select **Supabase**. |
||**Access method** |Select **public network self\-built Supabase**. |
||**region** |Select the region of the public network self\-built instance. |
||**API URL** |Enter the Supabase service external API entry. |
||**Service role key** |Enter the exclusive key in Supabase with the highest permissions and global instance administrator rights. |
||**Database URL** |enter the native direct connection address of the underlying Supabase PostgreSQL database (usually ending with 5432), not the Pooler address. It follows the standard PostgreSQL connection string format and is the credential for direct connection to the underlying database. |
||**Test connection** |Click **Test connection** to verify the connection to the instance. If the test connection fails, modify the configuration based on the failure prompt, and then click **Test connection** again to verify the connection. The details are as follows:<br><br><br>* **Connection authentication failed. Check the network**: When this error prompt appears, confirm network connectivity.<br><br>* **Connection authentication failed. Check the username and password**: When this error prompt appears, verify your username and password.<br><br>* **Invalid IP address**: When this error prompt appears, verify your IP address. |
|**Target database configuration** |**Select an existing data source** |You can choose whether to use an existing instance as needed:<br><br><br>* Use existing instances: Click **Select an existing data source**, then in the **Select data source** control panel, choose the target region from the **Region** drop\-down list, and select the target data source. Supports selecting data sources by data source name and ID. For methods to create data sources, refer to Data source management.<br><br>* Do not use existing instances: If not using an existing instance, you need to configure the following database instance information. |
||**Instance type** |Select **Supabase**. |
||**Access method** |Select **BytePlus Supabase**. |
||**region** |Select the region where the target instance is located. |
||**Workspace** |Enter the workspace ID information. |
||**Branch** |Enter the branch ID. |
||**Database name** |Enter the database name. |
||**Database account** |Enter the database account information. |
||**Database password** |Enter the database password corresponding to the database account. |
||**Test connection** |Click **Test connection** to verify the connection to the instance.<br><br>If the test connection fails, modify the configuration based on the failure prompt, and then click **Test connection** again to verify the connection. The specific prompts are as follows:<br><br><br>* **Connection authentication failed. Check if the username and password are correct**: When this error prompt appears, verify your username and password.<br><br>* **Connection authentication failed, unable to create connection normally, contact customer service**: When this error prompt appears, [submit a ticket](https://console.byteplus.com/workorder/create) for technical support. |
|**Project and billing**<br><br> |**Project** |Optional. Select the affiliated project for the task from the drop\-down list. By default, it is under **default (default project)** . You can also click **Create new project** to create a new project. For more information, refer to [Creating a new project](https://docs.byteplus.com/en/docs/6649/94336?_vtm_=a106466.b106468.0_0.0_0.0.820_7610615829733918244&lang=en#%E6%96%B0%E5%BB%BA%E9%A1%B9%E7%9B%AE).<br><br>> **tip**<br><br><br><br>* > After a task is created successfully, if you need to change its affiliated project, you can move the resource to another project.<br><br><br>* > A project is a virtual concept that includes a set of resources, users, and roles. A project allows for a unified view and management of a set of resources, and controls the permissions of users and roles within the project for those resources.<br> |
||**Tag** |(Optional) Click **Add tag** to add a tag to the instance. Tags can help you categorize cloud resources, control access to them, and allocate bills and costs. A tag is a key\-value pair that identifies a cloud resource. You can use tags to categorize resources with the same characteristics from different dimensions, such as purpose or owner, making it easier to filter, aggregate, and manage your cloud resources. For more details about tags, refer to Tag overview. The rules for tag key\-value pairs are as follows:<br><br><br>* Key<br><br>   * Supports any language, characters, numbers, spaces, or symbols (_.:/=+\-@).<br><br>   * Case\-sensitive, and the length is 1 to 128 characters.<br><br>   * In UTF\-8 encoded Unicode format.<br><br>   * Keys cannot start with any form of `volc:`, such as `Volc:` or `VOLC:`.<br><br>* (Optional) Value<br><br>   * Supports any language, character, digit, space, or symbol (_.:/=+\-@).<br><br>   * Case\-sensitive, and the length is 0 to 256 characters.<br><br>   * In UTF\-8 encoded Unicode format.<br><br><br>> **tip**<br><br><br><br>* > Support fuzzy search for selecting existing tag keys and tag values.<br><br><br>* > A maximum of 20 tags can be associated with a task in a single operation. A maximum of 50 tags can be associated with a single task.<br><br><br>* > For a single resource, tag keys must be unique, and each tag key can have only one value.<br> |
||**Billing method** |Currently, only **Pay\-as\-you\-go** is supported. No selection is required.<br><br>> **tip**<br><br><br>> For detailed billing information, refer to [Billing instructions](https://docs.byteplus.com/en/docs/DTS/billing_overview?lang=en).<br> |

6. Click **Next step: configure migration object**.

7. On the configure migration object wizard page, configure the following parameters as needed.

|**Name** ||**Description** |
|---|---|---|
|**Migration module** ||Select the required Supabase migration modules:<br><br><br>* **Database**: stores text and numeric structured data such as user information, account data, form data, and business records. Supports data queries, modifications, statistics, and permission control.<br><br>* **Storage object**: stores files like images, videos, documents, and attachments. Responsible for file uploading, downloading, storage, and access management. |
|**Database** |**Migration type** |Select migration types as needed, currently supporting **Schema migration** and **Full migration**. |
||**Select object** |In the source object list on the left, use regular expressions to precisely locate target databases and tables. (To use Global search, expand all object nodes first.) On the right in the **Selected databases and tables** area, use fuzzy search to quickly filter and batch delete selected databases and tables. |
|**Storage object** |**Migration type** |Currently only **Full migration** is supported. |
||**Select object** |In the source object list on the left, you can accurately locate the target storage object using regular expressions (to perform global search, first expand all object nodes). In the **Selected object** area on the right, you can quickly filter with fuzzy search and batch delete selected storage objects. |
|**Advanced configuration** |**Error retry time** |Setting this parameter is not supported temporarily; the default is 600 seconds. If a synchronization task fails due to a disconnection between the source and target databases, the system immediately retries connecting to them multiple times within the specified time. |

8. Click **Pre\-check**.

9. Optional. If a pre\-check has been performed for the created task, you can confirm whether to restart the pre\-check based on the prompts. If you need to restart, click **OK** in the **Whether to restart the pre\-check** dialog box.

   * If the instances of the source and target databases are not modified, there is no need to restart the pre\-check.

   * If you modify the source and target database instance information or the synchronization task parameters, it is recommended to restart the pre\-check to avoid task startup failures or interruptions.

10. On the **Pre\-check** configuration wizard page, perform the following actions based on the check result:

   * Click **Details** in the **Actions** column of the pre\-check results to view detailed alert and failure messages. After modifying the databases and tables accordingly, click **Retry**.

   * Click **Ignore** in the **Actions** column to ignore the alert and continue starting the synchronization task. You can also click **Ignore all** to ignore all alert messages with one click.

      * If you choose to **Ignore** the alert and start the synchronization task, it may cause data inconsistencies and business risks.

      * For details about the pre\-check, refer to [Pre-check items](https://docs.byteplus.com/en/docs/DTS/pre-check-items-supabase?TagIDs=2&lang=en).

11. At the bottom\-right of the **Pre\-check** page, click **Confirm order**.

12. On the **Confirm order** configuration wizard page, confirm the configuration information again. Read the Service\-Specific Terms for BytePlus Database Products and Services and check **I have read and agree to Service\-Specific Terms for BytePlus Database Products and Services**, and click **Create and start a task**.

   After successfully creating the data synchronization task, you can return to the DTS console to view the data synchronization task information on the data synchronization task list.

## FAQ

### What if the source end object is deleted during migration?

Do not change the source end object during migration. If the source end object is deleted during migration, it cannot be synchronized to the destination, which may cause data loss. Perform migration during off\-peak hours and try to pause write or delete operations on the source end data.

### Why is connecting to source end PostgreSQL necessary?

Connecting to source end PostgreSQL obtains a more stable and efficient object list. By directly reading the metadata tables of Supabase Storage (`storage.buckets` and `storage.objects`), this avoids pagination drift issues caused by solely relying on the Storage List API when handling large Buckets or frequent object changes, while significantly reducing API call overhead and delay.

### Why does the destination need to support the TUS protocol?

The destination supports the TUS protocol to ensure reliable transmission of large files. For large files, migration tasks use shard resumable upload based on the TUS protocol. If the destination does not support this capability, large file migration may fail due to network fluctuations or other reasons and cannot recover automatically.
