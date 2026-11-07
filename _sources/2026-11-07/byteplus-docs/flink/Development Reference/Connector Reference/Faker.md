---
title: "Faker"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/Faker"
---

The Faker connector can generate test data based on the Java Faker expressions of the fields in the table, commonly used to validate the correctness of business logic, and supports being used as both source and dimension tables.

<span id="5d6d192c"></span>
## Usage Limitations


* The Faker connector only supports data types such as CHAR, VARCHAR, STRING, TINYINT, SMALLINT, INTEGER, BIGINT, FLOAT, DOUBLE, DECIMAL, BOOLEAN, TIMESTAMP, DATE, TIME, ARRAY, MAP, MULTISET, and ROW.

* The Faker connector currently only supports use in the **Flink 1.11\-volcano** engine version.


<span id="fe32d82c"></span>
## DDL Definitions

```SQL
CREATE TABLE faker_source (
   name STRING,
   age INT
)  WITH (
  'connector' = 'faker',
  'fields.name.expression' = '#{superhero.name}',
  'fields.age.expression' = '#{number.numberBetween ''0'',''100''}'
);
```


<span id="18233593"></span>
## WITH Parameters


|**Parameter** |**Is it mandatory?**  |**Default Value** |**Data Type** |**Description** |
|---|---|---|---|---|
|connector |is |(none) |String |Specifies the connector to be used, here is the faker connector. |
|fields..expression |is |(none) |String |Generate test data based on the Java Faker expression for the field. For more details, please see[字段表达式](https://docs.byteplus.com/docs/flink/45794#235f59d6). |
|fields..null\-rate |No |0.0 |Float |The proportion of the field being empty. |
|fields..length |No |1 |Integer |Size of ARRAY, MAP, or MULTISET collections. |
|number\-of\-rows |No |\-1 |Integer |Parameter specific to the source table, indicating the number of data rows generated.<br><br>If the parameter is set, it indicates that the Faker source table is bounded; the default value \-1 indicates the source table is unbounded. |
|rows\-per\-second |No |10000 |Integer |Parameters specific to the source table, indicating the rate of data generation, i.e., how many data items are generated per second. |


<span id="a3af4c33"></span>
## Sample Code


* Source Table Example

   ```SQL
   CREATE TEMPORARY TABLE faker_source (
     name STRING,
     age INT
   ) WITH (
     'connector' = 'faker',
     'fields.name.expression' = '#{superhero.name}',
     'fields.age.expression' = '#{number.numberBetween ''0'',''100''}',
     'rows-per-second' = '10'
   );
   
   CREATE TEMPORARY table print_sink(
     name STRING,
     age INT
   ) WITH (
     'connector' = 'print'
   );
   
   INSERT INTO print_sink 
   SELECT * FROM faker_source;
   ```
   

* Dimension Table Example

   ```SQL
   CREATE TABLE datagen_source (
     character_id1 INT,
     location STRING,
     proctime AS PROCTIME()
   )
   WITH (
     'connector' = 'datagen'
   );
   
   
   CREATE TABLE faker_lookup (
     character_id INT,
     name STRING
   )
   WITH (
     'connector' = 'faker', 
     'fields.character_id.expression' = '#{number.numberBetween ''0'',''100''}',
     'fields.name.expression' = '#{harry_potter.characters}'
   );
   
   
   create table print_sink (
     character_id INT,
     location STRING,
     name STRING
     )
   with
     ('connector' = 'print');
   
   
   insert into print_sink
   SELECT 
     faker_lookup.character_id,
     datagen_source.location,
     faker_lookup.name
   FROM datagen_source
   LEFT JOIN faker_lookup FOR SYSTEM_TIME AS OF datagen_source.proctime
   ON datagen_source.character_id1 = faker_lookup.character_id;
   ```
   


<span id="235f59d6"></span>
## Field Expression

When using the Faker connector, each field in the table requires a fixed Java Faker expression to generate data, styled as

`'fields.<field>.expression' = '#{className.methodName ''parameter'', ...}'`。

The variables in the expression are explained as follows:


* `<field>`: The field name in the table.

* `className`: Class provided by the Faker connector. Java Faker currently provides more than 80 classes for generating the field expressions you need, please choose as needed. For more information on Faker classes, please see [Faker Class](https://github.com/DiUS/java-faker/#fakers).

* `methodName`: Method name.

* `parameter`: The input parameter of the method.


**Example** (Fill in field expression):

Choose `'fields.age.expression' = '#{number.numberBetween '0','100'}'` from the example code to introduce the field expression filling process.


1. In Java Faker, find the target class, see [All Classes of Java Faker](http://dius.github.io/java-faker/apidocs/index.html).

2. Locate and click on the target class (Number), then find the required method name and read the related description.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8f470889a962450292890be1c9ba7f1e~tplv-goo7wpa0wc-image.image) </span>

3. Fill in the field expression based on class and method.

   `'fields.age.expression' = '#{number.numberBetween '0','100'}'` expression means: the age field in the table ranges from [0, 100].
