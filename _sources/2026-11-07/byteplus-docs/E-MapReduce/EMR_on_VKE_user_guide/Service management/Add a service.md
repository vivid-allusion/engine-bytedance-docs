---
title: "Add a service"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Add_a_service"
---

Volcano Engine E\-MapReduce (EMR) allows you to add services that were not selected for installation during cluster creation after the cluster has been successfully created. You can also manage services in an existing cluster, including configuring service parameters, starting, stopping, or restarting services. This document describes how to add services in the EMR console.

<span id="cM4RCeTGgG"></span>
## prerequisites


* The cluster has been created, and its status is running. For detailed instructions on creating a cluster, see [Create virtual clusters](https://docs.byteplus.com/docs/E-MapReduce/109064).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When adding Spark, Ray, Hive, or Proton services, you must use the AK and SK associated with your current identity. For detailed instructions, see <a href="https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-access-keys">API access key management</a>.</div>


<span id="IdzDTrroPK"></span>
## procedure


1. Log in to [EMR console](https://console.byteplus.com/emr/region:emr_fe+ap-southeast-1/home).

2. In the left navigation bar, click **Resource Management \> on VKE \> Cluster Name** to go to the cluster details page.

3. In the left navigation bar, click the Service list tab to access the cluster service list page.

4. Click the Add service button in the upper right corner of the page to enter the Add service page and select the services to add.

5. Click the **Confirm** button and wait for the component installation to complete.


<span id="xOzVHdUhKz"></span>
## what's next

After the service is added, you can configure the service. For detailed instructions, refer to [Configuration management](https://docs.byteplus.com/docs/E-MapReduce/109076).
