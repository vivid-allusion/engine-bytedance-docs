---
title: "Overview"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/E2B-Overview"
---

VCI Agent Sandbox is compatible with the E2B protocol. This topic explains the core E2B concepts and usage methods to help you understand the E2B protocol and build foundational knowledge for managing VCI Agent Sandbox via this protocol.

<span id="zNErMql0"></span>
## Introduction to E2B

The E2B protocol (Agent Execution Protocol) is a standardized communication protocol built on Protobuf, HTTP/2, and Server\-Sent Events (SSE). It fully defines all interaction specifications between AI agents and remote execution environments (sandboxes).

Before the emergence of the E2B protocol, sandbox vendors used their own private APIs or Kubernetes CRDs. That practice causes the following problems:


* Developers need to re\-adapt and rewrite control\-plane code when switching sandbox services.

* AI agent applications are difficult to migrate across different cloud providers.


The E2B protocol unifies all interfaces and enables the "write once, run anywhere" capability, solving industry pain points such as fragmentation and inconsistency of sandbox APIs.

<span id="v56CsMbK"></span>
## E2B glossary

<span id="A4CRtB77"></span>
### Key terms


|**Term** |**Description** |
|---|---|
|Sandbox |The core CRD of the VCI Agent Sandbox. It provides instantly available, secure container sandboxes and supports advanced capabilities, such as pause, resume, state persistence, and in\-place upgrades. |
|Template |A template that defines parameters required for Sandbox startup, such as images, resources, and annotations. |
|Agent\-Sandbox\-Control\-Plane |The control\-plane component of the E2B API. It is a stateless service that serves as the execution entry point for the E2B protocol and processes control requests such as Sandbox creation and deletion. |
|Agent\-Sandbox\-Data\-Plane |The data plane component of the E2B API. It is a stateless service that performs operations (such as code or command execution) inside the Sandbox. |


<span id="LjDmGtbk"></span>
### Core E2B specifications


|**Module** |**Core feature** |
|---|---|
|Lifecycle management |Create, destroy, pause, and resume sandboxes. |
|Code execution |Run code synchronously or asynchronously and return streams of output results. |
|Filesystem operations |Upload, download, and delete files, and monitor file changes. |
|Terminal interaction |Implement pseudo\-terminal (PTY) emulation and support real\-time interaction. |
|Command execution |Run commands in sandboxes. |
|Observability |Retrieve sandbox logs, resource usage, and events. |


<span id="fbhDv90M"></span>
## Related documentation

The documentation for managing VCI Agent Sandbox via the E2B protocol is divided into two parts:


* [Getting started](https://docs.byteplus.com/en/docs/vke/Getting_started): Guides you to quickly create your first Agent Sandbox from scratch using E2B.

* [SDK reference](https://docs.byteplus.com/en/docs/vke/SDK_reference): Introduces the construction methods of each SDK request, request parameters, and configuration options.
