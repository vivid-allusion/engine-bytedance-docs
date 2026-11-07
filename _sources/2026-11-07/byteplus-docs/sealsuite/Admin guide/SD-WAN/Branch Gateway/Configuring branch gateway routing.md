---
title: "Configuring branch gateway routing"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/docs-configuring-branch-gateway-routing"
---

Configuring routing schemes for branch gateways helps you effectively route traffic to a particular destination, ensuring end\-to\-end Internet connectivity within the corporate network. In the Admin Portal, you can configure a dynamic routing scheme or a static routing scheme for a branch gateway according to your enterprise’s network requirements.

<span id="f02c7724"></span>
# Configuring a dynamic routing scheme

The dynamic routing scheme currently supports the Border Gateway Protocol (BGP) and the Open Shortest Path First (OSPF) protocol. You can choose to configure and enable the protocol that you deem fit.

<span id="b5e0c85b"></span>
## Configuring the BGP routing protocol for a branch gateway


1. Log in to the Admin Console.

2. In the left navigation bar, click **SD\-WAN** \> **Branch Gateway**.

3. In the branch gateway list, locate your target branch gateway card and click on it to enter the details page.

4. On the **Routing Configuration** tab of the details page, click **BGP protocol** and click **Edit** as shown in the below screenshot.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5cc8408a092a4b44802c6e91d5ddff87~tplv-goo7wpa0wc-image.image) </span>

5. In the configuration area that appears, fill in the provided configuration items and click **Save**.

   On the right of a configuration item, you can hover your mouse over the question mark icon to view specific description of the item.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ca229e0f824a43c495c6e70d0b81a5ac~tplv-goo7wpa0wc-image.image) </span>

6. Enable the BGP protocol by turning on the switch as shown in the below screenshot as needed.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/33adefc39174432daf4be024dc94d55a~tplv-goo7wpa0wc-image.image) </span>


<span id="d3abc643"></span>
## Configuring the OSPF protocol for a branch gateway


1. Log in to the Admin Console.

2. In the left navigation bar, click **SD\-WAN** \> **Branch Gateway**.

3. In the branch gateway list, locate your target branch gateway card and click on it to enter the details page.

4. On the **Routing Configuration** tab of the node details page, click **OSPF protocol** and click **Edit** as shown in the below screenshot.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2fe958df40f34c34a62e572e83279c8b~tplv-goo7wpa0wc-image.image) </span>

5. In the configuration area that appears, fill in the provided configuration items and click **Save**.

   On the right of a configuration item, you can hover your mouse over the question mark icon to view specific description of the item.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8ebbba765c054120820670e9a2499480~tplv-goo7wpa0wc-image.image) </span>

6. Enable the OSPF protocol by turning on the switch as shown in the below screenshot as needed.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/82c4fe7b2fb94b55868ce62ec3f8361d~tplv-goo7wpa0wc-image.image) </span>


<span id="4c482166"></span>
# Configuring a static routing scheme

If you have not configured any dynamic routing protocols, you need to configure a static routing scheme.


1. Log in to the Admin Console.

2. In the left navigation bar, click **SD\-WAN** \> **Branch Gateway**.

3. In the branch gateway list, locate your target branch gateway card and click on it to enter the details page.

4. On the **Routing Configuration** tab of the details page, locate the **Configuration Instructions** section and copy the value of the **Branch network segment** field.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/84d38de338414f17a2ff2e12af0ddc23~tplv-goo7wpa0wc-image.image) </span>

5. Your enterprise's IT administrator can use the copied network segment information to configure static routes on the switch associated with the specified branch gateway.

   After the configuration is completed, run a connectivity test to ensure the network functions properly.
