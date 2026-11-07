---
title: "[Product announcement] Announcing control-plane (API Server) connectivity path switch for managed VKE clusters"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Product_announcement_Announcing_API_Server_connectivity_path_switch_for_managed_VKE_clusters"
---

For VKE\-managed clusters created in or after May 2026, access to the control plane (API Server) by node\-side components (kubelet, kube\-proxy, and vpc\-cni) will be gradually switched from CLB VIP access to internal domain\-based access. This change aims to enhance cluster control\-plane performance and stability.

<span id="FmkbbjGD"></span>
## **Scope of change**

VKE\-managed clusters created in or after May 15, 2026.

<span id="L7SUjBeT"></span>
## **Changes and impact**

After the change in the connectivity path to the control plane (API Server) of VKE\-managed clusters, node components (such as kubelet, kube\-proxy, and vpc\-cni) will access the API Server by using its domain name instead of the associated CLB VIP.

The domain name of an API Server follows the format below and cannot be changed. This domain name is hosted and resolved by VKE through PrivateZone free of charge.

```Plain Text
{集群 ID}.vke.{地域 ID}.ibytepluses.com
```


The specific changes resulting from the connectivity path switch are as follows:


|**Item** |**Before the change (CLB forwarding)**  |**After the change (direct connection using the internal domain)**  |
|---|---|---|
|Kubernetes Service Endpoints |Point to the CLB IP address. |Point to the ENI IP address of the API Server. This enables direct connection for in\-cluster applications (such as Operator) and reduces performance overhead from intermediate forwarding. |
|Node\-side data\-plane component service discovery |kubelet, kube\-proxy, and vpc\-cni access the API Server via the CLB VIP. |Resolve the API Server domain name to the ENI IP address of the API Server, further enhancing the high availability of the cluster. |


<span id="o5BgrdRc"></span>
## **Considerations**


* If the security groups associated with nodes or Pods block outbound traffic on port 6443, the API Server connection will fail.

* API Server domain names are created and managed by VKE through PrivateZone.

* API Server domain name resolution takes effect within the VPC of the cluster. To ensure normal domain name resolution, use the default private DNS servers (`100.96.0.2` and `100.96.0.3`) in the VPC.

* If you have configured custom DNS server IP addresses on nodes, ensure the default private DNS servers are used to resolve the domain name of the API Server.

* To learn how to enable internal domain\-based access to the API Server for existing clusters, see [Best practices](https://docs.volcengine.com/docs/6460/2488937).


<span id="mAcSxXPJ"></span>
## **Contact us**

If you have any questions about this change, [submit a ticket](https://console.byteplus.com/workorder/create?step=1) to contact us.
