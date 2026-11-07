---
title: "Integrate full trace scenarios"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Integrate_full_trace_scenarios"
---

The full trace scenario allows you to view complete trace data from the server side to the client, helping you quickly identify issues. This article introduces how to integrate the end\-to\-end trace connectivity scenario monitored by WebPro.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* [@apmplus/web](https://www.npmjs.com/package/@apmplus/web) \>= 1.3.0

* Integrate the server\-side monitoring feature of the latest full\-trace version of application performance monitoring

    &nbsp;


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

The service needs to configure the response header `Access-Control-Allow-Headers` to allow the x\-rum\-traceparent and x\-rum\-tracestate request headers. Configuration example:

`Access-Control-Allow-Headers: x-rum-traceparent, x-rum-tracestate`

After configuration, thorough verification is required; otherwise, the request may fail to be sent due to a cross\-origin error.

<span id=".5o6l5YWl56S65L6L"></span>
## Integration example

```javascript
import client from '@apmplus/web'

client('init', {
 ...
  plugins: {
    ...
    fetch: {
      // If the request is sent using the fetch API, configuration is required on the fetch plugin.
      trace: {
        sample: 1, // trace sampling rate. The sampling rule is session-based, meaning that in a single session, all qualifying requests either have trace turned on or all have trace turned off.
        origins: ['xxx'],  // origins is used for request address matching; only requests that match origins will turn on trace
      }
    },
    ajax: {
      // If the request is sent using the xhr API, configuration is required on the ajax plugin.
      trace: {
        sample: 1, // trace sampling rate. The sampling rule is session sampling, which means that in a single session, all qualifying requests either have trace turned on or all have trace turned off.
        origins: ['xxx'] // origins is used for matching request addresses; only requests that match origins will turn on trace
      }
    }
  },
  ...
})
```



* If the request is sent using the fetch API, the configuration must be set in the fetch plugin; if the request is sent using the xhr API, the configuration must be set in the ajax plugin.

* Enabling trace pass\-through will add request headers, which is considered a side effect. Therefore, trace pass\-through is disabled by default.

* You must configure both sampleRate and origins simultaneously.

   * "sampleRate" represents the trace sampling rate. The sampling rule is session\-based sampling, which means that for all qualifying requests within a single session, trace is either turned on for all of them or turned off for all of them.

   * 'origins' is used for request address matching; trace will be turned on only for requests that match 'origins'.

       &nbsp;


<span id=".5o6l5YWl6aqM6K-B"></span>
## Access verification

If the configuration for @apmplus/web is correct, the corresponding request will include two request headers: X\-Rum\-Traceparent and X\-Rum\-Tracestate. At the same time, the current app_id is included in X\-Rum\-Tracestate.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/020141df3e684dd4ac7c9fd39d41f3f3~tplv-goo7wpa0wc-image.image) </span>

If the request header is not included, please check whether the SDK version is greater than or equal to v1.3.0 or whether the configuration structure is correct.
