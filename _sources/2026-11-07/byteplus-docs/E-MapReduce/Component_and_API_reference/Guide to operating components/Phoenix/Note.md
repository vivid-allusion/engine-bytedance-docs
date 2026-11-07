---
title: "Note"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/phoenix_Note"
---

<span id="phoenix简介"></span>
# Introduction to Phoenix

Phoenix is an SQL layer built on HBase that allows us to use standard JDBC APIs, instead of HBase client APIs, to create tables, insert data, and query HBase data.

Phoenix is written entirely in Java and serves as an embedded JDBC driver for HBase. The Phoenix query engine translates SQL queries into one or more HBase scans and orchestrates their execution to produce a standard JDBC result set. When using the HBase API, coprocessors, and custom filters directly, simple queries typically perform at the millisecond level, while queries involving millions of rows perform at the second level.

<span id="phoenix执行方式"></span>
# Phoenix execution methods

<span id="批处理"></span>
## Batch processing


* Create a user_phoenix.sql file containing table creation information

   ```sql
   CREATE TABLE IF NOT EXISTS us_population (
        state CHAR(2) NOT NULL,
        city VARCHAR NOT NULL,
        population BIGINT
        CONSTRAINT my_pk PRIMARY KEY (state, city));
   ```
   

* Create a user_phoenix.csv data file containing the data to be inserted

   ```undefined
   NY,New York,8143197
   CA,Los Angeles,3844829
   IL,Chicago,2842518
   TX,Houston,2016582
   PA,Philadelphia,1463281
   AZ,Phoenix,1461575
   TX,San Antonio,1256509
   CA,San Diego,1255540
   TX,Dallas,1213825
   CA,San Jose,912332
   ```
   

* Create tables and write data using commands


```undefined
/usr/lib/emr/current/phoenix/bin/psql.py <your_zookeeper_quorum> us_population.sql us_population.csv
```


<span id="交互式"></span>
# Interactive mode


* Run commands to enter interactive mode


```undefined
/usr/lib/emr/current/phoenix/bin/sqlline.py <your_zookeeper_quorum>
```



* Perform SQL queries


```undefined
SELECT state as "State",count(city) as "City Count",sum(population) as "Population Sum"
FROM us_population
GROUP BY state
ORDER BY sum(population) DESC;
```
