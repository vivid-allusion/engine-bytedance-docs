---
title: "Electron SDK Integration Scenario Practice"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Electron_SDK_Integration_Scenario_Practice"
---

<span id="e54486c1"></span>
# user_unique_id related

<span id="e7ec629e"></span>
## User login status settings

For example, the business has an account system and wants the SDK to synchronize user status. You can consider setting user_unique_id to the SDK immediately after the user logs in, and clearing the user_unique_id to the SDK immediately after the user logs out.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Tip: The concept of user login status is a statement from a business perspective. The SDK itself does not have the concept of user login/login. The SDK only cares about whether the user_unique_id has been actively set.</div>


```TypeScript
import { SDK } from '@datarangers/sdk-electron';
const $$sdk = new SDK({
    // ...
});

//Set user_unique_id immediately after user login
$$sdk.config({
    user_unique_id: '{{uuid}}', //Values can be considered as attributes that can be associated with the user
});

//Clear user_unique_id immediately after user logs out
$$sdk.config({
    user_unique_id: '',
});
```


<span id="78b62c1b"></span>
# Event public property

<span id="19a0bfde"></span>
## Set event public properties

Using the config method, you can set public properties that will be carried on all subsequent event reports.

```TypeScript
import { SDK } from '@datarangers/sdk-electron';
const $$sdk = new SDK({
    // ...
});

//Set event public properties, which will be carried on all subsequent event reports
$$sdk.config({
    city: '南京', //Nanjing
    nick_name: 'vikings',
});
```


Some public attribute fields are preset in the SDK, and these fields are predefined with field names, as listed in the following table.


|**Field** |**Type** |**Explain** |**Is it automatically set?**  |**Example** |
|---|---|---|---|---|
|width |number |Electron screen width |Yes |1792 |
|height |number |Electron screen high |Yes |1120 |
|os_version |string |operating system version |Yes |11_4_0 |
|os_name |string |operating system name |Yes |mac |
|platform |string |Platform name, default web |Yes |web |
|resolution |string |Screen width \* Screen height |Yes |1792x1120 |
|screen_width |number |Same width |Yes |1792 |
|screen_height |number |Same height |Yes |1120 |
|timezone |string |Time Zone |Yes |8 |
|tz_offset |string |Time zone offset seconds |Yes |\-28800 (East Eighth) |


<span id="d346cc4a"></span>
# Application instance correlation

<span id="d3ad2d12"></span>
## Using multiple instances

```TypeScript
import { SDK } from '@datarangers/sdk-electron';

//use the new operation on the constructor to generate instance 1
const $$sdk1 = new SDK({
    app_id: 1,
    // ...
});

//use the new operation on the constructor to generate instance 2
const $$sdk2 = new SDK({
    app_id: 2,
    // ...
});
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Tip:</div>



* <div data-tips="true" data-tips-type="tip">The app_id requirements of different instances cannot be the same.</div>


* <div data-tips="true" data-tips-type="tip">At present, only SaaS\-cloud\-native environments and privatized environments support multi\-application capabilities. Before use, you need to contact BytePlus technical support staff to turn on the function switch and bind multiple applications in the DataFinder project. See the end\-to\-end operation guide for multiple applications <a href="https://docs.byteplus.com/docs/DataFinder/Use_Multiple_Apps">Use Multiple Apps</a>.</div>
