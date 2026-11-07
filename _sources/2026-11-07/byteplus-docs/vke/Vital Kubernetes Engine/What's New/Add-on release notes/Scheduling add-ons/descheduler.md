---
title: "descheduler"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/descheduler"
---

The descheduler add\-on is compatible with the Descheduler in the community and is used for rescheduling pods in hot nodes according to the real load of nodes in the cluster. This topic describes the release notes for the descheduler add\-on.

For more information, refer to [Add-on management](https://docs.byteplus.com/en/docs/vke/Add-on-management).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">【<a href="https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features"><strong>Beta \- Apply for Trial</strong></a>】 This add\-on is currently in beta. To use this add\-on, submit an application.</div>


<span id="september-2023"></span>
## September 2023


|Version Number |Kubernetes Version Compatibility |Version Status |Description |Impact |
|---|---|---|---|---|
|v0.27.1\-vke.3 |Cluster version ≥ v1.24 |Being maintained |Optimized the code specification for the add\-on and upgraded the add\-on version. |None. |
|v0.27.1\-vke.2 |Cluster version ≥ v1.24 |EOM |* Fixed the issue that the `nodeselector` parameter is invalid in the filtering phase.<br><br>* Allows you to set `dryRun` to trigger a dry run. |None. |


<span id="august-2023"></span>
## August 2023


|Version Number |Kubernetes Version Compatibility |Version Status |Description |Impact |
|---|---|---|---|---|
|v0.27.1\-vke.1 |Cluster version ≥ v1.24 |EOM |Released the descheduler add\-on in beta for the first time. |None. |
