---
title: "Use the SDK to call an API"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Use_the_SDK_to_call_an_API"
---

This article describes how to use the SDK to call APIs in WebPro.

<span id="8h08Cqtl"></span>
## **Precautions**

Throughout the document, `client` refers to the SDK instance. For information on obtaining an SDK instance, refer to [SDK integration](https://docs.byteplus.com/en/docs/apmplus/Integrate_WebPro_SDK).

<span id="EZqViZe5"></span>
### Initialization

Initialize the client instance. The initialization configuration can include a general event context. Configuration settings other than the general event context take effect only once.

After init is called, the system will start to fetch the server side configuration and fetch plugins that are loaded asynchronously.

**client('init', c: InitConfig) =\> void**

```TypeScript
interface InitConfig  {
  aid: number; // Project unique identifier, must be provided
  token: string; // Project token (required)
  // General event context
  pid?: string;
  userId?: string;
  deviceId?: string; // If not provided, a uuid will be generated as the deviceId. If the value is provided by the business logic, please try to avoid special characters in the provided value. (may include dot, slash, hyphen, underscore, or comma)
  release?: string; // Used to distinguish different versions. If an input is provided, ensure that its length is less than 17 characters and try to avoid special characters. (May contain dot, slash, hyphen, underscore, and comma)
  env?: string; // Used to distinguish between different environments. If you pass in a value, please ensure it contains as few special characters as possible. (may contain dot, slash, hyphen, underscore, comma)
  useLocalConfig?: boolean; // Whether to use only local configuration; default is off
  storageExpires?: number | boolean;// Configure storage expiration time; default is 90 days
  
  // The specific settings for sampling configuration and plugin configuration can be viewed in the detailed configuration section.
  sample?: SampleConfig; // Sampling configuration
  plugins?: { ... }; // For details, you can view [Configuration plugin]

  // Special configuration
  pluginBundle?: {
    name: string;
    plugins: string[];
  }; // Plugin packaging and loading configuration; non-custom plugins do not require configuration
  pluginPathPrefix?：string; // Plugin loading path prefix, used for debugging (for example, http://localhost:8081/cn/plugins) or for loading custom plugins
  domain?: string; // Report domain name. Applications released in China report to servers located in mainland China, with the domain name https://apmplus.volces.com. Applications released overseas send data to the server in Johor, Malaysia, whose domain name is https://apmplus.ap-southeast-1.volces.com. If no configuration is provided, it will be reported to servers in mainland China by default.
}
```


<span id="nAUIEhMP"></span>
#### Example

```TypeScript
client('init', {
  aid: 123456, // Your aid
  token:'xxx-xxx', // Replace with your token
  env: 'boe',
  release: '1.0.221'
})
```


<span id="dLqyNKHN"></span>
### Update configurations

Change the general context; this only takes effect for events sent after the update. If you need this to apply to all events, make sure to call it before start.

**client('config', c?: Partial) =\>WebConfig**

```TypeScript
// config modifiable configuration
interface UserConfig {
  pid: string;
  userId: string;
  deviceId: string;
  sessionId：string;
  release: string;
  env: string;
}

// Configuration obtained by config
interface WebConfig {
  aid: number; // Unique project identifier, required
  token: string; // Project token (required)
  // General event context
  pid: string;
  userId: string;
  deviceId: string;
  sessionId: string; // Distinguish different sessions
  release: string;// Distinguish different versions
  env: string;// Distinguish between different environments
  useLocalConfig: boolean; // Whether to use only local configuration; default is off
  storageExpires?: number | boolean; // Configuration of the expiration time for storage. The default is 90 days.
  
  // The specific configuration for sampling configuration and plugin configuration can be viewed in the detailed configuration.
  sample: SampleConfig; // Sampling configuration
  plugins: { ... }; // Plugin configuration

  // Special configuration
  pluginBundle: {
    name: string;
    plugins: string[];
  }; // Plugin packaging and loading configuration; non-custom plugins do not require configuration
  pluginPathPrefix：string; // Plugin loading path prefix, used for debugging (for example, http://localhost:8081/cn/plugins) or for loading custom plugins
  domain?: string; // Reporting domain name. No configuration is required for SaaS; for private deployment, you must configure the reporting domain name for the specific environment.
}
```


<span id="IblRmfxV"></span>
#### Example

```TypeScript
// Update configuration
client('config', {
  userId: 'test_user',
})

// Obtain the SDK's current configuration. If the SDK has not been initialized, it will return undefined.
const config = client('config')
```


<span id="hoN1HaBW"></span>
### Turn on reporting

```JavaScript
client('start')
```


<span id="oAvTygbh"></span>
### Setting global context

Set a custom dimension. context is a globally scoped context that applies to all events. The updated context only applies to events that occur afterwards.

```TypeScript
client("context.set", "key", "value"); // Set a single key in the context
client("context.merge", { key: "value" }); // Merge context and the passed-in object to generate a new context
client("context.delete", "key"); // Delete a key from context
client("context.clear"); // Clear context
```



* If you want to provide some initialization context, you need to set the context before init. Some events are sent during initialization, for example, pageview.

* If you need to set the context after initialization and want it to take effect for all reporting, you can use the [refreshPreStartContext](https://docs.byteplus.com/en/docs/apmplus/Integrate_plugins_as_needed#refreshPreStartContext) plugin.


<span id="VgFRB6As"></span>
### Report PV

Report a PV. If the pid is the same as the current pid, this PV will be ignored.

**client('sendPageview',pid: string) =\> void**

<span id="yX29q2UU"></span>
#### Example

```JavaScript
client('sendPageview', '/test/pageA')
```


<span id="MolRCr0K"></span>
### Report a custom event

Report a custom event. Caution: Pay attention to the format. Events that do not comply with the required format will be converted if possible; events that cannot be converted will be ignored. Specific consumption methods can be viewed in the [custom monitor](https://docs.byteplus.com/en/docs/apmplus/custom_monitor).

**client('sendEvent', data: CustomEventPayload) =\> void**

```TypeScript
interface CustomEventPayload {
  /** Custom event name */
  name: string;
  /** Metrics report measurable values, that is, numerical values. */
  metrics?: { [key: string]: number };
  /** categories refers to classification and dimensions, which are used to filter and group */
  categories?: { [key: string]: string };
}
```


<span id="mj9yZu6M"></span>
#### Example

```TypeScript
client('sendEvent', {
  name: 'login_event',
  metrics: {
    login_count: 1,
    login_api_duration: 1000,
    server_timing: 3456,
    login_level: 23,
  },
  categories: {
    where: 'login_page',
  },
})
```


<span id="kYDigGIR"></span>
### Report a custom log

Report a custom log Caution: Ensure correct formatting. An attempt will be made to convert events that do not conform to the required format; events that cannot be converted will be ignored.

**client('sendLog', data: CustomLogPayload) =\> void**

```TypeScript
interface CustomLogPayload {
  /** Additional information. When reporting, numbers will be routed to metrics and strings will be routed to categories. */
  extra?: { [key: string]: string | number }; //
  /** Custom event content; any string, such as a log or the JSON string of an object, and more */
  content: string;
  /** Custom event level. The default is info. Available options: debug | info | warn | error. */
  level?: "debug" | "info" | "warn" | "error";
}
```


<span id="HGkVcqy4"></span>
#### Example

```TypeScript
client('sendLog', {
  level: 'error',
  content: `user loggedin from ${prev}`,
  extra: {
    where: 'login_page',
  },
})
```


<span id="nlFGUhqD"></span>
### Report a JavaScript error

**client('captureException', error: any, extra?: { [key: string]: string }, react?: ReactInfo) =\> void**

```TypeScript
export interface ReactInfo {
  version: string;
  componentStack: string;
}
```


<span id="RErGKDHu"></span>
#### Example

```TypeScript
// Report an error
client('captureException', new Error('test error'))

// Report an error message
client('captureException', 'custom error')

// Report an error and include relevant error context
client('captureException', new Error('login error'), { loginId: 'xxxxx' })
```


<span id="WkjSXYww"></span>
### Report performance metrics


* If the metric is integrated by default, for example FP or FCP, you can turn off reporting in the Performance plugin and report it up to the platform using this custom reporting method. The platform will then automatically consume the data.

* If the metric is not integrated by default, you can report it using this custom method. After registering the metric in performance metric management, it will then be available for consumption on the platform.


**client('sendCustomPerfMetric', metric: PerformancePayload) =\> void**

```TypeScript
interface PerformancePayload {
  /** Metric name */
  name: string;
  /** Current value */
  value: number;
  /** Performance metric type: perf => traditional performance, spa => SPA performance, mf => micro-frontend performance */
  type?: string = "perf";
  /** Whether it is supported */
  isSupport?: boolean;
  /** Whether this is a polyfill */
  isPolyfill?: boolean;
  /** Whether to exit */
  isBounced?: boolean;
  /** Whether custom is enabled */
  isCustom?: boolean;
  /** Related information about the metric */
  extra?: { [key: string]: string };
}
```


<span id="oyZHvDJO"></span>
#### Example

```TypeScript
client('sendCustomPerfMetric', { name: 'fcp', value: 3500 }
```


<span id="3oh0CHST"></span>
### Destroy an instance

Calling this method can remove all listeners and side effects, including hook or memory objects. The current instance is still available, so data can still be reported by manually calling the API.

```TypeScript
client('destroy')
```


<span id="qqOOYEQo"></span>
### Report any event

Report an event directly. For the specific format, see [Reporting format](https://docs.byteplus.com/en/docs/apmplus/Reporting_formats).

**client('report', ev: ReportEvent) =\> void**

<span id="g3gsNtln"></span>
#### Example

```TypeScript
client('report', {
  ev_type: 'pageview',
  payload: {
    source: 'history',
    pid: '/pageB'
  }
})
```


<span id="PNcsfnKq"></span>
### Custom additional breadcrumbs

Breadcrumbs are mainly included when reporting JavaScript errors. If your business wants to customize some breadcrumbs, you can use the following method.

**client('addBreadcrumb',breadcrumb: Breadcrumb) =\> void**

```TypeScript
export interface Breadcrumb {
  /** dom | http */
  type: string;
  /** xpath, keyvalue | url */
  message: string;
  /** ui.click, ui.keypress | post,get */
  category: string;
  /** status: 400 for http */
  data?: { [key: string]: string };
}
```


<span id="oVSXj9No"></span>
#### Example

```TypeScript
client('addBreadcrumb', { type: 'custom', message: 'user login', category: 'webview' })
```


<span id="SEqgZusX"></span>
### Manually package Fetch

**client('wrapFetch', fetch: typeof window.fetch) =\> typeof window.fetch ｜ undefined**

If manual packaging is required, pay attention to the following points:


* Must be executed after init. Because wrapFetch is mounted dynamically during init, you need to execute wrapFetch after init.

* You need to use the npm integration method. When integrating the script, the main script is loaded first. Before this occurs, all calls are only cached and are not actually executed, so if you execute calls in advance, the return value you receive will be undefined.

* You need to set the autoWrap configuration of the fetch plugin to false. Since manual packaging is selected, monitoring reports for other unrelated requests generated by automatic packaging should be avoided.


<span id="FcWqFoEr"></span>
#### Example

```TypeScript
import client from '@apmplus/web'

client('init', {
  ...
  plugins: {
    autoWrap: false,
  },
  ...
})

const fetchAfterWrap = client('wrapFetch', window.fetch)

// then, use  fetchAfterWrap to request
```


<span id="ITERJBgl"></span>
### Manually detect a blank screen

**client('detectBlankScreen')** 

<span id="mAnMa0zj"></span>
#### Example

```TypeScript
import client from '@apmplus/web'

client('init', {
  ...
  plugins: {
    blankScreen: {
       // Turn off automatic detection and switch to the manual detection option below
       autoDetect: false
    },
  },
  ...
})

client('detectBlankScreen')
```


<span id="0ICJDzbZ"></span>
### Immediately report data

By default, when the page is turned off, the SDK uses sendBeacon to forcibly send the data in the cached queue. However, if the user manually calls certain APIs to report data when the page is turned off, data may not be sent due to timing issues. You can use the following method to forcibly send the data:

```TypeScript
import client from '@apmplus/web'

// Placing this in the callback ensures that the SDK has been fully initialized and prevents errors.
onPageUnload(() => {
    client('on', 'init', () => {
       client.getSender().flush()
    })
})
```
