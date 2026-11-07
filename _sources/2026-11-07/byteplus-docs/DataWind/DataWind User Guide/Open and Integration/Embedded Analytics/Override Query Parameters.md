---
title: "Override Query Parameters"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Override_Query_Parameters"
---

DataWind supports overriding the query conditions of embedded dashboards or charts through URL parameters, allowing you to customize data filtering. This article provides a detailed introduction to the syntax and usage of the query parameter to help you flexibly control the content displayed.

<span id="5e632555"></span>
# Feature overview

To modify the query conditions of an embedded dashboard or chart based on actual scenarios, you can pass query configurations in the URL to override the original query conditions.


* When embedding a dashboard, you can override the dashboard's **public filters and public filters in the query container**. Add the corresponding filter fields as public filters of the dashboard and use the **filter name** to match and override.

* When embedding a single chart, you can override the **chart filter items**. Add the corresponding fields to the **filter** in the visual query module for the chart, and use the **field name** to match and override.

* To override the filter items of a specific chart when embedding a dashboard, add those filter items as public filters of the dashboard.


<span id="6c7c066f"></span>
# Usage

<span id="5a0ca785"></span>
## In an iframe

Pass the `query` parameter in the iframe URL to override filters.

```JavaScript
import React from 'react'
import ReactDOM from 'react-dom'
import '@aeolus/sdk'
 
class BIComponent extends React.Component {
  render() {
    return (
      <iframe
        src={`https://console.volcengine.com/bi/datawind-open/#/external/dashboard/*****?appId=********&inline=true&query=OrderDate between '20210101' and '20210301' and Profit >= 100`}
      />
    )
  }
}
 
ReactDOM.render(<BIComponent />, document.querySelector('body'))
```


<span id="c44b21e2"></span>
## In the SDK

In the SDK component, you can pass the `query` parameter to override filters.

```JavaScript
import React from 'react'
import ReactDOM from 'react-dom'
import '@aeolus/sdk'
 
class BIComponent extends React.Component {
  render() {
    return (
      <aeolus-dashboard
        urlPrefix="https://console.volcengine.com/bi/datawind-open"
        dashboardId="*****"
        appId="******"
        query={`OrderDate between '20210101' and '20210301' and Profit >= 100`}
      />
    )
  }
}
 
ReactDOM.render(<BIComponent />, document.querySelector('body'))
```


<span id="2f904fa1"></span>
# Complete example

Take the following dashboard link as an example. You can see that this dashboard has already configured four public filters: `Category`, `ShipMode`, `Region`, and `OrderDate`.

```Plain
https://console.volcengine.com/bi/datawind-open/#/dashboard/******?appId=*******
```


You may have noticed that `ShipMode` and `OrderDate` are not consistent with the chart dataset fields. The actual dataset fields are `Ship Mode` and `Order Date`. When configuring override filters, you need to use the **public filter name** to override, not the dataset field. Specifically, public filters cannot contain spaces; otherwise, they cannot be recognized during overriding.

<span id="28a7abf2"></span>
### Example 1

```Plain
&query=Category = 'Furniture' and Region in ('Central','South')
```


This configuration queries data where `Category` is `Furniture`, and `Region` is either `Central` or `South`.

<span id="dd4cca0a"></span>
### Example 2

```Plain
&query=Category != 'Furniture' and ShipMode = 'First Class' and ProductName like '%Desktop%'
```


This configuration queries data where `Category` is not `Furniture`, `ShipMode` is `First Class`, and `ProductName` contains `Desktop`.

<span id="b435b715"></span>
### Example 3

```Plain
&query=OrderDate between '20210101' and '20210301' and Profit >= 100
```


This configuration indicates querying data where `OrderDate` is between `2021-01-01` and `2021-03-01`, and `Profit` is greater than `100`.

<span id="9b652a15"></span>
# Configuration rules

A complete query configuration starts with `&query=` and consists of one or more query statements.

<span id="18cea8e6"></span>
## Single query statement syntax

`field op value scope?`

The basic syntax of each query statement consists of `field`, `op`, `value`, and an optional `scope`:

<span id="ac13f6b8"></span>
#### field (query component name)

When embedding in a dashboard, this refers to the name of the public filter or the public filter name in the query container; when embedding in a chart, it refers to the name of the filter field added to the chart.

As shown in the figure below, `test` is the name of this query component:

<span>![图片](https://data.bytedance.net/aeolus-developers/_next/static/media/query.9637ce49.png) </span>

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">When the <code>field</code> name is purely numeric, such as <code>123</code>, enclose it in square brackets, for example: <code>[123]</code></div>


* <div data-tips="true" data-tips-type="warning">When the <code>field</code> name contains special characters (other than Chinese, English, digits, or underscores), such as <code>$test filter</code> which contains a dollar sign and a space, enclose it in square brackets, for example: <code>[$test filter]</code></div>


* <div data-tips="true" data-tips-type="warning">When the <code>field</code> name contains special characters and also includes <code>[</code> or <code>]</code> brackets, use <code>\</code> for escaping. For example, if the name is <code>test [demo] filter</code> and contains brackets and a space, it can be represented as: <code>[test \[demo\] filter]</code></div>



<span id="9afaf545"></span>
#### op (query operator)

Depending on the actual scenario, operators such as `in` and `like` can be used. For a complete list of operators, see the section below in [Basic query operators](https://docs.byteplus.com/docs/DataWind/Override_Query_Parameters#5989fda6).

<span id="c8fa5bfb"></span>
#### value (query value)

This can be a number or a string.

If the query value is a string, it must be enclosed in single quotes `'*'`. For example, `'Shanghai'`.

For multiple values, use parentheses, for example, `('Jiangsu', 'Zhejiang')`.

**Example (current query component name is test):** 

`&query=test in ('北京','上海')`

<span id="f024aff6"></span>
#### scope (optional, specifies query scope)

When you need to specify the query scope, you can use scope, for example, to restrict the filter to a specific sheet:

`field op value scope sheetId = *`

<span id="e537e88e"></span>
## Multiple query statement syntax

When there are multiple query statements, use the `and` connector, indicating a logical AND relationship. DataWind does not support logical OR relationships between filters.

The syntax is as follows:

`field1 op1 value1 and field2 op2 value2`

When you need to specify precedence, you can use parentheses `()`, for example, `(test1 in ('Jiangsu', 'Zhejiang') scope sheetId = 123) and test2 like '%abc%'`

<span id="aa0b47b2"></span>
## Query operators

<span id="5989fda6"></span>
### Basic query operators


|op |Scope of application |Description |Example |
|---|---|---|---|
|`in` |Text: exact filter<br><br>Metric value: exact filter |For multiple values, enclose them in parentheses and separate with commas, for example: `('a', 'b')`<br><br>Caution: The comma must be an English (half\-width) comma. |`field in 'a'`<br><br>`field in ('a','b')` |
|`not in` |Same as above |Same as above |`field not in ('a','b')` |
|`like` |Text: conditional filter |You can use the wildcard `%`<br><br>`keyword%` means starts with `keyword`<br><br>`%keyword` means ends with `keyword`<br><br>`%keyword%` means contains `keyword`<br><br>For multiple values, enclose them in parentheses and separate with commas, for example: `('%a%', '%b%')` |`field like '%abc%'`<br><br>`field like ('%a%','%b%')` |
|`not like` |Text: conditional filter |Same as above |`field not like '%abc%'` |
|`contains` |Text: conditional filter |Fuzzy match for data items containing this value, equivalent to `like: %abc%`<br><br>For multiple values, enclose them in parentheses and separate with commas, for example: `('a', 'b')` |`field contains 'abc'`<br><br>`field contains with ('a','b')` |
|`not contains` |Text \- conditional filter |Same as above |`field not contains 'abc'` |
|`starts with` |Text \- conditional filter |Fuzzy match for data items starting with this value, equivalent to `like: abc%`<br><br>For multiple values, enclose them in parentheses and separate with commas, for example: `('a', 'b')` |`field starts with 'abc'`<br><br>`field starts with ('a','b')` |
|`ends with` |Text \- conditional filter |Fuzzy match for data items ending with this value, equivalent to `like: %abc`<br><br>For multiple values, enclose them in parentheses and separate with commas, for example: `('a', 'b')` |`field ends with 'abc'`<br><br>`field ends with ('a','b')` |
|`is empty` |Text \- conditional filter | |`field is empty` |
|`is not empty` |Text \- conditional filter | |`field is not empty` |
|`is null` |Text \- conditional filter | |`field is null` |
|`is not null` |Text \- conditional filter | |`field is not null` |
|`between value1 and value2` |Conditional filter<br><br>Dimension value \- conditional filter<br><br>Metric value |Closed interval |`field between 'a' and 'z'`<br><br>`field between 1 and 100` |
|`is NaN` |Metric value | |`field is NaN` |
|`is not NaN` |Metric value | |`field is not NaN` |
|`=` |Text \- conditional filter<br><br>Dimension value \- conditional filter<br><br>Metric value |equal to |`field = 100` |
|`!=/<>` |Text \- conditional filter<br><br>Dimension value \- conditional filter<br><br>Metric value |not equal to |`field != 100`<br><br>`field <> 100` |
|`>` |Text \- conditional filter<br><br>Dimension value \- conditional filter<br><br>Metric value |greater than |`field > 100` |
|`>=` |Text \- conditional filter<br><br>Dimension value \- conditional filter<br><br>Metric value |greater than or equal to |`field >= 100` |
|`<` |Text \- conditional filter<br><br>Dimension value \- conditional filter<br><br>Metric value |less than |`field <= 100` |
|`<=` |Text \- conditional filter<br><br>Dimension value \- conditional filter<br><br>Metric value |less than or equal to |`field <= 100` |


<span id="f95bf18f"></span>
### Date/datetime query operators


|op |Scope of application |Description |Example |
|---|---|---|---|
|`=` |Date \- single date |Value is a string in date format<br><br>Supports 'YYYY\-MM\-DD' (year\-month\-day) or 'YYYY\-MM' (year\-month) |`field = '2022-10-01'`<br><br>`field = '2022-06'` |
|`between value1 and value2` |Date \- fixed date<br><br>Date \- advanced date |When both value1 and value2 are strings in date format, it is a fixed date.<br><br>At the same time, either value1 or value2 can also be an advanced date described by the `advancedDate` function. For details, see the function description section. |`field between '2022-10-01' and '2022-11-30'`<br><br>`field between '2022-10-01' and advancedDate(1, {unit: "day", offset: -1})` |
|`>=` |Date \- advanced date |The start time is the specified time, and the end time is unlimited.<br><br>The specified time can be a string in date format or an advanced date described by the `advancedDate` function. |`field >= '2022-10-01'`<br><br>`field >= advancedDate(1, {unit: "day", offset: -1})` |
|`<=` |Date \- advanced date |The start time is unlimited, and the end time is the specified time.<br><br>The specified time can be a string in date format or an advanced date described by the `advancedDate` function. |`field <= '2022-10-02'` |
|`is empty` |Date \- special date | |`field is empty` |
|`is not empty` |Date \- special date | |`field is not empty` |


<span id="33aa7f0f"></span>
## Query functions

<span id="1b5203cf"></span>
### Date/datetime query functions

For some date\-type queries, we also provide functions such as latest, latest with available data, and advanced time functions to describe these more complex scenarios.

The query functions are described as follows:

<span id="132a7c1d"></span>
#### latestDate

Used to describe dynamic dates—the most recent \* days (weeks/months/bimonths/quarters/years).


* **Syntax**


`latestDate(field, data, options?)`


* **Example**


`latestDate(field, 1)`

`latestDate(field, 2, {unit: "week", offset: 0, until: "periodEnd" })`


* **Parameter description**


\-\- field: query component name

\-\- data: dynamic date value

\-\- options: configuration options, optional parameter; if not provided, defaults are used. Details are as follows


| |Note |List of values |
|---|---|---|
|**unit** |Unit (default value: "day") |`"minute" (minute)`, `"hour" (hour)`, `"day" (day)`, `"week" (week)`, `"month" (month)`, `"year" (year)`, `"bimonth" (every two months)`, `"quarter" (quarter)` |
|**offset** |Time offset unit (default value: \-1) |`-1 (does not include the current time unit period)`, `0 (includes the current time unit period)` (for example, if unit is set to `week`, then offset \-1 means excluding this week, and offset 0 means including this week) |
|**until** |Until (default: "yesterday") |`"now" (the current moment)`, `"yesterday" (yesterday)`, `"today" (today)`, `"periodEnd" (until the end of the current time unit period)` (for example, if unit is set to `week`, then until set to `periodEnd` means until the end of this week. Note: until is only meaningful when offset is set to 0) |


<span id="606c0f87"></span>
#### latestSyncDate

Used to describe dynamic dates—the most recent N days (weeks, months, bimonths, quarters, or years). Only partition fields are supported.


* **Syntax**


`latestSyncDate(field, data, options?)`


* **Example**


`latestSyncDate(field, 1)`

`latestSyncDate(field, 2, {unit: "week"})`


* **Parameter description**


\-\- field: Query component name

\-\- data: Dynamic date value

\-\- options: Configuration options. This parameter is optional. If not provided, the default value is used. Details are as follows:

The value of unit refers to **latestDate**.

<span id="af4d7760"></span>
#### advancedDate

Used to describe advanced dynamic dates. Must be used together with operators such as between, `>=`, `<=`, and so on.


* **Syntax**


`advancedDate(data, options?)`


* **Example**


`field between '2022-11-15' and advancedDate(1, {unit: "day", offset: -1})`

`field >= advancedDate(1, {unit: "day", offset: -1})`


* **Parameter description**


\-\- data: Dynamic date value

\-\- options: Configuration options. This parameter is optional. If not provided, the default value is used. Details are as follows:

```Plain
  unit: 单位(默认值"day"),  offset: 时间偏移单位(默认值-1)
```


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">In the function, <code>options</code> is a JSON object, so strings need to be enclosed in <code>""</code>.</div>


The value of unit refers to **latestDate**.

offset value list: `-1 (previous day)`, `1 (next day)`

<span id="f70e1277"></span>
### Array query functions

<span id="7ad069c3"></span>
#### arrayHas

Array function used to describe whether an array contains certain elements.


* **Syntax**


`arrayHas(field, data)`


* **Example**


`arrayHas(field, ('a', 'b'))`


* **Parameter description**


\-\- field: Query component name

\-\- data: Array value

<span id="666f7e4c"></span>
#### notArrayHas

Array function used to describe whether an array does not contain certain elements.


* **Syntax**


`notArrayHas(field, data)`


* **Example**


`notArrayHas(field, ('a', 'b'))`


* **Parameter description**


\-\- field: Query component name

\-\- data: Array value

<span id="2ed3acae"></span>
### Clear query function

<span id="7f253602"></span>
#### clear

To clear a query component, use the clear function as follows:

`clear(field)`
