---
title: "Date Filter"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Date_Filter"
---

This article introduces multiple methods for filtering datasets by date.

<span id="46111c9a"></span>
# Quick start


1. Click "Filter configuration" to enter the dataset filter configuration interface, then click "Add" to set filter conditions for the dataset metric fields used by the agent.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/eea417f6ae3e4167844c3d85ec2e8be6~tplv-goo7wpa0wc-image.image) </span>


2. For date\-type fields, multiple filtering methods are provided, including "dynamic date filter", "fixed date filter", "advanced filter", "special value filter", and "single date filter". Set the relevant filtering parameters according to your actual data requirements, and click "OK" to execute the filter.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/aa77ecc232a94954a4890dc5c622ce51~tplv-goo7wpa0wc-image.image) </span>

<span id="5dd605d5"></span>
# Applicable scenarios


|Date filtering methods |Applicable scenarios |
|---|---|
|Dynamic date filtering |The date range changes continuously over time. |
|Fixed date filtering |A fixed date range that does not change over time. |
|Special value filtering |Supports filtering date data by empty date, non\-empty date, or all dates. |
|Advanced filtering |Set the start and end times as fixed or dynamic separately to flexibly define the filter date range.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Advanced filtering is supported only when the date granularity is “year\-month\-day”, that is, when viewing filtered data by day.</div><br> |
|Single date |Only one day can be selected at a time. |


<span id="4f9111e3"></span>
# Feature overview

<span id="854d4e9f"></span>
## Switch date granularity

In the upper left corner of the date filter pop\-up window, you can switch the granularity of the date filter. Supported granularities: year\-month\-day, year\-month, and year\-week.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/aa8197a2bd51425ea680bf77d2386a94~tplv-goo7wpa0wc-image.image) </span>


* **Year\-month\-day:**  View filtered data by day granularity

* **Year\-month:**  View filtered data by month granularity

* **Year\-week:**  View filtered data by week granularity


<span id="9c237d27"></span>
## Dynamic date filter

The date range is generated based on user\-defined anchor points and changes continuously over time. For example, to view the order volume for "the last 30 days".

**Specific steps**:


1. Select the date granularity as day, month, or week, and click "Dynamic date".

2. Set the relevant conditions for the "dynamic date" filter. You can choose quick date options, customize, or use advanced settings.

3. Click "OK" to complete data filtering.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c486c3b8e16b43ca977cc84dc582d810~tplv-goo7wpa0wc-image.image) </span>

The configuration instructions for related parameters are as follows:


|Parameters |Configuration instructions |
|---|---|
|Date quick options |Based on business scenarios, the system provides preset date quick options such as "Last 1 day", "This month", and more, allowing users to quickly specify filter conditions. |
|Custom |If the above quick options do not meet requirements, users can also customize dynamic dates, for example: "Last 1 month".<br><br><br>* Operator: Last<br><br>* Date count: Enter a non\-zero natural number<br><br>* Date: day/natural week/custom week/month/bimonth/quarter/half\-year/year<br><br>* Include today: Yes/No<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">If the operator is “recent”, the product additionally provides checkboxes to offset the date range by the time window granularity. For example, with a date containing “hour, minute, second”, when the granularity is set to “hour”, two checkboxes will appear:</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">Include current hour: Includes the hour in which the current time falls. For example, if the current time is 19:13:23, selecting "Include current hour" will display data from 19:00:00 to 19:59:59.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">Full hour: Refers to a complete hour. For example, if the current time is 19:13:23, selecting "Full hour" will display data from 19:00:00 to 19:59:59. If "Full hour" is not selected, data from 19:13:23 to 20:13:23 will be displayed.</div><br> |
|Advanced settings |Users can add the following special date conditions in advanced settings and choose whether the relationship with the preceding condition is “and” or “exclude”, with “and” as the default.<br><br><br>* Working days: all dates minus Chinese mainland statutory holidays minus Saturdays and Sundays that are not make\-up workdays<br><br>* Weekend: Saturday and Sunday<br><br>* Holidays: Chinese mainland statutory holidays<br><br>* Trading days: trading days of the Shanghai and Shenzhen exchanges in the Chinese mainland<br><br>* Beginning of the month: the first day of the month, such as January 1<br><br>* End of the month: the last day of the month, such as January 31<br><br>* Beginning of the quarter: the first day of the quarter, such as January 1<br><br>* End of the quarter: the last day of the quarter, such as March 31<br><br>* Beginning of the year: the first day of the year, such as January 1<br><br>* End of the year: the last day of the year, such as December 31<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">If "workdays" are set in Advanced Settings, when filtering for the most recent days, the time preview may show information that includes non\-working days, but non\-working days will not appear in the actual chart. The time preview is for reference only.</div><br> |
|Include empty dates |Include dates without corresponding data |


<span id="4f6ee279"></span>
## Fixed date filter

In contrast to the dynamic date filter, the fixed date range does not change over time.

For example, if today is 2020\-02\-13, set the date filter condition to a fixed date: 2020\-02\-08 to 2020\-02\-12. Ten days later, the filter condition remains 2020\-02\-08 to 2020\-02\-12. When the date field includes hours, minutes, and seconds, you can select the precise time.

**Operation method**:


* Select the start date and end date directly in "Fixed date".

* The time range selected in "Dynamic date" can be directly passed to "Fixed date" for filtering.

   For example, if the current date is 2025\-05\-29 and you select "last month" in dynamic date, then click fixed date, the date range will automatically be set to 2025\-04\-01 to 2025\-04\-30.

   
   |Dynamic date selection |Click to display fixed date |
   |---|---|
   |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/02cbed22c15146ec94499eeed9ae9ce2~tplv-goo7wpa0wc-image.image) </span> |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4bd8a58a647944379d089b0b6ae4f85d~tplv-goo7wpa0wc-image.image) </span> |
   


<span id="62743491"></span>
## Advanced filter

Configure the start and end times of the date filter separately to flexibly define the filter date range. After selection, you can preview in the time preview.

For example, if today is 2025\-02\-28, set the date filter conditions as follows:

Start time: Fixed 2025\-02\-29

End time: Dynamic, 1 day later

The selected dates will be 2025\-05\-29 to 2025\-05\-30; after 1 day, the selection will be 2025\-05\-29 to 2025\-06\-01, and so on.

**Detailed steps**:


1. Select the date granularity as "Year\-Month\-Day" and click "Advanced".

2. Set the start time and end time, and choose advanced settings as needed.

3. Click "Confirm" to complete data filtering.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/51221ceb0cd24173b5f1f41873576cba~tplv-goo7wpa0wc-image.image) </span>

The configuration instructions for the start time and operation time operators are as follows:


|Operator |Note |
|---|---|
|Fixed |Select a fixed date as the start or end time for the filter. |
|Dynamic |Dynamically select a time point before or after the current time as the start or end time for the filter. |
|No limit |When used as the start time, the start time is not limited, and all time points less than or equal to the end time are selected;<br><br>When used as the end time, the end time is not limited, and all time points greater than or equal to the start time are selected; no limit on the end time allows the end time to be dynamically selected up to the most recent time point with data.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Start time and end time cannot both be set to unlimited; at least one time must be specified.</div><br> |


<span id="771e0b1d"></span>
## Special value filtering

Supports filtering date data by empty date, non\-empty date, or all dates. The default is all dates:


* Empty date: Filters all data where the date field is empty.

* Non\-empty date: Filters all data where the date field is not empty.

* All dates: Used to obtain a dataset containing all records, regardless of whether the date is filled in.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cb73b9115d674fabb13ce42dd5cfdad5~tplv-goo7wpa0wc-image.image) </span>

<span id="3fe4efe7"></span>
## Single date filtering

Definition of "single date": Only one day can be selected at a time.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ea2984ed3ed34c64b2c31c4ffbcb8cc9~tplv-goo7wpa0wc-image.image) </span>
