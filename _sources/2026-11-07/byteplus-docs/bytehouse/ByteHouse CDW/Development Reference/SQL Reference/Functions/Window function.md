---
title: "Window function"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/docs-window"
---

ByteHouse supports the standard syntax for window functions. A list of window\-related features is explained below.


|Feature |Status |
|---|---|
|ROWS mode |Support |
|RANGE mode |Support (default) |
|GROUPS mode |Support |
|Expressions involving window functions like: |Support |
|Use of aggregate functions in windows |Support |
|Navigations functions: |Support rank, dense_rank, percent_rank, cume_dist, ntile, nth_value, row_number, lagInFrame, leadInFrame, nonNegativeDerivative, lag, lead, first_value, last_value |
|Windows aliases like: |Support |



* The definition of peer group in ANSI/MySQL dialect and Clickhouse is different. For details, please refer to the ANSI section


<span id="4b4df00f"></span>
### row_number ()

Returns the number of rows in the current partition. Rows are numbered starting from 1 in the order of the ORDER BY clause in the window definition, or in any order if there is no ORDER BY clause.

<span id="84309d54"></span>
### Rank ()

Returns the number of the first sibling row in each group, with an interval in the ranking of the current row. If there is no ORDER BY clause, all rows are treated as sibling rows, and this function always returns 1.

<span id="903c31ad"></span>
### dense_rank ()

Returns the number of sibling groups within its partition for the current row, with no interval in ranking. Rows are numbered starting from 1, in the order of the ORDER BY clause in the window definition. If there is no ORDER BY clause, all rows are treated as sibling rows, this function always returns 1.

<span id="af884c93"></span>
### percent_rank ()

Despite its name, this function always returns a value between 0.0 and 1.0, calculated as (rank \- 1)/(partition\-rows \- 1), where rank is the value returned by the built\-in window function rank () and partition\-rows is the total number of rows in the partition. If there is only one row in the partition, this function returns 0.0.

<span id="9dcae443"></span>
### cume_dist ()

Cumulative distribution. Calculated as row\-number/partition\-rows, where row\-number is the value returned by the row_number () function for the last sibling row in the group, and partition\-rows is the number of rows in the partition.

<span id="6a71bb15"></span>
### Ntile (N)

The argument N is treated as an integer. This function divides the partition into groups of N as evenly as possible and assigns an integer between 1 and N to each group in the order defined by the ORDER BY clause, otherwise in any order. Larger groups appear first if necessary. This function returns the integer value of the group to which the current row belongs.

<span id="62323924"></span>
### lag (expr)/lag (expr, offset)/lag (expr, offset, default)

The first form of the lag () function returns the result of evaluating the expression expr on the previous line in the partition. Alternatively, if there is no previous line (because the current line is the first), NULL is returned.

If the offset argument is provided, it must be a non\-negative integer. In this case, the value returned is the result of the expression expr calculated for the offset row before the current row in the partition. If offset is 0, expr is calculated for the current row. If there is no offset row before the current row, NULL is returned.

If a default parameter is also provided, return default instead of NULL if the row specified by offset does not exist.

In contrast to lagInFrame, the user\-supplied Frame definition under the lag function is ignored, using the default rows between unbounded preceding and unbounded following

<span id="d873bcf9"></span>
### lead (expr)/lead (expr, offset)/lead (expr, offset, default)

The first form of the lead () function returns the result of evaluating the expression expr on the next line in the partition. Alternatively, if there is no next line (because the current line is the last), NULL is returned.

If the offset argument is provided, it must be a non\-negative integer. In this case, the value returned is the result of the expression expr calculated for offset rows after the current row in the partition. If offset is 0, expr is calculated for the current row. If there are no offset rows after the current row, NULL is returned.

If a default parameter is also provided, return default instead of NULL if the row specified by offset does not exist.

In contrast to leadInFrame, the user\-supplied Frame definition under the lead function is ignored, using the default rows between unbounded preceding and unbounded following

<span id="a47d1848"></span>
### first_value (expr)

This built\-in window function evaluates the window frame for each line in the same way as the aggregate window function. It returns the result of the expression expr evaluated on the first line of the window frame.

<span id="c2ff043b"></span>
### last_value (expr)

This built\-in window function evaluates the window frame for each line in the same way as the aggregate window function. It returns the result of evaluating the expression expr on the last line of the window frame.

<span id="083d42c7"></span>
### nth_value (expr, N)

This built\-in window function evaluates window frames for each row in the same way as the aggregate window function. It returns the result of evaluating the expression expr on the Nth line of the window frame. Rows are numbered from 1 within the window frame in the order defined by the ORDER BY clause, if any. If there is no Nth line in the partition, NULL is returned.

<span id="b76bea82"></span>
### lagInFrame (expr)/lagInFrame (expr, offset)/lagInFrame (expr, offset, default)

`lagInFrame` The first form of the function returns the previous line of the evaluation expression in the window frame `expr` The result of. Or, if there is no previous row (because the current row is the first row), return `NULL`.

If provided `offset` Parameter, it must be a non\-negative integer. In this case, the value returned is before the current line in the window frame `offset` row evaluation expression `expr` The result. If `offset` Is 0, then the current line is calculated `expr`If not before the current row `offset` Row, then return `NULL`.

If it is also provided `default` Parameters, then if `offset` The specified row does not exist, return `default` Instead of `NULL`.

<span id="dd1199cb"></span>
### leadInFrame (expr)/leadInFrame (expr, offset)/leadInFrame (expr, offset, default)

`leadInFrame` The first form of the function returns the next line of the evaluation expression in the window frame `expr` The result of. Or, if there is no next row (because the current row is the last row), return `NULL`.

If provided `offset` Parameter, it must be a non\-negative integer. In this case, the value returned is after the current line in the window frame `offset` row evaluation expression `expr` The result. If `offset` Is 0, then the current line is calculated `expr`If not after the current row `offset` Row, then return `NULL`.

If it is also provided `default` Parameters, then if `offset` The specified row does not exist, return `default` Instead of `NULL`.

<span id="cddecd65"></span>
### nonNegativeDerivative (value)

`nonNegativeDerivative` Function calculation input sequence `value` The difference between adjacent values in, but does not return a negative value. Specifically, if the difference between two adjacent values is positive, it returns the difference; if it is negative or zero, it returns zero.

This function is often used to handle time series data, especially when the data represents a cumulative counter, and it can effectively handle counter reset cases.
