---
title: "Data dictionaries"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/docs-data-dictionaries"
---

The ByteHouse CDW data dictionary supports internally predefined dictionary content. This article explains how to create and use a data dictionary.

<span id="73e1feec"></span>
# Create dictionary tables

You can use DDL statements directly in the SQL workbench to create a dictionary table.

```SQL
CREATE DICTIONARY [IF NOT EXISTS] [db.]dictionary_name
(
    key1 type1  [DEFAULT|EXPRESSION expr1] [HIERARCHICAL|INJECTIVE|IS_OBJECT_ID],
    key2 type2  [DEFAULT|EXPRESSION expr2] [HIERARCHICAL|INJECTIVE|IS_OBJECT_ID],
    attr1 type2 [DEFAULT|EXPRESSION expr3],
    attr2 type2 [DEFAULT|EXPRESSION expr4]
)
PRIMARY KEY key1, key2
SOURCE(SOURCE_NAME([param1 value1 ... paramN valueN]))
LAYOUT(LAYOUT_NAME([param_name param_value]))
LIFETIME({MIN min_val MAX max_val | max_val})
```


<span id="291b4552"></span>
## Parameter


|Parameter name |Required |Description |
|---|---|---|
|IF NOT EXISTS |No |Optional keyword; no error is raised if a dictionary with the same name exists. |
|[db.]dictionary_name |is |Set the database to which the dictionary belongs and the dictionary name. |
|keyN typeN |Is |Dictionary key fields and types, used to uniquely identify entries.<br><br>Example: `key1 UInt64, key2 String` |
|DEFAULT |EXPRESSION expr |No |
|HIERARCHICAL |INJECTIVE |IS_OBJECT_ID<br><br><br>* HIERARCHICAL: Hierarchical relationship<br><br>* Injective: one\-to\-one mapping<br><br>* IS_OBJECT_ID: The object ID feature |
|attrN typeN |is |Dictionary attribute fields and types, storing associated data. |
|PRIMARY KEY key1, key2 |is |Specify which combinations of keys serve as the primary key. |
|SOURCE(SOURCE_NAME(...)) |is |Data source types and parameters: internal data sources are supported. For configuration details, see [Data source configuration example](https://docs.byteplus.com/docs/bytehouse/docs-data-dictionaries#2c4558c0). |
|LAYOUT(LAYOUT_NAME(...)) |Yes |Dictionary data storage layouts support flat, hashed, and other types. |
|LIFETIME({MIN min_val MAX max_val |max_val}) |is<br><br><br>* MIN: Minimum refresh interval (seconds)<br><br>* MAX: Maximum refresh interval (seconds) |


<span id="2c4558c0"></span>
## Data source configuration example

`SOURCE` The configuration details are as follows:

```SQL
SOURCE(CLICKHOUSE(
    user 'default'
    [db 'dbName']
    table 'ids'
    where 'id=10'
))
```


Parameter descriptions


* `user`: Fixed as default.

* `db`: Optional. The name of the database containing the data source table.

* `table`: The specific table name used as the data source.

* `where`: Optional. The SQL WHERE clause condition used to filter data from the source table.


<span id="d2bdbc0a"></span>
# Use a dictionary table

You can perform operations such as querying dictionary data, deleting data, querying dictionaries, and querying statements used to create dictionaries.

<span id="0bbd168f"></span>
## Query dictionary data

You can use certain functions to obtain information about dictionaries. For commonly used functions, refer to [ClickHouse community dictionary functions](https://clickhouse.com/docs/en/sql-reference/functions/ext-dict-functions).

For example, you can obtain data from the data dictionary by using the `dictGet` or `dictGetOrDefault` functions:

```SQL
dictGet('db.dict_name', 'attr_name', id_expr)
dictGetOrDefault('db.dict_name', 'attr_name', id_expr, default_value_expr)
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The format of the first parameter of the dictGet function must be similar to <code>db.dict_name</code>, because the dictionary cache uses this field for indexing.</div>


Check whether a key `id_expr` exists in the dictionary:

```SQL
dictHas('db.dict_name', id_expr)
```


<span id="37c8441b"></span>
## Delete dictionaries

After this operation is performed, ByteHouse will delete the record of this dictionary in the Catalog.

```SQL
DROP DICTIONARY [IF EXISTS] [db.]dictionary_name;
```


<span id="299c11cf"></span>
## Query dictionaries

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Executing <code>SHOW DICTIONARIES</code> requires the global <code>*.*</code> privilege of the AccountAdmin role. Please make sure you have this permission. To configure, please contact the administrator and refer to <a href="https://docs.byteplus.com/docs/bytehouse/docs-access-control-administration">Role management</a> to grant permissions.</div>


```SQL
SHOW DICTIONARIES [FROM <db>]; 
```


If the `FROM` clause is not specified, the query will return the list of dictionaries in the current database.

<span id="206b05f4"></span>
## Query statements for creating dictionaries

```SQL
SHOW CREATE DICTIONARY [db.] dictionary_name
```


This query returns a string column named "statement", whose value is the CREATE statement used to create the dictionary. For example:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9663f711a2b94d0d9759d939e6151e6e~tplv-goo7wpa0wc-image.image) </span>

<span id="4ac2e271"></span>
# Best practices: Create and use data dictionaries


1. Create a database.

   ```SQL
   Create Database test_db;
   ```
   

2. Create a data table.

   ```SQL
   CREATE TABLE `test_db`.`range_key_dictionary_source_table` (
       `key` UInt64,
       `start_date` Date,
       `end_date` Date,
       `value` String,
       `value_nullable` Nullable(String)
   )
   ENGINE = CnchMergeTree()
   PRIMARY KEY (`key`, `start_date`) 
   ORDER BY (`key`, `start_date`, `end_date`)
   COMMENT='demo';
   ```
   

3. Create a dictionary.

   ```SQL
   CREATE DICTIONARY test_db.range_key_dictionary
   (
     `key` UInt64,
     `start_date` Date,
     `end_date` Date,
     `value` String,
     `value_nullable` String
   )
   PRIMARY KEY `key`
   SOURCE(CLICKHOUSE(USER 'default' DB 'test_db' TABLE 'range_key_dictionary_source_table'))
   LIFETIME(MIN 10 MAX 20)
   LAYOUT(COMPLEX_KEY_HASHED());
   ```
   

4. Query the contents of the dictionary.

   ```SQL
   SHOW DICTIONARIES FROM test_db; 
   ```
   

   The following is an example of the output:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f9faf84581e74547bb321ca62026a143~tplv-goo7wpa0wc-image.image) </span>

5. (Optional) Delete the dictionary.

   ```SQL
   DROP dictionary test_db.range_key_dictionary;
   ```
