---
title: "Overview"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/ds_overview"
---

<span id="_1-dolphinscheduler-简介"></span>
## 1 Introduction to DolphinScheduler

Apache DolphinScheduler is a distributed, easily extensible, visual DAG workflow task scheduling system designed for enterprise\-level scenarios. It provides visual task operations, workflow orchestration, and a solution for the entire lifecycle of data processing.

<span id="_2-部署拓扑"></span>
## 2 Deployment topology

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">indicates unlimited deployment quantity;</div>


* <div data-tips="true" data-tips-type="tip">indicates no deployment.</div>


* <div data-tips="true" data-tips-type="tip">Specific numbers indicate the maximum deployment quantity;</div>




| |**Master Server** |**Worker Server** |**API Server** |**Alert Server** |
|---|---|---|---|---|
|**Master** |*  |*  |1 |1 |
|**Core** |*  |8 |*  |*  |
|**Task** |*  |*  |*  |*  |


<span id="_3-文档指引"></span>
## 3 Documentation guide


* To quickly experience DolphinScheduler features, refer to [quickstart](https://docs.byteplus.com/docs/E-MapReduce/109217).

* To learn about DolphinScheduler configuration and parameter tuning, refer to [Configuration guide](https://docs.byteplus.com/docs/E-MapReduce/109218).

* To further explore DolphinScheduler integration with other compute engines and study cases that are closer to real\-world production, refer to [Integration example](https://docs.byteplus.com/docs/E-MapReduce/109220).
