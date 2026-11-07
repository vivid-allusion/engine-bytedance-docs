---
title: "Viewing basic information and performance statistics of a branch gateway"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/docs-e51gqmg9ny"
---

After adding a branch gateway, you can view the basic information of the gateway in the branch gateway list. In addition, the branch gateway component will dynamically monitor the operation of the corresponding server and transmit the monitoring data to the SealSuite Admin Portal. This article introduces how to view basic information of branch gateways and the relevant server performance statistics.

<span id="64990885"></span>
## Viewing basic information of a branch gateway


1. Log in to the Admin Console.

2. In the left navigation bar, click **SD\-WAN** \> **Branch Gateway**.

3. On the **Branch Gateway** page, click on a branch gateway card to view its basic information.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ec2646e59ed84051977e868c7513be21~tplv-goo7wpa0wc-image.image) </span>

   * In the **General** tab, you can view basic information including the branch gateway's name and type, the enabling status of the source network address translation feature, the branch network segment, the bandwidth speed limit, the version of the component, and more. In addition, the basic information of a software\-based branch gateway contains a unique information item named **Server Backfill Information**, while the basic information of a hardware\-based branch gateway consists of an information item named **Device Provisioning Info**.

   * If a new version of the branch gateway component is available for use, the **Update now** button will appear on the right side of the current version number under the **Component version** field. Besides, you can view the update history of the current component by clicking **View** under the **component update record** field.

   * By clicking **Go to Configuration** under the **Status Monitor** field, you can view the operational status of the branch gateway on the **Component Management** page under the **Integration** module.


<span id="bcc2ea03"></span>
## Viewing the basic information and performance statistics of a branch gateway component


1. Log in to the Admin Console.

2. In the left navigation bar, click **Settings** \> **Integration** \> **Components**.

3. In the upper right corner of the **Component** page, click **Branch Site**.

4. In the component list, click on your target branch gateway server card to view its basic information and performance statistics.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1a10ddb9c6c34239bbf8d699f5b76c1b~tplv-goo7wpa0wc-image.image) </span>

   * In the **General** tab, you can view basic information including the server's name, type, and operational status, as well as the branch network segment, the component ID, the version of the component, and more. If a new version of the branch gateway component is available for use, the **Update now** button will appear on the right side of the current version number under the **Component version** field. Besides, you can view the update history of the current component by clicking **View** under the **component update record** field.

   * In the **Performance Monitoring** tab, you can view server performance metrics such as **Memory Usage**, **CPU Usage**, **Disk Usage**, **Disk Read/Write IOPS**, **Disk Read/Write BPS**, and **Network Throughput**.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">You can only view the performance statistics of the current server on condition that the server is running smoothly.      </div>
