---
title: "Variables"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/variables"
---

When creating a data archiving ticket, you need to configure variables to define archiving policies, control archiving operations, and set archiving parameters. These variables help automate and optimize the data archiving process, enabling more effective database data management and organization, thereby improving database query performance and business operations.

<span id="background-information"></span>
## Background

In the data cleaning and archiving of databases, using variables can greatly enhance the flexibility and configurability of tasks. These variables can be divided into system variables, time variables, and non\-time variables, and are dynamically referenced in task nodes in the form of `${varName}`.


|**Variable type** |**Difference** |
|---|---|
|System variable |A system variable is typically predefined by the system. It is used to dynamically reference system information in the task flow, such as task ID, execution time, and the user executing the task. |
|Time variable |A time variable is commonly used to handle and refer to time\-related information, facilitating operations such as archiving data by date. For its time format, refer to the time format. |
|Non\-time variable |A non\-time variable can be custom variables you define to pass dynamic values used in the task flow. They can be strings, numerical values, or other types of data, such as the target and source table names for archiving. |


<span id="considerations"></span>
## Precautions


* Offset time: `current time` at scheduling + configured time offset. If it is a one\-time task, then the scheduling time is the time you click execute.

* The specific offset time is based on execution and may have an error of about 1 to 2 minutes due to scheduling reasons.

* The offset time is in the UTC+8 time zone. You need to calculate the precise time on your own when performing time computations.

* Time offset `-` means to move forward, `+` means to move backward. Both `+` and `-` are less than time conditions, with examples as follows:

   Configure the scheduled deletion time at 08:00 every morning. Assuming the deletion task is executed at 08:00 AM on October 2, 2024, the time offset configuration and where statement are as follows:

   * Time offset configuration `- 24` hours, time format `yyyy-mm-dd hh:MM:ss`, then the generated where condition is `time` < '2024\-10\-01 08:00:00'

   * Time offset configuration `+ 24` hours, time format `yyyy-mm-dd hh:MM:ss`, then the generated where condition is `time` < '2024\-10\-03 08:00:00'

* Multiple variables can be configured, which will be entered into the where condition simultaneously using the `AND` method.


<span id="configuration-related-to-time-variables"></span>
## Configuration for time variables


|**Time variables** |**Description** |**Input example** |**Return example** |
|---|---|---|---|
|Year |yyyy represents the year of the current day. |yyyy |2024 |
|Month |m is the Nth month of the current year, mm returns values from [01,12]. |mm |08 |
|Day |d represents the Nth day of the current month, d returns values between [1,31], dd returns values from [01,31]. |d |31 |
|Hour |h represents the Nth hour of the day, 0 represents midnight. The return value of h is [0, 23], the return value of hh is [00, 23]. |hh |10 |
|Minute |M represents the minutes. The return value of MM is [00, 59]. |MM |27 |
|Second |* s represents the seconds.<br><br>* S represents the milliseconds. |ss |08 |
|Time zone |Z represents the time zone. |Z |UTC+08:00 |
|Timestamp |* ss represents a timestamp at the second level.<br><br>* ss.SS represents a timestamp at the millisecond level. |ss |09 |


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">T represents the separator between date and time.</div>


Examples of time format combinations:


|**Input example** |**Return example** |
|---|---|
|`yyyy-mm-dd` |2024\-08\-12 |
|`yyyy-mm-dd hh:MM:ss` |2024\-08\-12 09:12:12 |
|`yyyy-mm-ddThh:MM:ssZ` |2024\-10\-26T00:12:00Z |
|`yyyy-mm-ddThh:MM:ss.SSSZ` |2024\-10\-23T00:15:00.000Z |


**Related documentation**

Variables are used to define filtering conditions when creating data cleaning and archiving tasks. For details, refer to:


* [Creating a data cleaning and archiving ticket (RDS for MySQL)](https://docs.byteplus.com/en/docs/DBW/create-data-cleansing-and-archiving-ticket-for-mysql)

* [Creating a data cleaning and archiving ticket (NDB for MySQL)](https://docs.byteplus.com/en/docs/DBW/create-data-cleansing-and-archiving-ticket-for-mysql)
