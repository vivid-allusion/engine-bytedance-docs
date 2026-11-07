---
title: "Version management"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/version_management_minipro"
---

The SDK automatically obtains the current version and environment of the mini program through the APIs of each mini program platform. Therefore, after integrating the SDK and completing version setup, you can turn on version management capabilities.

<span id=".54mI5pys5YiX6KGo"></span>
## version list

The version list allows you to monitor page views, JavaScript errors, mini program type, and other relevant information for all released versions. The version list supports filtering by release time, environment, version search, and mini program type, allowing you to find the corresponding version information more quickly and accurately.

<span id=".54mI5pys6K-m5oOF"></span>
## Version details

In the version list, click **details** to enter version details.

The top section of the details page displays basic information about the current version, including release time, the number of new JavaScript errors in the current version, count, user count, and other related information.

The overview area displays information about JavaScript errors. Click a specific error to go to the JavaScript error details for further action.

In the SourceMap area, users can manage the SourceMap associated with the current version.

The trend chart shows the recent trends in changes for some metrics of this version.

<span id=".5o6l5YWl5a6e6Le1"></span>
## Integration practices

Almost all mini programs on domestic platforms have an online environment and version. Therefore, when integrating the SDK, the environment and version of the current mini program are automatically obtained. For example, the environment for the WeChat Mini Program:


|**Environment** |**Version** |
|---|---|
|develop |Developer edition |
|trial |Trial version |
|release |Official version |
