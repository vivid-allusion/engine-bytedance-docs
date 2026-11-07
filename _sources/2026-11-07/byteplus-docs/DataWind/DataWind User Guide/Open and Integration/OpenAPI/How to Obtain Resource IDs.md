---
title: "How to Obtain Resource IDs"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/How_to_Obtain_Resource_IDs"
---

**A resource ID (Resource ID) is an identifier used to uniquely identify various types of "resources" in a computer system. Its core function is to accurately locate and distinguish different resource entities through standardized strings or numbers**. This article describes how to obtain the resource IDs for projects, datasets, dashboards, charts, and big screens (vscreen).

<span id="_1-项目（app）"></span>
# Project (app)

<span id="appid"></span>
## AppId

Project ID. The project ID can be obtained by opening any link within a project. As shown in the figure, open any link under a project. The URL is as follows, and the value of app_Id is 1010681.

```plaintext
https://console.volcengine.com/bi#/dashboard/47610?appId=1010681
```


<span id="34c1cec7"></span>
# Dataset (dataset)

<span id="a716891f"></span>
## DataSetId

Dataset ID. The dataset ID can be obtained by opening any link within a dataset. As shown in the figure, open any link in a dataset. The URL is as follows, and the value of dataSetId is 10285362.

```plaintext
https://console.volcengine.com/bi/datawind#/dataManage/detail/10285362?appId=20058765&belong=1&region=cn-beijing
```


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/878a508bd027434ea2a08f4eed2f4799~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-仪表盘（dashboard）"></span>
# Dashboard (dashboard)

All related IDs under a dashboard can be obtained from the dashboard page URL.

<span id="_2-1-dashboardid"></span>
## DashboardId

Open the dashboard to be embedded from the list page and obtain the browser URL as shown below. The value of dashboardId is 47610.

```plaintext
https://console.volcengine.com/bi#/dashboard/47610?appId=1010681
```


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/995648e07f0e4af897472936009c36a8~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-2-sheetid"></span>
## SheetId

[The new version of the dashboard](https://arcosite.bytedance.net/sites/1710493225840/65f8f721202f2c02eb982a3c/editor/65f8f72a38d1fd04c7bef851/?docLang=zh&bv=65f8f721202f2c02eb982a44) may contain multiple sheet pages. Each sheet page has a unique ID, which can be obtained by switching between different sheet pages. As shown in the figure, obtain the URL link, and the value of sheetId is 13815.

```plaintext
https://console.volcengine.com/bi#/dashboard/47780?appId=1010681&sheetId=13815
```


<span id="_3-图表（report）"></span>
# Chart (chart)

You can click the chart title on the dashboard page to enter the visual query. Obtain the following ID information from the visual query page URL.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2ad6f20d1cbf45c28eedb5762c4306c7~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c8078173ae084c179cead50ef46f9458~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-1-reportid"></span>
## ReportId

Chart ID, which identifies a unique chart. The `rid` in the visual query page URL represents the chart ID. In the following visual query link, the value of reportId is 306828.

```plaintext
https://console.volcengine.com/bi#/dataQuery?appId=1010681&id=98850742&rid=306828&sid=22569
```


<span id="_3-2-queryid"></span>
## QueryId

Query ID. Each chart query request generates a unique queryId. The `id` in the visual query page URL represents the query ID. In the following visual query link, the value of queryId is 98850742.

```plaintext
https://console.volcengine.com/bi#/dataQuery?appId=1010681&id=98850742&rid=306828&sid=22569
```


<span id="_4-大屏（vscreen）"></span>
# Big screen (VScreen)

You can click the View button on the big screen page to enter the big screen view page and obtain the big screen ID from the URL on the view page.

<span id="vscreenid"></span>
## VScreenId

Big screen ID. In the following dashboard link, the value of vscreenId is 4750

```plaintext
https://poc.volces.com/bi#/vScreen/4750?resizeMode=auto
```


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ac7ac384d33d4f6fbfb26fedd5fca938~tplv-goo7wpa0wc-image.image) </span>
