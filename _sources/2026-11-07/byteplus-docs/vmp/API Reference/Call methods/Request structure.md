---
title: "Request structure"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/Request-structure"
---

To call the BytePlus OpenAPIs, you need to send requests that are composed of valid signatures and specific business\-related elements to the service addresses. This topic covers the service addresses of BytePlus OpenAPIs, communication protocols, and other API\-related information.

<span id=".5pyN5Yqh5Zyw5Z2A"></span>
## Service addresses

The regions have their own OpenAPI addresses. For details, see [Service addresses](https://docs.byteplus.com/en/docs/vmp/Service_address).

<span id=".6YCa5L-h5Y2P6K6u"></span>
## Communication protocols

All communications with APIs are based on HTTPS protocol to ensure high security.

<span id=".6K-35rGC5pa55rOV"></span>
## Request methods

**POST** is the only method allowed for OpenAPI communications.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The public parameters  <code>Action</code> and <code>Version</code> need to be placed in the <code>Query String</code> of POST requests.</div>


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

There are two parameter categories for BytePlus OpenAPIs:


* **Public request parameters**: the parameters required by default. For details, see [Public parameters](https://docs.byteplus.com/en/docs/vmp/Common-parameters).

* **Specific parameters**: the parameters for specific APIs. For details, see the documentation specifically for that API.


<span id=".5a2X56ym57yW56CB"></span>
## Character encoding

Requests and responses are both encoded in UTF\-8.
