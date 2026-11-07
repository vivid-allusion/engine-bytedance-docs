---
title: "Product specifications"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/specifications"
---

This article introduces Cloud Search instance specifications to help you configure instance specifications more easily when creating instances.

<span id=".5YW85a6554mI5pys"></span>
## Instance version

The Cloud Search service console currently supports Elasticsearch and OpenSearch instances.


* Elasticsearch instances: support `6.7.1`, `6.8.23`, and `7.10.2` versions. Recommend using the more feature\-rich `7.10.2` version.

* OpenSearch instances: support `2.9.0` and `3.3.0` versions. OpenSearch 2.9.0 and 3.3.0 versions support vector and text hybrid search, DiskANN algorithm, and AI scenarios. Using OpenSearch 2.9.0 and 3.3.0 versions is highly recommended.


<span id="2b828379"></span>
## Instance node specification


|**Specification type** |**vCPU** |**Memory** |
|---|---|---|
|es.x4.small<br><br>(for testing only, disabled in production) |1 core |4 GiB |
|es.x2.medium |2 cores |4 GiB |
|es.x4.medium |2 cores |8 GiB |
|es.x8.medium |2 cores |16 GiB |
|es.x2.large |4 cores |8 GiB |
|es.x4.large |4 cores |16 GiB |
|es.x8.large |4 cores |32 GiB |
|es.x2.xlarge |8 cores |16 GiB |
|es.x4.xlarge |8 cores |32 GiB |
|es.x8.xlarge |8 cores |64 GiB |
|es.x1.2xlarge |16 cores |16 GiB |
|es.x2.2xlarge |16 cores |32 GiB |
|es.x4.2xlarge |16 cores |64 GiB |
|es.x8.2xlarge |16 cores |128 GiB |
|es.x2.2.5xlarge |24 cores |48 GiB |
|es.x4.2.5xlarge |24 cores |96 GiB |
|es.x8.2.5xlarge |24 cores |192 GiB |
|es.x1.3xlarge |32 cores |32 GiB |
|es.x2.3xlarge |32 cores |64 GiB |
|es.x4.3xlarge |32 cores |128 GiB |
|es.x8.3xlarge |32 cores |256 GiB |
|es.x2.5xlarge |48 cores |96 GiB |
|es.x4.5xlarge |48 cores |192 GiB |
|es.x1.6xlarge |64 cores |64 GiB |


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">es.x2.5xlarge and es.x4.5xlarge specifications currently support only the North China 2 (Beijing) region.</div>


<span id="b560ef2a"></span>
## Kibana node specification


|**Specification type** |**vCPU** |**Memory** |
|---|---|---|
|kibana.x2.small |1 core |2 GiB |
|kibana.x2.medium |2 cores |4 GiB |
|kibana.x4.medium |2 cores |8 GiB |
|kibana.x2.large |4 cores |8 GiB |
|kibana.x4.large |4 cores |16 GiB |
|kibana.x2.xlarge |8 cores |16 GiB |
|kibana.x4.xlarge |8 cores |32 GiB |
|kibana.x2.2xlarge |16 cores |32 GiB |
|kibana.x4.2xlarge |16 cores |64 GiB |
|kibana.x2.3xlarge |32 cores |64 GiB |
|kibana.x4.3xlarge |32 cores |128 GiB |


<span id="7b11a1ce"></span>
## Storage specifications


|**Storage type** |**Description** |
|---|---|
|es.volume.essd.pl0 |Standard edition \- high\-performance cloud disk \- pl0 |
|es.volume.essd.flexpl\-standard |Standard edition \- high\-performance cloud disk \- flexpl |
|es.volume.essd.tl0 |Standard edition \- high\-performance cloud disk \- tl0<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The TL0 storage specifications are currently in grayscale release, and TL0 specifications are not yet available in some regions. To use, please <a href="https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000255">submit a ticket</a> to contact technical support.</div><br> |


<span id="bc3ac6ae"></span>
## Public network bandwidth specifications

Enable public network access for instances and visualization tools. The system automatically allocates dedicated bandwidth for public network access based on your configured bandwidth.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The current public network bandwidth limits for instances are [1, 500] Mbps, and for Kibana/Dashboards are [1, 200] Mbps. If you require higher bandwidth, please <a href="https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000255">submit a ticket</a> to apply.</div>



|**Resource type** |**Instance bandwidth** |**Kibana/Dashboards bandwidth** |
|---|---|---|
|es.eip.bgp_fixed_bandwidth |[1，500] Mbps |[1，200] Mbps |


<span id="39af1ab3"></span>
## Analytical services specifications


|**Specification type** |**vCPU** |**Memory** |
|---|---|---|
|sql.x4.medium |2 cores |4 GiB |
|sql.x4.large |4 cores |16 GiB |
|sql.x4.xlarge |8 cores |32 GiB |
|sql.x4.2xlarge |16 cores |64 GiB |


&nbsp;
