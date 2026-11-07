---
title: "Private Network Ingress overview"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Private-Network-Ingress-overview"
---

<span id="ngTLY1AM"></span>
## Overview

ArkClaw Enterprise provides space\-level private network ingress for scenarios such as cloud or on\-premises services and employee logins. This avoids public network exposure and reduces security risks.

<div data-tips="true" data-tips-type="default">Note</div>


<div data-tips="true" data-tips-type="default">Private Network Ingress is currently in the invite\-only beta stage. To request a trial, contact your account manager.</div>


<span id="U0fFb9rA"></span>
## Features


|Feature |Description |Related documentation |
|---|---|---|
|Account allowlist |Administrators control which business accounts can access ArkClaw over the private network by adding them to the allowlist. Once added, a business account can [create an interface endpoint](https://docs.byteplus.com/en/docs/privatelink/Endpoint-02)​ to access the Claw instance via private network.interface endpoint |[Configuring account allowlist](https://docs.byteplus.com/en/docs/ArkClaw/Configuring-account-allowlist) |
|Connection management |Administrators can manually disconnect existing connections as needed For example, before removing an account from the private network ingress allowlist, its connection must be disconnected first Disconnected connections can be manually accepted to re\-establish access |[Accepting or rejecting a connection](https://docs.byteplus.com/en/docs/ArkClaw/Accepting-or-rejecting-a-connection) |
|Private ingress domain |The system automatically assigns a private ingress domain in the format `<SpaceId>.arkclaw-enterprise-<Region>.volceapi.com`.<br><br><br>* SpaceId: The space ID.<br><br>* Region: The pinyin initials of the region where the private network ingress is located, for example, China (Beijing) is `bj`. |\-\- |


<span id="fnTO1OwZ"></span>
## Custom domain name

The system\-assigned private ingress domain name is difficult to remember. To make it easier for employees to recognize, administrators can modify the system\-assigned private ingress domain prefix (i.e., the Space ID in the domain name) or configure a custom domain name.​


|**Comparison item** |**Custom domain name** |**Custom domain prefix** |
|---|---|---|
|Application scenarios<br><br> |* Shared public and private network: The same custom domain name is used for both public and private network ingresses. Employees access through the public network ingress when on the public network, and through the private network ingress when on the private network. This scenario requires the enterprise to complete domain registration and public/private DNS resolution on its own.<br><br>* Private network only: Employees only need to access within the private network, with no public network reachability required. The login entry is expected to fully carry the enterprise's own domain name (as opposed to a platform\-suffixed domain name). |No existing domain name or certificate maintenance capability. A simple branded entry is expected to go live quickly. The platform provides a unified suffixed domain name and certificate, with no registration or certificate management required. Suitable for employee\-side use only, without external presentation needs. |
|Configuration |Full domain name (must be enterprise\-owned and filed domain, e.g., login.example.com). |Domain prefix only (the suffix is provided uniformly by the platform, formatted as `arkclaw-enterprise-<Region>.volceapi.com`, where Region is the pinyin initials of the private network ingress region; for example, China (Beijing) is `bj`). |
|Certificate requirements |* Support purchasing SSL certificates from BytePlus (automatically hosted in the Certificate Center) or uploading third\-party CA certificates.<br><br>* The login becomes unavailable if the certificate expires without replacement.<br><br>* DNS resolution changes shall be handled by the enterprise. |HTTPS certificates are maintained by ArkClaw. No enterprise intervention is required. |
|Configuration method |[Configuring a custom domain name](https://docs.byteplus.com/en/docs/ArkClaw/Configuring-a-custom-domain-name) |[Configure a custom domain prefix](https://docs.byteplus.com/en/docs/ArkClaw/Configuring-a-custom-domain-prefix) |
|Permission requirements |Configurable only by enterprise space administrators ||


<span id="V9HwhAB3"></span>
## **Limits**

Each endpoint supports a maximum bandwidth of 10 Gbps per availability zone.

<span id="gAROZ0sU"></span>
## Billing

Endpoint fees apply when a business account creates an interface endpoint. For billing details, see [PrivateLink Billing](https://docs.byteplus.com/en/docs/privatelink/Billing-rules).

<span id="pgXV0UiL"></span>
## Configuration procedure


1. [Configure the account allowlist](https://docs.byteplus.com/en/docs/ArkClaw/Configuring-account-allowlist): The administrator adds business accounts to the allowlist.

2. (Optional) [Configure a custom domain name](https://docs.byteplus.com/en/docs/ArkClaw/Configuring-a-custom-domain-name) or [configure a custom domain prefix](https://docs.byteplus.com/en/docs/ArkClaw/Configuring-a-custom-domain-prefix): Administrators can modify the system\-assigned private ingress domain prefix (i.e., the Space ID in the domain name) or configure a custom domain name for easy memorization by employees.​

3. [Create an interface endpoint](https://docs.byteplus.com/en/docs/privatelink/Endpoint-02): When a business account creates an interface endpoint, set the “Endpoint service” parameter to the private ingress domain name to establish a PrivateLink connection.


&nbsp;

&nbsp;
