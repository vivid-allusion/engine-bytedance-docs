---
title: "Set parameters for embedding a console page"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Setting_parameters_for_embedding_a_console_page"
---

Torch Log Service (TLS) allows you to embed pages such as the query and analysis page and dashboard pages of the TLS console into a self\-managed website. When you configure the URL of a console page for password\-free access, specify URL parameters to customize the display effect of the console page that you want to embed.

<span id=".6aG16Z2iLXVybC3moLzlvI8="></span>
## URL format

When you configure the URL of a console page for password\-free access, set `redirectURI` to the encoded URL of the console page. The URL format is as follows:


* Query and analysis page

   ```SQL
   https://console.byteplus-embed.com/tls/region:tls+${regionId}/project/${projectId}/search?UI_Parameter1&UI_Parameter2
   ```
   

* Dashboard page

   ```SQL
   https://console.byteplus-embed.com/tls/region:tls+${regionId}/project/${projectId}/dashboard/${dashboardId}?UI_Parameter1&UI_Parameter2
   ```
   


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">说明</div>



* <div data-tips="true" data-tips-type="tip"><code>${regionId}</code>: the ID of the Region where the TLS resource is located. For TLS Region IDs, refer to <a href="https://docs.byteplus.com/en/docs/tls/endpoint">Endpoints</a>.</div>


* <div data-tips="true" data-tips-type="tip"><code>${projectId}</code>: the project ID. You can view the project ID in the TLS console. For more information, refer to <a href="https://docs.byteplus.com/en/docs/tls/Managing_projects">Manage a project</a>.</div>


* <div data-tips="true" data-tips-type="tip"><code>${dashboardId}</code>:the Dashboard ID. You can view the Dashboard ID in the TLS console.</div>


* <div data-tips="true" data-tips-type="tip">It supports to add UI parameters, multiple parameters are connected through <code>&</code>, and need to be added after <code>?</code>. </div>



<span id=".dWkt5Y-C5pWw"></span>
## UI parameters

TLS offers the following UI parameters for configuring redirect URLs.

<span id="345c77f4"></span>
### Query and analysis page parameters


|Parameter |Type |Required |Example |Description |
|---|---|---|---|---|
|`hideLeftBar` |Boolean |No |true |Specify whether to hide the left\-side navigation pane from the TLS console.<br><br><br>* true: hide.<br><br>* false: display. This is the default value. |
|`hideTitle` |Boolean |No |true |Specify whether to hide the title bar on the **query and analysis** page from the TLS console.<br><br><br>* true: hide.<br><br>* false: display. This is the default value. |
|`hideTopic` |Boolean |No |true |Specify whether to hide the **Topic** checkbox on the **query and analysis** page from the TLS console.<br><br><br>* true: hide.<br><br>* false: display. This is the default value. |
|`hideIndexBtn` |Boolean |No |true |Specify whether to hide the **Index configuration** button on the **query and analysis** page from the TLS console.<br><br><br>* true: hide.<br><br>* false: display. This is the default value. |
|`hideShareBtn` |Boolean |No |true |Specify whether to hide the **Share** icon on the **query and analysis** page from the TLS console.<br><br><br>* true: hide.<br><br>* false: display. This is the default value. |
|`topicId` |String |No |`c5c0a2a1-8431-4370-b98c-d20f5f7d****` |The topic ID. You can view the topic ID in the TLS console. For more information, refer to [Manage a topic](https://docs.byteplus.com/en/docs/tls/Managing_topics). |
|`codebase64` |String |No |`KiB8IHNlbGVjdCAq` |Specify the default query statement that is encoded with Base64Url. |
|`time` |String |No |`now-1m,now` |Specify the time range for querying logs. You can specify a fixed time range or a custom time range.<br><br><br>* Custom time range: specify a time range in the following format: `${startTime},${endTime}`. Wherein, `startTime` and `endTime` must be in the `YYYY-MM-DD HH:mm:ss.SSS` format.<br><br>* For more information on fixed time ranges, refer to the table below. |


<span id="dea092e4"></span>
### Dashboard page parameters


|Parameter name |Data type |Is required |Example |Description |
|---|---|---|---|---|
|`Time` |String |Optional |`Now-1m, now` |Set the time range for the logs to be queried. For more information, refer to Time Field Enumeration Value . |
|`refreshTime` |String |Optional |1M |Set the refresh rate of the dashboard. For more information, refer to Time Field Enumeration Value . |
|`Filter- ${filterName} = ${value}` |String |Optional |`Filter-a = v1` |Set dashboard filter defaults, you can use `filter-a = v1 & filter-a = v2`to set multiple defaults. |
|`Temp [Fixed \| Hidden] Var- ${key} = ${value}` |String |Optional |`tempFixedVar-httpStatusCode=200` |Add temporary variables, `${key}` is the variable name, `${value}` is the variable value, `Fixed` and `Hidden` are used to control whether the variable is displayed in the dashboard.<br><br><br>* When `Fixed` and `Hidden` are not selected, the variable is displayed in the dashboard and can be deleted.<br><br>* When `Fixed` is selected, the variable is displayed in the dashboard but is not allowed to be deleted.<br><br>* When `Hidden` is selected, the variable is not displayed in the dashboard. |
|`Temp [Fixed \| Hidden] Filter- ${name} = ${value}` |String |Optional |`tempFixedFilter-name=1` |Add a temporary filter condition, `${key}` is the field name, `${value}` is the field value, the actual value of `${value}` will be concatenated after the query statement. `Fixed` and `Hidden` are used to control whether the filter is displayed in the dashboard.<br><br><br>* When `Fixed` and `Hidden` are not selected, the filter is displayed in the dashboard and can be deleted.<br><br>* When `Fixed` is selected, the filter is displayed in the dashboard but deletion is not allowed.<br><br>* When `Hidden` is selected, the filter criteria are not displayed in the dashboard. |
|`hideFilters = ${filterNameList}` |String [] or 'all' |Optional |`hideFilters = ["a", "b`<br><br>`"]` |The list of hidden filter names.<br><br>When set to `all`, it hides all filters. |
|`fixedFilters = ${filterNameList}` |String [] or 'all' |Optional |`fixedFilters = ["a", "b`<br><br>`"]` |The list of filters to be displayed is not editable.<br><br>When set to `all`, all filters are fixed. |
|`Readonly` |Boolean |Optional |true |Whether to set to read\-only mode.<br><br><br>* true: (default) read\-only mode. In read\-only mode, some UI elements are automatically hidden.<br><br>* false: Edit mode. |
|`hideLeftBar` |Boolean |Optional |false |Whether to hide the navigation bar on the left side of the TLS console.<br><br><br>* true: hidden.<br><br>* false: display. This is the default value. |
|`hideHeader` |Boolean |Optional |false |Whether to hide the top menu bar of the dashboard in the TLS console, including the dashboard title, share button, and toolbar module.<br><br><br>* true: hidden.<br><br>* false: display. This is the default value. |
|`hideTitle` |Boolean |Optional |false |Whether to hide the title of the dashboard in the TLS console.<br><br><br>* true: hidden.<br><br>* false: display. This is the default value. |
|`hideShareBtn` |Boolean |Optional |false |Whether to hide the **Share** button of the dashboard in the TLS console.<br><br><br>* true: hidden.<br><br>* false: display. This is the default value. |
|`hideToolbar` |Boolean |Optional |false |Whether to hide the toolbar of the dashboard in the TLS console.<br><br><br>* true: hidden. Fixed to true in read\-only mode.<br><br>* false: display. This is the default value. |
|`hideSettings` |Boolean |Optional |false |Whether to hide the **Settings** button for the dashboard in the TLS console.<br><br><br>* true: hidden. Fixed to true in read\-only mode.<br><br>* false: display. This is the default value. |
|`hideSubscribeBtn` |Boolean |Optional |false |Whether to hide the \*\*Subscribe \*\*button for the dashboard in the TLS console.<br><br><br>* true: hidden. Fixed to true in read\-only mode.<br><br>* false: display. This is the default value. |
|`hideTimeSelector` |Boolean |Optional |false |Whether to hide the **time selection** button for the dashboard in the TLS console.<br><br><br>* true: hidden.<br><br>* false: display. This is the default value. |
|`hideRefreshSelector` |Boolean |Optional |false |Whether to hide the **auto\-refresh** button of the dashboard in the TLS console.<br><br><br>* true: hidden.<br><br>* false: display. This is the default value. |
|`hideFullScreenBtn` |Boolean |Optional |false |Whether to hide the **full screen** button of the dashboard in the Log Services Console.<br><br><br>* true: hidden.<br><br>* false: display. This is the default value. |
|`hideAddChartBtn` |Boolean |Optional |false |Whether to hide the **Add Chart** button for the dashboard in the TLS console.<br><br><br>* true: hidden. Fixed to true in read\-only mode.<br><br>* false: display. This is the default value. |
|`hideSaveBtn` |Boolean |Optional |false |Whether to hide the **Save** button of the dashboard in the TLS console.<br><br><br>* true: hidden. Fixed to true in read\-only mode.<br><br>* false: display. This is the default value. |
|`hidePanelMenu` |Boolean |Optional |false |Whether to hide the **action** buttons for statistical charts in the TLS console dashboard.<br><br><br>* true: hidden.<br><br>* false: display. This is the default value. |
|`hidePanelEdit` |Boolean |Optional |false |Whether to hide the **edit** button for the statistical chart in the TLS console dashboard.<br><br><br>* true: hidden. Fixed to true in read\-only mode.<br><br>* false: display. This is the default value. |
|`hidePanelCopy` |Boolean |Optional |false |Whether to hide the **Copy** button for statistical charts in the TLS console dashboard.<br><br><br>* true: hidden. Fixed to true in read\-only mode.<br><br>* false: display. This is the default value. |
|`hidePanelAddAlert` |Boolean |Optional |false |Whether to hide the **Add Alert** button for statistical charts in the TLS console dashboard.<br><br><br>* true: hidden.<br><br>* false: display. This is the default value. |
|`hidePanelDelete` |Boolean |Optional |false |Whether to hide the **Delete** button for statistical charts in the TLS console dashboard.<br><br><br>* true: hidden. Fixed to true in read\-only mode.<br><br>* false: display. This is the default value. |
|`hidePanelFullScreen` |Boolean |Optional |false |Whether to hide the **full\-screen** button for statistical charts in the TLS console dashboard.<br><br><br>* true: hidden.<br><br>* false: display. This is the default value. |
|`hideCharts` |string[] |Optional |hideCharts=["chartId"] |Whether to hide the chart with the specified chart ID. |
|`viewType` |String |Optional |fullScreen |Sets the display status of the dashboard. Optional:<br><br><br>* fullScreen: The dashboard is in full\-screen display.<br><br>* panelFullScreen: The statistical chart is displayed in full screen.<br><br>* panelEdit: The chart is in an edited state.<br><br><br>When setting the relevant state of a statistical chart, specify the `panelId`. |
|`panelId` |String |Optional |`40D9****7637` |Statistical chart ID.<br><br>When setting `viewType`to panelFullScreen and panelEdit, you need to set `panelId`. |


<span id="0adad030"></span>
### Time Field Enumeration Value

The following table describes the values that you can set as the value of the `time` parameter:


|Value |Description |
|---|---|
|now\-1m,now |The past one minute. |
|now\-5m,now |The past five minutes. |
|now\-15m,now |The past 15 minutes. |
|now\-30m,now |The past 30 minutes. |
|now\-1h,now |The past hour. |
|now\-3h,now |The past three hours. |
|now\-6h,now |The past six hours. |
|now\-1d,now |The past day. |
|now\-3d,now |The past three days. |
|now\-7d,now |The past seven days. |
|now\-30d,now |The past 30 days. |
|now\-90d,now |The past 90 days. |
|now/d,now/d |The current day. |
|now/w,now/w |This week. |
|now/M,now/M |This month. |


<span id="ab4699b8"></span>
## Advanced parameter

TLS supports obtaining postmessages for query analysis pages and dashboard pages in the following ways to achieve a more advanced embedded interaction effect.

<span id="91437a4b"></span>
### Query and analysis page

You can obtain the `topicId`, `query`, `searchQuery`, `gastTime`, `endTime`, `time`, `sort`, `isAccurateQuery`, `isParseQuery` and other parameters in the postmessage of the query and analysis page by the following methods, so as to realize one\-click copying of the query related log topics, query and analysis statements, query time and other information on the embedded page.


* Passively listens for `message`events and obtains data through callbacks.

   The complete example is as follows:

   ```HTML
   <!DOCTYPE html><html lang="en"><head>
       <meta charset="UTF-8">
       <meta http-equiv="X-UA-Compatible" content="IE=edge">
       <meta name="viewport" content="width=device-width, initial-scale=1.0">
       <title>Document</title>
     </head>
     <body>
       <iframe id="iframe" style="width: 100%; height: 100vh" src="***" frameborder="0"></iframe>
       <script>
         window.addEventListener('message', function(event) {
             const resp = event.data;
             if (resp.sender === 'TLS/Event/EmbedSearch/searchContextInfo') {
                 console.log(resp.data);
             }
       });
       </script>
     </body></html>
   ```
   

   The `event.data` data formats are as follows:

   ```JavaScript
   {
     sender: 'TLS/Event/EmbedSearch/searchContextInfo',
     // Corresponding to business name, message type (event, response), module name, and message name respectively.
     id: uuid(),
     data: {
         topicId: "xxxxx-xxx", // The Topic ID of the current query.
         
         query: "xxx | select xxx", // The complete query and analysis statement.
         searchQuery: "xxx", // The query statement.
         
         startTime: 17000033, // The start time of this query, it is a absolute time.
         endTime: 17000044, // The end time of this query, it is a absolute time.
         time: "now-5m,now", // The time interval used for this query.
         
         sort: 'asc', // Query sorting.
         
         isAccurateQuery: false, // Whether it is an exact query.
         isParseQuery: false // Whether it is a phrase query.
     }
   }
   ```
   

* Actively send a message to get data through the [postmsg-rpc ](https://www.npmjs.com/package/postmsg-rpc?activeTab=readme)library.

   An example of using react code is as follows:

   ```JavaScript
   import { caller } from 'postmsg-rpc'
   
   function App() {
     return (
       <div className="App">
         <button onClick={async () => {
           const getSearchContextData = caller('TLS/EmbedSearch/getLastSearchContext', {
             postMessage: (data, targetOrigin) => {
               document.querySelector('iframe').contentWindow.postMessage(data, targetOrigin);
             },
           })
           const searchContextData = await getSearchContextData()
           console.log(searchContextData);
         }}>
           Actively send messages to obtain.
         </button>
         <iframe id="iframe" style={{ width: '100%', height: '100vh' }} src="***"></iframe>
       </div>
     );
   }
   
   export default App;
   ```
   

   The data format of `searchContextData`is as follows:

   ```JavaScript
   data: {
     topicId: "xxxxx-xxx", // The Topic ID of the current query.
     query: "xxx | select xxx", // The complete query and analysis statement.
     searchQuery: "xxx", // The query statement.
     startTime: 17000033, // The start time of this query, it is a absolute time.
     endTime: 17000044, // The end time of this query, it is a absolute time.
     time: "now-5m,now", // The time interval used for this query.
     sort: 'asc', // Query sorting.
     isAccurateQuery: false, // Whether it is an exact query.
     isParseQuery: false // Whether it is a phrase query.
   }
   ```
   


<span id="4c1a395f"></span>
### Dashboard page

You can get the dashboardHeight parameter in the postmessage of the dashboard page as follows, which can be used to specify the height of the iframe inline frame on the inline page.

You can obtain data by passively listening to the message event. The code example is as follows:

```HTML
<!DOCTYPE html><html lang="en"><head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
  </head>
  <body>
    <iframe id="iframe" style="width: 100%; height: 100vh" src="***" frameborder="0"></iframe>
    <script>
      window.addEventListener('message', function(event) {
          const resp = event.data;
          if (resp.sender === 'TLS/Event/EmbedDashboard/dashBoardHeightChange') {
              console.log(resp.data.dashboardHeight);
          }
    });
    </script>
  </body></html>
```


The event.data data formats are as follows:

```JavaScript
{
  sender: 'TLS/Event/EmbedDashboard/dashBoardHeightChange',
  // Unique ID.
  id: uuid(),
  data: {
      dashboardHeight: 300
  },
  // Be compatible with the existing logic.
  dashboardHeight: 300
}
```


<span id=".56S65L6L"></span>
## Example

The following sample URL is used to embed a query page from the TLS console into an external system. The topic bar and the left\-side navigation pane of the current page are displayed, the data collected from the specified topic is displayed by default, the default query statement is set, then specify the query time range to the past hour.

According to the parameters configured in the URL, the left\-side navigation pane, the page title bar, the **Topic** checkbox, the **Share** button, and the **Index configuration** button are hidden from the page.

```xml
https://console.byteplus-embed.com/tls/region:tls+ap-southeast-1/project/e783ddd1-f07e-404f-b167-915d04d6****/search?topicId=999ecfa1-9eed-4cb4-ac2e-e130f656****&time=now-1h,now&codebase64=KiB8IHNlbGVjdCAq&hideTitle=true&hideTopic=true&hideIndexBtn=true&hideLeftBar=true&hideShareBtn=true
```


The page displayed is as follows:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5b15514a450e460aa59ac1fc1f0b9254~tplv-goo7wpa0wc-image.image) </span>
