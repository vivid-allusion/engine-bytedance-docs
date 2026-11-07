---
title: "URL Configuration"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/URL_Configuration"
---

<span id="_1-获得-url-链接"></span>
# 1. Obtain a URL link

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Both methods below can be used to obtain the target dashboard, chart, or large screen link, and the results are the same.</div>


* <div data-tips="true" data-tips-type="warning">The link to the mobile dashboard can only be obtained using the second method.</div>



<span id="_1-1-直接在-datawind-中获得"></span>
## 1.1 Obtain directly in DataWind

<span id="_1-1-1-仪表盘-图表"></span>
### 1.1.1 Dashboard/Chart

As described in [Chart Embedding](https://docs.byteplus.com/docs/DataWind/Chart_Embedding), directly obtain the link for the dashboard or chart.

**Note: Select Embed directly as shown below. There is no need to check any boxes.** 

<span id="_1-1-2-大屏"></span>
### 1.1.2 Large screen

As shown in the figure, select View on the list page. After opening, obtain the URL from the browser.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e932ec39afe64084b1e866e88a29395f~tplv-goo7wpa0wc-image.image) </span>

<span id="_1-2-自行拼接"></span>
## 1.2 Construct manually

If you choose to construct manually, follow the method below. The underlined content is a variable, which will be explained in the parameter details below. The rest is fixed content.

**Dashboard** <ins>$HOST</ins>/#/external/dashboard/<ins>DASHBOARD_ID</ins>?appId=<ins>APP_ID</ins>&inline=true

For example:

```plain
https://console.volcengine.com/bi/datawind-open/#/external/dashboard/47610?appId=1010681&inline=true
```


**Mobile dashboard** <ins>$HOST\-h5</ins>/dashboard/?appId=<ins>APP_ID</ins>&id=<ins>DASHBOARD_ID</ins>&inline=true

For example:

```plain
https://console.volcengine.com/bi/datawind-h5/dashboard/?appId=1010681&id=47610&inline=true
```


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The mobile link can only be accessed on mobile devices. If the link is opened on a PC, it will automatically redirect to the PC link by default.</div>


**Chart** <ins>$HOST</ins>/#/external/dashboard/<ins>DASHBOARD_ID</ins>/<ins>REPORT_ID</ins>?appId=<ins>APP_ID</ins>&inline=true

For example:

```plain
https://console.volcengine.com/bi/datawind-open/#/external/dashboard/47610/305962?appId=1010681&inline=true
```


**Large screen**

<ins>$HOST</ins>/vScreen/preview?appId=<ins>APP_ID</ins>&id=<ins>VSCREEN_ID</ins>&resizeMode=auto

For example:

```plain
https://console.volcengine.com/bi/datawind-open/#/vScreen/preview?appId=1010681&id=11&resizeMode=auto
```


**Parameter details:** 


|**Parameter** |**Description** |
|---|---|
|$HOST |* **SaaS environment** set to https://console.volcengine.com/bi/datawind\-open<br><br>* For a private deployment environment, replace with the domain name of your product deployment. |
|$HOST\-h5 |Mobile domain name<br><br><br>* **SaaS environment** set to https://console.volcengine.com/bi/datawind\-open\-h5<br><br>* For a private deployment environment, replace with the domain name of your product's mobile deployment. |
|APP_ID |Project ID of DataWind; see [How to Obtain Resource IDs](https://docs.byteplus.com/docs/DataWind/How_to_Obtain_Resource_IDs) for details |
|DASHBOARD_ID |Dashboard ID; see [How to Obtain Resource IDs](https://docs.byteplus.com/docs/DataWind/How_to_Obtain_Resource_IDs) for details |
|REPORT_ID |Chart ID; see [How to Obtain Resource IDs](https://docs.byteplus.com/docs/DataWind/How_to_Obtain_Resource_IDs) for details |
|VSCREEN_ID |Large screen ID; see [How to Obtain Resource IDs](https://docs.byteplus.com/docs/DataWind/How_to_Obtain_Resource_IDs) for details |


<span id="_2-在-iframe-中使用"></span>
# 2. Use in an iframe

The following code embeds a dashboard in the SaaS environment.

```Plain
<iframe src='https://console.volcengine.com/bi/datawind-open/#/external/dashboard/******?appId=******&inline=true'>
```


<span id="_3-在-sdk-中使用"></span>
# 3. Use in the SDK

Pass the `urlPrefix` parameter to the component to specify the access address.

```js
import React from 'react'
import ReactDOM from 'react-dom'

class BIComponent extends React.Component {
  render() {
    return (
      <bi-dashboard
        urlPrefix='https://console.volcengine.com/bi/datawind-open'
        appId='******'
        dashboardId='******'
      />
    )
  }
}

ReactDOM.render(<BIComponent />, document.querySelector('body'))
```
