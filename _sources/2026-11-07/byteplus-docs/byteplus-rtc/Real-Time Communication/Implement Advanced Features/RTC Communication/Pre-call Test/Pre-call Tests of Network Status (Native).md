---
title: "Pre-call Tests of Network Status (Native)"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-97200"
---

To provide a better user experience, you can conduct a network quality test before the user implements a call, and take measures according to the result of the test, for example, lower the bit rate, or remind users through UI to switch to a more stable network. As of version 3.31.0, the RTC Native SDK supports pre\-call network quality probe. The probe results present network quality statistics, including network scores that are closely linked to user experience and objective network quality metrics, such as round\-trip time, uplink and downlink packet loss rate, uplink and downlink internet bandwidth, etc.

<span id="prerequisite"></span>
# Prerequisite

You have integrated the RTC SDK to implement basic video call functions.

<span id="implementation"></span>
# Implementation

> Note: The steps are the same in different platforms, but interface and parameter names may differ slightly. This guide uses the Android RTC SDK as an example. You can refer to the API reference of the corresponding platform for more information.


1. After the engine is created, call `startNetworkDetection` to probe the network quality before starting a call.

   * Specify the expected maximum upstream and downstream bit rate in this method. You can refer to the [Video Profile List](https://docs.byteplus.com/en/docs/12/docs-70122) to estimate the required bandwidth and set the expected bandwidth. If you need to publish or subscribe to multiple streams, accumulate the bit rates for each stream.

   * You can specify whether the network to be probed is upstream or downstream.

2. When this method is successfully called, the SDK will provide statistics including network quality score and round\-trip time, packet loss rate, internet bandwidth, and network jitter in the `onNetworkDetectionResult` callback, which is triggered every 2 seconds. If the network probe fails, the SDK will notify you of the failure and its reason through an `onNetworkDetectionStopped` callback.

3. After starting the call, the network quality probe will automatically stop. You can also call `stopNetworkDetection` to stop the probe before the call.


<span id="api-reference"></span>
# API reference


|Platform |Android |iOS |MacOS |Windows |
|---|---|---|---|---|
|Start pre\-call network probe |[startNetworkDetection](https://docs.byteplus.com/en/docs/12/docs-70080#startnetworkdetection) |[startNetworkDetection:uplinkBandwidth:downlink:downlinkBandwidth:](https://docs.byteplus.com/en/docs/12/docs-70086#startnetworkdetection-uplinkbandwidth-downlink-downlinkbandwidth) |[startNetworkDetection:uplinkBandwidth:downlink:downlinkBandwidth:](https://docs.byteplus.com/en/docs/12/docs-70092#startnetworkdetection-uplinkbandwidth-downlink-downlinkbandwidth) |[startNetworkDetection](https://docs.byteplus.com/en/docs/12/docs-70095#startnetworkdetection) |
|Stop pre\-call network probe |[stopNetworkDetection](https://docs.byteplus.com/en/docs/12/docs-70080#stopnetworkdetection) |[stopNetworkDetection](https://docs.byteplus.com/en/docs/12/docs-70086#stopnetworkdetection) |[stopNetworkDetection](https://docs.byteplus.com/en/docs/12/docs-70092#stopnetworkdetection) |[stopNetworkDetection](https://docs.byteplus.com/en/docs/12/docs-70095#stopnetworkdetection) |
