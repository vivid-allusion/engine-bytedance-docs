---
title: "Intelligent Analysis Agent Third-Party Integration Guide"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Intelligent_Analysis_Agent_Third-Party_Integration_Guide"
---

This document introduces the third\-party integration guide for the Intelligent Analysis Agent. You will learn how to access the agent via API for both web and mobile platforms.

<span id="9728c995"></span>
# Caution


* Before using the APIs described in this document, you must complete the preliminary steps of integrating JWT\-Token and applying for a Token. Please review the invocation method first. For details, see [Invocation Methods](https://docs.byteplus.com/docs/dataagent/Invocation_Methods).

* The currently supported regions are:

   * North China 2 (Beijing), RegionID: cn\-beijing

   * East China 2 (Shanghai), RegionID: cn\-shanghai


<span id="90956b2f"></span>
# Third\-party integration interface

<span id="c605b31a"></span>
## Web access

Based on JWT\-Token + iframe, the result is shown below:


|General agent |Professional agent |
|---|---|
|<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/93b0bd58dcde495ba1383280aab255cf~tplv-goo7wpa0wc-image.image) </span> |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/228e6412287c4817b2bbf30eb62a2c76~tplv-goo7wpa0wc-image.image) </span> |


<span id="07429100"></span>
### **Request parameters**


|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|domain |string |Yes |`https://console.volcengine.com/bi/datawind/data-agent/analytics-agent-open` |Domain name<br><br><br>* SaaS environment domain: `https://console.volcengine.com/bi/datawind/data-agent/analytics-agent-open`<br><br>* Private deployment domain: Actual deployed environment domain address `${domain}/bi` |
|APPID |number |Yes |1 |Project ID. See explanation for acquisition method. |
|jwtToken |string |Yes |`eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9.eyJ0b2tlbl90eXBlIjoib3BlbmFwaSIsInVzZXJuYW1lIjoiYWRtaW4iLCJ1c2VyX3BheWxvYWQiOnt9LCJleHAiOjE3NDM1NjY0OTEsImNsaWVudF9pZCI6ImYzMDE5ZGMzZmZmNTE1MzhkMjM5Nzc0ZmI3ZjI4Mzg4In0.gHN39Aq3XQkiZpCJmcvBLaH1eM******` |User jwtToken. See [Invocation Methods](https://docs.byteplus.com/docs/dataagent/Invocation_Methods) for acquisition method. |
|AGENT_ID |number |Yes |1 |Agent ID. See explanation for acquisition method. |
|feature |json |No |'{}' |See [Feature configuration parameters](https://docs.byteplus.com/docs/dataagent/JS_SDK_Integration_Solution#98f7f3c0) for details. |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">APPID and AGENT_ID acquisition method can be found in the agent web page link:</div>


<div data-tips="true" data-tips-type="tip"><img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f4bc3bad87524d5caebc4d71c20219d4~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


<span id="71f21e35"></span>
### **Request example**

```TypeScript
<iframe
    src={`${domain}?region=${region}/#/agent?agentId=${AGENT_ID}&appId=${APPID}&inline=true&jwtToken=${jwtToken}&region=${region}`}
/>
```


<span id="8fe6d015"></span>
## Mobile access

The mobile view can be used for mobile H5, sidebar or floating window activation, or when space is limited. The mobile and PC view sessions are identical; only the display differs. The agent page is adaptive. When accessed from a mobile device, it automatically switches to the mobile view.

Access method: When using a mobile device, the view automatically switches to the mobile version. You can also use parameters to force the switch to the mobile view. Add `&forceMobile=true&inline=true` to the `url`'s `queryString`.

<span id="9c614d98"></span>
### **Request parameters**

Same as above **Web access \- Request parameters**

<span id="f3a7c8e2"></span>
### **Request example**

```TypeScript
<iframe 
    src={`${domain}?region=${region}/#/agent?agentId=${agentId}&appId=${APPID}&jwtToken=${jwtToken}&region=${region}&inline=true&forceMobile=true`}
/>
```
