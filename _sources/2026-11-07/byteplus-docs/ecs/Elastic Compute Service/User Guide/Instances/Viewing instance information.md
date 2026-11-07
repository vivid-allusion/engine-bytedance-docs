---
title: "Viewing instance information"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Instance-overview-1"
---

<span id=".5Zyo5a6e5L6L5qaC6KeI6aG15p-l55yL"></span>
## Viewing on the instance overview page

On the instance overview page, you can view the distribution of resources in all regions, including the number of instances in different states, the number of volumes and the number of custom images in each region. You can also view the security scores of the instances, common functions, help documentation, best practices, and updates and announcements.


1. Log on to the [ECS console](https://console.byteplus.com/ecs/instance). 

2. In the left\-side navigation pane, click "Overview" to view the instance distribution.

3. View instances by region in the resource list. For example, click a specific number in the "Running" column of a region that you want to view. Then, you are redirected to the Instances page to view all instances in the **Running** state in that region.

4. If you want to view instance details on the Instances page, refer to [Viewing on the Instances page](https://docs.byteplus.com/en/docs/ecs/Instance-overview-1#.5Zyo5a6e5L6L5YiX6KGo6aG15p-l55yL).


<span id=".5Zyo5a6e5L6L5YiX6KGo6aG15p-l55yL"></span>
## Viewing on the Instances page

After you purchase an instance, follow these steps to configure filter criteria and locate the purchased instance. Once the target instance is found, you can view its configuration information. The information includes instance name/ID, state, instance type, image, public/private IP addresses, billing method, and creation/due time.


1. Log on to the [ECS console](https://console.byteplus.com/ecs/instance). 

2. In the left\-side navigation pane, select "Instances & Images \> Instances".

3. In the top menu bar, select the project and region of the target instance.

4. Customize a filter criteria to find the target instance.

   Click the filter box at the top of the page. Enter a filter criteria to find the target instance. 

5. View configuration information of the target instance.

   * **Method 1: Viewing on the Instances page**

      When you view the configuration information of the target instance on the Instances page, the system usually displays the default options. You can [specify the items displayed on the Instances page](https://docs.byteplus.com/en/docs/ecs/Custom-instance-list#.6Ieq5a6a5LmJ5a6e5L6L5YiX6KGo6aG1).

   * **Method 2: Viewing on the instance details page**

      On the Instances page, click the name of the target instance to go to the details page. Click a tab and you can view the corresponding configuration information.


<span id=".5p-l55yL56S65L6L"></span>
## Examples


<Tabs>
<Tab zoneid="MCbTVIRj3w" title="View Elastic IP (EIP)">
<TabTitle>View Elastic IP (EIP)</TabTitle>

* On the Instances page:

   * Copy EIP address: When you hover the cursor over the EIP address of an instance, the<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_43072f6cf03b454be69d7443294c72f8.png) </span>icon appears. You can click the icon to copy the address.

   * View maximum bandwidth: Click on the EIP address. On the EIP details page that appears, you can view the maximum bandwidth.

* On the instance details page:

   * Copy EIP address: Copy in the "Network Interface" section under the "Overview" tab of the instance.

   * View maximum bandwidth: In the "Elastic IP Address (EIP)" section under the "Overview" tab of the instance, click the ID of the EIP. On the EIP details page that appears, you can view the maximum bandwidth.


</Tab>
<Tab zoneid="gFshNrRv2U" title="View operating system version">
<TabTitle>View operating system version</TabTitle>

* On the Instances page:

   When you hover the cursor over an icon in the "Image" column of the target instance, the system automatically displays the operating system type and version.

* On the instance details page:

   View in the "Image" section under the "Overview" tab of the instance.


</Tab>
</Tabs>


<span id=".55u45YWz5paH5qGj"></span>
## Related document

[DescribeInstances - Query instances](https://docs.byteplus.com/en/docs/ecs/DescribeInstances)

<span id=".5bi46KeB6Zeu6aKY"></span>
## FAQs


* [How do I view the IP address and Internet bandwidth of an instance?](https://docs.byteplus.com/en/docs/ecs/Instance-overview-1#.5p-l55yL56S65L6L)

* [How do I view the operating system of an instance?](https://docs.byteplus.com/en/docs/ecs/Instance-overview-1#.5p-l55yL56S65L6L)

* [How to view the hostname of an instance?](https://docs.byteplus.com/en/docs/ecs/Instance-FAQs#.5aaC5L2V5p-l55yL5a6e5L6L55qE5Li75py65ZCN77yf)

* [How to view the CPU model of an instance?](https://docs.byteplus.com/en/docs/ecs/Instance-FAQs#.5aaC5L2V5p-l55yL5a6e5L6L55qEY3B15Z6L5Y-377yf)

* [How to view the runtime duration of a program in an instance?](https://docs.byteplus.com/en/docs/ecs/Instance-FAQs#.5aaC5L2V5p-l55yL5a6e5L6L5Lit56iL5bqP6L-Q6KGM5pe26ZW_77yf)

* [How to view which ports are opened on an ECS instance?](https://docs.byteplus.com/en/docs/ecs/Network-FAQs#.5aaC5L2V5p-l55yLZWNz5a6e5L6L5pS-6YCa5LqG5ZOq5Lqb56uv5Y-j77yf)

* [How to view information of deleted instances?](https://docs.byteplus.com/en/docs/ecs/Instance-FAQs#.5aaC5L2V5p-l55yL5bey5Yig6Zmk5a6e5L6L55qE5L-h5oGv77yf)
