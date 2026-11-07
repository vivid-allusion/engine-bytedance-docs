---
title: "Windows License Guide"
product: "BytePlus Effects"
product_code: "effects"
source: "https://docs.byteplus.com/en/docs/effects/docs-windows-license-guide"
---

<span id="LicenseRequest Usage Guide"></span>
# LicenseRequest Usage Guide

```Plain
Install LicenseRequest, and ensure that the Windows clock is synchronized with the Internet time.
Enter the key and secret that you have applied for by contacting the business personnel.
Select a path to save the license file, download the file, and save it as license.bag.
```


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/doc-center/1bdb74e-1.png) </span>

<span id="Updating the Windows Demo License"></span>
# Updating the Windows Demo License

```Plain
Put the license.bag file under resource/license/ in the Windows demo directory, without changing the file name.
```


Start the Windows demo.

For more information about online licensing, see the [Online License Guide](https://byteplus-docs.readme.io/effects/docs/online-license-guide).

<span id="Appendix: Windows LicenseRequest Access Guide"></span>
## Appendix: Windows LicenseRequest Access Guide

This appendix describes the integration logic of online licensing in Windows, including how to obtain device information, configure request information, call request APIs, etc. Please contact technical support for online request examples and refer to the following content.

<span id="cvtob-license-requester Project"></span>
# cvtob\-license\-requester Project

```Plain
Enter the root directory of the cvtob-license-requester project, create a folder named "build", and execute "cmake ../ -DCMAKE_BUILD_TYPE=Release". The corresponding license-requester.sln project will then be generated. Open this project and compile it to generate license-requester.dll. The header file is as follows. Use the API shown in the following figure to configure the HTTP request information. For the specific call process, refer to the LicenseRequestWin project.
```


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/doc-center/96f1d8a-2.png) </span>

<span id="LicenseRequestWin Project"></span>
# LicenseRequestWin Project

```Plain
Enter the root directory of the LicenseRequestWin project.
```


<span id="#"></span>
### [#](https://www.volcengine.cn/docs/5888/62120#)

```Plain
Copy the header file license-requester.h and the generated dynamic library license-requester.dll from the cvtob-license-requester project to the following folders, respectively.
```


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/doc-center/c5e9e8a-3.png) </span>

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/doc-center/754845f-4.png) </span>

<span id="#"></span>
### [#](https://www.volcengine.cn/docs/5888/62120#-2)

```Plain
Go back to the root directory of the LicenseRequestWin project, open PowerShell, and execute "./build.bat Release" to generate LicenseRequestWin.exe.
```


<span id="#"></span>
### [#](https://www.volcengine.cn/docs/5888/62120#-3)

```Plain
In the LicenseRequest UI, use Qt to call the void get_request_content(const char* key, const char* secret, const char* authMsg,char** content,int* size) API to encapsulate the request information, and use QHTTP to complete the online request. The call method is as follows.
```


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/doc-center/82d2ae1-5.png) </span>

<span id="#"></span>
### [#](https://www.volcengine.cn/docs/5888/62120#-4)

```Plain
If you do not use Qt, you may refer to the int request_license(const char* key, const char* secret, const char* authMsg, char** license, int* size) API in license-requester.h and use cURL to complete the online request, as shown in the following figure.

```


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/doc-center/22aa67d-6.png) </span>

```Plain
You may also complete the online request logic by other means.
```
