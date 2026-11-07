---
title: "Previous versions of the iOS SDK"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/tls_sdk_for_ios_overview"
---

The BytePlus TLS iOS SDK encapsulates API interfaces for log collection, topic management, and more. You can use the TLS iOS SDK in iOS applications to collect log data and manage log topics.

## Description

For the update log and version information of the BytePlus TLS iOS SDK, please refer to [GitHub](https://github.com/volcengine/ve-tls-ios-sdk/tags). It is recommended to choose the latest version of the SDK to experience enhanced product capabilities and more stable services.

v1.x and v2.x are two independent version lines and are not in\-place upgrades. Existing v1.x calls will not automatically gain Producer semantics by upgrading dependencies; they should be designed and validated as new integrations. For usage scenarios, semantic differences, rollback methods, and more for each version, please refer to [v1.x to v2.x version details](https://github.com/volcengine/ve-tls-ios-sdk/blob/v2.0.1/docs/migration/v1-to-v2.md).

|Version lines |Positioning |Public interfaces |
|---|---|---|
|v1.x |Legacy iOS log client, encapsulating API interfaces for log collection, topic management, and more. |Objective\-C |
|v2.x |Log upload Producer for iOS, iPadOS, and native macOS.<br><br><br>* If your business relies on log query, consumption, or management capabilities, please continue to retain the corresponding v1.x client.<br><br>* Producer v2.x **only handles log upload**. |* Swift<br><br>* Objective\-C |

## Sample projects

The TLS iOS SDK provides sample projects for your reference, including log delivery, log topic management, and other scenarios. For details, please refer to the GitHub sample project repository.

|GitHub source code |Notice |
|---|---|
|[ve-tls-ios-sdk-v1.x](https://github.com/volcengine/ve-tls-ios-sdk/tree/legacy/1.x) |Legacy iOS TLS client for Apple platforms, providing Objective\-C interfaces. |
|[ve-tls-ios-sdk-v2.x](https://github.com/volcengine/ve-tls-ios-sdk/tree/master) |Volcengine TLS asynchronous log upload Producer for Apple platforms.<br><br><br>* Provides Swift and Objective\-C interfaces, but is not compatible with the class names and methods of v1.x.<br><br>* Supports iOS, iPadOS, and native macOS, offering batch processing, compression, retry, backpressure, and optional WAL. |

## More features

Due to iOS environment limitations, except for the DescribeCursor and ConsumeLogs interfaces, the TLS iOS SDK supports most APIs described in [API list](https://docs.byteplus.com/en/docs/tls/Operations). You can refer to the sample code in [Sample projects](https://docs.byteplus.com/en/docs/tls/tls_sdk_for_ios_overview#.56S65L6L6aG555uu) to see more usage examples for these interfaces.
