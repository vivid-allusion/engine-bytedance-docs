---
title: "Best Practices for Embedded Analytics"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Best_Practices_for_Embedded_Analytics"
---

Business intelligence (BI) has been widely applied in users' business processes. When BI is used as an independent application platform, users must frequently switch between different systems while using business systems such as CRM, ERP, or OA in their daily work. Cumbersome login procedures and switching between application systems interrupt business thinking and reduce efficiency. This not only hinders the adoption of BI within the enterprise but also makes it difficult to achieve a unified IT application management platform.

Therefore, by placing easy\-to\-use data analysis features and completed dashboard results directly within the UI of business system applications, the continuity and availability of data insights for business users can be ensured.

This article analyzes practical business application cases to help everyone achieve the following business scenarios.

<span id="416311f8"></span>
# Business scenarios

<span id="3319bc80"></span>
## Case 1

Zhang Xiaoming wants to integrate BI's visualization and analysis capabilities into their own operations platform, enabling quick generation of visualizations and access to data insights through page interactions such as clicking and dragging on the operations platform.

After conducting research, it was decided to integrate the DataWind platform, import their own data sources into DataWind as datasets through data preparation, and embed the visualization query page of this dataset into the operations platform. Afterwards, data drag\-and\-drop analysis can be performed directly on the operations platform, greatly improving data analysis efficiency.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8ed738ba74094ef4ba51c1cb76e69cca~tplv-goo7wpa0wc-image.image" width="1382px" /></div>


<span id="c6fcb457"></span>
## Case 2

Wang Xiaohong wants to create an operations data dashboard and share it with different regional managers, ensuring that each regional manager only sees data for their own region. Furthermore, these data dashboards can be integrated into the CRM system most commonly used by regional managers.

Xiaohong discovered that DataWind can meet the requirements for creating a data dashboard, and that DataWind's row\-level permissions and custom filters also satisfy the platform's needs for data access control. It can be quickly integrated into their own CRM system. Ultimately, Xiaohong decided to build the operations data dashboard by embedding a DataWind dashboard.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4bbb6efc05c54e4e881b1dbf6d675708~tplv-goo7wpa0wc-image.image" width="1052px" /></div>


<span id="dcd979f1"></span>
## Case 3

Li Xiaohua needs to query massive amounts of product transaction records. A query tool with the following features is required: the ability to query large volumes of detailed data, support for rich filtering operations, configurable table and cell styles, and the option to modify column field formulas when necessary. After confirming that DataWind meets the requirements, Li Xiaohua created a detailed data report in DataWind and embedded it into the product transaction management system, enabling each relevant operations team member to quickly query and obtain the desired data results.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d8fcf891c79342e0a90dcc211d23c988~tplv-goo7wpa0wc-image.image" width="3292px" /></div>


For the most convenient and efficient integration, you can connect using the Iframe method. The procedure is as follows.

<span id="e021f62c"></span>
# Iframe integration solution

<span id="746e76be"></span>
## Overview

This operation must be performed by developers. The main steps are as follows:

Step 1. Obtain the URL of the target dashboard/chart

Step 2. Modify the link

Step 3. Generate the code

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The developer recommends granting project administrator permissions in the project where operations are needed, and then assigning permissions as needed after completion.</div>


<span id="949deffe"></span>
## Step 1. Obtain the URL of the target dashboard/chart


* Both of the following methods can be used to obtain the link for the target dashboard, chart, or screen, and the results are identical.

* For dashboards on mobile devices, only the second method can be used.


<span id="7e6c9163"></span>
### 1. Obtain directly within the product

<span id="8d41a28c"></span>
#### Dashboard/chart


* **Chart**

   * Enter dashboard preview mode

   * Click the right side of the chart to be embedded, and select "Embed chart"

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/375be30a75714217a1ba734f109fbe50~tplv-goo7wpa0wc-image.image) </span>

   * The message "Copy successful" will be displayed. You can then paste the link by right\-clicking or using the keyboard shortcut Ctrl+V.

* **Dashboard**

   * Enter dashboard preview mode

   * Click the right side of the chart to be embedded, and select "Embed dashboard"

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/906022611a49475099b0b2e54b655b5f~tplv-goo7wpa0wc-image.image) </span>

   * The message "Copy successful" will be displayed. You can then paste the link by right\-clicking or using the keyboard shortcut Ctrl+V.


<span id="3e5d6cda"></span>
#### Screen

As shown in the figure, select View on the list page, and after opening, simply copy the browser URL.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3669decfd9b04da6908fad0b659831d0~tplv-goo7wpa0wc-image.image) </span>

<span id="1060a0a3"></span>
### 2. Manual concatenation

If you choose manual concatenation, proceed as follows. The underlined content represents variables, which are explained in the parameter details below; the rest is fixed content.

**Dashboard**

<ins>$HOST</ins>/#/external/dashboard/<ins>$DASHBOARD_ID</ins>?appId=<ins>$APP_ID</ins>&inline=true

For example:

```Plain
https://console.volcengine.com/bi#/external/dashboard/47610?appId=1010681&inline=true
```


**Mobile dashboard**

<ins>$HOST\-h5</ins>/dashboard/?appId=<ins>$APP_ID</ins>&id=<ins>$DASHBOARD_ID</ins>&inline=true

For example:

```Plain
https://console.volcengine.com/bi-h5/dashboard/?appId=1010681&id=47610&inline=true
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Caution: Mobile links can only be accessed on mobile devices. If the link is opened on a PC, it will automatically redirect to the PC link.</div>


**Chart**

<ins>$HOST</ins>/#/external/dashboard/<ins>$DASHBOARD_ID</ins>/<ins>$REPORT_ID</ins>?appId=<ins>$APP_ID</ins>&inline=true

For example:

```Plain
https://console.volcengine.com/bi#/external/dashboard/47610/305962?appId=1010681&inline=true
```


**Visual query**

<ins>$HOST</ins>/#/dataQuery?appId=<ins>$APP_ID</ins>&inline=true

For example:

```Plain
https://console.volcengine.com/bi#/dataQuery?appId=1010681&inline=true
```


**Large screen**

<ins>$HOST</ins>/vScreen/preview?appId=<ins>$APP_ID</ins>&id=<ins>$VSCREEN_ID</ins>&resizeMode=auto

For example:

```Plain
https://console.volcengine.com/bi#/vScreen/preview?appId=1010681&id=11&resizeMode=auto
```


**Parameter details:** 


|**Parameter** |**Description** |
|---|---|
|$HOST |* **SaaS environment** Set to https://console.volcengine.com/bi<br><br>* **Private deployment environment** Replace with the domain name where the product is deployed |
|$HOST\-h5 |Mobile domain name<br><br><br>* **SaaS environment** Set to https://console.volcengine.com/bi\-h5<br><br>* **Private deployment environment** Replace with the domain name where the product is deployed for mobile |
|$APP_ID |Project ID. You can obtain it by opening any address under the project. As shown in the figure, open any link under a project; the URL is as follows, and the appId value is 1010681.<br><br>```Plain```<br>```https://console.volcengine.com/bi#/dashboard/47610?appId=1010681```<br>```plaintext```<br> |
|$DASHBOARD_ID |Open the dashboard to be embedded on the list page and obtain the browser URL as shown below; the dashboardId value is 47610.<br><br>```Plain```<br>```https://console.volcengine.com/bi#/dashboard/47610?appId=1010681```<br> |
|$REPORT_ID |Chart ID, identifies a unique chart. The `rid` in the visual query page URL represents the chart ID. In the following visual query link, the reportId value is 306828.<br><br>```Plain```<br>```https://console.volcengine.com/bi#/dataQuery?appId=1010681&id=98850742&rid=306828&sid=22569```<br> |
|$VSCREEN_ID |Large screen ID. In the following dashboard link, the value of vscreenId is 4750<br><br>```Plain```<br>```https://poc.volces.com/bi#/vScreen/4750?resizeMode=auto```<br> |


<span id="c0f415c6"></span>
## Step 2: Add feature modification link

Pass the `feature` parameter in the iframe URL to configure general features. The following is an explanation of these features; you can select the features you need according to your actual requirements.

```JSON
{
  "dashboard": {                       // --- 仪表盘模块特性 ---
    "showHeader": true,                // 显示Header
    "showFavor": true,                 // 显示收藏
    "showOwner": true,                 // 显示owner
    "actions": [                       // 仪表盘操作，数组类型
      "refresh",                       // 刷新
      "fullscreen",                    // 全屏
      "share",                         // 分享
      "subscribe",                     // 订阅
      "snapshot",                      // 书签
      "auth",                          // 授权
      "edit",                          // 编辑
      "setAsDefaultDashboard",         // 设为默认仪表盘
      "exportImage",                   // 导出图片
      "embed",                         // 嵌出
      "accessStatistics"               // 访问统计
    ],
    "report": {                        // --- 仪表盘图表特性 ---
      "showHeader": true,              // 显示header
      "actions": [                     // 仪表盘图表操作，数组类型
        "imgExport",                   // 导出图片
        "excelExport",                 // 导出excel
        "pivotExport",                 // 导出透视表
        "copyToDashboard",             // 复制图表
        "embed",                       // 嵌出图表
        "createMonitor"                // 新建监控
      ],
    },
    "sheet": {                         // --- 仪表盘sheet特性 ---
      "tabPosition": "top"             // tab页显示位置，可选top/left
    },
  }
}
```


**Feature description**


|Module division |Feature name |Feature description |Feature value |Scope of effect |
|---|---|---|---|---|
|dashboard |showHeader |Show or hide the dashboard header |true<br><br>false |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f77997b5291a4d248519795a46a39607~tplv-goo7wpa0wc-image.image) </span> |
|dashboard |showFavor |Show dashboard favorites. Only takes effect when showHeader is set to true |true<br><br>false |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dbcd531193c347e29bfc608cfdf249c8~tplv-goo7wpa0wc-image.image) </span> |
|dashboard |showOwner |Show the dashboard owner. Only takes effect when showHeader is set to true |true<br><br>false |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/26d7b40f02c14e74a0246584ceaba69d~tplv-goo7wpa0wc-image.image) </span> |
|dashboard |actions |* Dashboard actions, array type. Only takes effect when showHeader is set to true.<br><br>* Add the required actions directly to the array |refresh Refresh fullscreen Full screen<br><br>auth Authorize share Share<br><br>snapshot Bookmark<br><br>subscribe Create subscription and manage subscriptions<br><br>setAsDefaultDashboard Set as default dashboard / Unset as default dashboard<br><br>embed Embed<br><br>exportImage Export image |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ec4ee3a97bc04cf2bc4f9edfc5c27ddb~tplv-goo7wpa0wc-image.image) </span> |
|report |showHeader |Show chart header |true<br><br>false |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fe11a45013f5461caecd1b56721d00f7~tplv-goo7wpa0wc-image.image) </span> |
|report |actions |* Chart actions, array type. Only takes effect when showHeader of report is set to true.<br><br>* Add the required actions directly to the array |imgExport Export image<br><br>excelExport Download<br><br>createMonitor Create monitor<br><br>pivotExport Export pivot table. This feature is only available when a pivot table exists.<br><br>copyToDashboard Copy to dashboard<br><br>embed*Embed chart* |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/06810e87dd8f4866a11816b42f7c5fd3~tplv-goo7wpa0wc-image.image) </span><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fc1ae893ed604af790567da2ffeae3f4~tplv-goo7wpa0wc-image.image) </span> |
|sheet |tabPosition |Tab position when there are multiple sheets in the dashboard |top Top<br><br>left Left |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/428fdaf660c44f15ae7a8ae4e7df59b0~tplv-goo7wpa0wc-image.image) </span><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b4c666f4f5c64c8999c3dd36750f701a~tplv-goo7wpa0wc-image.image) </span> |


<span id="0cd85062"></span>
## Step 3: Generate code

Concatenate the code based on the information obtained above. For example, using the dashboard link:

```Plain
https://console.volcengine.com/bi#/external/dashboard/47610?appId=1010681&inline=true
```


<span id="ce8d70c3"></span>
### Generate HTML code

For example, the following code hides the dashboard header.

```HTML
<iframe allowfullscreen="true" src='https://console.volcengine.com/bi#/external/dashboard/47610?appId=1010681&inline=true&feature={"dashboard":{"showHeader":false}}' />
```


<span id="a007a59f"></span>
### Usage example


* If you are using the React framework, refer to the following example.

* Pass the `feature` parameter in the iframe URL to configure general features. The `feature` parameter should be a feature configuration object serialized with `JSON.stringify`. You can refer to the following iframe embedding code to hide the dashboard header.


```JavaScript
import React from 'react'
import ReactDOM from 'react-dom'

class EmbedComponent extends React.Component {
  render() {  
    return (      
      <iframe 
        allowFullScreen
        src={`https://console.volcengine.com/bi#/external/dashboard/47610?appId=1010681&inline=true&feature=${
          JSON.stringify(
            {
              dashboard: {    
                 showHeader: false
              }
            }
          )   
        }`}
      />    
    )  
  }
}

ReactDOM.render(<AeolusComponent />, document.querySelector('body'))
```
