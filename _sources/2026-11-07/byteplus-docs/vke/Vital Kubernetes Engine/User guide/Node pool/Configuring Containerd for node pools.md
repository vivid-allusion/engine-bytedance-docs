---
title: "Configuring Containerd for node pools"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Configuring_containerd_for_node_pools"
---

VKE allows you to specify custom Containerd parameters for node pools to meet requirements such as image pull acceleration, security authentication, and concurrency performance tuning. This topic describes the supported Containerd parameters as well as their usage restrictions and configuration methods.

<span id="BIETOy6N"></span>
## Limits

Custom Containerd settings for node pools apply only to newly scaled\-out nodes and newly added nodes.

<span id="9spgtLLk"></span>
## Supported Containerd settings


|**Parameter** |**Description** |**Configuration recommendations** |
|---|---|---|
|Container image repository proxy (RegistryProxyConfigs) |CR proxies. A CR proxy allows the container runtime to pull images from an alternative image registry, speeding up image pulling.<br><br><br>* **Container image repository**: the address of the CR instance. The address format is [domain_or_IP][:port], where the port number is optional. Note that no protocol is included. Examples: `example.com` and `example.com:8080`<br><br>* **Proxy endpoint**: the proxy address. The format is [protocol]://[domain_or_IP][:port], where the protocol prefix is required, and the port number is optional. Examples: `https://example.com` and `https://example.com:8080`. |We recommend that you configure CR proxies by using the proxy cache capability of CR. |
|Container image repositories that skip certificate authentication (Insecure Registries) |Specify the URL of the CR instance for which certificate authentication will be skipped. When the container runtime pulls a container image from the CR instance, it skips certificate authentication. The value must be a domain name or IP address, optionally followed by a port number (for example, `example.com` or `example.com:8080`). Do not include a protocol. |Skipping certificate verification is typically applicable to testing environments for pulling container images from a Container Registry (CR) instance that uses a self\-signed certificate. This feature is not recommended for production. |
|**Custom parameters** |||
|max_concurrent_downloads |The maximum number of image layers that Containerd can download concurrently when pulling images at a time.<br><br><br>* The value is a positive integer. Default value: 3.<br><br>* If you do not specify this parameter, the default value is used.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter is supported only if the Containerd version is v2.1.0 or later.</div><br> |We recommend keeping the default value. You can increase the value to accelerate multi\-layer image pulls. Before increasing the value, make sure that the node has sufficient network bandwidth and disk I/O capacity and that the image registry has sufficient throttling capacity. |
|max_concurrent_unpacks |The maximum number of image layers that Containerd can decompress simultaneously.<br><br><br>* The value is a positive integer. Default value: 1.<br><br>* This parameter takes effect only if `use_local_image_pull` is disabled.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter is supported only if the Containerd version is v2.2.0 or later.</div><br> |Increasing this value can improve the concurrent decompression capability of image layers, but it also increases the CPU and disk I/O pressure on the node. We recommend performing stress testing based on node specifications and business load, and then adjusting it gradually. |
|concurrent_layer_fetch_buffer |The buffer size used when a single image layer is concurrently pulled in chunks. The value is a positive integer. Unit: bytes.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter is supported only if the Containerd version is v2.1.0 or later.</div><br> |We recommend specifying this parameter as needed. Increasing this value may increase pull throughput for large image layers, but it will also increase the memory usage of Containerd. Perform stress testing based on the image size, network bandwidth, and available node memory. This prevents node memory pressure from increasing due to a high value. |
|use_local_image_pull |The image pull mode of Containerd.<br><br><br>* true: (Default) Use a local client to pull images.<br><br>* false: Use Transfer Service to pull images.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter is supported only if the Containerd version is v2.1.0 or later.</div><br> |When this parameter is disabled, the Nydus image lazy loading feature cannot be used. Confirm that the node does not use the related capability before making the adjustment. |


<span id="Q2zQL7Dq"></span>
## Custom Containerd settings

<span id="QAOvBRPd"></span>
### Configuring when creating clusters

You can configure Containerd settings when you create clusters.

To do so, go to the **Advanced configurations** section in the **Node pool configuration** step of the cluster creation wizard. For detailed instructions, see [Creating clusters](https://docs.byteplus.com/en/docs/vke/Creating-a-cluster).

<span id="i89KLYJM"></span>
### Configuring when creating node pools

You can configure Containerd settings when you create new node pools for a cluster.

To do so, go to the ** Advanced configurations** section in the ** Node pool configuration** step of the node pool creation wizard. For detailed instructions, see [Creating node pools](https://docs.byteplus.com/en/docs/vke/Creating-a-NodePool) and [Creating managed node pools](https://docs.byteplus.com/en/docs/vke/Creating-a-managed-NodePool).

<span id="7DY2zgge"></span>
### Configuring existing node pools

You can configure Containerd settings for the existing node pools of a cluster.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">When you configure Containerd settings for an existing node pool, the settings take effect only for nodes newly added to the node pool, not for existing nodes.</div>


On the **Node pool** page, find the target node pool and click `...` \> **Containerd configuration**. For detailed instructions, see [Managing node pools](https://docs.byteplus.com/en/docs/vke/Managing-NodePools).
