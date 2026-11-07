---
title: "Querying instance metadata"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Viewing-instance-metadata"
---

Instance metadata provides basic VCI information, such as the instance hostname, instance ID, instance specifications, region, and availability zone. This topic describes how to query instance metadata.

<span id=".5L2_55So6aG755-l"></span>
## Usage notes

Metadata of an instance can be accessed only from within the instance. The metadata is not encrypted or protected, and anyone who can access the instance can query its metadata. If the metadata contains sensitive information, you should take appropriate measures to protect the sensitive data, such as limiting the scope of access and encrypting the metadata.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

The VCI has been created. For details, see [Creating instances](https://docs.byteplus.com/en/docs/vke/Creating-an-instance).

<span id=".5p-l55yL5a6e5L6L5YWD5pWw5o2u"></span>
## Querying instance metadata

<span id=".6K6_6Zeu5pa55byP6K-05piO"></span>
### Access method description

You can query instance metadata by using the cURL tool or an HTTP GET request. The query format is `http://100.96.0.96/latest/${metadata}`.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Replace <code>${metadata}</code> with a specific instance metadata item. For example, to query metadata item <code>instance_id</code>, use <code>http://100.96.0.96/latest/instance_id</code>.</div>


* <div data-tips="true" data-tips-type="tip">For a list of metadata items supported by VCI, see <a href="https://docs.byteplus.com/en/docs/vke/Instance-metadata-items">Instance metadata items</a>.</div>



<span id=".5q2l6aqk5LiA77ya55m75b2V5a6e5L6L"></span>
### Step 1: Log in to the instance

To perform instance metadata operations, you must first log in to the target instance. This topic describes how to log in to a VCI by using a Deployment as an example.


1. Go to the management page of the Deployment.

   1. Log in to the [VKE console](https://console.byteplus.com/vke/overview).

   2. In the left navigation bar, click **Cluster**.

   3. In the cluster list, click the target cluster that runs the VCI application.

   4. In the left navigation bar of the cluster management page, click **Workload** \> **Deployment**.

2. Click the name of the target Deployment to go to the **its ** page.

3. On the **Deployment page**, click **Console** in the upper\-right corner to log in to the VCI pod.


<span id=".5q2l6aqk5LqM77ya5p-l55yL5YWD5pWw5o2u56S65L6L"></span>
### Step 2: Query metadata

For example, after logging in to the VCI pod, you can run the following shell command to query instance metadata by using cURL:

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Ensure that the cURL tool is installed in the container image. If it is not installed, install it first.</div>



* Query the root directory for instance metadata:

   ```shell
   curl http://100.96.0.96/latest
   ```
   

* Query the instance ID:

   ```shell
   curl http://100.96.0.96/latest/instance_id
   ```
   

* Query the billing type of the instance:

   ```shell
   curl http://100.96.0.96/latest/payment/charge_type
   ```
   

* Query IAM roles of the instance:

   ```shell
   curl http://100.96.0.96/volcstack/latest/iam/security_credentials/
   ```
