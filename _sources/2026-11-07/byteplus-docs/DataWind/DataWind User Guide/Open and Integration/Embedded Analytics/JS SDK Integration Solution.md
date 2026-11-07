---
title: "JS SDK Integration Solution"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/JS_SDK_Integration_Solution"
---

<span id="_1-概述"></span>
# 1. Overview

DataWind supports a developer\-friendly integration method via JS SDK. Event listening and method invocation are not supported in the iframe integration mode; these features must be used through the SDK.

<span id="_2-快速入门"></span>
# 2. Quick start

<span id="_2-1-安装"></span>
## 2.1 Installation

Directly import the SDK in HTML

```html
<html>
  <head>
    <script src="https://unpkg.byted-static.com/aeolus/sdk/2.3.0/lib/components/index.umd.prod.js"></script>
  </head>
  <body></body>
</html>

```


<span id="_2-2-使用"></span>
## 2.2 Usage

The following is a sample code for embedding a dashboard:


* React framework:


```js
import React from 'react'
import ReactDOM from 'react-dom'

class BIComponent extends React.Component {
  render() {
    return (
      <bi-dashboard
        urlPrefix="******" // 应用访问地址，如SaaS环境Web端地址 https://console.volcengine.com/bi/datawind-open；私有化环境Web端地址https://${domain}/bi
        appId="******"         // 项目id
        dashboardId="******"   // 仪表盘id
      />
    )
  }
}

ReactDOM.render(<BIComponent />, document.querySelector('body'))

```



* Vue framework:


```js
<script setup>
// Actual business logic, obtain appId/ dashboardId
</script>

<template>
 <!-- Before using bi-dashboard, you need to import the SDK in the HTML template -->
 <bi-dashboard
 urlPrefix="******" // 应用访问地址，如SaaS环境Web端地址 https://console.volcengine.com/bi/datawind-open；私有化环境Web端地址https://${domain}/bi
 appId="******" // 项目id
 dashboardId="******" // 仪表盘id
 />
</template>
```


Since the SDK components are based on web components, they can be used in different frameworks (React / Vue).

<span id="_3-组件"></span>
# 3. Components

<span id="_3-1-通用参数"></span>
## 3.1 Common parameters


|**Property** |**Description** |**Default** |
|---|---|---|
|urlPrefix |**required**, application access address, such as the SaaS environment web endpoint https://console.volcengine.com/bi/datawind\-open. See [URL Configuration](https://docs.byteplus.com/docs/DataWind/URL_Configuration) section | |
|appId |**required**, project id, see [appId](https://docs.byteplus.com/docs/DataWind/How_to_Obtain_Resource_IDs#appid) |*  |
|feature |General feature configuration object, such as `'{"dashboard":{"sheet":{"tabPosition":"top"}}}'`, see [Feature Configuration](https://docs.byteplus.com/docs/DataWind/Feature_Configuration) section for more configuration details |'{}' |
|jwtToken |Custom permission token, refer to [Visualization – Dashboard and Chart Open API](https://docs.byteplus.com/docs/DataWind/Visualization_Dashboard_and_Chart_OpenAPI)acquisition ||
|lang |Multilingual configuration, available options are `zh_CN`, `en_US`, or `ja_JP` (version 2.44) |'zh_CN' |


<span id="_3-2-仪表盘"></span>
## 3.2 Dashboard

**bi\-dashboard** enables embedding of a single dashboard view page

<span id="_3-2-1-参数"></span>
### 3.2.1 Parameters


|Property |Description |Default |Example |
|---|---|---|---|
|dashboardId |required, dashboard id |*  |*  |
|sheetId |Specify the default active sheet page id |*  |*  |
|snapshotId |Bookmark id to access |*  |*  |
|autoHeight |Automatically synchronize the iframe height to the dashboard height, optional true or false |'false' |'true' |
|query |Global filter override configuration |*  |For example, 'projectId eq 123', see [Override Filters](https://docs.byteplus.com/docs/DataWind/Override_Filters) section |


<span id="_3-2-2-示例"></span>
### 3.2.2 Example

```js
import React from 'react'
import ReactDOM from 'react-dom'

class BIComponent extends React.Component {
  render() {
    return (
      <bi-dashboard
        urlPrefix="******"
        appId="******"
        dashboardId="******"
        sheetId="******"
      />
    )
  }
}

ReactDOM.render(<BIComponent />, document.querySelector('body'))
```


<span id="_3-3-移动端仪表盘"></span>
## 3.3 Mobile dashboard

**bi\-mobile\-dashboard** enables embedding of a single mobile dashboard view page

<span id="_3-3-1-参数"></span>
### 3.3.1 Parameters


|Property |Description |Default |Example |
|---|---|---|---|
|dashboardId |required, dashboard id |*  |*  |
|sheetId |Active sheet page id |*  |*  |
|query |Global filter override configuration |*  |For example, 'projectId eq 123', see [Override Filters](https://docs.byteplus.com/docs/DataWind/Override_Filters) section |


<span id="_3-3-2-示例"></span>
### 3.3.2 Example

```js
import React from 'react'
import ReactDOM from 'react-dom'

class BIComponent extends React.Component {
  render() {
    return (
      <bi-mobile-dashboard
        urlPrefix="******"
        appId="******"
        dashboardId="******"
        sheetId="******"
      />
    )
  }
}

ReactDOM.render(<BIComponent />, document.querySelector('body'))
```


<span id="_3-4-仪表盘图表"></span>
## 3.4 Dashboard chart

**bi\-dashboard\-report** enables embedding of a single dashboard chart

<span id="_3-4-1-参数"></span>
### 3.4.1 Parameters


|Property |Description |Default |
|---|---|---|
|dashboardId |required, dashboard id |*  |
|reportId |required, chart id |*  |
|sheetId |Active sheet page id, required when embedding a chart from a multi\-sheet dashboard |*  |
|query |Chart filter override configuration, for example, 'projectId eq 123', see [Override Filters](https://docs.byteplus.com/docs/DataWind/Override_Filters) section |*  |


<span id="_3-4-2-示例"></span>
### 3.4.2 Example

```js
import React from 'react'
import ReactDOM from 'react-dom'

class BIComponent extends React.Component {
  render() {
    return (
      <bi-dashboard-report
        urlPrefix="******"
        appId="******"
        dashboardId="******"
        reportId="******"
        feature={{
         dashboard: {
            report: {
                    actions: [],
            },
         },
        }}
      />
    )
  }
}

ReactDOM.render(<BIComponent />, document.querySelector('body'))

```


<span id="_3-5-可视化查询"></span>
## 3.5 Visual query

**bi\-viz\-query** enables embedding of the visual query module

<span id="_3-5-1-参数"></span>
### 3.5.1 Parameters


|Property |Description |Default |
|---|---|---|
|dataSetId |Dataset id |*  |
|queryId |Query id |*  |
|reportId |Chart id |*  |


<span id="_3-5-2-示例"></span>
### 3.5.2 Example

```js
import React from 'react'
import ReactDOM from 'react-dom'

class BIComponent extends React.Component {
  render() {
    return (
      <bi-viz-query
        urlPrefix="******"
        appId="******"
        reportId="******"
      />
    )
  }
}

ReactDOM.render(<BIComponent />, document.querySelector('body'))

```


<span id="_3-6-大屏"></span>
## 3.6 Large screen

**bi\-vscreen\-preview** enables embedding of a single large screen

<span id="_3-6-1-参数"></span>
### 3.6.1 Parameters


|Property |Description |Default |
|---|---|---|
|id |Large screen id |*  |


<span id="_3-6-2-示例"></span>
### 3.6.2 Example

```js
import React from 'react'
import ReactDOM from 'react-dom'
import '@aeolus/sdk'

class BIComponent extends React.Component {
  render() {
    return (
      <bi-vscreen-preview
        urlPrefix="******"
        appId="******"
        id="******"
      />
    )
  }
}

ReactDOM.render(<BIComponent />, document.querySelector('body'))

```
