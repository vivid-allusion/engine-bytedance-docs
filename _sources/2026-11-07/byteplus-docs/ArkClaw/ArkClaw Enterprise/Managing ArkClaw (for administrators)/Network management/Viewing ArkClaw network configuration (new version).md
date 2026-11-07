---
title: "Viewing ArkClaw network configuration (new version)"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Viewing_ArkClaw_network_configuration_new_version"
---

ArkClaw Network Configuration includes both ingress​ and egress​ information for public and private networks. After successfully activating ArkClaw Enterprise, as the administrator, you can view the related network configuration.

<span id="T1VtDgDE"></span>
## Before you begin

You have activated ArkClaw Enterprise and completed relevant network configuration. For details, see [ArkClaw Network Configuration overview](https://docs.byteplus.com/en/docs/ArkClaw/ArkClaw_Network_Configuration_overview).

<span id="Ood16TeK"></span>
## View the space ingress

<span id="MJRnigvO"></span>
### View public network ingress configuration


1. Log in to [the ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, select "Resource Configuration \> Network Configuration".

3. Click the "Space Ingress" tab, and view the public network ingress information.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The administrator can manage the public network ingress configuration as needed. For procedure, see <a href="https://docs.byteplus.com/en/docs/ArkClaw/configuring-a-custom-enterprise-domain-old-version">Configuring a custom enterprise domain</a> and <a href="https://docs.byteplus.com/en/docs/ArkClaw/configuring-a-custom-domain-prefix-old-version">Configuring a custom domain prefix</a>.   </div>
   

   
   |Public network ingress type |Description |
   |---|---|
   |Employee login link |The default public login entry point after ArkClaw is activated. It is automatically generated according to platform rules and cannot be modified. |
   |Custom enterprise domain |A fully customizable, enterprise\-exclusive public login entry point. The administrator configures it. It must be bound to an enterprise\-owned, ICP\-filed domain. |
   |Custom domain prefix |A semi\-customizable, enterprise\-exclusive public login entry point. The administrator configures it. No owned domain is required. A custom prefix is added before the fixed platform domain suffix. |
   


<span id="qaghdMKB"></span>
### View private network ingress configuration


1. Log in to [the ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, select "Resource Configuration \> Network Configuration".

3. Click the "Space Ingress" tab, and view the private network ingress information.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The administrator can manage the private network ingress configuration as needed. For procedure, see <a href="https://docs.byteplus.com/en/docs/ArkClaw/Configuring-account-allowlist">Configuring account allowlist</a>, <a href="https://docs.byteplus.com/en/docs/ArkClaw/Configuring-a-custom-domain-prefix">Configuring a custom domain prefix</a>, and <a href="https://docs.byteplus.com/en/docs/ArkClaw/Accepting-or-rejecting-a-connection">Accepting or rejecting a connection</a>.   </div>
   

   
   |Module |Description |
   |---|---|
   |Access domain |The system automatically assigns a private ingress domain in the format: `<spaceID>.arkclaw-enterprise-<region initials, e.g., China (Beijing) - bj>.volceapi.com`. Administrators can customize the prefix by replacing the <spaceID\> portion with a memorable string. |
   |Account allowlist |Business accounts that can create an interface endpoint​ to access the Claw instance via private network. Administrators control which business accounts can access Claw over the private network by adding them to the allowlist. |
   |Connection list |Connection that is established when the interface endpoint is linked to the private network ingress. Administrators can manually disconnect existing connections as needed. For example, before removing an account from the private network ingress allowlist, its connection should first be disconnected. Previously rejected or disconnected connections can also be manually accepted to re\-establish access. |
   


<span id="fcQGc7km"></span>
## View the space egress

<span id="UeW7kNfg"></span>
### View public network egress configuration


1. Log in to [the ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, select "Resource Configuration \> Network Configuration".

3. Click the "Space Egress" tab, and view the public network egress information.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The administrator can manage the public network egress configuration as needed. For procedure, see <a href="https://docs.byteplus.com/en/docs/ArkClaw/Public-network-egress">Public network egress</a>.   </div>
   

   * **View ** **configuration**: View the enablement status of the public network egress, access log, and cross\-border service, as well as egress details. The egress information shows ArkClaw Enterprise provides a public network egress IP pool. Custom editing is not supported.

      * **default**: The system\-assigned default public network egress for China Mainland, containing two IP addresses.

      * **Managed Asia\-Pacific egress group**: A managed cross\-border public egress group enabled after activating Cross\-Border Acceleration. Viewing or selecting specific IP addresses is not supported.

   * **View ** **security controls**: Respectively click the "Network access policy" or "Web access policy" tab, and view access controls configured for the public network egress, including the policy ID, enablement status, and rules.


<span id="lqPWME9V"></span>
### View private network egress configuration


1. Log in to [the ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, select "Resource Configuration \> Network Configuration".

3. Click the "Space Egress" tab, and view the private network egress information.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The administrator can manage the private network egress configuration as needed. For procedure, see <a href="https://docs.byteplus.com/en/docs/ArkClaw/Private-network-egress">Private network egress</a>.   </div>
   

   * **View ** **configuration**: View the enablement status, basic information (including the associated VPC, availability zones, and security group), access targets, and DNS resolution configuration of the private network egress, as well as the status of its access logs.

   * **View ** **security controls**: Respectively click the "Network access policy", "Web access policy" or "DNS access policy" tab, and view access controls configured for the private network egress, including the policy ID, enablement status, and rules.


&nbsp;
