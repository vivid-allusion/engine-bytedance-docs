---
title: "Version release records"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Version_release_records"
---

This article introduces the release records of server\-side monitoring APMPlusAgent, Operator, JavaAgent, and Go SDK.

<span id="48068373"></span>
## APMPlusAgent

<span id="0a1b28b9"></span>
### 1.0.28(2023\-03\-10)

[download links](http://apmplus-dl-cn-beijing.volces.com/server_warehouse/assets/download/apminsight-agent_1.0.28-1_amd64.tar.gz)


* Support uds stream protocol communication


<span id="7f727cd0"></span>
### 1.0.27(2023\-02\-24)

[download links](http://apmplus-dl-cn-beijing.volces.com/server_warehouse/assets/download/apminsight-agent_1.0.27-1_amd64.tar.gz)


*  Start obtaining appkey and increase retry attempts

* Support data downgrade

* Update the third\-party open source notice

* Use caching when accessing the K8s APIServer to prevent excessive load on ETCD during large cluster deployments.


<span id="ce7535d8"></span>
## APMPlusOperator

<span id="660c0633"></span>
### 1.0.1(2023\-03\-10)


|Image name |Container Registry |
|---|---|
|DockerImage |apmplus\-cn\-beijing.cr.volces.com/server/apmplus\-operator:1.0.1 |



* Initial release, supports Kubernetes auto instrument and mount volume.


<span id="28b2542d"></span>
## JavaAgent

<span id="ba4d00f3"></span>
### 1.1.4(2023\-02\-01)

[download links](https://apmplus-dl-cn-beijing.volces.com/server_warehouse/assets/java-agent/apminsight-java-agent_1.1.14.tar.gz)


|Image name |Container Registry |
|---|---|
|DockerImage |apmplus\-cn\-beijing.cr.volces.com/server/java\-agent:1.1.14 |



* feat: Supports agentless mode, allowing users to directly bypass the Agent to report data. Some RED Metrics will be lost when sampling trace data.


<span id="f9a21710"></span>
## Go SDK

<span id="aee62da4"></span>
### v1.3.18(2023\-02\-01)

[GitHub address](https://github.com/volcengine/apminsight-server-sdk-go/releases/tag/v1.3.18)


* feat: Support custom resource instrumentation in the Gin framework.
