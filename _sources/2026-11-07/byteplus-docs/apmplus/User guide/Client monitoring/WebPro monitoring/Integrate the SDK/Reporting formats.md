---
title: "Reporting formats"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Reporting_formats"
---

If you use the `beforeSend` lifecycle or conditional sampling, you need to pay attention to the reporting format of the SDK.

<span id="ReportEvent"></span>
## ReportEvent

```ts
export type SendEvent =
  | CustomReport
  | HttpReport
  | JsErrorReport
  | PageviewReport
  | PerformanceReport
  | PerformanceLongTaskReport
  | PerformanceTimingReport
  | ResourceErrorReport
  | ResourceReport
  | BlankReport

export type WebReport = Omit<SendEvent,'common'> 

export type ReportEvent<T extends WebReport> = T & {
  extra?: Partial<Common>
  // Allows you to report some additional context to override the assembled context, mainly in pre-collection and preloading scenarios
  overrides?: Partial<Common>
}
```


<span id="Common"></span>
## Common

```ts
interface Common {
  /** Application identifier */
  aid: number
  /** Page identifier */
  pid: string
  /** Page visit identifier, used to distinguish multiple visits to the same pid */
  view_id: string
  /** User identifier, set by the integrator */
  user_id: string
  /** Device identifier, stored in Local Storage */
  device_id: string
  /** Instance session identifier */
  session_id: string
  /** Custom dimension */
  context: { [key: string]: string }
  /** Code deployment version. Caution: Do not use a leading zero for release */
  release: string
  /** Code deployment environment */
  env: string
  /** Environment */
  url: string
  protocol: string
  domain: string
  path: string
  query: string
  /** Changes dynamically; requires monitoring */
  network_type: string
  /** Client timestamp, occurrence time */
  timestamp: number
  /** Report SDK version */
  sdk_version: string
  /** Report the SDK name to distinguish third-party SDKs */
  sdk_name: string
  /** Effective sampling rate for the current event hit */
  sample_rate: number
}
```


<span id="Custom"></span>
## Custom

```ts
interface CustomReport {
  /** custom */
  ev_type: string
  payload: CustomPayload
  common: Common
}

interface CustomPayload {
  /** Custom name, required when type is event */
  name?: string
  /** Custom value */
  metrics?: { [key: string]: number }
  /** Dimensions of the event itself; do not merge with external context */
  categories?: { [key: string]: string }
  /** Custom log content. Can be a log or the JSON representation of an object. Required when type is log. */ It is recommended that the length does not exceed 1024; the platform may truncate logs that are too long. */
  content?: string
  /** Levels of custom log: debug | info | warn | error */
  level?: string
  /** Custom type: event | log */
  type: string
}
```


<span id="Http"></span>
## Http

```ts
interface HttpReport {
  /** http */
  ev_type: string
  payload: HttpPayload
  common: Common
}

interface HttpPayload {
  /** xhr | fetch | request | jsbridge */
  api: string
  request: HttpReq
  response: HttpRes
  duration: number
  extra?: { [key: string]: string }
  trace?: HttpTrace
}

interface HttpReq {
  method: string
  url: string
  protocol: string
  domain: string
  path: string
  query: string
  headers?: { [key: string]: string }
  body?: string
  timestamp: number
}

interface HttpRes {
  status: number
  is_custom_error: boolean
  headers?: { [key: string]: string }
  body?: string
  timing?: PerformanceResourceTiming
  timestamp: number
}

interface HttpTrace {
  trace_id: string
  trace_host: string
  log_id: string
}
```


<span id="JS Error"></span>
## JS Error

```ts
interface JsErrorReport {
  /** js_error */
  ev_type: string
  payload: JsErrorPayload
  common: Common
}

interface JsErrorPayload {
  error: JsError
  breadcrumbs: Array<Breadcrumb>
  extra?: { [key: string]: string }
  react?: ReactInfo
}

interface JsError {
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

interface Breadcrumb {
  /** dom | http */
  type: string
  /** xpath, keyvalue | url */
  message: string
  /** ui.click, ui.keypress | post,get */
  category: string
  /** status: 400 for http */
  data?: { [key: string]: string }
  timestamp: number
}

interface ReactInfo {
  version: string
  componentStack: string
}
```


<span id="Pageview"></span>
## Pageview

```ts
interface PageviewReport {
  /** pageview */
  ev_type: string
  payload: PageviewPayload
  common: Common
}

interface PageviewPayload {
  pid: string
  /** Trigger reasons: init | path change | hash change | history state change | user-set */
  source: string
}
```


<span id="Performance Longtask"></span>
## Performance Longtask

```ts
interface PerformanceLongtaskReport {
  /** performance_longtask */
  ev_type: string
  payload: PerformanceLongtaskPayload
  common: Common
}

interface PerformanceLongtaskPayload {
  /** Performance metric type: perf => traditional performance, spa => SPA performance, garfish => Garfish micro-frontend performance */
  type: string
  longtasks: Array<PerformanceLongtask>
}

interface PerformanceLongtask {
  /** struct PerformanceEntry { */
  duration: number
  entryType: string
  name: string
  startTime: number
  /** } */
  attribution?: Array<TaskAttributionTiming>
}

interface TaskAttributionTiming {
  /** struct PerformanceEntry { */
  duration: number
  entryType: string
  name: string
  startTime: number
  /** } */
  containerType: string
  containerSrc: string
  containerId: string
  containerName: string
}
```


<span id="Performance Timing"></span>
## Performance Timing

```TypeScript
interface PerformanceTimingReport {
  /** performance_timing */
  ev_type: string
  payload: PerformanceTimingPayload
  common: Common
}

interface PerformanceTimingPayload {
  timing?: PerformanceTiming
  navigation_timing?: PerformanceNavigationTiming
  /** Whether to exit */
  isBounced: boolean
}

interface PerformanceTiming {
  connectEnd: number
  connectStart: number
  domComplete: number
  domContentLoadedEventEnd: number
  domContentLoadedEventStart: number
  domInteractive: number
  domLoading: number
  domainLookupEnd: number
  domainLookupStart: number
  fetchStart: number
  loadEventEnd: number
  loadEventStart: number
  navigationStart: number
  redirectEnd: number
  redirectStart: number
  requestStart: number
  responseEnd: number
  responseStart: number
  secureConnectionStart: number
  unloadEventEnd: number
  unloadEventStart: number
}

interface PerformanceNavigationTiming {
  /** struct PerformanceResourceTiming { */
  /** struct PerformanceEntry { */
  duration: number
  entryType: string
  name: string
  startTime: number
  /** } */
  connectEnd: number
  connectStart: number
  decodedBodySize: number
  domainLookupEnd: number
  domainLookupStart: number
  encodedBodySize: number
  fetchStart: number
  initiatorType: string
  nextHopProtocol: string
  redirectEnd: number
  redirectStart: number
  requestStart: number
  responseEnd: number
  responseStart: number
  secureConnectionStart: number
  transferSize: number
  workerStart: number
  /** } */
  domComplete: number
  domContentLoadedEventEnd: number
  domContentLoadedEventStart: number
  domInteractive: number
  loadEventEnd: number
  loadEventStart: number
  redirectCount: number
  type: string
  unloadEventEnd: number
  unloadEventStart: number
}

interface PerformanceResourceTiming {
  /** struct PerformanceEntry { */
  duration: number
  entryType: string
  name: string
  startTime: number
  /** } */
  connectEnd: number
  connectStart: number
  decodedBodySize: number
  domainLookupEnd: number
  domainLookupStart: number
  encodedBodySize: number
  fetchStart: number
  initiatorType: string
  nextHopProtocol: string
  redirectEnd: number
  redirectStart: number
  requestStart: number
  responseEnd: number
  responseStart: number
  secureConnectionStart: number
  transferSize: number
  workerStart: number
  serverTiming?: Array<PerformanceServerTiming>
}

interface PerformanceServerTiming {
  description: string
  duration: number
  name: string
}
```


For more information about parameters, refer to [mdn Web APIs](https://developer.mozilla.org/en-US/docs/Web/API/PerformanceResourceTiming).

<span id="Performance"></span>
## Performance

```ts
interface PerformanceReport {
  /** performance */
  ev_type: string
  payload: PerformancePayload
  common: Common
}

interface PerformancePayload {
  /** Metric name */
  name: string
  /** Current value */
  value: number
  /** Performance metric type: perf => traditional performance, spa => SPA performance */
  type: string
  /** Whether supported */
  isSupport?: boolean
  /** Whether it is a polyfill */
  isPolyfill?: boolean
  /** Whether to exit */
  isBounced?: boolean
  /** Whether custom */
  isCustom?: boolean
  /** Related information about the metric */
  extra?: { [key: string]: string }
}
```


<span id="Resource Error"></span>
## Resource Error

```ts
interface ResourceErrorReport {
  /** resource_error */
  ev_type: string
  payload: ResourceErrorPayload
  common: Common
}

interface ResourceErrorPayload {
  /** Type of trigger tag: script, link, or css */
  type: string
  url: string
  protocol: string
  domain: string
  path: string
  query: string
  timing?: PerformanceResourceTiming
}
```


<span id="Resource"></span>
## Resource

```ts
type ResourcePayload = PerformanceResourceTiming

interface ResourceReport {
  /** resource */
  ev_type: string
  payload: ResourcePayload
  common: Common
}
```
