---
title: "Application scenarios"
product: "Observability Platform"
product_code: "Observability_Platform"
source: "https://docs.byteplus.com/en/docs/Observability_Platform/Application_scenarios"
---

Observability Platform is used to unify cloud\-native observability services and build a complete observability ecosystem. This topic introduces the typical application scenarios of Observability Platform.

<span id="IaPyjfDS"></span>
## Cloud\-native dynamic resource optimization

Container environments often suffer from inaccurate auto\-scaling planning, low resource utilization, and resource shortages, which can cause performance issues. This solution addresses these pain points, reducing cloud resource costs by about 30% and ensuring application elasticity during peak hours. Core optimization items are as follows:


* Collect Cloud Monitor or VMP infrastructure metrics in real time, such as CPU, memory, and network IO metrics.

* Achieve precise scaling through the analysis of application performance data.

* Identify low\-utilization resources, such as zombie containers, to reduce costs.


<span id="kKhCCq2d"></span>
## End\-to\-end user experience guarantee

An end\-to\-end approach is adopted to quickly determine if a fault originates from the front\-end or back\-end. It resolves the pain points causing poor front\-end user experience. These pain points include failing to correlate front\-end issues with back\-end performance quickly and troubleshoot root causes. This in turn enhances overall user experience and satisfaction. Core optimization items are as follows:


* Real user monitoring (RUM) and session playback track and record user operations.

* Correlate and track front\-end user interactions with back\-end traces and database queries across the entire process.

* Monitor key web performance metrics, such as loading time and interaction response time.


<span id="5bTwwL8I"></span>
## Global cost insight and resource efficiency optimization

Issues related to cloud resource costs are addressed. For example, infrastructure consumption cannot be correlated with specific businesses, features, or code, and the basis for resource efficiency optimization is lacking. Provide data support for architecture optimization and resource scale\-in, which directly reduces cloud resource costs, makes costs visible, traceable, and optimizable, and accurately pinpoints waste. Core optimization items are as follows:


* Comprehensively collect Cloud Monitor or VMP resource metrics, such as CPU, memory, and disk IO metrics.

* Tag resource costs and assign them to corresponding entities using the application, service, and interface tags provided by APM.

* Display cost\-effectiveness views by using custom dashboards, such as cost per QPS and high\-consumption interface rankings.


<span id="GuxmOFFR"></span>
## Root cause identification and fault healing

Root cause identification and fault recovery are optimized for specific pain points. These pain points include severe alert storms, reliance on expert experience for manual troubleshooting, long mean time to repair (MTTR), and failure to recover automatically when exceptions occur. MTTR is reduced from hours to minutes, or even to seconds, turning reactive firefighting into proactive, predictive O&M and boosting system resilience. Core optimization items are as follows:


* Unified alerting enables alert aggregation and intelligent noise reduction, and automatically triggers the root cause identification process.

* The platform automatically associates observability topologies, log errors, and Prometheus metrics to quickly identify faults.

* Open APIs integrate with automation scripts to perform self\-healing operations, such as service restarts and traffic switching, and deliver synthetic monitoring verification.


<span id="LKQIF9uC"></span>
## End\-to\-end observability for agentic AI operations and inference optimization

Longstanding pain points in AI agents and complex LLM applications are addressed. These pain points include the black\-box inference processes, high costs, slow responses, and unstable result quality. Prompt policies and agent workflows are iterated based on data. This boosts the ROI and user experience of AI applications, achieves transparency and optimizability of the AI inference process, and accurately pinpoints cost and performance bottlenecks. Core optimization items are as follows:


* End\-to\-end data collection and correlation: Correlate RUM or logs to record user feedback behaviors on AI outputs, such as likes and adoption. Use APM or unified collection to track the complete chain of thought for each agent call, including performance (duration) and resource consumption (number of tokens) for steps such as tool calls, code execution, and API queries.

* Quality and cost correlation: Add metrics, such as inference latency, token cost, and user feedback scores, to custom dashboards.

* Root cause drill\-down: When cost spikes or quality degradation is detected, you can drill down into complete logs and traces of a specific inference to identify inefficient steps. Examples of the steps include redundant tool calls and inefficient prompts.


<span id="fsKnCEcY"></span>
## Microservices governance and fault identification

Microservice architecture pain points are addressed. Such pain points include: high complexity in microservice architectures makes a single service failure prone to triggering cascading failures, and traditional fault identification is inefficient, like finding a needle in a haystack. This reduces the period of time to identify faults from hours to minutes and enhances system availability and stability. Core optimization items are as follows:


* Distributed tracing visualizes the complete path of requests.

* Service topology maps are automatically discovered to display dependencies between services.

* Associate and analyze metrics, logs, and trace data, which achieves root cause identification through one\-click drill\-down.


<span id="5FmjeDx7"></span>
## Centralized multi\-cloud governance and SLA guarantee

This solution addresses critical issues in scenarios where businesses are distributed across multiple environments, such as Alibaba Cloud, AWS, and private clouds. It resolves issues such as fragmented monitoring data and the lack of a unified view, which result in difficulty guaranteeing Service Level Agreements (SLAs) for cross\-cloud business traces. This solution achieves centralized management across multi\-cloud environments, breaks down monitoring barriers caused by cloud vendor lock\-in, quantifies and ensures global continuity for businesses that are deployed across multiple clouds, and provides a basis for architectural decisions. Core optimization items are as follows:


* Standardized collection: Metrics, logs, and trace data are collected based on unified standards and aggregated on a central platform through O11yAgent deployed in each cloud environment.

* Global business topology: A cross\-cloud service global dependency topology map is automatically generated based on observability data, which visualizes business flows.

* Centralized SLA assessment: Monitor the availability and performance of cross\-cloud services from the perspective of public network users by using CloudDetect. Calculate a global business SLA in custom dashboards based on multi\-source data, and consolidate alerts to filter out infrastructure\-level noise and focus on business impact.
