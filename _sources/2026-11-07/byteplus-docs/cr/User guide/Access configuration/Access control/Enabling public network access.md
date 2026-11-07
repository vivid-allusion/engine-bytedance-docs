---
title: "Enabling public network access"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/enable-public-network-access"
---

By default, public network access is not enabled after a Standard Edition instance is created. To push or pull images via the public network, manually enable public network access and optionally configure a public network access allowlist.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">This operation applies only to Standard Edition instances. Public network access is enabled by default for Micro Edition instances, and no additional configuration is required.</div>


<span id="qrPzmTdC"></span>
## Background

After public network access is enabled, by default all IP addresses are inaccessible, and an allowlist must be configured for normal use. Adding an allowlist divides into the following two scenarios:


|**Scenario** |**Description** |**Trigger time** |
|---|---|---|
|Add allowlist when enabling |When enabling public network access for the first time, the system pops up a dialog box requiring at least one allowlist address to be entered, otherwise enabling cannot be completed. |This dialog automatically pops up when you click the public network access switch. |
|Add allowlist after enabling |After public network access is enabled, you can add more allowlist addresses at any time on the IAM page. |In the public network tab, click the **Add access allowlist** button. |


You can add a public network access allowlist as needed.


* Deny access from all addresses: Leave the field empty.

* Specify access from certain addresses: Enter the IP addresses (such as 192.168.0.1) or CIDR blocks (such as 192.168.1.0/24) for allowlist access.

   * Separate multiple IP addresses or CIDR blocks with line breaks or commas (,).

   * When you enter multiple entries, the IP ranges must not overlap.

* Allow access from all IPv4 addresses: Enter `0.0.0.0/0`.


<span id="YpBtif5N"></span>
## Prerequisites

A Standard Edition instance has been created. For instructions, see [Create standard instance ](https://docs.byteplus.com/en/docs/cr/create-a-container-registry-enterprise-edition-instance).

<span id=".5byA5ZCv5YWs572R6K6_6Zeu"></span>
## Enabling public network access

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">After you enable public access in the console, it typically takes 3 to 5 minutes for resolution before the instance becomes publicly accessible.</div>



1. Log in to the target instance.

   1. Log in to the [CR console](https://console.byteplus.com/cr).

   2. Select the target region in the top navigation bar.

   3. In the left navigation bar, click **List of instances**, find the target instance, and click **Enter instance**.In the left navigation bar, click **Access control**.

2. Click the **Public network** tab.

3. In the upper right corner of the page, click the **Turn off/Enable **  switch.

4. On the confirmation page, click **Confirm**.

5. In the **Enable public network access **  dialog box, configure the **allowlist address.** 

6. Click **Confirm**.


<span id="H6Yj5AVa"></span>
## Add a public network access allowlist

After public network access is enabled, you can add more allowlist addresses at any time.


1. Log in to the target instance.

   1. Log in to the [CR console](https://console.byteplus.com/cr).

   2. Select the target region in the top navigation bar.

   3. In the left navigation bar, click **List of instances**, find the target instance, and click **Enter instance**.

2. In the left navigation bar, click **Access control**.

3. Click the **Public network** tab.

4. Click **Add access allowlist**.

5. Enter the IP address or CIDR block to allow access. Separate multiple rules with line breaks or English commas.

6. Click **Confirm**.
