---
title: "Window function"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/window-function"
---

Window function is an advanced function that allows users to group and perform aggregate calculations on a result set without explicitly grouping the query. The input parameters of the window function query are taken from a "window" of one or more rows of the previous query result. For instance: ranking the query results in groups, accumulating the grouped query results again.

Window functions are commonly used in business for analysis of changes relative to the same period, ranking of the top N, etc.

<span id="0cf2ce51"></span>
# Syntax support

```SQL
aggregate_function (column_name)
  OVER ([[PARTITION BY grouping_column] [ORDER BY sorting_column] 
        [ROWS or RANGE or GROUPS <offest> PRECEDING and <offset> FOLLOWING]] | [window_name])
FROM table_name
WINDOW window_name as ([[PARTITION BY grouping_column] [ORDER BY sorting_column])
```


Explanation of Parameters:


* `PARTITION BY` \- Splits the data results into windows. Unlike Group By, data from different windows is not merged into one line, but rather marked for operations such as order by and row after splitting.

* `ORDER BY` \- In the `OVER` clause, `ORDER BY` is only used to determine the order of calculations for the window function, but it has no effect on the display order of the results.

* `ROWS or RANGE or GROUPS` \- Define the boundary scope of the window. Aggregate functions calculate within the boundary scope. 、

   * **ROW:**  Defines the boundary based on the physical location of rows. Example: `ROWS BETWEEN 1 PRECEDING AND 1 FOLLOWING` means that for the current row, the window includes the previous row, the current row, and the next row.

   * **RANGE:**  Defines the boundary based on the scope of row values. Example: If you sort by date and use `RANGE BETWEEN INTERVAL 1 DAY PRECEDING AND INTERVAL 1 DAY FOLLOWING`, the window for a given date will include all data from the previous day, the current date, and the next day.

   * **GROUPS**: Defines the boundary based on the group location relative to the current row. First sort by `ORDER BY`, then proceed to take values for `ROWS BETWEEN`. Example: `GROUPS BETWEEN 1 PRECEDING AND 1 FOLLOWING`, the window contains the row before and after the current row, sorted.

* `WINDOW` \- Allows naming a window for reuse across multiple expressions.


<span id="使用示例"></span>
# Example usage

The original table is as follows:


|**a** |**b** |**c** |**e** |
|---|---|---|---|
|1 |1 |1 |10 |
|1 |1 |2 |20 |
|1 |1 |3 |30 |
|1 |2 |1 |100 |
|1 |2 |2 |200 |
|2 |1 |1 |60 |
|3 |1 |1 |80 |


The SQL query is:

```sql
select a, b, c, sum(e), sum(sum(e)) over 
    (partition by a,b order by a,b,c rows between 3 preceding and 3 following) 
    as acc_sum
from t0_local group by a,b,c order by a,b,c;
```


The SQL returns the following:


|**a** |**b** |**c** |**sum(e)**  |**acc_sum** |
|---|---|---|---|---|
|1 |1 |1 |10 |10 |
|1 |1 |2 |20 |30 |
|1 |1 |3 |30 |60 |
|1 |2 |1 |100 |100 |
|1 |2 |2 |200 |300 |
|2 |1 |1 |60 |60 |
|3 |1 |1 |80 |80 |


By opening the results in four windows (1,1), (1,2), (2,1), (3,1), the `acc_sum` column displays the cumulative value within each window.

<span id="语法详解"></span>
##### Syntax explained

For detailed syntax of the window function, refer to [this document](https://sqlite.org/windowfunctions.html).

In this section, we briefly introduce the syntax that has been implemented.

A typical syntax example is:

```sql
select a, b, window_founction(c) over 
    (partition by a,b order by a,b rows between n preceding and m following)
```



1. In the example, `window_function()` refers to window\-capable functions, including all ClickHouse aggregate functions such as `sum`, `avg`, `count`, `min`, Max, etc., as well as Navigation functions. **Currently, Navigation functions only support the following four:**  `rank`, `row_number`, `dense_rank`, `percent_rank`.

   1. `row_number()` generates a self\-increasing number when sorting by value and is non\-repetitive.

   2. `rank()` produces a self\-increasing number when sorted by value, repeats if values are equal, and will result in gaps.

   3. `dense_rank()` generates a self\-increasing number when sorted by value, repeats if values are equal, and does not result in gaps.

   4. `percent_rank()` produces a percentage value when sorted by value, equals to `(rank() - 1)/(- 1)`.

2. The `OVER` clause contains three parts: `partition by`, `order by`, and `rows`.

   1. `partition by` is used for partitioning the data into windows. Unlike Group By, data in different windows is not merged into one line as with `Group by`; it rather identifies which groups to perform `order by` and `row` actions on after partitioning.

   2. order by, in the over clause, only determines the order in which window functions are calculated, but it does not affect the order of the results displayed.

   3. `rows`, semantically refers to calculating the scope of the window frame in row units. For example, `rows between 3 preceding and 2 following` means that the frame range includes the three rows before and two rows after the current row. If the current row is n, then the frame range is [n\-3, n+2]. The `rows` part can be omitted.

3. We support naming the windows, as shown below:

   ```sql
   SELECT a                        AS a,
          row_number() OVER win    AS row_number,
          rank() OVER win          AS rank,
          dense_rank() OVER win    AS dense_rank,
          percent_rank() OVER win  AS percent_rank
   FROM t2
   WINDOW win AS (ORDER BY a);
   ```
   

   In the SQL statement above, we use `win` to replace a `window: OVER (ORDER BY a)`, allowing the same window to be used in multiple output columns.

4. In the Window function, the start and end offsets of the frame can be represented by columns that have already been output. For example:

   ```sql
   select a, b, c, d, e, sum(e), sum(sum(e)) over 
       (partition by a,b order by a,b,c rows between d preceding and e following) 
       as acc_sum
   from t0_local group by a,b,c order by a,b,c;
   ```
   

   If d and e are both of integer type, then the offsets can be represented by the values of d and e, which are used row by row.

   
   |d |e |preceding |following |
   |---|---|---|---|
   |1 |2 |1 |2 |
   |3 |4 |3 |4 |
   

5. Window functions are optimized for specific SQL; if preceding and following meet certain conditions, the results will be calculated via streaming (each row of data is scanned only once), which can enhance read performance.

   
   |preceding |following |streaming |
   |---|---|---|
   |ignore |ignore |true |
   |Unbounded preceding |Current row |true |
   |Unbounded preceding |Constants, such as 3, 5 |true |
   |Anything else |Anything else |false |
   


<span id="bbb49628"></span>
# Support functions

All aggregate functions in ByteHouse, such as `sum`, `avg`, `count`, `min`, `max` etc., support use as functions under window syntax. In addition, the window syntax also supports the following Navigation functions: `rank`, `dense_rank`, `percent_rank`, `cume_dist`, `ntile`, `nth_value`, `row_number`, `lag`, and `lead`.

Assume we have the following data in the `sales_data` table:

```YAML
date        | sales
 -----------|------ 
 2022-01-01 | 100 
 2022-01-02 | 150 
 2022-01-03 | 150 
 2022-01-04 | 200
```


Function Explanation:


1. `row_number()` generates a unique self\-increasing number when sorting by value; it will not repeat.

2. `rank()` generates a self\-increasing number when sorting by value; it repeats for equal values and will have gaps.

3. `dense_rank()` generates a self\-increasing number when sorting by value; it repeats for equal values without gaps.

4. `percent_rank()` generates a percentage value when sorting by value, equals to `(rank() - 1)/(- 1)`.

5. `cume_dist()`: This function calculates the cumulative distribution for the current row, which is the ratio of the number of rows before the current row to the total number of rows. The following query calculates the cumulative distribution for each row of sales data among all sales data:

   ```SQL
   SELECT date, sales, CUME_DIST() OVER (ORDER BY sales) AS cum_distribution FROM sales_data; 
   ```
   

6. `nth_value(value, n)` **:**  The `nth_value` function returns the nth `item` in the window. This is very useful for retrieving values at specific positions within a window. The following query returns the second sales value for each row within a date\-sorted window:

   ```SQL
   SELECT date, sales, NTH_VALUE(sales, 2) OVER (ORDER BY date) AS second_sale_value FROM sales_data; 
   ```
   

7. `ntile(n)` **:**  This function divides the result set into `n` roughly equal parts and assigns each row a bucket number from 1 to `n`. In the query below, we divide the sales data into four quartiles and assign each row a quartile value:

   ```SQL
   SELECT date, sales, NTILE(4) OVER (ORDER BY sales) AS quartile FROM sales_data; 
   ```
   

8. `lag/lead(value, offset)`: The `lag` and `lead` functions can help you retrieve values before or after the current row. `Offset` is an integer indicating the number of rows from the current row. In the query below, we are looking for the previous day's sales data:

   ```SQL
   SELECT date, sales, LAG(sales, 1) OVER (ORDER BY date) AS prev_sales FROM sales_data; 
   ```
