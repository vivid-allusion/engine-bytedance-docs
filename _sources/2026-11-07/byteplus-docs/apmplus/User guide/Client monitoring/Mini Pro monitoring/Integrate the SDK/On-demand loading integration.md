---
title: "On-demand loading integration"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/On-demand_loading_integration"
---

If you are relatively sensitive to package size, you can refer to the following documentation to load feature modules as needed and remove unused code.

<span id=".5oyJ6ZyA5Yqg6L296ZuG5oiQ"></span>
## On\-demand loading integrations

On\-demand loading integration is only applicable to the NPM package access method.

If you only require monitoring for Js Error, Http, PV, and UV, you can load these three modules as needed. The following code uses the **WeChat Mini Program platform** as an example:

```typescript
import  {
    createBaseMiniProgramClient,
  JsErrorIntegration,
  HttpIntegration,
  PageviewIntegration,
  WxAdapter,

}  from '@apmplus/mini-program'
const  client =  createBaseMiniProgramClient([WxAdapter])!

client.init({
  aid:  123,  // Replace with your aid
  token:'xxx-xxx', // Replace with your token
  integrations: [HttpIntegration(),  PageviewIntegration(),  JsErrorIntegration()],

})
```


<span id=".6ZuG5oiQ5YiX6KGo"></span>
## Integration list


|**Integration items** |**Applicable mini program platforms and third\-party frameworks** |**Description** |
|---|---|---|
|HttpIntegration |WeChat, Douyin, Alipay, Baidu, Lark, Taro, Uni App |Reporting occurs when request, downloadFile, or uploadFile is called. |
|JsErrorIntegration |WeChat, Douyin, Alipay, Baidu, Lark, Taro, Uni App |Report when a Js Error or Navigate Error occurs. |
|BreadcrumbIntegration |WeChat, Douyin, Alipay, Baidu, Lark, Taro, Uni App |Collect HTTP and route change information, and report both together when a JavaScript error is reported. |
|PageviewIntegration |WeChat, Douyin, Alipay, Baidu, Lark, Taro, Uni App |Reported when the page loads, and used to collect statistics on PV, UV, and page time on site. |
|CustomIntegration |WeChat, Douyin, Alipay, Baidu, Lark, Taro, and Uni App |After loading this integration, the Client instance can call \*client.sendEvent\* and \*client.sendLog\*. |
|AppLaunchPerfIntegration |WeChat, Douyin, Alipay, Baidu, Lark, Taro, Uni App |Collect startup performance and report it after startup is complete. |
|PagePerfIntegration |WeChat, Douyin, Alipay, Baidu, Lark, Taro, Uni App |Collect pageload performance and report it after switching pages and after the page has finished loading. |
|PerformanceIntegration |WeChat, Douyin, Taro, and Uni App |Collect performance metrics, such as FR, FP, FCP, and LCP. Currently, these metrics are only available on certain device models for WeChat and TikTok Mini Program. |
|SetDataIntegration |WeChat, Douyin, Alipay, Baidu, Lark, Taro, Uni App |Reporting occurs when setData is called. Since setData is called frequently, enabling reporting may cause some minor fluctuations in pageload performance. |
|FrameworksAdapterIntegration |Taro |Products compatible with Alipay under Taro. |
