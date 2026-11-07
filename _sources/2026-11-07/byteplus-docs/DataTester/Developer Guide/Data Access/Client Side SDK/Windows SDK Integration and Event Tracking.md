---
title: "Windows SDK Integration and Event Tracking"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/Windows-SDK-Integration-and-Event-Tracking"
---

<span id="fee3cc2f"></span>
# Notes before operation


* SDK version: The current SDK version is being released in continuous iterations. You can go to the [Git open source page ](https://github.com/volcengine/datarangers-sdk-packages/tree/main)to view the SDK version of each end. The latest version of the SDK is recommended. The code examples in this article use a version number as an example. When you actually use it, you need to modify the version number according to the actual SDK version you are using.

* Download the SDK package: When integrating the SDK, if you need to manually import the SDK, you need to go to the [Git open source page ](https://github.com/volcengine/datarangers-sdk-packages/tree/main)to download the corresponding version of the SDK package.


<span id="78282415"></span>
# 1. Get the configuration parameters

<span id="f381eed5"></span>
## Version 1.1 Support Notes

Currently, only 32\-bit and 64\-bit Windows platforms are supported.

<span id="a2886d0b"></span>
## 1.2 Get the appid

Before starting the integration, you first need to access a project and application in the group. Before integrating the SDK, you need to obtain the appid, appkey, and other information of the corresponding application.

In the privatization scenario, you can view the appid, appkey and other information of the application in **Project management** \> **Project details** \> **Application list**, please refer to the details [View AppID, Appkey, and other information](https://docs.byteplus.com/docs/DataTester/Project-and-Application-Management_#c6975388).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fb76ac626e9d4712a95e4ca7c2e244d7~tplv-goo7wpa0wc-image.image) </span>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The viewing entrance paths of different privatized versions are inconsistent. The viewing path of the historical old version is Global Settings \> Group Settings, and the above path is the viewing entrance path of the current latest version.</div>


<span id="1c4212c5"></span>
## 1.3 Obtain the data upload address

The private deployment version needs to get the data upload `reportURL`.

If you are unsure of this address, please contact your project manager or customer success manager.

<span id="ebe7f8e8"></span>
# 2. Integration, Growth Marketing Suite SDK

<span id="c1309900"></span>
## 2.1 Download the SDK

Please go to the [Windows SDK package download page ](https://github.com/volcengine/datarangers-sdk-packages/tree/main/Windows)to obtain the corresponding version of the SDK package.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Windows offline package names are in <code>windows_</code><code><em>version number</em></code><code>.zip</code>format. For example: <code>windows_1.2.4.zip</code>, where 1.2.4 is the SDK version number.</div>


* <div data-tips="true" data-tips-type="tip">After downloading the SDK offline package, please unzip the compressed package, including:</div>


   * <div data-tips="true" data-tips-type="tip">WindowsSDK (32\-bit): For the unzipped <code>._x86 .zip</code>SDK package</div>


   * <div data-tips="true" data-tips-type="tip">WindowsSDK (64\-bit): For the unzipped <code>._x64 .zip</code>SDK package</div>



<span id="c0368dc5"></span>
## 2.2 SDK file description

Please download the SDK file compressed package of the corresponding platform. After decompression, three files, applogrs.hpp, applogrs.dll, and applogrs.dll.lib, will appear:


* Applogrs.hpp: Public interface header file.

* Applogrs.dll: The DLL file that is loaded at the runtime of the dynamic link library.

* Applogrs.dll.lib: The function export declaration file corresponding to the applogrs.dll file.


<span id="513a07c3"></span>
## 2.3 Integration

Copy the downloaded SDK file to the project, and note that the platform architecture file is placed in the corresponding platform build directory of the project.

<span id="851218a7"></span>
#### 2.3.1 Add Additional Library Directory

Modify the project properties \- configuration properties \- connector \- general \- additional library directory, increase the directory where the `applogrs.dll`file is located.

<span id="e5d9487a"></span>
#### 2.3.2 Add Function Export File

Modify Project Properties \- Configuration Properties \- Connectors \- General \- Additional Dependencies, add text content `applogrs.dll.lib`.

<span id="4d8de0bd"></span>
#### 2.3.3 add header files

Modify Project Properties \- Configuration Properties \- C/C++ \- Attach the include directory and increase the directory where the `applogrs.hpp`file is located.

<span id="69b6b1ee"></span>
#### Introducing header files 2.3.4 code

In the header of the code file that needs to call the SDK, the imported `applogrs.hpp`header file is displayed:

```C++
#include "applogrs.hpp"
```


<span id="5ec9ecea"></span>
# 3. Initialization, Growth Marketing Suite SDK

**Description**:

After initializing the SDK, some device information of the system will be collected, including device serial number, operating system software version, etc.

<span id="67555df1"></span>
## 3.1 Initializing the SDK

The SDK will cache data such as event tracking. In order to ensure that the data is not lost, the data needs to be persisted to the local disk. You need to prepare a file directory in advance where data can be written (the SDK does not automatically create directories).

```C++
// 1. Set the data cache directory, which requires existing file directories with access and write data permissions
applog::setDbDir("/xx/xx");
// 2. Set the domain name. If it is a private deployment, please pass in the private domain name.
char* domain = "https://xxx.xxx.xxx"
applog::setCustomDomain(domain); // server domain name
// 3. Enable A/B testing, which is turned off by default. If want to turn it off, please set to (0)
applog::setAbTestEnabled(1); 
// 4. To initialize SDK, it is necessary to prepare the appId and appChannel in advance (appChannel is usually the name of the published channel)
applog::init_rangers(appId, appChannel);
```


<span id="3df5e58e"></span>
# 4. Report experimental metrics (user behavior events)

<span id="fbf10d11"></span>
## 4.1 Obtaining experimental parameters

Usually, a shunt request is sent to the shunt service after the SDK is initialized. After obtaining the response of the shunt service, the client side development can complete the code branch according to the result parameters of the shunt.


* Please note the precondition of this step: the experiment and related parameters have been created according to the demand side of the experiment, see [Programming Experiment](https://docs.byteplus.com/docs/DataTester/Programming-Experiment).

* Note that each time getAbTestConfig is called, an exposure event **abtest_exposure** is reported by default.


```TypeScript
// Obtain all experimental parameters
const char* allConfigs = applog::getAllAbTestConfigs();

// Obtain the specified experimental parameters and report the exposure event abtest_dexposure
// params1: experimental configured key
// params2: If the remote experiment configuration interface is not obtained, the parameter value will be returned.
const char* config = applog::getAbTestConfig("key", "defaultValue");
```


<span id="386c37a9"></span>
## 4.2 Reporting event tracking

Support event tracking collection at any location. The event tracking content includes event tracking name and event tracking parameters. Interface example:

```C++
// Collect an event tracking here
// parameter description:
// parameter 1: event tracking name, can not be null
// parameter 2: JSON string of the parameter, cannot be null, and must be a valid JSON string
applog::onEvent("my_click", "{\"my_param\": 1}");
```


<span id="7bb91801"></span>
## 4.3 Public Attributes

If you want to include a property in each event, you can set it through a public property, without having to set it repeatedly in each event. Public properties only need to be set once to be included in all code event tracking events.


* Set public properties:


```C++
// Add public property
// parameter description:
// parameter 1: property name
// parameter 2: property value(only support string)
applog::addCustomHeader("header", "value");
```



* Remove public attributes:


```C++
// Remove public property
// parameter description:
// parameter 1: property name
applog::removeCustomHeader("header");
```


<span id="4bc077fb"></span>
# 5. Login status

If there is an account system in your product, please set the uuid immediately after the user logs in to ensure the consistency of the caliber before and after the user logs in.

```C++
// set user's uuid
applog::setUserUniqueId("your_user_unique_id");
```


<span id="124a925e"></span>
# 6. Other configurations

<span id="680c90c0"></span>
## 6.1 Print the log

If you need to look inside the SDK.
