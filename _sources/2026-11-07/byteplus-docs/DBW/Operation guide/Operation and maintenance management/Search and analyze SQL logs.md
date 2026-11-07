---
title: "Search and analyze SQL logs"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/Search_and_analyze_SQL_logs"
---

DBW provides real\-time search and analysis capabilities for collected database audit logs or full SQL log data, supporting second\-level queries on massive log data. It matches log fields with search statements to quickly filter and retrieve target information. Building on log search, DBW offers real\-time data analysis capabilities, performing SQL analysis and calculations based on search results and presenting the findings in analytical charts.

<span id="uj4HgsRE"></span>
## Limitation

<span id="MJIPjTXI"></span>
### Search limitations


|**Limitation** |**Description** |**Remarks** |
|---|---|---|
|Single\-field character count |After log segmentation, each individual term does not exceed 255 bytes in length. |When the limit is exceeded, this log cannot be retrieved via keyword search, but the log data stored on the server remains complete. |
|Search query length |The maximum length of a single query statement is 4,096 characters. |Null |
|Phrase query |Phrase queries select up to 10,000 logs for phrase matching. |Null |
|Query concurrency |The maximum query concurrency is 15. |Null |
|Timeout |The query operation timeout is set to 55 seconds. |Null |
|Fuzzy search |For fuzzy queries, DBW retrieves up to 100 matching terms and returns all logs containing these terms that meet the query conditions. |Null |
|Keyword query |Keyword queries support up to 30 conditions per search. |Null |
|Return results |By default, a maximum of 100 query results are returned per search. |Null |
|Sort query results |By default, logs are displayed starting from the latest, with second or millisecond precision. |Null |
|Single log content display |Due to web browser performance limitations, DBW only performs DOM word segmentation on the first 10,000 characters for logs exceeding 10,000 characters. |If the log exceeds 10,000 characters, the console will display: "This log contains data exceeding 10,000 characters, and some display features may be downgraded." |


<span id="vzZGf4ag"></span>
### Analysis limitations


|**Limitations** |**Description** |
|---|---|
|Data volume |A single Shard can only analyze 1 GiB of data at a time. |
|Search analysis statement length |The maximum length for a single search and analysis statement is 50,000 characters, with the search statement portion limited to 4,096 characters. |
|Field value size |The maximum size for a single field value is 16KB (16,384 bytes). Any content exceeding this limit will not be included in the analysis. |
|Concurrency count |The maximum query concurrency is 15. |
|Data validation mechanism |Analytics only apply to data written after enabling statistics. Fields without statistics enabled display empty SQL analysis results. |
||SQL analysis only applies to data corresponding to the latest version index. Data before index modification is searchable but excluded from SQL analysis. |
|Timeout |The timeout for query operations is 30s. |
|Number of results |By default, 100 results are returned for each analysis.<br><br>To retrieve more data, use the LIMIT syntax, such as `LIMIT n`, which returns the first n rows of the calculation results. The LIMIT syntax supports a maximum of 100,000 returned results. |


<span id="GHTouLB3"></span>
## Fields available for search and analysis

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">Search field names, i.e., the Key in key\-value pairs. All fields listed in the table below are searchable in logs, and case sensitivity is ignored for English letters during search and analysis.</div>


* <div data-tips="true" data-tips-type="default">When searching the <code>query</code> field, the log content can be split using specified delimiters <code>!@#%^&*()-_=\\"', <>/?|;: \n\t\r[]{}</code>.</div>




|**Search field name** |**Field type** |**Available for analysis** |
|---|---|---|
|bytes_sent |long |No |
|client_ip |text |Yes |
|client_port |long |No |
|db_name |text |Yes |
|end_time |long |No |
|exec_error_no |long |Yes |
|exec_time |long |No |
|node_id |text |Yes |
|query |text |No |
|record_id |text |No |
|rows_affected |long |No |
|rows_examined |long |No |
|rows_sent |long |No |
|server_command |text |Yes |
|server_port |long |No |
|session_id |text |No |
|sql_dbs |text |No |
|sql_fingerprint |text |Yes |
|sql_tables |text |Yes |
|sql_template |text |Yes |
|sql_type |text |Yes |
|start_time |long |No |
|user_name |text |Yes |


<span id="LK6k1U4p"></span>
## Search syntax

Filter conditions entered when searching logs; only logs matching the criteria will be returned. Search conditions support various logical and mathematical operators. This article introduces the search syntax supported by DBW's search functionality.

<span id="VumDbhKb"></span>
### Precautions


* Syntax operators are case\-insensitive. For example, `AND` and `and` both represent the logical search operator.

* Logical operations (`AND`,`OR`,`&&`,`！` Operators such as ")" must use half\-width parentheses (`()`) to clarify logical operation precedence; otherwise, search results may not match expectations.

* When multiple search statements are separated by spaces, it represents "AND" logic, equivalent to `AND`. For example, `warning error` is equivalent to `warning AND error`, indicating logs containing both the keywords `warning` and `error`.

* Operators in search syntax are reserved characters in DBW. If search keywords contain these reserved characters, they must be escaped.


<span id="qxyKcSkl"></span>
### Key\-value search method

When entering search conditions, specify the field name and field value. A match occurs if the log's specified field value meets the search criteria. The search statement format is as follows.

```SQL
key1 [ : | > | >= | < | <= | = ] value1 [ [ and | or | not ] key2 [ : | > | >= | < | <= | = ] value2 ]...
```


Here, `key` represents the indexed field. For example, `status:500` searches for access logs where `status` is 500.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">In search statements, if field names or values contain special characters (spaces, Chinese characters, etc.), search operators (and, or, etc.), or index delimiters, they must be enclosed in double quotes (\"\"), e.g., <code>\"cn guilin\"</code>.</div>


* <div data-tips="true" data-tips-type="default">Only fields of type long and double support numeric range queries.</div>


* <div data-tips="true" data-tips-type="default">Key\-value retrieval is only available after enabling key\-value indexing.</div>



<span id="7t7poYw1"></span>
### Search precision

DBW supports exact and fuzzy queries, as detailed in the table below.


|**Search precision** |**Description** |**Example** |
|---|---|---|
|Exact query |Specify complete keywords for exact matching during searches. For example, setting the search condition to GET retrieves logs containing the keyword GET.<br><br>DBW uses tokenization for data retrieval, so exact queries may not be fully precise. For instance, when executing the search query `successful request`, DBW retrieves based on `successful and request`, matching logs containing both `successful` and `request`, rather than the exact phrase `successful request`. |* `region: cn-shanghai`: Query logs where the `region` field value contains `cn-shanghai`.<br><br>* `URL:#\"successful request\"`: Query logs containing the phrase `successful request`.<br><br>* `* \| SELECT * WHERE \"__content__\" LIKE '%Error 2024-06-24%'`: Query logs where the `__content__` field contains the phrase `Error 2024-06-24`. |
|Fuzzy query |When only partial characters of a keyword are specified in the search criteria, i.e., by adding wildcard asterisks (`*`) or question marks (`?`), DBW will match up to 100 qualifying terms and return logs that meet the search criteria and contain any of these 100 terms. For example, the search condition `erro*` queries all logs for 100 terms starting with `erro`, then returns all logs containing these 100 terms and meeting the search criteria.<br><br><br>* The more precise the specified term, the more accurate the query results.<br><br>* When asterisks (`*`) or question marks (`?`) are enclosed in double quotes (<a i=1\>\"\"</a\>), the asterisk (`*`) or question mark (`?`) only represents regular characters and does not support fuzzy matching.<br><br>* Numeric fields (long, double) do not support wildcard characters (\* or ?) for fuzzy queries.`?`) for fuzzy searches. You can query using numeric ranges, such as specifying `age:{20 TO 30}`. |* `TopicID:6d*67`: Query logs containing the field name `TopicID`, where the field value starts with `6d` and ends with `67`.<br><br>* `cn*`: Query logs containing terms that start with `cn`. |


<span id="fbAQpkhN"></span>
### Supported operators

The search operators supported by DBW are listed in the table below.


|**Operators** |**Description** |**Example** |
|---|---|---|
|AND |The AND logical operator, which retrieves the intersection of multiple search results. Use half\-width parentheses `()` to specify the priority of logical operations when multiple operators are involved. |`status:400 AND status:500 Not error` |
|OR |OR logical operator, representing the union of multiple search results. Use half\-width parentheses `()` to specify the priority of logical operations when multiple are involved. |`error OR warning` |
|NOT |The NOT logical operator, which excludes search results containing the keyword following NOT. When specifying multiple logical operations, use half\-width parentheses `()` to clarify the priority of logical operations. |`ERROR AND NOT __path__:\/var\/log\/*` |
|TO |Range logical operator. Add spaces before and after TO.<br><br>If the start value is greater than the end value, they will be automatically swapped. For example, `age:[20 TO 1] ` is equivalent to `age:[1 TO 20] `. |`age:[1 TO 20]` |
|'' |Single quotes: When a string enclosed in single quotes contains preset delimiters, the keywords split by these delimiters have an AND relationship.<br><br>Use Single Quotes`'`Wrapped asterisks`*`and question marks`?`represent wildcards. |`'today is friday'` |
|"" |Double quotes: When a string enclosed in double quotes contains preset delimiters, the keywords split by these delimiters have an AND relationship.<br><br>Use double quotes`"`to enclose asterisks`*`and question marks`?`These symbols do not represent wildcards but are treated as regular characters. |`__hostname__:"Jone Doe"` |
|: |Colon, used for key\-value search to return logs containing the specified Key and Value. |`level:info` |
|\* |Wildcard for fuzzy search. The wildcard \* matches zero, one, or multiple characters.<br><br>Enclose asterisks (`\"\"`) in double quotes (`*`) or question marks (`?`), the asterisk (`*`) or question mark (`?`) Only represents regular characters and does not support fuzzy matching. For example:<br><br><br>* `gu*` matches keywords starting with `gu`.<br><br>* `"gu*"` matches the keyword `gu*`. |`level:erro*` |
|? |Wildcard, indicating a fuzzy search. The wildcard ? can match a single character.<br><br>Use double quotes (`\"\"`) to enclose an asterisk (`*`) or a question mark (`?`) followed by an asterisk (`*`) or question mark (`?`) only represents regular characters and does not support fuzzy matching. For example:<br><br><br>* `gu?n` matches keywords starting with `gu`, ending with`n`, and containing one additional character in between.<br><br>* `"gu?n"` matches the keyword `gu?n`. |`level:erro?` |
|() |Grouping operator, used to control the priority between multiple logical operations. |`((__source__:192.168.10.10 AND status:500) NOT error)` |
|= |Equal sign, used to query logs where the value of a numeric field equals a specified number. Equal sign (`=`) and colon (`:`) serve the same function. |`age=18` |
|\> |A range operator used to query logs where the value of a numeric field is greater than a specified number. |age\>18 |
|\>= |A range operator that queries logs where the value of a numeric field is greater than or equal to a specified number. |`age>=18` |
|< |Range operator, indicating to query logs where the value is less than a specified number in a numeric field. |`age<18` |
|<= |A range operator that queries logs where the value of a numeric field is less than or equal to a specified number. |`age<=18` |
|[] |Range operator that includes boundary values. |`age:[20 TO 30]` |
|{} |Range operator where boundary values are excluded. |`age:{20 TO 30}` |
|\ |Escape character. If the query keywords contain reserved characters, they must be escaped before retrieval. Escaped characters represent the characters themselves, not the keywords.<br><br>Characters that require escaping include `+ - = & \| > < !` `( ) { } [ ] ^ " ~ * ?` `: \ / `。<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Description</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">When using double quotes for search, only escape <code>\" \\ </code>.</div><br><br><br>* <div data-tips="true" data-tips-type="default">When using single quotes for search, only escape <code>' \\ * ?</code>.</div><br> |`__path__:\/images\/log` |


<span id="dkK4jjFL"></span>
## Analysis syntax

On the DBW search analysis page, enter the search analysis statement and specify the log time range and log topic to perform real\-time log search and analysis.

The search analysis statement consists of a search condition and an SQL analysis statement, separated by a pipe symbol (|), indicating analysis and calculation on data filtered by the search condition.

Structure of the search analysis statement:

```SQL
&{Search condition} | &{SQL analysis statement}
```


Including:


* Search criteria: Used to specify filtering rules, indicating analysis and calculations are performed on data filtered by the criteria. Log searches must comply with query syntax, supporting full\-text and key\-value searches. Query precision includes exact and fuzzy searches, or you can use a space or asterisk (`*`) to represent all data.

   When log analysis is not required, simply enter the search criteria.

* SQL analysis statement: Used to specify how query results are analyzed and calculated. Supports various SQL functions and syntax. For details, refer to the [function](https://docs.byteplus.com/en/docs/DBW/Search_and_analyze_SQL_logs#uNkPESpR) and [syntax](https://docs.byteplus.com/en/docs/DBW/Search_and_analyze_SQL_logs#yVeIlOfj) documentation.

   If log data analysis is needed, both search criteria and SQL analysis statements must be entered.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">Typically, the SQL analysis statement does not require a FROM clause, as it defaults to analyzing data from the specified log topic. Exceptions apply to the innermost layer of nested queries, where SELECT statements in nested subqueries must include a FROM clause.</div>


* <div data-tips="true" data-tips-type="default">SQL analysis statements do not support the use of offset, are case\-insensitive, and do not require a semicolon (<code>;</code>) at the end to indicate statement termination.</div>


* <div data-tips="true" data-tips-type="default">In analysis statements, single quotes (<code>''</code>) must be used to enclose string literals, while unquoted or double\-quoted (<code>\"\"</code>) characters represent field or column names. For example, <code>'time'</code> represents a string, while <code>time</code> or <code>\"time\"</code> represents a field or column name.</div>



Example search analysis statements:


|**Analysis scope** |**Search and analysis query examples** |**Description** |
|---|---|---|
|Perform log analysis based on full data |```SQL```<br>```* \| SELECT status, count(*) AS PV GROUP BY status```<br> |Count the number of accesses for different status codes. |
|Perform log analysis based on search results |```SQL```<br>```status:200 \| SELECT COUNT(*) AS PV```<br> |Count visits in requests with a status code of 200. |


<span id="dkK4jjFL"></span>
### Supported analysis functions and syntax

DBW supports various SQL analysis functions and syntax.

<span id="uNkPESpR"></span>
### SQL functions


|**Function** |**Description** |
|---|---|
|[Aggregation functions](https://docs.byteplus.com/en/docs/tls/Aggregate-functions-2) |Performs calculations on a set of values and returns a single value. |
|[Date and time functions](https://docs.byteplus.com/en/docs/tls/Date-and-time-functions-2) |Supports format conversion, grouping, and aggregation of dates and times in logs. |
|[String functions](https://docs.byteplus.com/en/docs/tls/String-functions-2) |Supports splitting strings using specified delimiters. |
|[Regular expression functions](https://docs.byteplus.com/en/docs/tls/Regular-expression-functions-2) |Perform string replacement and other operations using regular expression matching. |
|[Year-over-year and month-over-month functions](https://docs.byteplus.com/en/docs/tls/Period-over-period-comparison-functions) |Calculate year\-over\-year and month\-over\-month comparisons for numerical data. |
|[Mathematical calculation functions](https://docs.byteplus.com/en/docs/tls/Mathematical-calculation-functions-2) |Calculate numerical data. |
|[Mathematical statistical functions](https://docs.byteplus.com/en/docs/tls/Mathematical-statistics-functions-2) |Perform statistical analysis and calculations on numerical values. |
|[Array functions](https://docs.byteplus.com/en/docs/tls/Array_functions) |Parse data in array format. |
|[JSON Functions](https://docs.byteplus.com/en/docs/tls/JSON-functions) |Parse data in JSON format. |
|[IP Functions](https://docs.byteplus.com/en/docs/tls/IP-address-functions-2) |Analyzes information such as city, country, and ISP based on IP addresses. |
|[URL function](https://docs.byteplus.com/en/docs/tls/URL-functions-2) |Supports extraction, encoding, decoding, and other analytical operations in URLs. |
|[Estimation function](https://docs.byteplus.com/en/docs/tls/Approximate-functions-2) |Estimate numerical data. |
|[Binary functions](https://docs.byteplus.com/en/docs/tls/Binary-functions) |Parse binary type data. |
|[Bitwise operation function](https://docs.byteplus.com/en/docs/tls/Bitwise-functions) |Perform bitwise operations like AND, OR, and NOT on binary data. |
|[Geographic Functions](https://docs.byteplus.com/en/docs/tls/Geo-functions) |Perform Geohash encoding on latitude and longitude. |
|[Color function](https://docs.byteplus.com/en/docs/tls/Color-processing-functions) |Supports color functions like BAR and COLOR. |
|Phone number functions |Analyze the location, carrier, and other information of phone numbers in mainland China. |
|[Unit conversion functions](https://docs.byteplus.com/en/docs/tls/Unit-conversion-functions) |Convert units for data volume or time intervals. |
|[Window funnel functions](https://docs.byteplus.com/en/docs/tls/Window-funnel-functions) |Supports querying event chains within a sliding time window and calculating the maximum number of consecutive events in the chain. |
|[Window function](https://docs.byteplus.com/en/docs/tls/Window-functions) |Used for aggregation, sorting, and similar operations. Unlike standard aggregation functions, window functions generate a result for each row of data. |
|[Type conversion function](https://docs.byteplus.com/en/docs/tls/type_conversion_functions) |Convert and view field data types. |
|[Arithmetic operation syntax](https://docs.byteplus.com/en/docs/tls/Arithmetic-operation-syntax-2) |Supports arithmetic operations including addition, subtraction, multiplication, and division. |
|[Comparison operators](https://docs.byteplus.com/en/docs/tls/Comparison-operators-2) |Supports various comparison operators for evaluating value relationships. |
|[Logical operators](https://docs.byteplus.com/en/docs/tls/Logical-operators-2) |Supports AND, OR, and NOT logical operations. |


<span id="yVeIlOfj"></span>
### SQL syntax


|**Syntax** |**Description** |
|---|---|
|[SELECT syntax](https://docs.byteplus.com/en/docs/tls/SELECT-syntax-2) |Select column data from the table, which by default retrieves data matching the filter criteria from the current log topic. |
|[AS syntax](https://docs.byteplus.com/en/docs/tls/AS-syntax-2) |Assign an alias to the specified field name. |
|[GROUP BY syntax](https://docs.byteplus.com/en/docs/tls/GROUP-BY-syntax-2) |Combines with aggregate functions to group query results by one or more fields. |
|[ORDER BY syntax](https://docs.byteplus.com/en/docs/tls/ORDER-BY-syntax-2) |Sort search and analysis results based on specified field names. |
|[LIMIT syntax](https://docs.byteplus.com/en/docs/tls/LIMIT-syntax-2) |Limits the number of data rows returned by a SELECT statement, i.e., the row count of the output result. |
|[DISTINCT clause](https://docs.byteplus.com/en/docs/tls/DISTINCT-clause-2) |Used in the SELECT clause to deduplicate a column. |
|[WHERE syntax](https://docs.byteplus.com/en/docs/tls/WHERE-syntax-2) |Extract logs that meet specified conditions. |
|[Nested subqueries](https://docs.byteplus.com/en/docs/tls/Subqueries-2) |Nest a SELECT statement within another SELECT statement, indicating first performing statistical analysis on the original data via SELECT, then conducting secondary statistical analysis based on the results. |
|[JOIN clause](https://docs.byteplus.com/en/docs/tls/JOIN-clause-2) |Used for join table queries. |
|[UNION clause](https://docs.byteplus.com/en/docs/tls/UNION-clause-2) |Merge analysis results from multiple SELECT clauses. |


<span id="xeWhwI2A"></span>
## Search and analyze logs

After successfully collecting log data and configuring the index correctly, you can view the collected log data in real time in the DBW console and query log data for a specified time range using search criteria. After successfully collecting log data, configuring the index correctly, and enabling statistics for fields, you can perform real\-time log search and analysis in the DBW console using search and analysis statements. This article describes the steps for searching and analyzing logs.

<span id="j2caAUQi"></span>
### Search logs


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the project and region.

3. In the left\-side navigation pane, select **Operation and maintenance management** \> **Observability and diagnostics**.

4. In the upper\-right corner of the **Observability and diagnostics** page, select the database type, such as **RDS for MySQL** or **NDB ** **for MySQL**.

5. In the upper\-left corner of the **Observability and diagnostics** page, click the drop\-down icon and select the target instance.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">You can search for and switch to the target instance by its instance ID.   </div>
   

6. On the target instance page, click **SQL insights and auditing**.

7. Click **SQL** **audit** subtab, and select **Retrieve** ** analyze**.

8. Under the **Retrieve** ** analyze** subtab, specify the search time range.

   The default time range is 5 minutes, but you can customize it. Log data outside the specified query time range will not be retrieved.

9. Specify search or analysis conditions, then click **Search**.

   Click the icon left of the input box to switch between **tap mode** or **statement mode**. In **tap mode**, you can retrieve or analyze SQL logs by **adding filters** or **adding analysis statements**. In **Statement mode**, you can directly input search or analysis statements to retrieve or analyze SQL logs. For keys used in search or analysis, refer to [Fields available for search and analysis](https://docs.byteplus.com/en/docs/DBW/Search_and_analyze_SQL_logs#GHTouLB3).

   * When only searching logs without statistical analysis, simply enter the search criteria. For more information, see [Search syntax](https://docs.byteplus.com/en/docs/DBW/Search_and_analyze_SQL_logs#LK6k1U4p).

   * Empty search criteria indicate querying all logs within the specified time range.

   * A search and analysis statement consists of a search statement and an SQL analysis statement, formatted as `&{search statement} | &{SQL analysis statement}`, which performs data statistics and analysis on results matching the search criteria. For more information, see [Analysis syntax](https://docs.byteplus.com/en/docs/DBW/Search_and_analyze_SQL_logs#dkK4jjFL).


<span id="xciMrBNF"></span>
### View query results

After searching logs, you can view the results in the **Raw log** tab.

Log data is reported approximately every minute. If no real\-time data appears in the **Raw log** tab, wait a minute and refresh to retry.


* #### Log histogram <span id="Eu7NdQkA"></span>

   The log histogram displays the distribution of logs matching the search criteria across different time periods. To hide the histogram, click the hide chart button.

   * Hover over a blue data block to view its time range, the count of matching logs within that period, and whether the search was precise.

   * Click a blue data block to drill down for finer\-grained log distribution, while the **Raw log** tab simultaneously displays the matched Raw log within the specified time range.

   * When the **Query results** are marked as **Precise**, it indicates all matching results within the specified time range have been returned.

   * Duration: Shows the time taken for the current search.

   * Timeout: Occurs when the data volume exceeds processing capacity due to large search ranges, complex syntax, or excessive fields. The page then displays **Timeout**, and we recommend narrowing the time range and retrying the search.

* #### Raw log <span id="3h23WBVa"></span>

   The page defaults to displaying raw log data collected within the last 5 minutes.<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e50389e89c3d78d3e523960967652d3f.png) </span>

   The original log page information is described in the table below.

   
   |**Serial number** |**Description** |
   |---|---|
   |1 |Click **Original** or **Table** to switch log formats. |
   |2 |* Time: Supports sorting logs in ascending or descending order.<br><br>* Line break (only in **raw** format): Enabled by default, **line breaks** display each log field on a separate line for clearer visualization.<br><br>* Compact layout (only for **original** format): When **Compact layout** is enabled, the system will hide the **time** column and display the log time in the **log content** column.<br><br>* Filter preset fields: When **Filter preset fields** is enabled, the system will hide DBW's reserved fields. For detailed descriptions of reserved fields, refer to [Reserved Fields](https://docs.byteplus.com/en/docs/tls/Reserved-fields-2).<br><br>* More configurations:<br><br>   * Filter empty fields: When **Filter empty fields** is enabled, the system will not display fields with empty values.<br><br>   * Use pagination for navigation: Enable **Use pagination for navigation** to browse pages via the pagination control.<br><br>      Each query returns a maximum of 100 logs by default. Up to 100,000 logs can be retrieved through pagination.<br><br>   * Table sorting (only for **table** format): When **Table sorting** is enabled, the table supports frontend single\-page sorting.<br><br>   * Flatten JSON\-type fields: When **Flatten JSON\-type fields** is enabled, the system will display JSON fields in a flattened format (e.g., child_type.kind:\"SERVER\").<br><br>      Only applies to fields with JSON as the index data type.<br><br>   * Tree view for JSON fields: When **Tree view for JSON fields** is checked, the system will display JSON fields in a tree structure.<br><br>      Only applies to fields with JSON as the index data type.<br><br>   * Force JSON field parsing: When **Force JSON field parsing** is checked, the system will forcibly convert logs (JSON, arrays) into JSON format, regardless of index configuration. Highlighting in query results may be disabled.<br><br>   * Batch expand or collapse field values (only in **raw** format): When field values exceed the display length, they are collapsed by default. You can click **Expand** in **More settings** to batch expand all currently collapsed field values. To collapse expanded field values, click **Collapse**. |
   |3 |Click the **expand** icon before the log time to display the **raw log** area, where you can perform the following operations.<br><br><br>* Show or hide specified fields<br><br>   In the **raw log** area, click the eye icon before the target field to show or hide the specified field in the raw log.<br><br>* Copy value<br><br>   In the **raw log** area, click the copy icon before the target field to copy the value of the specified field.<br><br>* Search<br><br>   In the **raw log** area, click the search icon before the target field to use its value as a search condition.<br><br>* Add to search conditions<br><br>   Click the + icon before the target field in the **Raw log** section to add the key\-value pair as a search condition, which will be concatenated to the query with the AND operator.<br><br>   For fields with JSON index data types, check **Flatten JSON fields** to enable one\-click search addition.<br><br>* Remove from search conditions<br><br>   Click the \- icon before the target field in the **Raw log** section to exclude the key\-value pair as a search condition, which will be concatenated to the query with the NOT operator.<br><br>   For fields with JSON index data types, check **Flatten JSON fields** to enable one\-click search exclusion. |
   |4 |* Context query: Click the **Context query** icon for the target log to view its contextual information in the source log file, including several log entries before and after the collection time.<br><br>* Copy: Click the **Copy** icon for the target log to copy a single log entry to the clipboard. The copied log text is in JSON format.<br><br>* Expand or collapse field values: Click the **Expand** or **Collapse** icon for the target log to expand or collapse its field values. |
   |5 |* Copy: Supports copying the entire field value; when field values are split by delimiters, supports copying individual segments.<br><br>* Search: After selecting a field value, click **Search** to add the value to the search query.<br><br>* Add to search criteria: After selecting a field value, click **Add to search criteria** to include the key\-value pair as a search condition, concatenated with the AND operator in the query.<br><br>* Exclude from search results: After selecting a field value, click **Exclude from search results** to add the key\-value pair as a search condition, concatenated with the NOT operator in the query. |
   |6 |* Quick Analysis: Click the field name to quickly analyze the distribution of each value in the field over a recent period.<br><br>   For JSON subfields, the subfield list will only appear in the Quick Analysis section after setting up field indexing for the subfield.<br><br>* Hide or Show Fields: Click the **Hide** icon next to the field name in **Display fields** to hide the field in search results. Click the **Show** icon next to the field name in **Hidden fields** to restore its display.<br><br>* Set Display Order: Drag fields with the mouse to customize their display sequence. When there are many fields, use the search box to quickly locate a specific field. |
   

* #### Sort logs by high\-precision timestamps <span id="ktaWyyMi"></span>

   When collecting logs, enable the nanosecond timestamp precision feature, then select **Nanosecond Search Precision** on the log search and analysis page to sort logs by nanosecond timestamps.


<span id="2dSthnbL"></span>
### View analysis results

If analysis conditions are specified along with search criteria, analysis results can be viewed in the **Chart Analysis** tab.

The page displays query analysis results in table format by default, but you can also specify other statistical charts and configure corresponding chart settings.

The **Query Results** area also displays basic information about the current log analysis, including total log count and query accuracy.


* #### **View analysis data** <span id="RoMqFfZ6"></span>

   The **Query Results** area shows basic information about the current query analysis, such as total log count and result row count, helping you understand the overall context of the analysis.

   
   |**Display items** |**Description** |
   |---|---|
   |Total Logs |Total number of logs matching the search criteria. |
   |Number of result rows |Number of result rows returned by the page. |
   |Limit restriction |Limit on the number of data entries returned. The default is 100. In the search analysis statement, you can specify the number of results to return using the LIMIT statement, such as LIMIT n, which returns the first n rows of data from the calculation results.<br><br>It is recommended to set LIMIT reasonably based on the number of matching rows to avoid returning too much data, which may affect query analysis speed and performance, or returning too little data, making it difficult to overview the results. |
   |Statistical analysis |When statistical analysis is precise, it indicates that all results meeting the criteria within the specified time period have been returned. |
   |Elapsed time |Displays the time taken for this search and analysis. |
   

* #### View analysis charts <span id="mAAMbC91"></span>

   By default, query analysis results are displayed in table format. You can also select more appropriate chart types based on the SQL analysis statement type and analysis purpose to assist data analysis. Currently, DBW supports various analysis chart types including tables, bar charts, line charts, and more. For detailed descriptions, refer to [Statistical Charts](https://docs.byteplus.com/en/docs/tls/chart_overview).
