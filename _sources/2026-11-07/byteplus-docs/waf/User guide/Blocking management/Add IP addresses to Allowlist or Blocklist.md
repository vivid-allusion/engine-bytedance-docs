---
title: "Add IP addresses to Allowlist or Blocklist"
product: "Web Application Firewall"
product_code: "waf"
source: "https://docs.byteplus.com/en/docs/waf/Add_IP_addresses_to_Allowlist_or_Blocklist"
---

The restricted IP is in an unprocessed state by default, and subsequent access requests will still be detected by WAF rules. You can add an IP to an Allowlist or Blocklist to control subsequent access to the corresponding IP.

<span id="b947c8a2"></span>
## Requirements

An existing IP has triggered protection rules and access is restricted.

<span id="577a60e1"></span>
## Add IP addresses to the a**llowlist**

To avoid disruptions to normal business, you may need to quickly restore normal IP access if regular user access is intercepted due to strict protection policies. In this scenario, you can set the attack IP as **permanently whitelisted**.

<span id="FZaP4QDA"></span>
### Steps


1. Log in to [Web Application Firewall Console](https://console.byteplus.com/waf/dashboard).

2. Select the instance region in the top menu bar.

3. Select **Ban Management** in the left navigation.

4. Select the domain name for which you want to view banned IPs.

5. (Optional) Filter the list of banned IPs by attack type and time range.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The custom time range supports viewing data for up to 1 day in the last 6 days.   </div>
   

6. Select the destination IP and whiteout.

   * Single whiteout: Click the **Permanent Whiteout** in the action column and confirm.

   * Batch whiteout: After checking multiple IPs, click **Batch White** and confirm.


<span id="c2ecb7fe"></span>
### Operation result

After the operation is successful, the **Allowlist** will automatically generate one or more allowlist rules, and the target IP's access behavior to the current domain name will no longer be affected by all WAF detection rules.


* You can go to **Protection Policy \> Access Control \> Allowlist** to view the rule details. The automatically generated allowlist rules do not support editing.

* Once the target IP is removed from the allowlist, the corresponding rules in the allowlist will be automatically deleted.


<span id="d2fc1101"></span>
## Add IP addresses to the blocklist

If you need to directly intercept all subsequent accesses from the attack IP, without matching other detection rules, you can set the attack IP to **Permanent Ban**.

<span id="af5ae5e5"></span>
### Steps


1. Log in to [Web Application Firewall Console](https://console.byteplus.com/waf/dashboard).

2. Select the instance region in the top menu bar.

3. Select **Block Management** in the left navigation.

4. Select the domain name for which you want to view the blocked IPs.

5. (Optional) Filter the blocked IP list by attack type and time range.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The custom time range supports viewing data for up to 1 day in the last 6 days.   </div>
   

6. Select the destination IP and block.

   * Click **Permanent Block** in the action column and confirm.

   * Check multiple IPs and click **Batch Block**, then confirm.


<span id="81297ef6"></span>
### Operation result

After the operation is successful, accessing the allowlist will automatically generate one or more blocklist rules, and the target IP's access to the current domain name will be directly intercepted.


* You can go to **Protection Policy \> Access Control \> Blocklist** to view the rule details. The automatically generated blocklist rules do not support editing.

* After the target IP is unwhitened, the rules corresponding to the **Blocklist** will be automatically deleted.
