---
title: "The reporting format"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/The_reporting_format"
---

If you use the beforeSend lifecycle or conditional sampling, you need to pay attention to the SDK's reporting format.

<span id="ReportEvent"></span>
## ReportEvent

```typescript
export type MiniProgramReport =
  | CustomReport
  | HttpReport
  | JsErrorReport
  | PageviewReport
  | PagePerformanceReport
  | AppLaunchPerformanceReport
  | PerformanceReport
  | SetDataReport

export type ReportToReportEvent<T extends MiniProgramReport> = T & {
  extra?: Partial<CommonContext>
  // Allow reporting additional context to override the assembled context
  overrides?: Partial<CommonContext>
}

export type MiniProgramReportEvent = ReportToReportEvent<MiniProgramReport>
```


<span id="Common"></span>
## Common

```javascript
export interface Common {
  /** Application identifier */
  aid: number
  /** Page identifier */
  pid: string
  /** Page visit identifier, used to distinguish multiple visits with the same pid */
  view_id: string
  /** User identifier, set by the integrator */
  user_id: string
  /** User action ID */
  action_id?: string
  /** Custom dimension */
  context: { [key: string]: string }
  /** URL of the current page */
  url: string
  /** Network environment */
  network_type: string
  /** Client timestamp, occurrence time */
  timestamp: number
  /** Effective sampling rate for the current event hit */
  sample_rate: number
  /**@querysver: report SDK version */
  sdk_version?: string
  /**@querysname, used to report the SDK name to distinguish third-party SDKs */
  sdk_name?: string
  /**@query/* soffset client time offset, assists the server side with time calibration */
  sdk_offset?: number
  /**@querydid device identifier, stored in Local Storage */
  device_id?: string
  /**@querysid session instance identifier */
  session_id?: string
  /**@querymenv Mini Program platform environment versions: develop, trial, release (may be more) */
  mini_env?: string
  /**@query/* mver mini program online version */
  mini_version?: string
  /**@querydevice model: 'iPhone 12 pro' */
  model?: string
  /**@querybrand: device brand, Iphone Apple */
  brand?: string
  /**@queryratio: pixel ratio 2 */
  pixel_ratio?: number
  /**@query/* screen Screen width and height, in px. number * number, screenWidth * screenHeight */
  screen_area?: string
  /**@queryYou can use the window's width and height. Unit: px; format: number * number; example: windowWidth * windowHeight.
  window_area?: string
  /**@query  lang language
  lang?: string
  /**@queryosname Operating System */
  os_name?: string
  /**@queryOperating system version */
  os_version?: string
  /**@querylibver Mini Program base library version */
  lib_version?: string
  /**@queryhostname host name: douyin, xigua, and toutiao */
  host_name?: string
  /**@queryhostver host version */
  host_version?: string
  /**@queryscene Scene value */
  scene?: number
  /**@query  platform Current mini program host type: wx, tt, my, or swan */
  platform?: string
}
```


<span id="CustomReport"></span>
## CustomReport

```javascript
export interface CustomSend {
  /** custom */
  ev_type: string
  payload: CustomPayload
  common: common.Common
}

export interface CustomPayload {
  /** Custom name; required when type is event */
  name?: string
  /** Custom value */
  metrics?: { [key: string]: number }
  /** The dimension of the event itself; do not merge it with the external context. */
  categories?: { [key: string]: string }
  /** Custom log content. Can be a log or the JSON representation of an object. Required when type is log. */
  content?: string
  /** Custom log level: debug | info | warn | error */
  level?: string
  /** Custom type: event | log */
  type: string
}
```


<span id="Http"></span>
## Http

```javascript
export interface HttpSend {
  /** http */
  ev_type: string
  payload: HttpPayload
  common: common.Common
}

export interface HttpPayload {
  /** request | uploadFile | downloadFile*/
  api: string
  request: HttpReq
  response: HttpRes
  /** elapsed time from send to response calculate by SDK */
  duration: number
  /** elapsed time for callback of (fail+success+complete) after responded */
  cbTime: number
  extra?: { [key: string]: string }
}

export interface HttpReq {
  method: string
  url: string
  headers?: { [key: string]: string }
  body?: string
  timestamp: number
}

export interface HttpRes {
  /** Status code */
  status: number
  /** Whether it has been wrapped by extraExtractor */
  is_custom_error: boolean
  headers?: { [key: string]: string }
  body?: string
  timing?: PerformanceTiming
  timestamp: number
  err_msg?: string
}

export interface PerformanceTiming {
  /** tt is temporarily not supported */
  redirectStart?: number
  /** tt is temporarily not supported */
  redirectEnd?: number
  /** tt is temporarily not supported */
  fetchStart?: number
  domainLookupStart: number
  domainLookupEnd: number
  connectStart: number
  secureConnectionStart: number
  connectEnd: number
  requestStart: number
  requestEnd: number
  responseStart: number
  responseEnd: number
  /** Whether to reuse the connection */
  socketReused: boolean
  /** tt does not currently support the actual download speed (kbps) of the current network */
  throughputKbps?: number
  /** tt does not currently support the number of bytes sent */
  sendBytesCount?: number
  /** tt temporarily does not support the number of bytes received */
  receivedBytedCount?: number
  /** Protocol type in use. Valid values: http1.1, h2, quic, unknown */
  protocol?: string
}
```


<span id="JS Error"></span>
## JS Error

```javascript
export  interface  JsErrorPayload  {
  error:  JsError
  breadcrumbs:  Array<Breadcrumb>
    extra?: { [key: string]: string }
    react?:  ReactInfo
}

export  interface  JsError {
  /** Error name */
    name?: string
  /** Error message */
  message: string
  /** Stack trace */
    stack?: string
  /** Error file name */
    filename?: string
    lineno?: string
    colno?: string

}

export  interface  Breadcrumb  {
  /** route | http */
  type: string
  /** methodName | url */
  message: string
  /** errMsg | post,get | tap */
  category: string
  /** route {url} | http {mehtod,url,status_code} */
    data?: { [key: string]: string }
  timestamp: number

}

export  interface  ReactInfo  {
  version: string
  componentStack: string

}
```


<span id="Pageview"></span>
## Pageview

```typescript
export interface PageviewPayload {
  pid: string
  /** Trigger type: launch | show | history | user-set | hide | unload */
  source: string
} 
```


<span id="PagePerformance"></span>
## PagePerformance

```typescript
export interface PagePerformancePayload { 
  /** Route start time. Timestamp of invoking the route method. */
  navigate_start: number
  /** Routing methods: navigateTo | navigateBack | redirectTo | reLaunchTo | switchTab | native (for example, nativeTabBar is configured in app.json, and the SDK cannot intercept it) */
  navigate_name: string
  /** timestamp of page.onLoad invoked */
  load_start: number
  /** timestamp of page.onShow invoked */
  dom_end: number
  /** timestamp of page.onReady invoked */
  render_end: number
}
```


<span id="AppLaunchPerformance"></span>
## AppLaunchPerformance

```typescript
export interface AppLaunchPerformancePayload { 
  /** timestamp of app triggered(wx/tt) */
  trigger?: number
  /** timestamp of app.onLaunch */
  init_end: number
  /** timestamp of app.onShow */
  activate_start: number
  /** timestamp of page.onLoad */
  page_load_start: number
  /** timestamp of page.onShow / default: 0 */
  page_dom_end: number
  /** timestamp of page.onReady */
  page_render_end: number
}
```


<span id="Performance"></span>
## Performance

```typescript
export interface PerformancePayload { 
  is_custom: boolean
  /** fr fp fcp lcp downloadPackage evaluateScript */
  name: string
  /** perf => traditional performance user => user manual instrumentation */
  type: string
  /** elapsed time for current metric */
  duration?: number
  /** timestamp */
  value: number
  /** judging by SDK */
  is_support: boolean
  /** auto increment,means the numbers of page loaded. Use it to distinguish between first time and others */
  count: number
}
```


<span id="setData"></span>
## setData

```typescript
export interface SetDataPayload { 
  /** elapsed time of dom render after set data */
  duration: number
  /** the data's size(byte) */
  size?: number
}
```
