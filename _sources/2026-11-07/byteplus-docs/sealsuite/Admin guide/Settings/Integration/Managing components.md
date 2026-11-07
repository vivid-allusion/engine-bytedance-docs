---
title: "Managing components"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/docs-managing-components"
---

When you deploy VPN gateways, RADIUS gateways, application gateways, and branch gateways within SealSuite, you need to deploy the corresponding SealSuite components on your local server. For example, when adding VPN gateways, it is necessary to deploy VPN components within the server. While implementing its own functions, the component can also monitor the server's operating status and upload status data to the SealSuite Admin Portal. This article introduces how to view component information within each gateway and the server monitoring data uploaded by the components.

<span id="b170b0f3"></span>
# Procedure


1. Log in to the Admin Console.

2. In the left navigation bar, click **Settings** \> **Integration** ＞ **Component**.

3. On the **Component** page, view component information for **VPN**, **RADIU**, and **Branch Site**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0117364375024721846b50c7d5ee0e01~tplv-goo7wpa0wc-image.image) </span>

4. Select the specified component and view the following information.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">In the upper right corner of the page, click <strong>Go to the gateway</strong> to redirect to the details page within the corresponding functional module.   </div>
   

   * On the **General** tab:

      * Basic information such as the name, type, status, IP, and port of the component.

      * **Component ID** and **Component Secret**: Authorization credentials for the component. Generally used to verify components within the corresponding server.

      * **Component version**: The version information of the current component. If a new version exists, the **Update now** button will be displayed on the right of the version number.

      * **Component update record**: Click **View** to view the historical update records of components.

   * On the **Performance Monitoring** tab:

      * It includes monitoring data such as memory usage, CPU usage, disk usage, and network throughput.

      * You can configure Ping detection and HTTP detection manually in the **Intranet Connectivity** area to test the server's internal network connectivity.

      * You can configure Ping detection and HTTP detection manually in the **Internet connectivity** area to test the server's external network connectivity.
