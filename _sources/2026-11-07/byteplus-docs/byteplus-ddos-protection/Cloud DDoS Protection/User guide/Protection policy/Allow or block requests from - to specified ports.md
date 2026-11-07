---
title: "Allow or block requests from/to specified ports"
product: "DDoS Protection"
product_code: "byteplus-ddos-protection"
source: "https://docs.byteplus.com/en/docs/byteplus-ddos-protection/Allow_or_block_requests_from_or_to_specified_ports"
---

Port filtering helps you manage network access by setting rules to allow or block traffic on specific ports. This feature enhances security by defending against attacks and reducing your service's attack surface. To block malicious traffic from known attack ports or limit exposure by only allowing access to necessary service ports, you can follow this guide to configure port allowlists and blocklists.

<span id="bd9a74b1"></span>
## Applicable scenarios


* **Protecting specific ports**: When you identify that attack traffic primarily originates from one or more ports, you can block those ports to stop the attack traffic.

* **Reduce port exposure**: For services that only use fixed ports (such as TCP), unnecessary ports can be blocked to effectively reduce the attack surface.


<span id="3261a5b5"></span>
## Important notes


* **How protection is triggered**: When an attack is detected, Cloud DDoS Protection blocks traffic on the ports specified in your blocklist rules.

* **Port rule restrictions**:

   * Port filtering rules support IPv4 addresses. IPv6 addresses are not yet supported.

   * Each rule group can configure up to 16 port rules, including allowlists and blocklists.

   * Each rule must have a unique priority.

* **Policy priority**: If a request to a blocked port comes from an IP address in an allowlist, that request will be allowed.


<span id="4e9093e3"></span>
## Configure port allowlists


1. Log in to the [Cloud DDoS Protection Console](https://console.byteplus.com/ddos-protection/).

2. In the left navigation pane, select  **Cloud DDoS Protection** ** \> ** **Protection policy**.

3. From the protection policy list, find your target rule group. To open its settings, click the rule group's name or click **Set rules** in the **Actions** column.

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/2d4128bdd43940f5ab94402e70d5f3a0) </span>


&nbsp;


&nbsp;

4. Select **Port filtering**, then click **Add port filter**.

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/a93935540f994b93a0321342068bfb93) </span>

5. Configure port allowlist parameters.

   * **Action**: Allow

   * **Protocol type**: Supported protocols: **All**, **TCP**, **UDP**, or **ICMP**

   * **Port type**:

      * **Destination port**: Allow access to specific destination ports.

      * **Source port**: Allow access from specific source ports.

   * **Priority**: Set the rule's execution priority; P0 represents the highest priority.

      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">Caution      </div>
      

      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">Priorities must be unique across all allowlist and blocklist rules.      </div>
      

6. Click **OK**.


<span id="3b1553bf"></span>
## Configure port blocklists


1. Log in to the [Cloud DDoS Protection Console](https://console.byteplus.com/ddos-protection/).

2. In the left navigation pane, select  **Cloud DDoS Protection** ** \> ** **Protection policy**.

3. From the protection policy list, find your target rule group. To open its settings, click the rule group's name or click **Set rules** in the **Actions** column.

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/2d4128bdd43940f5ab94402e70d5f3a0) </span>


&nbsp;


&nbsp;

4. Select **Port filtering**, then click **Add port filter**.

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/a93935540f994b93a0321342068bfb93) </span>

5. Configure port blocklist parameters.

   * **Action**: **Block**

      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">\*Caution      </div>
      

      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">Cloud DDoS Protection will only block requests to specified ports when detecting an attack.      </div>
      

   * **Protocol type**: Supported protocols: **All**, **TCP**, **UDP**, or **ICMP**

   * **Port type**:

      * **Destination port**: Block access to specific destination ports.

      * **Source port**: Block access from specific source ports.

   * **Priority**: Set the rule's execution priority; P0 represents the highest priority.

      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">Caution      </div>
      

      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">Priorities must be unique across all allowlist and blocklist rules.      </div>
      

6. Click **OK**.


<span id="7416be88"></span>
## Related operations


* **Edit**: You can edit existing rules at any time.

* **Delete**: You can delete a single rule or multiple rules in bulk.

* **Adjust priority**: You can adjust rule priority by dragging and dropping. The priorities of other rules are automatically updated accordingly.


&nbsp;

&nbsp;
