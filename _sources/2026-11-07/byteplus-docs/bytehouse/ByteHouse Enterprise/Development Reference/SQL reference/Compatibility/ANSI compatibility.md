---
title: "ANSI compatibility"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/ce-ansi-compatibility"
---

ByteHouse ANSI Mode aims to make SQL syntax and execution behavior more consistent with ANSI standards or other mainstream databases
<span id="e4011710"></span>
## Set ANSI mode
Through the `dialect_type` option, ByteHouse can switch between ANSI mode and ClickHouse mode, for example:

* `SET dialect_type = 'CLICKHOUSE';`
* `SET dialect_type = 'ANSI';`

ByteHouse defaults to ClickHouse mode.
:::tip
It is recommended to set `dialect_type` using the above SET command, rather than setting it via query-level SETTINGS, such as:
`SELECT ... SETTINGS dialect_type = 'ANSI';`
:::
In terms of implementation, many ANSI features are controlled by individual sub-options, dialect_type can be considered the sum of these sub-options. If needed, sub-options can be used to control specific behaviors in ANSI mode, for example:
```SQL
SET dialect_type = 'ANSI'；

SELECT ... SETTINGS join_use_nulls = 0;
```

I listed the ANSI-related functions. If this function has separate sub-options, they are explained by **relevant sub-options**.
<span id="d889f460"></span>
## Compatibility details
<span id="dc441b47"></span>
### Data type
<span id="18752055"></span>
#### Default type can be empty
By default (ClickHouse) mode, data type cannot be empty, but ANSI standards require that it can be empty.

* In ANSI mode, data types that are not empty can be indicated as NOT NULL.
* In ClickHouse mode, fields can be non-empty without declaration; if the table is empty, use Nullable().

The following uses the int type to demonstrate the differences in usage between the two modes:

| | | | \
| |ANSI Mode |ClickHouse Mode |
|---|---|---|
| | | | \
|Nullable |id Int8 |id Nullable(Int8) |
| | | | \
|Not empty |id Int8 Not Null |id Int8 |


| || \
|Query example |\
|```SQL |\
|SELECT value, changed |\
|FROM system.settings |\
|WHERE name  |\
|LIKE '%dialect_type%'; |\
|``` |\
| | |
|---|---|
| | | \
|Output in default mode: |\
|0, 0 |Output in ANSI mode: |\
| |1, 1 |

<span id="def48ecf"></span>
#### Time data type time (includes timezone)
Added the Time data type.
The time data type with timezone support is an ANSI SQL standard, supported by MySQL and PostgreSQL. The format for the time data type is hh:mm:ss[.nnnnnnn]. Internally represented as Int64. Its precision is determined by the parameter scale. The maximum value for scale is 9, which equals the number of decimal places; the default value is 3.
Example of query: Example function using the Time data type.
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

<span id="08cc18d0"></span>
#### Date and time DateTime data type

1. Added the new DateTimeWithoutTz data type.
   It does not contain a timezone and is essentially similar to DateTime with "UTC" as its timezone.
2. ANSI SQL standard for using DATETIME and INTERVAL values
   Default mode supports the interval type, yet its format differs in ANSI mode.
   Interval type in ANSI mode is YEAR::MONTH and DAY::TIME.
3. Caution: DateTime format yyyy-mm-dd hh:mm:ss[.nnnnnnn] is not compatible. Please use DateTime64 Type, parameterized by scale for precision. The maximum scale is Sep, representing the number of decimal places; the default value is Mar.

DateTime64 Type supports a data range of: [1900-01-01 00:00:00, 2299-12-31 23:59:59.99999999].
<span id="31232288"></span>
### Parser
<span id="155b4c7e"></span>
#### Expression alias
In ByteHouse, aliases can be defined on expressions in any clause; in ANSI mode, aliases are only allowed on expressions in the SELECT clause.

| || \
|Query example 1: Define alias in With clause |\
|```SQL |\
|WITH |\
|  1 AS a, |\
|  (SELECT 2) AS b |\
|SELECT |\
|  a, b; |\
|``` |\
| | |
|---|---|
| | | \
|Output in default mode: |\
|1, 2 |Output in ANSI mode: |\
| |Syntax Error |\
| |*(Note: Syntax Error)* |


| || \
|Query Example 2: Define an alias in the WHERE clause |\
|```SQL |\
|SELECT |\
|  a |\
|WHERE (2 > 1) AS a |\
|``` |\
| | |
|---|---|
| | | \
|Output in default mode: |\
|1 |Output in ANSI mode: |\
| |Syntax Error |\
| |*(Note: Syntax Error)* |

<span id="37188f98"></span>
#### Sub-expression alias
ByteHouse mode allows you to define aliases for subexpressions, but this is disabled in ANSI mode.

| || \
|Query Example: |\
|```SQL |\
|SELECT 1 + (1 AS a) > a; |\
|``` |\
| | |
|---|---|
| | | \
|Output in default mode: |\
|1 |Output in ANSI mode: |\
| |Syntax Error |\
| |*(Note: Syntax Error)* |

<span id="85c75915"></span>
#### Decimal fixed-point data type Analysis *
By default, numerical literals with decimal points are parsed as floating-point types. In ANSI mode, literals are parsed as Decimal fixed-point data type to ensure accuracy.

| || \
|Example query: |\
|```SQL |\
|SELECT toTypeName(1.1); |\
|``` |\
| | |
|---|---|
| | | \
|Output in default mode: |\
|Float64 |Output in ANSI mode: |\
| |Decimal(18, 1) |

<span id="fa64b4f7"></span>
### Parser
<span id="a8f3d958"></span>
#### Scope of visibility for aliases under the SELECT statement
In the default mode, aliases defined in the SELECT clause are visible to both external queries and any sub-clauses of the current query; in ANSI mode, aliases are only visible to external queries and the ORDER BY clause of the current query.

| || \
|Example Query 1: Alias not visible to the WHERE clause |\
|```SQL |\
|SELECT 1 AS a |\
|WHERE a > 0; |\
|``` |\
| | |
|---|---|
| | | \
|Output in default mode: |\
|1= |Output in ANSI mode: |\
| |DB::Exception: Can not resolve identifier: a |\
| |(Note: DB throws an exception, unable to resolve identifier a) |


| || \
|Example Query 2: Alias not visible to the SELECT clause |\
|```SQL |\
|SELECT 1 AS a, a + 1; |\
|``` |\
| | |
|---|---|
| | | \
|Output in default mode: |\
|1, 2 |Output in ANSI mode: |\
| |DB::Exception: Can not resolve identifier: a |\
| |(Note: DB throws an exception, unable to resolve the identifier a) |


| || \
|Query Example 3: Alias visible to the ORDER BY clause |\
|```SQL |\
|SELECT 1 AS a |\
|ORDER BY a; |\
|``` |\
| | |
|---|---|
| | | \
|Output in default mode: |\
|1 |Output in ANSI mode: |\
| |1 |

<span id="f394d65c"></span>
#### Ambiguous aliases
In ANSI mode, referencing ambiguous names is prohibited in the case of multi-table joins, a feature inconsistent with mainstream databases.

| || \
|Query example: |\
|```SQL |\
|SELECT a |\
|FROM |\
|  (SELECT 1 AS a) x |\
|  CROSS JOIN |\
|  (SELECT 's' AS a) y; |\
|``` |\
| | |
|---|---|
| | | \
|Output in default mode: |\
|1 |Output in ANSI mode: |\
| |DB::Exception: Identifier a is ambiguous. |\
| |(Note: DB throws an exception, identifier 'a' is unclear) |

<span id="0e70ec0f"></span>
### Function
<span id="af439707"></span>
#### Cast can be empty*
In ANSI mode, if the argument for the CAST function is of a Nullable type, the result type remains Nullable.
**Related sub-option**: cast_keep_nullable

| || \
|Query example: |\
|```SQL |\
|SELECT |\
|  toTypeName(CAST(1::Int32 AS Int64)), |\
|  toTypeName(CAST(1::Nullable(Int32) AS Int64)); |\
|``` |\
| | |
|---|---|
| | | \
|Output in default mode: |\
|Int64, Int64 |Output in ANSI mode: |\
| |Int64, Nullable(Int64) |

<span id="5a61e8b6"></span>
#### Calculations for Decimal type
<span id="a8074e0a"></span>
##### Decimal division extends the number of digits *
In default mode, the number of decimal places for decimal division results is: S = S1. When S1 is not large enough, this can lead to significant rounding errors. In ANSI mode, the scale value is: S = max(6, S1).
**Related sub-option**: decimal_division_use_extended_scale

| || \
|Query example: |\
|```SQL |\
|SELECT 2.0::Decimal64(1) / 3, toTypeName(2.0::Decimal64(1) / 3); |\
|``` |\
| | |
|---|---|
| | | \
|Output in default mode: |\
|0.6, Decimal(18, 1) |Output in ANSI mode: |\
| |0.666666, Decimal(18, 6) |

<span id="e40331e1"></span>
##### Expand the storage type to avoid overflow
Some decimal number scenes are prone to overflow errors due to rescaling. In ANSI mode, the underlying storage type is automatically upgraded to minimize overflow. These scenarios include:

* Multiplication and division between Decimal types
* Division of Decimal type and Integer type

**Sub-options**: decimal_arithmetic_promote_storage

| || \
|Query example: |\
|```SQL |\
|SELECT 2.0::Decimal32(4) * 3.0::Decimal32(5); |\
|``` |\
| | |
|---|---|
| | | \
|Output in default mode: |\
|DB::Exception: Decimal math overflow |Output in ANSI mode: |\
| |6.000000000 |

<span id="a6f6f1be"></span>
#### Window functions
In ANSI mode, regardless of the frame type, all rows with the same value in `ORDER BY` expressions are viewed as the same row.

| || \
|Sample query: |\
|Query example: |\
|```SQL |\
|WITH nums AS (SELECT arrayJoin([1, 2, 1, 1]) as src) SELECT percent_rank() OVER (ORDER BY src ROWS CURRENT ROW) from nums |\
|``` |\
| | |
|---|---|
| | | \
|Output in default mode: |\
|0 |\
|0.3333333333333333 |\
|0.6666666666666666 |\
|1 |Output in ANSI mode: |\
| |0 |\
| |0 |\
| |0 |\
| |1 |

<span id="e2b238b3"></span>
#### Accurate support for null value equality judgment
In ANSI mode, like the regular `=` operator, comparing two values results in 0 (not equal) or 1 (equal); in other words: `'a' <=> 'b'` yields `0`, `'a' <=> 'a'` yields `1`.
Unlike conventional `equals` operators, the value of `null` has no special meaning, so it never results in a situation where `null` is produced as the outcome; thus: `'a'<=>null` yields `0`, `null<=>null` yields `1`.

| || \
|Query Example: |\
|```SQL |\
|SELECT NULL<=>NULL; |\
|SELECT NULL<=>0; |\
|SELECT 0 IS DISTINCT FROM NULL; |\
|SELECT 0 IS NOT DISTINCT FROM NULL; |\
|SELECT ''; |\
|``` |\
| | |
|---|---|
| | | \
|Output in ANSI mode: |\
|1 |\
|0 |\
|1 |\
|0 | |

<span id="7b598ed0"></span>
### Subquery expression
<span id="6db5d9ab"></span>
#### Correlated subquery
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
  amount >= (SELECT avg(amount)
             FROM customers y
             WHERE x.customer_id = y.customer_id)
```

<span id="63ab8d8d"></span>
#### Join connection
<span id="506bda02"></span>
##### Use null value
By default, for cases without connection records, the external connection defaults to 0 or null. In ANSI mode, the default value is null.
Related sub-option: join_use_nulls

| || \
|Query Example: |\
|```SQL |\
|SELECT a, b |\
|FROM |\
|  (SELECT 1 AS k, 100 AS a) x |\
|  LEFT JOIN |\
|  (SELECT 2 AS k, 200 AS b) y |\
|  ON x.k = y.k; |\
|``` |\
| | |
|---|---|
| | | \
|Output in default mode: |\
|100, 0 |Output in ANSI mode: |\
| |100, NULL |

<span id="38e2c4d1"></span>
##### Use external links
In default mode, you can specify the conditions for external links. In ANSI mode, it is not allowed to use specified conditions for external joins.

| || \
|Query example 1: In a left join, the output of the join key is the data from the left table |\
|```SQL |\
|SELECT k |\
|FROM |\
|  (SELECT 1 as k) |\
|  LEFT JOIN |\
|  (SELECT 2 as k) |\
|  USING k; |\
|``` |\
| | |
|---|---|
| | | \
|Output in default mode: |\
|1 |Output in ANSI mode: |\
| |Syntax error: failed at position 57; |


| || \
|Query example 2: In a right join, the output of the join key is the data from the right table |\
|```SQL |\
|SELECT k |\
|FROM |\
|  (SELECT 1 as k) |\
|  RIGHT JOIN |\
|  (SELECT 2 as k) |\
|  USING k; |\
|``` |\
| | |
|---|---|
| | | \
|Output in default mode: |\
|2 |Output in ANSI mode: |\
| |Syntax error: failed at position 57; |


| || \
|Search example 3: During Full join, the output of the join key is the data from both tables |\
|```SQL |\
|SELECT k |\
|FROM |\
|  (SELECT 1 as k) |\
|  FULL JOIN |\
|  (SELECT 2 as k) |\
|  USING k; |\
|``` |\
| | |
|---|---|
| | | \
|Output in default mode: |\
|1 |\
|2 |Output in ANSI Mode: |\
| |Syntax error: failed at position 57; |

<span id="2bff9111"></span>
##### Use Alias Join
In default mode, when the join using a key has the same alias, this alias is visible to the left table. This function is disabled in ANSI mode.

| || \
|Search example: |\
|```SQL |\
|SELECT |\
|  a + 1 AS k |\
|FROM |\
|  (SELECT 1 as a) |\
|  JOIN |\
|  (SELECT 2::UInt16 AS k) |\
|  USING k; |\
|``` |\
| | |
|---|---|
| | | \
|Output in default mode: |\
|2 |Output in ANSI Mode: |\
| |DB::Exception: Can not find column 'k' in join left side |

<span id="2a05e80c"></span>
##### Support for Hash Join / NestedLoop Join / Merge Join:
In ANSI mode, hash joins, nested loop joins, and merge joins are supported.

| || \
|Search Example: |\
|```SQL |\
|CREATE TABLE nse_lhs (key int, value Nullable(UInt8)) ENGINE=Memory; |\
|CREATE TABLE nse_rhs (key int, value Nullable(UInt8)) ENGINE=Memory; |\
| |\
|INSERT INTO nse_lhs VALUES (1,1) (2, 2) (3, NULL) (4, NULL) (5,6) (6, NULL); |\
|INSERT INTO nse_rhs VALUES (1,1) (2, NULL) (3, 2) (4, NULL) (5,7) (6, 0); |\
| |\
|select '# Null safe join (equi hash join)'; |\
|SELECT key, value FROM nse_lhs JOIN nse_rhs ON nse_lhs.key=nse_rhs.key AND nse_rhs.value IS NOT DISTINCT FROM nse_lhs.value; |\
|select ''; |\
| |\
|SET join_algorithm='partial_merge'; |\
|select '# Null safe join (merge join)'; |\
|SELECT key, value FROM nse_lhs JOIN nse_rhs ON nse_lhs.key=nse_rhs.key  |\
|AND nse_rhs.value<=>nse_lhs.value; |\
| |\
|SET join_algorithm='nested_loop'; |\
|select '# Null safe join (nested loop join)'; |\
|SELECT key, value FROM nse_lhs JOIN nse_rhs ON nse_lhs.key=nse_rhs.key  |\
|AND nse_rhs.value<=>nse_lhs.value; |\
|``` |\
| | |
|---|---|
| | | \
|Output in ANSI Mode: |\
|\# USING <=> hash |\
|1 1 |\
|4 \N |\
|\# USING <=> partial_merge |\
|1 1 |\
|4 \N |\
|\# USING <=> nested_loop |\
|1 1 |\
|4 \N | |

<span id="db0fefe6"></span>
#### Set operations
<span id="a0d8d4b2"></span>
##### Default mode actions
By default in union/intersect/except operations, if 'all/distinct' (distinctive) semantics are not explicitly specified, it defaults to 'all' semantics; under ANSI Mode, it defaults to 'distinct' semantics.

| || \
|Search example: |\
|```SQL |\
|SELECT 1 UNION SELECT 1; |\
|``` |\
| | |
|---|---|
| | | \
|Output in default mode: |\
|1 |\
|1 |Output in ANSI mode: |\
| |1 |
