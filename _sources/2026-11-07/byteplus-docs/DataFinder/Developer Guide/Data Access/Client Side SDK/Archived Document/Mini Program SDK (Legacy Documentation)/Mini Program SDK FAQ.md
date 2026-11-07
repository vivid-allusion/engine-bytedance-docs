---
title: "Mini Program SDK FAQ"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Mini_Program_SDK_FAQ"
---

<span id="8df7e86f"></span>
### 1. Mini Program SDK Data Reporting Strategy

Default real\-time reporting, in addition to enabling enable_buffer support buffering and enabling enable_cache support caching. Where the buffer, buffer_interval used to control the buffer interval, buffer_number used to control the number of buffers:


* buffer_interval: Default 5 seconds, can be adjusted

* buffer_number: Default 5, can be adjusted

   Quick App/Mini Game Report Strategy with Mini Program


&nbsp;

<span id="小程序同时集成growingio-gio-和finder-sdk-，发现finder没有请求上报数据？"></span>
### 2. The Mini Program integrates GrowingIO (gio) and the finder SDK at the same time. Did you find that the finder did not request to report data?

You need to complete the import and initialization (init) of the gio SDK first, and then import the finder SDK and initialization (init).

<span id="小程序如果没网状态下数据是怎么上传的？"></span>
### 3. How is the data uploaded to the Mini Program without the Internet?

The Mini Program SDK does not actively monitor network changes. When there is no network, the report request will theoretically fail. At this time, according to whether the enable_cache parameter is turned on, there are the following corresponding processing:


* When this parameter is enabled, the event (failed request) will be cached into the storage, and after waiting for the next SDK to perform initialization, it will try to check whether there are cached events from the storage, and if so, make supplementary reports.

* When this parameter is not enabled, the request fails without any processing.

   Note: The storage in the Mini Program has a size limit, and the event will be thrown when the limit is exceeded.

   Scenario example:

   When the Mini Program is currently running, there is no network at this time, and then suddenly there is a network, then the follow\-up behavior is reported normally, and those that have existed in the storage before will not be transmitted now. Only after the Mini Program is re\-initialized will the step of going to the storage to see if there is any.
