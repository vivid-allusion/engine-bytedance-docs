---
title: "React Native"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1455709"
---

After integrating the RTC SDK, you can use its interfaces to quickly build a basic application and achieve real\-time audio and video calls. You can also understand the best practices for audio and video calls by reading the code.

<span id="6dad7d83"></span>
## Prerequisites


* Node \>= 18.

* Obtain the [AppID](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-69865).

* If the target platform is Android:

   * Android 6.0+ (API Level 23).


Considering device performance, it is recommended to integrate on Android 8.0+ (API Level 26).


* Real devices with arm64\-v8a or armeabi\-v7a architecture.

* If the target platform is iOS:

   * Xcode 12.5+

   * iOS 13.4+

   * Real devices with arm64 architecture.

   * Valid developer signature in your project.


<span id="3b97b456"></span>
## Integrate the SDK

<span id="48cbeb52"></span>
### Step 1: (Optional) Create a project

> This step is about how to create a new project. If you are integrating into an existing project, please skip this step.


Please refer to [Get Started with React Native (without a Framework)](https://reactnative.dev/docs/getting-started-without-a-framework) to create a React Native project.

<span id="7e53632f"></span>
### Step 2: Install dependencies

<span id="da787ea4"></span>
#### Install React Native dependencies

Navigate to the project root directory in the terminal and run the following commands to install the dependencies:

```PowerShell
# Using npm
npm install @byteplus/react-native-rtc

# OR using Yarn
yarn add @byteplus/react-native-rtc
```


<span id="c7ae7da8"></span>
#### Integrate the SDK on the native platform


* Android application

> Assuming the project structure is the initialized structure.


* Configure the Maven repository address, edit the `./build.gradle` file.


```Groovy
allprojects {
            repositories {
                ...
                maven { url 'https://artifact.byteplus.com/repository/public/' }
            }
        }
```



* Add `android.enableJetifier=true` to the `./gradle.properties` file to resolve compatibility issues. Modify the `reactNativeArchitectures` property as needed to configure the architectures to be compiled.

* For iOS applications, please refer to the [iOS SDK Integration Guide](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70133#integrate-the-sdk).


<span id="483568a2"></span>
### Step 3: Configure Project Properties

The SDK has already declared the required permissions internally, so there is no need to add them manually.

For other considerations, please refer to:


* [Android configure permissions](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70134#configure-permissions)

* [iOS Configure Properties](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70133#step-3-configure-project-properties)


<span id="f0e28e27"></span>
## Implement a client for Video Call

<span>![图片](https://pblk.bytedance.com/svg/ZLDDJ-Cm4BtxLun0Mh47AhMgKcaFYCIBTxLR95JOlPja25uIJzTs-13YlpDs2qshe9939FkzUVFcmwS-Q1UwjX72tncxr4wtuCDJW_ntfapGhQdmXYXSqsEFTQtBkzfHPoj93JauLBagbEphuFyEROddwBskCMzCRQ546z0DiE1P0EJEqSDQBvjbnMp2btDpWtDZiI1NeLkZ-KIEbUgZktwcusasZOmBBj6KPgbj-1H9aGrlDQLFl0YntE1mCATID_37epi0xI7VHXTN4Yw__qvG0OTZMKoosGu5MmguKP1CozY84YA7unCE-mOM7u2bphNbvhcZh_05Vc20TdK6OtbstBTDm1ePbGvrG0uzipKtvZqIqt4WC08uyXWMeVpBmwQpUvxIJssh9YRU9bhS95WGjU_oZWy3ul4wQQ_eUwJJFkPTPKZgPUWSViH9FWSuATq_CdRbJOWY8ZaZ0mP6b6YNWSkHjzhMMCKG-P7O7gqupb_CJYfxkCeu7rPha4fH_1PmWPOtVCX4W_eUF-zY7kbHPQSnVPbjf49-yFJKlt_RfpNKMwXN) </span>

<span id="7ac95de9"></span>
### Encapsulating SDK Code

> For the convenience of explaining the subsequent steps, it is assumed here that the file path for encapsulation is `./src/core/index.ts` under the project root directory.


```TypeScript
import {
    RTCManager,IEngine, IRoom, RTCVideoEventHandler, RTCRoomEventHandler, IJoinRoomProps, ICreateRTCEngineOptions, StreamIndex, IVideoCanvas,
} from '@byteplus/react-native-rtc';

class RTCClient {
    manager?: RTCManager;
    engine?: IEngine | null;
    room?: IRoom | null;
 
    constructor() {
       this.manager = new RTCManager();
    }
 
    /** Engine module */
    async createEngine({ appID }: ICreateRTCEngineOptions) {
      this.engine = await this.manager!.createRTCEngine({ appID });
    }
    setRTCVideoEventHandler(handlers: RTCVideoEventHandler) {
       this.engine?.setRtcVideoEventHandler(handlers);
    }
    setRTCRoomEventHandler(handlers: RTCRoomEventHandler) {
       this.room?.setRTCRoomEventHandler(handlers);
    }
    startAudioCapture() {
       return this.engine?.startAudioCapture();
    }
    startVideoCapture() {
       return this.engine?.startVideoCapture();
    }
    setLocalVideoCanvas(streamIndex: StreamIndex, canvas: IVideoCanvas) {
        return streamIndex < 0 ? 0 : this.engine?.setLocalVideoCanvas(streamIndex, canvas);
    }
    destroyEngine() {
       this.leaveRoom();
       this.room?.destroy();
       this.room = null;
       this.manager!.destroyRTCEngine();
       this.engine = null;
    }
 
    /** Room module */
    joinRoom(params: IJoinRoomProps) {
       return this.room?.joinRoom({
            token: '<YOUR_TOKEN>',
            ...params,
       });
    }
    leaveRoom() {
       this.room?.leaveRoom();
    }
    createRoom(roomId: string) {
       this.room = this.engine?.createRTCRoom(roomId);
       return this.room;
    }
}

export default new RTCClient();
```


<span id="eb46e4b6"></span>
### Encapsulating RTC Event Listeners

> For the convenience of explaining the subsequent steps, it is assumed here that the file path for encapsulation is `./src/core/handlers.ts under the project root directory.`


```TypeScript
import {
  RTCVideoEventHandler,
  RTCRoomEventHandler,
  UserInfo,
  MediaStreamType,
} from '@byteplus/react-native-rtc';

function convertObjectForPrinting(obj: Record<string, string>) {
  if (typeof obj !== 'object') {
    return obj;
  }
  const result: Record<string, string> = {};
  const properties = Object.getOwnPropertyNames(obj);
  properties.forEach(prop => {
    const descriptor = Object.getOwnPropertyDescriptor(obj, prop);
    if (descriptor && typeof descriptor.get === 'function') {
      try {
        result[prop] = descriptor.get.call(obj);
      } catch (error) {}
    } else if (typeof obj[prop] !== 'function') {
      result[prop] = obj[prop];
    }
  });
  return result;
}

const logger = (fnName: string, executer?: any) => {
  /** Get function name */
  const f = (...args: unknown[]) => {
    console.log(
      `------ ${fnName} : ${args
        .map(arg =>
          typeof arg === 'object'
            ? JSON.stringify(
                Array.isArray(arg)
                  ? [...arg].map(convertObjectForPrinting)
                  : convertObjectForPrinting(arg as any),
              )
            : arg,
        )
        .join(' | ')}`,
    );
    executer?.(...args);
  };
  f.name = fnName;
  return f;
};

const useRTCVideoListeners = (): RTCVideoEventHandler => {
  // ...some hooks
  return {
    onUserStartAudioCapture: logger('onUserStartAudioCapture'),
    onUserStopAudioCapture: logger('onUserStopAudioCapture'),
    onUserStartVideoCapture: logger('onUserStartVideoCapture'),
  };
};

const useRTCRoomListeners = (): RTCRoomEventHandler => {
  // ...some hooks
  const apis = {
    onUserJoined: logger('onUserJoined', (userInfo: UserInfo) => {
        // ...
      }
    ),
    onUserPublishStream: logger(
      'onUserPublishStream', (uid: string, type: MediaStreamType) => {
        // ...
      },
    ),
  };
  return apis;
};

export {
  useRTCVideoListeners,
  useRTCRoomListeners,
};
```


<span id="bdcb0b20"></span>
### Create a View and Integrate SDK Capabilities

> For the convenience of explaining the subsequent steps, it is assumed here that the file path for encapsulation is `./src/page/index.ts` under the project root directory.


```TypeScript
import React, { useEffect, useState } from 'react';
import { Platform, KeyboardAvoidingView } from 'react-native';
import { ChannelProfile, NativeViewComponent, StreamIndex, RenderMode } from '@byteplus/react-native-rtc';
import { request, PERMISSIONS } from 'react-native-permissions';
import RTCClient from '../core';
import { useRTCRoomListeners, useRTCVideoListeners } from '../core/handlers';

const viewId = 'my-view';

const ExamplePage = () => {

    const [ isViewLoaded, setViewLoaded ] = useState<boolean>(false);
    const engineEventListeners = useRTCVideoListeners();
    const roomEventListeners = useRTCRoomListeners();

    const requestDevicePermission = async () => {
        if (Platform.OS === 'ios') {
            await request(PERMISSIONS.IOS.CAMERA);
            await request(PERMISSIONS.IOS.MICROPHONE);
        } else {
            await request(PERMISSIONS.ANDROID.CAMERA);
            await request(PERMISSIONS.ANDROID.RECORD_AUDIO);
        }
    };

    const handleViewLoad = () => {
        setViewLoaded(true);
    }

    const initialize = async () => {
        /** Request device permissions */
        await requestDevicePermission();

        /** Initialize RTC engine */
        await RTCClient.createEngine({
            appID: 'Your AppID',
        });

        /** Set relevant callback functions */
        RTCClient.setRTCVideoEventHandler(engineEventListeners);

        /** Set the local rendering view */
        RTCClient.setLocalVideoCanvas(
            StreamIndex.STREAM_INDEX_MAIN,
            {
                viewId,
                renderMode: RenderMode.ByteRTCRenderModeFill,
            },
        );
        /** Create a room instance */
        RTCClient.createRoom('Your roomId, for example, 123456');
        /** Set relevant callback functions */
        RTCClient.setRTCRoomEventHandler(roomEventListeners);

        /** Join room */
        RTCClient.joinRoom({
            userId: 'Your userId, for example, 123456',
            roomConfigs: {
                profile: ChannelProfile.CHANNEL_PROFILE_COMMUNICATION,
                isAutoPublish: true,
                isAutoSubscribeAudio: true,
                isAutoSubscribeVideo: true,
            },
        });

        /** Capture local streams */
        RTCClient.startVideoCapture();
        RTCClient.startAudioCapture();
    }

    useEffect(() => {
        if (isViewLoaded) {
            try {
                initialize();
            } catch {
            }
        }
    }, [isViewLoaded]);

    return (
        <KeyboardAvoidingView
            behavior={Platform.OS === "ios" ? "padding" : "height"}
        >
            <NativeViewComponent
                viewId={viewId}
                onLoad={handleViewLoad}
                kind={
                    Platform.select({
                        android: 'TextureView',
                        ios: 'UIView',
                    })!
                }
            />
        </KeyboardAvoidingView>
    );
};

export default ExamplePage;
```


Now you have completed a basic video call.

If you have other advanced requirements, you can refer to the following documents:


* Screen sharing

   * [Android](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-124176)

   * [iOS](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-124177)
