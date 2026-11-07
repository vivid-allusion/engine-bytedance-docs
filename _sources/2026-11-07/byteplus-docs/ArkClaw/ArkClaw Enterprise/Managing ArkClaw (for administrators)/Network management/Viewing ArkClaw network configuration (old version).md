---
title: "Viewing ArkClaw network configuration (old version)"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Viewing_ArkClaw_network_configuration"
---

ArkClaw Network Configuration includes both ingress​ and egress​ information for public and private networks. After successfully activating ArkClaw Enterprise, as the administrator, you can view the related network configuration.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Tip</div>


<div data-tips="true" data-tips-type="default">The old version of network configuration supports limited features. If you need to use the following features, go to <a href="https://console.byteplus.com/arkclaw/enterprise">the ArkClaw Enterprise console</a> to find your Space ID, and <a href="https://console.byteplus.com/workorder/create">submit a ticket</a> to upgrade the Space.</div>



* <div data-tips="true" data-tips-type="default">Public network egress features: Network Access Policy, Web Access Policy, and Access Log. After getting the permission, see <a href="https://docs.byteplus.com/en/docs/ArkClaw/Configuring_network_access_policy_for_public_network_egress">Configuring network access policy for public network egress</a>, <a href="https://docs.byteplus.com/en/docs/ArkClaw/Configuring-Web-access-policy-for-public-private-network-egress-non-cross-border">Configuring Web access policy for public network egress</a>, or <a href="https://docs.byteplus.com/en/docs/ArkClaw/Configuring-cross-border-acceleration-policy-new-version">Enabling or disabling access log for public network egress</a> for procedure.</div>


* <div data-tips="true" data-tips-type="default">Private network egress features: Network Access Policy, Web Access Policy, and Access Log. After getting the permission, see <a href="https://docs.byteplus.com/en/docs/ArkClaw/Configuring-a-private-egress-network-access-policy">Configuring network access policy for private network egress</a>, <a href="https://docs.byteplus.com/en/docs/ArkClaw/Configuring-a-private-egress-web-access-policy">Configuring Web access policy for private network egress</a>, or <a href="https://docs.byteplus.com/en/docs/ArkClaw/Configuring-a-private-egress-access-log">Configuring access log for private network egress</a> for procedure.</div>



<span id="8jk7Mvkw"></span>
## Before you begin

You have activated ArkClaw Enterprise and completed relevant network configuration. For details, see [ArkClaw Network Configuration overview](https://docs.byteplus.com/en/docs/ArkClaw/ArkClaw_Network_Configuration_overview).

<span id="UJXCZJAL"></span>
## View the space ingress


1. Log in to [the ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, select "Resource Configuration \> Network Configuration".

3. On the Network Configuration page, view the public network ingress information.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The administrator can manage the public network egress configuration as needed. For procedure, see <a href="https://docs.byteplus.com/en/docs/ArkClaw/Public-network-ingress">Public network egress</a>.   </div>
   

   
   |Public network ingress type |Description |
   |---|---|
   |Employee login link |The default public login entry point after ArkClaw is activated. It is automatically generated according to platform rules and cannot be modified. |
   |Custom enterprise domain |A fully customizable, enterprise\-exclusive public login entry point. The administrator configures it. It must be bound to an enterprise\-owned, ICP\-filed domain. |
   |Custom domain prefix |A semi\-customizable, enterprise\-exclusive public login entry point. The administrator configures it. No owned domain is required. A custom prefix is added before the fixed platform domain suffix. |
   


<span id="Ojkf4d2H"></span>
## View the space egress

<span id="NkpeOBt8"></span>
### View public network egress configuration


1. Log in to [the ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, select "Resource Configuration \> Network Configuration".

3. In the "Space Egress" section, view the enablement status of the public network egress and cross\-border service, as well as the acceleration domain.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The administrator can manage the public network egress configuration as needed. For procedure, see <a href="https://docs.byteplus.com/en/docs/ArkClaw/Public-network-egress">Public network egress</a>.   </div>
   

&nbsp;

<span id="I8VmSGfa"></span>
### View private network egress configuration


1. Log in to [the ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, select "Resource Configuration \> Network Configuration".

3. In the "Space Egress" section, view the enablement status, basic information (including the associated VPC, availability zones, and security group), access targets, and DNS resolution configuration of the private network egress.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The administrator can manage the private network egress configuration as needed. For procedure, see <a href="https://docs.byteplus.com/en/docs/ArkClaw/Private-network-egress">Private network egress</a>.   </div>
