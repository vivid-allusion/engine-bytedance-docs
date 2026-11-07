---
title: "Configure APIs globally"
product: "BytePlus Video Editor"
product_code: "video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/video-editor-sdk/120-configure-apis-globally"
---

You can call a set of APIs or methods within a software development kit (SDK) or framework that are used to manage global configurations or settings for an application or system. These interfaces would allow you to programmatically access and modify various global settings such as application preferences, environment variables, or system\-wide configurations.

The provided code snippet demonstrates how to clear resources within a designated folder in the `EOSDK` (Endless OS Software Development Kit). By invoking the `clearResource` method, all contents within the folder configured using the `setResourceBaseDir` method will be deleted. This action ensures the removal of unwanted or outdated resources, maintaining a clean and organized environment within the application.

<span id="20761674"></span>
# Code sample

```JSON
//  Clear resource. This line will delete all contents within a particular folder which has been configured by you using the specific line of code:{EOSDK#setResourceBaseDir}.
[EOSDK clearResource]; 
```
