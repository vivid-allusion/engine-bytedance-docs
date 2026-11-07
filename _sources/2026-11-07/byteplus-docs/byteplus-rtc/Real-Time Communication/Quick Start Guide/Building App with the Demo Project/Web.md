---
title: "Web"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-77374"
---

BytePlus RTC provides an open source demo project for real time audio & video calls. This documentation introduces how to quickly run through the demo project. After obtaining this project file, you can quickly build an application to experience the performance of BytePlus RTC. You can also read the code to learn about basic audio & video calling best practices.

<span id="prerequisites"></span>
## Prerequisites


* An operating system with graphical user interface

* Terminal

* A browser [supported by Web SDK](https://docs.byteplus.com/en/docs/12/docs-111854). We highly recommend using the latest version of Google Chrome to have the best experience.

* [Demo project](https://docs.byteplus.com/en/docs/12/docs-1163793)


<span id="project-structure"></span>
## Project structure

We provide the plain JavaScript demo and the React demo. The file structure of the demo project is listed below.


* Plain JavaScript demo


```Plain
   │─ BasicDemo                 // Plain JavaScript Demo
   │  ├─ assets                 // Static resources such as images
   │  ├─ js                    // Basic modules
   │  ├─ lib                    // BytePlusRTC SDK
   │  ├─ README.md              // Guide for running the quick-start demo
```



* React demo


```Plain
   │─ ReactDemo                 // React Demo
   │  ├─ public                 // Static resources such as images
   │  ├─ src                    // Basic modules
   │  ├─ README.md              // Guide for running the quick-start demo
```


<span id="demo-running-procedure"></span>
## Run the demo

<span id="step-1-obtain-the-appid-and-the-temporary-token"></span>
### Step 1. Obtain the AppID and a temporary token

Follow instructions in [Before Using RTC Service](https://docs.byteplus.com/en/docs/12/docs-69865) to get the AppID and generate a temporary Token.

Make a note of the room ID, user ID, and the generated temporary token. You will need these values to configure the demo.

> The temporary token is used only for running the demo. You can learn more about the token from [Authentication with Token](https://docs.byteplus.com/en/docs/12/docs-70121).


<span id="step-2-configure-the-demo-project"></span>
### Step 2. Configure the Demo Project


1. Install [Node.js and npm](https://docs.npmjs.com/downloading-and-installing-node-js-and-npm).

2. Use npm to install yarn globally. Run `npm install -g yarn`.

3. Modify the configurations below for the demo you want to experience. For the Plain JavaScript Demo, find `./js/common.js`, while for the React Demo, find `./src/config.ts`.

   * `appId`: Fill in your AppID.

   * `roomId`: Fill in the room ID when applying for the temporary token.

   * token: The `tokens` field is an array that can hold multiple user\-token pairs.


```javascript
const config = {
  appId: 'YourAppId',
  roomId: 'YourRoomId',
  tokens: [
    {
      userId: 'yourUserId1',
      token: 'yourToken1',
    },
    {
      userId: 'yourUserId2',
      token: 'yourToken2',
    }
  ],
};
```


<span id="step-3-compile-and-run-the-demo-project-file"></span>
### Step 3. Compile and Run the Demo Project File


1. Open terminal.

2. Enter the root directory of the plain JavaScript demo or the React demo.

3. Run `yarn` to install the project's dependencies.

4. Run `yarn start` to start the demo and you will be redirected to the login page.


<span id="experience-rtc-features"></span>
## Test the RTC features

To better experience RTC features, you can invite a friend or use another device to run the sample project, and make sure that the AppID is the same when configuring this project on both devices. Once both devices have joined the same room, you can start an audio and video call.

<span id="follow-up-steps"></span>
## Next steps

After trying this demo, you can read the following documents to learn more:


* In test or production environments, you need to use a token for authentication. To ensure communication security, we recommend obtaining the token from your server. For details, please refer to Complete Authentication with Token.

* When implementing different video calling scenarios, you need to configure different video publishing parameters to achieve the best results. For details, please refer to [Setting Video Publishing Parameters](https://docs.byteplus.com/en/docs/12/docs-70122).
