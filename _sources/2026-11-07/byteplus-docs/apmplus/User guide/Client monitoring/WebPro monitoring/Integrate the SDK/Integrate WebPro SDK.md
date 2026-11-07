---
title: "Integrate WebPro SDK"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Integrate_WebPro_SDK"
---

This article is the method for accessing web services, that is, by directly using the products and services on the  platform.

<span id=".5L2_55So6ZmQ5Yi2"></span>
## Usage Limits

SDK request addresses vary by region. For details, refer to the client SDK access addresses in the [server-launching region](https://docs.byteplus.com/en/docs/apmplus/server-launching_region) section.

<span id=".5q2l6aqk5LiA77ya5o6l5YWlU0RL"></span>
## Step 1: Integrate the SDK

There are two methods for integrating the SDK: via NPM package or via CDN.

The main differences between the two access methods are as follows:


* Upgrade: When upgrading the SDK version, NPM integration requires manual version updates and redeployment, while CDN integration does not require manual updates and always provides access to the latest SDK version.

* Monitoring timing: The NPM package is ultimately bundled into the business code, while CDN integration involves directly inserting a script into the HTML. The script starts collecting exceptions before the business code runs. Therefore, comparatively, the timing for monitoring exceptions in the CDN access method is earlier.


Therefore, among the two access methods, CDN access is recommended.

<span id="NPM"></span>
### NPM

<span id="baa78428"></span>
#### Prerequisites

NPM has been installed. For NPM installation and usage, refer to the [official documentation](https://docs.npmjs.com/getting-started).

<span id="e5afd35f"></span>
#### Operation Procedure


1. Run the following command to install the SDK.

   ```TypeScript
   npm install @apmplus/web
   ```
   

2. Modify the code and integrate the SDK.

   ```TypeScript
   // Include the following code at the very beginning of the project
   import browserClient  from '@apmplus/web'// Configuration parameters
   
   browserClient('init', {
    aid: 0, // Unique identifier for the application. Required parameter, type: number
    token:'xxx-xxx' // Apply token. Required parameter, type: string
   })
   // Turn on reporting
   browserClient('start')
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><code>aid</code> and <code>token</code> must be replaced with the AppID and AppToken corresponding to the application you create. For details, refer to <a href="https://docs.byteplus.com/en/docs/apmplus/Query_AppID_and_AppToken">How to query AppID and AppToken?</a>.   </div>
   

<span id=".Q0RO77yI5o6o6I2Q77yJ"></span>
### CDN (recommended)

Add the following code to the top of the head tag in HTML.

```HTML
<!-- At the top of the <head> tag of the page, add the following code -->
<script>
(function(n,e,r,t,a,o,s,i,c,l,f,m,p,u){o="precollect";s="getAttribute";i="addEventListener";c="PerformanceObserver";l=function(e){f=[].slice.call(arguments);f.push(Date.now(),location.href);(e==o?l.p.a:l.q).push(f)};l.q=[];l.p={a:[]};n[a]=l;m=document.createElement("script");m.src=r+"?aid="+t+"&globalName="+a;m.crossOrigin="anonymous";e.getElementsByTagName("head")[0].appendChild(m);if(i        in        n){l.pcErr=function(e){e=e||n.event;p=e.target||e.srcElement;if(p        instanceof        Element||p        instanceof        HTMLElement){n[a](o,"st",{tagName:p.tagName,url:p[s]("href")||p[s]("src")})}else{n[a](o,"err",e.error||e.message)}};l.pcRej=function(e){e=e||n.event;n[a](o,"reject",e.reason||e.detail&&e.detail.reason)};n[i]("error",l.pcErr,true);n[i]("unhandledrejection",l.pcRej,true)}if("PerformanceLongTaskTiming"in        n){u=l.pp={entries:[]};u.observer=new        PerformanceObserver(function(e){u.entries=u.entries.concat(e.getEntries())});u.observer.observe({entryTypes:["longtask"]})}})(window,document,"https://apm.volccdn.com/mars-web/apmplus/web/browser.cn.js",0,"apmPlus");
</script>
<script>
window.apmPlus("init",{
  aid:0,
  token: 'xxx-xxx'
});
window.apmPlus("start");
</script>
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><code>aid</code> and <code>token</code> must be replaced with the AppID and AppToken for the application you create. For details, refer to <a href="https://docs.byteplus.com/en/docs/apmplus/Query_AppID_and_AppToken">How to query AppID and AppToken?</a>.</div>


<span id=".77yI5Y-v6YCJ77yJ5q2l6aqk5LqM77ya6K-m57uG6YWN572u"></span>
## (Optional) Step 2: Detailed configuration

In the example above, only aid and token were configured. In addition to these two parameters, there are several other parameters. For the field names and meanings of all supported parameters, refer to [API Reference](https://docs.byteplus.com/en/docs/apmplus/Use_the_SDK_to_call_an_API).

<span id=".5q2l6aqk5LiJ77ya6aqM6K-B5LiK5oql"></span>
## Step 3: Verify reporting

Please use the Chrome browser to perform the following steps to verify whether data has been reported.

<span id=".5L2_55SoQ2hyb21lIERldlRvb2xz6aqM6K-B5LiK5oql"></span>
### Use Chrome DevTools to verify reporting


1. Open Chrome DevTools.

2. Select Networks. View requests where Request Method is POST.

   Requests with Request Method OPTIONS are preflight requests and do not contain any reported content.

   <span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_15cb5a416afe9ea0786b8f2f68a362ee.png) </span>
