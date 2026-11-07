---
title: "Connection instance"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Connection_instance"
---

This article describes how to connect to an EMR Serverless OLAP instance, using the StarRocks instance type as an example.

<span id="_1-前提条件"></span>
## 1 Prerequisites

A StarRocks instance has been created. For details, see Create an instance.

<span id="_2-通过客户端方式连接-starrocks-实例"></span>
## 2 Connect to a StarRocks instance using a client

Use the open\-source MYSQL client to connect to StarRocks. The procedure is as follows:

<span id="_2-1-下载-mysql-客户端并安装数据库"></span>
### 2.1 Download the MYSQL client and install the database


1. [MySQL client download](https://dev.mysql.com/downloads/mysql/5.7.html#downloads).

2. Extract the installation package.

   ```shell
   tar -zxvf mysql-xxx.tar.gz
   ```
   

3. Copy the extracted MySQL directory to the local software directory.

   ```shell
   cp mysql-xxx /usr/local/mysql -r
   ```
   

4. Add the system MySQL user group and MySQL user.

   ```shell
   sudo groupadd mysql
   sudo useradd -r -g mysql mysql
   ```
   

5. Install the database.

   1. Go to the MySQL software installation directory.

      ```shell
      cd /usr/local/mysql
      ```
      

   2. Change the ownership of the current directory to the MySQL user and MySQL user group.

      ```shell
      chown -R mysql:mysql ./
      ```
      

   3. Install the database.

      ```shell
      ./bin/mysql_install_db --user=mysql
      ```
      

      You can also perform initialization operations at the same time:

      ```shell
      sudo bin/mysqld --initialize --user=mysql
      ```
      

   4. Change the ownership of the current directory to the root user.

      ```shell
      chown -R root:root ./
      ```
      

   5. Change the ownership of the current data directory to the MySQL user.

      ```shell
      chown -R mysql:mysql data
      ```
      

   6. Copy files.

      ```shell
      cp /usr/local/mysql/support-files/mysql.server /etc/init.d/mysql
      ```
      

6. Start the MySQL service.

   ```shell
   sudo service mysql start
   ```
   


<span id="_2-2-连接-starrocks-实例"></span>
### 2.2 Connect to the StarRocks instance


1. Connect to the StarRocks instance

   ```shell
   /usr/local/mysql/bin/mysql -u admin -p -h xxx.cdw.emr-volces.com -P 9030
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">xxx.cdw.emr\-volces.com is the internal address of StarRocks. You can view it in the <strong>Instance details \> Network information</strong> section of StarRocks.   </div>
   

<span id="_3-通过-jdbc-方式连接-starrocks-实例"></span>
## 3 Connect to the StarRocks instance using JDBC


1. Add the dependency to pom.xml

   ```xml
   <!-- https://mvnrepository.com/artifact/mysql/mysql-connector-java -->
   <dependency>
       <groupId>mysql</groupId>
       <artifactId>mysql-connector-java</artifactId>
       <version>8.0.33</version>
   </dependency>
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">mysql\-connector\-java is the MYSQL Driver version. You can modify it according to actual conditions.   </div>
   

2. Connect to the StarRocks instance.

   The sample code is as follows:

   ```java
   public class EmrStarrocks {
       public static void main(String[] args) {
           Connection connection = null;
           Statement statement = null;
           
           // The database connection information, username, and password must be set according to actual conditions.
           String url = "jdbc:mysql://localhost:9030/database?useUnicode=true";
           String user = "user";
           String password = "password";
           try{
               // Register the JDBC driver. The driver name must be set according to actual conditions.
               Class.forName("com.mysql.jdbc.Driver");
   
               // Obtain the connection.
               conn = DriverManager.getConnection(url, user, password);
   
               // Execute the query.
               statement = conn.createStatement();
               String sql = "SELECT id FROM people";
               ResultSet result = statement.executeQuery(sql);
               
               // Close resources.
               result.close();
               statement.close();
               connection.close();
           }catch(SQLException se){
               // Handle JDBC errors.
           }catch(Exception e){
               // Handle other errors.
           }finally{
               // Close resources.
               if(statement!=null) {
                   statement.close();
               }
               if(connection!=null) {
                   connection.close();
               }
           }
       }        
   }
   ```
