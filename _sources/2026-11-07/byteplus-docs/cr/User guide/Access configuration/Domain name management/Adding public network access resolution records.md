---
title: "Adding public network access resolution records"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/Add_resolution_records_for_public_network_access"
---

If you need to access CR from the public network via a third\-party domain name, you need to manually configure the corresponding public network access resolution record on your domain name resolution platform. This topic uses TrafficRoute as an example to describe how to configure public network access resolution records. The configuration process is similar on other platforms.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When you add a custom domain name hosted on <strong>TrafficRoute</strong>, the public network access resolution record is automatically configured, and no manual configuration is required.</div>


<span id=".6IOM5pmv5L-h5oGv"></span>
## Background

In the example provided in this topic, a CNAME record is added to resolve the `www.test.team` custom domain name to the standard domain name `abc-cn-beijing.cr.volces.com`. In the standard domain name, `abc` is the name of the CR instance.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [DNS console](https://console.byteplus.com/TrafficRoute/dns/public-zone).

2. On the **Domain management** page, click the target domain name.

3. On the **DNS records** tab, click **Create record set**.

4. On the **Create record set** page, fill in the basic information and record value as shown below.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For detailed parameter description, see <a href="https://docs.byteplus.com/en/docs/byteplus-dns-suite/docs-creating-updating-or-deleting-dns-records">Create DNS Records</a> in the <strong>TrafficRoute</strong> product documentation.   </div>
   

5. After the configuration is complete, click **Confirm**.
