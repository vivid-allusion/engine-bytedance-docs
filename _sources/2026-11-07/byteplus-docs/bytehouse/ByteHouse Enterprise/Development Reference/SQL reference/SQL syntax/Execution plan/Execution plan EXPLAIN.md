---
title: "Execution plan EXPLAIN"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/execution-plan-explain"
---

<span id="c62912c3"></span>
# EXPLAIN


* Show the logical execution plan

* json = 1 Print the plan in JSON format

* stats=1 Output statistics including row count and cost, default 1

* verbose =1 Output detailed content of the logical plan, default 1


```SQL
EXPLAIN json=0
SELECT
    l_returnflag,
    l_linestatus,
    sum(l_quantity) AS sum_qty,
    sum(l_extendedprice) AS sum_base_price,
    sum(l_extendedprice * (1 - l_discount)) AS sum_disc_price,
    sum((l_extendedprice * (1 - l_discount)) * (1 + l_tax)) AS sum_charge,
    avg(l_quantity) AS avg_qty,
    avg(l_extendedprice) AS avg_price,
    avg(l_discount) AS avg_disc,
    count(*) AS count_order
FROM lineitem
WHERE l_shipdate <= (toDate('1998-12-01') - toIntervalDay('90'))
GROUP BY
    l_returnflag,
    l_linestatus
ORDER BY
    l_returnflag ASC,
    l_linestatus ASC
```


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/722b9c6c41204ab9bea1b3c084efbc3d~tplv-goo7wpa0wc-image.image" width="3790px" /></div>


<span id="d39ad8de"></span>
# EXPLAIN DISTRIBUTED


* Show the distributed execution plan

* json = 1 Print the plan in JSON format

* stats=1 Output statistics including row count and cost, default 1

* verbose =1 Outputs the detailed contents of logical plan nodes by default 1


```SQL
EXPLAIN DISTRIBUTED json=0
SELECT
    l_returnflag,
    l_linestatus,
    sum(l_quantity) AS sum_qty,
    sum(l_extendedprice) AS sum_base_price,
    sum(l_extendedprice * (1 - l_discount)) AS sum_disc_price,
    sum((l_extendedprice * (1 - l_discount)) * (1 + l_tax)) AS sum_charge,
    avg(l_quantity) AS avg_qty,
    avg(l_extendedprice) AS avg_price,
    avg(l_discount) AS avg_disc,
    count(*) AS count_order
FROM lineitem
WHERE l_shipdate <= (toDate('1998-12-01') - toIntervalDay('90'))
GROUP BY
    l_returnflag,
    l_linestatus
ORDER BY
    l_returnflag ASC,
    l_linestatus ASC
```


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e20ab138b1be48cf9f53e14d2fffc48d~tplv-goo7wpa0wc-image.image" width="2128px" /></div>


<span id="c34c01ee"></span>
# EXPLAIN ANALYZE

Explain analyze general setting

json = 1 Prints the plan in Json format, default 0

stats=1 Outputs statistics of row counts and cost, default 1

profile =1 Outputs execution time profiles, default 1

verbose =1 Outputs the detailed contents of logical plan nodes, default 1

<span id="3ec53973"></span>
## EXPLAIN ANALYZE


* Show the execution plan with runtime information

* json = 1 Prints the plan in JSON format


```SQL
EXPLAIN ANALYZE json=0
SELECT
    l_returnflag,
    l_linestatus,
    sum(l_quantity) AS sum_qty,
    sum(l_extendedprice) AS sum_base_price,
    sum(l_extendedprice * (1 - l_discount)) AS sum_disc_price,
    sum((l_extendedprice * (1 - l_discount)) * (1 + l_tax)) AS sum_charge,
    avg(l_quantity) AS avg_qty,
    avg(l_extendedprice) AS avg_price,
    avg(l_discount) AS avg_disc,
    count(*) AS count_order
FROM lineitem
WHERE l_shipdate <= (toDate('1998-12-01') - toIntervalDay('90'))
GROUP BY
    l_returnflag,
    l_linestatus
ORDER BY
    l_returnflag ASC,
    l_linestatus ASC
```


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c3f2669fc5c14ebbb3a45ceb6d421391~tplv-goo7wpa0wc-image.image" width="2160px" /></div>


<span id="6b4ec837"></span>
## EXPLAIN ANALYZE DISTRIBUTED


* Show the distributed execution plan with runtime information

* json = 1 Print the plan in JSON format

* [Description of the Explain Analyze Field](https://docs.byteplus.com/docs/bytehouse/description-of-the-explain-analyze-field)


```SQL
EXPLAIN ANALYZE DISTRIBUTED  json=0
SELECT
    l_returnflag,
    l_linestatus,
    sum(l_quantity) AS sum_qty,
    sum(l_extendedprice) AS sum_base_price,
    sum(l_extendedprice * (1 - l_discount)) AS sum_disc_price,
    sum((l_extendedprice * (1 - l_discount)) * (1 + l_tax)) AS sum_charge,
    avg(l_quantity) AS avg_qty,
    avg(l_extendedprice) AS avg_price,
    avg(l_discount) AS avg_disc,
    count(*) AS count_order
FROM lineitem
WHERE l_shipdate <= (toDate('1998-12-01') - toIntervalDay('90'))
GROUP BY
    l_returnflag,
    l_linestatus
ORDER BY
    l_returnflag ASC,
    l_linestatus ASC
```


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/67b252cbf2fb4822b2ce991da518bcb0~tplv-goo7wpa0wc-image.image" width="2160px" /></div>


<span id="47955e24"></span>
## EXPLAIN ANALYZE PIPELINE


* Show the physical execution plan with runtime information. This function, on the basis of explain pipeline, adds execution information. Print the specific execution information for each processor

* aggregate_profiles = 1 Print the aggregated profile of each worker, =0 Print the profiles of each worker separately

* json = 1 Print the plan in JSON format


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/df9efde9b8cf4c5bb1d33d67b9f43f8d~tplv-goo7wpa0wc-image.image" width="1960px" /></div>


<span id="ea373ae1"></span>
# EXPLAIN AST


* Show the generated AST structure


```SQL
EXPLAIN AST
SELECT
    l_returnflag,
    l_linestatus,
    sum(l_quantity) AS sum_qty,
    sum(l_extendedprice) AS sum_base_price,
    sum(l_extendedprice * (1 - l_discount)) AS sum_disc_price,
    sum((l_extendedprice * (1 - l_discount)) * (1 + l_tax)) AS sum_charge,
    avg(l_quantity) AS avg_qty,
    avg(l_extendedprice) AS avg_price,
    avg(l_discount) AS avg_disc,
    count(*) AS count_order
FROM lineitem
WHERE l_shipdate <= (toDate('1998-12-01') - toIntervalDay('90'))
GROUP BY
    l_returnflag,
    l_linestatus
ORDER BY
    l_returnflag ASC,
    l_linestatus ASC
```


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2e295e164a9841ccb9c6294838957140~tplv-goo7wpa0wc-image.image" width="916px" /></div>


<span id="4988b041"></span>
# EXPLAIN SYNTAX


* Show the SQL after optimizer rewrite


```SQL
EXPLAIN SYNTAX
SELECT
    l_returnflag,
    l_linestatus,
    sum(l_quantity) AS sum_qty,
    sum(l_extendedprice) AS sum_base_price,
    sum(l_extendedprice * (1 - l_discount)) AS sum_disc_price,
    sum((l_extendedprice * (1 - l_discount)) * (1 + l_tax)) AS sum_charge,
    avg(l_quantity) AS avg_qty,
    avg(l_extendedprice) AS avg_price,
    avg(l_discount) AS avg_disc,
    count(*) AS count_order
FROM lineitem
WHERE l_shipdate <= (toDate('1998-12-01') - toIntervalDay('90'))
GROUP BY
    l_returnflag,
    l_linestatus
ORDER BY
    l_returnflag ASC,
    l_linestatus ASC
```


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/817ca1422a8c4c54b5877fb005b90d43~tplv-goo7wpa0wc-image.image" width="1402px" /></div>


<span id="365ec1b1"></span>
# EXPLAIN TRACE_OPT


* Print the optimizer execution time


```SQL
EXPLAIN TRACE_OPT
SELECT
    l_returnflag,
    l_linestatus,
    sum(l_quantity) AS sum_qty,
    sum(l_extendedprice) AS sum_base_price,
    sum(l_extendedprice * (1 - l_discount)) AS sum_disc_price,
    sum((l_extendedprice * (1 - l_discount)) * (1 + l_tax)) AS sum_charge,
    avg(l_quantity) AS avg_qty,
    avg(l_extendedprice) AS avg_price,
    avg(l_discount) AS avg_disc,
    count(*) AS count_order
FROM lineitem
WHERE l_shipdate <= (toDate('1998-12-01') - toIntervalDay('90'))
GROUP BY
    l_returnflag,
    l_linestatus
ORDER BY
    l_returnflag ASC,
    l_linestatus ASC
```


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2294dd67d12140eda3cb42f80f0db930~tplv-goo7wpa0wc-image.image" width="814px" /></div>


<span id="4596f3f5"></span>
# EXPLAIN TRACE_OPT RULE


* Print the optimizer execution time, including the execution time of each rule with the RULE keyword.


```SQL
EXPLAIN TRACE_OPT RULE
SELECT
    l_returnflag,
    l_linestatus,
    sum(l_quantity) AS sum_qty,
    sum(l_extendedprice) AS sum_base_price,
    sum(l_extendedprice * (1 - l_discount)) AS sum_disc_price,
    sum((l_extendedprice * (1 - l_discount)) * (1 + l_tax)) AS sum_charge,
    avg(l_quantity) AS avg_qty,
    avg(l_extendedprice) AS avg_price,
    avg(l_discount) AS avg_disc,
    count(*) AS count_order
FROM lineitem
WHERE l_shipdate <= (toDate('1998-12-01') - toIntervalDay('90'))
GROUP BY
    l_returnflag,
    l_linestatus
ORDER BY
    l_returnflag ASC,
    l_linestatus ASC
```


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e202c39dd92a42e582d8c4b04c6b1f23~tplv-goo7wpa0wc-image.image" width="1028px" /></div>


<span id="64871731"></span>
# EXPLAIN METADATA


* Show the results of QueryAnalyzer: The names of columns, tables, and databases used in the query statement

* json = 1 Print the plan in JSON format


```SQL
EXPLAIN METADATA json = 0
SELECT
    l_returnflag,
    l_linestatus,
    sum(l_quantity) AS sum_qty,
    sum(l_extendedprice) AS sum_base_price,
    sum(l_extendedprice * (1 - l_discount)) AS sum_disc_price,
    sum((l_extendedprice * (1 - l_discount)) * (1 + l_tax)) AS sum_charge,
    avg(l_quantity) AS avg_qty,
    avg(l_extendedprice) AS avg_price,
    avg(l_discount) AS avg_disc,
    count(*) AS count_order
FROM lineitem
WHERE l_shipdate <= (toDate('1998-12-01') - toIntervalDay('90'))
GROUP BY
    l_returnflag,
    l_linestatus
ORDER BY
    l_returnflag ASC,
    l_linestatus ASC
```


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4b7fe12e671a4e61b61e3561b2da8764~tplv-goo7wpa0wc-image.image" width="3792px" /></div>
