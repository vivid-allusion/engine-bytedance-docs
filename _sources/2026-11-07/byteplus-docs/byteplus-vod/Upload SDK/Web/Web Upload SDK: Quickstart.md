---
title: "Web Upload SDK: Quickstart"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-web-upload-sdk"
---

To upload files from your web app to BytePlus VOD, you can integrate the Web Upload SDK. This guide provides step\-by\-step instructions and code examples covering SDK import, instance creation, and file upload management to help you get started quickly.

<span id="00a9e6f9"></span>
### Step 1: Import the SDK

To import the SDK, use [npm](https://www.npmjs.com/package/@byteplus/uploader) or the script tag:

<span id="5175ad2e"></span>
#### Using npm

```Shell
npm install @byteplus/uploader
```


<span id="5e38370f"></span>
#### Using the script tag

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Replace x.x.x with the version number. To get the latest version number, see <a href="https://docs.byteplus.com/docs/byteplus-vod/docs-web-upload-sdk-changelog">Web Upload SDK: Release notes</a>.</div>


```HTML
<script src="https://unpkg.com/@byteplus/uploader@x.x.x/dist/index.js"></script>
<script>
    const uploader = new BytePlusUploader({...});
</script>
```


<span id="ea6839ce"></span>
### Step 2: Create an `uploader` instance

To create an `uploader` instance, see the following sample code:

```JavaScript
import BytePlusUploader from '@byteplus/uploader';
const uploader = new BytePlusUploader({
    userId: 'xxx', // The unique user ID
    appId: xxx, // The app ID which you can get from the BytePlus VOD console
    region: 'ap-singapore-1', // For the Asia Pacific Southeast (Johor) region, use "ap-southeast-1"
    videoConfig: {
        spaceName: 'xxx' // The name of the space for storing the uploaded files 
 }
});
```


<span id="99c95025"></span>
### Step 3: Add the file to be uploaded

Call `addFile` to add the file to be uploaded.

```JavaScript
const fileKey = uploader.addFile({
    file: fileList[0],
    stsToken: {   // stsToken is an object with multiple properties obtained from the server
    CurrentTime: 'xxx',
    ExpiredTime: 'xxx',
    SessionToken: 'xxx',
    AccessKeyID: 'xxx',
    SecretAccessKey: 'xxx'
    }, 
    stsToken: token,
    type: 'video', // Set the file type as `video`, `image`, `object`, or `media`
  });
```


<span id="d19eca33"></span>
### Step 4: Listen for the SDK events

To listen for the SDK events, see the following sample code:

```JavaScript
uploader.on('complete', (infor) => {
    console.log('complete');
    console.log(infor.uploadResult);
});

uploader.on('error', (infor) => {
    console.log(infor.extra);
});

uploader.on('progress', (infor) => {
    console.log(infor.percent)
});
```


<span id="6817f431"></span>
### Step 5: Start uploading

Call `start` and pass in the `fileKey` .

```JavaScript
uploader.start(fileKey);
```
