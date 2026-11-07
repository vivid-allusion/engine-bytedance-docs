---
title: "Delivering event monitoring information to TLS"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Delivering-event-monitoring-data-to-TLS"
---

This topic mainly describes how to deliver information about events triggered by instances under  platform accounts to TLS. This helps you perform TLS\-based analysis more conveniently.

<span id=".5LuA5LmI5piv5pel5b-X5pyN5Yqh"></span>
## What is TLS

[Torch Log Service](https://docs.byteplus.com/en/docs/tls/What_is_TLS) (TLS) is a one\-stop, log data\-targeted service provided by the  platform. Its capabilities include log collection, massive storage, search and analysis, monitoring and alerts, and data visualization. Its applicable scenarios cover application O&M, service monitoring, and classified protection compliance for comprehensively enhancing R&D and O&M efficiency.

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenario

When you have multiple ECS instances under your  account, you can deliver information about events triggered during instance operations (such as a "SystemFailure.Redeploy" event) to TLS. This allows you to easily learn operations and conditions of each instance based on TLS features such as massive storage, search and analysis, and data visualization. Therefore, you can improve O&M and analysis efficiency.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* You have created an [ECS instance](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).

* You have enabled [TLS](https://docs.byteplus.com/en/docs/tls/What_is_TLS).

* You have enabled [Cloud Monitor](https://docs.byteplus.com/en/docs/cloudmonitor/What-is-Vitality-Cloud-Monitor).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5q2l6aqk5LiA77ya5Yib5bu65pel5b-X6aG555uu"></span>
### Step 1: Create a log project

Event information delivered to TLS is stored as logs, with tenant resources isolated and controlled based on log project. You can create log projects based on your needs. Typically, one log project is created based on a specific application, business, or product.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To reduce network latency, create log projects in a region that is geographically close to your business.</div>



1. Log in to the [TLS console](https://console.byteplus.com/tls).

2. Select "Log Project Management" in the left navigation pane to enter the log project list page.

3. In the top menu bar, select a region close to your business.

4. Click the "Create project" button and follow the instructions to enter log topic\-related information. For parameter details, see [Creating log projects](https://docs.byteplus.com/en/docs/tls/getting_started_creating_resources#create-a-project).

5. Click the "Confirm" button to complete the creation.


<span id=".5q2l6aqk5LqM77ya5Yib5bu65pel5b-X5Li76aKY"></span>
### Step 2: Create a log topic

Log topic is classified as the unit for collecting, reading, and writing log data. Based on your needs, you can create multiple log topics under the same log project to differentiate events based on type, business, and other categories.


1. Log in to the [TLS console](https://console.byteplus.com/tls).

2. Select "Log Project Management" in the left navigation pane to enter the log project list page.

3. Click the target log project name to enter the project details page.

4. Click the "Create topic" button and enter topic information as instructed. For parameter details, see [Creating log topics](https://docs.byteplus.com/en/docs/tls/getting_started_creating_resources#create-a-topic).

5. Click "Confirm" to complete the creation.


<span id=".5q2l6aqk5LiJ77ya6YWN572u57Si5byV"></span>
### Step 3: Configure an index

Before using TLS for search and analysis, you need to configure an index for the log topic.


1. Log in to the [TLS console](https://console.byteplus.com/tls).

2. Select "Log Project Management" in the left navigation pane to enter the log project list page.

3. Click the target log project name to enter the project details page.

4. In the "Actions" column of the target log topic, click the "Index configuration" button to enter the index configuration page.

5. Configure as shown below.

6. Click the "Confirm" button, and in the confirmation pop\-up window, click the "Confirm" button to complete the configuration.


<span id=".5q2l6aqk5Zub77ya5Yib5bu65LqL5Lu26KeE5YiZ"></span>
### Step 4: Create an event rule

To create an event delivery rule, you need to specify the event type to be delivered to TLS and the target log topic. When an instance under your account triggers an event of the specified type, Cloud Monitor automatically delivers the relevant information to TLS in real time.


1. Log in to the [Cloud Monitor console](https://console.byteplus.com/cloud-monitor/overview).

2. In the left navigation pane, select "Event Center \> Event Rule" to enter the Event Rule page.

3. Click the "Create event rule" button and follow the instructions to configure the event rule. For parameter details, see [Creating event rules](https://docs.byteplus.com/en/docs/cloudmonitor/Creating-an-event-rule).

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Select "Delivery method \> Delivery channel", check "log service", and then click the "Add a delivery topic" button. Next, select the region, project, and log project name of the log topic you created in steps 3 and 4.   </div>
   

4. Click the "Confirm" button to complete the rule creation.


<span id=".5p-l55yL57uT5p6c"></span>
## View results

After an instance triggers the specified event, you can view the corresponding log information in the TLS console.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For your ECS instances located in different regions under the same  account, all of their log information of the triggered events is displayed in TLS.</div>



1. Log in to the [TLS console](https://console.byteplus.com/tls).

2. Select "Log Project Management" in the left navigation pane to enter the log project list page.

3. Click the name of the target log project to enter the log project page.

4. Select "Query and analysis" in the left navigation pane to enter the search and analysis page.

5. In the "Topic" column, select the name of the target log topic.

   > The topic field is used to specify the data scope to be searched and analyzed. After you select a log topic, there is no need to specify a data scope via the from clause in the search and analysis statement.   
   

6. Specify the time range

   > The default time range is 5 minutes, and you can also customize the time range to be searched. When the specified time range exceeds the retention period of the log data, the expired and deleted data can not be retrieved.   
   

7. Click the "Query and analysis" button to view relevant information.

   In the "Query results" area, basic information about the current log analysis is displayed, including the total number of logs and whether the query results are accurate. For more details, see [Analyzing logs](https://docs.byteplus.com/en/docs/tls/Analyze-logs-2).

8. To query and analyze event monitoring logs, the following methods are also supported:

   1. Enter the search and analysis statement in the input box, and analyze the result data statistics that meet the search criteria. For details, refer to [Analysis overview](https://docs.byteplus.com/en/docs/tls/Analysis-overview).

   2. Select the "chart analysis" tab to view analysis results. For details, see [Viewing analysis charts](https://docs.byteplus.com/en/docs/tls/Analyze-logs-2#view-analysis-charts).
