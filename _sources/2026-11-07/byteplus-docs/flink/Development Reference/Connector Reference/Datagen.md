---
title: "Datagen"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/Datagen"
---

When you need to verify whether the work can operate normally and the logic is correct, in order to reduce external system overhead and avoid interference factors, you can choose to use some debugging\-specific connectors.

Datagen connector is a debugging\-specific source table built into the system. It periodically generates random data and can be directly referred to as a data source.

<span id="68b222bc"></span>
## DDL Definition

```sql
CREATE TABLE datagen_source (
    name String,
    score INT
 ) WITH (
     'connector' = 'datagen',
     'rows-per-second' = '5'   
 );
```


<span id="24845079"></span>
## WITH Parameters


|**Parameters** |**Required** |**Default Value** |**Data Type** |**Description** |
|---|---|---|---|---|
|connector |Is |(none) |String |Specifies the connector to use, which in this case is the Datagen connector. |
|rows\-per\-second |No |10000 |Long |The number of random numbers generated per second. |
|fields.#.kind |No |random |String |Specify the method for generating random numbers:<br><br><br>* random: Default, represents an unbounded random number generator, where you can specify the maximum and minimum values for the random numbers generated.<br><br>* sequence: A bounded sequence generator, where you can specify the start and end values of the sequence. Once the sequence reaches the end value, no more numbers are generated. |
|fields.#.min |No |(Minimum value of type) |(Type of field) |The minimum value of random numbers, suitable for numeric types. |
|fields.#.max |No |(Maximum value of type) |(Type of field) |The maximum value of random numbers, suitable for numeric types. |
|fields.#.length |No |100 |Integer |Length of randomly generated characters, applicable to char, varchar, string types. |
|fields.#.start |No |(none) |(Type of field) |Starting value of sequential data. |
|fields.#.end |No |(none) |(Type of field) |The end value of sequence data. |


<span id="4483c968"></span>
## Sample Code

```sql
CREATE TABLE datagen_source (
     siteid INT,
     citycode SMALLINT,
     username STRING,
     pv BIGINT
     )
WITH (
  'connector' = 'datagen',
  'rows-per-second' = '5',                
  'fields.username.length' = '30',            
  'fields.siteid.max' = '1000',   
  'fields.siteid.min' = '100'        
);
CREATE TABLE print_sink (
    siteid INT,
    citycode SMALLINT,
    username STRING,
    pv BIGINT
    )
WITH (
     'connector' = 'print',
     'print-identifier' = 'out'            
);
insert into print_sink
select * from datagen_source;
```
