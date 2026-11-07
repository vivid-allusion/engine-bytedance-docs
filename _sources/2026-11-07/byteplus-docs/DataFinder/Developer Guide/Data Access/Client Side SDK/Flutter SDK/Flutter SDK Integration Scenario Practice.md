---
title: "Flutter SDK Integration Scenario Practice"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Flutter_SDK_Integration_Scenario_Practice"
---

<span id="d79309ce"></span>
# Initialize related configuration

<span id="8628863e"></span>
## Manual start (separate from start)

By default, as shown in the initialization code below, the SDK starts automatically.

```Dart
import 'package:rangers_applog_flutter_plugin/rangers_applog_flutter_plugin.dart';

//Initialize the SDK
String appId = '{{APPID}}'; //replace with your own
String channel = '{{CHANNEL}}'; //Fill in the app download/distribution channel, for example iOS is generally'App Store'
bool enableEncrypt = true; //encryption switch
bool enableDebugLog = false; //native log switch
bool enableAB = false; //AB test switch

//Set the data upload address, assuming domestic - North China
String? host = 'https://gator.volces.com';

RangersApplogFlutterPlugin.addInitParams({
    'service_vendor': 'private', //fixed value private
});

RangersApplogFlutterPlugin.initRangersAppLog(appId, channel, enableAB, enableEncrypt, enableDebugLog, host);
```


If you need to separate initialization and start, you need to explicitly set autoStart to false to tell the SDK to only initialize and wait for subsequent calls to start.

```Dart
import 'package:rangers_applog_flutter_plugin/rangers_applog_flutter_plugin.dart';

//Initialize the SDK
String appId = '{{APPID}}'; //replace with your own
String channel = '{{CHANNEL}}'; //Fill in the app download/distribution channel, for example iOS is generally'App Store'
bool enableEncrypt = true; //encryption switch
bool enableDebugLog = false; //native log switch
bool enableAB = false; //AB test switch

//Set the data upload address, assuming domestic - North China
String? host = 'https://gator.volces.com';

RangersApplogFlutterPlugin.addInitParams({
    'service_vendor': 'private', //fixed value private
    'autoStart': false, //Set to false and wait for subsequent calls to start
});

RangersApplogFlutterPlugin.initRangersAppLog(appId, channel, enableAB, enableEncrypt, enableDebugLog, host);

//then start
RangersApplogFlutterPlugin.start();
```


<span id="c984e5ef"></span>
# event public property

If you want to include a property in each event, you can set it through a public property, without having to set it repeatedly in each event. Public properties only need to be set once to be included in all code event tracking events, preset events, and full event tracking events.

<span id="e1f7faa7"></span>
### Set public properties

Please note about customizing "public properties":


1. The reporting mechanism is submitted with each log sending, and the default log sending frequency is 1 minute, so if the custom public properties are continuously modified within one minute, the last modification before the log sending shall prevail;

2. It is not recommended to modify it frequently, such as once per second.


```Dart
import 'package:rangers_applog_flutter_plugin/rangers_applog_flutter_plugin.dart';

//Set a custom public property, the property name is key_public, and the property value is value_public
RangersApplogFlutterPlugin.setHeaderInfo({
    "key_public": "value_public"
});
```


<span id="faf87c35"></span>
### Remove public attributes

```Dart
import 'package:rangers_applog_flutter_plugin/rangers_applog_flutter_plugin.dart';

//Example: Remove a public property named key_public
RangersApplogFlutterPlugin.removeHeaderInfo("key_public");
```


<span id="9a42dd8b"></span>
# user_unique_id and user attributes

<span id="9c02a701"></span>
## user login settings

<span id="fa0eaf3e"></span>
### user login

If your product has an account system, please set the uuid immediately after the user logs in to ensure the consistency of the user's login before and after.

```Dart
import 'package:rangers_applog_flutter_plugin/rangers_applog_flutter_plugin.dart';

//Set the ID of your account system when logging in and ensure its uniqueness
RangersApplogFlutterPlugin.setUserUniqueId('{{USER_UNIQUE_ID}}');
```


<span id="df89e22c"></span>
### user logout

Called when the account is logged out.

```Dart
import 'package:rangers_applog_flutter_plugin/rangers_applog_flutter_plugin.dart';

//Set uuid to null when logging out
RangersApplogFlutterPlugin.setUserUniqueId(null);
```


<span id="d4d81dd9"></span>
## Set user properties

<span id="68c6bb44"></span>
### profileSet

Set user properties, override if they exist, and create if they don't.

```Dart
import 'package:rangers_applog_flutter_plugin/rangers_applog_flutter_plugin.dart';

//Example: Set the user property, the property name is key, and the property value is value
RangersApplogFlutterPlugin.profileSet({"key": "value"});
```


<span id="5033d8b5"></span>
### profileSetOnce

Set user properties, if they exist, they will not be set, and if they do not exist, they will be created. They are suitable for first\-time related user properties, such as first access time, etc.

```Dart
import 'package:rangers_applog_flutter_plugin/rangers_applog_flutter_plugin.dart';

//Example: Set a user property with the property name key_once and the property value value_once
RangersApplogFlutterPlugin.profileSetOnce({"key_once": "value_once"});
```


<span id="171ab082"></span>
### profileIncrement

Set the properties of the numeric type to accumulate.

```Dart
import 'package:rangers_applog_flutter_plugin/rangers_applog_flutter_plugin.dart';

//Example: Set the user property, the property name is key, and the property value is 1
RangersApplogFlutterPlugin.profileIncrement({"key": 1});
```


<span id="4279eefb"></span>
### profileAppend

Set the user properties of the List type to be continuously added to the List.

```Dart
import 'package:rangers_applog_flutter_plugin/rangers_applog_flutter_plugin.dart';

//Example: Set the user property, the property name is key, the original property value, now add the property value as value_append
RangersApplogFlutterPlugin.profileAppend({"key": "value_append"});
```


<span id="62632b09"></span>
### profileUnset

Delete the user's attributes.

```Dart
import 'package:rangers_applog_flutter_plugin/rangers_applog_flutter_plugin.dart';

//Example: Delete user attribute named key
RangersApplogFlutterPlugin.profileUnset("key");
```


<span id="98068314"></span>
# Get platform ID

<span id="8565a50f"></span>
## Get the platform generation ID

Please note that deviceid is a volcanic ID, not an original device ID.

```Dart
import 'package:rangers_applog_flutter_plugin/rangers_applog_flutter_plugin.dart';

//Please start fetching after 3 seconds of initialization completion, otherwise it may return empty
String did = await RangersApplogFlutterPlugin.getDeviceId();
```


<span id="5c3795fe"></span>
# Full event tracking scenario

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Minimum supported version: 1.4.0</div>


<span id="9cb5bdca"></span>
## complete code example

```dart
import 'package:rangers_applog_flutter_plugin/autotrack.dart';
// ...

class _MyAppState extends State<MyApp> {
    @override
    void initState() {
      RangersApplogAutoTrack().config(RangersApplogAutoTrackConfig(
        pageConfigs: [
          RangersApplogAutoTrackPageConfig<Home>(
            pageID: 'home-id',
            pageTitle: 'Home',
            pagePath: '/home-custom',
            ignore: false,
          ),
          RangersApplogAutoTrackPageConfig<Page2>(
            pageID: 'page2-id',
          ),
          RangersApplogAutoTrackPageConfig<Page3>(
            pageID: 'page3-id',
          ),
        ],
        ignoreElementKeys: [],
      )).enablePageLeave().enableLog().enable();
      super.initState();
    }
    
    // ...
    @override
    Widget build(BuildContext context) {
      return MaterialApp(
        navigatorObservers: RangersApplogNavigationObserver.wrap([]),
        initialRoute: '/',
        routes: {
          '/': ((context) => Home()),
          '/page2': ((context) => Page2()),
          '/page3': ((context) => Page3()),
        },
      );
    }
}
```


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning"><strong>Add navigatorObservers to MaterialApp</strong></div>


In the full event tracking pageview, pageleave is collected by NavigatorObserver, we can directly configure RangersApplogNavigationObserver in MaterialApp:

```Dart
import 'package:rangers_applog_flutter_plugin/autotrack.dart';

// ...
@override
Widget build(BuildContext context) {
  return MaterialApp(
    navigatorObservers: [RangersApplogNavigationObserver()],
    // ...
  );
}
// ...
```


You can also RangersApplogNavigationObserver the package in the existing navigatorObservers list:

```Dart
import 'package:rangers_applog_flutter_plugin/autotrack.dart';

// ...
@override
Widget build(BuildContext context) {
  return MaterialApp(
    navigatorObservers: RangersApplogNavigationObserver.wrap([]),
    // ...
  );
}
// ...
```


<span id="cd0b7c5a"></span>
## Use full event tracking


* ### Enable full event tracking   <span id="enable-full-event-tracking"></span>


Enable full event tracking in the app's `initState ()`:

```Dart
import 'package:rangers_applog_flutter_plugin/autotrack.dart';

// ...
@override
void initState() {
    RangersApplogAutoTrack().enable();
    super.initState();
}
// ...
```



* ### Full event tracking switch   <span id="full-event-tracking-switch"></span>


Full event tracking is turned off by default and can be turned on by the following methods:

```Dart
import 'package:rangers_applog_flutter_plugin/autotrack.dart';

RangersApplogAutoTrack().enable();
```


Turn off full event tracking:

```Dart
import 'package:rangers_applog_flutter_plugin/autotrack.dart';

RangersApplogAutoTrack().disable();
```



* ### PageView switch   <span id="pageview-switch"></span>


PageView is turned on by default and can be turned off by the following methods:

```Dart
import 'package:rangers_applog_flutter_plugin/autotrack.dart';

RangersApplogAutoTrack().disablePageView();
```


Open the pageview:

```Dart
import 'package:rangers_applog_flutter_plugin/autotrack.dart';

RangersApplogAutoTrack().enablePageView();
```



* ### Pageleave switch   <span id="pageleave-switch"></span>


Pageleave is turned off by default and can be turned on by the following methods (imported parameter is true, or not passed):

```Dart
import 'package:rangers_applog_flutter_plugin/autotrack.dart';

RangersApplogAutoTrack().enablePageLeave();
```


Close the pageleave:

```Dart
import 'package:rangers_applog_flutter_plugin/autotrack.dart';

RangersApplogAutoTrack().disablePageLeave();
```



* ### Click switch   <span id="click-switch"></span>


Click on the default on, you can use the following methods to close:

```Dart
import 'package:rangers_applog_flutter_plugin/autotrack.dart';

RangersApplogAutoTrack().disableClick();
```


Open click:

```Dart
import 'package:rangers_applog_flutter_plugin/autotrack.dart';

RangersApplogAutoTrack().enableClick();
```



* ### Set the custom ID of the click element   <span id="set-the-custom-id-of-the-click-element"></span>


We set the customized ID of the element through the Key. The customized ID will be reported together in the `element_manual_key`field in the click event tracking. The value is the return value of the `toString ()`method of the Key, which can be used directly `RangersApplogElementKey`.

Elements that trigger click event tracking currently support the following components:


* GestureDetector

* InkWell

* ElevatedButton

* ListTile


For components outside the support list, the customized ID cannot be set by Key, and clicking event tracking will trigger on the GestureDetector inside the component.

```Dart
import 'package:rangers_applog_flutter_plugin/autotrack.dart';

...
ListTile(
  key: RangersApplogElementKey('custom-key'),
  title: Text("Click Me"),
  onTap: () {}
)
...
```



* ### Ignore the click element   <span id="ignore-the-click-element"></span>


If you don't want to count the click event tracking of certain elements, you can ignore the click element by:

By RangersApplogElementKey setting ignore:

```Dart
import 'package:rangers_applog_flutter_plugin/autotrack.dart';

...
ListTile(
  key: RangersApplogElementKey('custom-key', ignore: true),
  title: Text("Click Me"),
  onTap: () {},
)
...
```


Specify the key of the element with the `ignoreElementKeys ()`method:

```Dart
import 'package:rangers_applog_flutter_plugin/autotrack.dart';

...
final customKey = RangersApplogElementKey('custom-key');

...
RangersApplogAutoTrack().ignoreElementKeys([customKey]);

...
ListTile(
  key: customKey,
  title: Text("Click Me"),
  onTap: () {},
)
...
```


The `ignoreElementStringKeys ()`method specifies the string value of the element key, as long as it matches the `toString ()`return value of the key, it is recommended to use RangersApplogElementKey:

```Dart
import 'package:rangers_applog_flutter_plugin/autotrack.dart';

...
RangersApplogAutoTrack().ignoreElementStringKeys(['custom-key']);

...
ListTile(
  key: RangersApplogElementKey('custom-key'),
  title: Text("Click Me"),
  onTap: () {},
)
...
```



* ### open log   <span id="open-log"></span>


Logging is turned off by default and can be turned on in the following ways:

```Dart
import 'package:rangers_applog_flutter_plugin/autotrack.dart';

RangersApplogAutoTrack().enableLog();
```


<span id="b99a2585"></span>
## Related configuration (optional)


* **pageConfigs:**  Parameters used to configure pages, affecting pageview, pageleave event tracking. The type of the page needs to be specified, and the configuration will only take effect on the specified page.

   * **pageID:**  The customized ID of the page, which will be reported in the `page_manual_key`field in pageview and pageleave event tracking.

   * **pageTitle:**  The title of the page, if not configured, use the title specified in the AppBar, and use the configured value first after configuration. In pageview, pageleave event tracking is reported in the `page_title`field.

   * **pagePath:**  the path of the page, if not configured, use the path configured by routes in MaterialApp, and use the configured value first after configuration. In pageview, pageleave event tracking is reported in the `page_path`field.

   * **Ignore:**  Default to false, set to true will ignore the current page's pageview, pageleave event tracking.

* **ignoreElementKeys:**  Ignore the click event tracking of the element specified by Key in the imported parameter.

* **ignoreElementStringKeys:**  Ignore the click event tracking of the element specified by string in the imported parameter, the match type is that the string content must be the same as the `toString ()`return value of the element key.

* **enablePageView:**  Default to true, set to false will turn off all pageview event tracking.

* **enablePageLeave:**  Default to false, set to true to enable all pageleave event tracking.

* **enableClick:**  Default is true, setting to false will turn off all click event tracking.


example

```Dart
import 'package:rangers_applog_flutter_plugin/autotrack.dart';

RangersApplogAutoTrack().config(RangersApplogAutoTrackConfig(
  pageConfigs: [
    RangersApplogAutoTrackPageConfig<Home>(
      pageID: 'home-id',
      pageTitle: 'Home',
      pagePath: '/home-custom',
      ignore: false,
    ),
    RangersApplogAutoTrackPageConfig<Page2>(
      pageID: 'page2-id',
    ),
    RangersApplogAutoTrackPageConfig<Page3>(
      pageID: 'page3-id',
    ),
  ],
  ignoreElementKeys: [],
  ignoreElementStringKeys: [],
  enablePageView: true,
  enablePageLeave: false,
  enableClick: true,
));
```
