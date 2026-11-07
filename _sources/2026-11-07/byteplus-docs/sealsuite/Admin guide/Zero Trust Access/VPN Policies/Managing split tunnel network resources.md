---
title: "Managing split tunnel network resources"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/docs-managing-split-tunnel-network-resources_1"
---

After the VPN gateway is configured with split tunnel mode, you must configure network resources for the gateway. The network resources are categorized as global resources and single\-gateway resources. This article introduces the difference between these resources and their configuration instructions.

<span id="e6cd7e9f"></span>
# Introduction

Split tunnel mode is one of the network modes supported by SealSuite. For more information about the configuration instruction of VPN network mode, please refer to [Setting network mode for VPN gateways](https://docs.byteplus.com/docs/sealsuite/docs-setting-network-mode-for-vpn-gateways_1). After you have enabled split tunnel mode for the VPN gateway, you must configure network resources that can be accessed through split tunneling. This allows only the traffic intended for specific sites to be routed through the VPN tunnel when users connect to the VPN gateway. Network resources that can be accessed through split tunneling are categorized as **global resources** and **single\-gateway resources**. Specific descriptions of these resources are as follows:


* **Global resources**: These resources can be accessed through all VPN gateways. You can add global resources via the Custom Attributes function of VPN.

* **Single\-gateway resources**: These resources can only be accessed through specified VPN gateways. You can add single\-gateway resources on the detail page of the VPN gateway that you want to configure.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For a split tunnel VPN gateway, single\-gateway resources have higher priority than global resources. Therefore, when you configure <strong>single\-gateway</strong> <strong>resources</strong> for a split tunnel VPN gateway, the <strong>global resources</strong> will be invalidated within the same VPN gateway automatically.</div>


<span id="c1ea3254"></span>
# Configuring split tunnel **global resources**


1. Log in to the Admin Console.

2. From the left navigation bar, go to **Zero Trust Access** \> **VPN** \> **Settings**.

3. In the **Split Tunnel Mode** section of the page, click  **+ Add**.

4. In the pop\-up **Add** **Resources** page, configure **Resource** **Name** and **Resource Type**, and then click **Confirm**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5421a56d2b01423197933ce568f02bea~tplv-goo7wpa0wc-image.image) </span>

   In the **Resource** **Type** field, you can select **Domain** or **IP** **address**, or both. Specific configuration instructions are as follows:

   
   |**Configuration Item** |**Description** |
   |---|---|
   |**Domain** |After you have selected **Domain**, please fill in **Static** **domain** **name** **list** and **Dynamic** **domain** **name** **list** as needed.<br><br><br>* **Static domain name list**: If the IP address corresponding to the domain name is fixed and known, it is recommended that you configure static domain name. You must enter the domain name and the list of IP addresses corresponding to the domain name. When filling in the list, you must pay attention to the following notes:<br><br>   * **Domain**: You can fill in:<br><br>      * a single domain, such as www.example.com.<br><br>      * a wildcard domain, such as \*.example.com.<br><br><br>Please use commas or spaces between domains.<br><br><br>* **IP Address**: you can fill in:<br><br>   * a single IP address, such as 10.10.0.0.<br><br>   * an IP address in CIDR format, such as 10.10.0.0/24.<br><br><br>Please use commas or spaces between IP addresses.<br><br><br>* If you include port numbers in your domain, the port numbers will be automatically filtered.<br><br>* In the **Static** **domain** **name** **list** section, you can click **Add** to add static domains. In the upper right corner of this section, you can click **Delete** to remove static domains that are no longer needed.<br><br>* **Dynamic domain name list**: If the IP corresponding to the domain name is not fixed or unknown, it is recommended that you configure dynamic domain name. SealSuite will automatically parse the mapping relationship between domain names and IP addresses. When filling in the list, you must pay attention to the following notes:<br><br>   * **Domain**: You can fill in:<br><br>      * a single domain, such as www.example.com.<br><br>      * a wildcard domain, such as \*.example.com.<br><br><br>Please use commas or spaces between domains.<br><br><br>* The frequent changes of IP addresses corresponding to the domain name may risk impeding the SealSuite Client's function to access domains.<br><br>* If you include port numbers in your domain, the port numbers will be automatically filtered. |
   |**IP address** |After you have selected **IP address**, you can fill in the IP list as needed. You can enter:<br><br><br>* a single IP address, such as 10.10.0.0.<br><br>* an IP address in CIDR format, such as 10.10.0.0/24.<br><br><br>Please use commas or spaces between IP addresses. |
   

   After you have added resources, you can view them in the **Resources** list. You can edit or delete these resources via the **Action** column.


<span id="b9d0f7ea"></span>
# Configuring split tunnel single\-gateway resources


1. Log in to the Admin Console.

2. From the left navigation bar, go to **Zero Trust Access** \> **Gateway Config** \> **VPN Gateway**.

3. On the **VPN Gateway** page, locate your target VPN gateway and click it.

4. Under the **Network Mode** tab, click **Edit**.

5. Select **Split Tunnel Mode**, and toggle the **Enable single gateway routing under split tunnel mode** switch.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b404ff0c0f6e4c18a5d256e80eedbcab~tplv-goo7wpa0wc-image.image) </span>

6. In the **Enable single gateway routing under split tunnel mode** section, click  **+ Add**.

7. In the **Add** **Resources** pane, configure **Resource** **Name** and **Resource Type**, and then click **Confirm**.

   In the **Resource** **Type** field, you can select **Domain** or **IP** **address**, or both. Specific configuration instructions are as follows:

   
   |**Configuration Item** |**Description** |
   |---|---|
   |**Domain** |After you have selected **Domain**, please fill in **Static** **domain** **name** **list** and **Dynamic** **domain** **name** **list** as needed.<br><br><br>* **Static domain name list**: If the IP address corresponding to the domain name is fixed and known, it is recommended that you configure static domain name. You must enter the domain name and the list of IP addresses corresponding to the domain name. When filling in the list, you must pay attention to the following notes:<br><br>   * **Domain**: You can fill in:<br><br>      * a single domain, such as www.example.com.<br><br>      * a wildcard domain, such as \*.example.com.<br><br><br>Please use commas or spaces between domains.<br><br><br>* **IP Address**: you can fill in:<br><br>   * a single IP address, such as 10.10.0.0.<br><br>   * an IP address in CIDR format, such as 10.10.0.0/24.<br><br><br>Please use commas or spaces between IP addresses.<br><br><br>* If you include port numbers in your domain, the port numbers will be automatically filtered.<br><br>* In the **Static** **domain** **name** **list** section, you can click **Add** to add static domains. In the upper right corner of this section, you can click **Delete** to remove static domains that are no longer needed.<br><br>* **Dynamic domain name list**: If the IP corresponding to the domain name is not fixed or unknown, it is recommended that you configure dynamic domain name. SealSuite will automatically parse the mapping relationship between domain names and IP addresses. When filling in the list, you must pay attention to the following notes:<br><br>   * **Domain**: You can fill in:<br><br>      * a single domain, such as www.example.com.<br><br>      * a wildcard domain, such as \*.example.com.<br><br><br>Please use commas or spaces between domains.<br><br><br>* The frequent changes of IP addresses corresponding to the domain name may risk impeding the SealSuite Client's function to access domains.<br><br>* If you include port numbers in your domain, the port numbers will be automatically filtered. |
   |**IP address** |After you have selected **IP address**, you can fill in the IP list as needed. You can enter:<br><br><br>* a single IP address, such as 10.10.0.0.<br><br>* an IP address in CIDR format, such as 10.10.0.0/24.<br><br><br>Please use commas or spaces between IP addresses. |
   

   After you have added resources, you can view them in the **Resources** list. You can edit or delete these resources via the **Action** column.


<span id="7a3cd796"></span>
# Related operations

You can use **Copy** resource and **Import** resource functions on both global resource configuration page and single\-gateway resource configuration page. By leveraging these functions, you can copy existing resources or create new resources. Specific instructions are as follows:


1. In the Resources list, select the check box of at least one resource.

2. Click **Copy**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/036e3f9a21a047dd84dc3feea8d345c5~tplv-goo7wpa0wc-image.image) </span>

3. Click **Import**.

4. In the **JSON** **import** dialog box, paste the copied data.

   You can refer to the notes on the dialog box to customize the resources formatted in JSON.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cd68bd005bb048e9b3ffacae3b84f670~tplv-goo7wpa0wc-image.image) </span>

5. Click **Analyze**. After you have confirmed that there is no problem with the parsing result, click **Confirm**.
