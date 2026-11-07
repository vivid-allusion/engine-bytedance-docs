---
title: "Integrate Mini Program Pro SDK"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Integrate_Mini_Program_Pro_SDK"
---

This article describes how mini programs can integrate the SDK provided by Application Performance Management Plus and directly use the products and services on the platform.

<span id=".5L2_55So6ZmQ5Yi2"></span>
## Usage Limits

SDK request addresses vary by region. For details, refer to the client SDK access addresses in the [server-launching region](https://docs.byteplus.com/en/docs/apmplus/server-launching_region) section.

<span id=".5q2l6aqk5LiA77ya5o6l5YWlU0RL"></span>
## Step 1: Integrate the SDK

<span id=".5Y6f55Sf5bCP56iL5bqP5o6l5YWl"></span>
### Native mini program integration

<span id=".Q0pT77yI5o6o6I2Q77yJ"></span>
#### CJS recommended

Compared to NPM, the CJS integration method eliminates the need to build NPM.


1. Obtain the SDK

   * [WeChat Platform SDK address](https://apm.volccdn.com/mars-web/apmplus/mini_program/wx.cn.cjs.js)

   * [Douyin Platform SDK address](https://apm.volccdn.com/mars-web/apmplus/mini_program/tt.cn.cjs.js)

   * [Alipay platform SDK address](https://apm.volccdn.com/mars-web/apmplus/mini_program/my.cn.cjs.js)

   * [Baidu platform SDK address](https://apm.volccdn.com/mars-web/apmplus/mini_program/swan.cn.cjs.js)

   * [Lark platform SDK address](https://apm.volccdn.com/mars-web/apmplus/mini_program/lark.cn.cjs.js)

      Copy the contents from the SDK directory and place them in the `minipro/monitor/apmplus.js` file.

2. Integrate and initialize.

   * Integration using the node module (require) method

      Add the following content to the `app.js` file to complete initialization.

      ```JavaScript
      // app.js
      const client = require('./monitor/apmplus.js');
      client.init({
        aid: 123, // Replace with your aid
        token:'xxx-xxx' // Replace with your token
      })    
      client.start()
      
      // App({...})
      ```
      

   * Integrate using the ES module (import) method

      Add the following content to the `app.js` file to complete initialization.

      ```javascript
      // app.js
      import client from './monitor/apmplus.js'
      client.init({
        aid: 123, // Replace with your aid
        token:'xxx-xxx' // Replace with your token
      })    
      client.start()
      
      // App({...})
      ```
      


<span id="NPM"></span>
#### NPM

Integrating the SDK using the NPM method requires introducing the adaptation layer for the specified mini program.

The adaptation layers for all platforms are as follows:


* WeChat Mini Program platform: WxAdapter

* TikTok Mini Program platform: TtAdapter

* Alipay Mini Program platform: MyAdapter

* Baidu Mini Program platform: SwanAdapter

* Lark mini program platform: LarkAdapter


For example, on the WeChat Mini Program platform, WxAdapter is introduced, which can effectively reduce unnecessary code redundancy. The following uses WeChat Mini Program as an example to describe the steps for integrating the SDK using the NPM method.


1. Integrate a mini program with NPM

   Each Mini Program platform has its own method for integrating NPM. For example: [WeChat Mini Program NPM integration guide](https://developers.weixin.qq.com/miniprogram/dev/devtools/npm.html).

2. Install NPM.

   ```Bash
   npm install @apmplus/mini-program
   ```
   

3. Add the following code to the `app.js` file to integrate and initialize.

   ```JavaScript
   // app.js
   import { createMiniProgramClient, WxAdapter } from '@apmplus/mini-program'
   const client = createMiniProgramClient([WxAdapter])
   client.init({
     aid: 123, // Replace with your aid
     token:'xxx-xxx' // Replace with your token
   })
   client.start()
   
   // App({...})
   ```
   


<span id=".5LiJ5pa55qGG5p625o6l5YWl"></span>
### Third\-party framework integration

<span id=".TlBN77yI5o6o6I2Q77yJ"></span>
#### NPM (recommended)

```bash
npm install @apmplus/mini-program
```


<span id="Taro"></span>
#### Taro

Taro supports building WeChat Mini Program, TikTok Mini Program, Alipay Mini Program, Baidu Mini Program, and Lark Mini Program.


* If your product is a platform, take **WeChat Mini Program** as an example.

   Add the following content to the `app.js` file to complete initialization.

   ```javascript
   // app.js
   import { createMiniProgramClient, WxAdapter } from '@apmplus/mini-program';
   
   const client = createMiniProgramClient([WxAdapter]);
   if (client) {
     client.init({
       aid: 123, // Replace with your aid
       token:'xxx-xxx' // Replace with your token
     });
     client.start();
   }
   // class App extends Component {
   ```
   

* If your product targets **multiple platforms**, you can use the [TARO_ENV environment variable method](https://taro-docs.jd.com/docs/envs#processenvtaro_env) to import the correct adaptation layer as needed.

   For example, you need to compile outputs for two platforms: WeChat Mini Program and TikTok Mini Program.

   1. Add the corresponding WeChat Mini Program file `wx.js`.

      ```javascript
      // wx.js
      import { createMiniProgramClient, WxAdapter } from '@apmplus/mini-program'
      const client = createMiniProgramClient([WxAdapter])
      export default client
      ```
      

   2. Add the corresponding file for the TikTok Mini Program`tt.js`.

      ```typescript
      // tt.js
      import { createMiniProgramClient, TtAdapter } from '@apmplus/mini-program'
      const client = createMiniProgramClient([TtAdapter])
      export default client
      ```
      

   3. In `app.js`, dynamically import the specified file based on the environment name TARO_ENV.

      ```javascript
      // app.js
      let client
      if (process.env.TARO_ENV === 'weapp') {
        client = require('./wx').default
      } else if (process.env.TARO_ENV === 'tt') {
        client = require('./tt').default
      }
      if (client) {
        client.init({
          aid: 123, // Replace with your aid
          token:'xxx-xxx' // Replace with your token
        })
        client.start()
      }
      // class App extends Component {
      ```
      

* If your product includes the **Alipay Mini Program** platform, you need to configure an additional **integration**.

   ```javascript
   import Taro from '@tarojs/taro';
   import { createMiniProgramClient, MyAdapter, FrameworksAdapterIntegration } from '@apmplus/mini-program';
   const client = createMiniProgramClient([MyAdapter]);
   if (client) {
     client.init({
       aid: 123, // Replace with your AID
       token:'xxx-xxx' // Replace with your token
       integrations: [FrameworksAdapterIntegration({ Taro })],
     });
     client.start();
   }
   ```
   


<span id="Uni app"></span>
#### Uni app

Uni app also supports output as WeChat Mini Program, TikTok Mini Program, Alipay Mini Program, Baidu Mini Program, and Lark Mini Program. If your product targets **multiple platforms**, you can use [conditional compilation](https://uniapp.dcloud.net.cn/tutorial/platform.html#preprocessor) to import the correct adaptation layer as needed. Sample code is as follows:

```javascript
import { createMiniProgramClient, WxAdapter, TtAdapter } from '@apmplus/mini-program'

const getCorrectAdapter = () => {
  switch (process.env.VUE_APP_PLATFORM) {
    case 'mp-weixin':
      return [WxAdapter]
    case 'mp-toutiao':
      return [TtAdapter]
    default:
      return null
  }
}

const client = createMiniProgramClient(getCorrectAdapter())
if (client) {
  client.init({
    aid: 123, // Replace with your aid
    token:'xxx-xxx' // Replace with your token
  })
  client.start()
}
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Different Uni App versions lead to different environment variable names, so the code should be optimized based on the specific business scenario.</div>


<span id=".5q2l6aqk5LqM77ya6K6-572u5ZCI5rOV5Z-f5ZCN"></span>
## Step 2: Setting valid domain name

Below, WeChat Mini Program is used as an example to introduce the detailed steps for setting valid domain names.


1. Log in to [WeChat Mini Program Background](https://mp.weixin.qq.com/).

2. In the left navigation bar, select **Development \> Development management**.

3. Click the **Developer settings** tab. In the **Server domain name** area, click **Edit**.

4. On the **authentication** page, the administrator completes authentication.

5. On the **configure server domain name** page, after you **request a valid domain name**, enter **https://apmplus.volces.com**, and then click **Save and Submit**.


<span id=".77yI5Y-v6YCJ77yJ5q2l6aqk5LiJ77ya6K-m57uG6YWN572u"></span>
## (Optional) Step 3: Detailed configuration

```JavaScript
export type InitOptions = {
  aid: number // Application ID, required parameter
  token: string // Token to apply, required parameter
  userId?: string // Manual user ID
  deviceId?: string // Device ID
  useLocalConfig?: boolean = false // Whether to use local configuration. If the setting is set to true, platform configuration sampling will not be fetched.
  domain?: string // The private deployment method field is required; enter the deployment domain name
  plugins?: Plugins // Plugin configuration. For details, see the "Plugin Configuration" Documentation.
  integrations?: Integration[] // Integration configuration, used when ensuring compatibility with Taro Alipay Mini Program. For details, see the "On-demand loading integration" documentation.
}
```


<span id=".5q2l6aqk5Zub77ya6aqM6K-B5LiK5oql"></span>
## Step 4: Verify reporting

All integrated mini program platforms can use the following methods to verify whether the SDK has been successfully integrated.

Using the WeChat Mini Program as an example, the detailed procedure is described.


1. Log in to the [WeChat Mini Program Background](https://mp.weixin.qq.com/).

2. In the left navigation bar, select **Developer Tools \> Network**.

3. Observe the circumstances under which page requests are triggered.

   Trigger at least the following two requests to indicate successful integration. After a short wait, the platform will also display the corresponding data.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_674558cdafc8426e5b7fd8e8b93a4b71.png) </span>


<span id=".5rOo5oSP5LqL6aG5"></span>
### Precautions


* Whenever possible, initialize the SDK before initializing the App, so that developers can obtain more comprehensive information. If you need to wait for an interface to issue data before configuring the userId and reporting, refer to [API Reference](https://docs.byteplus.com/en/docs/apmplus/Call_an_API_using_the_SDK).

* The device information obtained via getSystemInfo differs between debugging in the developer tool and debugging on a real device (online). The specific differences are as follows:

   * mver: Mini Program version

   * menv：Mini program environment

   * model: Device model

   * brand: device brand
