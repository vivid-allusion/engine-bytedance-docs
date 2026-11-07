---
title: "ANSI compatibility"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/docs-ansi-compatibility"
---

<span id="f3063557"></span>
## Data Types

<span id="d9e6be07"></span>
##### Default Types Can Be Null

The default data type cannot be null in the default mode. However, the ANSI standard requires that it can be null.


|**Query example**<br><br>```SQL```<br>```SELECT value, changed FROM system.settings WHERE name LIKE '%dialect_type%';```<br> ||
|---|---|
|Output in the default mode:<br><br>0, 0 |Output in ANSI mode:<br><br>1, 1 |


<span id="850257f1"></span>
##### Time Type with Timezone

Added Time data type.

The time data type supporting time zones is an ANSI SQL standard, supported by MySQL and PostgreSQL. The format of the time data type is hh:mm:ss[.nnnnnnn]. It is internally represented as Int64. Its precision uses scale as a parameter. The maximum value of Scale is 9, which equals the number of digits after the decimal point; the default value is 3.

Query example: Example using the Time data type function.

```SQL
select toHour('11:20:30'::Time);
select Hour('11:20:30'::Time);
select toMinute('11:20:30'::Time);
select Minute('11:20:30'::Time);
select toSecond('11:20:30'::Time);
select Second('11:20:30'::Time);
select addYears('11:20:30'::Time(3), 5);
select addYears('11:20:30'::Time(4), 20);
select subtractYears('11:20:30'::Time(5), 5);
select subtractYears('11:20:30'::Time(6), 20);
select addMonths('11:20:30'::Time(3), 5);
select addMonths('11:20:30'::Time(4), 20);
select subtractMonths('11:20:30'::Time(5), 5);
select subtractMonths('11:20:30'::Time(6), 20);
select addDays('11:20:30'::Time(3), 5);
select addDays('11:20:30'::Time(4), 20);
select subtractDays('11:20:30'::Time(5), 5);
select subtractDays('11:20:30'::Time(6), 20);
select addHours('11:20:30'::Time(3), 5);
select addHours('11:20:30'::Time(4), 20);
select subtractHours('11:20:30'::Time(5), 5);
select subtractHours('11:20:30'::Time(6), 20);
select addMinutes('11:20:30'::Time(2), 50);
select addMinutes('11:20:30'::Time(3), 2000);
select subtractMinutes('11:20:30'::Time, 50);
select subtractMinutes('11:20:30'::Time(1), 5000);
select addSeconds('11:20:30'::Time, 500);
select addSeconds('11:20:30'::Time(2), 200000);
select subtractSeconds('11:20:30'::Time, 500);
select subtractSeconds('11:20:30'::Time(1), 500000);
```


<span id="779cc262"></span>
##### Date Time DateTime


1. New data type added: DateTimeWithoutTz.

   * It does not contain a timezone and is essentially similar to DateTime with a timezone of "UTC".

2. ANSI SQL standard using DATETIME and INTERVAL values

   * The default mode supports the interval type, but its format differs in ANSI mode.

   * Interval type in ANSI mode is YEAR::MONTH and DAY::TIME.

3. Note: The DateTime format yyyy\-mm\-dd hh:mm:ss[.nnnnnnn] is not yet compatible; please use the DateTime64 type for storage, which uses scale as a parameter. The maximum value for Scale is 9, which corresponds to the number of decimal places; the default value is 3.


The DateTime64 type supports a data range of: [1900\-01\-01 00:00:00, 2299\-12\-31 23:59:59.99999999].

<span id="84459846"></span>
##### Allow extended type conversion

In ClickHouse mode, implicit type conversion cannot occur between some numeric types if the conversion would result in precision loss (such as Decimal & Float, Int64 & Float) or performance degradation (such as UInt64 & Ints). In ANSI mode, these kinds of implicit conversions are allowed.

**Related sub\-options**: allow_extended_type_conversion: 0 / 1


|Sample Query 1: Implicit conversion between Decimal and Float<br><br>```SQL```<br>```SELECT 1::Decimal32(2) UNION ALL SELECT 1::Float64```<br> ||
|---|---|
|Output in ClickHouse mode:<br><br>DB::Exception: There is no supertype for types Decimal(9, 2), Float64 because some of them have no lossless conversion to Decimal |Output in ANSI mode:<br><br>1<br><br>1 |



|Example Query 2: Implicit conversion between Int64 and Float<br><br>```SQL```<br>```SELECT 1::Int64 UNION ALL SELECT 1::Float64```<br> ||
|---|---|
|Output in ClickHouse mode:<br><br>DB::Exception: There is no supertype for types Int64, Float64 because some of them are integers and some are floating point, but there is no floating point type, that can exactly represent all required integers |Output in ANSI mode:<br><br>1<br><br>1 |



|Example Query 3: Implicit conversion between UInt64 and Int<br><br>```SQL```<br>```SELECT 1::UInt64 UNION ALL SELECT 1::Int32```<br> ||
|---|---|
|Output in ClickHouse mode:<br><br>DB::Exception: There is no supertype for types UInt64, Int32 because some of them are signed integers and some are unsigned integers, but there is no signed integer type, that can exactly represent all required unsigned integer values |Output in ANSI mode:<br><br>1<br><br>1 |


<span id="5e4aa47b"></span>
## Parser

<span id="025e8feb"></span>
##### Decimal fixed\-point data type parsing

By default, numeric literals with a decimal point are parsed as floating point types. In ANSI mode, literals are parsed as Decimal fixed\-point data types to ensure precision.


|**Query example:** <br><br>```SQL```<br>```SELECT toTypeName(1.1);```<br> ||
|---|---|
|Output in Default mode: Float64 |Output in ANSI mode: Decimal(18, 1) |


<span id="77893a7f"></span>
## Analyzer

<span id="4bc33d4a"></span>
##### Prefer parsing as table columns

In the presence of duplicated names for aliases and table columns, under CLICKHOUSE mode, it will prefer parsing as alias; under ANSI mode, it will prefer parsing as table columns. This rule does not apply to ORDER BY clauses.

**Related Sub\-options**: prefer_column_name_to_alias: 0 / 1


|Example query 1:<br><br>```SQL```<br>```SELECT a + 1 AS a```<br>```FROM```<br>``` (SELECT 1 AS a)```<br>```WHERE a > 1 ORDER BY a;```<br> ||
|---|---|
|Output in ClickHouse mode:<br><br>2 |Output in ANSI mode:<br><br>Empty set |



|Example Search 2: The "prefer column name to alias" Rules do not apply to the ORDER BY clause, in both modes 'a' is parsed as an alias<br><br>```SQL```<br>```SELECT a AS origin_a, -a AS a```<br>```FROM```<br>``` (SELECT 1 AS a UNION ALL SELECT 2)```<br>```ORDER BY a ASC;```<br> ||
|---|---|
|Output in ClickHouse mode:<br><br>2, \-2<br><br>1, \-1 |Output in ANSI mode:<br><br>2, \-2<br><br>1, \-1 |


<span id="686498b2"></span>
##### Ambiguous aliases

In ClickHouse mode, when joining two tables with the same field names, referring to that name is interpreted as referring to the first table's field. This feature deviates from mainstream databases and makes the semantics more ambiguous in the context of multi\-table joins. Under ANSI mode, referencing ambiguous names is prohibited.


|Example search:<br><br>```SQL```<br>```SELECT a```<br>```FROM```<br>```  (SELECT 1 AS a) x```<br>```  CROSS JOIN```<br>```  (SELECT 's' AS a) y;```<br> ||
|---|---|
|Output in ClickHouse mode:<br><br>1 |Output in ANSI mode:<br><br>DB::Exception: Identifier a is ambiguous. |


<span id="7a68b630"></span>
## Function

<span id="60cde9c2"></span>
##### Cast can be null

In ANSI mode, if the argument of the CAST function is of Nullable type, the result type remains Nullable.

**Related sub\-option**: cast_keep_nullable


|**Example Search**<br><br>```SQL```<br>```SELECT toTypeName(CAST(1::Int32 AS Int64)), toTypeName(CAST(1::Nullable(Int32) AS Int64));```<br> ||
|---|---|
|Output in the default mode:<br><br>Int64, Int64 |Output in ANSI mode:<br><br>Int64, Nullable(Int64) |


<span id="4257316b"></span>
##### Decimal type computation

<span id="19c77efe"></span>
###### Decimal division digit expansion

In default mode, the decimal places of the decimal division result type are: S = S1. When S1 is not large enough, this can lead to larger rounding errors. In ANSI mode, the scale is: S = max(6, S1).

**Related sub\-option**: decimal_division_use_extended_scale


|**Search Example**<br><br>```SQL```<br>```SELECT 2.0::Decimal64(1) / 3, toTypeName(2.0::Decimal64(1) / 3);```<br> ||
|---|---|
|Output in default mode:<br><br>0.6, Decimal(18, 1) |Output in ANSI mode:<br><br>0.666666, Decimal(18, 6) |


<span id="d91af720"></span>
###### Expand storage type to avoid overflow

Some decimal number scenarios may result in overflow errors due to rescaling. In ANSI mode, the underlying storage type is automatically promoted to minimize overflow. The scenarios include:


* Multiplication and division between Decimal types

* Division between Decimal type and Int integer type


**Relevant sub\-option**: decimal_arithmetic_promote_storage


|**Search Example**<br><br>```SQL```<br>```SELECT 2.0::Decimal32(4) * 3.0::Decimal32(5);```<br> ||
|---|---|
|Output in default mode:<br><br>DB::Exception: Decimal math overflow |Output in ANSI mode:<br><br>6.000000000 |


<span id="75d1c438"></span>
##### Window functions

In ANSI mode, regardless of the frame type, all rows with the same value in `ORDER BY` expressions are considered the same row.


|**Search Example**<br><br>```SQL```<br>```WITH nums AS (SELECT arrayJoin([1, 2, 1, 1]) as src) SELECT percent_rank() OVER (ORDER BY src ROWS CURRENT ROW) from nums```<br> ||
|---|---|
|Output in Default Mode:<br><br>0<br><br>0.3333333333333333<br><br>0.6666666666666666<br><br>1 |Output in ANSI Mode:<br><br>0<br><br>0<br><br>0<br><br>1 |


<span id="44a7b6ba"></span>
##### Accurate support for null value equality comparison

In ANSI mode, just like the regular `=` operator, comparing two values yields 0 (not equal) or 1 (equal); in other words: `'a' <=> 'b'` results in `0`, and `'a' <=> 'a'` results in `1`.

Unlike the conventional `=` operator, the value of `NULL` has no special meaning, hence it never results in a `NULL` output; thus: `'a'<=>NULL` yields `0`, `NULL<=>NULL` yields `1`.


|**Search Example**<br><br>```SQL```<br>```SELECT NULL<=>NULL;```<br>```SELECT NULL<=>0;```<br>```SELECT 0 IS DISTINCT FROM NULL;```<br>```SELECT 0 IS NOT DISTINCT FROM NULL;```<br>```SELECT '';```<br> ||
|---|---|
|Output in ANSI mode:<br><br>1<br><br>0<br><br>1<br><br>0 | |


<span id="afc4bddb"></span>
## Subquery expressions

<span id="e542b8a3"></span>
##### Correlated subquery

ANSI mode supports correlated subqueries.

Query example:

```SQL
INSERT INTO orders(order_id, customer_id, amount) VALUES
  (1, 101, 100),
  (2, 101, 120),
  (3, 102, 30);

SELECT order_id
FROM customers x
WHERE
  amount = (SELECT avg(amount)FROM customers yWHERE x.customer_id = y.customer_id)
```


<span id="f77d29d0"></span>
##### Join operations

<span id="7a04cb6e"></span>
###### Using NULL values

In default mode, for cases without matching records, the outer join defaults to 0 or "". In ANSI mode, the default is NULL.

**Related sub\-option**: join_use_nulls


|**Search Example**<br><br>```SQL```<br>```SELECT a, b FROM (SELECT 1 AS k, 100 AS a) x LEFT JOIN (SELECT 2 AS k, 200 AS b) y ON x.k = y.k;```<br> ||
|---|---|
|Output in default mode:<br><br>100, 0 |Output in ANSI mode:<br><br>100, NULL |


<span id="f9e895d9"></span>
###### Use external links

In the default mode, you can specify conditions for outer joins. In ANSI mode, outer joins do not allow specified conditions.


|**Search Example 1: When using a left join, the output for the join key is the data from the left table**<br><br>```SQL```<br>```SELECT k FROM (SELECT 1 as k) LEFT JOIN (SELECT 2 as k) USING k;```<br> ||
|---|---|
|Output in default mode:<br><br>1 |Output in ANSI mode:<br><br>Syntax error: failed at position 57; |



|**Search Example 2: When using a right join, the output for the join key is the data from the right table**<br><br>```SQL```<br>```SELECT k FROM (SELECT 1 as k) RIGHT JOIN (SELECT 2 as k) USING k;```<br> ||
|---|---|
|Output in default mode:<br><br>2 |Output in ANSI mode:<br><br>Syntax error: failed at position 57; |



|**Query Example 3: In a Full join, the output of the join key includes data from both the left and right tables**<br><br>```SQL```<br>```SELECT k FROM (SELECT 1 as k) FULL JOIN (SELECT 2 as k) USING k;```<br> ||
|---|---|
|Output in default mode:<br><br>1<br><br>2 |Output in ANSI mode:<br><br>Syntax error: failed at position 57; |


<span id="9a0a38c1"></span>
###### Use alias Join

In the default mode, when joining using keys with the same alias, the alias is visible to the left table. This feature is disabled in ANSI mode.


|**Query example**<br><br>```SQL```<br>```SELECT a + 1 AS k FROM (SELECT 1 as a) JOIN (SELECT 2::UInt16 AS k) USING k;```<br> ||
|---|---|
|Output in default mode:<br><br>2 |Output in ANSI mode:<br><br>DB::Exception: Can not find column 'k' in join left side |


<span id="b463273a"></span>
###### Support for Hash Join / Nested Loop Join / Merge Join:

In ANSI mode, hash joins, nested loop joins, and merge joins are supported.

**Example**

```SQL
CREATE TABLE nse_lhs (key int, value Nullable(UInt8)) ENGINE=CnchMergeTree order by key; 
CREATE TABLE nse_rhs (key int, value Nullable(UInt8)) ENGINE=CnchMergeTree order by key; 

INSERT INTO nse_lhs VALUES (1,1) (2, 2) (3, NULL) (4, NULL) (5,6) (6, NULL); 
INSERT INTO nse_rhs VALUES (1,1) (2, NULL) (3, 2) (4, NULL) (5,7) (6, 0); 

select '# Null safe join (equi hash join)'; 
SELECT key, value FROM nse_lhs JOIN nse_rhs ON nse_lhs.key=nse_rhs.key AND nse_rhs.value IS NOT DISTINCT FROM nse_lhs.value; 
select ''; 

SET join_algorithm='partial_merge'; 
select '# Null safe join (merge join)'; 
SELECT key, value FROM nse_lhs JOIN nse_rhs ON nse_lhs.key=nse_rhs.key AND nse_rhs.value<=>nse_lhs.value; 

SET join_algorithm='nested_loop'; 
select '# Null safe join (nested loop join)'; 
SELECT key, value FROM nse_lhs JOIN nse_rhs ON nse_lhs.key=nse_rhs.key AND nse_rhs.value<=>nse_lhs.value; SQL
```


```SQL
--Output in ANSI mode
# USING <=> hash
1 1
4 \N# USING <=> partial_merge
1 1
4 \N# USING <=> nested_loop
1 1
4 \N
```


<span id="379945dd"></span>
##### Set collection operations

<span id="7ba8f01f"></span>
###### Default operation mode

In the default mode, for union / intersect / except operations, if all / distinct (deduplication) semantics are not explicitly specified, the default is all semantics; under ANSI mode, the default is distinct semantics.


|**Search Example**<br><br>```SQL```<br>```SELECT 1 UNION SELECT 1;```<br> ||
|---|---|
|Output in Default Mode:<br><br>1<br><br>1 |Output in ANSI Mode:<br><br>1 |
