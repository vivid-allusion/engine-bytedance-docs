---
title: "Metadata connections"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Metadata_connections"
---

The metadata connection is a module in the Volcano Engine E\-MapReduce (EMR) Configuration Center, used to maintain configuration information for connections to external databases (for example, Hive, Ranger, Airflow, or DolphinScheduler metadatabases hosted in Volcano Engine RDS outside the EMR cluster), such as the RDS instance name, as well as the database name, username, password, and so on.

By managing metadata connections through the Configuration Center, you can reuse configured database connections and centrally manage database connection configurations.

<span id="_1-创建元数据连接"></span>
## Step 1: Create a metadata connection

You can create a metadata connection in either of the following two ways:


* Create a metadata connection from the Configuration Center page. The steps are as follows:

   1. Log in to the [E-MapReduce Console](https://console.byteplus.com/emr/region:emr_fe+ap-southeast-1/home?).

   2. In the left navigation pane of the EMR page, click **Configuration Center** \> **Metadata connection**entry to access the metadata connection page, where the list of created metadata connections is displayed.

   3. Click the **Create connection**button in the upper right corner of the page to enter the creation configuration.

* Create a metadata connection when creating a cluster. The steps are as follows:

   1. Go to the **Create Cluster** page, in the **Software configuration** \> **Metadata selection**section (if any), in the row of the service component to be bound to the metadata connection, select **Data connection type**as**External database.**  For details, see [Create clusters (version 3.18.0 and earlier)](https://docs.byteplus.com/docs/E-MapReduce/105456) **.** 

   2. Click the **Create Connection** button on the right side of the row to enter the creation configuration.


Using either of the two methods above, a **Create metadata connection**dialog box will pop up on the page. You can fill in the relevant information in this dialog box to create a metadata connection. The specific configuration items are described as follows:


|**Configuration item** |**Note** |
|---|---|
|Connection name |Enter the metadata connection name. |
|Description |Description of the metadata connection, to facilitate future management. |
|RDS instance ID |Select the RDS instance ID that the currently logged\-in user owns from the drop\-down list.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">You can search for RDS instances. The database RDS instance and the EMR cluster must be deployed in the same VPC to ensure network connectivity. You can go to the console to <a href="https://console.byteplus.com/db/region:db+ap-southeast-1/rds-mysql/create?ChargeType=PrePaid">Create RDS instance</a>.</div><br> |
|Database name |* Custom: You can explicitly specify the name of an existing database in the RDS instance. The database user configured in the metadata connection must have read and write permissions for the database.<br><br>* Random generation: If no database name is specified, when creating a cluster using this metadata connection, the system automatically creates a database with a random name (the database name does not duplicate any existing database name in the RDS instance) and grants the database user configured in the metadata connection read and write permissions for this database. |
|Database username |The username of the database. |
|Database password |The password of the database. |


After filling in the relevant information and confirming it is correct, perform the following operations:


1. Click the **Test connection**button in the dialog box to test the availability of the connection (including whether the user has read and write permissions for the database, as well as the accuracy of the username and password).

2. After the connection test passes, click the **OK** button in the dialog box to complete the creation of the metadata connection.

3. The successfully created metadata connection will appear in the metadata connection list on the **Configuration Center** \> **Metadata connection** page. When creating a cluster, it can be specified in the **Software Configuration** \> **Metadata connection** step (if applicable) as the data connection instance for the service component whose data connection type is **external database**.


<span id="_2-管理元数据连接"></span>
## 2 Managing metadata connections

On the list page of **Metadata connection**, you can manage the connection list as follows:


* **Search for metadata connections**: In the search box on the right side of the metadata connection page title bar, you can search for the required metadata connection by **connection name** or **connection ID**.

* **View clusters associated with the metadata connection (if any)** : In the **Actions** column of the corresponding row for the metadata connection, click **Associated Cluster** to view information about clusters associated with this metadata connection.

* **Edit metadata connection**: In the **Actions** column of the corresponding row for the metadata connection, click the **Edit** button to edit metadata connections that are not associated with clusters or cluster templates.

* **Delete metadata connection**: In the **Actions** column of the corresponding row for the metadata connection, click the **Delete** button to delete metadata connections that are not associated with clusters or cluster templates.

* **View metadata connection details**: In the corresponding row for the metadata connection, click the **connection name** to view the details of this metadata connection.


<span id="_3-注意事项"></span>
## 3 Important notes


* You must configure the EMRFullAccess access policy to access the Configuration Center.

* If the metadata connection is used for the external database of Airflow or DolphinScheduler, the database name of the metadata connection must be set to **randomly generated**. If the metadata connection is used for the external database of Hive or Ranger, the database name of the metadata connection must **be specified as** a database name that already exists in the configured RDS instance.

* Metadata connections cannot be reused across service components. That is, if a metadata connection has already been used by a cluster for a certain type of service component (for example, Hive), then this metadata connection cannot be used for any other type of service component (for example, Ranger) in any cluster.

* For a specific service component (for example, Hive), can a metadata connection be reused by multiple clusters?

   1. The same metadata connection can be reused by Hive in multiple clusters.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">For Hive instances that reuse the same metadata connection, their major version numbers must be consistent. If a metadata connection is currently or has ever been used by the Hive of a cluster, regardless of whether the cluster has been released, this metadata connection cannot be used by the Hive of other clusters with <strong>different major version numbers</strong>. However, it can be used by the Hive of other clusters with <strong>the same major version number</strong>.   </div>
   

   2. The same metadata connection cannot be reused by Ranger in multiple clusters (if a metadata connection is currently or has ever been used by Ranger in a cluster, regardless of whether the cluster has been released, this metadata connection cannot be used by Ranger in any other cluster).

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">For metadata connections where the database name is specified by the user during creation, if two different metadata connections are configured with the same RDS instance and database name and are used for the same service in two different clusters, the actual effect is the same as having the two clusters share the same metadata connection for that service. If the Ranger of these two clusters (regardless of whether they have been released) uses the same metadata database (regardless of whether it is the same metadata connection), or if Hive instances with different major version numbers use the same metadata database (regardless of whether it is the same metadata connection), exceptions may occur.   </div>
   

   3. The same **metadata database** cannot be reused by Airflow / DolphinScheduler in multiple clusters. However, the same **metadata connection** can be reused by Airflow / DolphinScheduler in multiple clusters, because the database name configured in the metadata connection for Airflow / DolphinScheduler is **randomly generated**, and is randomly generated and created when the cluster is created using the metadata connection (not when the metadata connection itself is created). Therefore, even if the metadata connection corresponding to Airflow / DolphinScheduler in multiple clusters is the same (the Airflow / DolphinScheduler metadata databases for these clusters will be under the same RDS instance and have the same access username and password), they are still different databases, which meets the requirement that "the same **metadata database** cannot be reused by Airflow / DolphinScheduler in multiple clusters".

* For a metadata connection that you specify for an existing database, the database user configured in the metadata connection must have read and write permissions for that database.
