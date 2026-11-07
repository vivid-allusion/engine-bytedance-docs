---
title: "Using JDBC"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/JDBC_usage"
---

<span id="_1-简介"></span>
# Overview

JDBC stands for Java DataBase Connectivity. It is the standard interface for Java programs to access databases. EMR Serverless Spark supports submitting tasks using JDBC. You can use the standard JDBC interface to access EMR Serverless Spark, and you can also integrate it with commonly used BI software.

<span id="_2-连接-emr-serverless-spark"></span>
# **Connect to EMR Serverless Spark**

<span id="_2-1-示例代码"></span>
## Sample code

```java
Class.forName("org.volcano.serverless.spark.jdbc.EMRServerlessSparkDriver");
Properties properties = new Properties();
properties.setProperty("user", "Ax");
properties.setProperty("password", "xx");
Connection conn = DriverManager.getConnection("jdbc:emr-serverless-spark://emr-serverless.cn-beijing.volcengineapi.com/;region=cn-beijing;queue_name=test_sparkjar-spark", properties);
Statement statement = conn.createStatement();
String sql = "select 1";
ResultSet resultSet = statement.executeQuery(sql);
while (resultSet.next()) {
    System.out.println(resultSet.getString(1));
}
```


<span id="_2-2-代码解释"></span>
## Code explanation

**Environment preparation**

Dependency: JDK 1.8

JDBC download address: [emr-serverless-spark-jdbc-driver.jar](https://emr-serverless.tos-cn-beijing.volces.com/spark/jdbc/serverless-spark-jdbc-1.8.2-release.jar)


2. Load the EMR Serverless Spark JDBC driver.


```java
Class.forName("org.volcano.serverless.spark.jdbc.EMRServerlessSparkDriver");
```



3. Connect to EMR Serverless Spark via DriverManager.


```java
Connection conn = DriverManager.getConnection("jdbc:emr-serverless-spark://xx/;region=cn-beijing;queue_name=test_sparkjar-spark", properties);
```



4. Create a Statement, execute SQL, and retrieve results.


```java
Statement statement = conn.createStatement();
String sql = "select 1";
ResultSet resultSet = statement.executeQuery(sql);
while (resultSet.next()) {
    System.out.println(resultSet.getString(1));
}
```


<span id="_2-3-jdbc-链接串参数说明"></span>
## JDBC connection string parameters

```bash
jdbc:emr-serverless-spark://${endpoint}/;region=${region};queue_name=${queueName}-${warehouseName}&user=${AccessKey}&password=${SecretKey}
```


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">As shown in the example, the four parameters region, queue_name, user, and password can also be placed in Properties.</div>



|Parameter name |Note |
|---|---|
|endpoint |The address for connecting to EMR Serverless Spark varies by region. For more details, see [Service address](https://docs.byteplus.com/docs/E-MapReduce/Service_address). |
|region |For region ID and more details, see [Service address](https://docs.byteplus.com/docs/E-MapReduce/Service_address). |
|queue_name |The queue name used for the connection. If not specified, the public queue is used by default. |
|warehouseName |Compute group name.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Specifying the Default compute group is not supported. You must create a separate compute group of Spark type.</div><br> |
|user |Enter the tenant's AccessKey |
|password |Enter the tenant's SecretKey |
|direct |Whether to use direct connection mode. The default is false (the system automatically routes). To configure this parameter, set it as follows: `properties.setProperty("direct", "true")`. |


<span id="_3-生态链接"></span>
# Ecosystem link

Using JDBC, you can use EMR Serverless Spark with any BI software that supports Hive, Spark, or custom JDBC connections. Below are examples of connecting BI software in various scenarios.

<span id="_3-1-使用idea连接emr-serverless-spark"></span>
## Use IDEA to connect to EMR Serverless Spark


1. In IDEA database connections, create a new JDBC connection Driver.

   * Click the  **+**  in the upper left corner to add a custom connection Driver.

   * In Driver Files, add the Driver Jar package for EMR Serverless Spark.

   * For Class, select: org.volcano.serverless.spark.jdbc.EMRServerlessSparkDriver.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ee9f2c09e1f022dde37fd1b4b9901535.png) </span>


2. Create a data source and select the Driver we just created.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0e5a944ca67a9cf853c6c5fad9943418.png) </span>


3. Fill in the relevant information.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f0a9452c9ff616aaa272d1f1c02d9157.png) </span>

**Parameter notes**


* Authentication: Select User&Password.

* User: Username. Enter your account's ak.

* Password: Password. Enter your account's sk.

* URL: Refer to the JDBC connection string parameter Note.

4. Click Test connection. If successful, the setup is complete.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ecdd5d4ca717a538c44f8441b4cb69c4.png) </span>


5. Open the database connection console, write SQL, and you can start your SQL analysis.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ffa2007c75e9664215b2a765d8fd9368.png) </span>
