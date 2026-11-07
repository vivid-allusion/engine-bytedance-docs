---
title: "Event Tracking Real-Time Verification"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/Event-Tracking-Real-Time-Verification"
---

Real\-time event tracking detection is a function that can detect and quickly verify whether the event tracking is correct and the data upload situation in real time. It is often used for research and development or tester debugging verification. It supports mobile end App (Android, iOS), WeChat Mini Program, web end, server level (Java). When using the event tracking detection function, after successfully establishing the event tracking detection connection, enter the event tracking verification page, and each event trigger will be displayed in the event tracking verification page in real time.

<span id="638a1edd"></span>
# Function entrance

After logging in to the DataTester console, click on the left navigation bar **Metrics Management** \> **metadata Management** \> **event tracking real\-time verification** to enter the event tracking real\-time verification page.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6e7241807db148acbf767ce04428e023~tplv-goo7wpa0wc-image.image) </span>

<span id="472587a0"></span>
# Establish event tracking real\-time verification connection

<span id="4470f629"></span>
## **Mobile end App**


1. Click the "**Mobile app**" tab at the top of the "Verify event tracking" page.

2. After selection, start real\-time detection and establish a real\-time verification connection.

   1. The first step is to scan the QR code.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a7633000280340559354f1a6a2d0946d~tplv-goo7wpa0wc-image.image) </span>

      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div>
      

      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">Make sure the correct version of the app (app name, App_name, App_id) is installed on the phone, and the correct evocation scheme is set and opened on the phone.      </div>
      

   2. Step 2: Open it in the mobile browser.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4a819f7dadcd45a1962bf97bc34ba59a~tplv-goo7wpa0wc-image.image) </span>

   3. Step 3: On the mobile phone, click "Start detecting event tracking", the connection is successfully established, and the detection starts.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b3c662c6bf8b43488bed749b8c95582c~tplv-goo7wpa0wc-image.image) </span>


<span id="1f3db40b"></span>
## **WeChat Mini Program**

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The SaaS\-cloud native environment does not currently support the Mini Program event tracking verification function.</div>



1. Click the "**WeChat Mini Program**" tab at the top of the "Verify event tracking" page.

2. After selection, start real\-time detection and establish a real\-time verification connection.

   1. If you have not uploaded the Mini Program QR code, go to the upload page.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a476515bcb9348d6bfb37bcbf6288018~tplv-goo7wpa0wc-image.image) </span>

   2. Click "Upload Mini Program Code" to enter the Upload Mini Program Code pop\-up page; generate the Mini Program code according to the provided parameters and upload it. After the upload is successful, click "Finish" to upload the Mini Program code.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c1efb2c7d14f484ab15a48300d896ce3~tplv-goo7wpa0wc-image.image) </span>

   3. The page displays the generated and uploaded Mini Program QR code, and the QR code parameters have relevant parameters to start event tracking verification.

   4. Scan the Mini Program Code.

      1. After scanning the code to enter the Mini Program, the SDK starts the real\-time detection connection according to the event tracking detection parameters.

      2. After scanning the code successfully, automatically enter the event tracking detection page.

         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7484cbfb755c40c6a370bdf56b7a6ec6~tplv-goo7wpa0wc-image.image) </span>

         If multiple users scan the code and do not start detection, according to the user who scans the code and related information (in reverse order according to the scanning time), you can select your mobile phone to scan the code, and automatically enter the event tracking detection page after success.

         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ca4e88a5dab84a808e91f7cc194d7001~tplv-goo7wpa0wc-image.image) </span>


<span id="a3cbc310"></span>
## **Web app**


1. Click the "**Web App**" tab at the top of the "Verify event tracking" page.

2. After selection, start real\-time detection and establish a real\-time verification connection.

   1. Enter the web page event tracking to detect the web page address (Note: The JS SDK version of the web page integration needs to be 5.1.2 and above).

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3e9fd496e69d450aa226bf0513cc530d~tplv-goo7wpa0wc-image.image) </span>

   2. Generate QR code and access URL address (Note: This page needs to integrate the web\-side SDK)

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5ca08928a29d4bbaa3306b0ec52963a5~tplv-goo7wpa0wc-image.image) </span>

   3. You can open the page in the following ways.

      * You can scan the code on the mobile phone and establish a link after scanning the code.

      * According to the generated access URL, the access page can be opened in the browser after copying, or it can be opened directly in the computer browser.


<span id="ece62aef"></span>
## **Server level event tracking**


1. Click the "**Server level event tracking**" tab at the top of the "Verify event tracking" page.

2. Start real\-time detection and establish a real\-time verification connection.

   1. Step 1: Enter the user_unique_id to verify your account.

   2. Step 2: Get the URL and set the URL to the specified location for SDK initialization according to the page prompts.

   3. Step 3: Start reporting event tracking and view real\-time detection data. The page will automatically jump after the connection is established.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f6319013fcca43ffaaa3c36687f0da15~tplv-goo7wpa0wc-image.image) </span>


<span id="46d15682"></span>
# View real\-time event tracking

Start real\-time detection, after successfully establishing a real\-time verification connection, automatically enter the real\-time verification page, and you can view each event trigger. Taking the mobile end App as an example, when the upload registration event (register) is triggered in the mobile end app, the following operations can be performed:


1. The trigger of the register event can be seen in the event axis on the left side of the real\-time verification page; the data reported by the register event can be seen in the code block on the right side of the page.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d97544b7c9fca567c35ae727c59128ec.png) </span>

2. Click "Finish Detection", disconnect, and navigate to the event tracking management page.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a545d58e0ca0ded26098cb7824687ad7.png) </span>
