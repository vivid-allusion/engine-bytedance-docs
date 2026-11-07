---
title: "Web DevTools"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Web_DevTools"
---

<span id="f19cf2e8"></span>
# How to use

The URL of the page that needs to be debugged for the first time plus open_devtool_web = true and app_id = xxxx can be accessed later without adding parameters.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The plugin body is remotely loaded js, no additional installation is required, and there is no need to worry about affecting the package size.</div>


<span id="a542d93b"></span>
## Demo：

```TypeScript

The page address that need to be debugged: 'https://www.xxx.com?open_devtool_web=true&app_id=xxxx'

window.collectEvent('init', {
  //...
  enable_debug: true 
  // ...
});

```


Visit the page with parameters to enable the debugging function on the page. There will be an icon displayed in the lower right corner of the page. Click on the icon shown below on the page to enter the panel.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/edaea8e1a38e4ac6b6a9252776f46e4e~tplv-goo7wpa0wc-image.image" width="204px" /></div>


<span id="1d42b751"></span>
# How to close

Modify the code


1. Remove the parameters added to the URL.

2. Delete the key __applog_open_devtool_web in localStorage.


<span id="bfae4cfa"></span>
## Modify the code

Refer to the code below.

```JavaScript

window.collectEvent('init', {
  //...
  enable_debug: false 
  // ...
});
```


<span id="d6326e6c"></span>
# Function display

<span id="1576a376"></span>
## Event tracking list

The event tracking list has been revamped, including UI and feature upgrades.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



1. <div data-tips="true" data-tips-type="tip"><strong>Overall display</strong></div>



<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/810d7148fde1487fa88f91a2fbbbf937~tplv-goo7wpa0wc-image.image" width="244px" /></div>


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



2. <div data-tips="true" data-tips-type="tip"><strong>Display event tracking name, time, type</strong></div>



<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3259dcb7e81a4249a3dde457f10b89d7~tplv-goo7wpa0wc-image.image" width="288px" /></div>


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



3. <div data-tips="true" data-tips-type="tip"><strong>Event tracking status:</strong></div>


   1. <div data-tips="true" data-tips-type="tip">Green means successful report</div>


   2. <div data-tips="true" data-tips-type="tip">Red means failed to report.</div>



<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9e3cb5ee0747451abe262b2969be37f1~tplv-goo7wpa0wc-image.image" width="314px" /></div>


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



4. <div data-tips="true" data-tips-type="tip"><strong>Event tracking property details:</strong></div>


   1. <div data-tips="true" data-tips-type="tip">Click on the event tracking card to display the property details</div>


   2. <div data-tips="true" data-tips-type="tip">The detailed reason for the failure will be displayed in the property details of the failure event tracking.</div>



<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/db01e9bf5af043abb6641653ff5e00a1~tplv-goo7wpa0wc-image.image" width="278px" /></div>


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



5. <div data-tips="true" data-tips-type="tip"><strong>Follow event tracking, which means I only want to see some event tracking. 👉</strong></div>


   1. <div data-tips="true" data-tips-type="tip">Click on the right side of the card... to add this event tracking in the drop\-down menu Unfollowed/Unfollowed</div>


   2. <div data-tips="true" data-tips-type="tip">Event tracking is followed, marked with ❤.</div>


   3. <div data-tips="true" data-tips-type="tip">Click Manually enter follow event tracking to add and delete event tracking in batches.</div>


   4. <div data-tips="true" data-tips-type="tip">If you choose to only follow event tracking, the list will only show the event tracking that has been followed.</div>



<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dd5072fce1be48e1b4b40043d01bbc4e~tplv-goo7wpa0wc-image.image" width="254px" /></div>


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6872b3f65dca42bb8f22177c0c112fde~tplv-goo7wpa0wc-image.image" width="238px" /></div>


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



6. <div data-tips="true" data-tips-type="tip"><strong>Follow event tracking statistics 👉</strong></div>



<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a396626b2e994f8db1d5c4456faf6c85~tplv-goo7wpa0wc-image.image" width="264px" /></div>


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



7. <div data-tips="true" data-tips-type="tip"><strong>Search and delete event tracking 👉</strong></div>



<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e2e8eb335c324bcd92f5351641f5c134~tplv-goo7wpa0wc-image.image" width="278px" /></div>


<span id="3a01bad9"></span>
## Application information:

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



1. <div data-tips="true" data-tips-type="tip"><strong>basic information area 👉</strong></div>



<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9427c2cb11c24d1ca556cf498414921f~tplv-goo7wpa0wc-image.image" width="288px" /></div>


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



2. <div data-tips="true" data-tips-type="tip"><strong>user information area 👉</strong></div>



<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/af5ad00f18344d61a012b1fa98ccfca9~tplv-goo7wpa0wc-image.image" width="316px" /></div>


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



3. <div data-tips="true" data-tips-type="tip"><strong>Public parameter information, displaying information such as the current browser 👉</strong></div>



<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f5d90c16872843d8887b5f09542cc644~tplv-goo7wpa0wc-image.image" width="372px" /></div>


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



4. <div data-tips="true" data-tips-type="tip"><strong>Configuration area where other functions are enabled 👉</strong></div>



<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9985747e89d247b1a3d3fc2a62a5db53~tplv-goo7wpa0wc-image.image" width="368px" /></div>


<span id="96c3b99f"></span>
## SDK run log:

The SDK runtime log also updates the UI and shows more SDK lifecycle and call logs.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



1. <div data-tips="true" data-tips-type="tip"><strong>Show call SDK execution log 👉</strong></div>


   1. <div data-tips="true" data-tips-type="tip">API call log</div>


   2. <div data-tips="true" data-tips-type="tip">SDK internal run log</div>


   3. <div data-tips="true" data-tips-type="tip">Log of SDK requests</div>



<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e23c5690fb174bf7a4e9c860e5154032~tplv-goo7wpa0wc-image.image" width="390px" /></div>


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



2. <div data-tips="true" data-tips-type="tip"><strong>Click on the card to display the log details. 👉</strong></div>



<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ee2b52751cf54b1b8851096a59426011~tplv-goo7wpa0wc-image.image" width="356px" /></div>


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



3. <div data-tips="true" data-tips-type="tip"><strong>Display exception information 👉</strong></div>



<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bec9064512ca4308a478bd2704532540~tplv-goo7wpa0wc-image.image" width="336px" /></div>
