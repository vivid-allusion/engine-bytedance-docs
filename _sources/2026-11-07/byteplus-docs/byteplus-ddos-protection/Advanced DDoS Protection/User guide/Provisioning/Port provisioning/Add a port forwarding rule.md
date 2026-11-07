---
title: "Add a port forwarding rule"
product: "DDoS Protection"
product_code: "byteplus-ddos-protection"
source: "https://docs.byteplus.com/en/docs/byteplus-ddos-protection/docs-adding-port-forwarding-rules"
---

To safeguard non\-website services, such as online gaming or e\-commerce activities, you can configure port forwarding rules. This involves replacing your service IP address with that of the Advanced DDoS Protection instance, thus network traffic can be redirected to its scrubbing center. This document provides a detailed guide on how to configure these port forwarding rules.

<span id="1a8e3aba"></span>
## Before you begin

Create an instance of BytePlus Advanced DDoS Protection.

<span id="0e6a169b"></span>
## Precautions

If the domain name of your origin server is non\-existent or unresolvable, the configuration may fail to take effect, or the requests to your origin server may not be forwarded properly.

<span id="5f3049de"></span>
## Procedure


1. Log in to the [BytePlus Advanced DDoS Protection Console](https://console.byteplus.com/ddos-protection/advance/instances).

2. In the left\-side navigation pane, choose **Advanced DDoS Protection** \> **Provisioning**.

3. On the **Port config** tab, select the instance you want to configure.

4. Click **Add forwarding rules**.

5. Choose **Add single rule** or **Add multiple rules in batches**, and configure the parameters.

   * **Add single rule**: Add a rule for one port at a time.

      
      |**Configuration** |**Description** |
      |---|---|
      |Forwarding protocol |The forwarding protocol supports both TCP and UDP. |
      |Forwarding port |* The port of Advanced DDoS Protection for forwarding requests. It should ideally be identical to the source port.<br><br>* Within a single Advanced DDoS Protection instance, each forwarding port must be unique per protocol. |
      |Origin server port |The port of the origin server. |
      |Origin server address |Specify the origin server's IP address or domain name. For load balancing purposes, multiple IP addresses or domain names can be entered simultaneously. However, do not mix the two types of addresses in a single entry.<br><br><br>* ✅Example 1. IP addresses.<br><br>   ```JSON```<br>```   1.1.1.1```<br>```   1.1.1.2```<br>```   1.1.1.3```<br>```   ```<br>   <br><br>* ✅Example 2. Domain names.<br><br>   ```JSON```<br>```   www.test1.com```<br>```   www.test2.com```<br>```   www.test3.com```<br>```   ```<br>   <br><br>* ❌Example 3. An IP address and a domain name.<br><br>   ```JSON```<br>```   1.1.1.1```<br>```   www.test2.com```<br>```   ```<br>    |
      

   * **Add multiple rules in batches**: Add multiple rules at once.

      * Enter multiple rules simultaneously, separating each rule by pressing the Enter key.

      * The rule format should be as follows: `protocol_forwarding port_origin server port_origin server address`. Use a space to separate the parameters.

      * Below is a valid example.

         ```JSON
         tcp 1234 1234 1.1.1.1
         udp 1234 1234 www.test.com www.test2.com
         ```
         

6. Click **Save**.

7. View the CIDR blocks, and add them all to the allowlist of the firewall, access control list (ACL), or any other security software installed on your origin server.

8. Replace your service's IP address with the one provided by the Advanced DDoS Protection instance.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">Tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If your service uses domain names to specify server addresses, you need to go to the corresponding DNS resolution provider, and modify the A record of the domain name to make the traffic redirect to the IP address of Advanced DDoS Protection.   </div>
   

<span id="1d2df977"></span>
## What to do next

After configuring the rules, confirm that they are effective. This step helps prevent service interruptions caused by an incorrect configuration.
