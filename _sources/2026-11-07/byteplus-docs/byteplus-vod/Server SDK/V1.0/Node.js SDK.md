---
title: "Node.js SDK"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-nodejs-sdk"
---

To programmatically manage your video assets and build powerful media features in your application, use the BytePlus VOD Node.js SDK. This guide provides installation steps, authentication configuration, and ready\-to\-use code examples for common operations such as uploading files, generating playback tokens, managing media spaces, and triggering workflows.

<span id="7ed1dd07"></span>
## Prerequisites


* A BytePlus account or an IAM user. For more information, see [Signing up for a BytePlus account](https://docs.byteplus.com/en/byteplus-platform/docs/signing-up-your-account) or [Managing IAM users and roles](https://docs.byteplus.com/byteplus-livesaas/docs/managing-iam-users-and-roles).

* Obtain the AccessKey ID (AK) and Secret Access Key (SK) for authentication.

   * To obtain the AK and SK of a BytePlus account, go to [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/) \> **User Profile** \> **IAM** \> **Key management**.

   * To obtain the AK and SK of an IAM user, complete the following steps:

      1. Go to [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/) \> **User Profile** \> **IAM** \> **Identity management** \> **User**.

      2. Find the user and then click **View details**.

      3. On the **Access key** tab, click **Create new access key**.

* Environment requirements: Install [Node.js](https://nodejs.org/en/download/package-manager) v12.0.0 or later.


<span id="e63ee629"></span>
## Installing the SDK

Use the npm package manager to install the [Node.js SDK](https://www.npmjs.com/package/@byteplus/vcloud-sdk-nodejs).

```Bash
npm install -S @byteplus/vcloud-sdk-nodejs
```


<span id="01584103"></span>
## Setting the AK and SK

To use the SDK, configure your Access Key and Secret Key (AK and SK) using one of the following methods.


* Method 1: Setting the AK and SK in code.

   ```JavaScript
   import { vodOpenapi } from '@byteplus/vcloud-sdk-nodejs';
   // Use the default service instance.
   const vodService = vodOpenapi.defaultService;
   
   // Set the AK and SK
   vodService.setAccessKeyId(AccessKeyId);
   vodService.setSecretKey(SecretKey);
   
   // If using STS to make requests, set the SessionToken after setting the AK and SK
   vodService.setSessionToken(SessionToken);
   ```
   

* Method 2: Setting the AK and SK in environment variables.

   ```JavaScript
   BYTEPLUS_ACCESSKEY="your ak" BYTEPLUS_SECRETKEY="your sk"
   ```
   

* Method 3: Setting the AK and SK in a configuration file.

   1. Create a file named `config.json` in the `~/.byteplus` directory.

   2. Add the following JSON structure to the file:

      ```JSON
      {
          "BYTEPLUS_ACCESSKEY":"your ak",
          "BYTEPLUS_SECRETKEY":"your sk"
      }
      ```
      


<span id="6e5071d1"></span>
## Code examples

This section provides the Node.js SDK code examples.

<span id="904a1cad"></span>
### Creating a space

For more details on the request parameters, see [CreateSpace](https://docs.byteplus.com/docs/byteplus-vod/reference-createspace).

```JavaScript
const CreateSpace = async () => {
  try {
    const options =   {   
     SpaceName: 'Your SpaceName',
      ProjectName: 'Your ProjectName',
      Region: 'Your Region',
      UserName: 'Your UserName',
      Description: 'Your Description',
    }
    const res = awaitvodOpenapiService.CreateSpace(options);;
    // do your work
    // ...
  } catch (err) {
    console.log(err);
  }
};
```


<span id="470839d2"></span>
### Getting space details

For more details on the request parameters, see [GetSpaceDetail](https://docs.byteplus.com/docs/byteplus-vod/reference-getspacedetail).

```JavaScript
const GetSpaceDetail = async () => {
  try {
    const options =   {   
      SpaceName: 'Your SpaceName',
    }
    const res = awaitvodOpenapiService.GetSpaceDetail(options);;
    // do your work
    // ...
  } catch (err) {
    console.log(err);
  }
};
```


<span id="49ce2ba6"></span>
### Listing spaces

For more details on the request parameters, see [ListSpace](https://docs.byteplus.com/docs/byteplus-vod/reference-listspace).

```JavaScript
const ListSpace = async () => {
  try {
    const options =   {  }
    const res = awaitvodOpenapiService.ListSpace(options);;
    // do your work
    // ...
  } catch (err) {
    console.log(err);
  }
};
```


<span id="090b5ce1"></span>
### Updating space upload configurations

For more details on the request parameters, see [UpdateSpaceUploadConfig](https://docs.byteplus.com/docs/byteplus-vod/reference-updatespaceuploadconfig).

```JavaScript
const UpdateSpaceUploadConfig = async () => {
  try {
    const options =    {
      SpaceName: 'Your SpaceName',
      ConfigKey: 2,
      ConfigValue: 'Available',
    },
    const res = awaitvodOpenapiService.UpdateSpaceUploadConfig(options);;
    // do your work
    // ...
  } catch (err) {
    console.log(err);
  }
};
```


<span id="54a7ba75"></span>
### Describing space storage data

For more details on the request parameters, see [DescribeVodSpaceStorageData](https://docs.byteplus.com/docs/byteplus-vod/reference-describevodspacestoragedata).

```JavaScript
const DescribeVodSpaceStorageData = async () => {
 try {
 const options = {
 Aggregation: 300,
 StartTime: '2025-11-10T00:00:00+08:00',
 EndTime: '2025-11-17T23:59:59+08:00',
 SpaceList: 'Your SpaceList',
 Type: 'hot',
 },
 const res = awaitvodOpenapiService.DescribeVodSpaceStorageData(options);;
 // do your work
 // ...
 } catch (err) {
 console.log(err);
 }
};
```


<span id="33f7aea6"></span>
### Uploading audio and video files

Read [media asset upload overview](https://docs.byteplus.com/en/docs/byteplus-vod/docs-media-upload-overview) to learn about the types of media assets and supported formats. For more details on the request parameters, see [ApplyUploadInfo](https://docs.byteplus.com/en/byteplus-vod/reference/applyuploadinfo) and [CommitUploadInfo](https://docs.byteplus.com/en/byteplus-vod/reference/commituploadinfo).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Media asset uploads are asynchronous. A successful submission indicates that the task has been queued, not that it has completed successfully.</div>


* <div data-tips="true" data-tips-type="tip">You must include the file extension. For example, if you want to upload an MP4 file, include <code>.mp4</code> or <code>.MP4</code>.</div>



```JavaScript
const UploadMedia = async () => {
  try {
    const options = {
       FilePath: 'yoour FilePath',
       SpaceName: 'your SpaceName',
    };
    const res = awaitvodOpenapiService.UploadMedia(options);;
    // do your work
    // ...
  } catch (err) {
    console.log(err);
  }
};
```


<span id="17600d9c"></span>
### Uploading materials

Read [media asset upload overview](https://docs.byteplus.com/en/docs/byteplus-vod/docs-media-upload-overview) to learn about the types of media assets and supported formats. For more details on the request parameters, see [ApplyUploadInfo](https://docs.byteplus.com/en/byteplus-vod/reference/applyuploadinfo) and [CommitUploadInfo](https://docs.byteplus.com/en/byteplus-vod/reference/commituploadinfo).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Media asset uploads are asynchronous. A successful submission indicates that the task has been queued, not that it has completed successfully.</div>


* <div data-tips="true" data-tips-type="tip">You must include the file extension. For example, if you want to upload an MP4 file, include <code>.mp4</code> or <code>.MP4</code>.</div>



```JavaScript
const UploadMaterial = async () => {
  try {
    const options = {
      FilePath: 'your FilePath',
      SpaceName: 'your SpaceName',
      FileType: 'object',
      Functions: JSON.stringify([
        { Name: 'GetMeta' },
        {
          Name: 'AddOptionInfo',
          Input: {
            Title: 'your Title',
            Tags: 'your Tags',
            Description: 'your Description',
            Category: 'your Category',
            Format: 'your Format',
            RecordType: 'your RecordType', // number
          },
        },
      ]),
    };
    const res = awaitvodOpenapiService.UploadMaterial(options);;
    // do your work
    // ...
  } catch (err) {
    console.log(err);
  }
};
```


<span id="db98cf19"></span>
### Generating temporary upload token

You can generate a temporary token on your application server using your AK and SK. This process does not require an external network connection. To generate multiple tokens, call the generation method for each token you need. To learn how to use the temporary upload token, see [Client-side uploads](https://docs.byteplus.com/docs/byteplus-vod/docs-client-side-uploads).

```JavaScript
// Generate a temporary upload token with a default expiration time of one hour
vodOpenapiService.GetUploadToken();

// Generate a temporary upload token with custom expiration time
vodOpenapiService.GetUploadToken(30 * 60 * 1000);
```


<span id="6df7020f"></span>
### Generating temporary playback token

You can generate a temporary playback token on the application server using AK and SK without an external network connection. To generate multiple tokens, call the generation method for each token you need.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">To learn how to use the temporary playback token, see <a href="https://docs.byteplus.com/docs/byteplus-vod/docs-playing-videos-with-temporary-playback-tokens">Playing videos with temporary playback tokens</a>.</div>


* <div data-tips="true" data-tips-type="tip">For more details on the request parameters, see <a href="https://docs.byteplus.com/en/docs/byteplus-vod/reference-getplayinfo">GetPlayInfo</a>.</div>



```JavaScript
const getPlayAuthToken = async () => {
  try {
    const tokenExpireTime = 900; // Token expiration time in seconds.The default is 3600 (1 hour)
    const query = {
      Vid: "your vid", // The video ID from the BytePlus VOD service
      FileType: "your file type", // Default is video. Supports: video, audio, evideo (for encrypted video), eaudio (for encrypted audio)
      Quality: "your quality", // Applicable when FileType is audio, eaudio. Supports: medium, higher, highest.
      Definition: "your definition", // Applicable when FileType is video and evideo. Supports: 240p, 360p, 480p, 540p, 720p, 1080p, 2k, 4k. By default, all definitions are included.
      Format: "your format",
      Codec: "your codec",
      Ssl: "your ssl", // Indicates whether to return HTTPS address. 1: true, 0: false
    };
    const res = vodOpenapiService.GetPlayAuthToken(query, tokenExpireTime);
    // perform your tasks
    // ...
  } catch (err) {
    console.log(err);
  }
};
```


<span id="1ef87c75"></span>
### Getting playback addresses by video ID

For more details on the request parameters, see [GetPlayInfo](https://docs.byteplus.com/en/docs/byteplus-vod/reference-getplayinfo).

```JavaScript
const GetPlayInfo = async () => {  
   try {
      // get your options from query    
      const options = {      
      Vid: "your Vid",
    };
    const res = await vodOpenapiService.GetPlayInfo(options);
    // perform your tasks
    // ...
  } catch (err) {    
     console.log(err);
  }
};
```


<span id="8d4fc2ab"></span>
### Publishing an audio or video file

For more details on the request parameters, see [UpdateMediaPublishStatus](https://docs.byteplus.com/en/docs/byteplus-vod/reference-updatemediapublishstatus).

```JavaScript
const updateMediaPublishStatus = async () => {
  try {
   const options = {
     Vid: "your vid",
     Status: "your status", // Published or Unpublished
   };
   const res = await vodOpenapiService.UpdateMediaPublishStatus(options);
   // perform your tasks
   // ...
  } catch (err) {
    console.log(err);
  }
};
```


<span id="dc780ba6"></span>
### Triggering a workflow for a specific audio or video file

For more details on the request parameters, see [StartWorkflow](https://docs.byteplus.com/en/docs/byteplus-vod/reference-startworkflow).

```JavaScript
const startWorkflow = async () => {
  try {
    const options = {
      Vid: "your vid",
      TemplateId: "your template id", // workflow id
      CallbackArgs: "your callback args", // The server will include this value in the 'callbackargs' field of your callback.
    };
    const res = await vodOpenapiService.StartWorkflow(options);
    // perform your tasks
    // ...
  } catch (err) {
    console.log(err);
  }
};
```


<span id="5dba715a"></span>
### Generating DRM auth token

```JavaScript
const startWorkflow = async () => {
  try {
    const options = {
      Vid: "your vid",
    };
    const res = await vodOpenapiService.GetThirdPartyDrmAuthToken(options);
    // do your work
    // ...
  } catch (err) {
    console.log(err);
  }
};
```


<span id="d07fa2ca"></span>
### Generating subtitle auth token

```JavaScript
const GetSubtitleAuthToken = async () => {
  try {
    const options = {
      Vid: "your vid",
    };
    const res = await vodOpenapiService.GetSubtitleAuthToken(options);
    // do your work
    // ...
  } catch (err) {
    console.log(err);
  }
};
```


<span id="5ad2120b"></span>
### Updating subtitle file status

For more details on the request parameters, see [UpdateSubtitleStatus](https://docs.byteplus.com/en/docs/byteplus-vod/reference-updatesubtitlestatus).

```JavaScript
const UpdateSubtitleStatus = async () => {
  try {
    const options = {
      Vid: 'your vid',
      Status: 'your status',
      FileIds: 'your fileIds',
      Formats: 'your formats',
      Languages: 'your languages',
    };
    const res = await vodOpenapiService.UpdateSubtitleStatus(options);
    // do your work
    // ...
  } catch (err) {
    console.log(err);
  }
};
```


<span id="c214eee7"></span>
### Getting subtitle info list

For more details on the request parameters, see [GetSubtitleInfoList](https://docs.byteplus.com/en/docs/byteplus-vod/reference-getsubtitleinfolist).

```JavaScript
const GetSubtitleInfoList = async () => {
  try {
    const options = {
      Vid: 'your vid',
      FileIds: 'your FileIds',
      Formats: 'your Formats',
      Languages: 'your Languages',
      LanguageIds: 'your LanguageIds',
      Status: 'your Status',
      Ssl: '1',
      SubtitleIds: 'your SubtitleIds',
      Title: '',
      Tag: '',
      Offset: '0',
      PageSize: '3',
    };
    const res = await vodOpenapiService.GetSubtitleInfoList(options);
    // do your work
    // ...
  } catch (err) {
    console.log(err);
  }
};
```


<span id="4567d38f"></span>
### Updating subtitle info

For more details on the request parameters, see [UpdateSubtitleInfo](https://docs.byteplus.com/en/docs/byteplus-vod/reference-updatesubtitleinfo).

```JavaScript
const UpdateSubtitleInfo = async () => {
  try {
    const options = {
      Vid: 'your vid',
      FileIds: 'your FileIds',
      Formats: 'your Formats',
      Languages: 'your Languages',
      Title: 'your Title',
      Tag: 'your Tag',
    };
    const res = await vodOpenapiService.UpdateSubtitleInfo(options);
    // do your work
    // ...
  } catch (err) {
    console.log(err);
  }
};
```


<span id="6da85b37"></span>
### Creating CDN refresh task

For more details on the request parameters, see [CreateCdnRefreshTask](https://docs.byteplus.com/en/docs/byteplus-vod/reference-createcdnrefreshtask).

```JavaScript
const CreateCdnRefreshTask = async () => {
  try {
    const options = {
      Urls: 'your Urls',
      Type: 'your Type',
      SpaceName: 'your SpaceName',
    };
    const res = await vodOpenapiService.CreateCdnRefreshTask(options);
    // do your work
    // ...
  } catch (err) {
    console.log(err);
  }
};
```


<span id="feb42552"></span>
### Listing snapshots

For more details on the request parameters, see [ListSnapshots](https://docs.byteplus.com/en/docs/byteplus-vod/reference-listsnapshots).

```JavaScript
const ListSnapshots = async () => {  
   try {
      // get your options from query    
      const options = {      
      Vid: "your Vid",
    };
    const res = await vodOpenapiService.ListSnapshots(options);
    // perform your tasks
    // ...
  } catch (err) {    
     console.log(err);
  }
};
```
