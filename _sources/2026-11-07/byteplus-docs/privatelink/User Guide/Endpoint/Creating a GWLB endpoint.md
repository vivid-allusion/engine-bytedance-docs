---
title: "Creating a GWLB endpoint"
product: "PrivateLink"
product_code: "privatelink"
source: "https://docs.byteplus.com/en/docs/privatelink/Creating_a_GWLB_endpoint"
---

<span id="rEuVYqTm"></span>
## Prerequisites


* Ensure that the service consumer has created a VPC and its subnets. For detailed actions, see [Creating a Virtual Private Cloud](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC).

* Ensure the service provider's account has already created an endpoint service. For detailed actions, see [Creating an endpoint service](https://docs.byteplus.com/en/docs/privatelink/Creating-endpoint-services).

* When an interface endpoint and its endpoint service reside under different accounts, the service provider must have added the account creating the endpoint to the endpoint service's allowlist. For detailed actions, see [Adding an endpoint service allowlist](https://docs.byteplus.com/en/docs/privatelink/Managing-allowlists-for-endpoint-services#.5re75Yqg5pyN5Yqh55m95ZCN5Y2V).


<span id="L05Q2vgP"></span>
## Action notes

A Gateway Load Balancer (GWLB) Endpoint is a special type of interface endpoint and shares the quota of general interface endpoints.


* The maximum number of interface endpoints that can be created by a single account in a single region is 500.

* The maximum number of interface endpoints that can be created in a single VPC is 50.


If the default quota cannot meet your needs, go to [Quota Center](https://console.byteplus.com/quota/productList) to increase the corresponding quota.

<span id="ctTuBTmr"></span>
## Procedures


1. Log in to the [Endpoint console](https://console.byteplus.com/pl/endpoints) using the Service consumer's account.

2. Accounts that have not completed cross\-service role authorization must follow the steps below to grant the required role.

   1. On the **Cross\-service access request** page, click **Authorize**.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">The authorized role will be displayed in the role list of the Identity and Access Management (IAM) platform. Deleting the authorized role may cause cross\-service access failures. Proceed with caution.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">If the authorization role is deleted and you need to continue using the PrivateLink service, you must re\-authorize the role.      </div>
      

   2. In the left navigation tree, click **Endpoint** again.

3. In the top menu bar, select the target project and region.

4. On the **Gateway Endpoint** tab, click **Create Endpoint** and configure the parameters according to the table below.

   
   |Parameters |Notes |Example |
   |---|---|---|
   |**Basic information** |||
   |Region |Select the region of endpoint. |cn\-shanghai |
   |Name |Enter the name of endpoint. |endpoint\-1 |
   |Type |Select the type of endpoint. |Gateway Load Balancer |
   |Project |Select the project to which the endpoint belongs. For more information, see [Project management](https://docs.byteplus.com/en/docs/privatelink/Managing-projects). |default |
   |**Endpoint service** |||
   |Add method |Select the method for associating an endpoint service. Choose how to specify the **Endpoint service** based on your needs.<br><br><br>* **Add by Service Name**: Enter the target endpoint service name (contact the service provider to obtain this). Enter the name and click **Verify** next to the input box to confirm if the name is correct.<br><br>   > If verification fails, see [Why does verification fail when entering the endpoint service name when creating an endpoint?](https://docs.byteplus.com/en/docs/privatelink/FAQs#.5Yib5bu657uI56uv6IqC54K55pe277yM6L6T5YWl57uI56uv6IqC54K55pyN5Yqh5ZCN56ew77yM5Li65LuA5LmI5pi-56S66aqM6K-B5aSx6LSl77yf) for troubleshooting.   <br>   <br><br>* **Select available services**: Choose from endpoint services under your account in the current region, as well as all cross\-account endpoint services for which authorization has been completed.<br><br>   > If using an IAM user, you may be unable to select available endpoint services. See [Why can't I select an available endpoint service when creating an endpoint?](https://docs.byteplus.com/en/docs/privatelink/FAQs#.5Li65LuA5LmI5Yib5bu657uI56uv6IqC54K55pe25peg5rOV6YCJ5oup5Y-v55So55qE57uI56uv6IqC54K55pyN5Yqh77yf) for resolution. |Add by service name, com.volces.privatelink.cn\-guangzhou.epsvc\-2fe630gurkl37k5gfuy33\*\*\*\* |
   |Payer account |Only endpoint account is supported. |Endpoint Account |
   |**Network configuration** |||
   |VPC |Select the VPC to which the endpoint belongs. |vpc\-2 |
   |Availability Zone and Subnet |Check the box for the Availability Zones of the endpoint service where you need to establish connections and select the corresponding subnet for each. The list displays all Availability Zones supported by the selected endpoint service.<br><br>After a subnet is selected, the system will automatically create an endpoint ENI for you. You can choose to have the system automatically assign a private IP address to this ENI, or you can manually assign one. When manually assigning a private IP address, the entered IP address must fall within the subnet's CIDR block. |Availability Zone A, subnet01 \| Auto\-assign IP, 192.168.3.0/24 |
   |**Advanced options** |||
   |Tag |A tag consists of a key\-value pair and is used for categorizing and searching resources For more information, see [Tag management](https://docs.byteplus.com/en/docs/privatelink/Managing-tags).<br><br>Click **Add tag**, enter the tag key and tag value to add a tag to the interface endpoint. |* Tag key: ep\-key<br><br>* Tag value: ep\-test |
   |IP address type |Please select the IP address type for endpoint. Supports both IPv4 and IPv6 types.<br><br><br>* By default, only IPv4 is selected, indicating the endpoint supports only IPv4.<br><br>* Selecting IPv4 and IPv6 indicates that the endpoint supports both IPv4 and IPv6 protocols.<br><br>* By default, only IPv6 is selected, indicating the endpoint supports only IPv6.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The PrivateLink IPv6 feature is currently in Beta stage. For trial requests, please contact your account manager.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If you need to enable both IPv4 and IPv6, ensure the following conditions are met:</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">The selected endpoint service supports IPv6.</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">The selected VPC has IPv6 CIDR enabled and contains at least one subnet with IPv6 CIDR configured.</div><br> |IPv4 |
   

5. Click **Buy now** to complete the action.

6. Click **Go to console** to view the created interface endpoint instances.


<span id="Zy2GNht4"></span>
## What to do next

After the endpoint is successfully created, it automatically sends a connection request to its associated endpoint service. The endpoint can only access its associated endpoint service via the private connection after this connection request is accepted by the service provider.

If the endpoint cannot successfully access its associated endpoint service after creation, contact the service provider for resolution.

<span id="5CYNd1RB"></span>
## Related documents

[CreateVpcEndpoint](https://docs.byteplus.com/en/docs/privatelink/CreateVpcEndpoint)
