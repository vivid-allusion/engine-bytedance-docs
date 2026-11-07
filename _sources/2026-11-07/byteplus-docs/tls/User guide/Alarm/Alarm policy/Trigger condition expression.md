---
title: "Trigger condition expression"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/trigger_condition_expressions"
---

When creating an alarm policy for Log Service, you must specify the trigger condition expression. Log Service determines whether the alarm conditions are met based on the execution result of the trigger condition expression.

When evaluating the execution result of the trigger condition expression, the execution results of analysis statements in the alarm policies corresponding to the expression variables serve as input. If the execution result of the trigger condition expression is true, an alarm is triggered. For example, if the execution statement is `result:error | SELECT count(*) AS ErrCount` and the trigger condition expression for the alarm is `$1.ErrCount>0`, it means the alarm triggers when logs with result error appear.

<span id=".6K-t5rOV6K-05piO"></span>
## syntax description

The syntax of the alarm trigger condition expression is `$N.keyname`, which supports referencing the results of query analysis.

Note:


* N is the corresponding monitoring object number, supporting up to 3 monitoring objects. For example, `$1.key` references the object numbered`1`The `key` field name in the query.

* keyname is the field name in the query analysis result; it supports letters, numbers, and underscores. It is recommended to use AS syntax to set aliases for analysis results, such as `SELECT count(*) AS ErrCount`.


When multiple values are returned in the query analysis result:


* Determine which results to evaluate based on the variables in the expression. For example, if A, B, and C are three analysis statements configured, and only A and B are set as monitoring targets in the expression, it means that the expression value only uses the analysis results from A and B.

* The results are calculated up to 1,000 times in sequence and stop when the result is true. For example, if the **set operation** selects the **Cartesian product**, the **trigger condition** is **data match**, and the expression is `$1.key1+$2.key2>100`, when analysis statements 1 and 2 return x and y results respectively, x\*y calculations will be performed. The calculation stops with an alarm when `$1.key1+$2.key2>100` is true during calculation, or stops without an alarm when the calculation reaches 1,000 times.


<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* An alarm triggers only when the expression evaluates to true. For example, `$1.key1+$1.key2` equals 100, `$1.key1+$1.key2 >100` will not trigger, while `$1.key1+$1.key2 >=100` will trigger.

* If a field name contains special characters, enclose the variable in `[]`. The variables inside `[]` are treated as a single unit. For example, `[$1.process-time]`, where `process-time` is considered a single key.

   Special characters include `+ - / * & | ^ ** % >> << > >= < <= == != =~ !~ || && !` `- ~ ?` `: ()`.

* Numeric types are treated as 64\-bit floating\-point numbers. Using equality or inequality comparisons may cause errors.


<span id=".5pSv5oyB55qE6L-Q566X56ym"></span>
## Supported operators


|Category |operator name |operator |Example |
|---|---|---|---|
|basic operator |sum operator |`+` |`$1.key1+$1.key2>10` |
||subtraction operator |`-` |`$1.key1-$1.key2>100` |
||multiplication operator |`*` |`$1.LatencyMs\*1000>10` |
||division operator |`/` |`$1.Distance/1000>10` |
||modulus operator |`%` |`$1.Column%10==0` |
|comparison operator |equals |`==` |`$1.Number==100`<br><br>`$1.Result=="Error"` |
||greater than |`>` |`$1.Number>100` |
||less than |`<` |`$1.Number<100` |
||greater than or equal to |`>=` |`$1.Number>=100` |
||less than or equal |`<=` |`$1.Number<=100` |
||not equal to |`!=` |`$1.Result != "error"` |
|parentheses |parentheses<br><br>control operation priority |`()` |`($1.key1+$1.key2)/$1.key3>100` |
|logical operator |and |`&&` |`$1.Number>100 && $1.Result=="Error"` |
||or |`\|\|` |`$1.Number>100\|\|$1.Result=="Error"` |
|escape operation |escape operation |`[]` |`[$1.process-time]`, where `process-time` is treated as a single key. |
