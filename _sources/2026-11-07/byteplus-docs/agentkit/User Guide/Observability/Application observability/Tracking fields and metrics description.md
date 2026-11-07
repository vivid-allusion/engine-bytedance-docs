---
title: "Tracking fields and metrics description"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Tracking_fields_and_metrics_description"
---

AI application monitoring and VeADK each provide an instrumentation\-based monitoring solution for AgentKit. Through unified and standardized instrumentation and automated data collection, they deliver full\-lifecycle observability across the entire AgentKit lifecycle, providing data support for system stability, performance optimization, fault localization, and service iteration.

<span id="RJDKy6kx"></span>
## AI application monitoring

AI application monitoring provides an embedded instrumentation solution tailored for AgentKit. OpenTelemetry instrumentation is built into the AgentKit SDK to enable comprehensive observability of the call processes of the . The overall solution covers two core modules: **distributed tracing (Tracing)**  and **metric monitoring (Metrics)** . For details, refer to [AgentKit tracking fields and metrics description](https://docs.byteplus.com/en/docs/Observability_Platform/AgentKit_tracking_fields_and_metrics_description).

<span id="PKkEpAeb"></span>
## VeADK

VeADK provides an embedded instrumentation solution tailored for agents. OpenTelemetry instrumentation is built into the VeADK SDK, enabling full observability of the processes where VeADK calls agents, runs agents, calls models, and calls tools. The overall solution covers three core modules: general type, LLM type, and tool type.
