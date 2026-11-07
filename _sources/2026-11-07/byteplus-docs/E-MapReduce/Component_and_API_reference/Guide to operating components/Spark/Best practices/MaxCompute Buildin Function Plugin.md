---
title: "MaxCompute Buildin Function Plugin"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/MaxCompute_Buildin_Function_Plugin"
---

<span id="2b8ef3be"></span>
## Configuration instructions

The MaxCompute plugin JAR package is released together with the Spark JAR package. To use functions compatible with MaxCompute built\-in functions, add the following configuration.

```SQL
spark.sql.extensions=org.apache.spark.sql.Spark4McExtensions
```


<span id="6df4bd61"></span>
## UDF list


| |Command format |Usage |
|---|---|---|
|SUM |```sql```<br>```--Calculate the aggregate value```<br>```DECIMAL```<br>```--Calculate the sum of expr in the window```<br>```sum([distinct] <expr>) over ([partition_clause]```<br>```[orderby_clause] [frame_clause])```<br> |Calculates the aggregate value.<br><br>DOUBLE |
|COALESCE |```sql```<br>```coalesce(<expr1>, <expr2>, ...)```<br> |Checks the input parameters one by one from left to right. As soon as the first non\-NULL value is found, it returns that value and stops checking the remaining parameters. |
|COUNT |```sql```<br>```-- Calculate the number of records```<br>```bigint count([distinct```<br>```--Calculate the number of records in the window```<br>```bigint count(*) over ([partition_clause]```<br>```[orderby_clause] [frame_clause])```<br>```bigint count([distinct] <expr>[,...]) over```<br>```([partition_clause] [orderby_clause] [frame_clause])```<br> |Calculates the number of records. |
|FIELD |```sql```<br>```T field(struct <s>, string <fieldName>)```<br><br><br>```sql```<br>```--Example```<br>```select (named_struct('f1', 'hello', 'f2', 3).f1)```<br> |Retrieves the value of a member variable in a STRUCT object. |
|SUBSTR |```plain```<br>```string substr(string <str>, bigint <start_position>```<br>```[, bigint <length>])```<br> |Returns the substring of the string **str** starting from `start_position` with a length of `length`. |
|MAX |```plain```<br>```--计算最大值```<br>```max(<colname>)```<br>```--计算窗口中的最大值```<br>```max(<expr>) over([partition_clause] [orderby_clause]```<br>```[frame_clause])```<br> |Calculates the maximum value. |
|INDEX |```plain```<br>```index(<var1>[<var2>])```<br><br><br>```sql```<br>```--Example```<br>```select array('a','b','c')[2];```<br>```select str_to_map("test1=1,test2=2",```<br>```',', ':')["test1"];```<br> |Returns the value in a MAP or List type parameter that meets the specified condition. |
|CONCAT |```plain```<br>```array<T> concat(array<T> <a>, array<T> <b>[,...])```<br>```string concat(string <str1>, string <str2>[,...])```<br> |Concatenates all elements from multiple ARRAYs to generate a new ARRAY, or concatenates multiple strings to generate a new string. |
|GET_JSON_OBJECT |```sql```<br>```string get_json_object(string <json, string <path)```<br> |Extracts a specified string from a standard JSON string according to the specified method. |
|SPLIT_PART |```plain```<br>```string split_part(string <str>, string <separator>,```<br>```bigint <start>[, bigint <end>])```<br> |Splits the string **str** by the delimiter **separator** and returns the substring from the **start** part to the **end** part (inclusive). |
|AVG |```plain```<br>```--计算平均值```<br>```DECIMAL```<br>```--计算窗口中expr的平均值。```<br>```double avg([distinct] double <expr>) over```<br>```([partition_clause] [orderby_clause] [frame_clause])```<br>```decimal avg([distinct] decimal <expr>) over```<br>```([partition_clause] [orderby_clause] [frame_clause])```<br> |Calculates the average value.<br><br>DOUBLE avg() |
|ROUND |```plain```<br>```double```<br>```<decimal_places>])```<br> |Rounds to the specified decimal point position.<br><br>decimal round([, bigint |
|LENGTH |```plain```<br>```bigint length(string <str>)```<br> |Calculates the length of the string **str**.<br><br>**str**: Required. STRING type. If the input is of BIGINT, DOUBLE, DECIMAL, or DATETIME type, it will be implicitly converted to STRING type before calculation. |
|REPLACE |```plain```<br>```string replace(string <str>, string <old>,```<br>```string <new>)```<br> |Replaces substrings in the string that match the specified string with another string.<br><br><br>* **str**: Required. STRING type. The string to be replaced. If the input supports conversion to STRING type, it will be implicitly converted to STRING type for calculation.<br><br>* **old**: Required. The string to be compared.<br><br>* **new**: Required. The string after replacement. |
|TRIM |```plain```<br>```string trim(string <str>[,<trimChars>])```<br>```string trim([BOTH] [<trimChars>] from <str>)```<br> |Removes characters from both ends of the string.<br><br>Removes characters from both ends of **str**:<br><br><br>* If **trimChars** is not specified, spaces are removed by default.<br><br>* If **trimChars** is specified, the characters contained in **trimChars** are treated as a set. The longest substring at both ends of **str** where all characters are in the set **trimChars** will be removed.<br><br>* **str**: Required. STRING type. The string whose characters at both ends are to be removed. If the input is of BIGINT, DECIMAL, DOUBLE, or DATETIME type, it will be implicitly converted to STRING type before calculation.<br><br>* **trimChars**: Optional. String type. The characters to be removed. |
|PERCENTILE_APPROX |```sql```<br>```double percentile_approx (double <colname[, double```<br>```<weight], <p [, <B]))```<br>```--Return multiple approximate percentile calculation results as an array. array<double```<br>```--percentile_approx (double <colname```<br>```   [, double <weight],array(<p1 [, <p2...])```<br>```   [, <B])```<br> |Use the PERCENTILE_APPROX function to calculate approximate percentiles |
|TO_CHAR |```plain```<br>```string to_char(datetime <date>, string <format>)```<br> |Convert a date to a string in the specified format. |
|CEIL |```plain```<br>```bigint ceil(<value>)```<br> |Round up and return the smallest integer that is not less than the input value **value**. |
|MIN |```plain```<br>```--计算最小值```<br>```min(<colname>)```<br>```--计算窗口中的最小值```<br>```min(<expr>) over([partition_clause] [orderby_clause]```<br>```[frame_clause])```<br> |Calculate the minimum value. |
|CONCAT_WS |```plain```<br>```string concat_ws(string <separator>, string <str1>,```<br>```string <str2>[,...])```<br>```string concat_ws(string <separator>, array<string>```<br>```<a>)```<br> |Return the result of joining all strings in the parameters or elements in the ARRAY array using the specified delimiter. |
|SPLIT |```plain```<br>```split(<str>, <pat>, [<trimTailEmpty>])```<br> |Split **str** by **pat** and return an array. |
|REGEXP_EXTRACT |```plain```<br>```string regexp_extract(string <source>, string```<br>```<pattern>[, bigint <groupid>])```<br> |Match the string **source** according to the grouping rules of **pattern**, and return the content matched by the **groupid**th group. |
|REGEXP_SUBSTR |```plain```<br>```string regexp_substr(string <source>, string```<br>```<pattern>[, bigint <start_position>[, bigint```<br>```<occurrence>]])```<br> |Return the substring in **source** that matches the specified **pattern** for the **occurrence**th time, starting from **start_position**. |
|INSTR |```plain```<br>```bigint instr(string <str1>, string <str2>[, bigint```<br>```<start_position>[, bigint <nth_appearance>]])```<br> |Calculate the position of the substring **str2** in the string **str1**. |
|STDDEV_SAMP |```plain```<br>```--计算样本标准差```<br>```double stddev_samp(double <colname>)```<br>```--计算窗口中expr的标准差```<br>```double stddev_samp([distinct] <expr>) over```<br>```([partition_clause] [orderby_clause] [frame_clause])```<br> |Calculate the sample standard deviation. |
|TOLOWER |```plain```<br>```string tolower(string <source>)```<br> |Convert uppercase characters in the string **source** to their corresponding lowercase characters. |
|ARG_MAX |```plain```<br>```arg_max(<valueToMaximize>, <valueToReturn>)```<br> |Return the **valueToReturn** from the row corresponding to the maximum **valueToMaximize**. |
|NAMED_STRUCT |```plain```<br>```struct named_struct(string <name1>, T1 <value1>,```<br>```string <name2>, T2 <value2>[, ...])```<br> |Create a STRUCT using the specified list of **name** and **value**. |
|MD5 |```plain```<br>```string md5(string <str>)```<br> |Calculate the MD5 value of the string **str**. |
|ANY_VALUE |```plain```<br>```any_value(<colname>)```<br> |Return any value within the specified range. |
|NULLIF |```plain```<br>```T nullif(T <expr1>, T <expr2>)```<br> |Compare the values of **expr1** and **expr2**; if they are equal, return NULL, otherwise return **expr1**. |
|EXPLODE |```plain```<br>```explode (<var>)```<br> |Convert a single row of data into multiple rows using a UDTF. |
|LOG |```plain```<br>```double log(<base>, <x>)```<br> |Calculate the logarithm of **x** with base **base**. |
|FROM_UNIXTIME |```sql```<br>```datetime from_unixtime(bigint <unixtime)```<br> |The FROM_UNIXTIME function supports converting numeric UNIX timestamp values to DATETIME type date values. |
|ARRAY |```plain```<br>```array array(<value>,<value>[, ...])```<br> |Construct an ARRAY array using the specified values. |
|COLLECT_SET |```sql```<br>```array collect_set(<colname)```<br> |Aggregate the values of the column specified by **colname** into an array with no duplicate elements. |
|TO_JSON |```sql```<br>```string to_json(<expr)```<br> |Output the given complex type **expr** as a JSON string. |
|ABS |```plain```<br>```bigint```<br> |The BS function supports obtaining the absolute value of the input parameter (number), ensuring the output is always positive or zero.<br><br>double |
|PERCENTILE |```plain```<br>```double percentile(bigint <colname>, <p>)```<br>```--以数组形式返回多个百分位精确计算结果。```<br>```array percentile(bigint <colname>, array(<p1>```<br>```[, <p2>...]))```<br> |Calculate exact percentiles, suitable for small datasets. First sort the specified column in ascending order, then take the exact **p**th percentile. **p** must be between 0 and 1. |
|POW |```plain```<br>```double```<br> |Calculate **x** raised to the power of **y**, that is, `x^y`.<br><br>decimal pow(,) |
|UNIX_TIMESTAMP |```plain```<br>```bigint unix_timestamp(datetime```<br>```string <date>)```<br> |Convert the date **date** to an integer UNIX format date\-time value.<br><br>date |
|ARRAY_JOIN |```plain```<br>```array_join(array<T> <a>, <delimiter>[,```<br>```<nullreplacement>])```<br> |Join the elements in the ARRAY array **a** into a string using **delimiter**. If an element in the array is NULL, use **nullreplacement** as a substitute. If **nullreplacement** is not set, NULL elements are ignored. |
|TOUPPER |```plain```<br>```string toupper(string <source>)```<br> |Convert lowercase characters in the string **source** to their corresponding uppercase characters. |
|SUBSTRING_INDEX |```plain```<br>```string substring_index(string <str>, string```<br>```<separator>, int <count>)```<br> |Extract the substring of **str** before the **count**th delimiter. If **count** is positive, extraction starts from the left. If **count** is negative, extraction starts from the right. |
|COVAR_SAMP |```plain```<br>```double covar_samp(<colname1>, <colname2>)```<br> |Calculates the sample covariance of two specified numeric columns. |
|FLOOR |```plain```<br>```bigint floor(<number>)```<br> |Rounds down and returns the largest integer value less than or equal to **number**. |
|TRANSFORM |```plain```<br>```array<R> transform(array<T> <a>, function<T, R>```<br>```<func>)```<br> |Transforms the elements of ARRAY **a** using **func** and returns a new ARRAY. |
|GREATEST |```plain```<br>```greatest(<var1>, <var2>[,...])```<br> |Compares a set of values and returns the largest value among them. |
|STDDEV |```plain```<br>```--计算总体标准差```<br>```double stddev(double <colname>)```<br>```decimal stddev(decimal <colname>)```<br>```--计算窗口中expr的总体标准差```<br>```double stddev```<br>```([partition_clause] [orderby_clause] [frame_clause])```<br>```decimal stddev```<br>```([partition_clause] [orderby_clause] [frame_clause])```<br> |Calculates the population standard deviation.<br><br>stddev_pop([distinct]) over<br><br>stddev_pop([distinct]) over |
|SIZE |```plain```<br>```int size(array<T> <a>)```<br>```int size(map<K, V> <b> )```<br> |Returns the number of key\-value pairs in the specified MAP or the number of elements in an array. |
|COLLECT_LIST |```sql```<br>```array collect_list(<colname)```<br> |Aggregates the values of the column specified by **colname** into an array. |
|ARG_MIN |```plain```<br>```arg_min(<valueToMinimize>, <valueToReturn>)```<br> |Returns the **valueToReturn** from the row where **valueToMinimize** is minimized. |
|DECODE |```plain```<br>```decode(<expression>, <search>, <result>[, <search>,```<br>```<result>]...[, <default>])```<br><br><br>```plain```<br>```string decode(binary <str, string <charset)```<br> |The DECODE function can implement `if-then-else` branching logic based on parameters, or decode **str** according to the **charset** format. |
|MAP |```plain```<br>```map(K, V) map(K <key1>, V <value1>, K <key2>, V```<br>```<value2>[, ...])```<br> |Generates a MAP using the given key\-value pairs. |
|FROM_JSON |```plain```<br>```from_json(<jsonStr>, <schema>)```<br> |Returns an ARRAY, MAP, or STRUCT type based on the JSON string **jsonStr** and **schema** information. |
|REGEXP_COUNT |```sql```<br>```bigint regexp_count(string <source, string```<br>```<pattern[, bigint <start_position])```<br> |Counts the number of times the specified character appears in the string. |
|FILTER |```sql```<br>```array<T filter(array<T <a, function<T,boolean <func)```<br> |Filters the elements of ARRAY **a** using **func** and returns a new ARRAY. |
|LEAST |```plain```<br>```least(<var1>, <var2>[,...])```<br> |Returns the minimum value among the input parameters. |
|SHIFTLEFT |```plain```<br>```int shiftleft(tinyint```<br>``` <number2>)```<br>```bigint shiftleft(bigint <number1>, int <number2>)```<br> |Bitwise left shift (<<).<br><br>smallint |
|UUID |```plain```<br>```string uuid()```<br> |Returns a random ID |
|ARRAY_MAX |```plain```<br>```T array_max(array<T> <a>)```<br> |Calculates the maximum element in ARRAY **a**. |
|VARIANCE |```plain```<br>```double variance(<colname>)```<br> |Calculates the variance of the specified numeric column. |
|VAR_POP |```plain```<br>```double var_pop(<colname>)```<br> |Calculates the variance of the specified numeric column. |
|ARRAY_CONTAINS |```plain```<br>```boolean array_contains(array<T> <a>, value <v>)```<br> |Determines whether ARRAY **a** contains the element **v**. |
|PARSE_URL |```plain```<br>```string parse_url(string <url>, string <part>[,```<br>```string <key>])```<br> |Parses **url** and extracts information according to **part**. |
|MEDIAN |```plain```<br>```--计算中位数```<br>```double median(double <colname>)```<br>```decimal median(decimal <colname>)```<br>```--计算窗口中expr的中位数。```<br>```median(<expr>) over ([partition_clause]```<br>```[orderby_clause] [frame_clause])```<br> |Calculates the median. |
|MAP_KEYS |```plain```<br>```array<K> map_keys(map<K, V> <a>)```<br> |Generates an ARRAY of all keys in the MAP object **a**. |
|SQRT |```plain```<br>```double```<br> |Calculates the square root of **number**.<br><br>decimal sqrt() |
|REVERSE |```plain```<br>```string```<br> |Returns the reversed string or array.<br><br>array reverse(string |
|STR_TO_MAP |```sql```<br>```str_to_map([string <mapDupKeyPolicy,] <text [,```<br>```<delimiter1 [, <delimiter2]])```<br> |Converts data to MAP format by splitting the target string into key\-value pairs using delimiter 1 (**delimiter1**), then splitting each key\-value pair into key and value using delimiter 2 (**delimiter2**). |
|LOCATE |```plain```<br>```bigint locate(string <substr>, string <str>[, bigint```<br>``` <start_pos>])```<br> |Finds the position of **substr** in **str**. You can specify the starting position for the search using **start_pos**, counting from 1. |
|MAP_VALUES |```plain```<br>```array<V> map_values(map<K, V> <a>)```<br> |Generates an ARRAY of all values in the MAP object **a**. |
|WEEKDAY |```plain```<br>```bigint weekday (datetime <date>)```<br> |Returns the day of the week for the date **date**. |
|VAR_SAMP |```sql```<br>```double var_samp(<colname)```<br> |Calculates the sample variance of the specified numeric column. |
|ARRAY_DISTINCT |```plain```<br>```array<T> array_distinct(array<T> <a>)```<br> |Removes duplicate elements from ARRAY **a**. |
|LPAD |```sql```<br>```string lpad(string <str1, int <length, string <str2)```<br> |Uses the LPAD function to left\-pad **str1** with **str2** until it reaches **length** characters. |
|DATEPART |```plain```<br>```bigint datepart(date```<br>```string <datepart>)```<br> |Extracts the value from **date** that matches the specified time unit **datepart**.<br><br>datetime |
|FIND_IN_SET |```plain```<br>```bigint find_in_set(string <str1>, string <str2>)```<br> |Finds the position of **str1** in the comma\-separated string **str2**, counting from 1. |
|UNIQUE_ID |```plain```<br>```string unique_id()```<br> |Returns a random unique ID |
|ARRAY_POSITION |```plain```<br>```bigint array_position(array<T> <a>, T <element>)```<br> |Calculate the position where the element **element** first appears in the ARRAY **a**. The positions of elements in the ARRAY are numbered from left to right, starting from 1. |
|STRUCT |```plain```<br>```struct struct(<value1>,<value2>[, ...])```<br> |Create a STRUCT using the specified **value** list. |
|TRANSFORM_VALUES |```plain```<br>```map<K, V2> transform_values(map<K, V1> <input>,```<br>```function<K, V1, V2> <func>)```<br> |Transform the input MAP object **input**, keeping the Key unchanged, and calculate the new Value using **func**. |
|POSEXPLODE |```plain```<br>```posexplode(array<T> <a>)```<br> |Expand the ARRAY **a**, with each value occupying a row. Each row contains two columns: the index (starting from 0) and the array element. |
|LOG2 |```plain```<br>```double log2(<number>)```<br> |Return the logarithm of **number** with base 2. |
|HOUR |```plain```<br>```int hour(datetime```<br> |Return the hour part of the date.<br><br>timestamp |
|LN |```plain```<br>```double```<br> |Calculate the natural logarithm of **number**.<br><br>decimal ln() |
|LOG10 |```plain```<br>```double log10(<number>)```<br> |Return the logarithm of **number** with base 10. |
|SLICE |```plain```<br>```array<T> slice(array<T> <a>, <start>, <length>)```<br> |Slice the ARRAY **a** to obtain a new ARRAY consisting of elements starting at **start** position and taking **length** elements. |
|ARRAY_REPEAT |```plain```<br>```array<T> array_repeat(T <element>, int <count>)```<br> |Return an ARRAY with the specified element repeated the specified number of times. |
|YEAR |```plain```<br>```int year(datetime```<br> |Return the year of the date **date**.<br><br>timestamp |
|ARRAY_REDUCE |```plain```<br>```R array_reduce(array<T> <a>, buf <init>, function```<br>```<buf, T, buf> <merge>, function<buf, R> <final>)```<br> |Aggregate the elements in the ARRAY **a**. |
|MAP_ENTRIES |```plain```<br>```array<struct<K, V>> map_entries(map<K, V> <a>):```<br> |Convert the Key and Value mappings of the MAP object **a** into an array of STRUCTs. |
|EXP |```plain```<br>```double```<br> |Calculate the exponential function of **number**.<br><br>decimal exp() |
|SHIFTRIGHT |```plain```<br>```int shiftright(tinyint```<br>``` <number2>)```<br>```bigint shiftright(bigint <number1>, int <number2>)```<br> |Bitwise right shift (\>\>).<br><br>smallint |
|DATE_FORMAT |```sql```<br>```string date_format(date```<br>```string <format)```<br> |DATE_FORMAT supports converting DATE, TIMESTAMP, and STRING types of data into strings in the specified format.<br><br>timestamp |
|REGEXP_EXTRACT_ALL |```plain```<br>```array<T> regexp_extract_all(string <source>, string```<br>```<pattern>[,bigint <group_id>])```<br> |Find all substrings in a string that match the regular expression pattern and return the found substrings as an array. |
|HEX |```plain```<br>```string hex(<number>)```<br> |Convert a numeric value or string to hexadecimal format. |
|TRANSFORM_KEYS |```plain```<br>```map<K2, V> transform_keys([string <mapDupKeyPolicy>,]```<br>``` map<K1, V> <input>, function<K1, V, K2> <func>)```<br> |Transform the MAP object **input**, keeping the Value unchanged, and calculate the new Key using **func**. |
|LASTDAY |```plain```<br>```datetime lastday(datetime <date>)```<br> |Get the last day of the month for **date**, truncated to the day, with the time part as `00:00:00`. |
|TO_MILLIS |```plain```<br>```bigint to_millis(datetime```<br> |Convert the given date **date** to a UNIX timestamp in milliseconds.<br><br>timestamp); |
|MAP_FILTER |```plain```<br>```map<K, V> map_filter(map<K, V> <input>, function```<br>```<K, V, boolean> <predicate>)```<br> |Filter the elements of the MAP object **input**, retaining only those that meet the **predicate** condition. |
|MONTH |```plain```<br>```int month(datetime```<br> |Return the month of a date.<br><br>timestamp |
|WEEKOFYEAR |```plain```<br>```bigint weekofyear (datetime <date>)```<br> |Return the week number of the year for the date **date**. Monday is considered the first day of the week. |
|ARRAY_UNION |```plain```<br>```array<T> array_union(array<T> <a>,  array<T> <b>)```<br> |Calculate the union of ARRAYs **a** and **b**, removing duplicate elements. |
|ARRAY_INTERSECT |```plain```<br>```array<T> array_intersect(array<T> <a>, array<T> <b>)```<br> |Calculate the intersection of two ARRAYs and return a new ARRAY containing the same values present in both arrays. |
|FROM_UTC_TIMESTAMP |```plain```<br>```timestamp from_utc_timestamp({any primitive type}*,```<br>```string <timezone>)```<br> |Convert a timestamp in the UTC time zone to a timestamp in a specified time zone, that is, display a UTC timestamp according to the specified time zone. |
|INLINE |```plain```<br>```inline(array<struct<f1:T1, f2:T2[, ...]>>)```<br> |Expand the given STRUCT array. Each array element corresponds to a row, and each STRUCT element in a row corresponds to a column. |
|ARRAY_MIN |```plain```<br>```T array_min(array<T> <a>)```<br> |Calculates the minimum element in the ARRAY array **a**. |
|QUARTER |```plain```<br>```int quarter (datetime```<br> |Returns the quarter of a date, ranging from 1 to 4.<br><br>timestamp |
|MINUTE |```plain```<br>```int minute(datetime```<br> |Returns the minute part of a date.<br><br>timestamp |
|ARRAY_SORT |```plain```<br>```array<T> array_sort(array<T> <a>, function<T, T,```<br>```bigint> <comparator>)```<br> |Sorts the elements in the ARRAY array **a** according to **comparator**. |
|ARRAY_REMOVE |```plain```<br>```array<T> array_remove(array<T> <a>, T <element>)```<br> |Removes elements equal to **element** from the ARRAY array **a**. |
|CORR |```plain```<br>```double corr(<col1>, <col2>)```<br> |Calculates the Pearson correlation coefficient between two columns of data. |
|<br>---<br><br> |<br>---<br><br> |<br>---<br><br> |
|SUM |```sql```<br>```--Calculate the aggregate value```<br>```DECIMAL```<br>```--Calculate the sum of expr in the window```<br>```sum([distinct] <expr>) over ([partition_clause]```<br>```[orderby_clause] [frame_clause])```<br> |Calculates the sum.<br><br>DOUBLE |
|COALESCE |```sql```<br>```coalesce(<expr1>, <expr2>, ...)```<br> |Checks the input parameters one by one from left to right, and as soon as the first non\-NULL value is found, returns that value immediately without checking the remaining parameters. |
|COUNT |```sql```<br>```-- Calculate the number of records```<br>```bigint count([distinct```<br>```--Calculate the number of records in the window```<br>```bigint count(*) over ([partition_clause]```<br>```[orderby_clause] [frame_clause])```<br>```bigint count([distinct] <expr>[,...]) over```<br>```([partition_clause] [orderby_clause] [frame_clause])```<br> |Calculates the number of records.<br><br>all]) |
|FIELD |```sql```<br>```T field(struct <s>, string <fieldName>)```<br><br><br>```sql```<br>```--Example```<br>```select (named_struct('f1', 'hello', 'f2', 3).f1)```<br> |Retrieves the value of a member variable in a STRUCT object. |
|SUBSTR |```plain```<br>```string substr(string <str>, bigint <start_position>```<br>```[, bigint <length>])```<br> |Returns the substring of string **str** starting from `start_position` **, with a length of** `length`. |
|MAX |```plain```<br>```--计算最大值```<br>```max(<colname>)```<br>```--计算窗口中的最大值```<br>```max(<expr>) over([partition_clause] [orderby_clause]```<br>```[frame_clause])```<br> |Calculates the maximum value. |
|INDEX |```plain```<br>```index(<var1>[<var2>])```<br><br><br>```sql```<br>```--Example```<br>```select array('a','b','c')[2];```<br>```select str_to_map("test1=1,test2=2",```<br>```',', ':')["test1"];```<br> |Returns the value in a MAP or List type parameter that meets the specified condition. |
|CONCAT |```plain```<br>```array<T> concat(array<T> <a>, array<T> <b>[,...])```<br>```string concat(string <str1>, string <str2>[,...])```<br> |Concatenates all elements from multiple ARRAY arrays to generate a new ARRAY array, or concatenates multiple strings to generate a new string. |
|GET_JSON_OBJECT |```sql```<br>```string get_json_object(string <json, string <path)```<br> |Extracts the specified string from a standard JSON string according to the specified method. |
|SPLIT_PART |```plain```<br>```string split_part(string <str>, string <separator>,```<br>```bigint <start>[, bigint <end>])```<br> |Splits string **str** by the separator **separator**, and returns the substring from part **start** to part **end** (inclusive). |
|AVG |```plain```<br>```--计算平均值```<br>```DECIMAL```<br>```--计算窗口中expr的平均值。```<br>```double avg([distinct] double <expr>) over```<br>```([partition_clause] [orderby_clause] [frame_clause])```<br>```decimal avg([distinct] decimal <expr>) over```<br>```([partition_clause] [orderby_clause] [frame_clause])```<br> |Calculates the average value.<br><br>DOUBLE avg() |
|ROUND |```plain```<br>```double```<br>```<decimal_places>])```<br> |Rounds to the specified decimal place.<br><br>decimal round([, bigint |
|LENGTH |```plain```<br>```bigint length(string <str>)```<br> |Calculates the length of string **str**.<br><br>**str**: Required. STRING type. If the input is of type BIGINT, DOUBLE, DECIMAL, or DATETIME, it will be implicitly converted to STRING type before participating in the operation. |
|REPLACE |```plain```<br>```string replace(string <str>, string <old>,```<br>```string <new>)```<br> |Replaces the substring in the string that matches the specified string with another string.<br><br><br>* **str**: Required. STRING type. The string to be replaced. If the input supports conversion to STRING type, it will be implicitly converted to STRING type for the operation.<br><br>* **old**: Required. The string to be compared.<br><br>* **new**: Required. The replaced string. |
|TRIM |```plain```<br>```string trim(string <str>[,<trimChars>])```<br>```string trim([BOTH] [<trimChars>] from <str>)```<br> |Removes characters from both ends of the string.<br><br>Removes characters from both ends of **str**:<br><br><br>* If **trimChars** is not specified, spaces are removed by default.<br><br>* If **trimChars** is specified, the characters contained in **trimChars** are treated as a set, and the longest substring at both ends of **str** where all characters are in the set **trimChars** will be removed.<br><br>* **str**: Required. STRING type. The string whose leading and trailing characters are to be removed. If the input is of BIGINT, DECIMAL, DOUBLE, or DATETIME type, it will be implicitly converted to STRING type before participating in the operation.<br><br>* **trimChars**: Optional. String type. Characters to be removed. |
|PERCENTILE_APPROX |```sql```<br>```double percentile_approx (double <colname[, double```<br>```<weight], <p [, <B]))```<br>```--Return multiple approximate percentile calculation results as an array. array<double```<br>```--percentile_approx (double <colname```<br>```   [, double <weight],array(<p1 [, <p2...])```<br>```   [, <B])```<br> |Use the PERCENTILE_APPROX function to calculate approximate percentiles. |
|TO_CHAR |```plain```<br>```string to_char(datetime <date>, string <format>)```<br> |Convert a date to a string according to the specified format. |
|CEIL |```plain```<br>```bigint ceil(<value>)```<br> |Round up and return the smallest integer not less than the input value **value**. |
|MIN |```plain```<br>```--计算最小值```<br>```min(<colname>)```<br>```--计算窗口中的最小值```<br>```min(<expr>) over([partition_clause] [orderby_clause]```<br>```[frame_clause])```<br> |Calculate the minimum value. |
|CONCAT_WS |```plain```<br>```string concat_ws(string <separator>, string <str1>,```<br>```string <str2>[,...])```<br>```string concat_ws(string <separator>, array<string>```<br>```<a>)```<br> |Return the result of joining all strings in the parameters or elements in the ARRAY array together using the specified delimiter. |
|SPLIT |```plain```<br>```split(<str>, <pat>, [<trimTailEmpty>])```<br> |Split **str** by **pat** and return an array. |
|REGEXP_EXTRACT |```plain```<br>```string regexp_extract(string <source>, string```<br>```<pattern>[, bigint <groupid>])```<br> |Match the string **source** according to the grouping rules of **pattern**, and return the content matched by the **groupid**th group. |
|REGEXP_SUBSTR |```plain```<br>```string regexp_substr(string <source>, string```<br>```<pattern>[, bigint <start_position>[, bigint```<br>```<occurrence>]])```<br> |Return the substring in **source** that matches the specified **pattern** for the **occurrence**th time, starting from position **start_position**. |
|INSTR |```plain```<br>```bigint instr(string <str1>, string <str2>[, bigint```<br>```<start_position>[, bigint <nth_appearance>]])```<br> |Calculate the position of substring **str2** in string **str1**. |
|STDDEV_SAMP |```plain```<br>```--计算样本标准差```<br>```double stddev_samp(double <colname>)```<br>```--计算窗口中expr的标准差```<br>```double stddev_samp([distinct] <expr>) over```<br>```([partition_clause] [orderby_clause] [frame_clause])```<br> |Calculate the sample standard deviation. |
|TOLOWER |```plain```<br>```string tolower(string <source>)```<br> |Convert uppercase characters in the string **source** to their corresponding lowercase characters. |
|ARG_MAX |```plain```<br>```arg_max(<valueToMaximize>, <valueToReturn>)```<br> |Return the **valueToReturn** of the row corresponding to the maximum **valueToMaximize**. |
|NAMED_STRUCT |```plain```<br>```struct named_struct(string <name1>, T1 <value1>,```<br>```string <name2>, T2 <value2>[, ...])```<br> |Create a STRUCT using the specified list of **name** and **value**. |
|MD5 |```plain```<br>```string md5(string <str>)```<br> |Calculate the MD5 value of the string **str**. |
|ANY_VALUE |```plain```<br>```any_value(<colname>)```<br> |Return any value within the specified range. |
|NULLIF |```plain```<br>```T nullif(T <expr1>, T <expr2>)```<br> |Compare the values of **expr1** and **expr2**; if they are equal, return NULL, otherwise return **expr1**. |
|EXPLODE |```plain```<br>```explode (<var>)```<br> |Convert a single row of data into multiple rows using a UDTF. |
|LOG |```plain```<br>```double log(<base>, <x>)```<br> |Calculate the logarithm of **x** with base **base**. |
|FROM_UNIXTIME |```sql```<br>```datetime from_unixtime(bigint <unixtime)```<br> |The FROM_UNIXTIME function supports converting numeric UNIX time date values to DATETIME type date values. |
|ARRAY |```plain```<br>```array array(<value>,<value>[, ...])```<br> |Construct an ARRAY array using the specified values. |
|COLLECT_SET |```sql```<br>```array collect_set(<colname)```<br> |Aggregate the values of the column specified by **colname** into an array with no duplicate elements. |
|TO_JSON |```sql```<br>```string to_json(<expr)```<br> |Output the given complex type **expr** as a JSON string. |
|ABS |```plain```<br>```bigint```<br> |The ABS function supports obtaining the absolute value of the input parameter (number), ensuring the output is always positive or zero.<br><br>double |
|PERCENTILE |```plain```<br>```double percentile(bigint <colname>, <p>)```<br>```--以数组形式返回多个百分位精确计算结果。```<br>```array percentile(bigint <colname>, array(<p1>```<br>```[, <p2>...]))```<br> |Calculate the exact percentile, suitable for small datasets. First sort the specified column in ascending order, then take the exact **p**th percentile. **p** must be between 0 and 1. |
|POW |```plain```<br>```double```<br> |Calculate **x** to the power of **y**, that is, `x^y`.<br><br>decimal pow(,) |
|UNIX_TIMESTAMP |```plain```<br>```bigint unix_timestamp(datetime```<br>```string <date>)```<br> |Convert the date **date** to an integer UNIX format date\-time value.<br><br>date |
|ARRAY_JOIN |```plain```<br>```array_join(array<T> <a>, <delimiter>[,```<br>```<nullreplacement>])```<br> |Join the elements in the ARRAY array **a** into a string using **delimiter**. If an element in the array is NULL, use **nullreplacement** as a replacement. If **nullreplacement** is not set, NULL elements will be ignored. |
|TOUPPER |```plain```<br>```string toupper(string <source>)```<br> |Convert the lowercase characters in the string **source** to their corresponding uppercase characters. |
|SUBSTRING_INDEX |```plain```<br>```string substring_index(string <str>, string```<br>```<separator>, int <count>)```<br> |Extract the substring of **str** before the **count**th delimiter. If **count** is positive, extraction starts from the left. If **count** is negative, extraction starts from the right. |
|COVAR_SAMP |```plain```<br>```double covar_samp(<colname1>, <colname2>)```<br> |Calculate the sample covariance of the specified two numeric columns. |
|FLOOR |```plain```<br>```bigint floor(<number>)```<br> |Round down and return the largest integer value less than or equal to **number**. |
|TRANSFORM |```plain```<br>```array<R> transform(array<T> <a>, function<T, R>```<br>```<func>)```<br> |Transform the elements of the ARRAY **a** using **func** and return a new ARRAY. |
|GREATEST |```plain```<br>```greatest(<var1>, <var2>[,...])```<br> |Compares a set of values and returns the largest value among them. |
|STDDEV |```plain```<br>```--计算总体标准差```<br>```double stddev(double <colname>)```<br>```decimal stddev(decimal <colname>)```<br>```--计算窗口中expr的总体标准差```<br>```double stddev```<br>```([partition_clause] [orderby_clause] [frame_clause])```<br>```decimal stddev```<br>```([partition_clause] [orderby_clause] [frame_clause])```<br> |Calculate the population standard deviation.<br><br>stddev_pop([distinct]) over<br><br>stddev_pop([distinct]) over |
|SIZE |```plain```<br>```int size(array<T> <a>)```<br>```int size(map<K, V> <b> )```<br> |Return the number of key\-value pairs in the specified MAP or the number of elements in an array. |
|COLLECT_LIST |```sql```<br>```array collect_list(<colname)```<br> |Aggregate the values of the column specified by **colname** into an array. |
|ARG_MIN |```plain```<br>```arg_min(<valueToMinimize>, <valueToReturn>)```<br> |Return the **valueToReturn** of the row where **valueToMinimize** is minimized. |
|DECODE |```plain```<br>```decode(<expression>, <search>, <result>[, <search>,```<br>```<result>]...[, <default>])```<br><br><br>```plain```<br>```string decode(binary <str, string <charset)```<br> |The DECODE function can implement `if-then-else` branch selection based on parameters, or decode **str** according to the **charset** format. |
|MAP |```plain```<br>```map(K, V) map(K <key1>, V <value1>, K <key2>, V```<br>```<value2>[, ...])```<br> |Generate a MAP using the given key\-value pairs. |
|FROM_JSON |```plain```<br>```from_json(<jsonStr>, <schema>)```<br> |Return an ARRAY, MAP, or STRUCT type based on the JSON string **jsonStr** and **schema** information. |
|REGEXP_COUNT |```sql```<br>```bigint regexp_count(string <source, string```<br>```<pattern[, bigint <start_position])```<br> |Count the number of occurrences of the specified character in the string. |
|FILTER |```sql```<br>```array<T filter(array<T <a, function<T,boolean <func)```<br> |Filter the elements of the ARRAY **a** using **func** and return a new ARRAY. |
|LEAST |```plain```<br>```least(<var1>, <var2>[,...])```<br> |Return the minimum value among the input parameters. |
|SHIFTLEFT |```plain```<br>```int shiftleft(tinyint```<br>``` <number2>)```<br>```bigint shiftleft(bigint <number1>, int <number2>)```<br> |Bitwise left shift (<<).<br><br>smallint |
|UUID |```plain```<br>```string uuid()```<br> |Return a random ID |
|ARRAY_MAX |```plain```<br>```T array_max(array<T> <a>)```<br> |Calculate the maximum element in the ARRAY **a**. |
|VARIANCE |```plain```<br>```double variance(<colname>)```<br> |Calculate the variance of the specified numeric column. |
|VAR_POP |```plain```<br>```double var_pop(<colname>)```<br> |Calculate the variance of the specified numeric column. |
|ARRAY_CONTAINS |```plain```<br>```boolean array_contains(array<T> <a>, value <v>)```<br> |Determine whether the ARRAY **a** contains the element **v**. |
|PARSE_URL |```plain```<br>```string parse_url(string <url>, string <part>[,```<br>```string <key>])```<br> |After parsing **url**, extract information according to **part**. |
|MEDIAN |```plain```<br>```--计算中位数```<br>```double median(double <colname>)```<br>```decimal median(decimal <colname>)```<br>```--计算窗口中expr的中位数。```<br>```median(<expr>) over ([partition_clause]```<br>```[orderby_clause] [frame_clause])```<br> |Calculate the median. |
|MAP_KEYS |```plain```<br>```array<K> map_keys(map<K, V> <a>)```<br> |Generate an ARRAY of all keys in the MAP object **a**. |
|SQRT |```plain```<br>```double```<br> |Calculate the square root of **number**.<br><br>decimal sqrt() |
|REVERSE |```plain```<br>```string```<br> |Return the reversed string or array.<br><br>array reverse(string |
|STR_TO_MAP |```sql```<br>```str_to_map([string <mapDupKeyPolicy,] <text [,```<br>```<delimiter1 [, <delimiter2]])```<br> |Convert data to MAP format by splitting the target string into key\-value pairs using delimiter 1 (**delimiter1**), then splitting each key\-value pair into key and value using delimiter 2 (**delimiter2**). |
|LOCATE |```plain```<br>```bigint locate(string <substr>, string <str>[, bigint```<br>``` <start_pos>])```<br> |Find the position of **substr** in **str**. You can specify the starting position for the search using **start_pos**, counting from 1. |
|MAP_VALUES |```plain```<br>```array<V> map_values(map<K, V> <a>)```<br> |Generate an ARRAY of all values in the MAP object **a**. |
|WEEKDAY |```plain```<br>```bigint weekday (datetime <date>)```<br> |Return the day of the week for **date** in the current week. |
|VAR_SAMP |```sql```<br>```double var_samp(<colname)```<br> |Calculate the sample variance of the specified numeric column. |
|ARRAY_DISTINCT |```plain```<br>```array<T> array_distinct(array<T> <a>)```<br> |Remove duplicate elements from the ARRAY **a**. |
|LPAD |```sql```<br>```string lpad(string <str1, int <length, string <str2)```<br> |Use the LPAD function to pad **str1** to the left with **str2** until it reaches **length** characters. |
|DATEPART |```plain```<br>```bigint datepart(date```<br>```string <datepart>)```<br> |Extract the value from the date **date** that matches the specified time Unit **datepart**.<br><br>datetime |
|FIND_IN_SET |```plain```<br>```bigint find_in_set(string <str1>, string <str2>)```<br> |Find the position of the string **str1** in the comma\-separated string **str2**, counting from 1. |
|UNIQUE_ID |```plain```<br>```string unique_id()```<br> |Return a random unique ID. |
|ARRAY_POSITION |```plain```<br>```bigint array_position(array<T> <a>, T <element>)```<br> |Calculate the first occurrence position of the element **element** in the ARRAY array **a**. ARRAY array element positions are numbered from left to right, starting from 1. |
|STRUCT |```plain```<br>```struct struct(<value1>,<value2>[, ...])```<br> |Create a STRUCT using the specified **value** list. |
|TRANSFORM_VALUES |```plain```<br>```map<K, V2> transform_values(map<K, V1> <input>,```<br>```function<K, V1, V2> <func>)```<br> |Transform the input MAP object **input**, keeping the Key unchanged, and calculate the new Value using **func**. |
|POSEXPLODE |```plain```<br>```posexplode(array<T> <a>)```<br> |Expand the ARRAY array **a**, with each Value in a row; each row contains two columns corresponding to the array index starting from 0 and the array element. |
|LOG2 |```plain```<br>```double log2(<number>)```<br> |Return the logarithm of **number** with base 2. |
|HOUR |```plain```<br>```int hour(datetime```<br> |Return the hour part of the date.<br><br>timestamp |
|LN |```plain```<br>```double```<br> |Calculate the natural logarithm of **number**.<br><br>decimal ln() |
|LOG10 |```plain```<br>```double log10(<number>)```<br> |Return the logarithm of **number** with base 10. |
|SLICE |```plain```<br>```array<T> slice(array<T> <a>, <start>, <length>)```<br> |Slice the ARRAY array, extracting elements starting from **start** with a length of **length** to form a new ARRAY array. |
|ARRAY_REPEAT |```plain```<br>```array<T> array_repeat(T <element>, int <count>)```<br> |Return an ARRAY array with the specified element repeated the specified number of times. |
|YEAR |```plain```<br>```int year(datetime```<br> |Return the year of the date **date**.<br><br>timestamp |
|ARRAY_REDUCE |```plain```<br>```R array_reduce(array<T> <a>, buf <init>, function```<br>```<buf, T, buf> <merge>, function<buf, R> <final>)```<br> |Aggregate the elements in the ARRAY array **a**. |
|MAP_ENTRIES |```plain```<br>```array<struct<K, V>> map_entries(map<K, V> <a>):```<br> |Convert the Key and Value mapping of the MAP object **a** into an array of STRUCT structures. |
|EXP |```plain```<br>```double```<br> |Calculate the exponential function of **number**.<br><br>decimal exp() |
|SHIFTRIGHT |```plain```<br>```int shiftright(tinyint```<br>``` <number2>)```<br>```bigint shiftright(bigint <number1>, int <number2>)```<br> |Bitwise right shift (\>\>).<br><br>smallint |
|DATE_FORMAT |```sql```<br>```string date_format(date```<br>```string <format)```<br> |DATE_FORMAT supports converting DATE, TIMESTAMP, and STRING types of data into a string in the specified format.<br><br>timestamp |
|REGEXP_EXTRACT_ALL |```plain```<br>```array<T> regexp_extract_all(string <source>, string```<br>```<pattern>[,bigint <group_id>])```<br> |Find all substrings in the string that match the regular expression pattern and return the found substrings as an array. |
|HEX |```plain```<br>```string hex(<number>)```<br> |Convert a numeric value or string to hexadecimal format. |
|TRANSFORM_KEYS |```plain```<br>```map<K2, V> transform_keys([string <mapDupKeyPolicy>,]```<br>``` map<K1, V> <input>, function<K1, V, K2> <func>)```<br> |Transform the MAP object **input**, keeping the Value unchanged, and calculate the new Key using **func**. |
|LASTDAY |```plain```<br>```datetime lastday(datetime <date>)```<br> |Get the last day of the month for **date**, truncated to the day, with the hour, minute, and second part as `00:00:00`. |
|TO_MILLIS |```plain```<br>```bigint to_millis(datetime```<br> |Convert the given date **date** to a UNIX timestamp in milliseconds.<br><br>timestamp); |
|MAP_FILTER |```plain```<br>```map<K, V> map_filter(map<K, V> <input>, function```<br>```<K, V, boolean> <predicate>)```<br> |Filter the elements of the MAP object **input**, retaining only those elements that meet the **predicate** condition. |
|MONTH |```plain```<br>```int month(datetime```<br> |Return the month of a date.<br><br>timestamp |
|WEEKOFYEAR |```plain```<br>```bigint weekofyear (datetime <date>)```<br> |Return the week number of the year for the date **date**. Monday is considered the first day of the week. |
|ARRAY_UNION |```plain```<br>```array<T> array_union(array<T> <a>,  array<T> <b>)```<br> |Calculate the union of ARRAY arrays **a** and **b**, removing duplicate elements. |
|ARRAY_INTERSECT |```plain```<br>```array<T> array_intersect(array<T> <a>, array<T> <b>)```<br> |Calculate the intersection of two ARRAY arrays and return a new array containing the values present in both arrays. |
|FROM_UTC_TIMESTAMP |```plain```<br>```timestamp from_utc_timestamp({any primitive type}*,```<br>```string <timezone>)```<br> |Convert a timestamp in the UTC time zone to a timestamp in a specified time zone, that is, display a UTC timestamp according to the specified time zone. |
|INLINE |```plain```<br>```inline(array<struct<f1:T1, f2:T2[, ...]>>)```<br> |Expand the given STRUCT array. Each array element corresponds to a row, and each STRUCT element in a row corresponds to a column. |
|ARRAY_MIN |```plain```<br>```T array_min(array<T> <a>)```<br> |Calculate the minimum element in the ARRAY array **a**. |
|QUARTER |```plain```<br>```int quarter (datetime```<br> |Return the quarter of a date, ranging from 1 to 4.<br><br>timestamp |
|MINUTE |```plain```<br>```int minute(datetime```<br> |Return the value of the minute part of a date.<br><br>timestamp |
|ARRAY_SORT |```plain```<br>```array<T> array_sort(array<T> <a>, function<T, T,```<br>```bigint> <comparator>)```<br> |Sort the elements in the ARRAY array **a** according to **comparator**. |
|ARRAY_REMOVE |```plain```<br>```array<T> array_remove(array<T> <a>, T <element>)```<br> |Remove elements equal to **element** from the ARRAY array **a**. |
|CORR |```plain```<br>```double corr(<col1>, <col2>)```<br> |Calculate the Pearson correlation coefficient for two columns of data. |
|ASCII |```plain```<br>```bigint ascii(string <str>)```<br> |Return the ASCII code of the first character in the string **str**. |
|DAY |```plain```<br>```int day(datetime```<br> |Return the day of a date.<br><br>timestamp |
|CHR |```plain```<br>```string chr(bigint <ascii>)```<br> |Convert the specified ASCII code to a character. |
|ASCII |```plain```<br>```bigint ascii(string <str>)```<br> |Return the ASCII code of the first character in the string **str**. |
|DAY |```plain```<br>```int day(datetime```<br> |Return the day of a date.<br><br>timestamp |
|CHR |```plain```<br>```string chr(bigint <ascii>)```<br> |Convert the specified ASCII code to a character. |
