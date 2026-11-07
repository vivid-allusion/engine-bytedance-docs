---
title: "React Native SDK Integration Scenario Practice"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/React_Native_SDK_Integration_Scenario_Practice"
---

<span id="d79309ce"></span>
# Event public property

If you want to include a property in each event, you can set it through a public property, without having to set it repeatedly in each event. Public properties only need to be set once to be included in all code event tracking events, preset events, and full event tracking events.

<span id="e1f7faa7"></span>
### Set public properties

Please note about customizing "public properties":


1. The reporting mechanism is submitted with each log sending, and the default log sending frequency is 1 minute, so if the custom public properties are continuously modified within one minute, the last modification before the log sending shall prevail;

2. It is not recommended to modify it frequently, such as once per second.

   ```TypeScript
   import { NativeModules } from 'react-native';
   const { RangersAppLogModule } = NativeModules;
   
   //Example: Set a custom public property with the property name key_public and the property value value_public
   RangersAppLogModule.setHeaderInfo({
       "key_public": "value_public"
   });
   ```
   


<span id="faf87c35"></span>
### Remove public attributes

```TypeScript
import { NativeModules } from 'react-native';
const { RangersAppLogModule } = NativeModules;

//Example: Set a custom public property with the property name key_public and the property value value_public
RangersAppLogModule.removeHeaderInfo("key_public");
```


<span id="9a42dd8b"></span>
# user_unique_id and user attributes

<span id="9c02a701"></span>
## user login settings

<span id="fa0eaf3e"></span>
### user login

If your product has an account system, please set the uuid immediately after the user logs in to ensure the consistency of the user's login before and after.

```TypeScript
import { NativeModules } from 'react-native';
const { RangersAppLogModule } = NativeModules;

//Set the ID of your account system when logging in and ensure its uniqueness
RangersAppLogModule.setUserUniqueId('{{USER_UNIQUE_ID}}');
```


<span id="df89e22c"></span>
### user logout

Called when the account is logged out.

```TypeScript
import { NativeModules } from 'react-native';
const { RangersAppLogModule } = NativeModules;

//Set uuid to null when logging out
RangersAppLogModule.setUserUniqueId(null);
```


<span id="d4d81dd9"></span>
## Set user properties

<span id="68c6bb44"></span>
### profileSet

Set user properties, override if they exist, and create if they don't.

```TypeScript
import { NativeModules } from 'react-native';
const { RangersAppLogModule } = NativeModules;

//Example: Set the user property, the property name is key, and the property value is value
RangersAppLogModule.profileSet({"key": "value"});
```


<span id="5033d8b5"></span>
### profileSetOnce

Set user properties, if they exist, they will not be set, and if they do not exist, they will be created. They are suitable for first\-time related user properties, such as first access time, etc.

```TypeScript
import { NativeModules } from 'react-native';
const { RangersAppLogModule } = NativeModules;

//Example: Set a user property with the property name key_once and the property value value_once
RangersAppLogModule.profileSetOnce({"key_once": "value_once"});
```


<span id="171ab082"></span>
### profileIncrement

Set the properties of the numeric type to accumulate.

```TypeScript
import { NativeModules } from 'react-native';
const { RangersAppLogModule } = NativeModules;

//Example: Set the user property, the property name is key, and the property value is 1
RangersAppLogModule.profileIncrement({"key": 1});
```


<span id="4279eefb"></span>
### profileAppend

Set the user properties of the collection type to continuously add to the collection.

```TypeScript
import { NativeModules } from 'react-native';
const { RangersAppLogModule } = NativeModules;

//Example: Set the user property, the property name is key, the original property value, now add the property value as value_append
RangersAppLogModule.profileAppend({"key": "value_append"});
```


<span id="62632b09"></span>
### profileUnset

Delete the user's attributes.

```TypeScript
import { NativeModules } from 'react-native';
const { RangersAppLogModule } = NativeModules;

//Example: Delete a user attribute named key
RangersAppLogModule.profileUnset("key");
```


<span id="98068314"></span>
# Get platform ID

<span id="8565a50f"></span>
## Get the platform generation ID

Please note that device_id is a volcano generated ID, not an original device ID.

```TypeScript
import { NativeModules } from 'react-native';
const { RangersAppLogModule } = NativeModules;

//Example: Get did
let didPromise = RangersAppLogModule.getDeviceID();
didPromise.then((deviceID) => {
    console.log(deviceID);
});
```


<span id="5c3795fe"></span>
# Full event tracking scenario

> You can refer to this demo with full event tracking. Note: When using the demo, please replace the app_id and reported domain names with your own.

> <Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f92b3b560cf24275aab043c900342084~tplv-goo7wpa0wc-image.image" name="ReactNavigationExample_带全埋点.zip">ReactNavigationExample_带全埋点.zip</Attachment>



<span id="9cb5bdca"></span>
## React Native side requirements

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Minimum version requirements to support full event tracking:</div>



* <div data-tips="true" data-tips-type="tip">react\-native ≥ 0.62.0</div>


* <div data-tips="true" data-tips-type="tip">react\-navigation ≥ 6.0.0</div>


   <div data-tips="true" data-tips-type="tip">React\-navigation currently only supports navigators:   </div>
   

   * <div data-tips="true" data-tips-type="tip">Stack</div>


   * <div data-tips="true" data-tips-type="tip">Native Stack</div>


   * <div data-tips="true" data-tips-type="tip">Bottom Tabs</div>


      <div data-tips="true" data-tips-type="tip">Note: Mixing other unsupported navigators may affect event tracking      </div>
      


Version correspondence:


|React version |rangers_applog_reactnative_plugin version |Finder sdk version |
|---|---|---|
|< 17 |≥ 0.2.0 |≥ 6.14.1 |
|≥ 17 |0.2.13\-rc.0 |≥ 6.14.1 |


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">React 17 and above introduces <a href="https://zh-hans.legacy.reactjs.org/blog/2020/09/22/introducing-the-new-jsx-transform.html">jsx tr</a></div>


<div data-tips="true" data-tips-type="warning"><a href="https://zh-hans.legacy.reactjs.org/blog/2020/09/22/introducing-the-new-jsx-transform.html">Ansform </a>, please use 0.2.13 and above versions of rangers_applog_reactnative_plugin for compatibility, and need to introduce the babel plugin as follows (react 17 can be ignored below)</div>


<div data-tips="true" data-tips-type="warning">```JavaScript
//babel.config.js
plugins: ['rangers_applog_reactnative_plugin/plugins/babel-plugin-jsx-hook.js']
```
</div>


<span id="b8d9c45b"></span>
## Native Android side code and requirements

Application integration, or Lifecycle integration, choose one of the two methods.

<span id="47ae9a90"></span>
### Application Integration

In the Application file (default is MainApplication.java), change the inherited Application to RangersAppLogApplication:

```java
import com.reactnativerangersapplogreactnativeplugin.RangersAppLogApplication;

public class MainApplication extends RangersAppLogApplication implements ReactApplication {
    // ...
}
```


<span id="2f45e338"></span>
### Integration via Lifecycle

In the Application file (default MainApplication.java), in the onCreate hook method, register RangersAppLogActivityLifecycle.

**Note: If you choose to integrate through Lifecycle, the current Application cannot inherit RangersAppLogApplication.** 

```java
import com.reactnativerangersapplogreactnativeplugin.RangersAppLogActivityLifecycle;
// ...

public class MainApplication extends Application implements ReactApplication {
    @Override
    public void onCreate() {
      super.onCreate();
      registerActivityLifecycleCallbacks(new RangersAppLogActivityLifecycle());
    }
}
```


<span id="f1fb71d2"></span>
## Use full event tracking

<span id="25a85407"></span>
### Enable full event tracking

Enable full event tracking in the entry file index.js:

```TypeScript
import { autoTrack } from 'rangers_applog_reactnative_plugin';
// ...

AppRegistry.registerComponent(appName, () => App);
autoTrack.enable();
```


<span id="261f9edf"></span>
### Full event tracking switch

Full event tracking is turned off by default and can be turned on by the following methods (imported parameter is true, or not passed):

```TypeScript
import { autoTrack } from 'rangers_applog_reactnative_plugin';

autoTrack.enable();
```


Turn off full event tracking:

```TypeScript
import { autoTrack } from 'rangers_applog_reactnative_plugin';

autoTrack.enable(false);
```


<span id="a8b7d7c2"></span>
### PageView switch

PageView is enabled by default, and can be enabled by the following methods (imported parameter is true, or not passed)

```TypeScript
import { autoTrack } from 'rangers_applog_reactnative_plugin';

autoTrack.enablePageView();
```


Close the pageview

```TypeScript
import { autoTrack } from 'rangers_applog_reactnative_plugin';

autoTrack.enablePageView(false);
```


<span id="e5e2b613"></span>
### Pageleave switch

Pageleave is turned off by default and can be turned on by the following methods (imported parameter is true, or not passed)

```TypeScript
import { autoTrack } from 'rangers_applog_reactnative_plugin';

autoTrack.enablePageLeave();
```


Close the pageleave

```TypeScript
import { autoTrack } from 'rangers_applog_reactnative_plugin';

autoTrack.enablePageLeave(false);
```


<span id="9630d991"></span>
### Click switch

Click to open by default, you can open it by the following methods (imported parameter is true, or not passed)

```TypeScript
import { autoTrack } from 'rangers_applog_reactnative_plugin';

autoTrack.enableClick();
```


Close click

```TypeScript
import { autoTrack } from 'rangers_applog_reactnative_plugin';

autoTrack.enableClick(false);
```


<span id="4aa5ca0c"></span>
### React navigation switch

React navigation is enabled by default, and can be enabled by the following methods (imported parameter is true, or not passed)

```TypeScript
import { autoTrack } from 'rangers_applog_reactnative_plugin';

autoTrack.enableReactNavigation();
```


Close the react navigation, and no longer collect the react navigation page after closing

```TypeScript
import { autoTrack } from 'rangers_applog_reactnative_plugin';

autoTrack.enableReactNavigation(false);
```


<span id="74f17f0d"></span>
## Related configuration (optional)

<span id="6d13b8ac"></span>
### custom parameters

You can configure some custom parameters to carry when the full event tracking report:


* **BindEvent:**  used to bind pageview information. After the pv event of full event tracking is triggered, all events triggered through RangersAppLogModule.onEventV3 will be added with page_key, page_manual_key event properties. Default is false.

* **pageTitleProp:**  Used to set the property name (props key) of the custom title.

* **elementIdProp:**  The property name (props key) used to set the customized ID of the click element.

* **elementCustomProp:**  The property name (props key) used to set the custom parameters of the clicked element.

* **Pages:**  Custom parameters used to configure RN pages (pages registered through AppRegistry), affecting event tracking events for pageview and pageleave.

* **ReactNavigation:**  Custom parameters used to configure ReactNavigation pages (pages registered with react navigation), affecting event tracking events for pageview, pageleave.


example

```TypeScript
import { autoTrack } from 'rangers_applog_reactnative_plugin';

autoTrack.config({
  bindEvent: false,
  pageTitleProp: 'rangers-app-log-title',
  elementIdProp: 'rangers-app-log-id',
   elementCustomProp: 'rangers-app-log-custom',
  pages: [
    {
      appKey: appName,
      pageID: 'app',
      pagePath: '/',
      ignore: false
    },
  ],
  reactNavigation: {
    combineApp: true,
    disableApp: true,
    screens: [
      {
        screenName: 'Home',
        pageID: 'navigationpage-home',
        pagePath: '/navigationpage/home',
        ignore: false
      },
    ]
  }
})
```


<span id="1a9b50d7"></span>
### Configure RN page


* **appKey:**  The appKey defined when registering a page through AppRegistry, which is the unique identifier of the page.

* **pageID:**  In pageview, the `page_manual_key`attribute of the pageleave event takes this field.

* **pagePath:**  In pageview, the `page_path`attribute of the pageleave event takes this field.

* **Ignore:**  In the pageview, pageleave event, whether to ignore the page. If set to true, the page is ignored and will not be in the referring page. Default is false.


example

```TypeScript
import { autoTrack } from 'rangers_applog_reactnative_plugin';

autoTrack.config({
  pages: [
    {
      appKey: appName,
      pageID: 'app',
      pagePath: '/',
      ignore: false
    },
  ],
  // ...
})
```


<span id="6c1a219a"></span>
### Configure ReactNavigation Page

The following configuration is used only if the react navigation switch is turned on:


* **CombineApp:**  Whether to treat the initial screen page and the rn page to which it belongs as the same page and share the refer information. When true, the initial screen page refers to the same information as the RN page to which it belongs. When false, the initial screen page refers to the rn page to which it belongs. Default is true.

* **DisableApp:**  Whether to disable event tracking on the rn page to which the screen belongs. When true, disable the event tracking of the rn page to which the screen belongs, and use the screen page information instead of the rn page in the jump link at the same level as the rn page. When false, the rn page to which the screen belongs triggers event tracking normally. Default is true.

* **ScreenName:**  The name specified for screen when registering a page with react navigation, which is the unique identifier of the page.

* **pageID:**  In pageview, the `page_manual_key`attribute of the pageleave event takes this field.

* **pagePath:**  In pageview, the `page_path`attribute of the pageleave event takes this field.

* **Ignore:**  In the pageview, pageleave event, whether to ignore the page. If set to true, the page is ignored and will not be in the referring page. Default is false.


example

```TypeScript
import { autoTrack } from 'rangers_applog_reactnative_plugin';

autoTrack.config({
  // ...
  reactNavigation: {
    combineApp: true,
    disableApp: true,
    screens: [
      {
        screenName: 'Home',
        pageID: 'navigationpage-home',
        pagePath: '/navigationpage/home',
        ignore: false
      },
    ]
  }
})
```


<span id="c5ab3f28"></span>
### Configure custom properties of components

**Configuration page custom title**

In pageview, the `page_title`attribute of the pageleave event takes the title value.

After setting the property, the title automatically fetches the content of the component:

```TypeScript
<Text rangers-app-log-title>App Page</Text>
```


You can also set the title value directly for this property:

```TypeScript
<Text rangers-app-log-title="App">App Page</Text>
```


If multiple components on the page have a title set, the last component loaded will prevail.

The property name defaults to: rangers\-app\-log\-title, if you need to modify it, please refer to the above `custom parameter`content.

**Configure the customized ID of the click element**

The `element_manual_key`attribute of the click event carries the title value.

```TypeScript
<TouchableOpacity rangers-app-log-id="页面1-确认" onPress={testPress}> //page1-confirm
    <Text>确认</Text> //confirm
</TouchableOpacity>
```


The property name defaults to: rangers\-app\-log\-id, if you need to modify it, please refer to the above `custom parameter`content.

**Configure custom parameters for click elements**

The value is carried in the `custom`property of the click event.

```TypeScript
<TouchableOpacity rangers-app-log-custom={{mykey:"myvalue"}} onPress={testPress}>
    <Text>确认</Text> //confirm
</TouchableOpacity>
```


The property name defaults to: rangers\-app\-log\-custom, if you need to modify it, please refer to the above `custom parameter`content.

<span id="0ca87dc0"></span>
### Set custom parameters for the page

After setting the custom attribute of the page, the value will be displayed in the `page_custom`attribute of the pageview event

**Set up RN page**

Set custom parameters for RN pages through initialProperties

`iOS`Setting method reference:

```objectivec
//When creating an RN page, the initialProperties passed in will be placed in the pv event tracking page_custom
NSDictionary *initialProperties = @{@"mykey": @"myvalue"};
RCTRootView *rootView = [[RCTRootView alloc] initWithBridge:[BridgeManager shared].bridge
                                                   moduleName:moduleName
                                            initialProperties:initialProperties];
```


`Android`setting method reference:

```java
@Overrideprotected ReactActivityDelegate createReactActivityDelegate() {
    return new ReactActivityDelegate(this, getMainComponentName()) {
        @Nullable@Overrideprotected Bundle getLaunchOptions() {
            Bundle initialProps = new Bundle();
            initialProps.putString("mykey", "myvalue");
            return initialProps;
        }
    };
}
```


**Set up ReactNavigation page**

Set custom parameters for the ReactNavigation page through route.params of navigation

```TypeScript
//When jumping through navigation, the incoming parameters will be placed in the pv event tracking page_custom
navigation.navigate('DetailScreen', { detailId: 12 });
```


<span id="d44666b9"></span>
# Circle function

Version requirements that support circling:


|react\-native version |rangers_applog_reactnative_plugin version |Finder sdk version |
|---|---|---|
|< 0.69.0 |≥ 0.2.4 |≥ 6.14.1 |
|≥ 0.69.0 |0.2.13\-rc.0 |≥ 6.14.1 |


Circle function dependencies:


1. React Native full event tracking function, you need to ensure that full event tracking is turned on

2. iOS/Android circle selection function, you need to integrate the circle selection module to complete the circle selection configuration


The sample code is as follows. In the entry file index.js, the initPicker method needs to be executed before importing the react\-native library to ensure the successful circling (because the circling needs to be injected through devtools, importing the react\-native library and then executing it will cause the injection to fail).

**Note:**  When you do not need to use the circling function, please remove the initPicker method, which may affect the rendering efficiency

```TypeScript
import { autoTrack } from '@dp/rangers_applog_reactnative_plugin';
autoTrack.initPicker();

import { AppRegistry } from 'react-native';
// register app root component
AppRegistry.registerComponent(appName, () => App);

autoTrack.enable();
```


After that, press the ios/android circle selection process to start the circle selection. When entering the React Native page, the information of the circle selection page will automatically become the React Native page & component information.
