---
title: "Reference: Mini Program SDK Integration FAQ"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Reference_Mini_Program_SDK_Integration_FAQ"
---

<span id="da29c0eb"></span>
# SDK integration

<span id="df17a2c3"></span>
## Can the Mini Program SDK turn off preset event collection?

A: Yes, setting the "auto_report" parameter to false at initialization closes the collection of preset events, including application launch, application exit, page access, Mini Program sharing and other related preset events.

<span id="436e8fe5"></span>
## How does Mini Program use full event tracking preset events and properties?

Answer: The Mini Program side supports the collection of click events \- "bav2b_click" events. This event is similar to the event name of the full event tracking event on other ends, but there are some differences in the actual integration operation. When collecting click events:


* Turn on the click event collection switch: By default, the click event collection switch is off, you need to set the value of the auto_report of init to the value of the object type during initialization, and the click field in the object is set to true, that is: `click: true`.

* Configure click event data collection: Unlike the full event tracking events of other terminals, when the Mini Program terminal collects click events, you need to configure specific collection attribute details in the SDK integration code, support filtering which attributes in the dataset of the clicked element are not collected, and also support clearly specifying which attributes in the dataset of the clicked element need to be collected. See configuration points [capture click events](https://docs.byteplus.com/docs/DataFinder/Mini_Program_SDK_Integration_Scenario_Practice#932b065c).


<span id="032d46d2"></span>
## What platforms does the Mini Program SDK support for full event tracking (bav2b_click)?

Answer: Currently supports WeChat Mini Program, Alipay Mini Program, Douyin Mini Program and other platforms.

<span id="5a6435db"></span>
## Mini Program SDK component click report bav2b_click event how to distinguish?

Answer: Set the id on the component. The value set by the id can distinguish the clicked view, and you can also add custom attributes: format data\-xxx, multiple can be added, and bindtap must be set to take effect.

<span id="a201c59f"></span>
## Is the Mini Program SDK instance globally unique?

Answer: Default exported instances are globally unique. But if you subcontract or build something special, it may not be the same. It is recommended to mount the default instance of the SDK on the global object, and then call the corresponding method after obtaining the default instance through the global object during use.

<span id="ac5f9f25"></span>
## The integration of SDK in Mini Program subcontracting, data reporting problems?

Answer: How to integrate the SDK in the Mini Program subcontract, you can refer to the "Using in the Mini Program Subcontract" section of the "SDK Integration Scenario Practices" document.

<span id="06a1a41a"></span>
## Mini Program, if the customer does not buy advertisements and wants to use the url to carry the utm parameter, will the utm parameter sdk be collected in this case?

Answer: By default, the Mini Program SDK attempts to obtain UTM\-related parameters from the applet startup parameters: utm_source, utm_medium, utm_campaign, utm_term, utm_content. If obtained, these parameters are placed in the event public property, and will be carried on all subsequent event reports. The ability is automatically turned on, and the business does not require any processing.

<span id="4a75690f"></span>
## What are the triggers for on_share and on_addtofavorites in WeChat Mini Program? How can these methods be implemented?

A: on_share and on_addtofavorites are preset events for the Mini Program itself, and triggering these events requires the client's Mini Program project itself to implement. For example, to implement the life cycle methods of onShareAppMessage and onAddToFavorites, you can check the official documentation of the Mini Program platform about the life cycle of the Page.

<span id="200a5138"></span>
## Mini Program web_id request logic?

Answer: web_id will initiate a webid request to the server (https://xxxx/webid) when the sdk is initialized and the init method is called.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6bdd0b891fc4484c94e87fc8bc4e5840~tplv-goo7wpa0wc-image.image) </span>

The request parameters are: app_id, the current URL, the referer of the URL, the useragent of the current browser, and user_unique_id (usually null), which mainly depends on the appid and the current environment. The request will generate a unique webid return at the server level, as shown below:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4952a34924c545a1bb20acdee056e1e3~tplv-goo7wpa0wc-image.image) </span>

After getting the web_id, it will be cached locally. As long as the appid and domain name remain unchanged, the cache will not be manually cleared, and the server will no longer be requested to obtain web_id.

<span id="dcf32383"></span>
## Mini Program SDK preset attribute $current_path value logic?

Answer: The preset attribute $current_path is the path to the current page that the SDK fetches during the page's onShow lifetime.

<span id="89a77987"></span>
## How does the Mini Program SDK enable buffering (batch request reporting)?

Answer: By enable_buffer parameters to open the buffer, the default 5 seconds 5, can be modified by buffer_interval and buffer_number, it is recommended not to be too large.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/86a7008d267c4fa8a5fbdfb503df748c~tplv-goo7wpa0wc-image.image) </span>

<span id="f6096b6e"></span>
## Does the Mini Program SDK support batch reporting? How to use buffering and caching?

Answer: The Mini Program SDK defaults to real\-time reporting, enabling enable_buffer supports buffering and enabling enable_cache supports caching.

When buffering is enabled, the SDK will combine multiple events into a single request report, which can achieve the goal of batch reporting. buffer_interval used to control the buffer interval, buffer_number to control the number of buffers:


* buffer_interval: Default 5 seconds, can be adjusted

* buffer_number: Default 5, can be adjusted


For more parameter details, please refer to the description of init in the "SDK API Description" documentation.

<span id="db420286"></span>
## How is the data uploaded in the Mini Program SDK without a network?

Answer: The Mini Program SDK does not actively monitor network changes. When there is no network, the report request will theoretically fail. At this time, according to whether the enable_cache parameter is turned on (starting from the 2.14.3 version, this parameter is turned on by default), there are the following corresponding processing:


* When this parameter is enabled, the event (failed request) will be cached into the storage, and after waiting for the next SDK to perform initialization, it will try to check whether there are cached events from the storage, and if so, make supplementary reports.

* When this parameter is not enabled, the request fails without any processing.


Note: The storage in the Mini Program has a size limit, and the event will be thrown when the limit is exceeded.

Scenario example:

When the Mini Program is currently running, there is no network at this time, and then suddenly there is a network, then the follow\-up behavior is reported normally, and those that have existed in the storage before will not be transmitted now. Only after the Mini Program is re\-initialized will the step of going to the storage to see if there is any.

<span id="f04e9652"></span>
## Can the Mini Program SDK delay event reporting? I want all reported events to carry information obtained from the interface. What should I do?

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
# abnormal reported data

<span id="bb4f2561"></span>
## Mini Program from anonymous to real name, during the period did not quit Mini Program, but why there is an exit event (app_terminate event)?

Answer: The Mini Program SDK will anonymously report app_terminate event when the real name is switched (essentially the user_unique_id is reset), which is the internal processing logic of the SDK.

<span id="573e50fa"></span>
## Why can't WeChat Mini Program SDK collect this collection/sharing event?

A: The mechanism of Mini Program requires the implementation of corresponding event handlers in the customer project to generate corresponding interaction capabilities, and the SDK can also trigger relevant event reports. For details, please refer to the description and implementation in the official documentation of the Mini Program platform：[Page](https://developers.weixin.qq.com/miniprogram/en/dev/reference/api/Page.html).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ad6e5dc46a9d40dc96648e997edd3afe~tplv-goo7wpa0wc-image.image) </span>

<span id="641d4be0"></span>
## In the Mini Program preset sharing event, what is the reason why the title cannot be obtained when sharing after jumping to an external link?

Answer: The possible reason is that onShareAppMessage defines promises (using promises to return asynchronously), and the SDK does not currently support obtaining sharing\-related information in this asynchronous scenario.

<span id="247075c1"></span>
## Mini Program integrates GrowingIO (gio) and Finder SDK. Finder does not request to report data. How to check?

Answer: You need to import the gio sdk first, and after the gio sdk is initialized, import the finder sdk, and then initialize the finder sdk (init call).

<span id="dd0710ed"></span>
## Does the Mini Program SDK automatically report predefine_pageview? No event tracking report predefine_pageview received.

Answer: Not by default. If you want to automatically report predefine_pageview events, you need to enable auto_report parameters during initialization.

<span id="436c71d1"></span>
# More FAQ

See the FAQ for more information on data access [SDK Integration & Data Reporting](https://docs.byteplus.com/docs/DataFinder/SDK_Integration_Data_Reporting).
