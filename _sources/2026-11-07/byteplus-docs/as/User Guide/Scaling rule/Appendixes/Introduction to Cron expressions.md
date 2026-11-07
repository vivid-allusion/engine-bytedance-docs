---
title: "Introduction to Cron expressions"
product: "Auto Scaling"
product_code: "as"
source: "https://docs.byteplus.com/en/docs/as/Cron-expressions"
---

<span id=".Q3JvbuihqOi-vuW8j-S7i-e7jQ=="></span>
## Introduction to Cron expressions

A Cron expression is a string with time semantics. Each time\-related component is called a field, and fields are separated by spaces. Auto Scaling scheduled tasks support Cron expressions with 5 fields, in the format `X X X X X`. `X` is a placeholder for a field. Each field in a Cron expression represents, in sequence, minute, hour, day, month, and day of the week. Each field can be a specific value or a logical special character.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Usage notes

When you configure a Cron expression for a scheduled task, note that:


* Cron expressions are based on `UTC +08:00` time zone (China Standard Time). Therefore, when you configure a Cron expression to schedule a task triggered every day at 20:00 in China, set the Cron expression to `0 20 * * *`.

* Detailed Cron expression rules are listed below. This section only describes commonly used and currently supported Cron expression rules.


<span id=".5Z-f5Y-W5YC8"></span>
## Field value range


|Field |Required |Value range |Special character |
|---|---|---|---|
|Minute |Yes |0\-59 |\* , \- \ |
|Hour |Yes |0\-23 |\* , \- \ |
|Day |Yes |1\-31 |\* , \- L W |
|Month |Yes |1\-12 |\* , \- \ |
|Day of the week |Yes |1\-7 |\* , \- \ L # |


<span id=".54m55q6K5a2X56ym5ZCr5LmJ"></span>
## Description of special characters


|Special character |Explanation |Example |
|---|---|---|
| |Indicates all numbers within the value range. |In the month field, `*` indicates every month. |
|, |Enumerates possible values. |In the week field, `1,2,5` indicates Monday, Tuesday, and Friday. |
|\- |Specifies a value range. |In the day field, `28-31` indicates the 28th, 29th, 30th, and 31st days of the month. |
|/ |Indicates an increment value. |In the minute field, `*/5` indicates every 5 minutes starting from minute 0. `3/5` indicates every 5 minutes starting from minute 3. |
|L |The abbreviation of `Last`, indicating the last day. This character is only supported in the day and week fields. |* In the day field, `L` indicates the last day of the specified month.<br><br>* In the week field, `L` indicates the last day of the week (Sunday), and must be used with a specific week number. `6L` indicates the last Saturday of the specified month. `4L,5L` indicate the last Thursday and Friday of the specified month. |
|W |Indicates the nearest working day (Monday to Friday) to the specified day in the day field. This character is supported only in the day field. |`15W` indicates the nearest working day to the 15th of each month. If the 15th is a working day, the target date is the 15th. If it is a Saturday, the target date is the 14th. If it is a Sunday, the target date is the 16th.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The nearest working day falls within the current month. For example: When <code>1W</code> is specified, if the 1st falls on a Saturday, the trigger time is the 3rd (Monday). When <code>31W</code> is specified, if the 31st falls on a Sunday, the trigger time is the 29th (Friday).</div><br><br><br>* <div data-tips="true" data-tips-type="tip"><code>W</code> can only be used to specify a single day, but not date ranges.</div><br><br><br>* <div data-tips="true" data-tips-type="tip"><code>LW</code> indicates the last working day of the current month.</div><br> |
|# |Specifies the Nth day of the week of each month with a specific number required. After `#`, only numbers 1\-5 are supported. This character is supported only in the week field. |`7#2` indicates the second Sunday of the specified month in the week field. |


<span id=".5Y-W5YC856S65L6L"></span>
## Sample values

The listed examples are based on China Standard Time (UTC +08:00) to explain the meaning of different Cron expressions.


|Example value |Description |
|---|---|
|15 10 \* \* \* |To trigger a task every day at 10:15 |
|0 /8 \* \* \* |To trigger a task daily at 08:00, 16:00, and 24:00 |
|0 10,14,16 \* \* \* |To trigger a task daily at 10:00, 14:00, and 16:00 |
|15 10 15 \* \* |To trigger a task at 10:15 on the 15th day of each month |
|15 10 L \* \* |To trigger a task at 10:15 on the last day of each month |
|15 10 \* \* 6L |To trigger a task at 10:15 on the last Saturday of each month |
|15 10 \* \* 6#3 |To trigger a task at 10:15 on the third Saturday of each month |
|10,44 14 \* 3 3 |To trigger a task at 14:10 and 14:44 on Wednesdays in March every year |
|15 10 \* \* 1\-5 |To trigger a task at 10:15 from Monday to Friday every week |
|\*/30 \* 15 \* \* |To trigger a task every 30 minutes on the 15th day of each month |
|0 10 15W 3 \* |To trigger a task at 10:00 on the nearest working day to March 15 every year |
