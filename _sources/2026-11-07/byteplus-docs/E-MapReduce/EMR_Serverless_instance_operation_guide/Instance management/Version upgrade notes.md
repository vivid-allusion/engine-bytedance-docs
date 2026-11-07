---
title: "Version upgrade notes"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Version_upgrade_notes"
---

<span id="ee80b126"></span>
## List of supported upgrade versions


|Engine |Current version |Target version |Remarks |
|---|---|---|---|
|StarRocks |3.2.7 /3.2.3 |3.2.11 |Only lakehouse and data warehouse modes are supported for upgrade. |
||3.2.7/3.2.11/3.3.3 |3.3.10 |To request an upgrade, please contact Volcano Engine technical support by [submitting a ticket](https://console.byteplus.com/workorder/create?ref=L2xhcy9yZWdpb246bGFzK2FwLXNvdXRoZWFzdC0xL25leHQvaG9tZQ%3D%3D). |
|Doris |2.0.1/2.1.5 |2.1.7 |— |
||2.1.7 |2.1.8 |To request an upgrade, please contact Volcano Engine technical support by [submitting a ticket](https://console.byteplus.com/workorder/create?ref=L2xhcy9yZWdpb246bGFzK2FwLXNvdXRoZWFzdC0xL25leHQvaG9tZQ%3D%3D). |
||3.0.6 (multi\-warehouse edition) |3.0.8 (multi\-warehouse edition) |Downgrade is not supported after the upgrade. To request an upgrade, please contact Volcano Engine technical support by [submitting a ticket](https://console.byteplus.com/workorder/create?ref=L2xhcy9yZWdpb246bGFzK2FwLXNvdXRoZWFzdC0xL25leHQvaG9tZQ%3D%3D). |


<span id="bb5738fc"></span>
## Restriction note


* StarRocks and Doris instances support upgrades.

* When the cluster is running, FE and CN/BE/compute node must not be undergoing changes.

* Only one upgrade operation can exist at a time.

* The remaining space on the data disk must be greater than 25 GB.

* The size of the FE metadata directory must not exceed 15 GB.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">When rolling restart is selected, the management system will upgrade and restart nodes one by one. All ongoing import and query jobs on the restarted node will fail due to service interruption.</div>


* <div data-tips="true" data-tips-type="warning">After the version upgrade is completed and acceptance is confirmed, downgrade is not possible.</div>


* <div data-tips="true" data-tips-type="warning">When upgrading StarRocks/Doris across two\-digit versions, behavioral changes may occur and there is a risk of incompatibility. Please fully verify version compatibility before upgrading to avoid impacting your business.</div>


* <div data-tips="true" data-tips-type="warning">During the upgrade process, the instance cannot perform scaling up, expansion, reduction, or mounting to the public network.</div>
