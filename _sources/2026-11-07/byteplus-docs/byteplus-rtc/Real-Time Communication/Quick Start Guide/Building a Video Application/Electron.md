---
title: "Electron"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-108795"
---

With the BytePlus RTC SDK, you can build a basic app for real\-time video calls. For the complete sample code of the demo project, see [Demo project](https://docs.byteplus.com/en/docs/12/docs-1163793).

<span id="prerequisites"></span>
## Prerequisites


* Get an [appId](https://docs.byteplus.com/en/docs/12/docs-69865).

* A PC with internet access, Windows or macOS

> Macs with ARM\-based chips are supported.


* node.js and other requirements for Electron development


<span id="_1-create-a-project"></span>
## 1. Create a project

Create a new project with the following files.


* `package.json`: Used to install and manage the project's dependencies.

* `index.html`: is used to design the user interface.

* `main.js`: for the main process of the app

* `renderer.js`: for the renderer process of the app


<span id="_2-integrate-the-sdk"></span>
## 2. Integrate the SDK

<span id="recommended-npm"></span>
### [Recommended] NPM

Run the following command in the root of the demo project.

```powershell
npm install @byteplus/byteplus-electron-sdk --save
```


> Run [npm init](https://docs.npmjs.com/cli/v9/commands/npm-init) to set up a new npm package if there is no package.json file in the folder.


<span id="manually"></span>
### Manually


1. Download an appropriate version of Electron SDK and move the SDK to your project folder, such as `node_modules/@byteplus/byteplus-electron-sdk`.

2. Import SDK to your project using the code below.


```javascript
const SDK = require('@byteplus/byteplus-electron-sdk');
// Here we take `node_modules` for example.
// You should change the path to where the SDK actually is.
```


<span id="_3-add-video-features"></span>
## 3. Add video features

<span id="user-interface"></span>
### User interface

To create an interface with views for local and remote videos, add the following code to your index.html file.

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <title>Electron Quickstart</title>
</head>
<body>
  <h1>Electron Quickstart</h1>
  <!--View for the local video -->
  <div id="join-channel-local-video" style="width: 240px; height: 180px; background-color: lightblue;"></div>
  <!--View for the remote video -->
  <div id="join-channel-remote-video" style="width: 240px; height: 180px; background-color: lightblue;"></div>
</body>
</html>
```


<span id="the-main-process"></span>
### The main process

The following sample provides the main process for an Electron project. Add the code below in `main.js`.

```javascript
const { app, BrowserWindow, systemPreferences } = require('electron')
const path = require('path')

function createWindow() {
  // Create a browser window.
  const mainWindow = new BrowserWindow({
    width: 800,
    height: 600,
    webPreferences: {
      preload: path.join(__dirname, 'renderer.js'),
      nodeIntegration: true
    }
  })

  // Load contents from index.html.
  mainWindow.loadFile('./index.html')
  // Open DevTools
  mainWindow.webContents.openDevTools()
}

// Application windows management for your Electron app
app.whenReady().then(async () => {
  if (process.platform === 'darwin') await checkAndApplyDeviceAccessPrivilege()
  createWindow()
  // For macOS, open a window if none are open.
  app.on('activate', function () {
    if (BrowserWindow.getAllWindows().length === 0) {
      createWindow()
    }
  })
})

// For Windows, quit the app when all windows are closed.
app.on('window-all-closed', function () {
  if (process.platform !== 'darwin') app.quit()
})
```


<span id="request-permissions"></span>
### Request permissions

For macOS 10.14 and later, you must request permissions for microphones and cameras by calling [systemPreferences.askForMediaAccess()](https://www.electronjs.org/docs/latest/api/system-preferences) in the main process.

```javascript
async function checkAndApplyDeviceAccessPrivilege() {
  // Check and request accessing permission for cameras.
  const cameraPrivilege = systemPreferences.getMediaAccessStatus('camera');
  console.log(`checkAndApplyDeviceAccessPrivilege before applying cameraPrivilege: ${cameraPrivilege}`);
  if (cameraPrivilege !== 'granted') {
    await systemPreferences.askForMediaAccess('camera');
  }
  // Check and request accessing permission for microphones.
  const micPrivilege = systemPreferences.getMediaAccessStatus('microphone');
  console.log(`checkAndApplyDeviceAccessPrivilege before apply micPrivilege: ${micPrivilege}`);
  if (micPrivilege !== 'granted') {
    await systemPreferences.askForMediaAccess('microphone');
  }
}
```


<span id="the-renderer-process"></span>
### The renderer process

Follow the steps below to create the renderer process.


1. Create an RTCEngine instance.

2. Call createRTCEngine() with the AppID to initialize the RTCEngine instance.

3. Call startVideoCapture() to start video capture before you can enable video in a call.

4. Call startAudioCapture() to start audio capture before you can enable audio in a call.

5. Call setupLocalVideo() to set up the local video view.

6. Call setupRemoteVideo() to set up the remote video view.

7. Call createRTCRoom with roomId to create an RTCRoom instance in the RTCEngine instance. This step is required, regardless of whether the user is creating a new room or joining an existing one.

8. Call joinRoom() with a valid token, user info, user visibility, and room configurations in the RTCRoom instance. In this example, audio and video are published and subscribed to automatically after the user joins the room.


```Plain
rtcRoom.joinRoom(token: string, { uid: string }, userVisibility: boolean, roomConfig?: RTCRoomConfig): number;
```



9. Call leaveRoom to end a call. Then, release the `RTCRoom` and `RTCEngine` instances.


```javascript
// End a call
rtcRoom.leaveRoom();
// Destroy RTCRoom
rtcRoom.destroy();
// Destroy RTCEngine
rtcEngine.destroyRTCEngine();
```


The following diagram shows the API call flow:

<span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/345demo/building%20electron%20app.png) </span>

Include the following code in `renderer.js`

```javascript
window.addEventListener('DOMContentLoaded',() => {
    const SDK = require('@byteplus/byteplus-electron-sdk')
    const RTCEngine = SDK.RTCEngine;

    // Fill in your appId
    const APPID = ""
    // Fill in your token
    const token = ""
    // Fill in the room ID and user ID used to generate the token
    const roomId = ""
    const userId = ""

    const localVideoContainer = document.getElementById('join-channel-local-video')
    const remoteVideoContainer = document.getElementById('join-channel-remote-video')

    let rtcEngine = new RTCEngine()
    let rtcRoom ;
    rtcEngine.createRTCEngine({ app_id: APPID, parameters: "" })

    // Start video capture.
    rtcEngine.startVideoCapture();
    // Start audio capture.
    rtcEngine.startAudioCapture();
    // Join a room.
    let roomConfig = {
        room_profile_type: 1,
        is_auto_publish_audio: true,
        is_auto_publish_video: true,
        is_auto_subscribe_audio: true,
        is_auto_subscribe_video: true
    };
    rtcRoom = rtcEngine.createRTCRoom(roomId);
    rtcRoom.on('onUserPublishStreamVideo', (streamId, streamInfo, isPublish) => {
        if (isPublish) {
            rtcEngine.setupRemoteVideo(streamId, remoteVideoContainer);
        } else {
            rtcEngine.removeRemoteVideo(streamId);
        }
    });
    let ret = rtcRoom.joinRoom(token,{ uid: userId }, true, roomConfig);
    rtcEngine.setupLocalVideo(localVideoContainer)
    console.log('join room ret : ' + ret)
})
```


<span id="_4-pack-your-application"></span>
## 4. Pack your application

We recommend electron\-builder and native\-ext\-loader for packaging your Electron application.

<span id="install-packing-tools"></span>
### Install packing tools

Use the commands below to install the packing tools.


* `electron-builder`


```shell
npm install electron-builder@latest --save-dev
```



* `native-ext-loader`


```shell
npm install native-ext-loader@latest --save-dev
```


<span id="configure-the-packing"></span>
### Configure the packing


1. Locate webpack.config.js which usually could be found in the root folder of your project.

* For the RTC demo project for Electron, webpack.config.preload.js is the configuration file.

* For a vue project, you can configure the build process in the `chainWebpack` of `vue.config.js`.

* For a react project, you can configure the building in the `create-react-app` of `node_modules/react-scripts/config/webpack.config.js`.


```javascript
rules: [
      {
        test: /\.node$/,
        loader: "native-ext-loader",
        options: {
          emit: false,
          basePath: ["vertc"], // The directory to which copySdkAddon.js copies the RTC native module.
        },
      },
    ]
```



2. Provide the required information for the packing in package.json which you can find in the root of your project.


```json
"main": "index.js",// Specify the entrance of the project.
"asar": true,// Compress and encrypt the web source files.
"asarUnpack": ["vertc"] // Keep the copied RTC native module outside the asar archive.
```



3. To include the RTC .node module in the `app` folder by running copySdkAddon.js during packing, add the following code to `scripts`.

> You can find copySdkAddon.js in the [Demo project](https://docs.byteplus.com/en/docs/12/docs-1163793). The script copies `node_modules/@byteplus/byteplus-electron-sdk/build/release` to `app/vertc`. Keep this destination consistent with `basePath` and `asarUnpack`.


```json
"scripts": {
    "start": "electron ./app",
    "build": "yarn buildApp && yarn start",
    "buildApp": "yarn copySdkAddon && yarn buildMain && yarn buildRenderer && yarn buildSetting && yarn buildPreload ",
    "buildMain": "webpack --config webpack.config.main.js --mode development",
    "buildRenderer": "webpack --config webpack.config.renderer.js --mode development",
    "buildPreload": "webpack --config webpack.config.preload.js --mode development",
    "buildSetting": "webpack --config webpack.config.setting.js --mode development",
    "copySdkAddon": "node ./scripts/copySdkAddon.js"
  },
```


<span id="_5-run-the-project"></span>
## 5. Run the project

Run the project with the following command.

```Plain
npm run start
```


<span id="faq"></span>
## FAQ

Q: Why do I receive the error "RTCEngine is not a constructor" when building the project?

A: It is probably because the .node module of the RTC is not packed into the executable program correctly. We recommend packing your project following the instructions in the section [Pack your project](https://docs.byteplus.com/docs/byteplus-rtc/docs-108795#pack).

> For answers to more integration issues, refer to [FAQ during Building an Electron App](https://docs.byteplus.com/en/docs/12/docs-1133953).
