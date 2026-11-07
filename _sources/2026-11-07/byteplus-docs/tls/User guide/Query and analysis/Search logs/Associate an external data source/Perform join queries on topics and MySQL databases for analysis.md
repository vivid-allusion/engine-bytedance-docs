---
title: "Perform join queries on topics and MySQL databases for analysis"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Perform-join-queries-on-topics-and-MySQL-databases-for-analysis"
---

After you associate Torch Log Service (TLS) with MySQL data sources, you can perform join queries on topics and MySQL databases for analysis, and insert the query and analysis results into the MySQL databases. This topic describes how to perform a join query.

## Before you begin

Associate TLS with a MySQL data source, and make sure that Connection status is successful.

## Precautions

|Category |Description |
|---|---|
|MySQL table size |When you perform a join query, we recommend that the size of the associated MySQL table be less than 20 MiB. If the size is large, the database stability is reduced when TLS initiates a complex SQL query on the database. |
|Query and analysis statement |* When you perform a join query, specify the SQL analysis statement in the format of `query statement \| analysis statement`.<br><br>* Specify a data source name in the query and analysis statement. Do not use the MySQL table name directly. The back\-end service automatically replaces the data source name with the MySQL database name and table name during the query.<br><br>* In the query and analysis statement, the topic name must precede the JOIN keyword and the data source name must follow the JOIN keyword. |

## Procedure

1. Log on to the [TLS console](https://console.byteplus.com/tls).

2. In the top menu bar, select the region where TLS is deployed.

3. In the left\-side navigation pane, choose **Common functions** \> **Query and analysis**.

4. Select a project and a topic.

5. Specify a time range.

   The default time range is 5 minutes. You can change the time range as needed.

6. Type the query and analysis conditions to perform a join query.

   When you perform a join query, use the JOIN clause to associate a topic and an external data source. For information on the supported JOIN syntax, refer to [JOIN clause](https://docs.byteplus.com/docs/tls/JOIN-clause-2).

   > **tip**

   > Pay attention to the limits on the size of MySQL tables and SQL syntax when performing query and analysis. For more information, refer to [Precautions](https://docs.byteplus.com/docs/tls/Perform-join-queries-on-topics-and-MySQL-databases-for-analysis#ef43ea5c).

   For example, you have created an external MySQL data source named `tls_join_meta_store`, and you want to use the JOIN syntax to query data from a topic and a MySQL database. To achieve this, associate the data resources based on the **userid** field of the topic and the uid field of the specified data source to analyze the activeness of different age groups. The example of a join query is as follows:

   ```SQL
   * | 
   select 
     count(*) as pv 
    from myproject.mytopic l join tls_join_meta_store u on l.userid = u.uid 
   group by u.age 
   order by pv desc
   ```

7. Type the query statement and save the query results to the MySQL database.

   Use the INSERT syntax to save the query results to a table in the database. The SQL statement example is as follows. After the statement is executed, you can view the query results in the MySQL database.

   ```SQL
   * | insert into tls_report_external_store select __time__- __time__ % 300 as min, count(1) as pv group by min
   ```
