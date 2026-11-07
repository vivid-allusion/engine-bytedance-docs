---
title: "apmplus-server-agent release notes"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Apmplus-server-agent_release_notes"
---

The apmplus\-server\-agent primarily collects ‌host metrics‌ (processes, CPU, memory, network, and more) while also collaborating with the APMPlus SDK and APMPlus JavaAgent to collect and export observability data (application logs, traces, metrics, profiling data‌, and more). This topic provides the change log of the apmplus\-server\-agent add\-on.

<span id="IKGDg0F3"></span>
## February 2026


|**Version number** |**Kubernetes version compatibility** |**Version status** |**Description** |**Impact** |
|---|---|---|---|---|
|v1.0.33 |Cluster version ≥ v1.20\-0 |Maintained |The authentication method is optimized. |None |


<span id="MiQDQZMG"></span>
## February 2025


|**Version number** |**Kubernetes version compatibility** |**Version status** |**Description** |**Impact** |
|---|---|---|---|---|
|v1.0.32 |Cluster version ≥ v1.20\-0 |Maintained |server\-agent cap_sys_ptrace permission verification is supported, and related metrics can be recorded. |None |


<span id="ee74032e"></span>
## January 2025


|**Version number** |**Kubernetes version compatibility** |**Version status** |**Description** |**Impact** |
|---|---|---|---|---|
|v1.0.31 |Cluster version ≥ v1.20\-0 |EOM |The server\-agent runs as a privileged container. |None |


<span id="fe25ed46"></span>
## March 2023


|**Version number** |**Kubernetes version compatibility** |**Version status** |**Description** |**Impact** |
|---|---|---|---|---|
|v1.0.28 |Cluster version ≥ v1.20\-0 |EOM |Communication via the UDS stream protocol is supported. |None |


<span id="188ff6d3"></span>
## February 2023


|**Version number** |**Kubernetes version compatibility** |**Version status** |**Description** |**Impact** |
|---|---|---|---|---|
|1.0.27 |Cluster version ≥ v1.20\-0 |EOM |* adds a retry mechanism for appkey retrieval.<br><br>* Data degradation is supported.<br><br>* The third\-party open\-source notice is updated.<br><br>* Caching is applied to k8s APIServer access to avoid placing excessive load on ETCD in large\-scale cluster deployments. |None |


&nbsp;
