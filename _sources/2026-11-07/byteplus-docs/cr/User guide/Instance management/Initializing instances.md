---
title: "Initializing instances"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/initialize-an-instance"
---

When you log in to a CR instance for the first time, you can follow the interactive wizard on the page to complete the initial setup of the instance. This facilitates your use of CR in subsequent business scenarios. The initial setup includes network configuration, key setup, and image push/pull address command configuration.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">This operation applies only to Standard Edition instances.</div>


<span id=".5YeG5aSH5bel5L2c"></span>
## Prerequisites

A Standard Edition instance has been created. For instructions, see [create a standard instance ](https://docs.byteplus.com/en/docs/cr/create-a-container-registry-enterprise-edition-instance).

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the target instance.

   1. Log in to the [CR console](https://console.byteplus.com/cr).

   2. Select the target region in the top navigation bar.

   3. In the left navigation bar, click **List of instances**, find the target instance, and click **Enter instance**.

2. Configure network information, then click **Next** after completion.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Enabling public network access may take 5 to 10 minutes. You can later check the status on the  <strong>Access control</strong> page.   </div>
   

   
   |Parameter |Description |
   |---|---|
   |Intranet access |* Associated project: Associate the target project. After association, members of that project will inherit corresponding permissions for the CR services based on project authorization. For details, please refer to Project Management and Managing Project Authorizations.<br><br>* Private network: Select the VPC that the CR instance can access. After you enable intranet access, push and pull speeds can be effectively improved without public network bandwidth consumption.<br><br>* Subnet: Select the subnet that the CR instance can access. |
   |Public NAT for internet endpoint |<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Enabling public network access requires 5–10 minutes. You can proceed with subsequent steps first, and verify the status in the access control page after initialization.</div><br><br><br>* <div data-tips="true" data-tips-type="default">After public network access is enabled, all IP access is denied by default. Please promptly configure the IP allowlist; to allow access from the entire network, add the rule 0.0.0.0/0.</div><br><br><br><br>After enabling public network access, resources in the public network environment can directly push and pull images in the Standard instance, and pull images in the proxy repository instance.<br><br><br>* Access portal: Whether to enable the public network access portal, click to enable.<br><br>* Allowlist address: According to business needs, enable public network access and add addresses to the public network access allowlist.<br><br>   * Deny access from all addresses: Leave the field empty.<br><br>   * Allow access from specific addresses: Enter the IP addresses or CIDR blocks that you want to allow. Separate multiple IP addresses or CIDR blocks with line breaks or commas (,). When you enter multiple entries, the IP ranges must not overlap.<br><br>   * Allow access from all IPv4 addresses: Enter `0.0.0.0/0`. |
   |Current instance network connectivity |Click **Get it now** to display the current status of intranet and public network access. |
   

3. Set the instance access password, then click **Next** after completion.

   
   |Parameter |Description |
   |---|---|
   |Set CR password |Supports configuring a fixed CR password, suitable for long\-term operations personnel for registry management; you can click the switch on the right to skip this configuration and complete login using a temporary access instruction. |
   |Get temporary access instruction |Click **Click to obtain and copy the temporary access instruction** to obtain the temporary login password for the CR instance for temporary access. The password is valid for 1 hour. |
   

4. Select the namespace where the instance resides. Obtain the commands for logging in to the CR instance and pushing or pulling images. For methods to create a namespace, see [Namespace management](https://docs.byteplus.com/en/docs/cr/create-a-namespace).

5. Click **Complete** to finish instance initialization.
