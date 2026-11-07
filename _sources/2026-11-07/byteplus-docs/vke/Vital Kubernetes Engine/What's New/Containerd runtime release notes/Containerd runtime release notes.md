---
title: "Containerd runtime release notes"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Containerd_runtime_release_notes"
---

This topic records the ‌version changes‌ of the containerd runtime used in VKE, including version compatibility, release time, status, and change details.

<span id="BzLS3Et8"></span>
## September 2026


|Version |Kubernetes version compatibility |Description |Impact |
|---|---|---|---|
|v2.3.4\-vke.1 |Node version ≥ v1.36 |* The containerd version has been updated from v2.1.9 to v2.3.4. For more details, see [Change details](https://github.com/containerd/containerd/compare/v2.1.9...v2.3.4).<br><br>* The runc version has been updated from v1.3.4 to v1.4.3. For more details, see [Change details](https://github.com/opencontainers/runc/compare/v1.3.4...v1.4.3).<br><br>* The crictl version has been updated from v1.34.0 to v1.36.0.<br><br>* The nerdctl version has been updated from v2.1.6 to v2.3.5. |Pay attention to deprecated features and APIs when you use containerd v2.3.4. For details, see [containerd 2.3.x](https://docs.byteplus.com/en/docs/VolcengineKubernetesEngine/Containerd23xIntroduction?lang=en). |


<span id="YR6L2D0l"></span>
## July 2026


|Version |Kubernetes version compatibility |Description |Impact |
|---|---|---|---|
|v2.1.9\-vke.1 |Node version ≥ v1.34 |The containerd version has been updated from v2.1.6 to v2.1.9. For more details, see [Change details](https://github.com/containerd/containerd/compare/v2.1.6...v2.1.9). |None |
|v1.6.38\-vke.18 |Node version ≤ v1.34 |The installation script has been updated. |None |


<span id="xQHg9deU"></span>
## January 2026


|Version |Kubernetes version compatibility |Description |Impact |
|---|---|---|---|
|v2.1.6\-vke.1 |Node version ≥ v1.34 |* The containerd has been updated from v1.6.38 to v2.1.6. For more details, see [Change details](https://github.com/containerd/containerd/compare/v1.6.28...v1.6.38).<br><br>* The runc has been updated from v1.1.15 to v1.3.4. For more details, see [Change details](https://github.com/opencontainers/runc/compare/v1.1.15...v1.3.4).<br><br>* The crictl has been updated from v1.32.0 to v1.34.0.<br><br>* The nerdctl has been updated from v1.7.4 to v2.1.6. |Pay attention to deprecated features and APIs when you use containerd v2.1.6. For details, see [containerd 2.1.x](https://docs.byteplus.com/en/docs/vke/Containerd_2-1). |


<span id="SZ2EKt2w"></span>
## September 2025


|Version |Kubernetes version compatibility |Description |Impact |
|---|---|---|---|
|v1.6.38\-vke.17 |Node version ≤ v1.34 |The installation script has been updated to support new GPU specifications. |None |


<span id="PjuMYPL4"></span>
## May 2025


|Version |Kubernetes version compatibility |Description |Impact |
|---|---|---|---|
|v1.6.38\-vke.16 |Node version ≤ v1.34 |* The containerd version has been updated from v1.6.28 to v1.6.38. For more details, see [Change details](https://github.com/containerd/containerd/compare/v1.6.28...v1.6.38).<br><br>* The runc has been updated from v1.1.12 to v1.1.15. A ‌probable cgroup leak‌ issue on kernel versions ‌earlier than 5.8‌ has been fixed. For more details, see [Change details](https://github.com/opencontainers/runc/compare/v1.1.12...v1.1.15).<br><br>* The crictl has been updated from v1.28.0 to v1.32.0. |None |


<span id="bIJbEiMK"></span>
## February 2025


|Version |Kubernetes version compatibility |Description |Impact |
|---|---|---|---|
|v1.6.28\-vke.15 |Node version ≤ v1.34 |The installation script has been updated to ‌enable cgroup v2 support‌ for operating systems Ubuntu 22 and veLinux 2.0. |None |
