---
title: "Connect to an instance"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/connecting-to-instance"
---

This topic describes how to connect to a RDS for SQL Server instance using Microsoft SQL Server Management Studio (SSMS) or sample code in Python, Java, or C#.

<span id="TdP9GuWP"></span>
## Preparation


* The instance has been created and is running. For more details, see [Create an instance](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/creating-instance-for-user-guide).

* According to the network type, prepare the corresponding environment, as shown in the table below.

   
   |**Network type** |**Preparation** |
   |---|---|
   |**Private network** |When an instance does not have public network access enabled and the instance's private network and the Elastic Compute Service(ECS) instance's private network are the same, you can connect through the private network and need to be prepared as follows:<br><br><br>1. Create Elastic Compute Service(ECS) instance. For steps, see [Purchasing and using ECS instance](https://docs.byteplus.com/en/docs/ecs/Buying-and-using-ECS-instances).<br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">When connecting to an instance through a private network address, ensure that the ECS instance and the SQL Server instance belong to the same private network.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">When connecting an instance via SSMS, you need to create a ECS instance for the Windows operating system.   </div><br>   <br><br>2. Create an allowlist in the RDS for SQL Server and add the private network address of the ECS instance to the allowlist. For more details, see [Creating allowlists](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/creating-allowlist).<br><br>3. Bind the allowlist to the target instance. For details, see [Associating allowlists to instances](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/associating-allowlist-to-instance).<br><br>4. Get the private network connection address of the SQL Server instance. For more information, see [Viewing connection address and port](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/viewing-connection-address-and-port). |
   |**Public network** |When you need to connect an instance via the public network, you need to make the following preparations:<br><br><br>1. Enable the public network access function of the SQL Server instance. For details, see [Enabling public network access](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/enabling-public-network-access).<br><br>2. Create a allowlist in the RDS for SQL Server and add the IP address of the local device to the allowlist. For more details, see [Creating allowlists](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/creating-allowlist).<br><br>3. Assiociate the allowlist to the target instance. For details, see [Associating allowlists to instances](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/associating-allowlist-to-instance).<br><br>4. Access the public network connection address of the SQL Server instance. For more information, see [View connection address and port](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/viewing-connection-address-and-port). |
   


<span id="rohMo2nL"></span>
## Connect to an instance via SSMS

[SQL Server Management Studio (SSMS)](https://learn.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms?spm=a2c63.p38356.879954.7.15df54088yM5PK&view=sql-server-2017) is a Graphical User Interface (GUI) tool for managing, configuring, monitoring, and developing all SQL Servers, primarily for configuring, monitoring, and managing SQL Server and database instances. This topic describes how to manage a RDS for SQL Server instance through a private or public connection in SSMS.

<span id="RCOWVGi0"></span>
### Precautions

SQL Server Management Studio (SSMS) only supports installation on Windows operating systems.

<span id="M05HJGdO"></span>
### Prerequisite

For more information, see [How to install SQL Server Management Studio](https://learn.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms?view=sql-server-ver16).

<span id="cmFZzLPB"></span>
### Operation steps


1. Start the SQL Server Management Studio client side on the ECS or local device.

2. Select **Connect ** \> **Database Engine** and configure the following login information in the **Connect to Server** pop\-up box.

   
   |**Parameter** |**Description** |
   |---|---|
   |**Server name** |The connection address of the target SQL Server instance. |
   |**Authentication** |Authentication method, select **SQL Server Authentication**. |
   |**Login name** |For the database account of the target SQL Server instance, the default administrator account is `veyun_user`. |
   |**Password** |The password for the database account of the SQL Server instance. |
   

3. Click **Connect** to connect the instance.


<span id="sfSESLBF"></span>
## **Connecting to a database through code**

The following describes sample code for connecting database instances in Python and C #.

<span id="jF1OCxOt"></span>
### Preparation

Install the corresponding language environment on demand according to the actual situation, as follows:


* [Python language](https://www.python.org/downloads/?spm=a2c4g.198933.0.0.7bd569bd2bLIh3)

* [Java languages](https://www.oracle.com/java/technologies/downloads/)

* C# language

   * Download and install [the. NET Framework or. NET Core](https://dotnet.microsoft.com/zh-cn/download).

   * Download and install [Visual Studio Code](https://visualstudio.microsoft.com/).


<span id="iZ7GUg4s"></span>
### Code example


* Python


```python
import pyodbc

# Build a connection
# SERVER specifies the address of the target SQL Server database server; DATABASE specifies the target database name for the connection; UID specifies the user name required to connect to the database, which defaults to veyun_user; PWD specifies the password required to connect to the database. 
conn_info = 'DRIVER={};DATABASE={};SERVER={};UID={};PWD={};TrustServerCertificate=yes'.format("ODBC Driver ** for SQL Server","master","mssqlf83eb5******.rds-mssql.ivolces.com","veyun_user","Admin*****")
conn = pyodbc.connect(conn_info)
cursor = conn.cursor()
cursor.execute('SELECT @@version')

rows = cursor.fetchall()

for row in rows:
    print(row)

# Close the connection 
conn.close()
```



* Java


```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;

public class SqlConnectionExample {
        public static void main(String[] args) {
            String connectionUrl = "jdbc:sqlserver://mssqlf83eb5******.rds-mssql.ivolces.com:1433;"
                    + "database=master;"
                    + "user=veyun_user;"
                    + "password=Admin*****;"
                    + "loginTimeout=30;";
    
            ResultSet resultSet;
            try (Connection connection = DriverManager.getConnection(connectionUrl);
                    Statement statement = connection.createStatement()) {
            
                    String selectSql = "SELECT @@version";
                    resultSet = statement.executeQuery(selectSql);
                    
                    while (resultSet.next()) {
                        System.out.println(resultSet.getString(1));
                    }
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }
}
```



* C#


```C#
using System;
using System.Data.SqlClient;

namespace SqlConnectionSSLExample
{
    class Program
    {
        static void Main(string[] args)
        {
            // Build a connection
            // Data Source specifies the address of the target SQL Server database server; Initial Catalog specifies the target database name for the connection; User ID specifies the user name required to connect to the database, which defaults to veyun_user; Password specifies the password required to connect to the database.  
            string connectionString = "Data Source=mssqlf83eb5******.rds-mssql.ivolces.com;Initial Catalog=master;User ID=veyun_user;Password=Admin*****;";
            using (SqlConnection connection = new SqlConnection(connectionString))
            {
                // establish connection 
                connection.Open();
                try
                {
                    SqlCommand cmd = new SqlCommand("SELECT @@version", connection);

                    string result = cmd.ExecuteScalar().ToString();

                    Console.WriteLine(result);
                }
                catch (Exception ex)
                {
                    Console.WriteLine($"Error: {ex.Message}");
                }
            }
        }
    }
}
```


<div data-tips="true" data-tips-type="tip">tip</div>


<div data-tips="true" data-tips-type="tip">Because the RDS hosting model provides a unified deployment architecture, some parameters may not be supported. You can configure appropriate connection parameters after actual verification according to your own business conditions. For details on specific parameters, please refer to Microsoft's <a href="https://learn.microsoft.com/en-us/dotnet/api/system.data.sqlclient.sqlconnection.connectionstring?view=dotnet-plat-ext-8.0&viewFallbackFrom=dotnet-plat-ext-8.0.">Official documentation</a>.</div>
