---
title: "Configure plugins"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Configure_plugins"
---

The plugin is a built\-in feature of Application Performance Management Plus, and these features can be turned on or off through SDK\-side configuration. Plugin configuration is a one\-off configuration; modifications made after initialization will no longer take effect.

<span id=".5L2_55So6K-05piO"></span>
## Usage instructions

Throughout the document, the **client** refers to the SDK instance.

<span id=".5byA5ZCv5o-S5Lu2"></span>
## Turn on a plugin

By default, all plugins are enabled. The following is an example configuration to turn on the Js Error plugin.

```javascript
client('init', {
  ...
  plugins: {
    js_error: true
  }
  ...
})
```


<span id=".5YWz6Zet5o-S5Lu2"></span>
## Turn off the plugin

Setting the plugin configuration to false means the plugin is turned off. The following is an example configuration to turn off the Js Error plugin.

```javascript
client('init', {
  ...
  plugins: {
    js_error: false
  }
  ...
})
```


<span id=".6YWN572u5o-S5Lu2"></span>
## Configuration plugins

<span id="Pageview"></span>
## Pageview

Reported on page load for collecting statistics on PV, UV, and page time on site.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">To avoid unexpected errors, the custom pid for the PV plugin should not contain special characters. It is recommended to use letters, numbers, slash (/), and hyphen (\-) when naming.</div>


```javascript
pageview: {
    // In routing mode, reporting is disabled when set to manual
    routeMode: 'history' | 'manual' = 'history'
    // Specify how to extract pid from the URL when history changes
    extractPid?: (url: string) => string
}
```


<span id="Js Error"></span>
## Js Error

Report when a Js Error or Navigate Error occurs.

```javascript
jsError: {
    // Ignore errors that correspond to the error message
    ignoreErrors: (string | RegExp)[] = []
    // Listen for App.error
    hookOnError: boolean = true
    // Listen for App.unhandledRejection
    hookOnUnhandledRejection: boolean = true
    // Listen for route errors
    hookRouteError: boolean = true
    // Compare identical errors that occurred before and after, and remove duplicates
    dedupe: boolean = true
}
```


<span id="Breadcrumb"></span>
## Breadcrumb

Collect HTTP and route switching information, and report them together when a JavaScript error is reported.

```javascript
breadcrumb: {
    // Maximum number of breadcrumbs to retain
    maxBreadcrumbs?: number = 20
    // Hook called when adding breadcrumbs
    onAddBreadcrumb?: (b: Breadcrumb) => Breadcrumb | false
    // Hook invoked when breadcrumbs are full
    onMaxBreadcrumbs?: (bs: Breadcrumb[], maxBreadcrumbs: number) => Breadcrumb[]
}
```


<span id="Http"></span>
## Http

Reporting occurs when request, downloadFile, or uploadFile is called.

The trace field is used to configure connectivity between the front end and back end. If the request path matches the configured origins, the request header will include the traceparent and baggage headers to facilitate server\-side monitoring and correlate the entire trace.

```TypeScript
http: {
    // whether to intercept instance.request
    hookRequest: boolean = true
    // whether to intercept instance.downloadFile
    hookDownloadFile: boolean = true
    // whether to intercept instance.uploadFile
    hookUploadFile: boolean = true
    // ignore the urls or RegExps passed in
    ignoreUrls: (string | RegExp)[] = ['/settings/minipro','monitor_browser/collect/batch']
    // whether to gather request.body and response.body when response.statusCode >= 400
    collectBodyOnError: boolean = false
    //  developer can extract extra with response.body and httpPayload.if the value returned wasn't undefined or null, it would be set to extra and is_custom_error would be set to true
    extraExtractor?: (body: string | any, related: HttpPayload) => { [key: string]: string } | false
    // whether to enable trace
    trace?: TraceConfig | boolean
}

/*
    export interface TraceConfig {
// Session-level sampling rate. Can be set to any value between 0 and 1 (inclusive). The default is 1. Indicates the proportion of sessions that add full trace-related request headers.
      sampleRate?: number
// If the request matches the rule, trace-related request headers will be included
      origins: (string | RegExp)[]
    }
*/
```


<span id="setData"></span>
## setData

Reporting occurs when setData is called. By default, the calculation of parameter size is set to false. Because setData is called frequently, enabling the calculation of parameter size may cause minor fluctuations in pageload performance.

```javascript
setData: {
  // Whether to calculate the size of the parameter passed to setData
  isCalculateSize: boolean = false
}
```


<span id="App Launch Perf"></span>
## App Launch Perf

Collect startup performance and report it after startup is complete. No additional parameters.

```javascript
// No configuration required; turned on by default. To turn off, set to false.
appLaunchPerf: {}
```


<span id="Page Perf"></span>
## Page Perf

Pageload performance is collected and reported after switching pages and once the page has fully loaded. No additional parameters are required.

```javascript
// No configuration required; enabled by default. To disable, set to false.
pagePerf: {}
```


<span id="Performance"></span>
## Performance

Collect individual performance metrics, such as FR, FP, FCP, and LCP. Currently, these metrics can only be obtained on certain device models of WeChat and TikTok Mini Program, and there are no additional configuration parameters.

```javascript
// No configuration required; turned on by default. To turn off, set to false.
performance: {}
```
