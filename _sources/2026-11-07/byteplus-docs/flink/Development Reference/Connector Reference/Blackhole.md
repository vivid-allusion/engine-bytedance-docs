---
title: "Blackhole"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/Blackhole"
---

When you need to validate if tasks can operate normally and the logic is correct, to minimize the overhead of external systems and avoid interference, you can opt to use some debugging\-specific connectors.

The Blackhole connector is a system\-built, debugging\-specific results table primarily used for high\-performance testing, but it does not print data in the Stdout result logs.

<span id="e750289d"></span>
## DDL Definition

```sql
CREATE TABLE blackhole_sink (
    name String,
    score INT
 ) WITH (
     'connector' = 'blackhole'
 );
```


<span id="99e63981"></span>
## WITH Parameters


|**Parameters** |**Required** |**Default Value** |**Data Type** |**Description** |
|---|---|---|---|---|
|connector |Is |(none) |String |Specifies the connector to be used, here it is the Blackhole connector. |


<span id="545a433a"></span>
## Example Code

The following example demonstrates: Using the Datagen connector to generate random numbers, selecting partial data for output, with no logs printed in the results.

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
CREATE TABLE blackhole_sink (
    citycode SMALLINT,
    username STRING,
    pv BIGINT
    )
WITH (
     'connector' = 'blackhole'           
);
insert into blackhole_sink
select
    citycode,
    username,
    pv
from
    datagen_source;
```
