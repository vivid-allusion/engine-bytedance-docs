---
title: "Create and manage domain groups"
product: "Web Application Firewall"
product_code: "waf"
source: "https://docs.byteplus.com/en/docs/waf/Create_and_manage_domain_groups"
---

A domain group refers to a collection of domains that can be used to batch associate corresponding blocklists or allowlists, improving the configuration and maintenance efficiency of access control policies. You can select the domains that have already been connected to the WAF and add them to the created domain group.

<span id="de040dd0"></span>
## Requirements

You have connected the website that needs to be protected to the WAF instance. For more details, see [Comparison of website association methods](https://docs.byteplus.com/en/docs/6511/935148).

<span id="c903fa2b"></span>
## Create a domain name group


1. Log in to [the Web Application Firewall Console](https://console.byteplus.com/waf/dashboard).

2. Select the instance region in the top menu bar.

3. In the left navigation, select **System Management \> Domain Group Management**.

4. Click **Create Domain Group**.

5. Configure the parameters related to the domain name group.

   
   |Parameter |Description |Example |
   |---|---|---|
   |Name |The name of the domain group.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Start with a letter or digit.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Letters, digits, Chinese characters, dot ".", underscore "_", and hyphen "\-" are allowed.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The length must be between 1 and 128 characters.</div><br> |Allowlist domain name_1 |
   |Description |Enter relevant remark information. |Allow all access for the corresponding domain name. |
   |Domain name |Select the domains you wish to add from the connected domain name list. |Select the following domains:<br><br><br>* test.com<br><br>* blog.test.com |
   

6. Click **OK**.


<span id="ecd42442"></span>
## View the details of the domain name group

After the domain name group is added, you can check the related information in the domain name group list to confirm whether the addition result meets expectations.


1. Log in to [Web Application Firewall Console](https://console.byteplus.com/waf/region:waf+cn-gaofang-nt3/purchase-guide).

2. Select the region of your instance in the top bar.

3. Select **System Management \> Domain Name Group Management** in the left navigation.

4. View the related information of the IP address group list, including domain name group name, domain name information, associated rules, update time, etc.

   
   |Parameter |Description |
   |---|---|
   |Name |The corresponding name entered when creating the IP address group, editable. |
   |Description |Remarks added when adding the domain name group. |
   |Domain name |View the domains included in this domain group; clicking the corresponding domain will redirect to the website settings list to view the access information for that domain. |
   |Related rules |* If you select the associated domain name group when creating a blocklist or allowlist, you can view the names of the rules associated with the domain name group in this list.<br><br>* Clicking on the number will display the names of the rules associated with that domain name group, and clicking on the corresponding rule name will show the rule details. |
   |Update Time |The last update time of the domain group. |
   |Operation |Supports viewing, editing, or deleting domain name group information. |
   


<span id="c49d1a73"></span>
## Other operations


* View domain name group details: Select the domain name group you want to edit, click **Details** in the operation column to view all domain names contained in that domain name group and the associated rules.

&nbsp;

* Edit domain name group: Select the domain name group you want to edit, click **Edit** in the operation column to modify the domain name group name and related domain names.

* Delete IP address group: select the IP address group to delete and click **delete** in the operation column to remove the corresponding domain group.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">It is recommended to confirm that the corresponding rules do not need to be associated with the domain group before deletion. Once the domain group is deleted, its associated rules will also remove the references to that domain group.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the protection rule only associates with the current domain group, the corresponding rule will be deleted directly.   </div>
