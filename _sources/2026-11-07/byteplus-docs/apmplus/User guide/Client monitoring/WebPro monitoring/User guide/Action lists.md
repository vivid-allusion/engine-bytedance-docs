---
title: "Action lists"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Action_lists"
---

The Action list (user behavior list) is a dashboard used for monitoring user behavior and measuring user behavior performance.

<span id=".5o6l5YWl"></span>
## Integration

Because the Action list feature is not required by all users, it is not integrated into the SDK by default. You can configure its integration according to your business needs.

Configure actionPlugin during initialization, and you will be able to monitor user behavior.

Version dependencies: apmplus/integrations \>= 1.1.0 and apmplus/web \>= 2.0.0

<span id=".5o-S5Lu26YWN572u6K-05piO"></span>
### Plugin configuration descriptions


|**Field** |**Type** |**Default value** |**DescriptionS** |
|---|---|---|---|
|types |string[] \| false |\- |Configuration listener types<br><br>By default, the SDK listens for multiple user behaviors, but users can specify which types to listen for through the types parameter. For example:<br><br><br>* click: Only listens for the click event.<br><br>* false: Does not listen to any event. However, you can call the SDK's startAction method to manually record user actions. |
|pure |boolean |false |Only view action data associated with longtask, http, js_error, and resource_error.<br><br>If you want to monitor button click behavior only and do not want to only view the associated action data mentioned above, you can set this field to true. In this case, the action does not need to be associated with performance data; once the action has stabilized, the data will be reported directly. |


<span id=".5o6l5YWl56S65L6L"></span>
### Integration examples

```TypeScript
import client from '@apmplus/web'
import { actionPlugin } from '@apmplus/integrations'

// Example 1: Integrate the action plugin
client('init',{
  ...
  integrations: [actionPlugin()],
  ...
})

// Example 2: Integrate the action plugin but does not listen to any event
client('init',{
  ...
  integrations: [actionPlugin({ types: false })],
  ...
})

// Example 3: Integrate the action plugin and listen for specified event types
client('init',{
  ...
  integrations: [actionPlugin({ types: ['click'] })],
  ...
})
```


In addition to the default monitoring items, you can also manually start a user action by calling the startAction method.

```TypeScript
client("startAction", "action name", "action type");
```


<span id=".6Ieq5a6a5LmJYWN0aW9uIG5hbWU="></span>
### The custom action name

By default, the SDK will obtain the text information of the currently clicked element to use as the action name. Additionally, the SDK supports custom action names. You can configure the value of the data\-apm\-action attribute on an element to serve as the action name.

Example:

```TypeScript
// In this example, clicking the span inside will set "this is action name" as the name of the element for this instance.
<Button data-apm-action="this is action name" onClick={...}>
    <span>trigger action</span>
</Button>
```


If the target browser is Internet Explorer and does not support Element.closest, the SDK will traverse up to 10 levels of parent elements to find an element with an attribute containing data\-apm\-action. For more information about Element.closest, refer to [Element.closest](https://developer.mozilla.org/en-US/docs/Web/API/Element/closest).

<span id=".6aG16Z2i5raI6LS5"></span>
## Page usage

User behavior refers to the actions users take on the product, which are reflected as relevant user data. You can view and analyze them from two aspects:


* Reproduce user paths

   When an exception occurs, you can help locate the issue by viewing the session in Data Explore to reproduce the user path.

* Behavior performance

   View associations based on monitoring data such as JavaScript error, static resource error, request, LongTask, and more; analyze issues according to different sorting criteria to optimize the interaction experience. You can view the monitoring data in the Action list.


<span id=".562b6YCJ"></span>
### filter


* The toolbar includes time range selection, time granularity selection, sorting criteria, statistical method for the time metric, and filter conditions.

* Supports saving filter criteria as favorites and viewing commonly used filters.

* Sorting criteria include: Actions time, request time, frontend Time, LongTask time, number of Action triggers, total JavaScript error count, average request count, and LongTask count.

   * Actions total time: Sort by response total time in descending order to identify which user behavior pages have slower responses

   * Action trigger count: By sorting by Action trigger count in descending order, you can view which actions are most commonly used by users.

   * LongTask count: Sort by LongTask count in descending order to view which actions cause more user lag

* The time consumption metrics include avg, pct50, pct75, pct90, and pct95.


<span id=".QWN0aW9u6K-m5oOF"></span>
### Action details


* The left side of the page displays a list sorted by the specified criteria, including Action name, pid, sorting metric name, and metric value.

* The metrics displayed within the module include the average number of triggered requests, the total JavaScript error count, and the LongTask count.

* Click **Jump to data explore** to navigate to the Actions section of data explore with the filter conditions applied, then view the waterfall chart for further analysis.

* The trend chart can toggle between displaying **response time** and **LongTask time**. The aggregated stacked chart clearly reflects the overall time spent.

   * Request time: The time Action spends on the request. Request time takes up a large proportion of the total processing time. Optimizing request time can improve user experience.

   * Frontend time: Actions time \- request time.

   * LongTask duration: The total sum of LongTask durations that occur during the process from the start to the settlement of an Action. LongTask is time\-consuming. You can optimize your code to reduce the number or duration of LongTasks and improve user experience.


<span id=".QWN0aW9u6Kem5Y-R5pWw"></span>
### Action trigger count

Combining the number of Action triggers with long\-duration LongTasks can effectively help identify the causes of lag.

<span id=".SlPplJnor6_liJfooag="></span>
### JavaScript error list


* The JavaScript error list displays data for all JavaScript errors associated with the current Action, helping to identify which specific JavaScript errors are causing user interactions to become unavailable.

* The JavaScript error list includes error content, start and end time, error count, impacted user count, and issue status.

* Click the error content to navigate to the corresponding JavaScript error details page.


<span id=".6K-35rGC5YiX6KGo"></span>
### request list


* The request list displays the data of all requests associated with the current Action to pinpoint which specific requests have affected the user experience.

* The request list includes: request path and request time.

* Clicking the request path can navigate you to the request list, carrying the request path and request domain name as parameters.
