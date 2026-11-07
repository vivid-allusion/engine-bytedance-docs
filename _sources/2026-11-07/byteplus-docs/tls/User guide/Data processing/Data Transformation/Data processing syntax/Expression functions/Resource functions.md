---
title: "Resource functions"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Resource-functions"
---

This topic describes the syntax format and typical examples of resource functions.

<span id="416383b0"></span>
## res_rds_mysql function

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The upper limit for data retrieval is 200,000 records, and any data exceeding this limit will be truncated.</div>


The res_rds_mysql function is used to pull table data from BytePlus RDS for MySQL database and self\-built public MySQL database. The following three pull methods are supported:


|pull mode |explain |
|---|---|
|normal pull mode |When the transformation task is executed for the first time, TLS will pull the full amount of table data and will not pull it later. If the data in your database is not continuously updated, you can choose the normal pull mode. |
|full update mode |During the execution of a transformation task, TLS will periodically pull the full amount of table data once. Each time the full amount is pulled, it is very time\-consuming. If the amount of data in your database is less than or equal to 2 GB and the value of the refresh_interval parameter is greater than or equal to 300 seconds, you can choose the full update mode. |
|incremental update mode |During the execution of a transformation task, TLS periodically pulls new data based on the timestamp field in the database table. In the incremental update mode, TLS only pulls new data each time, which is efficient. You can also set the refresh_interval parameter to 10 seconds to synchronize data in the database table at the second level with high immediacy. If you have a large amount of data in your database tables, updates are frequent, and you have high data real\-time requirements, you can choose the incremental update mode. |


<span id="d4a71906"></span>
### Function syntax/formatting

```Python
res_rds_mysql(host="The address of the database",port="The port of the database", username="The username used to connect to the database", password="The password used to connect to the database", database="The name of the database", table="The name of the table", vpc=None, fields=None, include_fields=None, exclude_fields=None,primary_keys=None, refresh_interval=0, update_time_key=None,base_retry_back_off=1, max_retry_back_off=60)
```


The parameters are described as follows:


|Parameter |Type |Required |Default Value |Description |
|---|---|---|---|---|
|host |String |Yes |/ |MySQL instance domain name, currently supports BytePlus cloud database MySQL version and self\-built public network database.<br><br>When using BytePlus Cloud Database MySQL Edition, set the **host** to the IP address of the VPC to which the MySQL instance belongs. You can view the IP address of the target VPC on its overview page. For details, please refer to [View Private Network Details](https://www.volcengine.com/docs/6401/69156). |
|port |String |Yes |/ |The port of the database. |
|username |String |Yes |/ |The username used to connect to the database. |
|password |String |Yes |/ |The password used to connect to the database. |
|database |String |Yes |/ |The name of the database. |
|table |String |Yes |/ |The name of database table. |
|vpc |String |No |/ |When using BytePlus RDS for MySQL, you need to configure the VPC ID used by the MySQL instance, such as `vpc-2byx ****`. |
|fields |String |No |All fields |The List of strings or string aliases to be pulled. If left blank, all columns returned by the table parameter are used by default. Use half\-width commas (,) when specifying multiple fields, such as `field1, field2`. |
|include_fields |String |No |/ |The field whitelist. The table data matching the include_fields is pulled and the rest is discarded. Single field names and values are joined with a half\-width colon (:), and multiple fields are separated by a half\-width comma (,), such as `field1: value1, field2: value2`. |
|exclude_fields |String |No |/ |The field blacklist, The table data matching the exclude_fields is discarded and the rest is pulled. Single field names and values are concatenated with colons (:), and multiple fields are separated by commas (,), such as `field1: value1, field2: value2`.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If you set both <code>include_fields</code> and <code>exclude_fields</code> parameters, the system preferentially matches <code>include_fields</code> parameters and then <code>exclude_fields</code> parameters.</div><br> |
|primary_keys |String |No |/ |Primary Key. After configuring this parameter, the data in the table will be pulled as key: Value in dictionary form and saved to memory. The key is the value of the primary_keys parameter, and the value is the entire row of data pulled into the table.<br><br><br>* When the amount of data in the table is large, it is recommended to use this parameter to improve efficiency.<br><br>* The value of the primary_keys parameter must exist in the field pulled from the data table. |
|update_time_key |String |No |/ |Used for incremental data retrieval. For example `update_time_key = "update_time"`, where `update_time` is the updated time field of the data in the MySQL database, which supports the Datetime, Timestamp data types. Please ensure that the value of this time field increases over time.<br><br>If this parameter is not configured, TLS will perform a full update.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Data transformation filters data based on this time field to achieve incremental updates. Ensure that the field is indexed in the data table; otherwise, a full table scan will be performed, which significantly affects performance.</div><br> |
|refresh_interval |Int |No |0 |The time interval between pulling data from the MySQL database, in seconds. The default value is 0, indicating that the full amount is pulled only once. |
|base_retry_back_off |Int |No |1 |The time interval for re\-pulling after failure to pull data, the default value is 1, in seconds. |
|max_retry_back_off |Int |No |60 |The maximum time interval to retry a request after a failed data pull. The default value is 60, in seconds. It is recommended to use the default value. |


<span id="8e31ee48"></span>
### Example

<span id="1a5ccc29"></span>
#### Example 1: All data is pulled every 300 seconds


* Scenario: Pull summary table data from `table_tls` table in BytePlus RDS for MySQL database `test_sql` every 300 seconds.

* Transformation rule:

   ```Python
   res_rds_mysql(
       host="192.168.**.**",
       port="3306",
       username="test_username",
       password="****",
       database="test_sql",
       vpc="vpc-xxxxx",    
       table="table_tls",
       refresh_interval=300
   )
   ```
   


<span id="43ab4e07"></span>
#### Example 2: Specify a black and white list for data pulling


* Scenario: Pull data from the `table_tls` table in the BytePlus RDS for MySQL database `test_sql`, and specify that only retrieve data where the **size** field value is `400` and the **method** field value is not `put`.

* Processing rules:

   ```Python
   res_rds_mysql(
       host="192.168.**.**",
       port="3306",
       username="test_username",
       password="****",
       database="test_sql",
       vpc="vpc-xxxxx",    
       table="table_tls",
       refresh_interval=300,
       include_fields='size:400',
       exclude_fields='method:put'
   )
   ```
   


<span id="e90a7239"></span>
#### Example 3: Pull data using primary key mode


* Scenario: Use the primary key schema to pull data from `table_tls` tables in the BytePlus RDS for MySQL database `test_sql`.

* Processing rules:

   ```Python
   f_table_map(
       res_rds_mysql(
           address="192.168.**.**",
           username="test_username",
           password="****",
           database="test_sql",
           vpc="vpc-xxxxx",    
           table="table_tls",
           primary_keys="id",
       ),
       "id",
       ["name", "desc"],
   )
   ```
   

* database data

   
   |id |name |desc |
   |---|---|---|
   |1 |zhangsan |Man out of law |
   

* Sample log:

   ```JSON
   [
   {
       "id":1,
       "age":10
   },
   {
       "id":2,
       "age":20
   }
   ]
   ```
   

* Processing result:

   ```JSON
   [
   {
       "id":1,
       "age":10,
       "name":"zhangsan",
       "desc":"Man out of law"    
   },
   {
       "id":2,
       "age":20
   }
   ]
   ```
   


<span id="364181cb"></span>
#### Example 4: Pull data using incremental update mode


* Scenario: Use incremental update mode to pull data from `table_tls` tables in the BytePlus RDS for MySQL database `test_sql`.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">When using incremental update mode to pull data, the following conditions must be met:   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The data database table must have a unique primary key and a time field, such as id and update_time in the example.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">When you use incremental update mode to pull data, you must set the primary_keys, refresh_interval, and update_time_key parameters in the function.   </div>
   

* Processing rules:

   ```Python
   f_table_map(
       res_rds_mysql(
           address="192.168.**.**",
           username="test_username",
           password="****",
           database="test_sql",
           vpc="vpc-xxxxx",    
           table="table_tls",
           primary_keys="id",
           update_time_key="update_time",
           refresh_interval=10    
       ),
       "id",
       ["name", "desc"],
   )
   ```
   

* database data

   
   |id |name |desc |update_time |
   |---|---|---|---|
   |1 |zhangsan |Man out of law |2024\-07\-08 14:23:14 |
   |2 |lisi |Hey man, what can i say! |2024\-07\-08 14:23:15 |
   

* Sample log:

   ```JSON
   [
   {
       "id":1,
       "age":10
   },
   {
       "id":2,
       "age":20
   }
   ]
   ```
   

* Processing result:

   ```JSON
   [
   {
       "id":1,
       "age":10,
       "name":"zhangsan",
       "desc":"Man out of law"    
   },
   {
       "id":2,
       "age":20，
       "name":"lisi",
       "desc":"Hey man, what can i say!"       
   }
   ]
   ```
