---
title: "Custom monitor"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/custom_monitor"
---

Custom monitor allows the frontend to report data through event tracking, and you can view overview information for the corresponding events in the management backend.

By tracking events, you can view the number of visits to key paths, the time key pages are opened, and other metrics that can be customized according to your business needs, all within the admin console. Using the custom monitor, you can configure the data to be alerted on and perform custom monitoring of the frontend runtime environment.

<span id="HRk70YWY"></span>
# **Custom event:** 

Reporting method

Report example code:

```TypeScript
// If you are using the npm method to import
import browserClient  from '@apmplus/web'

// If this is a regular counting event
browserClient('sendEvent', {
    name: 'basic-custom',
    categories: {
      fruit: 'banana',
    },
});

// For custom metric logging, the distinction from count metric logging is that count metric logging sets the default value of the metric to 1, whereas in custom metric logging, the value of the metric can be set arbitrarily.
const val = ~~(Math.random() * 200);
browserClient('sendEvent', {
    name: 'custom-metrics',
    metrics: {
      custom_metric: val,
    },
    categories: {
      fruit: val > 100 ? 'banana' : 'apple',
    },
});

// If you use the CDN method to import
window.apmPlus('sendEvent', {// The above configuration }
```


For specific parameter details, please refer to the CustomPayload field in [Custom reporting fields](https://docs.byteplus.com/en/docs/apmplus/Reporting_formats).

<span id=".5bmz5Y-w5raI6LS5"></span>
## Event list


* The list includes the `custom-metrics` event reported in the example, where you can observe the trends in user volume and report volume.

* **data analytic**: Click to view more trend\-related content, for example, you may want to group the current data points by a specific dimension, or modify the metric configuration in the chart.

   Find the custom metric in the metrics on the left, then select the corresponding event name. For example, select the metric custom_metric from the custom event custom\-metrics, and then group by the fruit reported in category.

* **data explore**: Click to view more single\-point related information. For example, you can view all reporting information for the event during a specific time period.

* Event name: Click to navigate to the corresponding event details.

    &nbsp;


<span id=".6Ieq5a6a5LmJ55uR5o6n6K-m5oOF"></span>
## Custom event monitoring details

Custom monitor details display the fine\-grained trends of sample size and user count reported for the current event.


* **Metric**: The specific values reported by each metric can be viewed in the field list.

* **Category**: View reporting information for each category, including the top 20 categories, displaying the sample size and corresponding proportion.

   For example, the figure shows the single dimension "fruit." Clicking fruit displays the report volume ranking for that dimension.


&nbsp;

<span id="FXrH77bF"></span>
# Custom log:

Reporting method

Sample code for reporting:

```TypeScript
// If you are using the npm method to import
import browserClient  from '@apmplus/web'

browserClient('sendLog', {
    content: 'test my info level', // Log content. It is recommended that the content length not exceed 1024. The platform may truncate logs that are too long.
    level: 'info', // Log level. You can select error, warn, info, or any other arbitrary custom error level string.
    extra: {  //Additional content
        name:'test', // Content of string type will be converted into the log's category and used to classify logs during analysis
        count: 10 // Number-type content will be converted into a log metric for analyzing log metrics.
    }
});

// If you import using the CDN method
window.apmPlus('sendLog', {// As configured above})
```


For specific parameters, refer to the CustomPayload field in [Custom reporting fields](https://docs.byteplus.com/en/docs/apmplus/Reporting_formats).

<span id="Xss9sgN5"></span>
## Log list


* The list contains custom logs that have been reported, allowing you to view trends in user volume and report volume.

* **Data analytic**: Click to view more about the corresponding log trends. For example, you can group the current data points by a specific dimension. You can also modify the metric configuration in the chart.

* **data explore**: Click to view more single\-point related information, for example, to view all reporting information for the log during a specific time period.

* **Log name or log details**: Click to navigate to the corresponding log details.

    &nbsp;


<span id="TApvhq9g"></span>
## Custom log details

Custom log details display the sample size for current log reporting and provide fine\-grained trends for user count.


* **Metric**: In the field list, you can view the specific reported values for each metric.

* **Category**: View reporting information for each category and the top 20 categories, displaying the sample size and corresponding proportion.

   For example, the figure displays the single dimension "name". Clicking "name" shows the ranking by report volume for this dimension.
