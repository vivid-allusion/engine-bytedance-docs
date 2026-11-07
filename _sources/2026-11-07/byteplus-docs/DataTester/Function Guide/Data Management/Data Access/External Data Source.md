---
title: "External Data Source"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/External-Data-Source"
---

You need to create a data source corresponding to the external data warehouse in DataTester, specify the connected data warehouse database and the authentication, login and other information required for the connection, so that you can directly query the data warehouse indicator table in the corresponding database when using the data warehouse indicator later.

<span id="71f0cfde"></span>
# Operation steps

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/12adf3c742454bdbacdff480a6746f93~tplv-goo7wpa0wc-image.image) </span>

The configuration instructions for the core configuration items of various data sources are as follows.


|Configuration item classification |Hive Data Source |Spark |Clickhouse |ByteHouse CE |ByteHouse CDW |
|---|---|---|---|---|---|
|Connection method |Support:<br><br><br>* **Ip/Port**: You need to configure the corresponding server Internet Protocol Address and port number<br><br>* **JDBC**: configure JDBC string<br><br>* **PSM** (Clickhouse only): When using the Clickhouse in the private cluster of BytePlus, you can use the PSM method to connect, and you need to configure the identity registered by the Clickhouse in the consul, such as: vpc.olap.clickhouse ||||Support: Auth Token |
|Authentication/Authentication Method |Select the authentication method of docking according to the authentication requirements of the database:<br><br><br>* **Username Password**: The username and password configured for the database<br><br>* **Kerberos** (Only supported by hive): Configure the corresponding authentication parameters and upload the authentication file ||||* ApiKey: You need to configure the apiKey, compute group name, and region name to connect to the database<br><br>* AK/SK: You need to configure the AK/SK connected to the database (including AK/SK under the Volcano Cloud customer account), the name of the computing group, and the name of the region. |
|Docking database |Configure the **database name and queue name** in the docking warehouse (Clickhouse, ByteHouse CE, ByteHouse CDW do not need to configure the queue). |||||
|Resource and memory limits |Configure the **resource usage limit** and the **memory usage limit**, which represent the CPU and memory limit respectively.<br><br>If this resource limit is exceeded, subsequent queries follow a first\-in, first\-out queuing policy. |||||
|Execution time and QPS limits |Does not involve |Does not involve |To avoid overloading the database cluster, set the maximum execution time of data reads and the limited viewership of QPS. |||
|Custom parameters |Does not involve |According to the actual situation of the data warehouse database, add the advanced parameters/custom parameters of the corresponding database to the custom parameter configuration here. ||||
|Test connection |After completing the configuration of the data source docking parameters, click **Test Connection** in the upper right corner to test whether the data source can be connected normally. |||||


<span id="9faa157a"></span>
# Next step

After you have created the external data source, you need to proceed with the warehouse data set creation, see activity details [Data Warehouse Dataset](https://docs.byteplus.com/docs/DataTester/Data-Warehouse-Dataset).
