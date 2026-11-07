---
title: "Web Player SDK: Quickstart"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-getting-started-with-the-web-player-sdk"
---

To quickly add video playback to your web application, you can integrate the BytePlus VOD Player SDK. This guide provides the essential steps to get started, including adding SDK dependencies, configuring your license, creating a player instance, and enabling quality monitoring. By following these instructions, you can implement a cross\-browser compatible player that supports advanced features like anti\-hotlinking and encrypted video playback.

<span id="336445f3"></span>
## Prerequisites

BytePlus VOD uses licenses to manage the usage rights and duration of the Player SDK and its value\-added services. During the project testing phase, you can apply for a free trial license in the BytePlus VOD console. You must create an application, apply for a free trial license, and bind the license to the application. For detailed instructions, see [Licenses](https://docs.byteplus.com/docs/byteplus-vod/docs-license-management).

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div>


<div data-tips="true" data-tips-type="warning">A trial license is for project testing only and cannot be renewed. An expired trial license will cause authentication to fail, which will affect the normal use of the service. Before the project goes live, please upgrade to an official license.</div>


<span id="741f6adb"></span>
## Procedure

<span id="70294bdd"></span>
### Step 1: **Add SDK dependencies**

There are three ways to import the SDK:

```mixin-react
const Render = () => {
  const sdkId = 49;
   const [data, setData] = React.useState({})
  const [fileInfo, setFileInfo] = React.useState({})

      const fixUrl = (versionId, fileName) => {
    if (!versionId || !fileName) return "";
    const link = `https://demo.volcvideo.com/exampleCenter/dynamicMarkdownManage/sourceFixedLink?queryType=sdk_version_source&reference_sdk_id=${sdkId}&reference_sdkversion_id=${versionId}&fileName=${fileName}&_sourceName=vsop`
    return link;
  };


React.useEffect(() => {

fetch(`https://demo.volcvideo.com/exampleCenter/sdkManage/queryAggregationData?id=${sdkId}&_sceneName=on_demand&_sourceName=vsop`, { mode: "cors", method: "get", headers: { "content-type": "application/json", "x-request-source": "Sandbox" } }).then(async(res)=>{
        const { Result } = await res.json();
        const { versions } = Result[0];
        const { package_list, id } = versions.find(ver => ver.status === 'published');
        console.log(JSON.stringify(package_list[0]))
        setData(package_list[0])
        setFileInfo({
          versionId: id,
          fileName: package_list[0]?.url.substring(package_list[0]?.url.lastIndexOf('/') + 1),
        })
 })
}, [])

   const scriptSrc = (data?.subFileList || []).find((item)=>item.endsWith('js'))
      const cssSrc = (data?.subFileList || []).find((item)=>item.endsWith('css'));
const dirArr = data?.url?.split('/') || [];
const version = dirArr.length - 3 > -1 ? dirArr[dirArr.length - 3] : '';
const fileName = 'VePlayer ' + version + '.zip';
return data.url?(
<Tabs defaultActiveTab="1">
  <Tabs.TabPane title="UMD" key="1">
  <RenderMd content={`
Add the following code to the index.html file in your local project. This code imports the CSS file and JS file of the Web Player SDK:
  `}></RenderMd>
  <PreCode lang="html" text={`
<link rel="stylesheet" href="${`https://sf-unpkg.bytepluscdn.com/obj/byteplusfe-sg/sdk/@byteplus/veplayer/${version}/index.min.css`}"/>
<script src="${`https://sf-unpkg.bytepluscdn.com/obj/byteplusfe-sg/sdk/@byteplus/veplayer/${version}/index.min.js`}"></script>
        `} />
  </Tabs.TabPane>
  <Tabs.TabPane title="Manual installation" key="2"><RenderMd content={`

1. Download the following zip package.

   `}>
   </RenderMd>

   <Attachment link={fixUrl(fileInfo?.versionId, fileInfo?.fileName)} name={fileName} size={data?.fileSize}></Attachment>

   <RenderMd content={`

2. Extract the JavaScript and CSS files from the zip package and place them in the appropriate directory within your project, such as the lib directory.

   `}></RenderMd>

<PreCode text={`
.
├── index.html
├── package.json
├── index.js
├── lib
    └── index.min.js
    └── index.min.css
        `} />

<RenderMd content={`

3. Manually reference the JavaScript and CSS files in your HTML or JavaScript code using <script> tags or module import statements. If you place these files in the lib directory, the code to import the dependencies in your HTML code would look like this:

  `}></RenderMd>


<PreCode lang="html" text={`
<script src="./lib/index.min.js" type="text/javascript"></script>
<link rel="stylesheet" href="./lib/index.min.css" />
        `} />


  </Tabs.TabPane>
     
  <Tabs.TabPane title="npm" key="3"><RenderMd content={`

1. Run the following command to import the SDK via [npm](https://www.npmjs.com/package/@byteplus/veplayer?activeTab=readme):
  
\`\`\`node
npm install @byteplus/veplayer@${version}
\`\`\`

2. After installing, import VePlayer and its CSS file to your project as shown below:

\`\`\`javascript
import VePlayer from '@byteplus/veplayer';
import '@byteplus/veplayer/index.min.css';
\`\`\`
  `}></RenderMd></Tabs.TabPane>  

       
</Tabs>):null;
}
return <Render />
```


<span id="948d1f6a"></span>
### Step 2: Add a player container

To add a player container to the page where you want to display the player, add the following code to `index.html`:

```HTML
<div id="video"></div>
```


<span id="5c74adef"></span>
### **Step 3: Configure the license**

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>



* <div data-tips="true" data-tips-type="tip">Starting from version 1.15.0, you must configure the license to use the Player SDK.</div>


* <div data-tips="true" data-tips-type="tip">Ensure that the domain of the page where the player is located is the same as the domain you provided when applying for the license, or a subdomain of it. Otherwise, the license verification will fail.</div>



License verification is performed at the page level, so you only need to set it once, even in a single\-page, multi\-instance scenario. To optimize the playback experience and improve the first\-frame loading speed, it is recommended to configure the license before initializing the player. VePlayer supports the following methods for configuring the license:


<Tabs>
<Tab zoneid="FPROLP0yZc" title="Set license file content">
<TabTitle>Set license file content</TabTitle>

Call `setLicenseConfig` and provide the license file content.


* `sign`: The `Signature` from the license file, used for authentication.

* `content`: The `Content` from the license file, which includes permission levels and version information.

* `mainUrl`: (Optional) The online URL of the license file. If provided, the SDK automatically updates to the latest license version upon upgrade or renewal.


Sample code:

```JavaScript
VePlayer.setLicenseConfig({
  license: {
    sign: "xxx",
    content: "xxx",
    mainUrl: "xxx", 
 },
})
```



</Tab>
<Tab zoneid="AkzM3lCDks" title="Set license file online address">
<TabTitle>Set license file online address</TabTitle>

Call `setLicenseConfig` and provide the online address of the license file. The SDK will automatically handle the authentication logic and enable automatic license updates.

```JavaScript
VePlayer.setLicenseConfig({
    license: "http://example.volcengine.com/obj/vod-license/license.lic"
})
```



</Tab>
</Tabs>


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>



* <div data-tips="true" data-tips-type="tip">If the player initializes and plays a video without any license\-related errors, the verification is successful.</div>


* <div data-tips="true" data-tips-type="tip">To facilitate local integration and debugging for developers, the License verification result defaults to the Premium License for the local domain name localhost and local IP addresses such as 127.0.0.1 and 192.168.<em>.</em>.</div>



<span id="c34c170d"></span>
### Step 4: Create a player instance

Create a player instance with the appropriate configuration settings. The player starts playing once the page loads.


<Tabs>
<Tab zoneid="eHOiIAGjNO" title="URL">
<TabTitle>URL</TabTitle>

One way to set the video source is by passing in the container ID and the URL of the video you want to play. See the following sample code:

```JavaScript
const playerSdk = new VePlayer({
  id: 'video',
  url: 'xxx.mp4'
});
```



</Tab>
<Tab zoneid="GPY4uXJ74M" title="VID">
<TabTitle>VID</TabTitle>

You can also play a video by setting `Vid` and `playAuthToken`. For details, see [Play a video with vid and playAuthToken](https://docs.byteplus.com/docs/byteplus-vod/docs-implementing-basic-features-web#78bc4285).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="tip">To play videos that are in formats other than MP4 or encrypted, you need to configure cross\-domain resource sharing (CORS) for the video resource. If the video is hosted on a CDN, you should contact the CDN provider for assistance in configuring CORS.</div>



</Tab>
</Tabs>


<span id="e473800a"></span>
### Step 5: Report playback quality logs

To monitor important playback metrics such as video views, unsuccessful playback rate, and time to first frame, implement the playback quality reporting feature. This feature allows you to track and analyze these metrics on the **Quality insights** page of the BytePlus VOD console. For details, see [Quality insights overview](https://docs.byteplus.com/docs/byteplus-vod/docs-quality-insight-overview).

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Player version requirement</div>


<div data-tips="true" data-tips-type="warning">Since May 1, 2026, to ensure the quality and compliance of the log reporting pipeline, use Web Player SDK version 1.16.0 or later. If you use an earlier version, some features on the <strong>Quality insights</strong> page may be unavailable.</div>


To implement the playback quality reporting, you can simply set the `vodLogOpts` parameter during the instantiation of the player. This parameter allows you to customize the reporting settings according to your requirements. Here's a sample code snippet:

```JavaScript
const player = new VePlayer({
  id: 'video',
  width: 600,
  height: 400,
  url: "https://demo.vod.com/xxx.mp4",
  vodLogOpts: {
    line_app_id: XXXX, // [Required] The Application ID for Video On Demand, which is an integer value. You can obtain it from the SDK management > Applications page in the BytePlus VOD console.
    line_user_id: 'XXX', // The user ID, either a string or an integer. If not provided, a random value will be generated based on the user's browser.
    tag: 'Normal Video', // A tag corresponding to the type of the content, used to differentiate business scenarios for future multi-dimensional analysis.
  }
});
```


<span id="e7ea579d"></span>
## Next steps

The Web Player SDK offers a range of features that cater to various playback scenarios. These include the ability to add custom cover images, enable picture\-in\-picture mode, display preview thumbnails when hovering over the progress bar, and even play encrypted videos. To incorporate the basic and advanced features of the Web Player SDK, see the following articles:


* [Web Player SDK: Basic features](https://docs.byteplus.com/docs/byteplus-vod/docs-implementing-basic-features-web)

* [Web Player SDK: Advanced features](https://docs.byteplus.com/docs/byteplus-vod/docs-implementing-advanced-features-web)

* [Web Player SDK: API reference](https://docs.byteplus.com/docs/byteplus-vod/docs-web-api-reference)
