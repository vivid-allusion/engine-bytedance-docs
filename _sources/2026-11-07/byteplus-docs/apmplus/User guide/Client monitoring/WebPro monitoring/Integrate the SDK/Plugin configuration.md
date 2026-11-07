---
title: "Plugin configuration"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Plugin_configuration"
---

Plugin configuration is a built\-in feature of Application Performance Management Plus. You can configure whether to turn on or turn off these plugins on the SDK side. Plugin configuration is a one\-off configuration; changes made after initialization will not take effect.

<span id=".5YWz6Zet5o-S5Lu2"></span>
## Turn off plugin

The SDK supports turning off any plugin. If you want to turn off a plugin, set the corresponding pluginName configuration to false.

```TypeScript
import browserClient  from '@apmplus/web'

browserClient('init', {
  ...
  plugins: {
    [pluginName]: false // The specific pluginName can be viewed in the configuration examples for each plugin.
  },
  ...
})


// Example: turn off the performance plugin
browserClient('init', {
  ...
  plugins: {
    performance: false // For specific pluginName, view the configuration examples for each plugin
  },
  ...
})
```


<span id=".6YWN572u5o-S5Lu2"></span>
## Plugin configuration

Except for blank screen monitoring, all plugins have default configurations and do not require additional configuration by default. Details of the default parameters can be found in the description below. If there are any differences from the default configuration, you can configure them separately.

<span id="3738244d"></span>
### PV plugin

<span id="cebd6ada"></span>
#### Configurable fields description


|**Field** |**Type** |**Default value** |**DescriptionS** |
|---|---|---|---|
|sendInit |boolean |TRUE |Send PV on first page load? If PV is sent manually by the business, it can be set to false. |
|routeMode |string |history |Select the mode for automatic monitoring of routing. Manually specify the routing mode for the current site.<br><br><br>* Monitor path changes<br><br>* Hash: Monitoring hash changes<br><br>* manual: Does not automatically monitor route changes |
|extractPid |(url: string) =\> string |\- |Manually specify the rule for generating the pid and pass in the current page address. The return value serves as the PID.<br><br>By default, pid is automatically obtained from the pathname or hash of the current page URL. If the automatically generated pids are too dispersed, making data analysis difficult, you can configure this function to achieve manual aggregation. |


<span id="f5f5747c"></span>
#### Configuration example

```TypeScript
import browserClient  from '@apmplus/web'

browserClient('init', {
  ...
  plugins: {
    pageview: {
      routeMode: 'hash',
      extractPid: (url) => {
        return new URL(url).pathname
      }
    }
  },
  ...
})
```


<span id="PageView"></span>
### JavaScript error plugin

<span id="2dd5dd22"></span>
#### Configurable field descriptions


|**Field** |**Type** |**Default value** |**DescriptionS** |
|---|---|---|---|
|ignoreErrors |（string \| RegExp）[] |[] |Match error message and ignore any JavaScript errors that match the error message. |
|onerror |boolean |true |Whether to enable global onerror listener.<br><br>If your business involves a third\-party component or SDK, you can set this option to false to disable the global onerror listener. In this case, you need to use captureException to manually report JavaScript errors. |
|onunhandledrejection |boolean |true |Whether to turn on the global onunhandledrejection listener.<br><br>If the business itself is a third\-party component or SDK, you can set it to false, which means the global onunhandlerejection listener is not enabled. In this case, you need to use captureException to manually report JavaScript errors. |
|captureGlobalAsync |boolean |false |Hook all global asynchronous APIs.<br><br>Errors within exception APIs, such as setTimeout, often lack a complete stack trace when thrown globally due to inherent limitations. If this field is set to true, additional information can be obtained, for example, identifying which API the error was thrown from. |
|dedupe |boolean |true |The currently occurring JavaScript error will be compared with the previous error. If it is the same error, should it no longer be reported?<br><br>To prevent looped reporting, deduplication is turned on by default. If the business scenario wants the same error to be reported multiple times, you need to set this field to false. |


<span id="dbeea0c5"></span>
#### Configuration example

```TypeScript
import browserClient  from '@apmplus/web'

browserClient('init', {
  ...
  plugins: {
    jsError: {
      ignoreErrors: ['Failed to fetch']
    }
  },
  ...
})
```


<span id="e8a6f4ba"></span>
### Breadcrumbs plugin

The breadcrumbs plugin is not a standalone feature plugin, but rather an auxiliary plugin to the JavaScript error plugin. This plugin provides additional user\-related behavioral context for JavaScript errors.

<span id="1e050271"></span>
#### Configurable fields description


|**Field** |**Type** |**Default value** |**DescriptionS** |
|---|---|---|---|
|maxBreadcrumbs |number |20 |What is the maximum number of breadcrumbs that can be stored in memory?<br><br>If your business scenario requires visibility into user actions that occurred even earlier before a JavaScript error, you can set maxBreadcrumbs to a higher value. |
|dom |boolean |true |Whether to listen for click and keypress events.<br><br>Currently, the SDK only collects xpath data. If your business still has security concerns regarding user privacy, you can set the dom configuration to false, which will prevent the collection of user behavior. |
|onAddBreadcrumb |(b: Breadcrumb) =\> Breadcrumb |\- |Add a breadcrumbs hook function.<br><br>Commonly used in partial masking scenarios or to provide additional context. |
|onMaxBreadcrumb |(bs: Breadcrumb[], maxBreadcrumbs: number) =\> Breadcrumb[] |\- |Hook function for when the breadcrumbs queue reaches the length limit.<br><br>Commonly used for one\-off processing of breadcrumbs in a queue. |


<span id="a3639a80"></span>
#### Type description

```TypeScript
interface Breadcrumb {
  /** dom | http ｜ any string */
  type: string;
  /** xpath, keyvalue | url */
  message: string;
  /** ui.click, ui.keypress | post,get */
  category: string;
  /** status: 400 for http */
  data?: { [key: string]: string };
}
```


<span id="b39aa277"></span>
#### Configuration example

```TypeScript
import browserClient  from '@apmplus/web'

browserClient('init', {
  ...
  plugins: {
    breadcrumb: {
      dom: false,
      maxBreadcrumbs: 50,
      onAddBreadcrumb: (b) => {
        return {
          ...b,
          data: null // Set sensitive data to null
        }
      }
    }
  },
  ...
})
```


<span id="45cf4e0e"></span>
### Static resources performance plugin

<span id="55faa72d"></span>
#### Configurable field descriptions


|**Field** |**Type** |**Default value** |**DescriptionS** |
|---|---|---|---|
|ignoreUrls |(string \| RegExp)[] |[] |Specify resource paths to ignore. If a match is found, the corresponding resource performance data will not be reported. |
|slowSessionThreshold |number |4000 |Slow session threshold, unit: ms.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">If a session does not finish loading within the threshold time, then all static resources performance data for the current session will be reported, even if a sampling rate configuration is set, to facilitate better troubleshooting of pageload performance exceptions.</div><br><br><br><div data-tips="true" data-tips-type="warning">If this mechanism is not required, you can set the parameter to Number.MAX_SAFE_INTEGER.</div><br> |
|ignoreTypes |string[] |['xmlhttprequest', 'fetch', 'beacon'] |Specify the resource types to be ignored; the corresponding matching field is PerformanceResourceTiming.initiatorType. For details, refer to [PerformanceResourceTiming.initiatorType](https://developer.mozilla.org/en-US/docs/Web/API/PerformanceResourceTiming/initiatorType). |


<span id="82e6e3ae"></span>
#### Configuration example

```JavaScript
import browserClient  from '@apmplus/web'

browserClient('init', {
  ...
  plugins: {
    resource: {
      ignoreTypes: ['css'],
    }
  },
  ...
})
```


<span id="4ac1ce8a"></span>
### Static resource error plugin

<span id="ee540882"></span>
#### Configurable field description


|**Field** |**Type** |**Default value** |**DescriptionS** |
|---|---|---|---|
|ignoreUrls |(string \| RegExp)[] |[] |Specify resource paths to ignore. If a match is found, the corresponding static resource error will not be reported. |
|includeUrls |(string \| RegExp)[] |[] |Specify the matched resource path. If no match is found, the corresponding static resource error will not be reported. Priority is higher than `ignoreUrls`. |
|dedupe |boolean |true |The current resource error is compared with the previous resource error. If they are the same error, should it no longer be reported?<br><br>To prevent cyclic reporting, deduplication is turned on by default. If the business scenario requires the same resource error to be reported multiple times, you need to set this field to false. |


<span id="ae18f757"></span>
#### Configuration example

```JavaScript
import browserClient  from '@apmplus/web'

browserClient('init', {
  ...
  plugins: {
    resourceError: {
      dedupe: false,
    }
  },
  ...
})
```


<span id="d5f02ef7"></span>
### XHR monitoring plugin

<span id="9f884192"></span>
#### Configurable field descriptions


|**Field** |**Type** |**Default value** |**DescriptionS** |
|---|---|---|---|
|autoWrap |boolean |true |Whether to automatically wrap the global xhr.<br><br>If your business does not use the global xhr, but instead uses your own wrapped xhr, you must set this field to false and manually wrap xhr by calling the wrapXhr method. |
|ignoreUrls |(string \| RegExp)[] |[] |Specified request paths to ignore; if a request matches one of these paths, the corresponding request data will not be reported. |
|collectBodyOnError |boolean |false |Whether to collect the request body and response body on error.<br><br>By default, the SDK does not collect the request body or the response body. If your business requires collecting these data when an error occurs to facilitate better troubleshooting, you need to set this field to true.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Overseas business may involve security risks. It is not recommended to turn on this field.</div><br> |
|trace |{ sampleRate?: number, origins: (string \|RegExp)[] } \| boolean |false |Configure connectivity between the frontend and backend. If the request path matches the configured origins, the traceparent and baggage headers will be added to the request headers. This facilitates server\-side monitoring and correlation of the entire trace, helps diagnose the causes of long request times, and helps pinpoint performance bottlenecks. For details, refer to [Full trace scenario integration](https://docs.byteplus.com/en/docs/apmplus/Integrate_full_trace_scenarios). |
|extractUrl |(*originalUrl*: string) =\> string |\- |Define a custom rule for generating the request path: the original path is provided as input, and the return value is used as the new request path.<br><br>Often used to aggregate RESTFUL request paths. |


<span id="51f56a07"></span>
#### Configuration example

```JavaScript
import browserClient  from '@apmplus/web'

browserClient('init', {
  ...
  plugins: {
    ajax: {
      autoWrap: false,
      collectBodyOnError: true,
    }
  },
  ...
})
```


<span id="2a5d7e9f"></span>
### Fetch monitoring plugins

<span id="fd545c72"></span>
#### Description of configurable fields


|**Field** |**Type** |**Default value** |**DescriptionS** |
|---|---|---|---|
|autoWrap |boolean |true |Should the global fetch be wrapped automatically?<br><br>If your application does not use the global fetch and instead uses a custom\-wrapped fetch, you need to set this field to false and call the wrapFetch method to manually wrap fetch. |
|ignoreUrls |(string \|<br><br>RegExp)[] |[] |Specify the request paths to be ignored. If a request matches one of these paths, the corresponding request data will not be reported.<br><br>If you need to manually ignore certain request paths, you can configure this field. |
|collectBodyOnError |boolean |false |Whether to collect the request body on error.<br><br>By default, the SDK does not collect the request body or response body. If your business requires the collection of these data during an error to facilitate better troubleshooting, you need to set this field to true.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Overseas business may have security risks. It is not recommended to turn on this field.</div><br> |
|trace |{ sampleRate?: number, origins: (string \|RegExp)[] } \| boolean |false |Configure front\-end and back\-end integration. If the request path matches the configured origins, the traceparent and baggage headers will be added to the request header to facilitate server\-side monitoring and linking the entire trace.<br><br>Commonly used in scenarios where an end\-to\-end trace between the front\-end and back\-end is established, it can help troubleshoot the causes of long request times and accurately pinpoint request performance bottlenecks. For details, refer to [Full trace scenario integration](https://docs.byteplus.com/en/docs/apmplus/Integrate_full_trace_scenarios). |
|extractUrl<br><br>(version \>= 2.5.0 \*\*\*\* ) |(*originalUrl*: string) =\> string |\- |Define a custom rule for generating the request path. The original path is provided as input, and the return value is used as the new request path.<br><br>Commonly used to aggregate RESTFUL request paths. |


<span id="0eda6947"></span>
#### Configuration example

```JavaScript
import browserClient  from '@apmplus/web'

browserClient('init', {
  ...
  plugins: {
    fetch: {
      autoWrap: false,
      collectBodyOnError: true,
    }
  },
  ...
})
```


<span id="866b5f42"></span>
### Performance monitoring\-related plugins

The performance monitor plugin is not a single plugin, but is composed of multiple plugins. Its configuration is relatively simple and mainly provides switches for various performance metrics. The typical usage scenario is that after turning off a metric, you manually report this performance metric using the sendCustomPerfMetric method provided by the SDK.

<span id="e5f28efd"></span>
#### Performance configurable fields description


|**Field** |**Type** |**Default value** |**DescriptionS** |
|---|---|---|---|
|fp |boolean |true |The fp metric switch is commonly used when the corresponding metric is not reported. |
|fcp |boolean |true |FCP metric switch, commonly used to disable reporting of the corresponding metric. |
|lcp |boolean |true |LCP metric switch, commonly used to not report the corresponding metric. |
|cls |boolean |true |CLS metric switch, commonly used to disable reporting of the corresponding metric. |
|inp |boolean |true |inp metric switch, commonly used to disable reporting of the corresponding metric. |
|longtask |boolean |true |The longtask metric switch is commonly used to disable reporting of the corresponding metric. |
|timing |boolean |true |Timing metric switch, commonly used to disable reporting of the corresponding metric. |


<span id="931ed61c"></span>
#### Performance configuration examples

```JavaScript
import browserClient  from '@apmplus/web'

browserClient('init', {
  ...
  plugins: {
    performance: {
      fp: false,
    }
  },
  ...
})
```


<span id="11625cc0"></span>
#### Description of FMP configurable fields


|**Field** |**Type** |**Default value** |**DescriptionS** |
|---|---|---|---|
|renderType |string |CSR |Specify the rendering type of the current page.<br><br><br>* CSR: Calculate FMP using the default algorithm.<br><br>* SSR does not calculate FMP using the default algorithm; instead, it uses FCP as a substitute for FMP. |


<span id="9a6cdd1c"></span>
#### FMP configuration example

```JavaScript
import browserClient  from '@apmplus/web'

browserClient('init', {
  ...
  plugins: {
    fmp: {
      renderType: 'SSR',
    }
  },
  ...
})
```


<span id="96b08e51"></span>
#### TTI plugins

Because the TTI algorithm depends on requests and starts early, it is implemented as a separate plugin. No parameters are exposed, but you can disable this metric by setting its configuration to false.

```JavaScript
import browserClient  from '@apmplus/web'

browserClient('init', {
  ...
  plugins: {
    tti: false
  },
  ...
})
```


<span id="24457f75"></span>
### Blank screen plugin

The blank screen plugin is not turned on by default; you need to configure it manually to turn it on. The screenshot capability included in the plugin is based on further development of html2canvas, with an additional toggle to hide specific text information.

<span id="b3213c8c"></span>
#### Configurable field descriptions


|**Field** |**Type** |**Default values** |**DescriptionS** |
|---|---|---|---|
|rootSelector |string |body |The root node for DOM scoring supports querySelector syntax.<br><br>Only by manually configuring rootSelector as the root node for scoring will accuracy be higher. If you only want to monitor whether a specific area has a blank screen, you can also configure the monitoring for the designated area node. |
|autoDetect |boolean |true |Whether to automatically turn on blank screen monitoring.<br><br>If you do not want to turn on automatic monitoring, you can set this field to false. Then, call the detectBlankScreen method provided by the SDK to manually check for blank screens. |
|threshold |number |1.5 |DOM scoring threshold. If the calculated score is less than the threshold, it may be a blank screen. |
|screenshot |boolean |true |Whether to automatically report the screenshot picture of the current page.<br><br>Taking screenshots involves security and privacy to some extent, but it can help determine whether the current page is actually a blank screen.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If the height and width are 0 or exceed the maximum canvas size, the screenshot picture base64 will back <code>"data:,"</code>.</div><br><br><br><div data-tips="true" data-tips-type="tip">For more information about maximum canvas size, refer to <a href="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/canvas#maximum_canvas_size">Maximum canvas size</a>.</div><br> |
|mask |boolean |false |Apply data masking to the content of the following nodes:<br><br><br>* Text<br><br>* input<br><br>* Svg<br><br>* Img<br><br>* canvas<br><br><br>This field can be configured only in @apmplus/web version 2.0.0 or later.<br><br>If the page contains private data, you can enable this field. The result is shown in the figure below.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/02707deb70114ebca5d0d780bd04f566~tplv-goo7wpa0wc-image.image) </span> |
|partialShot |boolean |false |Partial node screenshots Configuration of this field is only supported in @apmplus/web version 2.0.0 or above.<br><br>By default, during a blank screen, the screenshot is taken of document.body. After you start this field, only the specified rootSelector is captured. |
|quality |number |0.1 |Screenshot picture clarity (value range: 0 to 1). Configuration of this field is supported only in @apmplus/web \>= 2.0.0.<br><br>If you want to obtain clearer screenshot information, you can increase the value of this field.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Because the base64 encoding of a 1:1 screenshot after transcoding is too large, the original page has already been scaled down by default. Scaling formula: 360 / window.innerWidth.</div><br><br><br>For more information about the clarity of screenshots, refer to [Syntax](https://developer.mozilla.org/en-US/docs/Web/API/HTMLCanvasElement/toDataURL). |


<span id="e562ba87"></span>
#### Configuration example

```JavaScript
import browserClient  from '@apmplus/web'

browserClient('init', {
  ...
  plugins: {
    blankScreen: {
      rootSelector: '#app',
    }
  },
  ...
})
```
