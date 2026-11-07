---
title: "Associate Torch Log Service with a MySQL database"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Associate-Torch-Log-Service-with-a-MySQL-database"
---

The query and analysis module of Torch Log Service (TLS) allows you to associate TLS log data with a MySQL database when you query logs. This topic describes how to associate TLS with a MySQL data source.

<span id="0dd0f88b"></span>
## Background

In the actual production environment, fact tables that store data related to production events such as system logs and sales records and dimension tables that store basic business metadata are usually stored in different systems or databases. In e\-commerce scenarios, information related to user events and behaviors is stored in TLS in the form of logs. The information includes access data, product purchase data, payment methods, and network types; User registration information and member data are stored in database systems and not printed to logs due to data security considerations.

In log analysis scenarios, fact tables can be associated with dimension tables. Raw data streams are the foundation for query and analysis, while a large number of associated external tables store details and properties. Based on the preceding scenarios, the query and analysis engine of TLS allows you to associate TLS with external MySQL data sources to perform join queries. When you query data from TLS, you can use the JOIN clause of SQL to associate TLS log data with MySQL database data to expand the search scope.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The external data source is a feature available via invitation\-only testing. If you have business needs, please contact your account manager to apply for the whitelist.</div>


* <div data-tips="true" data-tips-type="tip">For now, there is no charge for using the external data source. Please pay attention to subsequent product announcements regarding the charging time and corresponding billing rules.</div>



<span id="644c8c98"></span>
## Precautions


|Category |Description |
|---|---|
|Data security |For security purposes, TLS accounts that access a MySQL database must have the minimum required permissions. TLS requires only the SELECT and INSERT permissions. We recommend that you specify a dedicated database account to perform join queries and keep the account properly. |
|MySQL Database Connection Address |When building a self\-hosted MySQL database in ECS, it is recommended to set the connection address to `0.0.0.0`, allowing all servers to access the MySQL database. Then, control the access rights through the ECS security group to enhance the security of the database. |
|MySQL Database User |By default, the root user of the MySQL database is only allowed to log in to the MySQL database on the local server. Therefore, you need to create a new user for remote access to the MySQL database or grant the root user remote access permission. |
|MySQL Database Whitelist |The whitelist is a security prevention and control measure for database connections. Only IP addresses within the whitelist can access the database. That is, before associating the MySQL data source, you need to set up a whitelist on the MySQL data source side to allow the IP addresses related to TLS to access the MySQL data source. |


<span id="Limits"></span>
## Limits


|Item |Description |
|---|---|
|External data source |MySQL data sources can be BytePlus RDS for MySQL instances and self\-managed MySQL databases on BytePlus Elastic Compute Service (ECS) instances. Make sure that the RDS instance or ECS instance is in the same Region as the TLS topic. |
|MySQL version |MySQL 5.7 and MySQL 8.0 are supported. |
|MySQL table size |When you perform a join query, we recommend that the size of the associated MySQL table be less than 20 MiB. If the size is large, the database stability is reduced when TLS initiates a complex SQL query on the database. |
|Quota of external data sources |Up to 50 external data sources can be created in a project. |


<span id="Procedure"></span>
## Procedure

<span id="bf40f05c"></span>
### 1. Configure an allowlist

Before you associate TLS with an external data source, make sure that you have configured an allowlist to allow relevant TLS IP addresses to access the data source. The following table lists the IP addresses that must be added to the allowlist.


|Data Source |IP Address |Description |
|---|---|---|
|BytePlus RDS for MySQL instance |* 10.0.0.0/8<br><br>* 33.0.0.0/8<br><br>* 100.64.0.0/10 |Add the IP addresses to the database allowlist. |
|Self\-managed MySQL database on a BytePlus ECS instance |* 10.0.0.0/8<br><br>* 33.0.0.0/8<br><br>* 100.64.0.0/10 |If the ECS instance has a security group, add a rule to the security group to allow access from the specified IP addresses. |


<span id="2. Associating TLS with a MySQL data source"></span>
### 2. Associate TLS with a MySQL data source


1. Log on to the [TLS console](https://console.byteplus.com/tls).

2. In the top menu bar, select the region where TLS is deployed.

3. In the left\-side navigation pane, choose **Resource management** \> **Project**, then click the name of the target project.

4. On the **External data source** tab, click **Create data source association**.

5. Configure the data source.

   * Self\-managed database:

      
      |Parameter |Description |
      |---|---|
      |Data source name |The name of the external data source. The name must be unique in the project. |
      |Type |The type of the external data source. Only **MySQL** is supported, which indicates a MySQL data source. |
      |Database type |The database type. In this example, select **self\-built database**, which indicates a self\-managed MySQL database on a BytePlus ECS instance. |
      |Connection address |The private IP address of the ECS instance. |
      |Port |The port number used by the MySQL service. |
      |VPCId |The ID of the virtual private cloud (VPC) where the ECS instance is located. |
      |Database username |The username of the MySQL database. |
      |Database password |The password of the MySQL database. |
      |Database |The name of the MySQL database. |
      |Data databases & tables |The name of a table in the MySQL database. |
      

   * BytePlus RDS for MySQL instance:

      
      |Parameter |Description |
      |---|---|
      |Data source name |The name of the external data source. The name must be unique in the project. |
      |Type |The type of the external data source. Only **MySQL** is supported, which indicates a MySQL data source. |
      |Database type |The database type. In this example, select **Byteplus RDS for MySQL**, which indicates a BytePlus RDS for MySQL instance. |
      |Select region |The Region where the RDS for MySQL instance is located. The Region must be the same as the current project. |
      |Select AZ |The Availability Zone where the RDS for MySQL instance is located. |
      |Select instance |The name of the RDS for MySQL instance. |
      |Connection address |The private endpoint of the RDS for MySQL instance. |
      |Port |The port number in the private endpoint of the RDS for MySQL instance. When the endpoint is specified, the port number is automatically populated. |
      |VPCId |The VPC where the RDS for MySQL instance is located. When the instance is specified, the VPC is automatically populated. |
      |Database username |The username of the database on the RDS for MySQL instance. |
      |Database password |The password of the database on the RDS for MySQL instance. |
      |Database |The name of the database on the RDS for MySQL instance. |
      |Data databases & tables |The name of a table in the database on the RDS for MySQL instance. |
      

6. Click **Test connection**.

   TLS automatically tests the connectivity between the server and the MySQL data source. If the connectivity test is passed, click **Create Data Source Association**.


<span id="aa357fce"></span>
## Related operations

After you associate TLS with an external data source, you can view, modify, or delete the data source. The following table describes the operations.


|Related Operation |Description |
|---|---|
|View external data sources |On the **External data source** tab of the project details page, view all the external data sources associated with the current topic. Click the name of a data source to view its details. |
|Modify the configurations of an external data source |On the **External data source** tab, find the target data source, then click **Edit** in the **Actions** column to modify the configurations. Currently, you cannot change the value of **Type** or **Database type** for a data source. |
|View the connection status of an external data source |On the **External data source** tab, view the connection status in the<br><br>**Connection status** column. If the connection fails, modify the configurations and click **Retry**. |
|Delete an external data source |If an external data source is no longer required, find the data source on the **External data source** tab, then click **Delete** in the **Actions** column. |
|Perform join queries on a topic and an external data source |Use the JOIN clause to query data from a topic and a MySQL database, and save the query and analysis results to the MySQL database. |
