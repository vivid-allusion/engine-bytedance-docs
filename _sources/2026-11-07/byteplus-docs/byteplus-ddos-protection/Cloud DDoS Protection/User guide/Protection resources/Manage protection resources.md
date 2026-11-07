---
title: "Manage protection resources"
product: "DDoS Protection"
product_code: "byteplus-ddos-protection"
source: "https://docs.byteplus.com/en/docs/byteplus-ddos-protection/Manage_protection_resources"
---

Once you have added your Elastic IP (EIP) resources to a Cloud DDoS Protection instance, you can perform various management tasks from the protected resources list. This guide provides step\-by\-step instructions for viewing resource status, modifying associated rule groups, manually unblocking blackholed IPs, binding resources to other cloud services, and removing EIPs from the protection instance.

<span id="3ad059a9"></span>
## Prerequisites

You have added the EIP to the Cloud DDoS Protection instance. Refer to [Add an EIP to your instance](https://docs.byteplus.com/docs/byteplus-ddos-protection/Add_an_EIP) for more details.

<span id="3a11b5c5"></span>
## View the protection resources list


1. Log in to the [Cloud DDoS Protection console](https://console.byteplus.com/ddos-protection/).

2. On the left side of the page, select **Cloud DDoS Protection \> Protected resources**.

3. At the top of the list, select the Cloud DDoS Protection instance that you want to view.

4. View information about the protection resource list.

   The following table describes each parameter in the protection resource list.

   
   |Configuration |Description |
   |---|---|
   |Protected EIPs (Added / Total)<br><br> |* Added EIPs: The number of EIPs currently associated with the instance.<br><br>* Total EIPs: The maximum number of EIPs that can be associated with the instance.<br><br>* For example, **`10/10`** indicates that this instance has already been associated with 10 EIPs and can be associated with up to 10 EIPs. |
   |Remaining unblocks today |* **Manual unblock**: After a resource is added to a Cloud DDoS Protection instance, if blackholing occurs, you can perform manual unblocking.<br><br>* **Auto unblock**: When a resource is added to a Cloud DDoS Protection instance, if the IP address is currently in a blackhole state, the system automatically unblocks it.<br><br>* For detailed information about the number of times unblocking occurs, refer to [DDoS blackholing strategy](https://docs.byteplus.com/docs/byteplus-ddos-protection/DDoS_blackholing_policy). |
   |Protected EIP |The IP address of the protected object. |
   |Protected resources |Types of protection resources.<br><br><br>* **Associated resources**: If the EIP is associated with a resource, its resource type and instance name are displayed.<br><br>* **Unassociated resources**: If a protected EIP is not associated with a resource, click **Go to associate** to open the [Elastic IP Console](https://console.byteplus.com/eip) and complete the association. |
   |Status |An EIP's protection status can be one of the following:<br><br><br>* **Normal**: Indicates that the current EIP is not under a DDoS attack.<br><br>* **Mitigating**: Indicates that the current EIP is under a DDoS attack and protection has been triggered. You can view the corresponding attack information on the traffic report page.<br><br>* **Blackholing**: Indicates that the current EIP is under a DDoS attack, and the attack volume has exceeded the protection bandwidth limit, triggering blackhole routing by the ISP. We recommend increasing your plan's protection bandwidth.<br><br>   * Hover over the icon following **Blackholing** to view the blackhole type and automatic unblocking time. |
   |Protection rule group |The protection rule groups associated with protection resources include:<br><br><br>* **Default rule group**: The default rule group for the DDoS protection engine system.<br><br>* **Expert rule group**: DDoS operations experts assist in customizing protection rules.<br><br>* **Custom rule group**: Protection rules customized and configured by the user.<br><br>* For detailed information about protection rule groups, refer to [Overview of protection policies](https://docs.byteplus.com/docs/byteplus-ddos-protection/Overview_of_protection_policies). |
   |Actions |* **Remove**: You can manually remove EIP resources from the instance. The removed EIP will no longer have the protection capabilities of the Cloud DDoS Protection instance.<br><br>* **Configure rules**: Go to the corresponding protection rule group to configure detailed rules or associate protection IP addresses.<br><br>* **Unblock**: When attack traffic targeting an EIP exceeds the protection bandwidth, the blackhole policy is triggered. You can manually unblock EIP resources that are in a blackhole state by clicking **Unblock** in the Actions column. |
   


<span id="b962133d"></span>
## Modify protection rule groups

When adding a protection resource, you can specify the rule group associated with the protected EIP. If rule group association settings are not configured, the system will automatically associate the protected EIP with the default rule group. You can also adjust the rule group associated with an EIP at any time in the protection resource list. To modify the associated rule group, follow these steps:


1. Log in to the [Cloud DDoS Protection console](https://console.byteplus.com/ddos-protection/).

2. On the left side of the page, select **Cloud DDoS Protection \> Protected resources**.

3. At the top of the list, select the Cloud DDoS Protection instance you want to view.

4. In the resource list, select the target EIP and modify its associated rule group.

   * **Edit individually**: Click the edit icon next to the rule group name, then select the rule group to associate with or create a new custom rule group.

      <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/facf94e63619460aade698c37c7840a2) </span>

   * **Batch edit**: After selecting multiple EIPs, click **Associate to rule group**, then choose a rule group to associate or create a custom rule group.

      <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/8cb6f15ca3d7457190729e20904e74d2) </span>

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">Note   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">After you switch rule groups, the new settings will apply to all selected EIPs.   </div>
   

5. Click **OK**.


<span id="1c0601e2"></span>
## Unblock from blackholes manually

If the attack on your protection resources is too large and exceeds the protection bandwidth, the ISP's blackhole mechanism is triggered. Normally, the blackhole is automatically lifted about two hours after the attack ends. However, the actual unblocking time will be dynamically adjusted based on the frequency of attacks: it may be shortened to 1 hour, or extended to 24 hours or longer. To restore services quickly, you can manually unblock the EIP in the DDoS console.


1. Log in to [Cloud DDoS Protection console](https://console.byteplus.com/ddos-protection/).

2. On the left side of the page, select **Cloud DDoS Protection \> Protected resources**.

3. At the top of the list, select the Cloud DDoS Protection instance you want to view.

4. In the resource list, select the target EIP that is in the blackhole, and click **Unblock** in the operation column.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">Caution   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Each instance has a limited number of manual unblocking attempts per day, and unused attempts cannot be carried over to the next day. For a detailed explanation of the number of unblocking attempts, refer to <a href="https://docs.byteplus.com/docs/byteplus-ddos-protection/DDoS_blackholing_policy#49e4bd31">Manual unblocking</a>   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If your instance frequently triggers blackhole filtering, it is recommended to increase your plan's protection bandwidth.   </div>
   


<span id="43d63673"></span>
## Bind protection resources

If the EIP you added has not yet been bound to the relevant resource type, you can navigate from the protection list page to the EIP console to bind it.


1. Log in to the [Cloud DDoS Protection console](https://console.byteplus.com/ddos-protection/).

2. On the left side of the page, select **Cloud DDoS Protection \> Protected resources**.

3. At the top of the list, select the Cloud DDoS Protection instance to view.

4. In the resource list, select the target EIP, and click **Go to associate**.

5. Associate relevant resource types in the Elastic IP console.


<span id="b270a7f7"></span>
## Remove protection resources

Multiple EIPs in an instance share its protection capabilities. To ensure sufficient protection bandwidth for critical EIPs, you can remove less important ones. After being removed, the EIP is no longer protected by the Cloud DDoS Protection instance.


1. Log in to the [Cloud DDoS Protection console](https://console.byteplus.com/ddos-protection/).

2. On the left side of the page, select **Cloud DDoS protection \> Protected resources**.

3. At the top of the list, select the Cloud DDoS Protection instance you want to view.

4. In the resource list, select the target EIP to remove.

   * **Remove individually**: Click **Remove** in the operation column.

      <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/7008a92d7388409d8eccd947295d74d0) </span>

   * **Batch remove**: Select multiple EIPs, then click **Remove selected**.

      <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/73a16a35fbd049c0be383853fc8ea129) </span>

5. Click **OK**.
