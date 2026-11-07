---
title: "MAB(Multi-Armed Bandit) Experimental SDK Integration: Support In and Out of Groups (Turn Off Experience Consistency)"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/MAB-Multi-Armed-Bandit-Experimental-SDK-Integration-Support-In-and-Out-of-Groups-Turn-Off-Experience"
---

The APP/Mini Program optimization scenario of the MAB experiment supports turning off experience consistency, that is, allowing users to enter/leave groups; after closing, the tuning will be tuned according to the configuration parameters of the experiment, while the experimental group version (VID) will be tuned in the unclosed scenario. The experimental SDK integration methods in the two scenarios are different. This article takes the client side experiment as an example to introduce the experimental integration ideas and operation points after closing the experience consistency.

<span id="b573f351"></span>
# Background information


|Comparison term |MAB experiment not close "experience consistency" |MAB Experiment close "experience consistency" |
|---|---|---|
|Tuning benchmark |Tuning is performed for the group version (VID) of the experiment |Tuning will be tuned for the configuration parameters of the experiment |
|Experimental SDK integration ideas |The MAB experiment SDK integration method is similar to that of ordinary A/B experiments, without special logic. |In order to obtain the configuration parameters of the MAB experiment and calculate the corresponding input and conversion metrics, you need to synchronously report the dimension values corresponding to the MAB experiment configuration parameters to the event public attribute `mab_arm`when using this function, so as to ensure that the user's subsequent behavior events can be associated with the corresponding experimental grouping, without manually adding this attribute to each event. |


Here's how to experiment with SDK integration after turning off "Experience Consistency".

<span id="9b910ba5"></span>
# Preparation

You need to manually create a custom "event public property" for subsequent reporting of the dimension values of the MAB experimental configuration parameters. The configuration requirements for event public properties are as follows:


* Event public property name: `mab_arm`.

* Property type: must be `string`.


The configuration example is as follows.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fdcb2dee4fee4be1908c8e28302bb6e6~tplv-goo7wpa0wc-image.image) </span>

<span id="a4cfc7ab"></span>
# SDK integration

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">There are currently two ways to experiment with SDK integration, as detailed in the <strong>Integration Scheme Description</strong> section below.</div>


* <div data-tips="true" data-tips-type="warning">The following takes the client side as an example to introduce the sample code. The operation of the server side is similar.</div>



<span id="74572dda"></span>
## Method 1: Get the configuration val through `getVar`.

<span id="f40ea328"></span>
## Integration Solution Description

When doing client\-side integration in this way, you need to call the `getVar`method twice:


* When the shunt result is actually obtained, `getVar`is called first, and the shunt result value is set as the event public property `mab_arm`after getting the shunt result value.

* Then call `getVar`again to ensure that the second time you call `getVar`, you can bring the `mab_arm`property value.


It is recommended that you make business logic judgments when you call `getVar`the second time.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">By calling the <code>getVar</code>method twice, first obtain the shunt result and set it as a public property, and then call it twice to ensure that the property takes effect, so that subsequent events can automatically carry <code>mab_arm</code>.</div>



* <div data-tips="true" data-tips-type="warning">Advantage: After setting the public attribute, all subsequent exposure events and behavior events will automatically carry <code>mab_arm</code>without manual processing.</div>


* <div data-tips="true" data-tips-type="warning">Disadvantages: It will trigger two exposure event reports. If customers are billed according to the event volume, they need to pay attention to the resulting costs.</div>



<span id="31745bec"></span>
### Operation steps


1. Call `getVar`for the first time to get the experimental shunt result;

2. Set the result to the event public property `mab_arm`through the `config`method;

3. Calling `getVar`a second time, ensuring that the request carries the `mab_arm`properties that have been set, and processing the business logic in this callback.


Reference code:

```JavaScript
window.collectEvent('getVar', 'ab-key', 'ab-default-value', (res) => {
    console.log(res)
    if(res){

        window.collectEvent('config',{
            mab_arm: res, //User experiment configuration value
        });
        
        window.collectEvent('getVar', 'ab-key', 'ab-default-value', (res) => {
            //business logic processing
            // XXX
        })
    }
});
```


<span id="1d34c7ec"></span>
## Method 2: Use getAllVars to get the vid and configuration first

<span id="294c6794"></span>
## Integration Solution Description

When performing client\-side integration in this way, it is recommended to obtain all the configurations through getAllVar when accessing the experimental SDK, traverse the specified configuration, set the public properties, and then call the getVar method normally and process the logic.


* You need to call `getAllVars`first to get all the experimental configurations, extract the target configuration values and set them to public properties.

* Then call `getVar`to handle business logic to reduce the number of exposure event reports.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The way of event properties:</div>



* <div data-tips="true" data-tips-type="warning">Advantages: Trigger only one exposure event report, reducing event volume costs.</div>


* <div data-tips="true" data-tips-type="warning">Disadvantages: When there are many experimental configurations, loading the full configuration may cause certain resource consumption, and the client side memory may be occupied extra.</div>



<span id="61783975"></span>
### Operation steps


1. Call `getAllVars`to get all experimental configurations;

2. Extract the `val`(configuration value) of the target experiment from the full configuration and set it to the public attribute `mab_arm`through the `config`method;

3. A normal call to `getVar`handles the business logic (at which point the request already carries `mab_arm`).


Reference code:

```JavaScript
window.collectEvent('getAllVars', (res) => {
    console.log(res);
    config_val = res['test_key']
    if(config_val) {
        vid = config_val['vid']
        val = config_val['val']
        console.log(vid, val)
        window.collectEvent('config',{
            mab_arm: val, //User experiment configuration value
        });
    }
});
 window.collectEvent('getVar', 'ab-key', 'ab-default-value', (res) => {
    //business logic processing
    // XXX
});
```


<span id="0dc45b51"></span>
# Reference: Experimental SDK Debugging

After completing the experimental SDK integration configuration, you can debug the SDK to verify the connected results. For the debugging operations of each end, please refer to the SDK debugging documentation of the corresponding end. Taking Web/Js SDK as an example, the detailed operation of debugging can be referred to: [Web/JS SDK Debugging and Data Validation](https://docs.byteplus.com/docs/DataTester/Web-JS-SDK-Debugging-and-Data-Validation).
