---
title: "Electron"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-115523"
---

The Quick Start Demo is an open\-source sample project file with basic RTC functions provided by BytePlus RTC. With this project file, you can quickly build an application for the hands\-on experience of BytePlus RTC. You can also refer to the code for best practices of basic RTC calls.

<span id="prerequisites"></span>
## Prerequisites


* A PC with internet access, Windows or Mac.

> Macs with ARM\-based chips are supported.


* Node.js, npm, Yarn, and other prerequisites for Electron development.

* Download the [demo project](https://docs.byteplus.com/en/docs/12/docs-1163793).


<span id="procedure"></span>
## Procedure

<span id="_1-get-appids-and-temporary-tokens"></span>
### 1. Get AppIDs and Temporary Tokens

After applying for a temporary token, you should record the room ID, user ID, and the generated temporary token, which are needed when configuring the environment and joining the room.

> Refer to [Before Using RTC Service](https://docs.byteplus.com/en/docs/12/docs-69865) to get your AppID and temporary token.

> The temporary token is used only for debugging. You can learn more about tokens by reading [Authentication with Token](https://docs.byteplus.com/en/docs/12/docs-70121).


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f9620371a0e97f6cf03b5e7d73e5a938.png) </span>

<span id="_2-configuration"></span>
### 2. Configuration

Fill in the configuration file `./src/config/config.js` with AppID and Token.

```javascript
const config ={
 
    appId:"Put your appId here",
    token:"Put your token here"
};
module.exports = config;
```


<span id="_3-install-dependencies"></span>
### 3. Install dependencies

Install dependencies by running the following command in the root of the demo project.

```Plain
npm install
```


<span id="_4-download-and-integrate-sdk"></span>
### 4. Download and integrate SDK

<span id="recommended-npm"></span>
#### [Recommended] NPM

Run the following command in the root of the demo project.

```powershell
npm install @byteplus/byteplus-electron-sdk --save
```


<span id="manually"></span>
#### Manually

Download [Electron SDK](https://docs.byteplus.com/en/docs/12/docs-75707) and save as `node_modules/@byteplus/byteplus-electron-sdk`.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a9907f18b67c7609998cbcc26d90d8db.png) </span>

<span id="_5-build-and-run-the-demo-project"></span>
### 5. Build and run the demo project

Run the following command in the root of the demo project.

```Plain
npm run build
```


The application window opens when the demo starts. Input the user ID and room ID that you used to generate the token. Click **Enter Room** and start your video chat.

> Different users must use the same AppID and join the same room to successfully make an RTC call.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_711e0f1b4f446dd9f78c12afc91b0939.png) </span>

<span id="experience-rtc-features"></span>
## Experiencing RTC Features

To better experience RTC features, you can invite a friend or use another device to run the sample project, and make sure that the AppID is the same on both devices. After two devices join the same room, you can experience audio and video calls within the same room.

<span id="follow-up-steps"></span>
## Follow\-up Steps

After trying the demo, read the following documents to learn more:


* In test or production environments, you need to use a Token for authentication. To ensure communication security, it is recommended to obtain the Token from the server. For details, please refer to [Complete Authentication with Token](https://docs.byteplus.com/en/docs/12/docs-70121).

* When implementing different video calling scenarios, you need to configure different video publishing parameters to achieve the best results. For details, please refer to [Setting Video Publishing Parameters](https://docs.byteplus.com/en/docs/12/docs-70122).
