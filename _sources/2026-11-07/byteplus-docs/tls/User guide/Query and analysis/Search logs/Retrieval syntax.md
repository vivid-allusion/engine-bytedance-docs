---
title: "Retrieval syntax"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Log-query-syntax-2"
---

This article introduces the retrieval syntax supported by the log service retrieval function.

## Precautions

* Syntax operators are case\-insensitive, for example, `AND` and `and` both represent the retrieval logical operator.

* Logical operation (`AND`,`OR`,`&&`,`！` Parentheses such as half\-width brackets (`()`) must be used to clearly define logical operation precedence; otherwise, search results may not match expectations. For example, to search for logs under the `log` directory on a specific machine that do not contain `error`, specify the condition as `((__source__:192.168.10.10 AND __path__:\/var\/log\/*) NOT error)`.

* Multiple query statements separated by spaces indicate an "and" operation, equivalent to `AND`. For example, `warning error` equals `warning AND error`, indicating logs containing both keywords `warning` and `error`.

* Operators in query syntax are reserved characters in Log Service; if keywords contain these reserved characters, they must be escaped.

## Search methods

Log Service supports full\-text search and key\-value search; details are shown in the table below.

|Search method |Description |
|---|---|
|Full\-text search |When entering search conditions, directly input keywords without specifying the log field name. The log service segments the original logs based on the specified delimiters and matches if any segmented word meets the search conditions. The search query format is as follows:<br><br>```Plain Text```<br>```keywords1 [ [ and \| or \| not ] keywords2 ] ... ```<br><br><br>Among them, `keywords` are the keywords to search for, supporting combination with logical operators. For example, `404 AND 500` means querying all logs containing both 404 and 500 keywords.<br><br>> **tip**<br><br><br><br>* > Full\-text search requires enabling full\-text indexing.<br><br><br>* > In search statements, if the search content contains special characters (spaces, Chinese characters, etc.), search operators (and, or, etc.), or index tokenizers, enclose the content in double quotes (""), for example `"cn guilin"`.<br> |
|Key\-value search<br><br>（Key:Value） |When entering search criteria, specify both the field name and its value. Logs match if the specified field value meets the search condition. Search query format:<br><br>```Plain Text```<br>```key1 [ : \| > \| >= \| < \| <= \| = ] value1 [ [ and \| or \| not ] key2 [ : \| > \| >= \| < \| <= \| = ] value2 ]... ```<br><br><br>Here, `key` refers to the index field. For example, `status:500` indicates accessing logs where the `status` is 500.<br><br>> **tip**<br><br><br><br>* > In retrieval statements, if field names or values contain special characters (spaces, Chinese characters, etc.), retrieval operators (and, or, etc.), or index token separators, double quotes ("") are required, for example `"cn guilin"`.<br><br><br>* > Only fields of type long and double support numeric range queries.<br><br><br>* > Key\-value index must be enabled before performing key\-value retrieval.<br> |

## Search accuracy

Log Service supports exact and fuzzy queries, detailed as shown in the table below.

|search accuracy |Description |Example |
|---|---|---|
|exact search |Specify the complete keyword during query to match using the full keyword. For example, specifying the query condition as GET means searching logs containing the keyword GET.<br><br>When the log service queries data, it uses tokenization; the exact match results are not entirely precise. For instance, when executing the query `successful request`, the log service searches based on `successful and request`, matching logs containing `successful` or `request`, rather than exactly matching the phrase `successful request`. If you want to exactly match the phrase `successful request`, use phrase query or LIKE syntax. For detailed instructions, please refer to [How to precisely query phrases?](https://docs.byteplus.com/docs/tls/How-to-query-for-phrases-accurately). |* `region: cn-shanghai`: Search logs where the `region` field contains `cn-shanghai`.<br><br>* `URL:#"successful request"`: Search logs containing the phrase `successful request`.<br><br>* `* \| SELECT * WHERE "__content__" LIKE '%Error 2024-06-24%'`: Search logs where the `__content__` field contains the phrase `Error 2024-06-24`. |
|Fuzzy query |Specify only part of the keyword characters in the query conditions by adding a wildcard asterisk (`*`) or question mark (`?`), Log Service will match up to 100 words that meet the criteria and return logs that contain these 100 words and meet the query conditions. For example, the query condition `erro*` means searching for 100 words starting with "erro" in all logs, then returning all logs that contain these 100 words and meet the query conditions.<br><br><br>* The more accurate the specified word, the more accurate the query result. <br><br>* An asterisk ( \* ) or question mark ( ? ) can only appear in the middle or end of a keyword, not at the beginning of a word. <br><br>* If asterisk (\*) or question mark (?) are enclosed in double quotes (" "), asterisk (\*) or question mark (?) represents only literal characters and can not be used for fuzzy match. <br><br>* Fields of numeric types (long, double) do not support fuzzy queries with asterisks ( \* ) or question marks ( ? ). You can query using a numeric range, for example by specifying age: {20 TO 30} . |* `TopicID:6d*67`: query logs containing the field named `TopicID` with values starting with `6d` and ending with `67`<br><br>* `cn*`: query logs containing words starting with `cn` |

## Operator

The query and analysis operators supported by Log Service are shown in the table below.

|Operator |Description |Example |
|---|---|---|
|`AND` |AND logical operator retrieves the intersection of multiple search results. When specifying multiple logical operators, use parentheses () to clarify the precedence. |`__path__:\/var\/log\/* AND error` |
|`OR` |Or logical operator, representing the union of multiple search results. Use half\-width parentheses `()` to specify multiple logical operations and clearly define the precedence of logic operations. |`error OR warning` |
|`NOT` |Non\-logical operator indicating that search results exclude keywords following NOT. Use half\-width parentheses () to specify logical operator precedence when defining multiple logical operations. |`ERROR AND NOT __path__:\/var\/log\/*` |
|`TO` |Range logical operators require spaces before and after TO.<br><br>If the start value is greater than the end value, it will be automatically swapped. That is, `age:[20 TO 1]` is equivalent to `age:[1 TO 20]`. |`age:[1 TO 20]` |
|`''` |Single quotes: when the string inside single quotes contains preset delimiters, the keywords split by delimiters are connected by AND.<br><br>use single quotes`'`enclosed asterisks`*`and question marks`?`represent wildcards. |`'today is friday'` |
|`""` |Double quotes: when the string within double quotes contains preset delimiters, the keywords separated by the delimiters are connected by AND.<br><br>Use double quotes`"`Wrapped asterisks`*`and question marks`?`do not represent wildcards; they only represent ordinary characters. |`__hostname__:"Jone Doe"` |
|`:` |Colon indicates key\-value retrieval, returning logs that contain the specified key and value. |`level:info` |
|`*` |Wildcard, used for fuzzy queries. The wildcard `*` can match zero, single, or multiple characters. <br><br>If asterisk (\*) or question mark (?) are enclosed in double quotes (" "), asterisk (\*) or question mark (?) represents only literal characters and can not be used for fuzzy match. For example: <br><br><br>* `gu*` matches keywords that start with `gu`. <br><br>* `"gu*"` matches the keyword `gu*`. |`level:erro*` |
|`?` |Wildcard, used for fuzzy queries. The wildcard `?` can match a single character <br><br>If asterisk (\*) or question mark (?) are enclosed in double quotes (" "), asterisk (\*) or question mark (?) represents only literal characters and can not be used for fuzzy match. For example: <br><br><br>* `gu?n` matches the keyword that starts with `gu`, ends with `n`, and has one character in between. <br><br>* `"gu?n"` matches the keyword `gu?n`. |`level:erro?` |
|`()` |Grouping operator, used to control the priority among multiple logical operations. |`((__source__:192.168.10.10 AND __path__:\/var\/log\/*) NOT error)` |
|`=` |Equals sign, used to query logs where the value of a numeric field equals a certain number. Equals sign (=) and colon (:) have the same function. |`age=18` |
|`!=` |The inequality sign indicates that the query does not contain the logs with the specified value. |`age!=18` |
|`>` |Range operator indicates querying logs where the value in a numeric field is greater than a certain number. |`age>18` |
|`>=` |Range operator, used to query logs where the value in a numeric field is greater than or equal to a certain number. |`age>=18` |
|`<` |The range operator searches logs with numeric fields where the value is less than a certain number. |`age<18` |
|`<=` |Range operator queries logs with numeric fields where the value is less than or equal to a certain number. |`age<=18` |
|`[]` |The range operator includes boundary values. |`age:[20 TO 30]` |
|`{}` |Range operator excluding boundary values. |`age:{20 TO 30}` |
|`\` |Escape character. If the search keyword contains reserved characters, escape them before searching. Escaped characters represent themselves, not keywords.<br><br>Characters that need escaping include `+ - = & \| > < !` `( ) { } [ ] ^ " ~ * ?` `: \ /`.<br><br>> **tip**<br><br><br><br>* > When searching with double quotes, only escape `" \`.<br><br><br>* > When searching with single quotes, only escape `' \\ * ?`.<br> |`__path__:\/images\/log` |

## Query statement reference

> **tip**

> Different index configurations yield different query results.

### Common query statements

|Scenarios |Statement |
|---|---|
|search logs containing the keyword ERROR. |`ERROR` |
|Query logs containing the `level` field. |`level:*` |
|Query logs that do not contain the `level` field. |`NOT level:*` |
|Query logs where the `level` field value is not empty |`NOT level:""` |
|Query logs where the `level` field value is empty. |`level:""` |
|Search logs where the `level` field is not null. |`NOT level:"null"` |
|Query logs from a specific machine or several machines with the specified IP. |`__source__:192.168.10.10` or `__source__:192.168.10.*` |
|Query logs from a specific file or several files with a designated log collection path name. |`__path__:"/var/log/access.log"` or `__path__:\/var\/log\/*.log` |
|Query access logs with status code `4xx`. |`status:[400 TO 500}` |
|Query logs with status code greater than `400`, indicating access failure. |`status:>400` |
|Query logs of failed requests in GET access logs. |`method:GET AND status:>400` |
|Searches for exception logs, that is, logs with levels other than INFO. |`NOT level:INFO` |
|Query logs with ERROR or WARNING level. |`level:ERROR OR level:WARNING` |
|Query abnormal logs on a specific machine, that is, logs from the specified IP address with a level other than INFO. |`__source__:192.168.10.10 NOT level:INFO` |
|Logs from specified IP addresses with level ERROR or WARNING. |`__source__:192.168.10.10 AND (level:ERROR OR level:WARNING)` |
|Search abnormal logs on a specified machine in a specific file, meaning logs from a specified IP address, with a path to the specified file, and a level other than INFO. |`(__source__:192.168.10.10 AND __path__:\/var\/log\/access.log) NOT level:INFO` |
|Query logs for a specific Pod name using the reserved field `__pod_name__`. |`__pod_name__:nginx` |
|Query logs where Pod name is application and request delay exceeds 3s. |`__pod_name__:application AND request_time:>3` |
|Query logs containing the field name `ProjectID` with a field value starting with `6d` and ending with `67`. |`ProjectID:6d*67` |
|Search logs containing the keyword `not`. |`"not"`<br><br>> **tip**<br><br><br>> not is the default log service search operator. When not is used as a regular search string, enclose it in double quotes ("").<br> |

### Query based on delimiters

If you enable the delimiter feature when creating an index, Log Service splits the log content into multiple keywords based on delimiters, allowing you to search each keyword for log retrieval. Log Service supports delimiters including `!@#%^&*\"()-_=', <>/?|;:\\n\\t\\r[]{}\`.

For example, the `region` field value is `cn-guilin`, and a key\-value index is configured for this field.

* When tokenization is disabled, `cn-guilin` is treated as a whole, and a search using `guilin` will not return this log.

* When you set the token separators to `!@#%^&*\"()-_=', <>/?|;:\\n\\t\\r[]{}`, `cn-guilin` will be split into `cn` and `guilin`. You can use the following statements to search logs.

   |Scenarios |search statement |
   |---|---|
   |Query logs with `region` field containing `guilin`. |`region:guilin` |
   |Query logs where the `region` field contains `cn` and `guilin` |`region:"cn guilin"` |
   |Search logs containing words starting with `gu`. |`gu*` |

### Phrase query

You can use phrase queries to precisely match specific phrases. For more details, refer to [Phrase query to search logs](https://docs.byteplus.com/docs/tls/Phrase-search-2).

|Scenarios |Retrieval statement |
|---|---|
|Searches logs where the `URL` field contains `ShardId=7`. |`URL:#"ShardId=7"` |

### Reserved field query

|reserved field |Description |Example |
|---|---|---|
|`__source__` |Filter logs from the specified IP address. Supports fuzzy search using wildcards. |`__source__:127.0.0.*` |
|`__path__` |Filter logs from files in the specified path. Support fuzzy queries using wildcards. |`__path__:\/var\/log\/messages` |
|`__time__` |Filter logs by the `__time__` field, supporting range queries. |`__time__:[1524952304123 TO 1724958207123]` |

## Example queries

This example demonstrates the use of search syntax from various dimensions, including full\-text search, key\-value search, exact match, fuzzy search, phrase queries, and SQL LIKE queries.

### Original logs

```Plain
Action:ConsumeLogs
Host:t.*.com
UID:210006
ReqID:f118a5b781
ReqSize:51
ReqTime:16
RespSize:1
Method:GET
status:200
URL:/ConsumeKafkaLogs?ShardId=5&TopicId=d6cb02b5-1cd1-4265-9b8b-83b7
level:error
error:Too many requests in a short period of time, please slow down.
```

### Configure index

Different index configurations produce different query and analysis results. When both full\-text and lookup indexes are created, the key\-value index configuration takes precedence.

### Query statement

#### Fuzzy query

|Category |Scenarios |Query statements and results |
|---|---|---|
|Basic fuzzy search |Query logs containing keywords starting with `Consume`. |* search statement<br><br>   ```Plain```<br>```   Consume*```<br>```   ```<br>   <br><br>* search results<br><br>   Return logs containing keywords such as ConsumeOriginalLogs, ConsumeKafkaLogs, ConsumerHeartbeat.<br><br>   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a7260fa962d7469f8503bc893abf4be5~tplv-goo7wpa0wc-image.image) |
|Fuzzy search based on SQL LIKE syntax |Query logs where the `host` field contains the string `ces`. |* Query statement<br><br>   ```SQL```<br>```   * \| SELECT * WHERE Host LIKE '%ces%' ```<br>```   ```<br>   <br><br>* Query results![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_4353f3f56f734981ff67e41aa3c8db2d.png) |

#### Exact query

|Category |Scenarios |search query and results |
|---|---|---|
|Basic precise query |Search logs containing the keyword `ConsumeLogs`. |* Search statement<br><br>   ```Plain```<br>```   ConsumeLogs```<br>```   ```<br>   <br><br>* Search results<br><br>   Return logs containing the keyword ConsumeLogs.<br><br>   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a18dbaadc80b4cb99a76783e2915f3a3~tplv-goo7wpa0wc-image.image) |
||search logs with ConsumeLogs in the `URL` field. |* Query statement<br><br>   ```Plain```<br>```   URL:ConsumeLogs```<br>```   ```<br>   <br><br>* Query results<br><br>   Return logs where the `URL` field contains the keyword ConsumeLogs.<br><br>   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1e517a4ede4d4b5991d4028e9f3efe87~tplv-goo7wpa0wc-image.image) |
||Query related logs of `ConsumeLogs?ShardId=5`. |in this example, question mark (?) and equals sign (=) act as delimiters, so the log service splits `ConsumeLogs?ShardId=5` into ConsumeLogs, ShardId, and 5 for the query. if you need to match the phrase `ConsumeLogs?ShardId=5` exactly, please refer to the phrase query and SQL LIKE query below.<br><br><br>* search statement<br><br>   ```Plain```<br>```   "ConsumeLogs?ShardId=5"```<br>```   ```<br>   <br><br>* search results<br><br>   Return all logs containing ConsumeLogs, ShardId, and 5 simultaneously.<br><br>   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2a94e2f48e8f4e0bacf857eda4e5497f~tplv-goo7wpa0wc-image.image) |
|Phrase query |Precise query for the phrase `ConsumeLogs?ShardId=5`\-related logs. |Exact match `ConsumeLogs?ShardId=5`, supports phrase search or exact retrieval based on SQL LIKE syntax.<br><br><br>* search query<br><br>   ```Plain```<br>```   #"ConsumeLogs?ShardId=5"```<br>```   ```<br>   <br><br>* search results<br><br>   Precisely matched logs containing the phrase `ConsumeLogs?ShardId=5`.<br><br>   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/27ae1dec9ff64b05bab0a4fc358f4a8f~tplv-goo7wpa0wc-image.image) |
|Exact search based on SQL LIKE syntax |Precise query for logs with `URL` field containing `ConsumeLogs?ShardId=5`. |* Search statement<br><br>   ```SQL```<br>```   * \| SELECT * WHERE URL LIKE '%ConsumeLogs?ShardId=5%' ```<br>```   ```<br>   <br><br>* Search results<br><br>   Exact match of phrase `ConsumeLogs?ShardId=5` in related logs.![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_e5a218568821a464928543e6b9082a08.png) |
