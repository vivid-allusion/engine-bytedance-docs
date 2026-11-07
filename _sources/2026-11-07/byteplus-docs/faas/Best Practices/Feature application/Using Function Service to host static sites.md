---
title: "Using Function Service to host static sites"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/Using_Function_Service_to_host_static_sites"
---

This article explains how to quickly build a static site through Function Service (FaaS) and obtain an accessible site URL.

<span id=".5Zy65pmv5LuL57uN"></span>
## Scenario introduction

Hosting static sites on the FaaS reduces traffic entry costs and offers benefits such as billing according to the actual usage of resources, automatic scaling, and maintenance\-free operation. The FaaS provides the **vefaas\-nodejs14\-static\-server** code template, allowing you to build static sites based on the Astro framework and quickly serve externally through the API Gateway Trigger.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information

Astro is a multi\-functional Web framework that uses islands of components to build fast, content\-focused websites. For more information, refer to the [Astro official website](https://astro.build/).

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The FaaS is activated.

* API Gateway is activated.

* An API Gateway instance and service have been created. For specific operations, refer to [Creating an instance](https://docs.byteplus.com/en/docs/apig/Creating_an_instance) and [Creating a service](https://docs.byteplus.com/en/docs/apig/Creating_a_service).

* Node.js environment is already deployed locally. It is recommended to download Node.js version 18.x. For specific operations, refer to [the official documentation](https://nodejs.org/en). After successful installation, executing `node --version` will return the Node.js version number.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5q2l6aqk5LiA77ya5pys5Zyw5byA5Y-RIEFzdHJvIOermeeCuQ=="></span>
### Step One: Develop the Astro site locally


1. **Initialize the Astro project locally**

   1. Open the terminal command line tool, navigate to the desired working directory, and execute the following command.

      ```shell
      # Create an Astro project using the default template npm create astro@latest
      ```
      

   2. Follow the prompts of the tool and enter configurations step by step to initialize the Astro project.

   3. Navigate to your Astro project directory, execute the following command to start the Astro site.

      ```shell
      npm run dev
      ```
      

   4. Use the Local URL provided by the system to access the Astro site.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_59bac773d82c087b5f898cf701458c4c.png) </span>

   5. Press `CTRL+C` to exit the service process.

2. **Develop Astro project**

   This example simply modifies the title text in `src/pages/index.astro` to show you the effect of a custom\-developed Astro site. If you want to customize more development, refer to the [Astro official documentation](https://docs.astro.build/en/getting-started/).

   Open the `src/pages/index.astro` file and replace the title "Welcome to Astro" with "Welcome to My Blog". Save and exit.

3. **Build Astro site and obtain static resources**

   Run the following command in the Astro project directory to build the Astro site.

   ```shell
   npm run build
   ```
   

   After successfully building the Astro site, a **dist** folder which is used to store the generated static resources will be generated under the project directory.


<span id=".5q2l6aqk5LqM77ya5bCGIEFzdHJv56uZ54K56Z2Z5oCB6LWE5rqQ6YOo572y6Iez5Ye95pWw5pyN5Yqh"></span>
### Step Two: Deploy Astro site static resources to the FaaS


1. **Create a function**

   Create a function using the **vefaas\-nodejs14\-static\-server** template.

   1. Log in to the [Function Service Console](https://console.byteplus.com/vefaas).

   2. On the top navigation bar, select the target region.

   3. On the function list page, click **Create function**.

   4. On the Create function page, select the **vefaas\-nodejs14\-static\-server** template, then click **Next: function configuration.** 

   5. Enter the function name, keep the function code and advanced configuration as default, then click **Create** to start creating the function.

   After the function is created successfully, it will automatically redirect to the Code tab of the current function.

2. **Upload the code package**

   1. Click the download button in the upper\-right corner to download the function code package locally and unzip it.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_08f24de3e4901d9dd413defb11ead1d5.png) </span>

   2. Replace the contents of the static folder under the **test\-static\-server\-latest** directory with the contents of the **dist** folder obtained in Step One.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_83ec4523bda98b5e3d958eeb1aeaa6c7.png) </span>

   3. Select all files under the **test\-static\-server\-latest** directory and compress them into a Zip package.

      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div>
      

      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">Do not compress the directory directly! Compressing the directory directly will cause the FaaS to fail to find the <code>index.js</code> entry file, blocking the function startup process.      </div>
      

   4. On the Code tab of the current function, click the **Upload** button in the upper\-left corner to upload the code to the FaaS console.

3. **Release the function**

   Release the current code and configuration of the function online.

   1. On the function details page, click **Release** in the upper\-right corner.

   2. Use Latest for **function revision**. Fill in the **revision description** as needed, and keep the **maximum instance number** default.

   3. Click **Confirm,**  the function will be released. The function release is successful as shown in the figure below.


<span id=".5q2l6aqk5LiJ77ya5Yib5bu6IEFQSSDnvZHlhbPop6blj5HlmajvvIzojrflj5YgQXN0cm8g56uZ54K56K6_6Zeu5Zyw5Z2A"></span>
### Step Three: Create an API Gateway trigger to obtain the access address of Astro site

Configure an API Gateway Trigger for the current function to obtain an access address of the public network/private network of the Astro site, thus to achieve a static site providing services to both public and private networks.


1. Switch to the Trigger tab and click **Create Trigger**.

2. Configure the Trigger information as required. For more parameters description, refer to [Creating API Gateway Trigger](https://docs.byteplus.com/en/docs/faas/Creating_a_API_Gateway_trigger).

3. Click **Confirm** to complete the API Gateway Trigger creation.

4. Obtain the public access address shown above and visit your deployed static site in the browser.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7a1e0350caba29fe8b0fcfda81ef97c2.png) </span>


<span id=".5ZCO57ut5pON5L2c"></span>
## Subsequent operations

The FaaS provides powerful version management, and supports canary release, allowing you to conduct agile iteration and development of the static site. The main steps are as follows:


1. Modify the source code information of the project locally and build to obtain the dist directory.

2. Replace the contents of the static directory of the function with the new dist directory, and re\-upload the code package. The operation steps are the same as **2. Upload code package in Step Two**.

3. Republish the function, and select a full release or a canary release as needed. For detailed operations, refer to [Releasing a function](https://docs.byteplus.com/en/docs/faas/Release_function).
