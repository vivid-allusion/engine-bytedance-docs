---
title: "Web/JS SDK Classification Function"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Web_JS_SDK_Classification_Function"
---

<span id="_1-web-js-停留时长功能"></span>
# 1. Web/JS Duration Function

<span id="_1-1-停留时长介绍"></span>
## 1.1 Introduction to the length of stay

The time spent on a page (browsing) is a very common indicator in website analysis, used to reflect the length of time users spend browsing certain pages, reflecting the stickiness of users to a website.

<span id="_1-2-功能开启"></span>
## 1.2 Function enabled

Please refer to [Web/JavaScript SDK Integration](https://docs.byteplus.com/docs/DataFinder/Web_JavaScript_SDK_Integration_)the access SDK first, and turn on the dwell time function during initialization.

```javascript
window.collectEvent('init', {
    // ...... Other initialization configurations
    enable_stay_duration: true //true: turn on stay duration
});
```


<span id="_1-3-上报事件介绍"></span>
## 1.3 Introduction to the reported incident

<span id="_1-3-1-predefine-page-alive"></span>
### 1.3.1 predefine_page_alive

When the function is turned on, predefine_page_alive event will be reported regularly every minute when the page is active, or once when it is switched to inactive.

**Active state: The page is in a visual or actionable state.** 

**Inactive state: The page is in the background, hidden, minimized, and other invisible states.** 

Event reporting parameters:


|**Parameter** |**Explain** |
|---|---|
|title |String, page title |
|url |String, page address |
|url_path |String, page path |
|duration |Number, milliseconds, normal is 60000, less than or equal to 60000 when switching state |


<span id="_1-3-2-predefine-page-close"></span>
### 1.3.2 predefine_page_close

After the function is turned on, the timestamp of each time the user [enters the page, switches the state, leaves the page] will be recorded, and then the predefine_page_close event will be reported when leaving or closing the page, and the duration of each [active state] will be added as the overall usage duration.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">In the H5 scenario in the App, predefine_page_close events may not be reported normally. If you need to analyze the length of stay, you can consider based on predefine_page_alive events. For details on how to analyze the length of stay, please refer to the following <code>1.6 analysis methods</code>.</div>



|**Parameter** |**Explain** |
|---|---|
|title |String, page title |
|url |String, page url |
|url_path |String, path to page url |
|duration |Number, ms, sum of the length of time the user stayed active |
|active_times |Number, the number of times a user is active, defaults to 1 |
|total_duration |Number, the total time the user visited the page, from start to close |


<span id="_1-4-重置时长"></span>
## 1.4 Reset time

When your page is a single\-page application, click the tab on the page to access other pages, you need to reset the dwell time.

```javascript
window.collectEvent('resetStayDuration', url_path?: string, title?: string, url?: string);
//Parameters can not be passed, if not passed, take the default value of the current page
```


**Note: The meaning of this API is to reset the dwell duration. Suppose you initially visit page A, and then click the button on the page to visit page B. You can call this API and pass in the relevant parameters of page B. Calling this API immediately initiates the alive and close events (the content of the event is the parameters of the A page and the length of time you have visited the A page). The duration of the B page will not be reported until the B page is closed, or you call the API again (you will visit page C).** 

<span id="_1-5-自动重置时长"></span>
## 1.5 Automatic reset time

When the route changes, the dwell time is automatically reset, that is, the SDK will automatically call resetStayDuration)

```TypeScript
window.collectEvent('init', {
   spa: true
});
```


If you feel that the parameters obtained by alive or close event tracking when the dwell duration is automatically reset are inaccurate, or you want to control this behavior yourself, you can turn off automatic route monitoring through the settings below.

```javascript
window.collectEvent('init', {
   disable_route_report: true
});
```


Or fix the parameter issue by calling the following API every time you enter a new page.

```TypeScript
window.collectEvent('resetStayParams', url_path?: string, title?: string, url?: string);
```


<span id="aed7b7a5"></span>
## 1.6 Analysis methods

Select `predefine_page_alive`event on DataFinder (page active event)


* Average screen time: Select `the average length of stay (SUM/UV)`

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/364e6bdaff2b4d77b2bca93a40474aba~tplv-goo7wpa0wc-image.image) </span>

* Average use time: select `Average by stay time (SUM/PV)`

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/80a88750155549de8bde6560f97e0bc9~tplv-goo7wpa0wc-image.image) </span>


<span id="_1-6-验证埋点"></span>
## 1.7 Validation event tracking

Since most of the time, it will be triggered when the page leaves or closes, so the SDK uses the sendBeacon api to send this request. You need to select the ALL category in the network category of the browser console to view it (type is ping, xhr for abnormal requests).

<span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_ec9099a90bc5d25381ae4c74c3218326) </span>

<span id="_2-web-js-全埋点"></span>
# 2. Web/JavaScript event tracking

<span id="_2-1-全埋点介绍"></span>
## 2.1 Introduction to full event tracking

In comparison to custom event tracking, full event tracking can automatically monitor user visits, clicks, and other behaviors, and then automatically report relevant event tracking.

<span id="_2-2-设置代码"></span>
## 2.2 Setting up the code

Please refer to [Web/JavaScript SDK Integration](https://docs.byteplus.com/docs/DataFinder/Web_JavaScript_SDK_Integration_)the access SDK first, and turn on full event tracking during initialization

```javascript
window.collectEvent('init', {
    // ...... Other initialization configurations
    autotrack: true
});
```


<span id="_2-3-配置说明"></span>
## 2.3 Configuration Instructions

`In addition`to setting the boolean type, autotrack also supports object passing.


|**Autotrack built\-in object** |**Explain** |
|---|---|
|text |Boolean, whether to collect the text of the element, the default collection |
|svg |Boolean, whether to collect svg elements, not by default |
|track_attr |[String], string array, configure the properties customized by clicking on the element |
|collect_url |Function, function, configure whether to collect a certain page, return the element click event that will really collect the current page, and return false to indicate that the current page is not collected. After setting this function, if the content is empty, it will return false. If the function is not set, the default is to collect all pages. |
|pv |Whether to enable pv reporting of full event tracking, the default is true, false is disabled |
|click |Whether to enable click reporting of full event tracking, the default is true, false is disabled |
|beat |Whether to turn on full event tracking scrolling heartbeat reporting, the default is true, false is disabled |
|exposure |Any, exposure event collection, the default is false, if you pass true, you will start exposure event collection. For details, please refer to the detailed description below. |


<span id="_2-3-1-配置示例"></span>
### 2.3.1 configuration example

```javascript
window.collectEvent('init', {
    autotrack: {
      text: false, //do not collect element text
      svg: true, //capture svg elements
      track_attr: ['attr1', 'attr2'],
      collect_url: () => {
        if (location.href === 'xxx') {
           //If the page address is xxx, it will not be collected.
           return false
        }
        //Other page collection
        return true
      }
    }
})
window.collectEvent('start')
```


<span id="_2-3-2-设置自定义属性"></span>
### 2.3.2 set custom properties


1. Custom attribute method 1


After turning on full event tracking, support the collection of custom attributes. The code is as follows:

```javascript
window.collectEvent('init', {
    autotrack: {
       track_attr: ['attr1', 'attr2']
    }
})
```


```javascript
<div attr1='ss'  attr2='ddd'></div>
//The SDK will collect the attributes and attribute values of att1 and attr2
```



2. Custom attribute method 2


```TypeScript
window.collectEvent('init', {
   autotrack: {
     custom_attr: 'datastring'
   }
})
```


```TypeScript
<div id="test" datastring="%7B%22id%22%3A2%2C%22name%22%3A3%7D">测试属性采集</div> //test property collection
```


```TypeScript
the raw value of datastring is
{
  id:2,
  name:3
}

Filled on dom byencodeURIComponent(JSON.stringify({id:2, name:3}))
```


<span id="_2-3-3-设置页面采集"></span>
### 2.3.3 settings page capture

After turning on full event tracking, support setting which pages need to be collected and which pages do not need to be collected

```javascript
window.collectEvent('init', {
    autotrack: {
      collect_url: () => {
        if (location.href === 'xxx') {
           //If the page address is xxx, it will not be collected.
           return false
        }
        //Other page collection
        return true
      }
    }
})
```


<span id="_2-3-4-设置元素采集"></span>
### 2.3.4 Set Element Collection

If an element itself cannot be captured, you can set attributes for the SDK to capture

```javascript
<div data-tea-container="true"></div>
```


<span id="_2-3-5-设置元素不采集"></span>
### 2.3.5 set elements do not collect

If an element does not need to be collected, you can set attributes for SDK filtering

```javascript
<div data-tea-ignore="true"></div>
```


<span id="_2-3-5-设置曝光采集"></span>
### 2.3.5 Set Exposure Acquisition

```javascript
window.collectEvent('init', {
    autotrack: {
      exposure: true You can also pass in an object
      exposure: {
        radio: 0.5 //Element exposure ratio, 0-1, default 0.5, that is, exposure when the element display area exceeds 50%
        eventName: '' //You can customize the reported exposure event name, the default is bav2b_exposure
      }
    }
})
```


An element is exposed only if it contains the data\-exposure attribute.

<span id="_2-4-全埋点事件"></span>
## 2.4 Full event tracking events

<span id="108545e2"></span>
### Preset event list and reporting logic


|Full event tracking event list |Event description |Event triggering mechanism |
|---|---|---|
|bav2b_page |page view event |Trigger the report after the page is opened |
|bav2b_click |element click event |Trigger a report after clicking on a page element |
|bav2b_page_statistics |page access event |Trigger the report after the page is opened |
|bav2b_beat |page heartbeat event |The report will be triggered after 500ms after the page is opened, closed, or the page scrolling stops. |
|bav2b_exposure |element exposure event |The appearance of elements that need to be exposed in the visible area will trigger a report |


See below for a detailed description of each preset event and the associated event properties.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Of which:</div>



* <div data-tips="true" data-tips-type="warning"><strong>Page duration related properties (refer_page_duration_ms)</strong> is to record the length of stay on a page, you need to rely on the user has turned on <strong>Dwell duration function (</strong> enable_stay_duration: true, please refer to the above Dwell duration function section for details <strong>)</strong> , the user starts timing after opening the page, during the cut background, cut tab and other operations will suspend timing, and when the visit ends and jumps to the next page, the current accumulated time will be temporarily stored. Wait until the next page to get this length as the value of the refer_page_duration_ms.</div>


* <div data-tips="true" data-tips-type="warning">After completing the data report, if the attribute value of the refer_page type is empty, it may be because you did not turn on the dwell time function; or this value is not fetched in the cache (that is, the previous page was not successfully temporarily stored); where refer_page_key is the URL of the previous page, which is empty also means that the referrer of the page is a direct visit, so the refer_page_key is empty.</div>



<span id="_2-4-1-bav2b-page"></span>
### 2.4.1 bav2b_page

Page view events are reported when a page is opened or when routing changes. The reporting time is divided into independent pages and SPAs (single\-page applications). For independent pages, it will be reported once after the page is opened and the SDK initialization is completed. If it is a SPA page, it will be reported once after the SDK initialization is completed, and once when clicking to switch the page. The main data collected are some parameters of page browsing, which are used to analyze page browsing behavior.

<span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_bb4533a0481c26753f5a22ff06206870) </span>


|**Parameter** |**Explain** |
|---|---|
|is_html |Default is 1. |
|is_back |Whether backwards are generated |
|page_key |The current page key, the default value is the page address |
|url |Current page address |
|page_title |page title |
|page_path |page path |
|page_host |Page hosting |
|page_total_height |total page height |
|page_total_width |total page width |
|scroll_height |page scroll bar height |
|scroll_width |page scrollbar width |
|page_manual_key |Page manual_key, the current page manual_key is an idle field, no practical significance, you don't need to pay attention |
|page_start_ms |page opening time |
|refer_page_title |Previous page title |
|refer_page_duration_ms |Last page visit time |
|refer_page_key |Previous page key |
|refer_page_manual_key |The previous page manual_key, the current page manual_key is an idle field, no practical significance, you don't need to pay attention |
|is_first_time |Whether to visit for the first time |


<span id="_2-4-2-bav2b-click"></span>
### 2.4.2 bav2b_click

Element click events are reported when a page click occurs.

<span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_4f1a5de5dbc5fa2d30c1e3bb23f487ce) </span>


|**Parameter** |**Explain** |
|---|---|
|is_html |Default is 1. |
|page_key |The current page key, the default value is the page address |
|page_title |page title |
|element_path |element path |
|positions |element position |
|element_title |element title |
|element_id |Element ID |
|element_class_name |Element class name |
|element_type |element type |
|element_width |element width |
|element_height |element height |
|touch_x |Click position X coordinate |
|touch_y |Click position Y coordinate |
|page_start_ms |page opening time |
|since_page_start_ms |The time since the page opened when the click occurred |
|page_path |page title |
|page_host |Page hosting |


<span id="_2-4-3-bav2b-page-statistics"></span>
### 2.4.3 bav2b_page_statistics

Page access events are reported when the page is accessed. After the page is opened, it is reported once after the SDK initialization is completed (both the independent page and the SPA are reported only once). The data collected is mainly statistical information on page loading time and page width, which is used to analyze page loading statistics and other information.

<span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_76edd8b2282e7a3a749d23c8332a3df0) </span>


|**Parameter** |**Explain** |
|---|---|
|is_html |Default is 1. |
|page_key |The current page key, the default value is the page address |
|page_title |page title |
|page_manual_key |Page manual_key, the current page manual_key is an idle field, no practical significance, you don't need to pay attention |
|page_start_ms |page opening time |
|page_init_cost_ms |Time spent on page opening |
|refer_page_key |Previous page key |
|refer_page_manual_key |The previous page manual_key, the current page manual_key is an idle field, no practical significance, you don't need to pay attention |


<span id="_2-4-4-bav2b-beat"></span>
### 2.4.4 bav2b_beat

The page heartbeat event is accessed on the page, stopped for 500ms after scrolling the page, and reported once when leaving the page.

<span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_a774d3073abf9754c76361692f03fde9) </span>


|**Parameter** |**Explain** |
|---|---|
|is_html |Default is 1. |
|page_key |The current page key, the default value is the page address |
|beat_type |Beat type, 0: leave page, 1: scroll stop, 3: visit page |
|page_title |page title |
|page_viewport_width |Page visual window width |
|page_viewport_height |Page viewable window height |
|page_total_height |total page height |
|page_total_width |total page width |
|scroll_height |page scroll bar height |
|scroll_width |page scrollbar width |
|page_manual_key |Page manual_key, the current page manual_key is an idle field, no practical significance, you don't need to pay attention |
|page_start_ms |page opening time |
|since_page_start_ms |The time from the time the page was opened when the event occurred |


<span id="_2-4-5-bav2b-exposure"></span>
### 2.4.5 bav2b_exposure

<span id="v5-1-1以上版本支持。"></span>
#### V5.1.1 and above are supported.

An element exposure event is reported when an element scrolls into the visible area and meets the exposure ratio. Repeated scrolling in the visible area will only be counted once, and will not be exposed again until it is removed from the visible area and then scrolled.

<span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_874a8e461639f3b7f1864c8e9960fdfe.png) </span>


|**Parameter** |**Explain** |
|---|---|
|is_html |Default is 1. |
|page_key |The current page key, the default value is the page address |
|page_title |page title |
|element_path |element path |
|positions |element position |
|element_title |element title |
|element_id |Element ID |
|element_class_name |Element class name |
|element_type |element type |
|element_width |element width |
|element_height |element height |
|touch_x |Click position X coordinate |
|touch_y |Click position Y coordinate |
|page_start_ms |page opening time |
|since_page_start_ms |The time since the page opened when the click occurred |
|page_path |page title |
|page_host |Page hosting |


<span id="_2-5-全埋点采集元素过滤规则"></span>
## 2.5 Full event tracking element filtering rules


|**Element type** |**Whether to collect** |
|---|---|
|HTML, header, body, footer, script, link, ifram, svg etc |Do not collect |
|Div, span, a, p, img, ul, li, etc |acquisition |
|element nodeType is not equal to 1 (non\-visual element tags) |Do not collect |
|Displayed as none |Do not collect |
|The clicked element has more than 2 layers (with multiple layers of child elements). |Do not collect |
|When the element level exceeds 2 layers, but the element is a container element (a, button, or user\-specified label attribute'teaContainer ',' data\-tea\-container ') |acquisition |


<span id="_2-6-产品功能开启"></span>
## 2.6 Product function is enabled

After enabling full event tracking in the SDK, you need to check and confirm that the switch of full event tracking is turned on in the DataFinder console before actual use.

<span id="b26e9737"></span>
## 2.7 Exposure event tracking using detailed examples


1. Integrate the web JavaScript SDK.

2. Enable exposure event tracking.

   ```JavaScript
   window.collectEvent('init', {
      autotrack: {
         exposure: {
           ratio: 0.4 , //0-1 exposure ratio
           stay: 500 //Report when the stay time of unit ms reaches 500ms
           //Only one of the above two conditions can be set. If both are set, it needs to be met at the same time before reporting.
           callback: (data) => {
            //You can modify the data, data is the property of the exposure report
             return data
           }
         }
      }
   })
   ```
   

3. Set the element to be exposed

   ```HTML
   <div data-exposure>我是需要曝光的元素</div> //I am element need to be exposed
   ```
   

4. Set functions that modify properties

   ```JavaScript
   window.collectEvent('init', {
      autotrack: {
         exposure: {
           callback: (data) => {
            //You can modify the data, data is the attribute of the exposure report, and you can also add
             data.element_class_name = 'sijie'
             return data
           }
         }
      }
   })
   
   there is another general method, where elements with attr1 and attr2 attributes are also collected
   window.collectEvent('init', {
      autotrack: {
         track_attr: ['attr1', 'attr2']
      }
   })
   
   <div attr1='ss'  attr2='ddd'></div>
   ```
   

5. Custom event name

   Exposure event name Default: $bav2b_exposure custom event name There are 2 ways:

   * effective globally

      ```HTML
      window.collectEvent('init', {
         autotrack: {
            exposure: {
              eventName: 'customexposure'
            }
         }
      })
      ```
      

   * Binding elements take effect

      ```HTML
      // report custom event customexposure
      <div data-exposure data-exposure-event="customexposure"></div>
      ```
      

6. exposure_type properties in detail

   * $exposure_type: 0 first exposure

   * $exposure_type: 3 duplicate exposures

   * $exposure_type: 6 Exposure returned from other pages

   * $exposure_type: 7 Background Return Exposure


<span id="b7188c63"></span>
## 2.8 Slide event tracking usage detailed example


1. Integrate the web JavaScript SDK.

2. Enables sliding event tracking.

   ```JavaScript
   window.collectEvent('init', {
      autotrack: {
         scroll: {
           distance: 200 //It will not be reported until the continuous sliding distance exceeds 200px. Sliding and stopping does not count.
           callback: (data) => {
            //You can modify the data, data is the property reported by sliding
             return data
           }
         }
      }
   })
   
   <div id="test" data-scroll='true'></div>
   ```
   

3. Sets the element that needs to report sliding event tracking.

   ```JavaScript
   window.collectEvent('init', {
      autotrack: {
         scroll: {
           callback: (data) => {
            //You can modify the data. Data is an attribute reported by sliding, and you can also add new ones.
             data.element_class_name = 'sijie'
             return data
           }
         }
      }
   })
   
   there is another general method, where elements with attr1 and attr2 attributes are also collected
   window.collectEvent('init', {
      autotrack: {
         track_attr: ['attr1', 'attr2']
      }
   })
   
   <div attr1='ss'  attr2='ddd'></div>
   ```
   

4. Exposure event name Default: $bav2b_slide custom event name There are 2 ways

* effective globally

   ```JavaScript
   window.collectEvent('init', {
      autotrack: {
         scroll: {
           eventName: 'customscroll'
         }
      }
   })
   ```
   

* Binding elements take effect

   ```JavaScript
   //Report custom event customscroll
   <div id="test" data-scroll data-scroll-event="customscroll" style="width:200px;height:200px;">
     <div style="width:2000px;height:200p0x;">我才是真正滑动的元素</div> // I am the true slide element
   </div>
   ```
   

5. Slide direction property: direction

   ```JavaScript
   $direction:1 slide upward
   $direction:2 slide downward
   $direction:3 slide left
   $direction:4 slide right
   The scrolling direction here refers to the direction in which the scrollbar slides
   ```
   

6. Slide offset property: offset

   The initialization values are all 0, the downward slide is positive, and the upward slide is negative

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8af5e014f0ae43dfbfc1339a590d9d7e~tplv-goo7wpa0wc-image.image) </span>


<span id="_3-web-js-多实例使用"></span>
# 3. Web/JS multi\-instance usage

<span id="_3-1-多实例介绍"></span>
## 3.1 **Introduction of multiple examples**

Multi\-instance reporting is used to report to multiple applications (multiple appids) on one page, and only one SDK needs to be introduced.

<span id="_3-2-功能设置"></span>
## 3.2 Function settings

Please refer to the [Web/JavaScript SDK Integration](https://docs.byteplus.com/docs/DataFinder/Web_JavaScript_SDK_Integration_)access SDK first

```javascript
//Example 1, report to appid = {{APPID_1}}

window.collectEvent('init', {
    app_id: {{APPID_1}},
    //..... other initialization configurations
});
window.collectEvent('start');

//Example 2, report to appid = {{APPID_2}}
//Here "finder" can be given any name, as long as it is consistent with the start below
window.collectEvent('finder.init', {  
    app_id: {{APPID_2}},
    //..... other initialization configurations
});
//Here "finder" can be given any name, as long as it is consistent with the init above
window.collectEvent('finder.start');
```


<span id="_4-追踪事件"></span>
# Step 4 Track events

<span id="v5-1-1-以上版本支持"></span>
#### V5.1.1 and above are supported

<span id="_4-1-事件介绍"></span>
## 4.1 Introduction to the event

<span id="_4-1-1-starttrackevent"></span>
### 4.1.1 startTrackEvent

Start tracking an event

```javascript
//Start tracking play events
window.collectEvent('startTrackEvent', 'play')
```


Calling this method will not report the play event

<span id="_4-1-2-endtrackevent"></span>
### 4.1.2 endTrackEvent

To finish tracking an event, you can pass in the event and event properties

```javascript
//Start tracking play events
window.collectEvent('endTrackEvent', 'play', {
  name: '播放结束了' // play is over
})
```


The play event is not finally reported until this event is called, with the duration parameter, which is the time elapsed during the entire play event.

<span id="_4-1-3-pausetrackevent"></span>
### 4.1.3 pauseTrackEvent

Pause listening for an event

```javascript
//Pause tracking of play events
window.collectEvent('pauseTrackEvent', 'play')
```


<span id="_4-1-4-resumetrackevent"></span>
### 4.1.4 resumeTrackEvent

Restart listening for an event

```javascript
//retrace the play event
window.collectEvent('resumeTrackEvent', 'play')
```


<span id="_5-spa单页应用"></span>
# 5. SPA single page application

Under normal circumstances, the SPA project only sends a PV once after the SDK is initialized. After the SPA is turned on, the PV of the new page will be automatically reported when switching routes (if the dwell time function is turned on, it will also be automatically reported).

```javascript
//Start tracking play events
window.collectEvent('init', {
  spa: true, //Whether to capture single-page applications
  allow_hash: true //V5.1.3 starts to support, whether to allow listening to hash changes, the default is false, if it is not a hash route, this parameter is not required
})
```


<span id="_6-web-js-数据加密上报"></span>
# 6. Web/JS data encryption and reporting

Use the data encryption reporting function, please upgrade the SDK to the latest version of the official website, and only support privatization, saas version does not support, the minimum supported version 5.1.6, and does not support browsers below IE11.

<span id="_6-1-开启加密"></span>
## 6.1 Encryption enabled

```javascript
   The following parameters must be set
   window.collectEvent('init', {
      enable_encryption: true,
      crypto_publicKey: 'xxxxx', //Encrypt the public key, the public key must start with 04
      encryption_type: 'sm', //Encryption type, currently only sm type is supported
      encryption_header: 'gm_sm2' //Encrypted request header type, currently only supports gm_sm2 type
   })
```


After encryption is turned on, the data will be reported in the form of national secret encryption

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0fca0acf112732e148d980f663f6938c.png) </span>

<span id="_6-1-适用接口"></span>
## 6.1 Applicable interface

This feature applies to the following interfaces


1. Data reporting /list

2. User attribute reporting /profile/list

3. Device Registration /webid

4. ab experimental /abtest_config

5. request ssid /tobid

    &nbsp;


<span id="_6-2-online-decryption"></span>
## 6.2 Online decryption

You can decrypt encrypted data at this website [Decrypt Online](https://the-x.cn/cryptography/Sm2.aspx)

<span id="_7-暂停和恢复"></span>
# 7. Pause and Resume

<span id="_7-1-暂停"></span>
## 7.1 Suspension

Suspension of SDK data collection and reporting

```javascript
   window.collectEvent('stop')
```


<span id="_7-2恢复"></span>
## 7.2 Recovery

Restore SDK data collection and reporting

```javascript
   window.collectEvent('reStart')
```
