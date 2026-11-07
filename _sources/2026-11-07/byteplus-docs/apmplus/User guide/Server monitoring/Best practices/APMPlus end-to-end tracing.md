---
title: "APMPlus end-to-end tracing"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/APMPlus_end-to-end_distributed_tracing"
---

APMPlus provides enterprise\-level users with an end\-to\-end tracing solution covering clients such as apps, Web, and mini programs, as well as servers including Java, Go, and Python. With the distributed tracing technology, it enables full\-process visualization and performance analysis of user behaviors, network requests, service calls, and dependent components such as databases and message queues. This helps enterprises quickly identify root causes of anomalies, optimize system performance, improve user experience, and support data\-driven business decisions.

<span id="ynksA1XN"></span>
## Background

APMPlus now fully supports end\-to\-end connectivity from user terminals to AI and middleware. The complete link includes: User terminals (e.g., Android/iOS/Web/mini programs) → Gateways (e.g., API Gateway/Ingress/Nginx) → Backend services (e.g., Java/Go/Python) → AI and middleware (e.g., Large Language Models, Databases, Caches, Message Queues).

<span id="6VWh2t4u"></span>
## Prerequisites

Before using the end\-to\-end tracing solution, ensure that the client SDK version meets the following requirements.


|SDK |Version requirements |
|---|---|
|Android SDK |Use the Android SDK apm_insight version 1.5.16.cn or later. |
|iOS SDK |Use iOS SDK version 5.1.10 or later. |
|WebPro SDK |Use WebPro SDK version 2.10.0 or later. |
|Mini Pro SDK |Use Mini Pro SDK version 0.4.0 or later. |


<span id="BOgcDk21"></span>
## Procedure

<span id="JRLhUf95"></span>
### Step 1: Integrate the client application

Based on your actual requirements, select the appropriate client type and integrate your application with APMPlus client monitoring via SDK. The following 4 integration methods for client applications are provided:


<Tabs>
<Tab zoneid="akcoZD7bUJ" title="Android monitoring">
<TabTitle>Android monitoring</TabTitle>

1. See the description in [Integrating Android SDK](https://docs.byteplus.com/en/docs/apmplus/Integrate_the_Android_SDK_into_the_application) to obtain the appropriate SDK package and initialize the SDK.

2. Add the following sample code to start the SDK and enable data collection and end\-to\-end monitoring.


```Java
ApmInsightInitConfig.Builder builder = ApmInsightInitConfig.builder();
// Controls whether network monitoring is enabled. To enable it, the apm-plugin add-on must be configured simultaneously.
builder.netMonitor(true);
// Controls whether end-to-end monitoring is enabled. The server-side APMPlus must be integrated simultaneously.
builder.enableNetTrace(true);
ApmInsight.getInstance().start(builder.build());
```



3. After integrating your application with the Android SDK, see the instructions in [Verifying Data Reporting](https://docs.byteplus.com/en/docs/apmplus/Report_verification_data_Android) to verify data reporting.


</Tab>
<Tab zoneid="bmU3Tmase5" title="iOS monitoring">
<TabTitle>iOS monitoring</TabTitle>

1. See the description in [Integrating iOS SDK](https://docs.byteplus.com/en/docs/apmplus/Integrate_the_iOS_SDK_app) to obtain the appropriate SDK package and initialize the SDK.

2. Add the following sample code to start the SDK and enable data collection and end\-to\-end monitoring.


```C++
// The following header files need to be imported
#import <RangersAPMConfig+NetworkPro.h>
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    
    RangersAPMConfig *apmConfig = [RangersAPMConfig configWithAppID:@"{{app_id}}" appToken:@"{{app_token}}"];
    apmConfig.channel = @"App Store";
    
    // Set enableTracing to YES to enable end-to-end monitoring
    apmConfig.enableTracing = YES;
    [RangersAPM startWithConfig:apmConfig];
    
    return YES;
}
```



3. After integrating your application with the iOS SDK, see the instructions in [Verifying data reporting](https://docs.byteplus.com/en/docs/apmplus/Report_verification_data) to verify data reporting.


</Tab>
<Tab zoneid="itcfCcphpt" title="WebPro Monitoring">
<TabTitle>WebPro Monitoring</TabTitle>

1. See the instructions in [Integrating Web SDK](https://docs.byteplus.com/en/docs/apmplus/Integrate_WebPro_SDK) to integrate the SDK.

2. Add the following sample code to start the SDK and enable data collection and end\-to\-end monitoring.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">If the request is made via the "fetch" API, configuration is required on the "fetch" add\-on. If the request is made via the "xhr" API, configuration is required on the "ajax" add\-on.</div>


* <div data-tips="true" data-tips-type="default">Enabling trace will add request headers to the request. Therefore, trace is disabled by default.</div>


* <div data-tips="true" data-tips-type="default">Both sampleRate and origins must be configured simultaneously.</div>



```JavaScript
import client from '@apmplus/web'
client('init', {
 ...
  plugins: {
    ...
    fetch: {
      // If the request is made via the "fetch" API, configuration is required on the "fetch" add-on.
      trace: {
        sampleRate: 1, // Trace sampling rate. The sampling rule is based on sessions, meaning that eligible requests within a single session either all have tracing enabled or all have tracing disabled.
        origins: ['xxx'],  // The "origins" parameter is used for request URL matching. Only requests that match the specified origins will have tracing enabled.
      }
    },
    ajax: {
      // If the request is made via the "xhr" API, configuration is required on the "ajax" add-on.
      trace: {
        sampleRate: 1, // Trace sampling rate. The sampling rule is based on sessions, meaning that eligible requests within a single session either all have tracing enabled or all have tracing disabled.
        origins: ['xxx'] // The "origins" parameter is used for request URL matching. Only requests that match the specified origins will have tracing enabled.
      }
    }
  },
  ...
})
```



3. After integrating your application with the Web SDK, see the instructions at [Integrating Web SDK](https://docs.byteplus.com/en/docs/apmplus/Integrate_WebPro_SDK) to verify data reporting.


</Tab>
<Tab zoneid="DfDRY3fasB" title="Mini Pro Monitoring">
<TabTitle>Mini Pro Monitoring</TabTitle>

1. See the instructions at [Integrating Mini Pro SDK](https://docs.byteplus.com/en/docs/apmplus/Integrate_Mini_Program_Pro_SDK) to integrate the SDK.

2. Add the following sample code to start the SDK and enable data collection.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">Enabling trace will add request headers to the request. Therefore, trace is disabled by default.</div>


* <div data-tips="true" data-tips-type="default">Both sampleRate and origins must be configured simultaneously.</div>



```JavaScript
const apm = require('@apmplus/mini-program')
const client = apm.createMiniProgramClient([apm.WxAdapter])
client('init', {
 ...
  plugins: {
    ...
    http:{
      ...
      trace: {
        sampleRate: 1   // Trace sampling rate. The sampling rule is based on sessions, meaning that eligible requests within a single session either all have tracing enabled or all have tracing disabled.
        origins: ['xxx'],  // The "origins" parameter is used for request URL matching. Only requests that match the specified origins will have tracing enabled.
      }
    }
  },
  ...
})
```



3. After integrating your application with the Mini Pro SDK, see the instructions at [Integrating Mini Pro SDK](https://docs.byteplus.com/en/docs/apmplus/Integrate_Mini_Program_Pro_SDK) to verify data reporting.


</Tab>
</Tabs>


<span id="lAO4zMzD"></span>
### Step 2: Integrate the server\-side application

End\-to\-end tracing relies on the OpenTelemetry SDK that has been properly integrated with the server\-side applications. The SDK can help identify HTTP requests from App, Web, or mini program clients and convert the relevant header fields into trace attributes to be reported to the APMPlus server. Integration methods vary by language. The following integration methods for 4 languages are provided; you can choose the appropriate one based on the language used by your server\-side application.


<Tabs>
<Tab zoneid="fidTzYBzus" title="Java">
<TabTitle>Java</TabTitle>

1. To integrate a Java application via OpenTelemetry, see the detailed instructions at [Integrating Java applications](https://docs.byteplus.com/en/docs/apmplus/Java_application_integration).

2. Configure automatic injection based on different integration methods.

* If you install the apmplus\-opentelemetry\-collector add\-on via the Addons in the VKE console, automatic injection is supported by default, and no configuration changes are required.

* If you integrate via the community\-provided SDK or Agent, you need to add the following environment variables:


```Shell
OTEL_JAVA_EXPERIMENTAL_SPAN_ATTRIBUTES_COPY_FROM_BAGGAGE_INCLUDE:apmplus.app_id,apmplus.origin,apmplus.client_domain
```





</Tab>
<Tab zoneid="AyuZcbyzB6" title="Go">
<TabTitle>Go</TabTitle>

1. To integrate a Go application via OpenTelemetry, see the detailed instructions at [Integrating Go applications](https://docs.byteplus.com/en/docs/apmplus/Integrate_Go_applications).

2. See the following steps to configure automatic injection.

   1. Obtain the official "baggagecopy" package.

   ```Go
   go get "go.opentelemetry.io/contrib/processors/baggagecopy"
   ```
   

   2. When initializing the TracerProvider, add the SpanProcessor from baggagecopy.

   ```Go
   tp := trace.NewTracerProvider(
       trace.WithSpanProcessor(baggagecopy.NewSpanProcessor(nil)),
       ...
   )
   ```
   





</Tab>
<Tab zoneid="eg2CxNUCV0" title="Python">
<TabTitle>Python</TabTitle>

1. To integrate a Python application via OpenTelemetry, see the detailed instructions at [Integrating Python applications](https://docs.byteplus.com/en/docs/apmplus/Integrate_Python_applications).

2. See the following steps to configure automatic injection. For more details, also refer to [opentelemetry-processor-baggage](https://pypi.org/project/opentelemetry-processor-baggage/).

   1. Install opentelemetry\-processor\-baggage.

   ```Python
   pip install opentelemetry-processor-baggage
   ```
   

   2. Configure Tracer Provider.

   ```Python
   from opentelemetry.processor.baggage import BaggageSpanProcessor, ALLOW_ALL_BAGGAGE_KEYS
   from opentelemetry import trace
   
   # Get the global TracerProvider
   trace.get_tracer_provider().add_span_processor(BaggageSpanProcessor(ALLOW_ALL_BAGGAGE_KEYS))
   ```
   





</Tab>
<Tab zoneid="IHXA1JILuq" title="Nodejs">
<TabTitle>Nodejs</TabTitle>

1. To integrate a Node.js application via OpenTelemetry, see the detailed instructions at [Integrating Nodejs applications](https://docs.byteplus.com/en/docs/apmplus/Integrate_a_Nodejs_application).

2. Refer to the following steps to configure automatic injection. For more details, see [baggage-span-processor](https://www.npmjs.com/package/@opentelemetry/baggage-span-processor).

   1. Install opentelemetry/baggage\-span\-processor.

   ```SQL
   npm install --save @opentelemetry/baggage-span-processor
   ```
   

   2. Configure BaggageSpanProcessor.

   ```JavaScript
   import { NodeSDK, tracing } from '@opentelemetry/sdk-node';
   import { ALLOW_ALL_BAGGAGE_KEYS, BaggageSpanProcessor } from '@opentelemetry/baggage-span-processor';
   const spanProcessors = [
       new tracing.SimpleSpanProcessor(
           new tracing.ConsoleSpanExporter()),
           new BaggageSpanProcessor(ALLOW_ALL_BAGGAGE_KEYS)];
   const sdk = new NodeSDK({serviceName: "example-service",spanProcessors});
   sdk.start();
   ```
   





</Tab>
</Tabs>


<span id="NIiGmJP0"></span>
### Step 3: End\-to\-end distributed tracing


<Tabs>
<Tab zoneid="cLFamchIXg" title="App end-to-end">
<TabTitle>App end-to-end</TabTitle>

After both the client applications (e.g., Android, iOS) and server\-side applications are properly integrated, requests initiated from the clients will be sent to the server\-side applications. You can go to the Trace details page of the APMPlus console to view the spans of client app requests, and you can also jump to the App monitoring page in client monitoring to view more information.


1. Log in to the [APMPlus console](https://console.byteplus.com/observe/apmplus-server). 

2. Search for the target service, click the service name, and go to the management page of the target service.

3. In the left navigation pane, select **Trace analysis** to go to the Trace analysis page.

4. Based on your actual requirements, filter target traces by conditions such as time, tags, Span attributes, Trace ID, Span type, and service name. Click the target TraceID to go to the **Single trace details** page.

5. Click **Jump to mobile client to view** in the target app request to navigate to the app page in Client monitoring for more information.


Additionally, from the app page in Client monitoring, you can navigate back to the Trace details page of APMPlus.


1. Log in the [Client monitoring console](https://console.byteplus.com/observe/apmplus-client). 

2. Click the target application service name, and on the application management page, click **Use service** under **App monitoring** to go to the App monitoring page.

3. In the left navigation pane, select **All functions \> Network analysis \> HTTP** to go to the network overview page.

4. Select analysis metrics on the left and analysis dimensions on the right, then click **Network details** to go to the **Log search** page and view more detailed information.

5. In the details section of the Log search page, click the link under end\-to\-end Trace to jump to the server\-side **single trace query** page to view more information.


</Tab>
<Tab zoneid="Y2MPiFn6Qz" title="Web end-to-end">
<TabTitle>Web end-to-end</TabTitle>

After both the Web application and the server\-side application are properly integrated, requests initiated from the Web side will be sent to the server\-side application. You can go to the trace details page of the APMPlu console to view the Spans of Web requests, and you can also jump to the WebPro page in Client monitoring to view more information.


1. Log in to the [APMPlus console](https://console.byteplus.com/observe/apmplus-server). 

2. Search for the target service, click the service name, and go to the management page of the target service.

3. In the left navigation pane, select **Trace analysis** to go to the Trace analysis page.

4. Based on your actual requirements, filter target traces by conditions such as time, tags, Span attributes, Trace ID, Span type, and service name. Click the target TraceID to go to the **Single trace details** page.

5. Click **Jump to WebPro to view** in the target Web request to navigate to the WebPro page in Client monitoring for more information.


Additionally, from the WebPro page in Client monitoring, you can navigate back to the Trace details page of APMPlus.


1. Log in to the [Client monitoring console](https://console.byteplus.com/observe/apmplus-client). 

2. Click the target application service name, and on the application management page, click **Use service** under **WebPro Monitoring** to navigate to the WebPro Monitoring page.

3. In the left navigation pane, select **All functions \> Data explore** to go to the "Data explore" page.

4. Select a dimension, switch to the Requests tab, and click the target request name to view detailed information about the request.

5. Click rum_trace_id in the trace to jump to the Trace details page of APMPlus for more information.


</Tab>
<Tab zoneid="wayb2d0qjs" title="Mini Pro end-to-end">
<TabTitle>Mini Pro end-to-end</TabTitle>

After both the Mini Pro application and the server\-side application are properly integrated, requests initiated from the Mini Pro side will be sent to the server\-side application. You can go to the Trace details page of the APMPlus console to view the Spans of Web requests, and you can also jump to the Mini Pro page in Client monitoring to view more information.


1. Log in to the [APMPlus console](https://console.byteplus.com/observe/apmplus-server). 

2. Search for the target service, click the service name, and go to the management page of the target service.

3. In the left navigation pane, select **Trace analysis** to go to the Trace analysis page.

4. Based on your actual requirements, filter target traces by conditions such as time, tags, Span attributes, Trace ID, Span type, and service name. Click the target TraceID to go to the **Single trace details** page.

5. Click **Jump to Mini Pro to view** in the target Mini Pro request to navigate to the Mini Pro page in Client monitoring for more information.


Additionally, from the Mini Pro page in Client monitoring, you can navigate back to the Trace details page of APMPlus.


1. Log in to the [Client monitoring console](https://console.byteplus.com/observe/apmplus-client). 

2. Click the target application service name, and on the application management page, click **Use service** under **Mini Pro Monitoring** to navigate to the WebPro Monitoring page.

3. In the left navigation pane, select **All functions \> Data explore** to go to the "Data explore" page.

4. Select a dimension, switch to the HTTP tab, and click the target request name to view detailed information about the request.

5. Click the TraceID in the trace to jump to the Trace details page in APMPlus for more information.


</Tab>
</Tabs>
