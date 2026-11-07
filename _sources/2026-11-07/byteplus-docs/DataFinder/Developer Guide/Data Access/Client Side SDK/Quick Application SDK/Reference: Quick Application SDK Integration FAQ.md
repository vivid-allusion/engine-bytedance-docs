---
title: "Reference: Quick Application SDK Integration FAQ"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Reference_Quick_Application_SDK_Integration_FAQ"
---

<span id="da29c0eb"></span>
# SDK integration

<span id="df17a2c3"></span>
## Can the Fast App SDK delay event reporting? I want all reported events to carry information obtained from the interface. What should I do?

Answer: You can control when the send method is called. For example, the scenario is to wait for the user interface request to complete, obtain the user's nickname and set it to the SDK as the event public attribute, and then hope that all events of the SDK can carry this user's nickname, then the practice is to set it to the SDK public attribute and then call the send method.

```TypeScript
//similar to the following processing

//SDK initialization
$$sdk.init(/**/) 

//Request the user interface somewhere to get the information
fetch('用户接口').then((user) => { //user interface
    $$sdk.config({
        'nickname': user.nickname，
    })
    //call send after config
    $$sdk.send()
});
```


Note: Send is used to control when the SDK starts reporting events, but if you don't call send, the SDK will not report events, so you must ensure that send is called.

<span id="9fac904b"></span>
# Abnormal reported data

<span id="bb4f2561"></span>
## Does the SDK automatically report predefine_pageview? No event tracking report predefine_pageview received.

Answer: Not by default. If you want to automatically report predefine_pageview events, you need to enable auto_report parameters during initialization.

<span id="436c71d1"></span>
# More FAQ

See the FAQ for more information on data access [SDK Integration & Data Reporting](https://docs.byteplus.com/docs/DataFinder/SDK_Integration_Data_Reporting).
