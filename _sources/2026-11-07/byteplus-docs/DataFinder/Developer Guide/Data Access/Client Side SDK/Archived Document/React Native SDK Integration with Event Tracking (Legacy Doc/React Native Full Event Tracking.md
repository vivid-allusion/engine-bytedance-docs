---
title: "React Native Full Event Tracking"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/React_Native_Full_Event_Tracking"
---

<span id="_1-接入全埋点"></span>
# 1. Access full event tracking

<span id="_1-1-js-代码"></span>
## 1.1 JavaScript Code

Minimum version requirements to support full event tracking:


* react\-native ≥ 0.62.0

* react\-navigation ≥ 6.0.0


Version correspondence:


|React version |rangers_applog_reactnative_plugin version |Finder sdk version |
|---|---|---|
|< 17 |≥ 0.2.0 |≥ 6.14.1 |
|≥ 17 |0.2.13\-rc.0 |≥ 6.14.1 |


React\-navigation currently only supports navigators:


* Stack

* Native Stack

* Bottom Tabs


Note: Mixing other unsupported navigators may affect event tracking

```shell
npm install rangers_applog_reactnative_plugin
```


<span id="_1-2-android-代码"></span>
## 1.2 Android Code

Application integration, or Lifecycle integration, choose one of the two methods.

<span id="_1-2-1-通过-application-集成"></span>
### 1.2.1 through Application Integration

In the Application file (default is MainApplication.java), change the inherited Application to RangersAppLogApplication:

```java
import com.reactnativerangersapplogreactnativeplugin.RangersAppLogApplication;

public class MainApplication extends RangersAppLogApplication implements ReactApplication {
    ...
}
```


<span id="_1-2-2-通过-lifecycle-集成"></span>
### 1.2.2 integration via Lifecycle

In the Application file (default MainApplication.java), in the onCreate hook method, register RangersAppLogActivityLifecycle.

**Note: If you choose to integrate through Lifecycle, the current Application cannot inherit RangersAppLogApplication.** 

```java
import com.reactnativerangersapplogreactnativeplugin.RangersAppLogActivityLifecycle;
...

public class MainApplication extends Application implements ReactApplication {
    @Override
    public void onCreate() {
      super.onCreate();
      registerActivityLifecycleCallbacks(new RangersAppLogActivityLifecycle());
    }
}
```


**Note: React 17 and above introduces** [jsx transform ](https://zh-hans.legacy.reactjs.org/blog/2020/09/22/introducing-the-new-jsx-transform.html) **. For compatibility, please use 0.2.13 and above versions of rangers_applog_reactnative_plugin, and you need to introduce the babel plugin as follows (react 17 can be ignored below)** 

```JavaScript
//babel.config.js
plugins: ['rangers_applog_reactnative_plugin/plugins/babel-plugin-jsx-hook.js']
```


<span id="_2-使用全埋点"></span>
# 2. Use full event tracking

<span id="_2-1-启用全埋点"></span>
## 2.1 Enable full event tracking

Enable full event tracking in the entry file index.js:

```javascript
import { autoTrack } from 'rangers_applog_reactnative_plugin';
...

AppRegistry.registerComponent(appName, () => App);
autoTrack.enable();
```


<span id="_2-2-全埋点开关"></span>
## 2.2 Full event tracking switch

Full event tracking is turned off by default and can be turned on by the following methods (imported parameter is true, or not passed):

```javascript
import { autoTrack } from 'rangers_applog_reactnative_plugin';

autoTrack.enable();
```


Turn off full event tracking:

```javascript
import { autoTrack } from 'rangers_applog_reactnative_plugin';

autoTrack.enable(false);
```


<span id="_2-3-pageview-开关"></span>
## 2.3 pageview switch

PageView is turned on by default and can be turned off by the following methods:

```javascript
import { autoTrack } from 'rangers_applog_reactnative_plugin';

autoTrack.enablePageView(false);
```


Open the pageview:

```javascript
import { autoTrack } from 'rangers_applog_reactnative_plugin';

autoTrack.enablePageView();
```


<span id="_2-4-pageleave-开关"></span>
## 2.4 pageleave switch

Pageleave is turned off by default and can be turned on by the following methods (imported parameter is true, or not passed):

```javascript
import { autoTrack } from 'rangers_applog_reactnative_plugin';

autoTrack.enablePageLeave();
```


Close the pageleave:

```javascript
import { autoTrack } from 'rangers_applog_reactnative_plugin';

autoTrack.enablePageLeave(false);
```


<span id="_2-5-click-开关"></span>
## 2.5 click switch

Click on the default on, you can use the following methods to close:

```javascript
import { autoTrack } from 'rangers_applog_reactnative_plugin';

autoTrack.enableClick(false);
```


Open click:

```javascript
import { autoTrack } from 'rangers_applog_reactnative_plugin';

autoTrack.enableClick();
```


<span id="_2-5-react-navigation-开关"></span>
## 2.5 react navigation switch

React navigation is enabled by default and can be turned off by the following methods:

No more reacting navigation pages after closing.

```javascript
import { autoTrack } from 'rangers_applog_reactnative_plugin';

autoTrack.enableReactNavigation(false);
```


Turn on react navigation:

```javascript
import { autoTrack } from 'rangers_applog_reactnative_plugin';

autoTrack.enableReactNavigation();
```


<span id="_3-1-配置（可选）"></span>
# 3.1 Configuration (optional)

<span id="_3-1-示例"></span>
## 3.1 Example

You can configure some custom parameters to carry when the full event tracking report:

**BindEvent:**  used to bind pageview information. After the pv event of full event tracking is triggered, all events triggered through RangersAppLogModule.onEventV3 will be added with page_key, page_manual_key event properties. Default is false.

**pageTitleProp:**  Used to set the property name (props key) of the custom title.

**elementIdProp:**  The property name (props key) used to set the customized ID of the click element.

**elementCustomProp:**  The property name (props key) used to set the custom parameters of the clicked element.

**Pages:**  Custom parameters used to configure RN pages (pages registered through AppRegistry), affecting event tracking events for pageview and pageleave.

**ReactNavigation:**  Custom parameters used to configure ReactNavigation pages (pages registered with react navigation), affecting event tracking events for pageview, pageleave.

```javascript
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


<span id="_3-2-配置-rn-页面"></span>
## 3.2 Configuring the RN page

**appKey:**  The appKey defined when registering a page through AppRegistry, which is the unique identifier of the page.

**pageID:**  In pageview, the `page_manual_key`attribute of the pageleave event takes this field.

**pagePath:**  In pageview, the `page_path`attribute of the pageleave event takes this field.

**Ignore:**  In the pageview, pageleave event, whether to ignore the page. If set to true, the page is ignored and will not be in the referring page. Default is false.

```javascript
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
  ...
})
```


<span id="_3-3-配置-reactnavigation-页面"></span>
## 3.3 Configuring the ReactNavigation page

The following configuration is used only if the react navigation switch is turned on:

**CombineApp:**  Whether to treat the initial screen page and the rn page to which it belongs as the same page and share the refer information. When true, the initial screen page refers to the same information as the RN page to which it belongs. When false, the initial screen page refers to the rn page to which it belongs. Default is true.

**DisableApp:**  Whether to disable event tracking on the rn page to which the screen belongs. When true, disable the event tracking of the rn page to which the screen belongs, and use the screen page information instead of the rn page in the jump link at the same level as the rn page. When false, the rn page to which the screen belongs triggers event tracking normally. Default is true.

**ScreenName:**  The name specified for screen when registering a page with react navigation, which is the unique identifier of the page.

**pageID:**  In pageview, the `page_manual_key`attribute of the pageleave event takes this field.

**pagePath:**  In pageview, the `page_path`attribute of the pageleave event takes this field.

**Ignore:**  In the pageview, pageleave event, whether to ignore the page. If set to true, the page is ignored and will not be in the referring page. Default is false.

```javascript
import { autoTrack } from 'rangers_applog_reactnative_plugin';

autoTrack.config({
  ...,
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


<span id="_3-4-配置组件的自定义属性"></span>
## 3.4 Configuring custom properties of components

<span id="_3-4-1-配置页面自定义-title"></span>
### Customize title 3.4.1 configuration page

In pageview, the `page_title`attribute of the pageleave event takes the title value.

After setting the property, the title automatically fetches the content of the component:

```javascript
<Text rangers-app-log-title>App Page</Text>
```


You can also set the title value directly for this property:

```javascript
<Text rangers-app-log-title="App">App Page</Text>
```


If multiple components on the page have a title set, the last component loaded will prevail.

The property name defaults to: rangers\-app\-log\-title. If you need to modify it, please refer to Section 3.1.

<span id="_3-4-2-配置点击元素的自定义-id"></span>
### 3.4.2 configure the customized ID of the clicked element

The `element_manual_key`attribute of the click event carries the title value.

```javascript
<TouchableOpacity rangers-app-log-id="页面1-确认" onPress={testPress}> //page1-confirm
    <Text>确认</Text> //confirm
</TouchableOpacity>
```


The property name defaults to: rangers\-app\-log\-id. If you need to modify it, please refer to Section 3.1.

<span id="_3-4-3-配置点击元素的自定义参数"></span>
### 3.4.3 configure custom parameters for clickable elements

The value is carried in the `custom`property of the click event.

```javascript
<TouchableOpacity rangers-app-log-custom={{mykey:"myvalue"}} onPress={testPress}>
    <Text>确认</Text> //confirm
</TouchableOpacity>
```


The property name defaults to: rangers\-app\-log\-custom. If you need to modify it, please refer to Section 3.1.

<span id="_3-5-设置页面的自定义参数"></span>
## 3.5 Set the custom parameters of the page

After setting the custom attribute of the page, the value will be displayed in the `page_custom`attribute of the pageview event

<span id="_3-5-1-设置-rn-页面"></span>
### 3.5.1 settings RN page

Set custom parameters for RN pages through initialProperties

iOS setting method reference:

```objectivec
// When creating an RN page, the initialProperties passed in will be placed in the page_custom of the PV event tracking point
NSDictionary *initialProperties = @{@"mykey": @"myvalue"};
RCTRootView *rootView = [[RCTRootView alloc] initWithBridge:[BridgeManager shared].bridge
                                                   moduleName:moduleName
                                            initialProperties:initialProperties];
```


Android setting method reference:

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


<span id="_3-5-2-设置-reactnavigation-页面"></span>
### 3.5.2 settings ReactNavigation page

Set custom parameters for the ReactNavigation page through route.params of navigation

```javascript
//When jumping through navigation, the incoming parameters will be placed in the pv event tracking page_custom
navigation.navigate('DetailScreen', { detailId: 12 });
```


<span id="_4-圈选功能"></span>
# 4. Circle selection function

<span id="_4-1-启用圈选"></span>
## 4.1 Enable Circle Selection

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

```javascript
import { autoTrack } from '@dp/rangers_applog_reactnative_plugin';
autoTrack.initPicker();

import { AppRegistry } from 'react-native';
// register app root component
AppRegistry.registerComponent(appName, () => App);

autoTrack.enable();
```


After that, press the ios/android circle selection process to start the circle selection. When entering the React Native page, the information of the circle selection page will automatically become the React Native page & component information.
