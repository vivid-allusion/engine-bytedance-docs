---
title: "Create and manage IP address groups"
product: "Web Application Firewall"
product_code: "waf"
source: "https://docs.byteplus.com/en/docs/waf/Create_and_manage_IP_address_groups"
---

An IP address group refers to a collection of IP addresses that can be used for batch association with corresponding access allowlist or blocklist, improving the configuration and maintenance efficiency of access control policies. You can add IP address groups by manually entering them in the console or uploading files. Once the IP address group is successfully uploaded, you can view and edit it at any time in the IP address group management list.

<span id="6fc6cff3"></span>
## Notes


* A maximum of 100 IP address groups are supported under each region.

* The number of IP addresses that can be added to an IP address group varies under different versions of instances.

   
   |Instance version |The number of IPs supported by each address group |
   |---|---|
   |Basic edition |10 items |
   |Premium edition |100 items |
   |Enterprise edition |500 items |
   |Flagship edition |1000 items |
   


<span id="41c212a6"></span>
## Create an IP address group


1. Log in to [Web Application Firewall Console](https://console.byteplus.com/waf/region:waf+cn-beijing/overview?).

2. In the top menu bar, select the region of your instance.

3. Select **System Management \> IP address group Management** in the left navigation.

4. Click **New IP address group**.

5. Configure the parameters related to the IP address group.

   
   |Parameter |Description |Example |
   |---|---|---|
   |Name |Name of the IP address group.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Start with a letter or digit.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Allow letters, digits, Chinese characters, the dot “.”, underscore “_”, and hyphen “\-”.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The length must be between 1 and 128 characters.</div><br> |Allowlist IP_1 |
   |Adding method |* Manually add: Enter the IP address or address segment and confirm.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Support IPv4 and IPv6 formats.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Please use the Enter key to separate multiple address inputs.   </div><br>   <br><br>* File upload:<br><br>   1. Download the template provided by the platform.<br><br>   2. Input IP information in the template file.<br><br>   3. Upload the completed template file.<br><br>   4. Click **Next: View Addresses** to confirm the imported IP information.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Different versions of instances support a different number of IP addresses that can be added to the IP address group.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Up to 5 files can be imported, and multiple files can have a cumulative maximum size of 8 MB.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Duplicate IP addresses added will be overwritten.   </div><br>    |Manually add: 1.1.1.1 |
   

6. Click **OK**.


<span id="0420428f"></span>
## View the details of the IP address group

After adding the IP address group, you can check the relevant information in the IP address group list. This helps you confirm whether the IPs in the IP address group meet expectations.


1. Log in to [Web Application Firewall Console](https://console.byteplus.com/waf/region:waf+cn-gaofang-nt3/purchase-guide).

2. Select the region of your instance in the top bar.

3. Select **System Management \> IP address group Management** in the left navigation.

4. View relevant information in the IP address group list, including the IP address group name, IP address, associated rules, and update time.

   
   |Parameter |Note |
   |---|---|
   |Name |Corresponding name entered when creating the IP address group, editable. |
   |IP address |* View the IP addresses contained in this IP address group. Click the corresponding number to view the details of the IP addresses in this group.<br><br>* Supports searching by IP address or IP segment when viewing details. |
   |Related rules |* If you selected the associated IP address group when creating the Blocklist or Allowlist, you can view the rule names associated with the IP address group in this list.<br><br>* Clicking on the number allows you to view the Details of the rules associated with the IP address group, including the rule ID and associated domain/domain group information. Clicking on the rule ID allows you to view the rule details. |
   |Update Time. |Last updated time of the IP address group. |
   |Operation |Supports editing, deleting, or downloading IP address group information. |
   


<span id="acb235fb"></span>
## Other operations


* Edit IP address group: Select the IP address group to be edited, click **Edit** in the operation column to modify the group name and related IP addresses.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you modify by uploading a file, the original IP addresses will be overwritten after uploading and recognizing the IP addresses.   </div>
   

* Delete IP address group: Select the address group to be deleted, and perform the operation by single deletion or batch deletion.

   * Single deletion: Click **Delete** in the operation column corresponding to the address group.

   * Batch deletion: After selecting multiple address groups, click **Batch delete** at the bottom of the list.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">It is recommended to confirm that the corresponding rules do not need to be associated with the address group before deleting. Because after the address group is deleted, the associated rules will be updated to delete the reference to that address group.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the protection rules only associate with the current address group, the corresponding rules will be deleted directly.   </div>
   

* Download IP address group: If you need to view the details of the IP addresses under the current address group, you can download the address group file to your local machine; the exported file format is `.xlsx`.
