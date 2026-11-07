---
title: "Flutter SDK Full Event Tracking"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Flutter_SDK_Full_Event_Tracking"
---

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The Flutter SDK integration documentation has been revised, please check the new documentation: <a href="https://docs.byteplus.com/docs/DataFinder/Flutter_SDK_Integration">Flutter SDK Integration</a>.</div>


<span id="_1-接入全埋点"></span>
# 1. Access full event tracking

Minimum supported version: 1.4.0

<span id="_1-1-完整-demo"></span>
## 1.1 Full Demo

```dart
import 'package:rangers_applog_flutter_plugin/autotrack.dart';
...

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
    
    ...
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


<span id="_1-2-materialapp-中增加-navigatorobservers"></span>
## 1.2 Adding navigatorObservers to MaterialApp

In the full event tracking pageview, pageleave is collected by NavigatorObserver, we can directly configure RangersApplogNavigationObserver in MaterialApp:

```dart
import 'package:rangers_applog_flutter_plugin/autotrack.dart';

...
@override
Widget build(BuildContext context) {
  return MaterialApp(
    navigatorObservers: [RangersApplogNavigationObserver()],
    ...
  );
}
...
```


You can also RangersApplogNavigationObserver the package in the existing navigatorObservers list:

```dart
import 'package:rangers_applog_flutter_plugin/autotrack.dart';

...
@override
Widget build(BuildContext context) {
  return MaterialApp(
    navigatorObservers: RangersApplogNavigationObserver.wrap([]),
    ...
  );
}
...
```


<span id="_2-使用全埋点"></span>
# 2. Use full event tracking

<span id="_2-1-启用全埋点"></span>
## 2.1 Enable full event tracking

Enable full event tracking in the app's `initState ()`:

```dart
import 'package:rangers_applog_flutter_plugin/autotrack.dart';

...
@override
  void initState() {
    RangersApplogAutoTrack().enable();
    super.initState();
  }
  ...
```


<span id="_2-2-全埋点开关"></span>
## 2.2 Full event tracking switch

Full event tracking is turned off by default and can be turned on by the following methods:

```javascript
import 'package:rangers_applog_flutter_plugin/autotrack.dart';

RangersApplogAutoTrack().enable();
```


Turn off full event tracking:

```javascript
import 'package:rangers_applog_flutter_plugin/autotrack.dart';

RangersApplogAutoTrack().disable();
```


<span id="_2-3-pageview-开关"></span>
## 2.3 pageview switch

PageView is turned on by default and can be turned off by the following methods:

```javascript
import 'package:rangers_applog_flutter_plugin/autotrack.dart';

RangersApplogAutoTrack().disablePageView();
```


Open the pageview:

```javascript
import 'package:rangers_applog_flutter_plugin/autotrack.dart';

RangersApplogAutoTrack().enablePageView();
```


<span id="_2-4-pageleave-开关"></span>
## 2.4 pageleave switch

Pageleave is turned off by default and can be turned on by the following methods (imported parameter is true, or not passed):

```javascript
import 'package:rangers_applog_flutter_plugin/autotrack.dart';

RangersApplogAutoTrack().enablePageLeave();
```


Close the pageleave:

```javascript
import 'package:rangers_applog_flutter_plugin/autotrack.dart';

RangersApplogAutoTrack().disablePageLeave();
```


<span id="_2-5-click-开关"></span>
## 2.5 click switch

Click on the default on, you can use the following methods to close:

```javascript
import 'package:rangers_applog_flutter_plugin/autotrack.dart';

RangersApplogAutoTrack().disableClick();
```


Open click:

```javascript
import 'package:rangers_applog_flutter_plugin/autotrack.dart';

RangersApplogAutoTrack().enableClick();
```


<span id="_2-6-设置-click-元素的自定义id"></span>
## 2.6 Set the custom ID of the click element

We set the customized ID of the element through the Key. The customized ID will be reported together in the `element_manual_key`field in the click event tracking. The value is the return value of the `toString ()`method of the Key, which can be used directly `RangersApplogElementKey`.

Elements that trigger click event tracking currently support the following components:


* GestureDetector

* InkWell

* ElevatedButton

* ListTile


For components outside the support list, the customized ID cannot be set by Key, and clicking event tracking will trigger on the GestureDetector inside the component.

```dart
import 'package:rangers_applog_flutter_plugin/autotrack.dart';

...
ListTile(
  key: RangersApplogElementKey('custom-key'),
  title: Text("Click Me"),
  onTap: () {}
)
...
```


<span id="_2-7-忽略-click-元素"></span>
## 2.7 Ignoring the click element

If you don't want to count the click event tracking of certain elements, you can ignore the click element by:

By RangersApplogElementKey setting ignore:

```dart
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

```dart
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

```dart
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


<span id="_2-8-开启日志"></span>
## 2.8 Open log

Logging is turned off by default and can be turned on in the following ways:

```dart
import 'package:rangers_applog_flutter_plugin/autotrack.dart';

RangersApplogAutoTrack().enableLog();
```


<span id="_3-1-配置（可选）"></span>
# 3.1 Configuration (optional)

<span id="_3-1-示例"></span>
## 3.1 Example


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


```dart
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
