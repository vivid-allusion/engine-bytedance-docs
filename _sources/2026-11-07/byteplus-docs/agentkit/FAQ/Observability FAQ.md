---
title: "Observability FAQ"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Observability_FAQ"
---

## Can trace data from the observability module be exported locally?

Yes, you can. After you select trace data in the trace interface, you can export and download it locally.

## Do I have a free usage quota after enabling observability capabilities?

Currently, no free quota is available. During the public preview, you can apply for APMPlus vouchers.

## Do I need to enable observability capabilities to evaluate agents in AgentKit?

Yes. Trace information is required for evaluations and is collected only after observability capabilities are enabled.

## Request latency is too high and the system reports a timeout error. How can I query the related trace data?

Go to the Trace analysis tab, set the filter condition of the parameter status code to "Include 1", and you can quickly query exception stack traces for issues such as timeouts and connection failures.

## Trace data exists, but data backflow does not take effect.

This issue usually occurs because the data filter rules in the data backflow task are not configured correctly. As a result, trace data cannot be filtered, which ultimately affects the data backflow result. Refer to the following configuration requirements to troubleshoot the issue:

* Multiple data filter rules take effect based on AND logic. For example, if you set the filter condition of the parameter service name to "Include service A" and the filter condition of the parameter SDK language to "Include Go", only data that meets both conditions is filtered.

* A parameter in the same data filter rule can be configured with multiple values, which take effect based on OR logic. For example, if you set the filter condition of the parameter service name to "Include service A and service B", data that meets any condition is filtered.

* Filter parameter names and values in the same data filter rule must match those used in the actual environment. For example, a service name follows the naming rule `{runtime_id}.{runtime_name}`. When you filter data by service name, enter the full service name as the parameter value, rather than only `{runtime_id}` or `{runtime_name}`.
