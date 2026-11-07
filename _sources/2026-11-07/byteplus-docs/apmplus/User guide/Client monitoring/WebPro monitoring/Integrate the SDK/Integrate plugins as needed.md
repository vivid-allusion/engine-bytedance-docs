---
title: "Integrate plugins as needed"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Integrate_plugins_as_needed"
---

Some less commonly used requirements are not integrated into the SDK by default due to their limited usage scenarios. You can integrate them as needed using a custom plugin.

<span id="1075e3d3"></span>
## Basic usage

```TypeScript
client('init',{
  ...
  integrations: [{
    name: 'name', // Plugin name, used for deduplication
    setup: (client) => void, // Initialization code; the client passed in is an instance of the SDK
    tearDown: () => void, // Optional; must be provided if there are side effects. Will be executed when the SDK's destroy method is called.
  }],
  ...
})
```


<span id=".5L2_55So5o-S5Lu25YyF"></span>
## Use plugin packages

<span id="refreshPreStartContext"></span>
### refreshPreStartContext


|**Plugin package modules** |**DescriptionS** |
|---|---|
|Version requirements |apmplus/integrations version \>=1.2.2 |
|Feature descriptions |Refresh the contexts in the pre\-send queue before start using the context at the time of start. |
|Application scenarios |If you want the setting of certain context to take effect for all reporting events, but some context can only be obtained asynchronously, you can use this plugin. The plugin refreshes the context of all items in the pre\-send queue before start, using the context at the time start is called. |
|Sample code |```TypeScript```<br>```import { refreshPreStartContext } from '@apmplus/integrations/refreshPreStartContext'```<br>```import client from '@apmplus/web'```<br>``````<br>```client('init', {```<br>```  ...```<br>```  integrations: [refreshPreStartContext()]```<br>```  ...```<br>```})```<br> |


<span id="captureConsole"></span>
### captureConsole


|**Plugin package modules** |**DescriptionS** |
|---|---|
|Version requirements |apmplus/integrations version \>=1.2.2 |
|Feature description |When calling the global console object, the parameter passed in the call is wrapped as a JavaScript error and reported to the platform. |
|Parameter Description |Specify the levels array that need to be hooked, including "log", "info", "warn", "error", "debug", "assert", and so on. |
|Risk descriptions |Because the global console object has been hooked, using console methods in the browser console will also trigger reporting. |
|Sample code |```TypeScript```<br>```import { captureConsole } from '@apmplus/integrations/captureConsole'```<br>```import client from '@apmplus/web'```<br>``````<br>```client('init', {```<br>```  ...```<br>```// levels is required. Specify which console methods need to be hooked as shown below. The feature demonstrated here hooks console.error, wraps the call parameter as a JS error, and reports it to the platform.```<br>```  integrations: [captureConsole({ levels: ['error'] })]```<br>```  ...```<br>```})```<br> |


<span id="actionPlugin"></span>
### actionPlugin


|**Plugin package modules** |**DescriptionS** |
|---|---|
|Version requirements |* apmplus/integrations version \>=2.0.0<br><br>* apmplus/web version \>=1.7.0 |
|Feature description |Monitor user actions to measure their performance. |
|Application scenarios |If the business team wants to restore the complete path of user actions and evaluate their performance, they can use this plugin. |
|Sample code |```TypeScript```<br>```import client from '@apmplus/web'```<br>```import { actionPlugin } from '@apmplus/integrations/action'```<br>``````<br>```// Example 1: Integrate the action plugin```<br>```client('init',{```<br>```  ...```<br>```  integrations: [actionPlugin()],```<br>```  ...```<br>```})```<br>``````<br>```// Example 2: Integrate the action plugin but do not listen to any event```<br>```client('init',{```<br>```  ...```<br>```  integrations: [actionPlugin({ types: false })],```<br>```  ...```<br>```})```<br>``````<br>```// Example 3: Integrate the action plugin while also listening for a specified event type```<br>```client('init',{```<br>```  ...```<br>```  integrations: [actionPlugin({ types: ['click'] })],```<br>```  ...```<br>```})```<br>``````<br>```// API support: Manual start of an action is supported```<br>```client("startAction", "action name", "action type");```<br> |


<span id=".6Ieq5a6a5LmJ5o-S5Lu2"></span>
## Custom plugins

If the plugins in the plugin package do not meet your business requirements, you can publish a plugin package yourself.


1. Publish the plugin package.

   A plugin can be implemented by directly returning an object or a method. You can pass in some configuration and return an object, as long as this object satisfies the integrations type specification.

   ```typescript
   import client from '@apmplus/web'
   client('init',{
     ...
     integrations: [{
       name: 'name', // Plugin name, used for deduplication
       setup: (client) => void, // Initialization code; the passed-in client is a Monitoring instance
       tearDown: () => void, // Optional; must be provided if there are side effects. Executed when the SDK's destroy method is called.
     }],
     ...
   })
   ```
   

   Sample code is as follows:

   ```typescript
   import client from '@apmplus/web'
   
   // A custom plugin
   // feature: Refresh the context of the pre-collection queue using the context at start
   const refreshPreStartContext = () => ({
     name: 'refreshPreStartContext',
     setup: (client: WebClient) => {
       client.on('start', () => {
         const preStartQueue = client.getPreStartQueue()
         preStartQueue.forEach((ev: WebReportEvent, index: number) => {
           preStartQueue[index] = {
             ...ev,
             overrides: {
               ...(ev.overrides ?? {}),
               context: client?.context?.toString() || {},
             },
           }
         })
       })
     },
   })
   
   client('init',{
     ...
     // Use this plugin
     integrations: [refreshPreStartContext()],
     ...
   })
   ```
   

2. Integrate into the plugin package.

   If your custom plugin is applicable to most business use cases, please contact the developers to have it integrated into apmplus/integrations.

   ```typescript
   // Import a plugin from the official plugin package
   import { refreshPreStartContext } from '@apmplus/integrations'
   import client from '@apmplus/web'
   
   client('init', {
     ...
     integrations: [refreshPreStartContext()]
     ...
   })
   ```
   


<span id="22300ca2"></span>
## How to integrate plugins as needed using the Script method

With the on\-demand integration method, plugin configuration must be performed during init, whereas with the script\-based integration method, init is typically performed in the HTML. All you need to do is move the init\-related code from html to business code.

After introducing the pre\-collection script in HTML, initialize it in the business code. Using the action plugin as an example:

```TypeScript
import { actionPlugin } from '@apmplus/integrations/action'

window.{{GlobalName}}('init', {
  aid: xxx,
  token: 'xxx', 
  integrations: [actionPlugin()]，
})
window.{{GlobalName}}('start')
```


Actions like this generally have no side effects, and the presence of the pre\-collection script ensures that any error or exception occurring before initialization will not be missed. However, if the initialization occurs too late, it may result in earlier requests not being collected. Therefore, make sure to execute the initialization code early in the business logic.
