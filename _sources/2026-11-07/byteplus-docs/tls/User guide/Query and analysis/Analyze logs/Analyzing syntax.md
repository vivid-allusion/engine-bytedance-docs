---
title: "Analyzing syntax"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Analyzing_Grammar"
---

TLS supports various types of SQL functions and syntax.

<span id="fjbaVnnL"></span>
### SQL functions


|Function |Description |
|---|---|
|[Aggregate functions](https://docs.byteplus.com/docs/tls/Aggregate-functions-2) |Calculates a group of values and returns a single value. |
|[Date and time functions](https://docs.byteplus.com/docs/tls/Date-and-time-functions-2) |Converts the format of date and time values in logs and aggregates the results by group. |
|[String functions](https://docs.byteplus.com/docs/tls/String-functions-2) |Splits a string using a specified delimiter. |
|[Regular expression functions](https://docs.byteplus.com/docs/tls/Regular-expression-functions-2) |Replaces a string with another string using a regular expression. |
|[Period-over-period comparison functions](https://docs.byteplus.com/docs/tls/Period-over-period-comparison-functions) |Performs year\-over\-year and month\-over\-month comparisons on numerical data. |
|[Mathematical calculation functions](https://docs.byteplus.com/docs/tls/Mathematical-calculation-functions-2) |Calculates numerical data. |
|[Mathematical statistics functions](https://docs.byteplus.com/docs/tls/Mathematical-statistics-functions-2) |Performs statistical analysis and calculations on numerical data. |
|[Array functions](https://docs.byteplus.com/docs/tls/Array_functions) |Parses data in array format. |
|[Map functions](https://docs.byteplus.com/docs/tls/Map-function) |Parses data in map format. |
|[JSON functions](https://docs.byteplus.com/docs/tls/JSON-functions) |Parses data in JSON format. |
|[IP address functions](https://docs.byteplus.com/docs/tls/IP-address-functions-2) |Returns information such as the city, country, and internet service provider (ISP) based on an IP address. |
|[URL functions](https://docs.byteplus.com/docs/tls/URL-functions-2) |Extracts, encodes, and decodes data from a URL. |
|[Approximate functions](https://docs.byteplus.com/docs/tls/Approximate-functions-2) |Calculates the approximations of numerical data. |
|[Binary functions](https://docs.byteplus.com/docs/tls/Binary-functions) |Parses data in binary format. |
|[Bitwise functions](https://docs.byteplus.com/docs/tls/Bitwise-functions) |Performs bitwise operations such as AND, OR, and NOT on binary data. |
|[Geo functions](https://docs.byteplus.com/docs/tls/Geo-functions) |Encodes latitude and longitude data using Geohash. |
|[Color processing functions](https://docs.byteplus.com/docs/tls/Color-processing-functions) |Supports color functions such as BAR and COLOR. |
|[Unit conversion functions](https://docs.byteplus.com/docs/tls/Unit-conversion-functions) |Converts the unit of data volume or time interval. |
|[Window funnel functions](https://docs.byteplus.com/docs/tls/Window-funnel-functions) |Supports querying event chains within a sliding time window and calculating the maximum number of consecutive events occurring within the event chain. |
|[Window functions](https://docs.byteplus.com/docs/tls/Window-functions) |Used for aggregation, sorting, and other operations. Unlike ordinary aggregate functions, window functions support generating a result for each row of data. |
|[Type conversion functions](https://docs.byteplus.com/docs/tls/Type-conversion-functions) |Converts and view the data type of fields. |
|[Arithmetic operation syntax](https://docs.byteplus.com/docs/tls/Arithmetic-operation-syntax-2) |Performs arithmetic operations such as add, subtract, multiply, and divide. |
|[Comparison operators](https://docs.byteplus.com/docs/tls/Comparison-operators-2) |Supports multiple comparison operators to compare values. |
|[Logical operators](https://docs.byteplus.com/docs/tls/Logical-operators-2) |Supports AND, OR, and NOT operations. |


<span id="V0q5OnCs"></span>
### SQL syntax


|Syntax |Description |
|---|---|
|[SELECT syntax](https://docs.byteplus.com/docs/tls/SELECT-syntax-2) |Selects columns from tables. By default, the statement selects data that meets the query condition from the current topic. |
|[WHERE syntax](https://docs.byteplus.com/docs/tls/WHERE-syntax-2) |Extract the logs that meet the specified conditions. |
|[AS syntax](https://docs.byteplus.com/docs/tls/AS-syntax-2) |Specifies an alias for a field. |
|[GROUP BY syntax](https://docs.byteplus.com/docs/tls/GROUP-BY-syntax-2) |Works with an aggregate function to group the query and analysis results based on one or more fields. |
|[ORDER BY syntax](https://docs.byteplus.com/docs/tls/ORDER-BY-syntax-2) |Sorts the query and analysis results based on a specified field. |
|[LIMIT syntax](https://docs.byteplus.com/docs/tls/LIMIT-syntax-2) |Limits the number of rows of data to be returned by the SELECT statement. |
|[DISTINCT clause](https://docs.byteplus.com/docs/tls/DISTINCT-clause-2) |Works in a SELECT statement to remove duplicate values from a column. |
|[JOIN clause](https://docs.byteplus.com/docs/tls/JOIN-clause-2) |Combines columns from one or more tables. |
|[UNION clause](https://docs.byteplus.com/docs/tls/UNION-clause-2) |Combines the analysis results from multiple SELECT statements. |
|[Having clause](https://docs.byteplus.com/docs/tls/Having-clause-2) |filters out group results that meet specific conditions. |
|[Subqueries](https://docs.byteplus.com/docs/tls/Subqueries-2) |Nests a SELECT statement into another SELECT statement to conduct statistical analysis on raw data and then conduct secondary statistical analysis on the results. |
