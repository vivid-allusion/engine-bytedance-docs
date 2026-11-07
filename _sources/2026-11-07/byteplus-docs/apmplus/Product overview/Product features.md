---
title: "Product features"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Product_features"
---

APMPlus provides two main modules: Server\-side Monitoring and RUM. This topic provides a detailed introduction to the features supported by APMPlus.

<span id="yZAPpBHg"></span>
## Server\-side Monitoring

Server\-side Monitoring delivers benefits such as low integration costs and non\-intrusive deployment. It supports performance monitoring for basic resources, service and code layer monitoring, and end\-to\-end monitoring for online application health. Through self\-developed Agent, OpenTelemetry, and other methods, Java, Go, Python, and other applications (such as LLMs and agents) can be integrated for end\-to\-end monitoring. This provides more exception scene restoration capabilities. Core features include service monitoring, trace analysis, error analysis, log monitoring, custom monitoring, and alert tasks. Typical AI‑related features are as follows:


* Agent monitoring: Supports automatic instrumentation for agent frameworks such as Eino and LangChain and associated MCP services, without the need to manually integrate SDKs.

* Inference engine monitoring: Supports transparent instrumentation for mainstream inference frameworks, parses agent traces, and quickly identifies end\-to\-end issues from agents to inference engines.

* AI scenario monitoring: Supports aggregated views centered on LLMs for observability, supports LLM\-based session monitoring and upstream/downstream monitoring of MCP services, and provides monitoring capabilities for AI business scenarios.


<span id="1ZEBs2g0"></span>
## RUM

After being integrated with the client via the SDK, APMPlus provides comprehensive monitoring and analysis capabilities. Supported client monitoring capabilities include App Monitoring, WebPro Monitoring, Mini Monitoring, Mini Pro Monitoring Monitoring.

<span id="mHuhHQOk"></span>
### App Monitoring

App Monitoring supports tracking and analyzing exception scenarios via exclusive technical methods. It comprehensively monitors and analyzes applications on iOS, Android, and Harmony operating systems. This covers various crash types, comprehensive performance analysis, custom event tracking, memory optimization, event analysis, battery analysis, and error analysis.

In addition, it features the most comprehensive exception capture capabilities and industry\-leading proactive protection mechanisms, truly enabling reconstruction of Native (C/C++) crash scenes. Its intelligent aggregation algorithm efficiently groups similar exceptions. It also supports both Native and hybrid monitoring and reporting of custom exceptions and custom instrumentation metrics. It provides across iOS and Android not only collection of multiple crash types with on\-site data restoration and analysis, but also comprehensive performance analysis covering memory optimization, startup analysis, page monitoring, and network analysis. This enables precise root\-cause tracing and helps developers resolve issues efficiently.

<span id="vrAXtdJW"></span>
### WebPro Monitoring

WebPro Monitoring generally refers to web monitoring. It supports monitoring for browser pages, in\-app H5 pages, and Electron applications. It offers flexible data collection and consumption methods. Additional capabilities include support for multi\-page applications, single\-page applications, micro frontend applications, and inter\-app communications, as well as diverse lifecycle monitoring and more flexible customization. Key capabilities include blank screen monitoring, custom monitoring, and version management. Additionally, it supports blank screen root cause analysis, performance analysis, detailed user action replay, and real\-time alerts for new errors in specified versions.

<span id="A2TiDqHI"></span>
### Mini Pro Monitoring

The Mini Pro Monitoring provides the capability to analyze the launch performance, request analysis, page performance, JS error analysis, and page loading performance of mini programs on platforms such as Douyin, WeChat, Alipay, Baidu, and Feishu. It supports the integration of native mini programs and third\-party frameworks including UniApp and Taro. Key features include setData frequency monitoring, custom monitoring, and performance monitoring. In addition, it leverages an overall performance score to flexibly quantify and analyze the overall performance of mini programs, helping you quickly track and diagnose issues.

<span id="UE7y7uBN"></span>
### Mini Monitoring

Mini Monitoring provides free JS error analysis and page load performance analysis for TikTok Mini Program, WeChat Mini Program, and Alipay Mini Program.
