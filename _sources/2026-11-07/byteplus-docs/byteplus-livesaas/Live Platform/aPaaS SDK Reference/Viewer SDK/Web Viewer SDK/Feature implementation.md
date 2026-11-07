---
title: "Feature implementation"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/feature-implementation"
---

This topic introduces how to implement complex features using the Web Viewer SDK to create personalized live rooms.

<span id="c5d19ee4"></span>
## Prerequisite

You have integrated the Web Viewer SDK. For more information, see [Integrating the Web Viewer SDK](https://docs.byteplus.com/docs/byteplus-livesaas/docs-integrating-the-web-viewer-sdk).

<span id="065efa57"></span>
## Using custom mode for authentication

If viewers can log in via your own account system, such as your company's official website, you can use custom mode for authentication, allowing viewers to use their identity information from your account system to join the live room. You can choose when viewers log in to your account system.

<span id="645e07bd"></span>
### Supported platforms

The custom authentication mode is supported on both PC and mobile platforms.

<span id="409202e7"></span>
### Demo

Since the implementation effects are similar across devices, BytePlus Live provides a PC demo of this feature for you to experience the differences between the two login timings. Click [here](https://live.byteplus.com/demo/sdk/index.playground.html?mode=pc-custom) to try it out.


<Tabs>
<Tab zoneid="iNHmmvpEKo" title="Login Before Entering the Live Room">
<TabTitle>Login Before Entering the Live Room</TabTitle>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/448026580d4444ad9d12ac285eaecb46~tplv-goo7wpa0wc-image.image) </span>


</Tab>
<Tab zoneid="xiRAWx4frI" title="Login After Entering the Live Room">
<TabTitle>Login After Entering the Live Room</TabTitle>

Viewers join the live room first to watch the live stream and view comments, and then trigger the custom login process when they perform operations such as sending comments and participating in interactions.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1de67904227b4e19a15f359340d61749~tplv-goo7wpa0wc-image.image) </span>


</Tab>
</Tabs>


<span id="3075a0fa"></span>
### **Method 1: Login before entering the live room**

For this method, viewers are required to log in before entering the live room, after which they can watch the live stream or participate in interactions.

<span id="45ae575b"></span>
#### Scenario

This method is suitable for scenarios that require identity verification, access control, or data tracking, such as member\-only events, internal corporate training, or paid courses. It provides higher security and clear user identification but may increase the entry barrier for viewers.

<span id="c302c753"></span>
#### Sample code

When initializing the SDK, set the parameter value of `mode` to `2` and set the parameter value of token to the authorization token returned by calling [GetSDKTokenAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getsdktokenapi).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">After viewers log in to your account system, pass the viewer's nickname and ID when calling <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-getsdktokenapi">GetSDKTokenAPI</a> to get the authorization token when the value of <code>mode</code> is set to <code>2</code>.</div>


The sample code is as follows.

```JavaScript
  var webSDK = new window.ByteLiveWebSDK({
    activityId: 172291833994****,
    token: 'ak3T%2FdaGJDL5zSFD7%2F1GPGP****',
    service: 'liveDemo',
    mode: 2, 
    ...
```


<span id="80085084"></span>
### **Method 2: Login after entering the live room**

For this method, viewers can first enter the live room to watch the stream and browse comments without logging in. A custom login flow is triggered only when they attempt to post comments, like, or engage in other interactions.

<span id="2b8319b1"></span>
#### Scenario

This method is suitable for public events, open courses, or marketing livestreams that aim to increase traffic and user conversion. It lowers the initial entry barrier and improves the viewing experience, though some features remain restricted for anonymous users.

<span id="14ca81e0"></span>
#### Implementation process

The implementation process is as follows:


1. When initializing the SDK, set the parameter value of `mode` to `1`, disable BytePlus Live's built\-in login system, and listen to the [permission.need](https://docs.byteplus.com/en/docs/byteplus-livesaas/events#permission-need) event.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can get the authorization token when the value of <code>mode</code> is set to <code>1</code> in any of the following ways:   </div>
   

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Log in to the <a href="https://console.byteplus.com/livesaas/liveManagement/">BytePlus Live console</a> and get the token from the <strong>Web SDK embedding</strong> tab on the <strong>Producer</strong> \> <strong>Page embedding</strong> page in a live room.   </div>
   

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Call <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-getsdktokenapi">GetSDKTokenAPI</a> to get the token.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Currently, the <code>permission.need</code> event only applies to this scenario.   </div>
   

2. You need to implement the logic for viewers' login and the logic for getting the authorization token when the value of `mode` is set to `2`.

3. The SDK will trigger the `permission.need` event when viewers perform the following operations requiring user information:

   * Click the comment text box, including that under the menus for chat interaction and Q&A

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">The menu for Q&A is supported only on PCs and mobile devices in landscape mode.      </div>
      

   * Like comments

   * Reward hosts with gifts

   * Check in

   * Participate in quizzes

   * Participate in votes

   * Participate in lucky draws

   * Participate in non\-anonymous questionnaires

   * Book a live stream (the `permission.need` event is triggered only when the SMS reminder feature for booking is disabled)

   * Like the live room (the `permission.need` event is triggered only when login is required for liking a live room, namely when the value of `loginInToThumbUp` is set to `true`)

4. You need to trigger the custom login process after detecting the `permission.need` event.

5. Viewers log in to your account system.

6. Pass the viewer's nickname and ID when calling [GetSDKTokenAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getsdktokenapi) to get the authorization token when the value of `mode` is set to`2`.

7. Call the SDK's [updateMode2Token](https://docs.byteplus.com/en/docs/byteplus-livesaas/api#updatemode2token) method to update the token when the value of `mode` is `1` to the token when the value of `mode` is `2`.


The sample code is as follows.

```JavaScript
  var webSDK = new window.ByteLiveWebSDK({
    activityId: 172291833994****,
    token: 'ps****',
    service: 'liveDemo',
    mode: 1,
    options: {
      saveUserInfo: true, // Optional. Used to cache user information when the value of mode is set to 1.
      disabledLogin: true, // Disable BytePlus Live's built-in login system.
    }
  })
  
    const login = () => {
    // Implement the login logic yourself.
    return {
      Nickname: 'Viewer A',
      UserIdStr: '57584'
    }
  }

  const getSDKToken = () => {
    //  Implement the logic yourself to get the token when the value of mode is set to 2.
    return {
      Token: 'hdsh****'
    }
  }
  // Execute the handleLogin function after detecting the permission.need event.
  const handleLogin = async () => {
      // Trigger the custom login process and viewers must log in to your account system.
      const userInfo = await login();
      // Use the login user information to call GetSDKTokenAPI to get the token when the value of mode is set to 2.
      const res = getSDKToken(userInfo);
      // Call the SDK's updateMode2Token method to update the token when the value of mode is 1 to the token when the value of mode is 2.
      webSDK.updateMode2Token(res.Token);
  }
  // Listen to the permission.need event.
  webSDK.on('permission.need', handleLogin);
```


<span id="1b8b0536"></span>
## Customizing the style and background color of icons

For portrait\-mode live rooms on mobile platforms, you can customize the style and background color of icons.

<span id="ce0f5c8a"></span>
### Supported platforms

This customization is supported on mobile platforms.

<span id="4e3d885c"></span>
### Icon style sample code

You can replace the following default icons or insert new ones using the `portraitMenuExtends` parameter.


|Default Icon |Key |Default Style |
|---|---|---|
|Interaction tools |IMAGETEXT_LIVE |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6a2410780be54e1785230526b2355fde~tplv-goo7wpa0wc-image.image) </span> |
|Graphics |IMAGE_MENU |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bac5f8c1c4df4c9c9086260824937409~tplv-goo7wpa0wc-image.image) </span> |
|Gift |GIFT |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9720e583ed9049588bf3bca76a14f9aa~tplv-goo7wpa0wc-image.image) </span> |
|Embedded link |EMBEDDED_URL |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cd15bc47815244c4ad37337a86e94e49~tplv-goo7wpa0wc-image.image) </span> |
|Shopping cart |CART |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/634e78ec991447f4a9a65dc3566d2ae1~tplv-goo7wpa0wc-image.image) </span> |


The sample code is as follows.

```JavaScript
  var webSDK = new window.ByteLiveWebSDK({
    token: 'Ik****',
    activityId: 180812505419****,
    service: 'Test',
    mode: 1,
    modules: [
      {
        id: 'content', // The page element ID. The full-page module for the portrait mode of mobile devices will be embedded into this element.
        mode: "mobile-portrait" 
      },
    ],
    options: {
      saveUserInfo: true,
      portraitMenuExtends: [
      // Replaces the shopping cart icon, using Flexbox layout, and the image is centered both vertically and horizontally within the container.
        {
          render: '<div style="display: flex; align-items: center; justify-content: center;"><img src="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a604f7ff249215d68b9702f2ec7ab217.png" /></div>', //  Only network paths are supported.
          key: 'CART'
        },
     // Inserts a new icon.   
        {
          render: '<div style="color: #fff">Like</div>', // The text content is "Like", and the text color is white.
          key: '222', // The key that is different from the one of a default icon, which means to insert a new icon.
          onClick: console.log, // The click event callback.
          index: 2, // The display order of the icon. The larger the parameter value, the closer to the left the icon. If the parameter value is larger than 70, viewers can only view the icon after tapping the ellipsis icon. At most 4 icons, including the default ones in your live room, can be displayed at one time. Viewers can only view other icons after tapping the ellipsis icon.
        },
      ],
    },
  });
```


View the comparison as follows.


<Tabs>
<Tab zoneid="A1svMuF1Tp" title="Before customization">
<TabTitle>Before customization</TabTitle>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ce391ccf0bc948e4aea1a6e550d531a5~tplv-goo7wpa0wc-image.image) </span>


</Tab>
<Tab zoneid="mo59Jpnyce" title="After customization">
<TabTitle>After customization</TabTitle>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3353c29825d748a08302235d0b7f9dea~tplv-goo7wpa0wc-image.image) </span>


</Tab>
</Tabs>


<span id="ba2ecd2f"></span>
### Icon background color sample code

After customizing the icon style as mentioned above, the element of the new icon will have an `id` attribute in the format `portrait-menu-icon-{key}`. For example, after replacing the shopping cart icon, the new icon element's `id` attribute will be `portrait-menu-icon-CART`. You can use this `id` attribute to perform DOM operations on the element, such as modifying the background color and image size.

The sample code changes the background color of the new icon to red using the `id` attribute `portrait-menu-icon-CART`.

```JavaScript
document.querySelector('#portrait-menu-icon-CART').style.background = 'red'
```


View the comparison as follows.


<Tabs>
<Tab zoneid="ec0FtKFmCN" title="Before customization">
<TabTitle>Before customization</TabTitle>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/084b5dd7ae2a4fbd99020db47cd3b060~tplv-goo7wpa0wc-image.image) </span>


</Tab>
<Tab zoneid="Zwi4hA7GBr" title="After customization">
<TabTitle>After customization</TabTitle>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0ef451b2b82845098a61b895b1775921~tplv-goo7wpa0wc-image.image) </span>


</Tab>
</Tabs>


<span id="86db69f2"></span>
## Customizing the style of the disabled comment text box

After disabling the comment text box and setting the placeholder text for the disabled comment text box using the `disabledCommentConfig` parameter, you can customize the style, such as the background color, corner radius, border width, border color, and placeholder text color, of the disabled comment text box.

<span id="338e09bc"></span>
### Supported platforms

This customization is supported on both PC and mobile platforms.

<span id="916710bc"></span>
### Demo

Here is how the effect looks, along with the corresponding sample code for customizing the style of the disabled comment text box.


<Tabs>
<Tab zoneid="m2rurMihpB" title="For PCs">
<TabTitle>For PCs</TabTitle>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c3820cf2ff5d4726b74c6bd0d985cd04~tplv-goo7wpa0wc-image.image) </span>

The sample code is as follows.

```HTML
<style>
    .bytelive-Chat-message-footer-input-box.bytelive-Chat-message-footer-input-box-disabled {
      background-color: lightcoral; // Changes the background color of the comment text box.
      border-radius: 16px; // Changes the corner radius of the comment text box.
      border: 5px dashed yellow; // Changes the border width and color of the comment text box. Here, dashed indicates a dashed border. Use solid instead for a solid border.
    
      textarea::placeholder {
        color: lightgreen !important; // Changes the color of the placeholder text in the comment text box.
      }
    }
</style>
```



</Tab>
<Tab zoneid="r55KodJm2m" title="For mobile devices">
<TabTitle>For mobile devices</TabTitle>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e9bc1069a942421d811c434eb5dd3277~tplv-goo7wpa0wc-image.image) </span>

The sample code is as follows.

```HTML
<style>
  .bytelive-InputBar-input-wrapper.bytelive-InputBar-input-wrapper-disabled {
    input::placeholder {
      color: lightgreen !important; // Changes the color of the placeholder text in the comment text box.
    }
  }

  .bytelive-InputBar-input-wrapper.bytelive-InputBar-input-wrapper-disabled
    input {
    background-color: lightcoral !important; // Changes the background color of the comment text box.
    border-radius: 5px !important; // Changes the corner radius of the comment text box.
    border: 5px dashed yellow; // Changes the border width and color of the comment text box. Here, dashed indicates a dashed border. Use solid instead for a solid border. 
  }
</style>
```



</Tab>
</Tabs>


<span id="9314659f"></span>
### Sample code

The sample code for configuring the `disabledCommentConfig` parameter is as follows. For more information on parameters, see [Web Viewer SDK: Parameters](https://docs.byteplus.com/docs/byteplus-livesaas/parameters).

```JavaScript
var webSDK = new window.ByteLiveWebSDK({
  activityId: 180025****643845, 
  token: 'AB**nK', 
  service: 'Demo', 
  mode: 1, 
  modules: [
    {
      id: 'player', // The page element ID. The player module will be embedded into this element.
      mode: 'player',
    },
    {
      id: 'menu', // The page element ID. The menu module will be embedded into this element.
      mode: 'menu',
    },
  ],
  options: {
    disabledCommentConfig: {
      disabled: true, // Disables the comment text box. Viewers cannot enter content when they click the comment text box. 
      placeholder: "Muted" // The placeholder text for the disabled comment text box. To configure multilingual placeholder texts, first enable the viewing page languages through the BytePlus Live console or server-side OpenAPI. Then, follow the order of "Simplified Chinese|English|Japanese|Traditional Chinese|Korean|Thai|Vietnamese|Arabic|Turkish|Spanish|Indonesian|Portuguese|Russian" and use "|" to separate the placeholder texts for each language. For example, if the enabled languages are Simplified Chinese and English, then the value of the parameter is "禁言中|Muted".
    }
  },
});

webSDK.on('error', console.log);
```


<span id="f3a0e201"></span>
## Customizing the error page

After you subscribe to the live concurrent viewers package, if the total peak concurrent users (PCU) of all your live rooms with the status of **Live** under your account exceeds the concurrency upper limit, an error page is displayed when viewers enter the viewing page.

For example, you have subscribed to a live concurrent viewers package designed for 300 viewers. Now, you have a total of 3 live rooms in the **Live** status under your account, with PCUs of 100, 150, and 200 respectively. The total PCU is now 450 (100+150+200), which exceeds the concurrency upper limit of 300 for your package. If a viewer tries to enter the viewing page when the total PCU exceeds 300, an error page is displayed.

<span id="df37fe88"></span>
### Supported platforms

This customization is supported on both PC and mobile platforms.

<span id="4a9ee5fa"></span>
### Demo

You can customize the text and image of the error page, as shown in the red box below.


<Tabs>
<Tab zoneid="iNHBrVkJ8d" title="For PCs">
<TabTitle>For PCs</TabTitle>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8f6e7ee09e024872aaa1088edf95ab82~tplv-goo7wpa0wc-image.image) </span>


</Tab>
<Tab zoneid="ISUAGJcaJV" title="For mobile devices">
<TabTitle>For mobile devices</TabTitle>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b64157c391864686bcc0b141e27e65c5~tplv-goo7wpa0wc-image.image) </span>


</Tab>
</Tabs>


Additionally, you can listen to the `activity.pcu` event and execute your own logic, such as redirecting viewers to your custom page, without displaying the default error page when the PCU exceeds the concurrency upper limit.

<span id="dad45aa8"></span>
### Sample code

The sample code is as follows.

```JavaScript
options: {
    pcuConfig:{
      text:'The event is so popular', // Your custom text.
      img:'https://example.com/image.image', // Your custom image.
    },
}
// Listen to the event that is triggered when a viewer enters the viewing page. Replace console.log with your own logic. When the PCU exceeds the concurrency upper limit, your own logic will be executed. 
webSDK.on('activity.pcu', console.log); 
```


For more information on the parameter and event, see [Web Viewer SDK: Parameters](https://docs.byteplus.com/docs/byteplus-livesaas/parameters) and [activity.pcu](https://docs.byteplus.com/docs/byteplus-livesaas/events#75c92017).
