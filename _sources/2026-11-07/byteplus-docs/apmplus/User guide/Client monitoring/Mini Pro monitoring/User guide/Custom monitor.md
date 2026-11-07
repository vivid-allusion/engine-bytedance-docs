---
title: "Custom monitor"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/custom_monitor_minipro"
---

The custom monitor feature enables the frontend to report data using event tracking, and allows users to obtain an overview of the corresponding tracked events in the management background. By tracking events, you can obtain the visit counts for key paths, the opening times for key pages, customize the data you want to observe, and monitor these metrics in the management backend. Additionally, you can specify which data should trigger alerts by configuring the reporting fields of the custom monitor.

<span id=".6Ieq5a6a5LmJ5LqL5Lu2"></span>
## custom event

When you need to collect statistics for a specific event metric across the entire platform, custom event can meet your needs. For example: the total number of clicks for a button.

<span id=".5LiK5oql5pa55byP"></span>
### Reporting method

Reporting example is as follows

```javascript
interface CustomEventPayload {
  /** Custom event name */
  name: string
  /** metrics report measurable values, that is, numerical values */
  metrics?: { [key: string]: number }
  /** categories reports classification and dimension, which are used for filter and grouping */
  categories?: { [key: string]: string }
}
client.sendEvent(data:CustomEventPayload) =>  void // Type
// Call
client.sendEvent({
  name:  "name_test",
  metrics: {
    count:  1,
    },
  categories: {
    user:  "user_x",
    pathname:  "xxxxx",
    },
})
```


For specific parameters, please refer to [API Reference](https://docs.byteplus.com/en/docs/apmplus/Call_an_API_using_the_SDK).

<span id=".55WM6Z2i6K-05piO"></span>
### The interface description


* On the list page, there is a test_sendEvent event reported in the example, and you can see the trends in user volume and report volume.

* For more trend\-related features (for example, view current data points grouped by a dimension), please click **data analytic**.

* For more information about single points (for example, to view all reporting information for this event during a specific time period), please click **data explore**.


<span id=".5LqL5Lu26K-m5oOF"></span>
### Event details

In the event list, click the event name to navigate to the corresponding custom monitor details page.


* The event report trend chart allows you to view fine\-grained trends in the current event report volume and user count.

* On the Metric page of the field list, you can view the specific values reported for each metric.

* On the Category page of the field list, you can view reporting information for each category, the top 20 categories, the sample size, and the corresponding proportion. For example, the following figure shows the number and proportion of reports where the value of the user field is test_user.


<span id=".6Ieq5a6a5LmJ5pel5b-X"></span>
## custom log

When you only want to record logs in a single session without associating them with other sessions, custom log can meet your needs. For example, track the user behavior path within a single session, and attach some log context each time an event is logged. This log context can be a String or JSON.

<span id=".5LiK5oql5pa55byP"></span>
### Reporting methods

An example of reporting is as follows:

```typescript
export interface CustomLogPayload  {
  /** Additional supplementary information. When reporting, 'number' will be routed to metric, and 'string' will be routed to categories. */
    extra?: { [key:  string]:  string  |  number  }  //    /** Custom event content, which can be a log or the JSON representation of an object. */
  content:  string
  /** Custom event level. The default is info. Available options: debug, info, warn, error. */
    level?:  'debug'  |  'info'  |  'warn'  |  'error'
}

client.sendLog(data:  CustomLogPayload) =>  void // Type
// Call
client.sendLog({
  level:  'debug',
  content:  'function `test` was invoked',
  extra: {
    num:  1,
    country:  'SomeCountry'
    }

})
```


For detailed parameter information, please refer to [API Reference](https://docs.byteplus.com/en/docs/apmplus/Call_an_API_using_the_SDK).

<span id=".55WM6Z2i6K-05piO"></span>
### Interface description

Currently, Custom Log does not have a separate page. All previous features can be viewed in the `Custom Log` section of **data explore**. For details, refer to [data explore](https://docs.byteplus.com/en/docs/apmplus/data_explore_minipro).

The list page displays each reported data entry, allowing you to view the following:


* Reporting trends

* Different log levels

* Log content

* Filter based on current information


For more detailed information, you can click each log to view its details.


* Detailed dimension information, such as browser, release version, country, and more

* Supports navigating to the single sign\-on information for the current user or the current session


<span id="Q&A"></span>
## FAQ

How to manually add custom metrics in data analytic, and how to add them to a custom dashboard


1. Click **data analytic** to enter the page for creating a new chart.

2. When plotting a chart, in the metrics section, find the event name or custom log, and select the corresponding metric and grouping.

   For example, in the figure above, first select the test_sendEvent event, then select the count metric, and group by user.

3. Click **Save**.
