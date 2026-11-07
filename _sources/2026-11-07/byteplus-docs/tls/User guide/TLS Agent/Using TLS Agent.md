---
title: "Using TLS Agent"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Using-the-TLS-Agent"
---

This document describes how to use TLS Agent.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Tip</div>



* <div data-tips="true" data-tips-type="default">TLS Agent is currently in closed beta. To use it, please contact your account manager to have your account added to the allowlist.</div>


* <div data-tips="true" data-tips-type="default">This feature is supported only in <strong>Asia Pacific (Johor)</strong>.</div>



<span id="5d42eb32"></span>
## Prerequisites

You can use TLS Agent on a standalone page or on the query and analysis page. You can also use it when creating a collection or alert policy.

Before using TLS Agent, you must grant the required policy permissions in [TLS Agent](https://docs.byteplus.com/docs/tls/Permissions_policy_template#2eb74af6).


|Scenario |Permission description |
|---|---|
|Using TLS Agent on a standalone page |By default, the agent is bound to the `ServiceRoleForTLS` role, with permissions limited to the read\-only `action`. |
|Using TLS Agent in real tasks |If you are using an IAM user, you need to grant the necessary permissions to the IAM user first. |


<span id="IalLeYR3"></span>
## Steps


1. Log on to the [TLS Console](https://console.byteplus.com/tls).

2. In the top menu bar, select the region where your resources is located.

3. TLS Agent is available in the following ways.

   
   <Tabs>
   <Tab zoneid="rd9nP4LSWg" title="Standalone page">
   <TabTitle>Standalone page</TabTitle>
   
   1. In the left navigation pane, click **TLS Agent** to enter the chat interface.
   
      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">Tip   </div>
      
   
      <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The first time you use TLS Agent, you must grant TLS read\-only permission according to the instructions on the page. Then, check the user agreement and activate the feature.   </div>
      
   
   2. On the chat interface, you can customize your requirements.
   
      * Click the **DevMind** or **Query and analysis** card to enter the pre\-defined prompt into the chat box.
   
      * Click **History** on the left to view the historical task details.
   
         <span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260922093158-1664956257275.png) </span>
   
   
   </Tab>
   <Tab zoneid="dvMFcWkMRG" title="Query and analysis">
   <TabTitle>Query and analysis</TabTitle>
   
   1. In the left navigation pane, select **Common functions** \> **Query and analysis**.
   
   2. On the Query and analysis page, select the project and topic that you want to manage from the list on the left.
   
   3. In the Retrieve Analysis Statement box, click the AI Statement Assistant icon to open its input box.
   
   4. Type your requirements into the input box. The system automatically identifies the issue type and generates a response..
   
      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">Tip   </div>
      
   
      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The first time you use TLS Agent, you must read and agree to the <strong>Disclaimer and service usage rules</strong>.   </div>
      
   
      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">You can upload local files for intelligent analysis.   </div>
      
   
   
   </Tab>
   </Tabs>
   


<span id="6c9094b0"></span>
## Example

Sample responses are for reference only. Your actual environment takes precedence.


* Sample input

   <span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260922095359-1109545685140.png) </span>

* Sample output

   <span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260922095315-103644451638.png) </span>
