---
title: "Trying the Video Editing Web SDK demo"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/video_editing_web_sdk_demo"
---

VevDemo is a complete Web application that demonstrates how to integrate and use the Video Editing Web SDK. It consists of a Vue/React frontend built with Vite and a Node.js backend. This guide walks you through deploying the demo locally and trying the main video editing features.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Region availability</div>


<div data-tips="true" data-tips-type="tip">The Video Editing Web SDK is currently available only in the Asia Pacific (Johor) region. Use <code>ap-southeast-1</code> when configuring the SDK and its backend APIs.</div>


<span id="prerequisites"></span>
## Prerequisites

Before running the demo, ensure that you have completed the following:


* [Create a BytePlus account](https://console.byteplus.com/auth/signup/) and enable BytePlus VOD. For details, see [Getting started with BytePlus VOD](https://docs.byteplus.com/docs/byteplus-vod/docs-getting-started).

* Create a VOD space in the Asia Pacific (Johor) region for storing editing materials and exported videos.

* [Upload media assets](https://docs.byteplus.com/docs/byteplus-vod/docs-upload-media) to the VOD space.

* Create an IAM user, grant the permissions required to access the VOD space, and obtain its Access Key ID (AK) and Secret Access Key (SK). For details, see [Access authorization overview](https://docs.byteplus.com/docs/byteplus-vod/docs-access-authorization).

* Install the following software in your development environment:

   * Node.js v14 or later. An [LTS version](https://nodejs.org/) is recommended.

   * npm, which is normally installed with Node.js.


<span id="run-the-demo"></span>
## Run the demo

<span id="download-the-demo"></span>
### Step 1: Download the demo

<Attachment link="https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260817085707-201089235224.zip" name="vevdemo.zip">vevdemo.zip</Attachment>


Download `vevdemo.zip` and extract it to a local working directory. The extracted directory has the following structure:

```text
vevdemo/
├── fe/          # Frontend project
├── nodejs/      # Node.js backend
└── package.json
```


<span id="start-the-backend"></span>
### Step 2: Configure and start the backend

The backend calls BytePlus VOD APIs for operations such as project management, material management, and export task submission. Configure the AK and SK only on the backend.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Credential security</div>


<div data-tips="true" data-tips-type="warning">Never place an AK or SK in frontend code, commit it to source control, or expose it to the browser. Use a dedicated IAM user with only the permissions required by your application.</div>



1. Go to the backend directory:

   ```shell
   cd vevdemo/nodejs
   ```
   

2. Create a file named `.env` in this directory.

3. Add the following values. Replace the environment\-variable name placeholders after the BytePlus demo package is confirmed, and replace the sample values with your credentials:

   ```dotenv
   BYTEPLUS_ACCESS_KEY=your-access-key-id
   BYTEPLUS_SECRET_KEY=your-secret-access-key
   ```
   

4. Install the dependencies and start the backend:

   ```shell
   npm install
   npm run dev
   ```
   

   When the terminal displays output similar to `Server is running on http://localhost:3001`, the backend is ready.


<span id="start-the-frontend"></span>
### Step 3: Configure and start the frontend


1. Open another terminal and go to the frontend directory:

   ```shell
   cd vevdemo/fe
   ```
   

2. Obtain the IDs required to initialize the editor:

   * **`projectId`** ** and ** **`groupId`** ** (required):**  Log in to the [BytePlus VOD console](https://console.byteplus.com/vodpaas), enter the Johor VOD space, and select **Video editing \> Projects**. Create a project and open it. Copy the `projectId` and `groupId` from the page URL.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">Note      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Obtaining the IDs from the console is intended only for quickly trying the demo. In a production application, call <a href="https://docs.byteplus.com/docs/byteplus-vod/reference-createproject">CreateProject</a> from your backend. For integration requirements, see <a href="https://docs.byteplus.com/docs/byteplus-vod/integrating_video_editing_web_sdk#prerequisites">Prerequisites</a>.      </div>
      

   * **`defaultClassificationId`** ** (optional):**  In the BytePlus VOD console, select **System settings \> Categories** and copy the ID of the category to select by default. For details, see [Categories](https://docs.byteplus.com/docs/byteplus-vod/docs-system#e83439dc). Leave this value empty to use **Uncategorized**.

3. Open `fe/index.js` and configure the IDs:

   ```javascript
   projectId: '',                 // Required. Enter your project ID.
   groupId: '',                   // Required. Enter your group ID.
   defaultClassificationId: '',  // Optional. Empty or null means Uncategorized.
   ```
   

4. Install the dependencies and start the frontend:

   ```shell
   npm install
   npm run dev
   ```
   

   The Vite development server normally listens on `http://localhost:8084`.


<span id="try-the-editor"></span>
### Step 4: Try the editor

Open `http://localhost:8084` in a browser. You can upload or import materials, arrange them on the timeline, add text, transitions, effects, and filters, and submit an export task.

<span>![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20260817090202-1139835059409.png) </span>

<span id="faq"></span>
## FAQ

<span id="what-should-i-do-if-a-port-is-already-in-use"></span>
### What should I do if a port is already in use?

By default, the backend and frontend use ports `3001` and `8084`, respectively. Stop the process using the port, or change the backend port in `nodejs/config/default.js` and the frontend port in `fe/vite.config.js`.

<span id="what-should-i-do-if-npm-install-fails"></span>
### What should I do if `npm install` fails?

Check your network and proxy configuration, then retry. If the npm cache is corrupted, run `npm cache clean --force` and install the dependencies again.

<span id="why-does-the-page-open-but-uploading-or-editing-does-not-work"></span>
### Why does the page open but uploading or editing does not work?

Check the following:


* The backend is running without errors.

* The `.env` file is in the `nodejs` directory and is not named `.env.txt`.

* The credential and region values are correct. Restart the backend after changing `.env`.

* The frontend sends requests to the correct backend address, such as `http://localhost:3001`.

* The browser console does not report blocked cross\-origin requests.


For a production integration, see [Integrating the Video Editing Web SDK](https://docs.byteplus.com/docs/byteplus-vod/integrating_video_editing_web_sdk).
