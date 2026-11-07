---
title: "Reference: Web/JavaScript SDK FAQ"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Reference_Web_JavaScript_SDK_FAQ"
---

<span id="e96d50cb"></span>
# Web SDK reporting logic and storage policies

<span id="web-sdk数据上报策略"></span>
## Web SDK data reporting strategy

Default "near real\-time" event reporting, the SDK uses a queue, waiting for 30ms, events triggered within the waiting time will be combined into one request for reporting, if the wait time of 30ms is not reached, and the number of events reaches 10, it will be merged into one request for reporting immediately. You can change the number of bars by setting the max_report parameter (10 is the default).

<span id="7b35371d"></span>
## web_id request logic

web_id a webid request is made to the server ( **https://xxxx/webid** ) when the sdk is initialized, that is, when the init method is called

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_34b80788fc03234ea41aff8086eea549.png) </span>

The request parameters are: app_id, the current URL, the referer of the URL, the useragent of the current browser, and user_unique_id (usually null), which mainly depends on the appid and the current environment. The request will generate a unique webid return at the server level, as shown below:

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_213588c058ffd259d63a4fb0e43cf98c.png) </span>

After getting the web_id, it will be cached locally. As long as the appid and domain name remain unchanged, the cache will not be manually cleared, and the server will no longer be requested to obtain web_id.

<span id="72c328fa"></span>
## User ID Storage Logic for Web SDK

After the WebSDK initialization is complete, the webid/user_unique_id is stored in the browser's localStorage (under the domain name of the current page) by default, as long as the user does not manually clear the browser's cache, then this storage will be permanent, and the value will not change.

In some special scenarios, such as when you need to count information across subdomain (a.b.com and c.b.com) pages, you can turn on the cookie storage switch of the SDK (see the function configuration of the SDK for details). At this time, the SDK will store the webid/user_unique_id in the browser's cookie (the default expiration time is 7 days, which can be changed through configuration). This stored value will not change until the cookie has expired. After the cookie expires, or if the user manually clears the browser's cookies, the SDK will regenerate the webid.

<span id="947f0f89"></span>
## Web SDK session id generation and storage logic


1. When a user first accesses a page, the SDK initializes and generates a sessionid, stores the sessionid in the sessionstorage, and records the generated timestamp.

2. Every time this page has an event trigger (user active trigger + SDK automatic report trigger), update the timestamp of sessionid in sessionstorage.

3. When there is no action on the same page for 30 minutes (the user does not trigger event reporting, and the SDK does not automatically report any events), the sessionid is considered expired, a new sessionid is generated, and the timestamp of the sessionid is updated.

4. When a button in the page is clicked to open a new window, a new session is generated according to the sessionstorage.

5. When the page is closed, empty the sessionstorage and open the page again to generate a new sessionid.

6. During the sessionid valid period, each event is reported with sessionid as a public parameter.


<span id="91bd55b6"></span>
## bav2b_beat page heartbeat event collection logic

The page heartbeat event is accessed on the page, stopped for 500ms after scrolling the page, and reported once when leaving the page. For details, please refer to the 2.4.4 chapter of the document[Web/JS SDK Classification Function](https://docs.byteplus.com/docs/DataFinder/Web_JS_SDK_Classification_Function).

<span id="1f122b9d"></span>
# Web SDK capabilities and usage consulting

<span id="a7af2cac"></span>
## Web multi\-page application integration SDK, public property should be reported for each page?

Initialization and public properties Each page needs to be written once, user_unique_id will be cached, set once.

<span id="e87db7e3"></span>
## Web micro frontend project, the main application and sub\-applications are connected to different applications (app_id different), is there any solution in this scenario?

It can be solved by multiple instances, please refer to this document for details: see [3. Web/JS multi-instance usage](https://docs.byteplus.com/docs/DataFinder/Web_JS_SDK_Classification_Function#_3-web-js-%E5%A4%9A%E5%AE%9E%E4%BE%8B%E4%BD%BF%E7%94%A8).

<span id="ff586623"></span>
## When there are multiple web page domains, how to connect the WebID across domain names to keep the WebID unchanged?


* When opening WebIDs across subdomains, such as `a.yourdomain.com`and `b.yourdomain.com`:

   When integrating and initializing the SDK, you can configure the **cross_subdomain** parameters to automatically identify anonymous users using the same browser in multiple subdomains as the same user when set to true. Please see for details [3.5 Initialization configuration list](https://docs.byteplus.com/docs/DataFinder/Web_JavaScript_SDK_Integration_#_3-5-%E5%88%9D%E5%A7%8B%E5%8C%96%E9%85%8D%E7%BD%AE%E4%B8%80%E8%A7%88%E8%A1%A8).

* When connecting WebIDs across web sites, such as `yourdomain.com .cn`and `yourdomain.com .hk`:

   * When you integrate and initialize the SDK, turn on and configure custom webid to unify the webid of web pages across multiple sites by manually setting the webid. Please see for details [3.4 Custom webid](https://docs.byteplus.com/docs/DataFinder/Web_JavaScript_SDK_Event_Tracking_and_Properties#_3-4-%E8%87%AA%E5%AE%9A%E4%B9%89webid).


<span id="7496c20c"></span>
## Integrated Web/JavaScript SDK How to view user's SSID?

```javascript
//Get various IDs generated by the platform
window.collectEvent('getToken', (res) => {
    console.log(res)
}); 
 
 window.collectEvent('getToken', (token) => {
    The token data content is similar to the following:
    // {
    //    "web_id":"6748002161499735560",
    //    "ssid":"579bc89a-bd45-4021-8314-669c35f38e3d",
    //    "user_unique_id":"xxx",
    // }
    window.collectEvent('test', {
      id: `web_id/ssid的值` //the value of web_id/ssid
    });
});
```


<span id="d1fd8b0f"></span>
## Does the Web SDK have the ability to collect page crashes?

No, the Web SDK only collects data for event tracking, not page errors. If you need to collect page crashes, you can guide customers to buy apm products.

<span id="b90997ed"></span>
## What is the scope of the Web SDK Circle event?

The circling rule restricts filtering when an element has more than 2 layers of child elements. If you want to circle an outer element, it is recommended not to have more than 2 layers of child elements.

<span id="e856f13b"></span>
## Web/JS SDK access, if you do not actively report data, what data will be collected by default?

As long as the SDK is integrated and the initialization is completed, the preset events and properties will be collected. Please refer to the documentation for details: [Web Preset Events and Properties](https://docs.byteplus.com/docs/DataFinder/Web_Preset_Events_and_Properties).

If you need to collect full event tracking data, you can turn on the full event tracking switch, full event tracking event description: see [Full Event Tracking Preset Events and Properties](https://docs.byteplus.com/docs/DataFinder/Full_Event_Tracking_Preset_Events_and_Properties).

<span id="28fdd175"></span>
## What is the meaning of the reportTime and max_report parameters of the Web SDK?

The event tracking report policy is divided into two types, the default max_report is 10, the first type, the number of event tracking triggered within 30ms is greater than 10, and it is directly reported; the second type, if there is no trigger within 30ms, it will wait for 30ms and then report the previous event tracking together.

<span id="4a0a65e2"></span>
## What is the difference between "total_duration" and "duration"?

Duration is the active time, which simply means the time the user actually uses it.

total_duration is the total time the page was open to close, including the time the user switched pages without actually using them. For example, minimization, background, etc., switching the page will be understood as "leaving the page" and a close event will be reported at this time.

<span id="6df053cf"></span>
## The difference between predefine_pageview and bav2b_page?


* predefine_pageview is a preset page access event for Web and Mini Programs, mobile end does not;

* bav2b_page is a full event tracking page access event, as long as the switch is turned on, it will be collected;

* For the Web platform, the two are also different, bav2b_page is the event of the full event tracking report, the spa parameter is false, bav2b_page the routing switch of the single\-page application will also be reported, predefine_pageview will only report once when the page is opened. SPA is true, bav2b_page and predefine_pageview are the same, after the JS SDK 5.0 version, bav2b_page and predefine_pageview reporting are unified.


<span id="596e479b"></span>
## Does collectEvent have a ts type definition?

```TypeScript
interface IInitParam {
  app_id: number;
  channel?: 'cn' | 'va' | 'sg';
  channel_domain?: string;
  app_key?: string;
  caller?: string;
  log?: boolean;
  disable_webid?: boolean;
  disable_sdk_monitor?: boolean;
  disable_storage?: boolean;
  autotrack?: any;
  enable_stay_duration?: any;
  disable_route_report?: boolean;
  disable_session?: boolean;
  disable_heartbeat?: boolean;
  disable_auto_pv?: boolean;
  enable_spa?: boolean;
  user_unique_type?: string;
  enable_ab_test?: boolean;
  max_storage_num?: number;
  enable_storage?: boolean;
  enable_cookie?: boolean;
  enable_ab_visual?: boolean;
  cross_subdomain?: boolean;
  cookie_domain?: string;
  enable_multilink?: boolean;
  multilink_timeout_ms?: number;
  reportTime?: number;
  timeout?: number;
  max_report?: number;
  report_url?: string;
  maxDuration?: number;
  ab_channel_domain?: string;
  configPersist?: number;
  extend?: any;
  ab_timeout?: number;
  disable_tracer?: boolean;
  extendConfig?: any;
  filter?: any;
  spa?: boolean;
  cookie_expire?: number;
  enable_custom_webid?: boolean;
  disable_track_event?: boolean;
  allow_hash?: boolean;
  enable_native?: boolean;
  ab_cross?: boolean;
  ab_cookie_domain?: string;
  disable_ab_reset?: boolean;
  enable_encryption?: boolean;
  enable_anonymousid?: boolean
  enable_debug?: boolean
  crypto_publicKey?: string
  encryption_type?: string
  encryption_header?: string
  enable_logsetting?: boolean
  enable_track_id?: boolean
  track_level?: number
  overlay_opacity?: number
  auto_exposure_expriment?: boolean
}


interface IConfigParam {
  _staging_flag?: 0 | 1;
  user_unique_id?: string;
  disable_auto_pv?: boolean;
  web_id?: string;
  user_type?: number;
  os_name?: string;
  os_version?: string;
  device_model?: string;
  ab_client?: string;
  ab_version?: string;
  ab_sdk_version?: string;
  traffic_type?: string;
  utm_source?: string;
  utm_medium?: string;
  utm_campaign?: string;
  utm_term?: string;
  utm_content?: string;
  platform?: string;
  browser?: string;
  browser_version?: string;
  region?: string;
  province?: string;
  city?: string;
  language?: string;
  timezone?: number;
  tz_offset?: number;
  screen_height?: number;
  screen_width?: number;
  referrer?: string;
  referrer_host?: string;
  os_api?: number;
  creative_id?: number;
  ad_id?: number;
  campaign_id?: number;
  ip_addr_id?: number;
  user_agent?: string;
  verify_type?: string;
  sdk_version?: string;
  channel?: string;
  app_id?: number;
  app_name?: string;
  app_version?: string;
  app_install_id?: number;
  user_id?: any;
  device_id?: any;
  wechat_openid?: string,
  wechat_unionid?: string,
  evtParams?: EventParams,
  reportErrorCallback?(eventData: any, errorCode: any): void;
  [key: string]: any;
}


type EventParams = Record<string, any>;


export type SdkOption = Omit<IInitParam, 'app_id'>;


export type SdkHookListener = (hookInfo?: any) => void;


export interface Plugin {
  apply(sdk: Sdk, options: SdkOption): void;
}
export interface PluginConstructor {
  new(): Plugin;
  pluginName?: string;
  init?(Sdk: SdkConstructor): void;
}


declare enum SdkHook {
  Init = 'init',
  Config = 'config',
  Start = 'start',
  Ready = 'ready',
  TokenComplete = 'token-complete',
  TokenStorage = 'token-storage',
  TokenFetch = 'token-fetch',
  TokenError = 'token-error',
  ConfigUuid = 'config-uuid',
  ConfigWebId = 'config-webid',
  ConfigDomain = 'config-domain',
  CustomWebId = 'custom-webid',
  TokenChange = 'token-change',
  TokenReset = 'token-reset',
  ConfigTransform = 'config-transform',
  EnvTransform = 'env-transform',
  SessionReset = 'session-reset',
  SessionResetTime = 'session-reset-time',
  Event = 'event',
  Events = 'events',
  EventNow = 'event-now',
  CleanEvents = 'clean-events',
  BeconEvent = 'becon-event',
  SubmitBefore = 'submit-before',
  SubmitScuess = 'submit-scuess',
  SubmitAfter = 'submit-after',
  SubmitError = 'submit-error',
  SubmitVerify = 'submit-verify',
  SubmitVerifyH = 'submit-verify-h5',
  Stay = 'stay',
  ResetStay = 'reset-stay',
  StayReady = 'stay-ready',
  SetStay = 'set-stay',
  RouteChange = 'route-change',
  RouteReady = 'route-ready',
  Ab = 'ab',
  AbVar = 'ab-var',
  AbAllVars = 'ab-all-vars',
  AbConfig = 'ab-config',
  AbExternalVersion = 'ab-external-version',
  AbVersionChangeOn = 'ab-version-change-on',
  AbVersionChangeOff = 'ab-version-change-off',
  AbOpenLayer = 'ab-open-layer',
  AbCloseLayer = 'ab-close-layer',
  AbReady = 'ab-ready',
  AbComplete = 'ab-complete',
  Profile = 'profile',
  ProfileSet = 'profile-set',
  ProfileSetOnce = 'profile-set-once',
  ProfileUnset = 'profile-unset',
  ProfileIncrement = 'profile-increment',
  ProfileAppend = 'profile-append',
  ProfileClear = 'profile-clear',
  TrackDuration = 'track-duration',
  TrackDurationStart = 'track-duration-start',
  TrackDurationEnd = 'track-duration-end',
  TrackDurationPause = 'track-duration-pause',
  TrackDurationResume = 'tracl-duration-resume',
  Autotrack = 'autotrack',
  AutotrackReady = 'autotrack-ready',
}
interface SdkConstructor {
  new(name: string): Sdk;
  instances: Array<Sdk>;
  usePlugin: (plugin: PluginConstructor, pluginName?: string) => void;
}
interface Sdk {
  Types: typeof SdkHook;
  on(type: string, hook: SdkHookListener): void;
  once(type: string, hook: SdkHookListener): void;
  off(type: string, hook?: SdkHookListener): void;
  emit(type: string, info?: any, wait?: string): void;
  init(options: IInitParam): void;
  config(configs?: IConfigParam): void;
  getConfig(key?: string): Record<string, any>;
  setDomain(domain: string): void;
  start(): void;
  send(): void;
  set(type: string): void;
  event(event: string, params?: EventParams): void;
  beconEvent(event: string, params?: EventParams): void;
  event(
    events:
      | Array<[string, EventParams] | [string, EventParams, number]>
  ): void;
  predefinePageView(params: any): void;
  clearEventCache(): void;
  setWebIDviaUnionID(unionId: string): void;
  setWebIDviaOpenID(openId): void;
  getToken(callback: (info: Record<string, string | number>) => void, timeout?: number): void;
  resetStayDuration(url_path?: string, title?: string, url?: string): void;
  resetStayParams(url_path?: string, title?: string, url?: string): void;
  profileSet(profile: any): void;
  profileSetOnce(profile: any): void;
  profileIncrement(profile: any): void;
  profileUnset(key: string): void;
  profileAppend(profile: any): void;
  startTrackEvent(eventName: string): void;
  endTrackEvent(eventName: string, params: any): void;
  pauseTrackEvent(eventName: string): void;
  resumeTrackEvent(eventName: string): void;
  setExternalAbVersion(vids: string): void;
  getVar(name: string, defaultValue: any, callback: (value: any) => void): void;
  getAllVars(callback: (value: any) => void): void;
  getAbSdkVersion(): string;
  onAbSdkVersionChange(callback: (vids: string) => void): () => void;
  offAbSdkVersionChange(callback: (vids: string) => void): void;
  setExternalAbVersion(vids: string | null): void;
  getABconfig(params: Record<string, any>, callback: (value: any) => void): void;
  openOverlayer(): void;
  closeOverlayer(): void;
  autoInitializationRangers(
    config: IInitParam & { onTokenReady: (webId: string) => void },
  ): void;
}

type FunctionKeysObject<T extends Record<string, any>> = {
  [K in keyof T]: T[K] extends Function ? T[K] : never
}
type InnerEventsMap = FunctionKeysObject<Sdk>
type CustomEventsMap = Record<string, (params?: Record<string, any>) => void>
type EventsMap = InnerEventsMap & CustomEventsMap
type CollectEvent = <T extends keyof EventsMap>(key: T, ...args: Parameters<EventsMap[T]>) => void

interface Window {
  collectEvent: CollectEvent
}
```


<span id="9f315aed"></span>
## What browsers does the Web SDK support?

As long as it is a standard browser environment that supports native JavaScript (no ES6 required), it can be used regardless of the operating system, platform type, browser type, or browser version. There is no guarantee that some niche browsers do not implement standard JavaScript, resulting in some property differences related to operating system, platform type, browser type, browser version.

Some features require relatively new browsers to support, such as batch sending requires LocalStorage storage. If some features (such as batch sending) are not supported in the version browser, the SDK will not report an error, but will automatically downgrade (use image sending), or remove this function.


|Browser |Support Notes |
|---|---|
|IE6～9 |IE7, IE8 limited support (only support event reporting, not view exposure), other versions of IE browser do not support |
|IE10～11 |✅ |
|Chrome |✅ |
|Safari |✅ |
|Edge |✅ |
|FireFox |✅ |
|Opera |✅ |


<span id="8085048d"></span>
## Is the web SDK compatible with old versions of IE browsers?

The js file with the core path (including base or other) is compatible with lower versions of IE browsers (below IE11).


* IE9 and above:

   * SaaS usage: https://lf3\-data.volccdn.com/obj/data\-static/log\-sdk/collect/5.0/core/collect\-rangers\-v5.1.x.js

* IE7、IE8：https://lf3\-data.volccdn.com/obj/data\-static/log\-sdk/collect/5.0/core/collect\-base\-rangers\-v5.1.x.js

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">IE7 and IE8 only support event reporting, not view exposure.   </div>
   

<span id="ae2ec3b2"></span>
## Is the web SDK compatible with old versions of Google Chrome?

Before Google 6.x version, you can use js files with core: https://lf3\-data.volccdn.com/obj/data\-static/log\-sdk/collect/5.0/core/collect\-privity\-v5.1.6.js

<span id="ce2f20b1"></span>
# Troubleshooting and handling of faults/errors

<span id="1696a3c3"></span>
## Element exposure events (element exposure events are not experimental exposures) cannot be reported in IE browser

The element exposure event does not support IE browser, only EDGE (except for other mainstream browsers in IE).

<span id="218947f6"></span>
## When integrating the Web SDK configuration multi\-link experiment, it prompts that the SDK is not installed. How to deal with it?

The multi\-link experiment requires the following configuration to be enabled during initialization: enable_ab_visual: true.

<span id="前向地址referrer为空如何排查？"></span>
## Forward address referrer is empty how to check?

(1) Whether the SDK version is above 5.0;

(2) Whether it is a SPA application, whether init has set spa = true;

(3) Whether the refer permission is set to disable referrer in the response header of the server level request
