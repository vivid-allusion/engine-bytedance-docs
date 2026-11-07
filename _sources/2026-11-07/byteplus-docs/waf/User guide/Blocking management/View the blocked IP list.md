---
title: "View the blocked IP list"
product: "Web Application Firewall"
product_code: "waf"
source: "https://docs.byteplus.com/en/docs/waf/View_the_blocked_IP_list"
---

Under the protection of the Web Application Firewall, IPs that trigger protection rules will be restricted from access. For example, access IPs from blocked regions, or access IPs that have triggered rate limiting rules, etc. The WAF displays these restricted IPs in the Ban Management module, making it easy for you to view and manage them uniformly, and quickly implement response actions.

<span id="b947c8a2"></span>
## Requirements

An existing IP has triggered protection rules and access is restricted.

<span id="vchMG3Ia"></span>
## Steps


1. Log in to [Web Application Firewall Console](https://console.byteplus.com/waf/dashboard).

2. Select the instance region in the top menu bar.

3. Select **Ban Management** in the left navigation.

4. Select the domain name for which you want to view the blocked IPs.

5. (Optional) Filter the list of banned IPs by attack type and time range.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The custom time range supports viewing data for up to 1 day in the last 6 days.   </div>
   

6. View the banned IP list information.

   
   |Parameter |Note |
   |---|---|
   |Source IP of attack |* IPs restricted from access due to triggering WAF protection rules.<br><br>* Supports sorting by IP letters or numbers in ascending or descending order.<br><br>* Click before the IP`+`You can expand details to view the number of times the IP triggered the rules in detail. |
   |Number of interceptions |The total number of all types of protection rules triggered by this IP within the currently selected time range. |
   |IP status |The current ban status of the IP.<br><br><br>* Unprocessed: The IP has not yet been processed, and requests from this IP will be detected through WAF rules.<br><br>* Permanently allowlisted: The IP has been permanently added to the access allowlist, and requests from this IP will not be detected by WAF rules.<br><br>* Allowlisting canceled: The IP has been removed from the access allowlist, and requests from this IP will be detected through WAF rules.<br><br>* Permanently banned: The IP has been permanently added to the access blocklist, and requests from this IP are automatically intercepted.<br><br>* Ban canceled: The IP has been removed from the access blocklist, and requests from this IP will be detected through WAF rules. |
   |Status update time |The time of the last update on the IP ban status. Not displayed in the unprocessed state. |
   |Operation |* View logs: Click to jump to the log management page to view the attack log corresponding to the attack IP.<br><br>* Permanent allowlist: Click to add the IP to the access allowlist, and automatically generate a allowlist rule. You can go to **Protection policy \> Access control \> Access allowlist** to view rule details.<br><br>* Cancel allowlist: Click to remove the IP from the access allowlist, and the original allowlist rule will also be deleted.<br><br>* Permanent blocklist: Click to add the IP to the access blocklist, and automatically generate a blocklist rule. You can go to **Protection policy \> Access control \> Access blocklist** to view rule details.<br><br>* Cancel block: Click to remove the IP from the access blocklist, and the original blocklist rule will also be deleted. |
