---
title: "Query Task List"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Query_Task_List_"
---

DataFinder provides you with a query task list page, where you can view the task list, task status, and other details corresponding to asynchronous query tasks, asynchronous download tasks. This article introduces you to the details page for asynchronous query tasks and asynchronous download tasks.

<span id="8ef4ef74"></span>
# Enter the query task list

After logging in and entering the DataFinder console, click the top navigation, Application Management \> Task Management \> Query Task List, and you can enter the Query Task List page.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1220f5d744674954984db6e424f48610~tplv-goo7wpa0wc-image.image) </span>

<span id="822053d6"></span>
## Supported task types

The current page shows you the task list and task details for asynchronous query and asynchronous download tasks.


* Asynchronous Query: Shows you asynchronous data query tasks triggered by analytics tools. Usually when the amount of query data is relatively large and the wait exceeds 10 seconds, you will be prompted to manually create asynchronous query tasks on the analysis tools page. For details, please refer to the following [Asynchronous query task description](https://docs.byteplus.com/docs/DataFinder/Query_Task_List#ea1f1b41)sections.

* Asynchronous download: Shows you the asynchronous download task triggered by the analysis tool. Usually when the actual query data is more than the query data displayed on the page, you can trigger the asynchronous download task to download the full amount of query result data, see the following [Asynchronous download task description](https://docs.byteplus.com/docs/DataFinder/Query_Task_List#b500e0e0)section.


<span id="8d8327f6"></span>
## Supported analysis tools


|Analysis tool |Whether to support asynchronous queries |Whether to support asynchronous download |
|---|---|---|
|Event Analysis |✔️ |✔️ |
|Custom Retention |✔️ |❌ |
|Funnel Analysis |✔️ |❌ |
|Distribution Analysis |✔️ |❌ |
|User Composition |✔️ |❌ |
|User Path |✔️ |❌ |
|Attribution Analysis |❌ |❌ |
|User Lifecycle |❌ |❌ |
|Heat Map Analysis |❌ |❌ |
|LTV Analysis |✔️ |❌ |
|Item Analysis |✔️ |❌ |
|Custom SQL query |❌ |❌ |


<span id="ea1f1b41"></span>
# Asynchronous query task description

In order to improve the user's data query experience and avoid the long waiting time for data queries due to some special scenarios, the asynchronous query task function is launched, which can be calculated asynchronously in the background by creating a query task. After the query is completed, the query results will be reached to the user through the "in\-app letter".

Scenarios for asynchronous query tasks include:


* When the amount of query data is too large or the query cycle is long, and the cache cannot be hit, the asynchronous query task can be triggered and used after waiting for more than 10 seconds.

* When the number of queries is large and the cache cannot be hit, the asynchronous query task can be triggered and used after waiting for more than 10 seconds.


<span id="_2-使用流程"></span>
## Conditions that trigger an asynchronous query task

After configuring the conditions on the analysis tool page, initiate a query. After the query exceeds 10s, the query task creation pop\-up window will automatically pop up:

<span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_01e2da1a6d48bff8659b6ab39121950c) </span>

<span id="7c6ccd0a"></span>
## Create asynchronous query task

Make sure that the information of the query task is correct and submit the task. The query will be calculated in the background. At this time, you can continue to use the Finder for analysis operations. After the query results are completed, they will be contacted to you through the "in\-app letter".

<span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_e5a5bebd896e26fb01009555309cecf6) </span>

<span id="_2-3-站内信触达结果"></span>
## **Asynchronous query result notification: in\-app letter**

After the query results are completed, get the query results through the "in\-app letter" in the upper right corner of the system, and click hyperlinke to enter the details page.

<span id="_2-4-查询任务列表"></span>
## **View the asynchronous query task list**

Ordinary users can view and manage all query tasks in the task list, including canceling queries and restarting queries

Administrator users can view and manage all query tasks under the application in addition to the query tasks submitted by themselves

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d156b362a8044ec1807dc7b7417dba80~tplv-goo7wpa0wc-image.image) </span>

<span id="b500e0e0"></span>
# Asynchronous download task description

<span id="1ed2d585"></span>
## Precautions


* Since asynchronous downloads are usually large\-scale data downloads, which have a significant impact on overall performance and stability. Usually, up to 6 asynchronous download tasks can be executed in parallel. It is recommended that you try to avoid creating multiple asynchronous download tasks simultaneously.

* The current DataFinder will keep the results of asynchronous download tasks created within the past 30 days for you. You can download the result data locally as soon as the asynchronous download task finishes running.


<span id="7b7c6eab"></span>
## Conditions that trigger the asynchronous download task

On the Event Analysis page, if you configure attribute grouping and the actual number of groupings is greater than the number of groupings displayed on the configured page, the asynchronous download task can be triggered.

For example, you have configured to use "user IDs" for grouping, and the page query results show the top 50 grouped result data.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f818d4a1e30d4817bdbf534b3403ec54~tplv-goo7wpa0wc-image.image) </span>


* If there are 200 groups after the actual user ID is grouped, the actual group result is more than the number of groups displayed on the page, triggering the entry of the asynchronous download task.

* If there are 10 groups after the actual user ID is grouped, the actual group result is less than the number of groups displayed on the page, and the entry of the asynchronous download task is not triggered.


<span id="c44bf806"></span>
## Create asynchronous download task

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2f0d755b4a6846d8ab94b7ad00c68cfb~tplv-goo7wpa0wc-image.image) </span>

After triggering the asynchronous download task, when downloading the query analysis results, it supports flexible selection of the downloaded data range, and supports selection:


* **Page Results:**  Downloading data directly from the current query results page is a real\-time data download process that downloads data directly to your local computer.

* **More data:**  If you need to download data beyond the scope of the page display to select Download "More data", the subsequent DataFinder will create an asynchronous download task to ensure that the downloaded data is all grouped result data.


<span id="8a7d8879"></span>
## Notification of asynchronous download task running result: in\-app letter

After the asynchronous download task is completed, you will be notified via an in\-app letter.

<span id="f694db60"></span>
## View and download the resulting data

You can export data in **App Management** \> **Task Management** \> **Query Task List** and download the data locally.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d1704a5de5ce443aadabb36e60944c3c~tplv-goo7wpa0wc-image.image) </span>
