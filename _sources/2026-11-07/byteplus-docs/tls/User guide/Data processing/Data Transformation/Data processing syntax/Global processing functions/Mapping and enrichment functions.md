---
title: "Mapping and enrichment functions"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/mapping_and_enrichment_functions"
---

This document introduces the syntax, format, and related usage scenarios of the enriched mapping function.

<span id="lvybPxbp"></span>
## f_table_map function

The f_table_map function is used to map table data and returns the corresponding field value in the table according to the specified field name.

<span id="e3ac8f8f"></span>
### Function syntax and format

```SQL
f_table_map(value, field, output_fields, missing=None, mode="overwrite")
```


The parameters are described as follows:


|Parameter |Type |Required |Default Value |Description |
|---|---|---|---|---|
|value |String |Yes |/ |The target table.<br><br>When using resource function `res_rds_mysql` as a data source, to improve processing performance, please set the **primary_keys** parameters where possible. For detailed instructions, please refer to [res_rds_mysql function](https://docs.byteplus.com/en/docs/tls/Resource-functions). |
|field |String |Yes |/ |The source log field mapped to table data. Use half\-width commas (,) to separate multiple fields, such as `"id, age"`.<br><br>If no corresponding field exists in the log, the function performs no operation. |
|output_fields |String |Yes |/ |After mapping, the field to be output. Use half\-width commas (,) to separate multiple fields, such as `"name, desc"`. |
|missing |String |No |/ |The default value. If there is no matching field value, assign the value of the **missing** parameter to the **output_fields.**  |
|mode |String |No |overwrite |Override mode for the field. Include:<br><br><br>* Overwrite: When overwrite is selected, field values are overwritten.<br><br>* Fill: When the target field does not exist or the value is empty, you can choose fill to add a new field. |


<span id="8e66684b"></span>
### Sample function

<span id="30555740"></span>
#### Example 1


* Scenario: Mapping with the `table_tls` table in the BytePlus RDS for MySQL database `test_sql`, returning the values of the name and desc fields according to the id and age fields.

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
       "id,age",
       "name,desc"
   )
   ```
   

* Sample database data:

   
   |id |age |name |desc |
   |---|---|---|---|
   |1 |10 |zhangsan |Man out of law |
   |2 |18 |lisi |Hey man, what can i say! |
   

* Sample log:

   ```JSON
   [
   {
       "id":1,
       "age":10
   },
   {
       "id":2,
       "age":18
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
       "age":18,
       "name":"lisi",
       "desc":"Hey man, what can i say!"  
   }
   ]
   ```
   


<span id="42bd04c2"></span>
#### Example 2


* Scenario: Mapping with the table_tls table in the BytePlus RDS for MySQL database `test_sql`, returning the values of the name and desc fields according to the id and age fields, and setting the **missing** parameter to `unknown`.

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
       "id,age",
       "name,desc",
       missing='unknown'
   )
   ```
   

* Sample database data:

   
   |id |age |name |desc |
   |---|---|---|---|
   |1 |10 |zhangsan |Man out of law |
   

* Sample log:

   ```JSON
   [
   {
       "id":1,
       "age":10
   },
   {
       "id":2,
       "age":18
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
       "age":18,
       "name":"unknown",
       "desc":"unknown" 
   }
   ]
   ```
   


<span id=".Zi1kaWN0LW1hcC3lh73mlbA="></span>
## f_dict_map function

This function performs mapping based on a specified dictionary and maps an input field to a new field according to the mapping relationship.

<span id=".5Ye95pWw6K-t5rOVLeagvOW8jw=="></span>
### Function syntax and format

```python
f_dict_map(value=mapped dictionary,fields=mapped field,output_field=output fields,missing=default filled field,mode="fill")
```


The following table describes the parameters.


|Parameter |Type |Required |Default Value |Value Range |Description |
|---|---|---|---|---|---|
|value |Dict |Yes |/ |/ |Specify a string dictionary for mapping. Make sure the keys and values are in string format. |
|fields |String |Yes |/ |/ |Specify one or more field names. Separate field names with commas ( , ). When you specify multiple field names:<br><br><br>* Torch Log Service (TLS) maps the matched values in sequence.<br><br>* If multiple log data entries are matched and the value of the **mode** parameter is overwrite, the result last generated overwrites the previous results.<br><br>* If no fields are matched, the system uses the value of the **missing** parameter as that of output_field. |
|output_field |String |Yes |/ |/ |Specify the name of an output field. |
|missing |String |No |/ |/ |If the default field is not matched, the system assigns the value of this parameter to output_field. The default value is None. This value specifies that no values are assigned during mapping. |
|mode |String |No |overwrite |* overwrite<br><br>* fill |Specify how the value of an output field is overwritten.<br><br><br>* overwrite: performs overwriting under all circumstances by default.<br><br>* fill: sets the target field when it does not exist. |


<span id=".5Ye95pWw56S65L6L"></span>
### Sample function


* Scenario: The function maps the `status` field in log content to the `status_msg` field based on the mapping in dict.

* Transformation rule:

   ```python
   f_dict_map(dict_make("200","success","400","parameter exception"),"status","status_msg","unknown status")
   ```
   

* Sample log:

   ```json
   {
       "status": "200"
   }
   ```
   

* Transformation result:

   ```json
   {
       "status": "200",
       "status_msg": "success"
   }
   ```
