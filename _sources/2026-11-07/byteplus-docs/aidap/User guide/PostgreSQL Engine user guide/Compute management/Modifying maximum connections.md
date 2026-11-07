---
title: "Modifying maximum connections"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/Modifying_maximum_connections"
---

This topic introduces how to modify the maximum connections of compute.

<span id="vIKECKZF"></span>
## Background

For services that require high concurrency, set a sufficient number of connections to prevent users from being unable to access the database. Therefore, AI Native BaaS for Supabase provides a method to modify the maximum connections through Open API to support scenarios with increased connections.

The compute of the AI Native BaaS for Supabase supports automatic scaling within the configured compute expansion range; before modifying the maximum connections of compute, calculate the maximum connections according to the compute expansion range for a reasonable setting. The method to calculate the maximum connections based on the compute expansion range is as follows:

`max_connections = max(100, min(4000, 450.5*min(max_compute_size, 8*min_compute_size)))`

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default"><code>max_compute_size</code> is the upper limit of the compute expansion range, <code>min_compute_size</code> is the lower limit of the compute expansion range.</div>


<span id="lB4bgsXm"></span>
## Precautions

Different specifications of compute support different max connections. However, if you previously modified the max connections after creating a compute, the value will remain unchanged after a specification change. In this case, you must manually adjust the max connections to a reasonable value. If you do not modify the value, the previously reasonable max connections value will be too high after you downgrade the specifications, which may cause a memory overflow.

<span id="BIQAG3Zt"></span>
## Modification method

Call the Open API to modify the max connections. For detailed steps, refer to [ModifyComputeParameters](https://docs.byteplus.com/en/docs/aidap/ModifyComputeParameters).
