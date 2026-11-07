---
title: "[Product update] fsx-service deprecation notice"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Product_announcement_FSX_add-on_feature_optimization_and_fsx-service_add-on_sunsetting"
---

<span id="PRdB68qd"></span>
## Background information

In the existing FSX client management solution, FSX capabilities in clusters rely on multiple add\-ons (csi\-fsx and fsx\-service). This solution presents issues such as an excessive number of add\-ons, overlapping functional boundaries, and unclear division of responsibilities. Users need to manage the installation, upgrades, and version compatibility of multiple add\-ons, resulting in high O&M and governance costs. As certain capabilities are gradually migrated, the legacy architecture also introduces issues such as code redundancy, complex management workflows, and difficulty in unifying subsequent changes. This further complicates stability governance and long\-term maintenance.

<span id="Ds1J2bdR"></span>
## Description

To address the above issues, VKE provides redesigned FSX\-related add\-ons in csi\-fsx  v1.0.0. The new solution reduces user\-facing add\-ons, simplifies version dependencies, and clarifies component responsibilities. This not only lowers operational complexity but also provides a more stable architectural foundation for unified management, on\-demand provisioning, hot upgrades, and independent release capabilities of FSXSet. The main changes are as follows:


* The csi\-fsx add\-on now integrates core capabilities (such as mount/unmount and permission refresh) previously provided by fsx\-service.

* The managed fsxset\-controller add\-on is introduced to manage control\-plane capabilities (such as FSX client lifecycle management).


The following table compares FSX client management solutions for different csi\-fsx versions.


|Item |Solution before v1.0.0 |Solution for v1.0.0 and later |
|---|---|---|
|Involved add\-ons |csi\-fsx and fsx\-service |csi\-fsx and fsxset\-controller (managed add\-on). |
|Add\-on responsibilities |The fsx\-service add\-on manages the lifecycle of FSX clients. |FSXSet centrally manages the lifecycle of FSX clients.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">For details about FSXSet resources, see <a href="https://docs.byteplus.com/en/docs/vke/Introduction_to_FSXSet_resources">Introduction to FSXSet resources</a>.</div><br> |
|Feature differences |* ‌Configuration adjustments are supported only at the cluster level and cannot adapt to different node specifications.<br><br>* The FSX client version is bound to the fsx\-service add\-on version. To upgrade the FSX client version, the fsx\-service add\-on version must be upgraded. |* FSX clients are centrally managed by FSXSet. The solution supports features such as rolling upgrades, canary upgrades, and multi\-environment isolation.<br><br>* FSX client versions are managed independently. The solution supports independent release without binding to other add\-ons. |


<span id="pwgVMtxM"></span>
## Impact

When you upgrade the csi\-fsx add\-on in your cluster to v1.0.0 or later, the fsx\-service add\-on will cease to function, and all its capabilities will be taken over by the csi\-fsx add\-on. Existing configurations and FSX clients will be automatically migrated and managed without disrupting normal operations. The new solution simplifies FSX client configuration and supports features such as rolling upgrades, canary releases, and multi\-environment isolation. For details, see [Migrating FSX clients](https://docs.byteplus.com/en/docs/vke/Migrating_FSX_clients).

We recommend that you plan the migration process based on your business scenario. If you encounter any issues during migration or need technical support, feel free to [submit a ticket](https://console.byteplus.com/workorder/create?step=1).

<span id="7NGBs6oO"></span>
## Related documentation


* [Introduction to FSXSet resources](https://docs.byteplus.com/en/docs/vke/Introduction_to_FSXSet_resources)

* [Migrating FSX clients](https://docs.byteplus.com/en/docs/vke/Migrating_FSX_clients)

* [Release notes for csi-fsx](https://docs.byteplus.com/en/docs/vke/csi-fsx)

* [csi-fsx instructions](https://docs.byteplus.com/en/docs/vke/csi-fsx-add-on)
