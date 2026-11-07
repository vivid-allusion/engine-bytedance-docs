---
title: "How to integrate monitoring capability based on a non-instrumentation approach?"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/How_to_integrate_monitoring_capability_based_on_a_non-instrumentation_approach"
---

To simplify the integration of certain monitoring capabilities and enable non\-intrusive integration, initialization code for application startup and network monitoring can be inserted by default using the Apm Plugin instrumentation method.

If a conflict between the instrumentation plugin and the host environment causes compilation to fail, you should preferably integrate this monitoring capability using a non\-instrumentation method.

<span id="9813f15b"></span>
## Prerequisites

Annotate the following code:

```Nginx
apply plugin: 'apm-plugin'

ApmPlugin {
}

classpath "com.volcengine:apm_insight_plugin:1.4.1"
```


<span id="4959ec33"></span>
## Integrate network monitoring

<span id="9381622d"></span>
### Integrate examples

By calling the `OkHttp3Instrumentation.build()` method to create an OkHttpClient instance, you can automatically monitor OkHttp network requests.

```Plain
OkHttpClient.Builder builder = new OkHttpClient.Builder();
// Simply call the OkHttp3Instrumentation method to generate an OkHttpClient, and the network requests of OkHttp will be automatically monitored.
OkHttpClient okHttpClient = OkHttp3Instrumentation.build(builder);
```


<span id="c6817a46"></span>
### Data validation

Initialize and set debug mode. By filtering ApmInsight, you can see `Receive:NetData`, which means that network monitoring data has been successfully obtained in non\-instrumented mode.

```Apache
2021-09-17 21:18:20.031 8698-9358/com.example.apm.insight.demo D/ApmInsight: Receive:NetData
```


<span id="6028e0a1"></span>
## Integrate the start monitoring feature

<span id="4a3b8de7"></span>
### An integration example

Configure the code to start Monitoring in the Application:

```TypeScript
public class App extends Application {

    public App(){
        super();
        // Turn on the page monitoring switch
        InstructOperationSwitch.sPageLoadSwitch=true;
        // Monitoring app constructor
        AppAgent.onTrace(AppAgent.CONSTRUCT,true);
        AppAgent.onTrace(AppAgent.CONSTRUCT,false);
    }

    @Override
    protected void attachBaseContext(Context base) {
        //Monitoring the start of the attachBaseContext() method
        AppAgent.onTrace(AppAgent.ATTACH_BASE_CONTEXT,true);
        super.attachBaseContext(base);
        AppAgent.onTrace(AppAgent.ATTACH_BASE_CONTEXT,false);
    }

    @Override
    public void onCreate() {
        // Monitoring the start of the onCreate() method
        AppAgent.onTrace(AppAgent.ON_CREATE,true);
        super.onCreate();
        
        // You can initialize other business code here
        AppAgent.onTrace(AppAgent.ON_CREATE,false);
    }
}
```


If the constant `AppAgent.CONSTRUCT` cannot be found, you can configure:

```PHP
public static final String CONSTRUCT = "<init>";
public static final String ATTACH_BASE_CONTEXT = "attachBaseContext";
public static final String ON_CREATE = "onCreate";
```


Add the following code to register a listener during Application initialization:

Caution: The following registerActivityLifecycleCallbacks method should be registered only once.

```TypeScript
app.registerActivityLifecycleCallbacks(new ActivityLifecycleCallbacks() {

    @Override
    public void onActivityCreated(@NonNull Activity activity, @Nullable Bundle savedInstanceState) {
        ActivityAgent.onTrace(activity.getLocalClassName(), "onCreate", true);
        ActivityAgent.onTrace(activity.getLocalClassName(), "onCreate", false);
    }

    @Override
    public void onActivityStarted(@NonNull Activity activity) {
        ActivityAgent.onTrace(activity.getLocalClassName(), "onStart", true);
        ActivityAgent.onTrace(activity.getLocalClassName(), "onStart", false);
    }

    @Override
    public void onActivityResumed(@NonNull Activity activity) {
        ActivityAgent.onTrace(activity.getLocalClassName(), "onResume", true);
        ActivityAgent.onTrace(activity.getLocalClassName(), "onResume", false);
        ActivityAgent.onTrace(activity.getLocalClassName(), "onWindowFocusChanged", true);
    }
    

    @Override
    public void onActivityPaused(@NonNull Activity activity) {

    }

    @Override
    public void onActivityStopped(@NonNull Activity activity) {

    }

    @Override
    public void onActivitySaveInstanceState(@NonNull Activity activity, @NonNull Bundle outState) {

    }

    @Override
    public void onActivityDestroyed(@NonNull Activity activity) {

    }
});
```


<span id="965f4f02"></span>
### Data validation

Initialize settings for debug mode. After filtering ApmInsight, you can see `Receive:StartData`, which indicates that start data was successfully obtained in non\-instrumentation mode.

```Apache
2021-09-17 21:15:07.351 8698-8781/com.example.apm.insight.demo D/ApmInsight: Receive:StartData
2021-09-17 21:15:08.714 8698-8781/com.example.apm.insight.demo D/ApmInsight: Receive:PageData
```
