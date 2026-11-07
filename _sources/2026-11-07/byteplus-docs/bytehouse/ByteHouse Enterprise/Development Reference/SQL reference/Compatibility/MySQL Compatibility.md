---
title: "MySQL Compatibility"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/mysql-compatibility"
---

Starting from version 2.4.0, ByteHouse Enterprise Edition added compatibility with MySQL 5.7 and MySQL 8.0, including commonly used features and syntax, enabling seamless integration with MySQL client applications and tools. This allows users to interact with ByteHouse Enterprise Edition using the familiar MySQL protocol and leverage the functions of the MySQL ecosystem.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Please use this feature with ByteHouse version 2.4 or higher, and it is advisable to upgrade to the latest version for better support.</div>


<div data-tips="true" data-tips-type="tip">Upgrade method: <strong>BytePlus Console</strong> \> \*\*\*\* <strong>Clusters management</strong> \> <strong>Cluster</strong> <strong>list</strong> \> <strong>Cluster</strong> <strong>Name</strong> \> <strong>Basic Information</strong> \> <strong>Engine</strong> \> <strong>Upgrade.</strong></div>


<div data-tips="true" data-tips-type="tip"><img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5383e8d0de9b45cfb0d330004d3db245~tplv-goo7wpa0wc-image.image" width="2102px" /></div>


<span id="f548477a"></span>
## Protocol Compatibility

<span id="0f1260b2"></span>
### Connecting using MySQL Client Command Line


1. If you have installed the MySQL client, you can connect to ByteHouse using the following syntax.

   ```SQL
   --Access, the default port is 9004 
   mysql --protocol tcp -h [hostname] -u [username] -P [port_number] --password=[password]
   
   -- Example
   mysql --protocol tcp -h 7277767706697666852-public.bytehouse-ce.bytepluses.com -u bytehouse_test -P 9004 --password=XXXXXX
   ```
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/69712baa9c37440e90817070ee3755cb~tplv-goo7wpa0wc-image.image) </span>

2. After successfully connecting to the ByteHouse cluster, you can query existing databases with the reference statement below.

   ```PHP
   show databases;
   ```
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8d9557ddd8044d559442df8912041c9e~tplv-goo7wpa0wc-image.image) </span>


<span id="75b5f539"></span>
### Connecting through ClickHouse Client Command Line

You can refer to [ClickHouse Client](https://docs.byteplus.com/docs/bytehouse/clickhouse-client) to learn how to connect to ByteHouse and using MySQL syntax to operate ByteHouse.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6695e24427cb441ea0cc65d62dac39bc~tplv-goo7wpa0wc-image.image) </span>

<span id="bd7e04d4"></span>
## Grammar Compatibility

<span id="af6c28ce"></span>
### Support but mode settings required

Some MySQL functions conflict with functions of the same name in ClickHouse mode.

Therefore, when using, it is necessary to set `dialect_type='MYSQL'`, as shown in the following example:

```PHP
select adddate('2022-01-22',interval '3' day) settings dialect_type='MYSQL';
```


Queries that currently need a dialect setting to be used include, but are not limited to:


1. Function Function

   1. adddate

   2. date_sub

   3. subdate

   4. concat_ws

   5. format AS

2. DQL：

   1. union except


<span id="3fad1e84"></span>
### Detailed explanation of features that differ from MySQL


1. locate: The computing logic of ByteHouse Corporate Edition differs from MySQL, so settings are required to maintain consistency

2. cast: Under MySQL mode, the return values of some functions differ from those under ClickHouse mode (mainly due to differences in default types); some will cause errors under ClickHouse mode. As

   1. Return value differs:

      1. `SELECT cast(4.3 AS boolean);`

   2. Error:

      1. `SELECT cast('a' AS boolean);`

      2. `SELECT cast( 'China' AS decimal(5,2));`

      3. `SELECT cast('China' AS smallint);`

      4. `SELECT cast('a' AS bigint);`

      5. `SELECT cast(date '2021-09-18' AS bigint);`

      6. `SELECT cast( date '2021-09-17' AS double);`

      7. `SELECT cast(timestamp '2001-1-22' AS time);`

3. In the case of empty results, ClickHouse mode returns NaN, while MySQL returns NULL, as the default types in the avg function differ.

4. The default numerical values for min and max in ByteHouse are 0, whereas in MySQL they are NULL, leading to discrepancies in the min and max results between the two.


<span id="707fbe97"></span>
### There are no plans currently to support this issue.


1. The log function does not support usage with two parameters.

   1. MySQL supports this.

   2. ByteHouse can use log_with_base as an alternative.

2. The range of results for the rand function.

   1. MySQL returns a range of 0 to 1.

   2. On ByteHouse, use randCanonical() to return random numbers in the range [0,1).

3. Differences in the round function.

   1. ByteHouse omits trailing zeros in results; for example, `SELECT round(345.983,1);` returns 346 in ByteHouse and 346.0 in MySQL.

4. Syntax error if the curdate function is used without parentheses.

   1. MySQL supports this.

   2. When using `select curdate`, an error occurs; ByteHouse requires parentheses `select curdate();`

5. The date_format function differs.

   1. In ByteHouse, dateformat is occupied so date_format_mysql can replace date_format;

6. Parameters of some non\-standard usages are not supported, such as:

   1. Non\-standard usage of yyyy\-mm\-dd: `select datediff('2022-01-22 23:59:59','2022-1-21') settings dialect_type='MYSQL';`

   2. Non\-standard usage of hh\-mm\-ss: `select subtime('2022-10-31 23:59:59','0:1:1');`

7. The return value of the dayofweek function differs.

   1. Under ClickHouse dialect, it is consistent with ClickHouse; under MySQL dialect, it is the same as the return values of MySQL and adb;

8. The format of the return value of localtime differs.

   1. MySQL returns year month day+time; ByteHouse only returns time, and ClickHouse's time includes three decimal places;

   2. ByteHouse can use localtimestamp() as a substitute.

9. Time functions have a different time range compared to MySQL when calculating time.

   1. Currently, time only supports 00:00:00 \- 23:59:59; MySQL will return a negative value, ByteHouse will not return a negative value.

   2. For example

      1. `select maketime(-1,15,30);`

      2. `select sec_to_time(86401);`

      3. `select subtime(date '2022-10-31','00:01:01');`

      4. `select subtime(time '02:12:59','10:13:01');`

      5. `select timediff(time '12:09:11','13:59:30');`

      6. `select timediff(time '12:09:10',time '12:56:34');`

10. Missing validity checks for some abnormal time values

11. `select minute('2022-02-03 10:61:03');`

12. The return value of time_format differs

13. For example, `select time_format(date '2022-01-22','%H %k %h %I %l')`; MySQL uses %k for 0...23, while ours is 00...23

14. Default timezone differences result in differing return values for some functions

15. `SELECT to_seconds('2022-02-02');`

16. `select to_seconds('2022-02-02 09:09:00');`

17. `select to_seconds(timestamp '2022-02-02 09:09:00');`

18. `select to_seconds(time '09:09:00');`

19. The return value of the bin function differs

20. In ClickHouse, there are additional prefixes compared to MySQL, such as `SELECT bin(12);`

21. Some functions in MySQL involve an additional hex conversion layer compared to ByteHouse, such as

22. `SELECT char(97,110,97,108,121,116,105,99,100,98);`

23. `SELECT unhex(hex('China'));`

24. `SELECT from_base64('Q2hpbmE=');`

25. Parameter validation in Concat

26. When the Space parameter is negative, MySQL does not strictly validate it, but ClickHouse will report an error

27. Such as `SELECT concat('#', space(-1), '#');`

28. The encrypt function uses diff

29. ClickHouse only supports three parameters, while MySQL 5.6 can support two parameters

30. ClickHouse currently does not support `|`, use `bitOr(a,b)` as a replacement

31. For example, `SELECT make_set(bitOr(1,4),'hello','nice',NULL,'world') AS result;`

32. The unnest function is not supported


<span id="6966f353"></span>
### Other considerations


1. When using ClickHouse client versions older than 2.4, some MySQL functions will not be recognized and will throw syntax errors, such as `select adddate();`.

2. Ecosystem compatibility issues: When connecting to ByteHouse through programs like Workbench and Navicat, compatibility issues may occur. Currently, the main errors are `Unknown function: current_user` and `Database doesn’t exist: information_schema`. Fixes are planned in future versions.
