---
title: "Integrate the mini program SDK"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Integrate_the_mini_program_SDK"
---

This document applies to products and services directly on the  platform. Supported native mini programs include WeChat Mini Program, ByteDance Mini Program, Alipay Mini Program, and Baidu Mini Program, but frameworks such as taro or uniapp are not supported.

<span id=".5L2_55So6ZmQ5Yi2"></span>
## Usage Limits

Currently, the SDK is limited to use by applications in mainland China (excluding the Hong Kong, Macau, and Taiwan regions).

<span id=".5b-r6YCf5o6l5YWl"></span>
## Integrate quickly

<span id="NPM"></span>
### NPM

`npm install` After that, run the "build npm" command.

https://www.npmjs.com/package/@apm\-insight\-web/rangers\-mini\-sdk

```Plain Text
npm install @apm-insight-web/rangers-mini-sdk

```


```Plain Text
// You must call the vemars.init method for initialization in App.js before configuring the App.

const vemars = require('@apm-insight-web/rangers-mini-sdk').default
// Or
import vemars from '@apm-insight-web/rangers-mini-sdk'

vemars.init({ / The init method can only be called once.
  aid: 'app_id', // Required. Enter the aid registered on the platform here.
  userId: 'xxx' // Optional. You can enter the user UUID. If not provided, a random ID will be generated.
})

App({
    onLaunch: function() {
        userLogin().then(userId => {
            vemars.config({ // You can also set the userId after successful login.
                userId: userId
            })
        })
    },
    ...
})

```


<span id="CDN"></span>
### CDN

```Plain Text
// You must call the vemars.init method for initialization in App.js before configuring the App.

// For use in the source file, assuming it is placed in the vendors/rangers - mini - sdk/ directory, reference it through a relative path in app.js.
const vemars = require('./vendors/rangers-mini-sdk/index.0.0.22.cn.js').default
// If your mini - program compilation environment supports ES6 syntax, you can use it.
import vemars from './vendors/rangers-mini-sdk/index.0.0.22.cn.js'

vemars.init({ // The init method can only be called once.
  aid: 'app_id', // Required. Enter the aid registered on the platform here.
  userId: 'xxx' // Optional. You can enter the user UUID. If not provided, a random ID will be generated.
})

App({
    onLaunch: function() {
        userLogin().then(userId => {
            vemars.config({ // You can also set the userId after successful login.
                userId: userId
            })
        })
    },
    ...
})


```


<span id=".6YWN572u5LiK5oql5Z-f5ZCN55m95ZCN5Y2V"></span>
### Configure the allowlist of reporting domain names

Please add your reporting domain to the list of valid request domains in the mini program management backend; otherwise, the reporting request will be blocked.

The built\-in reporting domain for the SDK is currently https://tbm.snssdk.com.

<span id=".6ZuG5oiQRGF0YUZpbmRlcg=="></span>
### Integrate DataFinder

If you have also purchased the DataFinder product and need to enable UserID integration, you can use the following methods:

```Plain Text
import vemars from './vendors/data-finder/rangers'
... // Configure the Finder instance.

vemars.init({ // The init method can only be called once.
  aid: 'app_id', // Required. Enter the aid registered on the platform here.
  finderInstance: $$Ranger // If you pass in the DataFinder instance, the UUID will be obtained from DataFinder, and there is no need to set the userId.
})

App({
    onLaunch: function() {
        userLogin().then(userId => {
            vemars.config({ // You can also set the userId after successful login.
                userId: userId
            })
        })
    },
    ...
})

```


<span id=".6K-m57uG6YWN572u"></span>
### Detailed configurations

In the previous example, only the aid and userId parameters were configured. In addition to these two parameters, there are several other parameters. All supported parameter names and their meanings are as follows:

```Plain Text
export type UserOptions = {
  aid: number
  // Sampling class. Supported since version 0.1.1.
  sampleRate?: number
  // Switch class
  hookPath?: boolean // Whether to monitor page route changes
  hookRequest?: boolean // Whether to monitor network requests
  enableCapture?: boolean // Whether to capture exceptions
  // Context
  context?: Record<string, any>
  // Reporting related
  maxBatchReportLength?: number // Maximum number of aggregated items, default is 10
  batchReportWait?: number // Aggregation waiting time, default is 1000, unit: ms
  // User related
  userId?: string
  sessionId?: string
  reportDomain?: string // Private reporting domain name
  reportPath?: string // Private reporting path
  pid?: string // Page identifier
  maxBreadcrumbs?: number // Maximum breadcrumb length
  // finder
  finderInstance?: FinderInstance
}

```


<span id=".6aqM6K-B5LiK5oql"></span>
### Report verification

After calling `init`, the SDK will call `getSystemInfo` and `getNetworkType` to collect some environment information, and report a PV event when `Page.onShow` is triggered on the home page. You can see the `/monitor_microapp/collect` request in the debugger console.

<span>![图片](https://lf3-volc-editor.volccdn.com/obj/tos-cn-v-697126/04447ef9422341228a7ce3505ca8e20c) </span>

<span id=".5Yqf6IO95LuL57uN"></span>
## Introduction to features


* Error collection: The SDK monitors the `App.onError` and `App.onUnhandledRejection` events, collects and reports error messages, and you can also try to trigger errors manually.

* On onShow, obtain page route changes and send PV.

* Performance monitor: Monitor the page lifecycle and report pageload performance

* SetData performance: Monitor performance by hooking into setData

* Request monitor: Monitor requests by hooking requests


<span id="API"></span>
## API

The following lists all interfaces exposed by the imported Monitoring instance, along with explanations of each interface's feature. You may call these interfaces as needed.

<span id="vemars.init(config?: UserConfig) => void"></span>
### vemars.init(config?: UserConfig) =\> void

Initialize the monitoring instance. The type of UserConfig is the same as that in the detailed configuration above.

<span id="vemars.config(config?: Partial) => void"></span>
### vemars.config(config?: Partial) =\> void

Configure a monitoring instance. UserOptions is of the same type as in the detailed configuration above.

```Plain Text
interface MutableConfig {
  context: Record<string, any>
}

```


<span id="vemars.capture(error: Error) => void"></span>
### vemars.capture(error: Error) =\> void

Actively capture errors.

<span id="vemars.report(event: ReportEvent) => void"></span>
### vemars.report(event: ReportEvent) =\> void

Custom reporting for various event types; the different reporting types are not described here.

```Plain Text
type ReportEvent =
  | PageviewReportEvent
  | JsErrorReportEvent
  | RequestReportEvent
  | SetDataReportEvent
  | PageFirstLoadReportEvent
  | PageOnReadyReportEvent

```


<span id="vemars.addBreadcrumb(type: BreadcrumbType, payload: any) => void"></span>
### vemars.addBreadcrumb(type: BreadcrumbType, payload: any) =\> void

For custom breadcrumb reporting, the payload will be unpacked into the breadcrumbs.

```Plain Text
enum BreadcrumbType {
  DOM = 'dom',
  HTTP = 'http',
}

```


<span id="vemars.sendNow() => void"></span>
### vemars.sendNow() =\> void

To reduce the request count per second, the SDK adopts a batch reporting policy. A reporting request is sent only after either 10 events have been collected or 1 second has passed since the previous request. Calling this method allows you to report immediately.
