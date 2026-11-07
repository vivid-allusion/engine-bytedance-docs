---
title: "Compilation failed: Unable to build the Alibaba Sophix hotfix package"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Unable_to_build_the_Alibaba_Sophix_hotfix_package"
---

**Problem description**

To enable the collection of application start data, the APMInsight SDK instruments the attachBaseContext() and onCreate() methods of the Application class at compile time. However, the Alibaba Hotfix patch tool requires that the Application must not call non\-official Android APIs, which results in patch generation failure.

**Solutions**

Analysis:


1. Why is instrumentation being inserted into Alibaba's classes?

   1. Ali Hotfix: Ali Hotfix uses its own SophixStubApplication to proxy the business Application class. When monitoring is started, instrumentation is inserted into the actual Application, which results in modifications to the code of the SophixStubApplication class.

2. How to avoid instrumenting Alibaba's classes Can start monitoring be implemented as well?

   1. Configure the blocklist for the Ali SophixStubApplication class and your own application.

   2. Manually add code for starting monitoring to your own application.


Plugin configuration:

If you use Alibaba's Sophix hotfix, the following configuration is required.

```Plain Text
ApmPlugin{
    blackList = [
        "com.apm.app.SophixStubApplication",// Alibaba Hotfix's Application
        "com.apm.app.MyApp"// Your own Application
    ]
}
```


Start the application configuration:

Configure the code that starts monitoring in your own application.

```Plain Text
public class App extends Application {

    public App(){
        super();
        // Monitor the App constructor
        AppAgent.onTrace(AppAgent.CONSTRUCT,true);
        AppAgent.onTrace(AppAgent.CONSTRUCT,false);
    }

    @Override
    protected void attachBaseContext(Context base) {
        // Monitor the startup attachBaseContext() method
        AppAgent.onTrace(AppAgent.ATTACH_BASE_CONTEXT,true);
        super.attachBaseContext(base);
        AppAgent.onTrace(AppAgent.ATTACH_BASE_CONTEXT,false);
    }

    @Override
    public void onCreate() {
        // Monitor the startup onCreate() method
        AppAgent.onTrace(AppAgent.ON_CREATE,true);
        super.onCreate();
        
        // Other business code can be initialized here.
        
        AppAgent.onTrace(AppAgent.ON_CREATE,false);
    }
}

```


If the constant AppAgent cannot be found. *CONSTRUCT* can be configured

```Plain Text
public static final String CONSTRUCT = "<init>";
public static final String ATTACH_BASE_CONTEXT = "attachBaseContext";
public static final String ON_CREATE = "onCreate";

```


Verification:

Added blocklist and added code to start monitoring.

During initialization, set debug mode. Then, filter ApmInsight. You will see "Receive:StartData", which indicates that the start data has been successfully obtained.
