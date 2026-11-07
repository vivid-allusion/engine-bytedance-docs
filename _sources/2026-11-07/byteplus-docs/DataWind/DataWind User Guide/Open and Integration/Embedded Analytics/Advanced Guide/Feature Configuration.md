---
title: "Feature Configuration"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Feature_Configuration"
---

To meet the needs of integrators for page customization, DataWind defines a set of general feature configurations. The commonly used feature configurations and default values for the dashboard module and visualization query module are as follows:

<span id="_1-特性清单"></span>
# 1. Feature list

```Plain
{
  "dashboard": {                       // --- 仪表盘模块特性 ---
    "showHeader": true,                // 显示Header
    "showTitle": true,                 // 显示标题
    "showFavor": true,                 // 显示收藏
    "enableAutoRefresh": true,         // 启用自动刷新
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
    "showOwner": true,                 // 显示owner
    "showSideMenu": true,              // 显示仪表盘列表
    "showDescription": true,           // 显示描述
    "report": {                        // --- 仪表盘图表特性 ---
      "showTitle": true,               // 显示标题
      "showOwner": true,               // 显示owner
      "showDesc": true,                // 显示图表描述
      "showHeader": true,              // 显示header
      "showToolbar": true,             // 显示工具栏
      "actions": [                     // 仪表盘图表操作，数组类型
        "imgExport",                   // 导出图片
        "excelExport",                 // 导出excel
        "pivotExport",                 // 导出透视表
        "copyToDashboard",             // 复制图表
        "embed",                       // 嵌出图表
        "createMonitor"                // 新建监控
      ],
      "editable": true,                // 显示编辑操作
      "enableEnterVizQuery": true,     // 启用进入可视化查询按钮
      "enableCustomEnterVizQueryHandler": false  // 自定义处理进入可视化查询
    },
    "sideMenu": {                      // --- 仪表盘列表特性 ---
      "actions": [                     // 仪表盘列表操作，数组类型
        "createDashboard",             // 创建仪表盘
        "createFolder"                 // 创建文件夹
      ]
    },
    "sheet": {                         // --- 仪表盘sheet特性 ---
      "tabPosition": "top"             // tab页显示位置，可选top/left
    },
  },
  "vizQuery": {                        // --- 可视化模块特性 ---
    "showSave": true,                  // 显示保存
    "showSaveAs": true,                // 显示另存为
    "showHeader": true,                // 显示header
    "showAutoQuery": true,             // 显示自动查询
    "showSample": true,                // 显示抽样
    "showRoutine": true,               // 显示例行
    "showQueryHistory": true,          // 显示查询历史
    "showIndexPlatform": true,         // 显示指标平台入口
    "showResultTooltip": true,         // 显示查询结果小灯泡
    "showMonitor": true,               // 显示监控报警
    "dataSet": {                       // --- 可视化数据集特性 ---
      "actions": [                     // 数据集列表操作
        "switchDataSet",               // 切换数据集
        "addField",                    // 添加字段
        "addMultipleFields",           // 批量添加字段
        "checkDataSet"                 // 查看数据集详情
      ],
      "fieldActions": [                // 数据集字段操作
        "modifyExpr",                  // 修改表达式
        "delete"                       // 删除字段
      ]
    },
    "switchDataSetModal": {            // --- 可视化切换数据集弹窗特性 ---
      "showOwner": true                // 显示Owner
    },
    "saveModal": {                          // --- 可视化保存/另存为弹窗特性 ---
        "showSaveToPublicDashboard": true,    // 另存为时仪表盘目录显示公共仪表盘
        "showCreateDashboard": true           // 显示创建仪表盘
    },
    "addFieldModal": {                      // --- 可视化添加字段弹窗特性 ---
      "showParameterManagementEntry": true, // 显示参数管理入口
    }
  },
  "peopleMeta": true,                  // 显示用户元数据，包括仪表盘的所有者头像、图表的联系所有者图标等
}
```


Caution: Only the configuration in `dashboard.report` takes effect when embedding individual dashboard charts. Other configurations will not take effect. For example, when embedding a dashboard chart, `dashboard.enableAutoRefresh` will not take effect.

**Feature description**


|Module division |Feature name |Feature description |Feature value |Scope of effect |
|---|---|---|---|---|
|dashboard |showHeader |Whether to show or hide the dashboard header |true<br><br>false |<span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_9c75b9c2734163e44d7048630a6b75f9) </span> |
|dashboard |showFavor |Whether to show the option to favorite the dashboard. Only takes effect when showHeader is true. |true<br><br>false |<span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_4217c09fb98d7a6fda6aca07995bb79f) </span> |
|dashboard |showOwner |Whether to show the owner of the dashboard. Only takes effect when showHeader is true. |true<br><br>false |<span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_1e553c13951059e7b14b08cc8a5794e4) </span> |
|dashboard |actions |* Dashboard actions (array type). Only takes effect when showHeader is true.<br><br>* Simply add the required actions to the array. |refresh (Refresh), fullscreen (Full screen), auth (Authorization), share (Share)<br><br>snapshot (Bookmark)<br><br>subscribe (Create subscription and subscription management), setAsDefaultDashboard (Set as default dashboard / Cancel set as default dashboard)<br><br>embed (Embed)<br><br>exportImage (Export image) |<span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_0a7f41d48d2f0a42b743df445084cf08) </span> |
|report |showHeader |Whether to show the chart header |true<br><br>false |<span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_b450c1e4c3c2184da5f9814b1a2ca53f.png) </span> |
|report |actions |* Chart actions (array type). Only takes effect when report's showHeader is true.<br><br>* Simply add the required actions to the array. |imgExport (Export image), excelExport (Download), createMonitor (Create monitor)<br><br>pivotExport (Export pivot table; this feature is only available for pivot tables), copyToDashboard (Copy to dashboard), embed*Embed chart* |<span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_795edac9045bd8f732c0dfb0b0951999) </span><br><br><span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_d723fa0fe6992e483dd2a8d9ef82b927) </span> |
|sheet |tabPosition |Tab display position when there are multiple sheets in the dashboard |top (Top)<br><br>left (Left) |<span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_83ab36cbcefd370c931675841d0c103f) </span><br><br><span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_1aa97facbb81add132d243c9b0b3f9c9) </span> |


<span id="_2-特性说明"></span>
# 2. Feature description

<span id="_2-1-在-iframe-中使用"></span>
## 2.1 Usage in iframe

Pass the `feature` parameter in the iframe URL to configure general features. The `feature` parameter should be a feature configuration object stringified by `JSON.stringify`. Refer to the following iframe embedding code to hide the dashboard header.

```Plain
import React from 'react'
import ReactDOM from 'react-dom'

class BIComponent extends React.Component {
  render() {
    return (
      <iframe 
        src={`https://console.volcengine.com/bi/datawind/#/external/dashboard/36154?appId=1000157&inline=true&feature=${
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

ReactDOM.render(<BIComponent />, document.querySelector('body'))

```


<span id="_2-2-在-sdk-中使用"></span>
## 2.2 Usage in SDK

In the SDK component, you can pass the `feature` parameter to configure general features. The type of `feature` is a feature configuration object. The following SDK component example hides the dashboard header.

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
        feature={{
          dashboard: {
            showHeader: false
          }
        }}
      />
    )
  }
}

ReactDOM.render(<BIComponent />, document.querySelector('body'))

```
