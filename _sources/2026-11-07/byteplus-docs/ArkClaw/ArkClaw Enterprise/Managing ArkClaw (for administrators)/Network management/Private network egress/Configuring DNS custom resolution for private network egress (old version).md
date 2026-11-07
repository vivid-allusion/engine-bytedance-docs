---
title: "Configuring DNS custom resolution for private network egress (old version)"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/Configuring-the-private-egress-domain-resolution-Old-version"
---

After private network egress is enabled, ArkClaw forwards DNS queries within the Space to BytePlus DNS servers (`100.96.0.2` and `100.96.0.3`) by default. This topic describes the configuration to forward DNS queries from the Space to a specified external DNS server.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">This topic provides the instructions for the old version of the network configuration interface. We recommend upgrading to the new version for more DNS resolution capabilities. For upgrade instructions, see <a href="https://docs.byteplus.com/en/docs/ArkClaw/Configuring-the-private-egress-domain-resolution-New-version?lang=en">Configuring DNS custom resolution for private network egress (new version)</a>.</div>


<span id="tV8TyI51"></span>
## **Before you begin**

The private network egress is enabled. For procedure, see [Disabling or enabling private network egress](https://docs.byteplus.com/en/docs/ArkClaw/Enabling-or-disabling-the-private-egress-Old-version).

<span id="uqMjqnih"></span>
## Procedure


1. Log in to the[ ArkClaw Enterprise console](https://console.byteplus.com/arkclaw/enterprise).

2. In the left navigation pane, select "Resource Configuration \> Network Configuration".

3. In the private network egress detail section, click the edit icon to the right of "DNS resolution configuration". Configure the private network information based on the table below.

    &nbsp;

   
   |Configuration item |Description |
   |---|---|
   |**DNS resolution configuration** ||
   |Configure DNS resolution |Specify whether to enable DNS resolution.<br><br><br>* If disabled, ArkClaw forwards DNS queries from the Space to BytePlus DNS servers (`100.96.0.2` and `100.96.0.3`).<br><br>* If enabled, ArkClaw forwards DNS queries from the Space to the specified external DNS server. This is suitable for resolving enterprise internal domains (e.g., gitlab.internal and jenkins.corp). |
   |External DNS system IP address and port |Specify the IP address and port of the external DNS server.<br><br><br>* Currently only IPv4 addresses are supported. Up to 10 external DNS server addresses are allowed.<br><br>* The DNS server address cannot be set to system\-reserved addresses: `100.96.0.2` and `100.96.0.3`.<br><br>* "Port" is optional. It defaults to 53 if left blank. |
   |Forwarding domain |Specify the domain that needs to be resolved by an external DNS server, and press Enter to confirm. Domains not specified will still be resolved by BytePlus DNS server.<br><br><br>* Batch pasting of multiple domains is supported. Separate the domains with commas (,).<br><br>* A maximum of 500 domains can be added for forwarding.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">If cross\-border public acceleration is enabled, we recommend that the forwarding domains do not overlap with the acceleration domains. If a domain is configured for both forwarding and public acceleration, requests for that domain will be prioritized to go through the acceleration path. <a href="https://docs.byteplus.com/en/docs/ArkClaw/Configuring-cross-border-acceleration-policy-new-version">Learn more</a></div><br> |
   

4. Click "OK" to complete the action.


<span id="g4cHGze8"></span>
## Verify

After configuration, follow these steps to verify DNS resolution via external DNS.


1. Log in to the Claw instance. Open two terminal windows.

2. Terminal 1 (packet capture):​ Run the following command to capture DNS requests.

   ```JSON
   tcpdump -i any port 53 -n
   ```
   

   The terminal will output capture results continuously. Press **Ctrl+C** to stop after verification.

3. Terminal 2 (verification):​ Run the following command to send an HTTP HEAD request. This triggers DNS resolution.

   ```Bash
   curl -I <domain to verify, e.g., example.com>
   ```
   

   Replace <domain to verify, e.g., example.com\> with the domain name actually configured.

4. **Check if resolution succeeds**

   * If Terminal 2 returns any HTTP response header (e.g., HTTP/1.1 200 OK or HTTP/1.1 404 Not Found), resolution succeeded. An IP is obtained and a connection is established.

   * If Terminal 2 returns an resolution error, like Could not resolve host. Check the following: whether the domain is correct, whether domain resolution is enabled, and whether the private network egress security group allows DNS (UDP port 53).

5. **Check if external DNS is used**

   * If the destination IP of DNS requests in Terminal 1 is **the external DNS server address you configured**, traffic is resolved via external DNS. Configuration is effective.

      Example output (external DNS set to 10.0.0.8):

      ```JSON
      10:00:00.000000 IP 192.168.1.10.54321 > 10.0.0.8.53: 12345+ A? example.com. (30)
      ```
      

   * If the destination IP of DNS requests in Terminal 1 is 100.96.0.2 or 100.96.0.3, traffic is resolved via BytePlus DNS. Check whether the "Configure DNS resolution" toggle is enabled.
