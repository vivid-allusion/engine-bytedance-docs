---
title: "[Product announcement] NGINX Ingress EOM"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Product_announcement_NGINX_Ingress_EOM"
---

<span id="Yp7mP6Lt"></span>
## Change

Kubernetes SIG Network and the Security Response Committee announced the retirement of Ingress NGINX in the community blog [Ingress NGINX Retirement: What You Need to Know](https://kubernetes.io/zh-cn/blog/2025/11/11/ingress-nginx-retirement/). To align with the community changes, VKE adjusted its maintenance policy for the NGINX Ingress Controller add\-on:


1. **Limited maintenance stage**: From now until November 30, 2026, VKE will provide minimal maintenance required to address only a very limited number of critical security issues (depending on available maintenance resources).

2. **Official retirement time**: Starting from December 1, 2026, VKE will fully discontinue all maintenance efforts, including but not limited to:

   * No longer releasing new versions or feature iterations.

   * No longer fixing any known or newly discovered vulnerabilities.

   * No longer providing security patches or compliance updates.

   * Switching the GitHub code repository to read\-only mode.


<span id="a3IXbPhJ"></span>
## Impact

VKE plans to stop support for the NGINX Ingress Controller starting from December 1, 2026, Beijing Time (UTC+8). The following cluster features will be affected by this support change:


|Features affected |Change |Reference |
|---|---|---|
|cluster |The ingress\-nginx add\-on will no longer be available during cluster creation. |[Create a cluster.](https://docs.byteplus.com/en/docs/vke/Creating-a-cluster) |
|Ingresses |Creation of NGINX Ingresses is no longer supported. |[Nginx Ingress](https://docs.byteplus.com/en/docs/vke/Nginx-Ingress) |
|Add\-on management |The ingress\-nginx add\-on can no longer be installed in clusters. |[Installing add-ons](https://docs.byteplus.com/en/docs/vke/Installing-an-add-on) |
|Application templates |The ingress\-nginx entry in the application templates will be retained. You can still use the application templates to install resources in a cluster. However, the VKE team will no longer provide security and reliability maintenance for template resources. Use these application templates with caution. |[Application templates](https://docs.byteplus.com/en/docs/vke/Application-templates) |


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The discontinuation of the feature and add\-on will have slightly different impacts on new and existing users:</div>



* <div data-tips="true" data-tips-type="warning">For new users: We recommend using APIG Ingress or ALB Ingress. If you continue using NGINX Ingress, fully understand the associated risks before contacting your account manager.</div>


* <div data-tips="true" data-tips-type="warning">For existing users: Existing deployments and capabilities in clusters with the ingress\-nginx component installed or NGINX Ingress resources created continue functioning normally. However, we recommend prompt migration to avoid potential usage risks.</div>



<span id="9zyz77zF"></span>
## Migration solutions

To ensure security of cluster\-based applications, we recommend migrating existing NGINX Ingress workloads to other types of Ingresses before the retirement of the NGINX Ingress Controller. For details, see the following documentation:


* [Migrating from NGINX Ingresses to APIG Ingresses](https://docs.byteplus.com/en/docs/vke/Migrating_from_NGINX_Ingresses_to_APIG_Ingresses)

* [Migrating from NGINX Ingresses to ALB Ingresses](https://docs.byteplus.com/en/docs/vke/Migrating_from_NGINX_Ingresses_to_ALB_Ingresses)


Plan your Ingress migration based on your business scenarios. If you encounter any issues during migration or need more technical support, feel free to [submit a ticket](https://console.byteplus.com/workorder/create?step=1).

&nbsp;
