---
title: "Data source management"
product: "Observability Platform"
product_code: "Observability_Platform"
source: "https://docs.byteplus.com/en/docs/Observability_Platform/data-source-management"
---

You can use data source management to establish connections between Observability Platform and external databases. After you configure a data source, you can use it directly in custom dashboards to query and visualize external data.

## Prerequisites

* You have obtained the host address, port, database name, username, and password of the target database.

* The database account has query permissions on the target data.

* The database supports public network access, and Observability Platform can access the server where the database resides.

## Limits

Currently, you can connect only to MySQL databases.

## Procedure

1. Log in to the [Observability Platform ](https://console.byteplus.com/observe/dashboard/dashboard)console, and in the left navigation bar, select **Custom Dashboard**.

2. Click the **Data source management** tab and **Create data source**.

3. Select the data source type, configure the parameters based on your business requirements, and click **Save and test**.

   |Parameter |Parameters |Description |Figure |
   |---|---|---|---|
   |Basic information |Data source name |The custom name of the data source. You can use this name to identify and select the data source when you create a dashboard. Data source names must be unique within the same project and can contain up to 190 characters. | |
   |Connection |Host address |The hostname or IP address of the server where the database resides. This parameter identifies the database server to connect to.<br><br>> **tip**<br><br><br>> Make sure that the address is accessible over the public network and from Observability Platform.<br> | <br><br> <br><br> |
   ||Port |The listening port of the database, which is used to establish database connections. The default value is 3306. ||
   ||Database |The name of the database to connect to. ||
   ||User name |The name of the account used to connect to the database.<br><br>> **tip**<br><br><br>> The account must have the`SELECT`permission on the target data.<br> ||
   ||Password |The login password of the account. Enter the password that matches the username. ||
   |TLS / SSL |TLS client authentication |Specifies whether to use the client certificate specified in the secure JSON configuration for TLS authentication.<br><br>> **tip**<br><br><br><br>* > Before you enable this option, make sure that TLS is enabled for the database.<br><br><br>* > After you enable this option, upload a valid client certificate and private key, and the database verifies the identity of the client. For more information about TLS and configuring encrypted connections in MySQL, see [Using TLS connections](https://dev.mysqlserver.cn/doc/refman/8.4/en/mysql-cluster-tls-using.html) and [Configuring MySQL to use encrypted connections](https://dev.mysqlserver.cn/doc/refman/8.4/en/using-encrypted-connections.html).<br> | <br><br> <br><br> |
   ||Custom CA certificate |Specifies whether to use a CA certificate for authentication. The system uses the specified CA certificate to verify the identity of the server where the database resides.<br><br>> **tip**<br><br><br><br>* > Enable this option to verify self\-signed TLS certificates. Follow the instructions of your CA (certificate authority) to download the certificate file.<br><br><br>* > After you enable this option, upload the root CA certificate. The system uses the certificate to verify the identity of the database server.<br> ||
   ||Skip TLS verification |Specifies whether to skip verification of the server's TLS certificate chain and hostname.<br><br>> **warning**<br><br><br>> If you enable this option, the system skips verification of the server certificate, which poses security risks. Proceed with caution.<br> ||
   |Advanced Settings |Session timezone |Specifies the time zone used by database connections, which affects how date and time data is queried and displayed. For more information about session time zones, see [MySQL Server Time Zone Support](https://dev.mysqlserver.cn/doc/en/time-zone-support.html). | |
   ||Minimum interval |The minimum time granularity for database queries. Data at intervals shorter than this value is not displayed separately.<br><br> ||
   ||Connection timeout |The maximum amount of time to wait when connecting to the database. If the timeout is exceeded, the connection request fails. ||
   ||Query timeout |The maximum execution time of a single database query. If the timeout is exceeded, the query is terminated. ||
   ||Max returned rows |The maximum number of rows that a single database query can return. Rows that exceed this limit are truncated. ||
   ||Max active connections |The maximum number of open connections to the database. You can increase this value if there are many concurrent queries. ||
   ||Max idle connections |The maximum number of idle connections kept for the database, which reduces the overhead of frequently establishing connections. ||
   ||Max connection lifetime |The maximum lifetime of a single database connection. When it expires, the system automatically re\-establishes the connection. ||

## What to do next

* After you create a data source, you can use it directly in custom dashboards to query and visualize external data. For more information, see [Data query](https://docs.byteplus.com/en/docs/Observability_Platform/Data_query).

* After you create a data source, you can perform the following operations on the **Data source management** tab.

|Actions |Description |
|---|---|
|Edit |Click **Edit** in the Actions column of the target data source to modify its configuration parameters. After the modification, we recommend that you click **Test** to check whether the connection works properly. |
|test |Click **Test ** in the Actions column of the target data source to check whether the connection to the data source works properly. If the test fails, check the host address, port, database name, account permissions, password, and network access configuration. |
|Delete |Click **Delete** in the Actions column of the target data source to delete it. If a dashboard references the data source, the system prompts you to confirm whether to continue the deletion.<br><br>> **warning**<br><br><br>> Deleted data sources cannot be recovered, and queries in dashboards that reference the data source may fail. Proceed with caution.<br> |
