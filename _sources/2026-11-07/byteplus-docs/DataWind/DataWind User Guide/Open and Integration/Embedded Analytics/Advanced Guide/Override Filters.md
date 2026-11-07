---
title: "Override Filters"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Override_Filters"
---

<span id="_1-概述"></span>
# 1. Overview

You can provide filter configurations to override filter operations and filter values for embedded dashboards and embedded charts.


* When embedding a dashboard, you can override the dashboard's **public filters**. Add the corresponding filter fields as public filters for the dashboard and use the **filter name** for matching and overriding.

* When embedding a single chart, you can override the **chart filter items**. In the visual query module, add the corresponding fields to **Filters** for the chart and use the **field name** for matching and overriding.

* To override specific chart filter items when embedding a dashboard, add those filter items as public filters for the dashboard.


<span id="_2-配置规则"></span>
# 2. Configuration rules

A complete filter configuration is as follows:

`field1 op1 value1 and field2 op2 'value2','value22' and field3 op3 value3,value33`

Different filter configurations are connected by `and`, indicating an AND relationship between configurations. Intelligent Data Insight does not support OR relationships between override filters.

Each filter configuration consists of three parts: `field`, `op`, and `value`:


* `field` \- The filter name. For embedded dashboards, this is the public filter name; for embedded charts, this is the name of the filter field added to the chart.

* `op` \- The filter operator.

* `value` \- The filter value. If the filter value is a string, it must be enclosed in single quotes ''. Multiple filter values are separated by commas.


Let S denote the complete filter configuration and A denote a single filter configuration. The filter rule grammar is described as follows.

```Plain
S -> S | S and A
S -> A
A -> [filterName] OP V
OP -> eq | ne | lt | gt | le | ge | in | ni | btw | lk | nl | arrayhas | last | lastsync
V -> NUMBER | STRING | V,NUMBER | V,STRING
```


The explanations for all filter operators are as follows.


|op |Note |
|---|---|
|eq |equal |
|ne |not equal |
|lt |less than |
|gt |greater than |
|le |less or equal |
|ge |greater or equal |
|in |in (value1,value2)<br><br>Caution: Do not add spaces between value entries. |
|ni |not in |
|btw |between |
|lk |like |
|nl |not like |
|arrayhas |array has |
|last |last \* time\-units |
|lastsync |last sync \* time\-units |


<span id="_3-配置示例"></span>
# 3. Configuration examples

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">To embed a complete dashboard and override the filter criteria of dashboard charts, <strong>you must</strong> add a public filter to the dashboard and override the public filter to affect chart queries.</div>


* <div data-tips="true" data-tips-type="warning">To embed a single chart from a dashboard and override the chart's filter criteria, <strong>you must</strong> add the corresponding filter field to the chart.</div>



<span id="_3-1-示例一"></span>
## 3.1 Example 1

```Plain
Category eq 'Furniture' and Region in 'Central','South'
```


This configuration queries data where `Category` is `Furniture` and `Region` is `Central` or `South`.

<span id="_3-2-示例二"></span>
## 3.2 Example 2

```Plain
Category ne 'Furniture' and ShipMode eq 'First Class' and ProductName lk '%Desktop%'
```


This configuration queries data where `Category` is not `Furniture`, `ShipMode` is `First Class`, and `ProductName` contains `Desktop`. Specifically, the lk operator requires the use of wildcards:


* `keyword%` indicates that the value starts with `keyword`

* `%keyword` indicates that the value ends with `keyword`

* `%keyword%` indicates that the value contains `keyword`


<span id="_3-3-示例三"></span>
## 3.3 Example 3

```Plain
OrderDate btw '20210101','20210301' and Profit gt 100
```


This configuration queries data where `OrderDate` is between `2021-01-01` and `2021-03-01`, and `Profit` is greater than `100`.

<span id="_4-使用方式"></span>
# 4. Usage

<span id="_4-1-在-iframe-中使用"></span>
## 4.1 Usage in an iframe

Pass the `filter` parameter in the iframe URL to configure override filters.

```js
import React from 'react'
import ReactDOM from 'react-dom'
import '@aeolus/sdk'

class BIComponent extends React.Component {
  render() {
    return (
      <iframe 
        src={`https://console.volcengine.com/bi/datawind/#/external/dashboard/******?appId=******&inline=true&filter=OrderDate btw '20210101','20210301' and Profit gt 100`}
      />
    )
  }
}

ReactDOM.render(<BIComponent />, document.querySelector('body'))
```


<span id="_4-2-在-sdk-中使用"></span>
## 4.2 Usage in the SDK

In the SDK component, you can pass the `filter` parameter to configure override filters.

```js
import React from 'react'
import ReactDOM from 'react-dom'

class BIComponent extends React.Component {
  render() {
    return (
      <bi-dashboard
        urlPrefix='https://console.volcengine.com/bi/datawind'
        dashboardId='******'
        appId='******'
        filter={`OrderDate btw '20210101','20210301' and Profit gt 100`}
      />
    )
  }
}

ReactDOM.render(<BIComponent />, document.querySelector('body'))
```
