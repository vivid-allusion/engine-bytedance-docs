---
title: "Overview"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/new-Overview"
---

This topic introduces `ve-tos-cli`, the official command\-line tool for TOS.

<span id="5d71c5c9"></span>
## Introduction

`ve-tos-cli` supports the entire TOS workflow, including file transfer, bucket configuration, advanced feature invocation, and control plane operations. It provides low\-level APIs, bucket configuration commands, advanced feature commands, and control plane commands to meet varying requirements. The following features are provided:


|Feature |Description |
|---|---|
|Specify storage type |You can use `--storage-class` to specify storage type. |
|Use control plane capabilities |You can use control plane capabilities via `--control-endpoint` and `--account-id`. |
|Automatically adapt to namespaces |The `auto` listing semantic automatically adapts to flat and hierarchical namespaces. |
|Command layering |There are three layers available.<br><br><br>* High\-level APIs: Designed for day\-to\-day operations and automation.<br><br>* Low\-level APIs: Designed for fine\-grained control. These APIs map one\-to\-one with TOS server\-side APIs.<br><br>* Utilities: Designed for configuration, diagnostics, and other auxiliary tasks. |


<span id="86049383"></span>
## Version information

Current version: v1.0.0.

<span id="a3b65d55"></span>
## Related documentation


|Documentation |Description |
|---|---|
|[Quick start with ve-tos-cli](https://docs.byteplus.com/docs/tos/Quick_start_with_ve-tos-cli) |Covers how to install and begin using `ve-tos-cli`. |
|[High-level APIs](https://docs.byteplus.com/docs/tos/High-level_APIs) |Explains how to use high\-level APIs for everyday tasks and automation, along with examples. |
|[Low-level APIs](https://docs.byteplus.com/docs/tos/Low-level_APIs) |Explains how to use low\-level APIs for fine\-grained control, along with examples. |
|[Utilities](https://docs.byteplus.com/docs/tos/Utilities) |Explains how to use utilities for configuration, diagnostics, and other auxiliary tasks, along with examples. |
|[AI agent guide](https://docs.byteplus.com/docs/tos/AI_agent_guide) |Covers design principles, recommended workflows, and other information for use cases involving AI automation. |
