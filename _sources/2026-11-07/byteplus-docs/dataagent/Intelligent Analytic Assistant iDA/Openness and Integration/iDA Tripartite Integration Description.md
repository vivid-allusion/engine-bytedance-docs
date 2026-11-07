---
title: "iDA Tripartite Integration Description"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/iDA-Tripartite-Integration-Description"
---

This article introduces you to the three\-way integration instructions of Intelligent Analytics Agent, and you will learn how to access the agent on the web and mobile end through the API.

<span id="9728c995"></span>
# Precautions

Before you use the API described in this article, you need to complete the pre\-operation of accessing JWT\-Token and applying for Token. Please understand the calling method first, and read the details [Invocation Methods](https://docs.byteplus.com/docs/dataagent/Invocation_Methods).

<span id="90956b2f"></span>
# Tripartite Integrated Solution Interface

<span id="c605b31a"></span>
## Web access

The effect based on JWT\-Token + iframe is as follows:


|General agent |Professional agent |
|---|---|
|<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/edafa3f5809641a09bd1d5e7bf2d8658~tplv-goo7wpa0wc-image.image) </span> |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9ae595eb6ce24a46ac65699c3923b56d~tplv-goo7wpa0wc-image.image) </span> |


<span id="07429100"></span>
### **Request parameters**


|**Parameter** |**Type** |**Is it required?**  |**Sample value** |**Description** |
|---|---|---|---|---|
|domain |string |Yes |`https://console.volcengine.com/bi/datawind/data-agent/analytics-agent-open` |domain name<br><br><br>* Saas environment domain: `https://console.volcengine.com/bi/datawind/data-agent/analytics-agent-open`<br><br>* Privatized domain: the actual deployed environment domain address `${domain}/bi` |
|APPID |number |Yes |1 |Project id, see the description for the acquisition method. |
|jwtToken |string |Yes |`eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9.eyJ0b2tlbl90eXBlIjoib3BlbmFwaSIsInVzZXJuYW1lIjoiYWRtaW4iLCJ1c2VyX3BheWxvYWQiOnt9LCJleHAiOjE3NDM1NjY0OTEsImNsaWVudF9pZCI6ImYzMDE5ZGMzZmZmNTE1MzhkMjM5Nzc0ZmI3ZjI4Mzg4In0.gHN39Aq3XQkiZpCJmcvBLaH1eM******` |User jwtToken, see how to get it [Invocation Methods](https://docs.byteplus.com/docs/dataagent/Invocation_Methods) |
|AGENT_ID |number |Yes |1 |Agent ID, see the description for the acquisition method. |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">APPID and AGENT_ID can be obtained from the agent webpage link:</div>


<div data-tips="true" data-tips-type="tip"><img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/78940282b35b43f2a2973eb67668e458~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


<span id="71f21e35"></span>
### **Request example**

An example of a request is as follows:

```TypeScript
<iframe
    src={`${domain}/#/agent?agentId=${AGENT_ID}&appId=${APPID}&inline=true&jwtToken=${jwtToken}`}
/>
```


```TypeScript
<iframe 
    src={`${domain}/#/agent?agentId=${agentId}&appId=${APPID}&jwtToken=${jwtToken}&inline=true&forceMobile=true`}
/>
```


<span id="a36a0c10"></span>
# Visual information configuration

<span id="5ce3633a"></span>
## Function Description

After appending `embed_settings = true`to the page `url`parameter, you can enter the **embedded visual configuration mode**. In this mode, an embedding settings panel will appear, which can quickly switch various embedding configurations and preview the effect in real time through the switches in the panel; after the configuration is completed, copy the corresponding embedding link with one click.

<span id="4c3313c5"></span>
## Operation steps


1. **Enter the embedded visual configuration mode:**  append `embed_settings = true`to the `url`parameter of the target page, and enter the embedded visual configuration mode after refreshing the page.

2. **Adjust the embed configuration and preview:**  In the embed settings panel, switch the configuration item through the relevant switch, and the page will display the corresponding effect in real time.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/73d71b146fe347b3928ae04b1ac4ae8c~tplv-goo7wpa0wc-image.image) </span>

3. **Copy Embed Link**: After the effect is confirmed, click the **Copy Embed Link** button at the bottom of the panel to get the embed link corresponding to the current configuration.


<span id="0ed8f85d"></span>
## Parameter description


|Parameter |Location |Description |
|---|---|---|
|`embed_settings=true` |Page URL parameters |Enable the embedded visual configuration mode and display the embedded settings panel;<br><br>**Supported since version release_v4.**  |
