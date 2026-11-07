---
title: "Custom Visualization Overview"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Custom_Visualization_Overview"
---

<span id="b0c2b9d6"></span>
# 1. Overview

Custom visualization is one of the open capabilities provided by this product, which allows users to create personalized data presentations according to their needs. This capability includes not only Custom Fields and configuration options, but also compatibility support for multiple frameworks. In addition to leveraging the system's preset Chart components, users can also use the Component Software Development Kit (SDK) and popular tools in the community to further develop and customize their own Charts and controls. This provides users with great flexibility, making the data performance more in line with specific Scenario and personal preferences. (Currently, the custom visualization function is still in the closed beta stage. If you have specific needs for this function, please contact the BytePlus commerce team for more details on purchasing and collaborating.)

<span id="eb741be0"></span>
# 2. Quick start

First, you need to quickly understand the basic development process with the `Echarts Pie Chart`plugin. The plugin loads a `Pie Chart`Chart based on `Echarts`in the Chart of Visual Query.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/009e3033d6784610a90de871d19fdee1~tplv-goo7wpa0wc-image.image) </span>

<span id="6a5d991f"></span>
# 3. Specific operation process

<span id="453e7ec4"></span>
## 3.1 Environmental preparation

You need to complete the following two items to prepare the required environment:

 **(1) Install Node and Npm**

Node.js installation package and source code download address is: [https://nodejs.org/zh-cn/download/](https://nodejs.org/zh-cn/download/)

After you install Node, Npm is automatically installed.

 **(2) plugin power builder**  **`@datawind/extension-cli`**

You can use the CLI tool `@datawind/extension-cli`to debug and compile plug\-in projects. By calling `datawind-extension -h`, you can see all the commands.

```Bash
npm i -g @datawind/extension-cli
datawind-extension -h
```


**Note** : If the current `registry`is not https://registry.npmjs.org, you need to specify a `registry`for installation:

```Shell
npm i -g @datawind/extension-cli --registry=https://registry.npmjs.org
```


<span id="ecc519d4"></span>
## 3.2 Initialization of the project

First, please download the following sample plug\-in archive.

React + Echarts Template Package:

<Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0008d70708d946a3a55373c93d3a05c5~tplv-goo7wpa0wc-image.image" name="react-echarts.zip">react-echarts.zip</Attachment>


&nbsp;

Vue + Echarts Template Package:

<Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/afb265d714c34e629a8ce37363a99c4f~tplv-goo7wpa0wc-image.image" name="vue-echarts.zip">vue-echarts.zip</Attachment>


&nbsp;

Secondly, after you download the plug\-in compressed package, you need to unzip it, and then enter the project root directory of the plug\-in package to install the dependencies.

```Shell
cd <YOUR_PROJECT_DIR>
npm install

// 同上，如果当前使用的registry不是https://registry.npmjs.org，需要指定registry进行安装
npm install --registry=https://registry.npmjs.org
```


Finally, the role of each file in the project will be described in detail in [the article "Custom Chart Plugin Structure" ](https://www.volcengine.com/docs/4726/1232739), where you can first complete the operation flow of developing Chart.

<span id="5d5e81a8"></span>
## 3.3 Commissioning

You need to do the following to debug your development environment.

 **(1) Execute** **`npm run dev to start`the plugin**

```Bash
npm run dev
```


If you access [http://localhost:5000/satellite/dev/extension ](http://localhost:5000/satellite/dev/extension)see the Json description of the plug\-in, the local plug\-in debugging server started successfully.

 **(2) Start the development environment and debug plug\-ins**

**Step 1** : Enter the product plug\-in debugging settings page `https://< HOST >/< PATH >/#/devtools/extensionDebug`


* Set the port number `5000`(the same as the debug port number configured locally)

* Switch the switch to `enable`, click `Confirm`

* Enable local plug\-in debugging


**Step 2** : Enter the Visual Query page of this product `https://< HOST >/< PATH >/#/dataQuery`


* The plug\-in Chart can be seen below the location of the original Chart selection area.

* Select the locally developed `Pie Chart`plugin Chart, add a Dimension and a Measure, and output the rendering result of the Chart in the Chart area on the right.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/05334399c4c540cebd2f4d5b0b7066ae~tplv-goo7wpa0wc-image.image) </span>

<span id="421baec3"></span>
# 4. Access address description

The URL mentioned in this article `https://< HOST >/< PATH >`has different settings in different deployment environments. You can directly access this product to confirm the current HOST and PATH.

For example, suppose a Dashboard address in your deployment environment is: https://company.site.com/console/bi/#/dashboard/1?appId=2, then:


* HOST=company.site.com

* PATH=console/bi

* Plugin debugging configuration address: https://company.site.com/console/bi/#/devtools/extensionDebug

* Visual Query page address: https://company.site.com/console/bi/#/dataQuery
