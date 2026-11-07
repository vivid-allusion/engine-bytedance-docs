---
title: "JS SDK Integration Solution"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/JS_SDK_Integration_Solution"
---

This article describes how to integrate DataAgent using the JS SDK.

<span id="26a94c0a"></span>
# Feature overview

DataAgent supports a developer\-friendly integration method through the JS SDK. Event listening and method invocation are not supported in the iframe integration method; these features must be used through the SDK.

<span id="28f91fde"></span>
# Quick start

<span id="5bd3a406"></span>
## Installation

Directly import the SDK in HTML

```XML
<html>
 <head>
 <script src="https://unpkg.byted-static.com/aeolus/sdk/2.15.0/lib/components/index.umd.prod.js"></script>
 </head>
 <body></body>
</html>
```


<span id="0d9a8d17"></span>
## Usage

The following is a sample code for embedding DataAgent:

<span id="144785c0"></span>
### React framework

```Python
import React from 'react'
import ReactDOM from 'react-dom'

class BIComponent extends React.Component {
  render() {
    return (
      <!-- Before using Aeolus agent, it is necessary to introduce SDK in the HTML template -->
      <aeolus-agent
      urlPrefix="https://console.volcengine.com/bi/datawind/data-agent/analytics-agent-open?region=cn-shanghai" // saas 嵌入
      jwtToken="***" // Not mandatory, token authentication is obtained from the backend and passed in
      // Not necessary, if it is necessary to control the function switch, please refer to <FEATURE_CONFIG>
      feature={{
          copilot: {
            /**  Do you want to enable intelligent agent configuration  **/
            enableConfigAgent: false
          }
        }}
      searchParams="region=cn-shanghai"
    />
    )
  }
}

ReactDOM.render(<BIComponent />, document.querySelector('body'))
```


<span id="dcd01877"></span>
### Vue framework

```JavaScript
<script setup>
// Actual business logic, obtain appId/dashboardId
</script>

<template>
   <!-- Before using aeolus-agent, you need to import the SDK in the HTML template -->
   <aeolus-agent
      urlPrefix="https://console.volcengine.com/bi/datawind/data-agent/analytics-agent-open?region=cn-shanghai" // saas 嵌入
      jwtToken="***" // Not mandatory, token authentication is obtained from the backend and passed in
      // Not necessary, if it is necessary to control the function switch, please refer to <FEATURE_CONFIG>
      :feature="{
          copilot: {
            /**  Do you want to enable intelligent agent configuration  **/
            enableConfigAgent: false
          }
        }"
      searchParams="region=cn-shanghai"
    />
 </template>
```


Since the SDK component is based on web components, it can be used in different frameworks (React / Vue).

<span id="f9cbf7e1"></span>
# Component

<span id="7d41695f"></span>
## Common parameters

<span id="535cff12"></span>
### General parameters


|Parameter |Required |Description |Default value |
|---|---|---|---|
|urlPrefix |Yes |Application access address, such as the SaaS environment web address `https://console.volcengine.com/bi/datawind/data-agent/analytics-agent-open`. See [Third-party integration interface](https://docs.byteplus.com/docs/dataagent/Intelligent_Analysis_Agent_Third-Party_Integration_Guide#90956b2f). |None |
|jwtToken |Yes |Custom permission token, user's jwtToken. For how to obtain it, see [Invocation Methods](https://docs.byteplus.com/docs/dataagent/Invocation_Methods). |None |
|lang |No |Multilingual configuration. Options are `zh_CN`, `en_US`, or `ja_JP`. |'zh_CN' |
|region |No |The region to access. For details, see [Third-party integration interface](https://docs.byteplus.com/docs/dataagent/Intelligent_Analysis_Agent_Third-Party_Integration_Guide#90956b2f).<br><br>Caution: The region configuration must be passed in both urlPrefix and searchParams, and they must be consistent. |'cn\-beijing' |
|searchParams |No |Additional URL parameters. |None |


<span id="98f7f3c0"></span>
### Feature configuration parameters

The display content after integration can be controlled through the relevant feature configuration.

For example, to hide the sidebar, configure as follows: `https://console.volcengine.com/bi/datawind/data-agent/analytics-agent-open/pages/agent/detail?agentId= xxxx&appId= xxxxx&feature={"dataAgent":{"enableSidebar":false}}`

The currently supported full set of feature configuration parameters is as follows.

```JSON
{
   "copilot":{
       /** Whether to display the agent configuration in the lower right corner of the sidebar **/
       "enableConfigAgent": false,
       /** Whether the agent supports the download feature */
       "enableAgentDownload": true,
       /** Whether the agent supports displaying code */
       "enableAgentShowCode": true,
       /** Whether to display the one-click group creation for Feishu; defaults to false when embedded */
       "showOncall": false,
       /** Whether to display the username on the homepage; defaults to false when embedded, that is, the username is not displayed by default */
       "enableAgentHomePageUsernameVisible": false
   },
   "downloadConf":{
       /** Whether download supports 飞书. Default is false when embedded. */
       "showFeishuExport": false
   },
   "dataAgent":{
      /** Hide deep research mode */
     "forceDisabledDeepResearch": false,
     /** Product name at the top of the sidebar  */
     "customProductName": "Data Agent",
     /** Hide the DataAgent label in the upper left corner of the agent */
     "enableProductName": true, 
     /** Hide general agent */
     "enableGeneralAgent": true,
     //  Whether to display the left navigation. Displayed by default.
     "enableSidebar": true,
     // Type of initial session question. Defaults to intelligent Q&A, for third-party web embedding scenarios.
     "initSessionType":  "normal",// 'normal' | 'deep_research'
     // Initial session question. No initial question by default, for third-party web embedding scenarios.
     "initSessionQuestion": "",
     // Whether to show agent settings in the top navigation bar
     "enableNavigationSettings": true,
     // Whether to show agent conversation history in the top navigation bar
     "enableNavigationHistory": true, 
     // Whether to show agent new conversation in the top navigation bar
     "enableNavigationNew": true, 
    }
}
```


<span id="c4661c62"></span>
## Agent: standard embedding method

`aeolus-agent` provides embedding for a single agent usage page.

<span id="a159a6c0"></span>
### Parameters

The above common parameters must be configured, along with the following parameters related to the standard embedding method for agents.


|Parameter |Required |Description |
|---|---|---|
|agentId |No |Agent ID. To force selection of a specific agent, pass the agent ID. For how to obtain the agent ID, see [agentId](https://docs.byteplus.com/docs/dataagent/Reference_Methods_for_Obtaining_Resource_IDs#6c63d736). |
|feature |No |Control the integrated display content through feature\-related configuration.<br><br>For example, to hide the sidebar, configure as: `https://console.volcengine.com/bi/datawind/data-agent/analytics-agent-open/pages/agent/detail?agentId=**&appId=4**&`**`feature={"dataAgent":{"enableSidebar":false}}`** <br><br>For more configuration parameters and effects of feature properties, see [Feature configuration parameters](https://docs.byteplus.com/docs/dataagent/JS_SDK_Integration_Solution#98f7f3c0). |


<span id="dd0135dd"></span>
## Agent: secure embedding method

`aeolus-agent-security` provides embedding for a single agent usage page. Unlike `aeolus-agent`, using `aeolus-agent-security` does not include `jwtToken` in the queryString of the `GET` request's `queryString`.

<span id="e518a7cd"></span>
### Parameters

The above common parameters must be configured, along with the following parameters related to the secure embedding method for agents.


|Parameter |Required |Description |Default value |
|---|---|---|---|
|agentId |No |Agent ID. To force selection of a specific agent, pass the agent ID. For how to obtain the agent ID, see [agentId](https://docs.byteplus.com/docs/dataagent/Reference_Methods_for_Obtaining_Resource_IDs#6c63d736). |None |
|feature |No |Feature configuration. See [Feature configuration parameters](https://docs.byteplus.com/docs/dataagent/JS_SDK_Integration_Solution#98f7f3c0). |'{}' |
|securityUrlPrefix |Yes |Prefix for the intermediate page access URL:<br><br><br>* For SaaS environment: `https://console.volcengine.com/bi/datawind`<br><br>* For private domain: actual deployed environment domain address `${domain}/bi` |None |


<span id="1be312dc"></span>
### Example

For example, with SaaS region set to Shanghai:

```Python
<aeolus-agent-security
    urlPrefix="https://console.volcengine.com/bi/datawind/data-agent/analytics-agent-open?region=cn-shanghai"
    securityUrlPrefix="https://console.volcengine.com/bi/datawind?region=cn-shanghai"
    searchParams="region=cn-shanghai"
    jwtToken="{jwtToken}"
  ></aeolus-agent-security>
```
