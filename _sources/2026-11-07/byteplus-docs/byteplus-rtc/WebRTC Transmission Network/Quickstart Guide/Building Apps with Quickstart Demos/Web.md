---
title: "Web"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/132447"
---

To quickly experience WTN's real\-time video streaming capabilities, you can run the provided open\-source Quick Start Demo.

Follow the doc to run the Demo to experience WTN and understand the best practices for using WTN by reading the source code.

<span id="prerequisites"></span>
## Prerequisites


* Your operating system must have a graphical user interface (GUI).

* Install the latest version of the Chrome browser and set it as the default browser.

* Node.js is globally installed.

* Yarn is globally installed.

* Obtain the WTN project files. See [Download Demos](https://docs.byteplus.com/docs/byteplus-rtc/132439).

* Obtain the `AppID` and `AppKey` for WTN from the [console](https://console.byteplus.com/rtc/listRTC).


> Note:


> * For installing Node.js, see [Node.js](https://nodejs.org/en/).

> * For installing Yarn, see [Installation](https://classic.yarnpkg.com/lang/en/docs/install/).


<span id="running-the-demo"></span>
## Running the Demo

<span id="step-1-get-the-publishing-and-subscribing-addresses"></span>
### Step 1: Obtain the Publishing and Subscribing Addresses


1. Call the API to create the publishing resource and get the publishing address from the `location` field in the response. See [Create Publishing Resource](https://docs.byteplus.com/docs/byteplus-rtc/132482).

2. Call the API to create the subscribing resource and get the subscribing address from the `location` field in the response. See [Create Subscription Resource](https://docs.byteplus.com/docs/byteplus-rtc/132484).


<span id="step-2-fill-in-the-publishing-and-subscribing-addresses-in-the-demo"></span>
### Step 2: Fill in the Publishing and Subscribing Addresses in the Demo

Fill in the publishing and subscribing stream addresses in the configuration file `./src/config.ts`.

```Plain Text
export const pubUrl = 'YOUR_PUB_URL';
export const subUrl = 'YOUR_SUB_URL';
```


<span id="step-2-compile-and-run"></span>
### Step 3: Compile and Run


1. In the terminal, navigate to the root directory of the demo project files.

2. Compile the Demo. Run `yarn` and wait for the installation to complete.

3. Start the Demo. Run `yarn dev`.

4. Access the local address in Chrome. The application will display the following page:

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_29d42023af401a8ffd2620e2b6bc2deb.png) </span>


On this page, you can:


* Capture and publish the video stream.

* subscribe to and render the video stream.
