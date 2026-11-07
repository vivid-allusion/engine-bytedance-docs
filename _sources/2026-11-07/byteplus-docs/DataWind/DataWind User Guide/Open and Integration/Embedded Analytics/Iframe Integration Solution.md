---
title: "Iframe Integration Solution"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Iframe_Integration_Solution"
---

<span id="_1-前提"></span>
# 1. Prerequisites

This operation must be performed by a developer. It is recommended to grant the developer the permission to embed third\-party resources in the target project. For convenience, project administrator permissions are suggested. After completing the operation, assign permissions as needed based on the actual situation. For details about permissions, see [Permission Overview](https://docs.byteplus.com/docs/DataWind/Permission_Overview)

<span id="_2-操作步骤"></span>
# 2. Operation steps

<span id="_2-1-step1-获得目标仪表盘-图表的-url-链接"></span>
## 2.1 Step 1. Obtain the URL link and jwtToken of the target dashboard/chart

Obtain the target resource URL from the URL configuration in [URL Configuration](https://docs.byteplus.com/docs/DataWind/URL_Configuration).

To obtain the jwtToken, refer to [Chart Embedding](https://docs.byteplus.com/docs/DataWind/Chart_Embedding).

<span id="_2-2-step2-加入自定义参数"></span>
## 2.2 Step 2. Add custom parameters

<span id="_2-2-1-自定义参数"></span>
### 2.2.1 Custom parameters

You can pass custom parameters to change the embedding effect:


* **inline** \- Must be set to `true`, indicating the use of embed mode

* **feature** \- Feature configuration, used to control the display or hiding of some interface functions or their presentation. For detailed usage, see [Feature Configuration](https://docs.byteplus.com/docs/DataWind/Feature_Configuration).

* **filter** \- Filter parameter configuration. When embedding a dashboard, you can override the default value of the public filter. When embedding a chart, you can override the chart filter fields. For detailed usage, see [Override Filters](https://docs.byteplus.com/docs/DataWind/Override_Filters).


<span id="_2-2-2-示例"></span>
### 2.2.2 Example


* Embed a single dashboard


```Plain
https://console.volcengine.com/bi/datawind-open/#/external/dashboard/36154?appId=1000157&inline=true&jwtToken={jwtToken}
```



* Embed a dashboard, hide the header, and override the op of the `Region` public filter to `in`, with value set to `'East','South'`


```Plain
https://console.volcengine.com/bi/datawind-open/#/external/dashboard/36154?appId=1000157&inline=true&jwtToken={jwtToken}&feature={"dashboard": {"showHeader": false }}&filter=Region in 'East','South'
```


<span id="_2-3-step3-生成代码"></span>
## 2.3 Step 3. Generate code

Combine the information obtained above to construct the code. For example, using the obtained dashboard link:

```plain
https://console.volcengine.com/bi/datawind-open/external/#/dashboard/47610?appId=1010681&inline=true&jwtToken={jwtToken}
```


<span id="_2-3-1-生成-html-代码"></span>
### 2.3.1 Generate HTML code

For example, the following code hides the dashboard header

```html
<iframe allowfullscreen="true" src='https://console.volcengine.com/bi/datawind-open/#/external/dashboard/47610?appId=1010681&inline=true&jwtToken={jwtToken}&feature={"dashboard":{"showHeader":false}}' />
```


<span id="_2-3-2-使用实例"></span>
### 2.3.2 Usage example


* If using the React framework, refer to the following example

* Pass the `feature` parameter in the iframe URL to configure general features. The type of `feature` is the feature configuration object after `JSON.stringify`. You can refer to the following iframe embedding code to hide the dashboard header


```javascript
import React from 'react'
import ReactDOM from 'react-dom'

class AeolusComponent extends React.Component {
  render() {  
    return (      
      <iframe 
        allowFullScreen
        src={`https://console.volcengine.com/bi/datawind-open/#/external/dashboard/47610?appId=1010681&inline=true&jwtToken={jwtToken}&feature=${JSON.stringify(             
              {               
                dashboard: {    
                  showHeader: false          
                }          
              }      
        )}`}
      />
    )
  }
}
ReactDOM.render(<AeolusComponent />, document.querySelector('body'))
```
