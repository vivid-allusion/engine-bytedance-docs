---
title: "Proxy mode configuration guide"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/overview-of-proxy-pattern"
---

SealSuite proxy mode is an access solution built on the Zero Trust concept. It controls access at the network port and application URL path levels. The SealSuite client routes traffic through encrypted channels, creating a logical security boundary between endpoints and business systems. It enables precise authorization based on user identity and device status, with support for IP\-, port\-, and URL\-level control. By building a unified logical access boundary, proxy mode ensures consistent security and audit capabilities when employees access internal resources from different network environments.

## Core value and benefits

* **Fine\-grained access control**: Unlike traditional VPNs, which provide broad network segment connectivity, proxy mode uses multiple checks, including traffic routing, basic access policies, and fine\-grained control policies, to control access permissions down to specific IP addresses, domain names, ports, and even URL paths. Employees can access only specific authorized resources. This effectively prevents unauthorized lateral access within the intranet and minimizes security risks.

* **Broad business compatibility**: Proxy mode works at both the network layer and application layer. It is compatible with standard non\-web office software and protocols, such as Git repositories, database clients, and SSH remote connections. It also provides in\-depth access path parsing for web services, meeting diverse enterprise security requirements for R&D and office work.

* **Zero Trust resource hiding**: Following the principle of "authenticate first, connect later," internal resources are invisible to endpoints by default. The gateway opens a dedicated encrypted access channel only after the employee passes identity authentication, the device status is compliant, and access to a specific application is explicitly authorized.

* **Coordination with device security baselines**: The client monitors device security status, such as antivirus software status and non\-compliant processes, so the system can dynamically adjust access permissions. This device trust\-based access mechanism replaces traditional physical Network Access Control (NAC), ensuring flexible and secure permission control.

* **Intelligent routing and access performance**: The client can detect the latency of each proxy gateway cluster and implement **low\-latency\-first routing** to improve the employee access experience. It also supports automatic traffic path determination, using either the proxy channel or local direct connection, to ensure efficient and stable business access.

## Overall architecture and working principles

In proxy mode, the SealSuite Admin Console (Server), client, and proxy gateways work together to enforce zero trust access through traffic routing and access checks.

1. **Configure resources and policies**: The administrator builds the infrastructure in the Admin Console by deploying proxy gateway clusters, defines accessible internal resources, and creates endpoint\-side traffic routing policies, gateway\-side basic Access Policies (ACLs), and fine\-grained control policies for web applications.

2. **Policies and configurations are delivered and synchronized**:

   * **Client side**: After an end user installs the SealSuite client and completes identity authentication, the client pulls the latest traffic routing policies, available proxy gateway cluster information, and accessible application list from the server.

   * **Gateway side**: The proxy gateway also synchronizes the latest basic access policies and fine\-grained control policies in real time.

3. **Endpoint initiates access (client\-side traffic routing decision)** : When an employee initiates network access from an endpoint, the SealSuite client determines whether to take over the traffic based on the traffic routing policy. Traffic is routed through the encrypted proxy tunnel or sent through the local network according to the matched policy action. Traffic that does not match a proxy routing policy uses the local network.

4. **Connection establishment and gateway authentication (gateway\-side permission check)** : After traffic reaches the proxy gateway, the gateway extracts identity, device attributes, and target resource information from the request and compares them with the policy library. For web requests, the gateway further parses the URL path. The gateway evaluates the applicable policies and default access mode to determine whether to forward the request to the backend business system.

5. **Audit log reporting**: The gateway records detailed access traces, including network connection logs and application\-layer access path logs, and continuously reports them to the Admin Console. This provides administrators with in\-depth access audit and traceability capabilities.

## Administrator configuration guide

### Required configurations

To help you quickly deploy and use proxy mode in your enterprise, we recommend that you configure it as follows:

1. [Deploy a proxy gateway and configure a gateway cluster](https://docs.byteplus.com/en/docs/sealsuite/access-proxy-gateway)

   Prepare server resources, add and install proxy gateway nodes, and create a cluster with associated nodes to provide a physical channel for subsequent traffic forwarding.

2. [Define a proxy application](https://docs.byteplus.com/en/docs/sealsuite/management-agent-mode-application-resources)

   Enter the specific network addresses of internal business systems that employees are allowed to access, such as code repositories and financial systems, in the Admin Console, and register them as proxy applications.

3. [Configure a proxy mode ACL policy](https://docs.byteplus.com/en/docs/sealsuite/configure-proxy-mode-acl-policy)  **(set gateway\-side allow rules)**

   Configure an access control list (ACL) based on identity or device attributes, and specify who can access which business ports.

4. [Configure a proxy mode traffic routing policy](https://docs.byteplus.com/en/docs/sealsuite/configuring-proxy-mode-traffic-diversion-strategy)  **(set client\-side traffic routing rules)**

   Deliver traffic routing policies to notify the SealSuite client to intercept access requests to target applications and send them into the proxy channel.

### Optional configurations

* [Configure a proxy mode fine-grained control policy](https://docs.byteplus.com/en/docs/sealsuite/configure-proxy-mode-fine-control-strategy)  **(set URL\-level web application access rules)**

   For published web applications, configure fine\-grained control policies if URL path\-level permission\-based access is required.

* [Configure a proxy mode client access policy](https://docs.byteplus.com/en/docs/sealsuite/configure-proxy-mode-client-access-policy)  **(set cluster access scope and manual cluster selection permissions)**

   Configure a client access policy to restrict the cluster scope for automatic selection if specified employees or devices must use proxy gateway clusters only in specific regions. The policy can also define whether employees may manually select a cluster in the client. When enabled, employees can switch among clusters they are allowed to connect to.

* [Configure proxy mode client rate limiting](https://docs.byteplus.com/en/docs/sealsuite/configure-proxy-mode-client-rate-limiting)  **(set bandwidth control rules)**

   In the advanced configuration of a proxy policy, you can enable client rate limiting to prevent end users from consuming excessive proxy gateway bandwidth. You can also configure different rate limits for employees or devices.
