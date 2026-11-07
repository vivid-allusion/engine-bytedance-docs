---
title: "Call an API using the SDK"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Call_an_API_using_the_SDK"
---

This article introduces how to use the SDK to call APIs in Mini Program Pro.

<span id="frY8uSu8"></span>
## Usage description

Throughout this document, 'client' refers to an SDK instance.

<span id="jlbYeJSC"></span>
## Initialize

<span id="qye6pHm0"></span>
### init

After the call, the server side configuration is fetched and various events are listened for. To ensure that the information being monitored is as complete as possible, place init at the very beginning. It is recommended to call this method before initializing the App; reporting will begin after start is called.

```JavaScript
interface InitConfig  {
  aid: number // Unique project identifier, required
  token: string // Project token, required
  userId?: string // user ID,
  deviceId?: string // device ID
  useLocalConfig?: boolean // Whether to use only the local configuration. The default is false, in which case the rules will be merged with the platform configuration.
  // The specific configuration for sampling configuration and plugin configuration can be viewed in the detailed configuration
  sample?: SampleConfig // Sampling configuration
  plugins?: { ... } // Plugin configuration. For details, see the "Plugin configuration" page.
  domain?: string// Report domain name. Applications released in China report data to servers located in mainland China. The domain name is https://apmplus.volces.com. Applications released overseas: report to the server in Johor, Malaysia. The domain name is https://apmplus.ap-southeast-1.volces.com. If no configuration is provided, data will be reported to servers in mainland China by default.
}
client.init(c: InitConfig) =>  void // Type

// Call
client.init({
   aid: 66, // Replace with your aid
   token:'xxx-xxx' // Replace with your token
})
```


<span id="SGEjAJFJ"></span>
### config

Change the general property context. Calling this before start can be used to asynchronously set userId and deviceId.

```javascript
interface MiniProgramUserConfig {
  pid: string
  userId: string
  deviceId: string,
}
client.config(config: MiniProgramUserConfig) =>  void // type

// Called to asynchronously modify general properties: userId & deviceId
client.config({
    userId: 'userId_test',
    deviceId: 'deviceId_test'
})
```


<span id="Nsol8zQv"></span>
### start

Data reporting is typically triggered after asynchronous modification of general attributes.

```javascript
client.start()
```


For example, if you need to wait for an API to issue a UserId and then report it, you can integrate using the following pseudocode method:

```typescript
// Start collecting monitoring data
client.init({
   aid: 123, // Replace with your aid
   token:'xxx-xxx' // Replace with your token
})
App({
  onLaunch() {},
  onShow() {
    getUserId().then(res => {
      // Set userId
      client.config({
        userId: res.userId
      })
      // Start reporting data
      client.start()
    })
  },
})
```


<span id="2waR2ynz"></span>
## Change the general context

<span id="dB6yKpLC"></span>
### context.set

Setting a custom dimension: context is the global dimension context and applies to all events. After the context is updated, only events that are packaged after the update are affected.

Because some events, such as pageview, are sent during init. If you need to set some initialization context, make sure to set the context before init.

```javascript
interface ContextAgent {
  set: (k: string, v: any) => ContextAgent
  merge: (ctx: Record<string, any>) => ContextAgent
  delete: (k: string) => ContextAgent
  clear: () => ContextAgent
  get: (k: string) => string
  toString: () => Record<string, string>
}

client.context.set('key', 'value') // Setting a single key in the context
client.context.merge({ key: 'value' })  // Merge context and the passed-in object to generate a new context
client.context.delete('key')  // Delete a key from context
client.context.clear() // Clear context
```


<span id="RehLyWND"></span>
## Active reporting

<span id="z8IGTRQ0"></span>
### sendPageview

A PV is reported each time, even when the same PID is reported repeatedly.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The program includes a relaunch event that can re\-render the current page.</div>


```javascript
client.sendPageview(pid: string) =>  void //type

client.sendPageview('pid_test') // Call
```


<span id="Q330J9ga"></span>
### sendPageviewWithHide

Settle the dwell time for the current PID. Each call will consume the current PID, and if called multiple times, it will only be reported once.

```javascript
const enum PageviewSourceType {
  init = 'init',
  history = 'history',
  user_set = 'user_set',
  hide = 'hide',
  unload = 'unload',
}
client.sendPageviewWithHide(source = PageviewSourceType.hide) =>  void // type

client.sendPageviewWithHide('hide') // Call
```


<span id="3t6vVJhI"></span>
### sendEvent

Report a custom event.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">If the event format does not conform, conversion will be attempted. Events that cannot be converted will be reported, but the server side will not be able to consume them.</div>


```javascript
interface CustomEventPayload {
  /** Custom event name */
  name: string
  /** metrics report measurable values, that is, numbers */
  metrics?: { [key: string]: number }
  /** categories contains classifications and dimensions, which are used for filtering and grouping */
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


<span id="yZjyynCI"></span>
### sendLog

Report a custom log.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">If the log format is invalid, an attempt will be made to convert it. Logs that cannot be converted will be reported, but the server side cannot consume them.</div>


```javascript
export  interface  CustomLogPayload  {
  /** Additional supplementary information. When reporting, number values are routed to metric, and string values are routed to categories. */
    extra?: { [key: string]: string | number }  //    /** Custom event content, which can be a log or the JSON representation of an object. */
  content: string
  /** Custom event level. The default is info. Enumerated values: debug, info, warn, error. */
    level?:  'debug'  |  'info'  |  'warn'  |  'error'
}

client.sendLog(data:  CustomLogPayload) =>  void // type
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


<span id="Ptr2G1ER"></span>
### captureException

Manually capture JS exceptions and pass the error's name, message, and stack.

```javascript
export interface JsError {
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
client.captureException(error: JsError, extra?: { [key: string]: string }) => void // type

// Call
client.captureException({
   name: 'Error',
   message: 'Test Error'
})
```


<span id="wIrnx7YP"></span>
### addBreadcrumb

Add user behavior stack. It will not be reported separately; user behavior stack information will be included when reporting JS Error.

```javascript
interface Breadcrumb {
  /** route | http */
  type: string
  /** methodName | url */
  message: string
  /** errMsg | post,get | tap */
  category: string
  /** route {url} | http {mehtod,url,status_code} */
  data?: { [key: string]: string }
 }
client.addBreadcrumb(breadcrumb: Breadcrumb) => void // type

client.addBreadcrumb({
    type: 'route',
    message: 'navigateTo',
    category: 'ok',
    data: 'pages/index/index'
})
```


<span id="pdNidrou"></span>
## Lifecycles

When you need to understand what has been done in the Client or need to debug the Client, you can use the following lifecycle functions.

<span id="R1t9IkwK"></span>
### init

The listener instance has been initialized.

```javascript
client.on('init',() => {
  ...
})
```


<span id="DcrKrHWs"></span>
### start

Turn on reporting for listener instances.

```javascript
client.on('start', () => {
   ...
})
```


<span id="YdwtvRW9"></span>
### beforeConfig

The new configuration can be obtained before monitoring instance configuration changes.

```javascript
client.on('beforeConfig', (config: Partial<Config>) => {
    ...
})
```


<span id="4HMz1van"></span>
### config

The moment immediately after an instance configuration change is detected.

```javascript
client('on', 'config', () => {
    ...
})
```


<span id="uYDQhzAL"></span>
### provide

When the instance listens for the moment a property is mounted, the property name can be obtained.

```javascript
client('on', 'provide', (name: string) => {
   ...
})
```


<span id="aUmnSnex"></span>
### report

At the moment an event is sent by the Monitoring plugin, this is used to supplement the event context. If a Falsy type is returned, the event will not be reported.

```javascript
type Falsy = false | null | undefined
client.on('report', (ev: ReportEvent): ReportEvent | Falsy => {
    ...
    return ev
})
```


<span id="l9kbLuO1"></span>
### beforeBuild

At the moment just before the event is wrapped in context, you can access the data that is about to be wrapped. If a falsy type is returned, the event will not be reported.

```javascript
type Falsy = false | null | undefined
client.on('beforeBuild', (ev: ReportEvent): ReportEvent | Falsy => {
    ...
    return ev
})
```


<span id="VyoDe1YG"></span>
### build

At the moment when the event is wrapped in context, the data that is about to be reported can be accessed; if a Falsy type is returned, the data will not be reported.

```javascript
type Falsy = false | null | undefined
client.on('build', (ev: SendEvent): SendEvent | Falsy => {
    ...
    return ev
})
```


<span id="2Wf3BLqj"></span>
### beforeSend

If a falsy value is returned at the moment before the event is sent, the event will not be reported.

```javascript
type Falsy = false | null | undefined
client.on('beforeSend', (ev: SendEvent): SendEvent | Falsy => {
    ...
    return ev
})
```


<span id="vJj5F6Xd"></span>
### send

Callback after the register event is sent.

```javascript
interface Callback<T> {
  (arg: T): void
}
client.on('send', (e: Callback<SendEvent>) => {
    ...
})
```


<span id="RCy6WPhJ"></span>
### beforeDestroy

Callback before the destruction of a registered instance.

```javascript
client('on', 'beforeDestroy', () => {
   ...
})
```


<span id="mr5Mo25g"></span>
## Active trigger

<span id="0aKXxmYv"></span>
### getSender().flush()

Report data immediately. By default, the SDK caches data in a queue and sends it in batches. It also ensures all cached data is reported before you turn off the mini program, reducing network connection loss. When the user wants to force a data report at any time, the following method can be called:

```TypeScript
// Can only be called after client init, so it must be invoked in the init callback
client('on', 'init', () => {
   client.getSender().flush()
})
```
