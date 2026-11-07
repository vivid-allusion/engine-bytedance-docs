---
title: "Modify configuration parameters"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/modify-configuration-parameters"
---

This tutorial introduces how to configure cluster parameters and user parameters in ByteHouse Enterprise, how to grant or revoke permission to use user parameters for specified users, and how to create custom user parameters.

<span id="49af5e16"></span>
# Feature overview

ByteHouse Enterprise clusters support configuring cluster parameters and user parameters separately through the config.xml and user.xml configuration files, in order to meet your needs for cluster performance optimization and business adaptation.


| |Cluster parameter (config.xml) |User param (user.xml) |
|---|---|---|
|**Definition** |Cluster\-level global configuration items affect the operating rules of the entire cluster, such as resource allocation caps, service timeouts, and so on. |Parameters for a specified user, used to personalize system behavior for that user during operations such as query optimization, import optimization, and so on. |
|**Function scope** |Covers all nodes, users, and query tasks in the cluster. |Applies only to the specified user and does not affect other users or the entire system. |
|**Use cases** |Cluster parameters can be used for cluster architecture adjustment, global performance optimization, general rules management, and other scenarios. |You can adjust user parameters as needed to satisfy the requirements of your specific business scenarios. ByteHouse also provides built\-in user parameter templates for different scenarios, which satisfy the needs of specific data model queries—such as star schema, snowflake schema, and wide table data—as well as high\-concurrency scenarios. |
|**Configuration method** |You can adjust Param through visual settings or an XML configuration file. For Activity details, see [Configure cluster parameters](https://docs.byteplus.com/docs/bytehouse/modify-configuration-parameters#aba77abc). |* **Modify user parameters**: ByteHouse allows you to adjust user parameters through visual settings or an XML configuration file. For operation details, please refer to [Configure user parameters](https://docs.byteplus.com/docs/bytehouse/modify-configuration-parameters#a343f25c).<br><br>* **Manage user param templates**:<br><br>   * **Enable user param template**: By default, all users use the ByteHouse Default Profile. You can use other user param templates by granting permissions to specified users; for details on these actions, see [Grant or revoke user param permissions for users](https://docs.byteplus.com/docs/bytehouse/modify-configuration-parameters#6144ef37).<br><br>   * **Custom user param template**: ByteHouse also supports creating user parameters as needed. For details, see [Create user param templates](https://docs.byteplus.com/docs/bytehouse/modify-configuration-parameters#e36174f1). |
|**Activation mechanism** |After cluster parameter changes, you usually need to **restart the cluster** for the changes to take effect. Therefore, the operation should be performed during off\-peak business hours to avoid affecting online services. |After modifying user parameters or granting or removing user parameter permissions, the parameters will take effect immediately for the specified user. |


The following is a description of the built\-in user parameter template in ByteHouse:


* Default configuration: This refers to the Default Profile, which contains the system default user parameters. ByteHouse grants this permission to all users by default.

* Built\-in templates: ByteHouse provides user parameter templates for specific scenarios. You can authorize a specified user to activate the template, including:

   * Complex query template (star schema): Suitable for datasets with a star schema.

   * Complex query template (snowflake model): Suitable for datasets in the snowflake model.

   * Wide table search template: Suitable for wide table search.

   * High concurrency template: Suitable for modes with concurrency between 100 and 1000.


<span id="3678158b"></span>
# Usage limitations

Only users with the Cluster Admin and System Admin roles can modify configuration parameters.

<span id="326b827f"></span>
# Caution


* After the cluster parameter changes are complete, you need to manually restart the cluster for the changes to take effect. Before restarting, please confirm that restarting the target cluster will not affect business operations.

* After user parameters have been modified, there is no need to restart the cluster; the parameters take effect in real time.


<span id="aba77abc"></span>
# Configure cluster parameters

<span id="31d05a75"></span>
## Steps


1. Log in to the ByteHouse Enterprise console. In the upper left corner of the page, select the region where the target cluster is located. Click the **Cluster management** tab, and go to the **Cluster list** page. Click Cluster parameters in the Actions column of the row for the target cluster, then click Edit cluster configurations.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c63a59ce488a40d2b691a3f18a0dbf45~tplv-goo7wpa0wc-image.image) </span>

2. Enter parameter editing state, enter a change description, and **Configure in table** or use **XML Configuration** to modify the parameter value.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/49bedc471a2a46ceb0e4a5f947c6f7ac~tplv-goo7wpa0wc-image.image) </span>

   * **Configure in table**: This option sisually displays the names, reference values, running parameter values, and other information of commonly used parameters. However, the visual settings only display commonly used parameters. If you do not find the parameter you want to modify in the parameter list, or if you need to customize parameters, you can modify them through the XML configuration.

   * **XML Configuration**: This option displays parameters in XML format, including common parameters and custom parameters.

3. After completing the changes, click **Save and release changes**.

4. After submitting the configuration delivery task, some parameters require a cluster restart to take effect. Click **Restart Cluster** on the page. Before restarting, please confirm that restarting the target cluster will not affect business operations.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9ca34ced03fc4b158c6776aa8bad68c4~tplv-goo7wpa0wc-image.image) </span>


<span id="1d1d2afc"></span>
## Cluster parameter description


|**Parameter Name** |**Default Value** |**Parameter Description** |
|---|---|---|
|builtin_dictionaries_reload_interval |3600 s |Automatic reload interval for the built\-in dictionary. |
|compiled_expression_cache_size |134,217,728 bytes |Cache size of compiled expressions. |
|default_session_timeout |3600 s |Default session timeout period. |
|keep_alive_timeout |10 s |Number of seconds to wait for incoming requests before the connection is terminated. |
|max_session_timeout |3600 s |The maximum session timeout value. |
|mark_cache_size |4,294,967,296 bytes |Size of the Mark cache. |
|max_concurrent_queries |200 |Maximum number of concurrent searches. |
|max_connections |4096 |The maximum number of concurrent connections for the cluster. |
|max_open_files |0 |Maximum number of open files.<br><br><br>* 0: Unlimited size.<br><br>* Other ≥ 0 values: restrict the specified size. |
|max_partition_size_to_drop |0 bytes |Delete the size limit for the part.<br><br><br>* 0: Unlimited size.<br><br>* Other values ≥ 0: Restrict the specified size. |
|max_server_memory_usage_to_ram_ratio |0.9 |Maximum proportion of server memory usage to physical memory. |
|max_table_size_to_drop |0 bytes |Remove the table size limit.<br><br><br>* 0: Unlimited.<br><br>* For other values greater than or equal to 0: Limit the specified size. |
|uncompressed_cache_size |4,294,967,296 bytes |Cache size used for uncompressed data, default 4GB. |
|timezone |UTC |The timezone used by the cluster. |


<span id="a343f25c"></span>
# Configure user parameters

ByteHouse Enterprise user parameters support the following functions:


* **Modify user parameters**: ByteHouse supports adjusting parameters through a visual interface or an XML configuration file.

* **Manage user param templates**:

   * Grant or revoke permission for the specified user to use user parameters.

   * Create a custom user parameter template.


<span id="ad0a47ae"></span>
## Modify user parameters


1. Log in to the ByteHouse Enterprise management console. In the upper left corner of the page, select the region where the target cluster is located. Click the **Cluster management** tab to enter the **Cluster list** page. Click Cluster parameters in the Actions column of the row for the target cluster then click **View profile**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c83131a76a8f46809ff0974b2afbd699~tplv-goo7wpa0wc-image.image) </span>

2. Click the **Profile name** you want to modify, for example, Default Profile, and enter the details page.

3. Click **Modify configurations** to modify the parameter value via **Configure in table** or **Configure in XML**.

   Edit interface examples are as follows:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c938eb4def244fffb6f7ffac58101748~tplv-goo7wpa0wc-image.image) </span>

   * **Configure in table**: This option visually displays the names, runtime parameter values, types, and other information of commonly used parameters. However, visual settings only display commonly used parameters. If you cannot find the parameter you want to modify in the Parameter List, or if you need to use custom parameters, you can modify them through XML settings.

   * **XML Configuration**: This option displays parameters in XML format, including common parameters and custom parameters.

4. After completing the modification, click **Save and release changes**. The system will then modify the corresponding cluster parameters. User parameters do not require a restart. Changes take effect within seconds after modification.


<span id="e36174f1"></span>
## Create user param templates

ByteHouse supports creating user param templates as needed.


1. Log in to the ByteHouse Enterprise console. In the upper left corner of the page, select the region where the target cluster is located, click the **Cluster management** tab, and go to the **Cluster list** page. Click Cluster parameters in the Actions column of the row corresponding to the target cluster, then click **View profile**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c83131a76a8f46809ff0974b2afbd699~tplv-goo7wpa0wc-image.image) </span>

2. Click **Create new profile** to go to the creation page.

3. According to the interface requirements, fill in the user parameter information.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/def4032f8cae43ffb3a4dbf25c087964~tplv-goo7wpa0wc-image.image) </span>

   * **Profile name**: Define your user parameter name

   * **Granted users**: Grant view, use, and manage permissions to specified users for user parameters.

   * **Description**: Custom description for easier subsequent management.

   * **User parameters**: Define your user parameters according to your business requirements by using visual or XML settings.

4. After completing the form, click **Create and release**.


<span id="6144ef37"></span>
## Grant or revoke user param permissions for users

To use either the built\-in user parameter templates in ByteHouse or the user parameters you create, users must first be granted permission.

Each user can only be granted permission to use one user parameter template. After permission is granted, the system will use the new user parameters to overwrite the existing user parameter configuration. After removing the binding between the user and the specified user parameter, the system will overwrite the existing user parameter configuration with the default user parameter (Default Profile) configuration.

**Steps:** 


1. Log in to the ByteHouse Enterprise console. In the upper left corner of the page, select the region where the target cluster is located. Click the **Cluster management** tab to enter the **Cluster list** page. In the Actions column of the row for the target cluster, click **Cluster parameters** and then click **View profile**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c83131a76a8f46809ff0974b2afbd699~tplv-goo7wpa0wc-image.image) </span>

2. On the user parameter page, click the **Grant to users** button in the row containing the user parameter name to go to the user parameter authorization page.

   * Grant permission: Select users from the list of users who have already been granted permission.

   * Revoke granted permissions: Click the × icon after the user name.

3. After the configuration is complete, click **Confirm**. After you submit, you can view the user name in the granted users column to confirm that the permission adjustment has taken effect. You can also, based on the adjusted parameter type, log in as an authorized user to perform search operations and verify whether the search behavior meets expectations.


<span id="da2863f5"></span>
## User param descriptions


|**Parameter name** |**Default** |Param**description** |
|---|---|---|
|`dialect_type` |CLICKHOUSE |SQL dialects. Available options: ClickHouse, ANSI, or MySQL. |
|`enable_sharding_optimize` |0 |Determines whether the query computes results within each node before aggregating results across multiple nodes. If you can ensure that the JOIN KEY, GROUP BY KEY, and SHARDING KEY are the same in the query, setting this parameter to 1 will significantly improve query performance. In all other cases, set the value to 0; otherwise, the query results will be incorrect. |
|`input_format_skip_unknown_fields` |1（True） |Whether to ignore unknown columns when importing in JSONEachRow, TSKV, and other formats. If set to 1, it will be ignored; if set to 0, an error will be reported. |
|`max_execution_time` |300 s |Maximum timeout duration for a single SQL query (in seconds). |
|`max_insert_block_size` |1,048,576 rows |Maximum number of rows generated for a data block (Part) in a single INSERT operation. |
|`max_insert_block_size_bytes` |0 bytes (Unlimited) |Estimated maximum size in bytes of a data block (Part) generated during a single INSERT operation. |
|`max_memory_usage` |9,771,050,598 bytes (approximately 9.1 GB) |The maximum memory allowed for a single query.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip"><code>max_memory_usage</code> and <code>max_memory_usage_for_user</code> are two independent memory parameters; there is no constraint on the relationship between their values.</div><br> |
|`max_memory_usage_for_user` |9,771,050,598 bytes (approximately 9.1 GB) |The maximum total memory allowed for all user queries at the same time. |
|`max_partitions_per_insert_block` |1,000 |The maximum number of partitions over which data can be distributed in a single INSERT operation, to avoid generating too many small files. |
|`max_query_size` |1,048,576 bytes (approximately 1 MB) |Maximum length limit for SQL statements. |
|`max_threads` |8 |The maximum number of query processing threads (excluding threads that retrieve data from remote servers). |
