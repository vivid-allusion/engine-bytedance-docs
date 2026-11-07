---
title: "Enable RTC Communication with Restrictions of Firewall"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-146420"
---

During audio and video calls with RTC, audio and video streams are relayed through the RTC server and signaling interaction occurs between the RTC clients and server. Audio and video communication may be restricted by a firewall.

Refer to this article and use the cloud proxy feature to ensure smooth audio and video communication when behind firewalls.


> * Because RTC server IP addresses are dynamic, you cannot add them to a firewall whitelist. Instead, you must use the cloud proxy feature to bypass firewall restrictions.

> * The feature is available on native SDK 3.41+ and web SDK 4.41+.


<span id="step-1-apply-for-cloud-proxy"></span>
## Step 1: Apply for cloud proxy

Contact technical support to apply for the cloud proxy.

When applying, you need to provide the following information:


* AppID;

* Application distribution regions and traffic distribution for each region;

* Maximum number of concurrent streams. You can calculate the number of streams using the following examples:

   * 1v1 calls = 2 streams

   * 4\-person conferences = 4\*3 = 12 streams

   * single\-hosted live broadcasts with 1000 viewers = 1000 streams

   * dual\-hosted live broadcasts with 1000 viewers = 2\*1000 = 2000 streams

* Network operator information


After your application is approved, you will receive an exclusive cloud proxy IP address and port.

<span id="step-2-configure-firewall-whitelist"></span>
## Step 2: Configure firewall whitelist

Set the configuration of your firewall based on the RTC SDK type in use. Follow the sub\-steps:


1. Add the exclusive cloud proxy IP and port information to the firewall whitelist.

2. If you are using the RTC Native SDK, Electron SDK, or Flutter SDK, add the following domain names and ports to the firewall whitelist:



|Service Type |Domain/IP |Port |Protocol |
|---|---|---|---|
|Native SDK Access and Log Service |`122.14.236.65` |`443` |TCP |
|Native SDK Access and Log Service |`122.14.236.66` |`443` |TCP |
|Native SDK Access and Log Service |`220.243.190.114` |`443` |TCP |
|Native SDK Access and Log Service |`220.243.190.115` |`443` |TCP |



3. If you are using the RTC Web SDK, add the following domain names and ports to the firewall whitelist additionally:



|Service Type |Domain/IP |Port |Protocol |
|---|---|---|---|
|Web SDK client access (`accessProxy`) |`rtc-access-src.zijieapi.com`, `rtc-access-src-hl.zijieapi.com` |`443` |TCP |
|RTC configuration distribution proxy (`configProxy`) |`rtc-src.zijieapi.com` |`443` |TCP |
|Log report proxy (`logProxy`) |`rtc-log-report-src.zijieapi.com` |`443` |TCP |



4. If you are using the Web SDK and implementing basic beauty or virtual background features via plugins, add the following domain names and ports to the firewall whitelist additionally:



|Service Type |Domain/IP |Port |Protocol |
|---|---|---|---|
|Web SDK Basic Beauty and Virtual Background |`webar.volccdn.com` |`443` |TCP |
|Web SDK Virtual Background Authentication |`webar.volces.com` |`443` |TCP |


<span id="step-3-call-the-client-interface"></span>
## Step 3: Call the client interface

For clients under firewall restrictions, call the `startCloudProxy` API to enable the cloud proxy feature.

For the Native SDK, the parameters are:


|`cloudProxyIp` |`cloudProxyPort` |
|---|---|
|`122.14.236.65` |`443` |
|`122.14.236.66` |`443` |
|`220.243.190.114` |`443` |
|`220.243.190.115` |`443` |


For the Web SDK, the configuration is:

```Plain
{
    "logProxy": "rtc-log-report-src.zijieapi.com",
    "accessProxy": ["rtc-access-src.zijieapi.com", "rtc-access-src-hl.zijieapi.com"],
    "configProxy": "rtc-src.zijieapi.com"
}
```


After the API is called successfully, the client receives the `onCloudProxyConnected` callback. Use a network quality test to confirm that audio and video services are functioning correctly.

> Note: Clients that use the cloud proxy can still communicate with clients that do not.


<span id="related-interfaces-and-callbacks"></span>
## Related interfaces and callbacks


| |Android |iOS |macOS |Windows |Web |
|---|---|---|---|---|---|
|Start cloud proxy |[startCloudProxy](https://docs.byteplus.com/en/docs/12/docs-70080#startcloudproxy) |[startCloudProxy](https://docs.byteplus.com/en/docs/12/docs-70086#startcloudproxy) |[startCloudProxy](https://docs.byteplus.com/en/docs/12/docs-70092#startcloudproxy) |[startCloudProxy](https://docs.byteplus.com/en/docs/12/docs-70095#startcloudproxy) |[startCloudProxy](https://docs.byteplus.com/en/docs/12/docs-104478#startcloudproxy) |
