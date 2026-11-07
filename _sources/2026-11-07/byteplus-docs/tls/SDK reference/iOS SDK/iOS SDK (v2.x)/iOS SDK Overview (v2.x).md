---
title: "iOS SDK Overview (v2.x)"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/iOS-SDK-Overview-v2-x"
---

BytePlus TLS iOS SDK v2.x wraps the logging collection interface of TLS, providing an asynchronous log upload producer for Apple platforms (`VolcengineTLSProducer`) with high\-throughput async log writing capability for iOS and native macOS applications.

## Description

For the release notes and version information of the BytePlus TLS iOS SDK, see [GitHub](https://github.com/volcengine/ve-tls-ios-sdk/tags). We recommend using the latest SDK version for enhanced product features and more stable service.

iOS SDK v2.x **only handles log upload** and does not offer interfaces for query, consumption, alert, or data transformation. It supports Swift and Objective\-C.

## Sample projects

TLS iOS SDK provides sample projects for your reference. For details, see the Github sample repository.

|GitHub source code |Notice |
|---|---|
|[ve-tls-ios-sdk-v2.x](https://github.com/volcengine/ve-tls-ios-sdk/tree/master) |Async log upload Producer for Volcengine TLS on Apple platforms<br><br><br>* Provides Swift and Objective\-C interfaces but is not compatible with v1.x class names and methods<br><br>* Supports iOS, iPadOS, and native macOS, offering batch processing, compression, retry, backpressure, and optional WAL |

## Reference

|Reference |Notice |
|---|---|
|[Overview](https://github.com/volcengine/ve-tls-ios-sdk/blob/v2.0.1/docs/README.md) |`VolcengineTLSProducer` offers high\-throughput asynchronous log writing for iOS and native macOS applications It completes local reception on the calling thread and then aggregates, compresses, and sends logs in the background |
|[Installation](https://github.com/volcengine/ve-tls-ios-sdk/blob/v2.0.1/docs/getting-started/installation.md) |Environment requirements, installation steps, and version selection for the VolcengineTLSProducer SDK. |
|[Objective-C integration](https://github.com/volcengine/ve-tls-ios-sdk/blob/v2.0.1/docs/getting-started/objective-c.md) |Upload logs using Producer v2 without adding Swift source files to the business target The SDK still includes Swift internally for sharing implementation with Swift `Producer`, but it is not a compatibility layer for the old v1.x client |
|[Verify write](https://github.com/volcengine/ve-tls-ios-sdk/blob/v2.0.1/docs/getting-started/verify-ingestion.md) |Successfully returning from `add` alone does not confirm completion. Verification should cover local reception, batch callback, and server\-side query. |
|[Configuration parameters](https://github.com/volcengine/ve-tls-ios-sdk/blob/v2.0.1/docs/reference/configuration.md) |`ProducerConfiguration` is a mutable value type. Parameters are validated during initialization, and `Producer.open` validates and saves the configuration again at that time. After opening successfully, modifying the original configuration does not affect the running Producer. |
|[Platform compatibility](https://github.com/volcengine/ve-tls-ios-sdk/blob/v2.0.1/docs/reference/compatibility.md) |Compatibility of product platforms, toolchains, and access methods |
|[Persistence and recovery](https://github.com/volcengine/ve-tls-ios-sdk/blob/v2.0.1/docs/guides/persistence-and-recovery.md) |Data persistence helps restore unconfirmed data after an exception exit, device restart, or extended offline periods. Provides at\-least\-once delivery assurance, but does not support exactly\-once. |
|[Troubleshooting](https://github.com/volcengine/ve-tls-ios-sdk/blob/v2.0.1/docs/operations/troubleshooting.md) |When troubleshooting, first determine where the failure occurs: `open`, local `add`, asynchronous batch callback, server\-side query, or `close`. The meaning of success varies at each stage. |
|[Performance reference](https://github.com/volcengine/ve-tls-ios-sdk/blob/v2.0.1/docs/operations/performance.md) |Performance results are closely related to device, system, log size, persistence method, and network conditions. Related data is used to estimate resource consumption. Results are for selection and configuration reference and do not represent throughput limits or service guarantees. |
