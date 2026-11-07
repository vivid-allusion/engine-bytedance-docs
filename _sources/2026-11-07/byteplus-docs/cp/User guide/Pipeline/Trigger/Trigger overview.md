---
title: "Trigger overview"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Trigger_overview"
---

The pipeline supports the following trigger rules, which can be used simultaneously.

<span id=".5Luj56CB5rqQ6Kem5Y-R"></span>
## Trigger the code source

By using a Webhook plugin to listen for events in the code repository, any qualifying code change will automatically trigger the pipeline to run.

<span id=".5a6a5pe26Kem5Y-R"></span>
## Scheduled trigger

Supports configuration of minute\-level scheduled trigger rules to periodically trigger pipeline execution.

<span id=".6YCa55SoLXdlYmhvb2st6Kem5Y-R"></span>
## General Webhook triggers

Used to trigger pipeline runs from third\-party tools or proprietary systems outside of the code source.

<span id=".6ZWc5YOP5rqQLXdlYmhvb2st6Kem5Y-R"></span>
## The mirror source webhook trigger

Monitor actions in the BytePlus image repository via a Webhook plugin; when a qualifying event occurs, the pipeline is automatically triggered.

<span id=".5omL5Yqo6Kem5Y-R"></span>
## Manual trigger

Manual pipeline execution is supported. For detailed steps, please refer to [Run pipeline](https://docs.byteplus.com/en/docs/cp/Run_a_pipeline).
