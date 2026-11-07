---
title: "Best practice"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-best-practice"
---

When playing on mobile devices, we provide the following recommendations to improve compatibility, optimize real\-time streaming, and offer styling configuration methods suitable for mobile devices.

<span id="3f8f7725"></span>
## RTM Playback Lag Optimization

To improve playback smoothness under unstable network conditions, you can adjust the buffer delay setting. Below are two common integration methods:


<Tabs>
<Tab zoneid="n2RBMkJQG0" title="From CDN">
<TabTitle>From CDN</TabTitle>

When creating a player instance, configure the `delayHint` parameter in the RTM module. Code example:

```JavaScript
VePlayer.createLivePlayer({
    url: 'XXXX.sdp',
    rtm: {
        //Set buffer delay to 1s
        delayHint: 1
    }
}) 
```



</Tab>
<Tab zoneid="MCMYNjWfIx" title="By NPM">
<TabTitle>By NPM</TabTitle>

When creating a player instance, configure the `delayHint` parameter in the RTM module. Code example:

```JavaScript
import { createLivePlayer, register } from '@byteplus/veplayer';
import { rtm } from '@byteplus/veplayer-plugin';
import '@byteplus/veplayer/style'

register([rtm]);

createLivePlayer({
    url: 'XXXX.sdp',
    rtm: {
        // Set buffer delay to 1s
        delayHint: 1
    }
})
```



</Tab>
</Tabs>


<span id="6c8ea845"></span>
## Mobile Device Styling Configuration

If you need to remove the default H5 styles on mobile devices, you can follow the steps below.

<span id="43301374"></span>
### Removing certain icons

You can remove unwanted plugin icons by configuring the `ignores` option. This allows you to customize the icons displayed on the player interface, such as removing the `start`, `enter`, and `unmute` buttons.

<span id="6a1820b4"></span>
### Removing H5 shadow overlay effects

By default, the H5 player may display shadow overlay effects on the top and bottom of the video area, as shown in the image below.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/696ee2f4c3974c7d8ea29ac0ec5f90df~tplv-goo7wpa0wc-image.image) </span>

If you wish to remove this overlay effect, you can configure it using the following code.

```JavaScript
mobile: {
    gradient: 'none',
}
```


<span id="24e3a121"></span>
### Customizing error message

If you are using the default error display plugin, there are two ways to customize error messages.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/58d79030e8fc4e8682a6a48b463c1683~tplv-goo7wpa0wc-image.image) </span>


<Tabs>
<Tab zoneid="NEmNH2GCw6" title="Override All Error Messages">
<TabTitle>Override All Error Messages</TabTitle>

To override all error messages with a single custom message, configure the `errorTipsText` parameter in the `error` section, as shown below:

```JavaScript
error: {
  errorTipsText: { 'en': 'Custom Error Info' }
}
```



</Tab>
<Tab zoneid="qiCSy9mRU7" title="Customize Messages for Specific Errors">
<TabTitle>Customize Messages for Specific Errors</TabTitle>

To define custom messages for specific error types, configure them in the `i18n` section:

```JavaScript
i18n: {
          texts:{
            'en': {
              MEDIA_ERR_ABORTED: 'Custom Error Info', // corresponding to error code 5101 or 1
              MEDIA_ERR_NETWORK:  'Custom Error Info', // corresponding to error code 5102 or 2
              MEDIA_ERR_DECODE: 'Custom Error Info', // corresponding to error code 5103 or 3
              MEDIA_ERR_SRC_NOT_SUPPORTED: 'Custom Error Info', // corresponding to error code 5104 or 4
              NETWORK: 'Custom Error Info', // corresponding to error code 2100
              NETWORK_TIMEOUT: 'Custom Error Info', //  corresponding to error code 2101
              NETWORK_FORBIDDEN: 'Custom Error Info', //  corresponding to error code 2103
              NETWORK_NOTFOUND: 'Custom Error Info', //  corresponding to error code 2104
            }
          }
        },
```



</Tab>
</Tabs>
