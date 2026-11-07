---
title: "Creating an interface endpoint"
product: "PrivateLink"
product_code: "privatelink"
source: "https://docs.byteplus.com/en/docs/privatelink/Endpoint-02"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Prerequisites


* Ensure that the service consumer has created a VPC and its subnets. For detailed actions, see [Creating a Virtual Private Cloud](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC).

* Ensure the service provider's account has already created an endpoint service. For detailed actions, see [Creating an endpoint service](https://docs.byteplus.com/en/docs/privatelink/Creating-endpoint-services).

* When an interface endpoint and its endpoint service reside under different accounts, the service provider must have added the account creating the endpoint to the endpoint service's allowlist. For detailed actions, see [Adding an endpoint service allowlist](https://docs.byteplus.com/en/docs/privatelink/Managing-allowlists-for-endpoint-services#.5re75Yqg5pyN5Yqh55m95ZCN5Y2V).


<span id="2g8YeqWX"></span>
## Action notes


* The maximum number of interface endpoints that can be created by a single account in a single region is 500. If the default quota cannot meet your needs, go to [Quota Center](https://console.byteplus.com/quota/productList) to increase the corresponding quota.

* The maximum number of interface endpoints that can be created in a single VPC is 50. If the default quota cannot meet your needs, go to [Quota Center](https://console.byteplus.com/quota/productList) to increase the corresponding quota.

* The maximum number of security groups that can be associated with a single endpoint is 5.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedures


1. Use the service consumer account to log in to the [Endpoint console](https://console.byteplus.com/pl/endpoints).

2. Accounts that have not completed cross\-service role authorization must follow the steps below to grant the required role.

   1. On the **Cross\-service access request** page, click **Authorize**.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">The authorized role will be displayed in the role list of the Identity and Access Management (IAM) platform. Deleting the authorized role may cause cross\-service access failures. Proceed with caution.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">If the authorization role is deleted and you need to continue using the PrivateLink service, you must re\-authorize the role.      </div>
      

   2. In the left navigation tree, click **Endpoint** again.

3. In the top menu bar, select the target project and region.

4. On the **Interface Endpoint** tab, click **Create Endpoint** and configure the parameters as shown in the table below.

   
   |Parameters |Notes |Example |
   |---|---|---|
   |**Basic information** |||
   |Region |Select the region of endpoint. |cn\-shanghai |
   |Name |Enter the name of endpoint. |endpoint\-1 |
   |Type |Select the type of endpoint.<br><br>The interface endpoint is an elastic network interface with a private IP address from the subnet, capable of forwarding access traffic to the attached endpoint service. Suitable for scenarios requiring shared access to service resources in VPCs, whether within the same account or across different accounts. |Interface |
   |Project |Select the project to which the endpoint belongs.<br><br><br>* When no project is specified, the endpoint belongs to the default project "default".<br><br>* Endpoints cannot be shared across different projects. Once a project is selected, the created endpoint will be accessible only to users with permissions for that project.<br><br>* For more information about the project feature for endpoints, see [Project management](https://docs.byteplus.com/en/docs/privatelink/Managing-projects). |default |
   |**Endpoint service** |||
   |Enable cross\-region |Enable cross\-region. After enabled, the endpoint can connect to endpoint services in a different region. |Enable |
   |Service region |Select the region where the endpoint service to which the endpoint needs to connect is located. |China (Guangzhou) |
   |Add method |Select the method for associating an endpoint service. Choose how to specify the **Endpoint service** based on your needs.<br><br><br>* **Add by Service Name**: Enter the target endpoint service name (contact the service provider to obtain this). Enter the name and click **Verify** next to the input box to confirm if the name is correct.<br><br>   > If verification fails, see [Why does verification fail when entering the endpoint service name when creating an endpoint?](https://docs.byteplus.com/en/docs/privatelink/FAQs#.5Yib5bu657uI56uv6IqC54K55pe277yM6L6T5YWl57uI56uv6IqC54K55pyN5Yqh5ZCN56ew77yM5Li65LuA5LmI5pi-56S66aqM6K-B5aSx6LSl77yf) for troubleshooting.   <br>   <br><br>* **Select available services**: Choose from endpoint services under your account in the current region, as well as all cross\-account endpoint services for which authorization has been completed.<br><br>   > If using an IAM user, you may be unable to select available endpoint services. Refer to [Why can't I select an available endpoint service when creating an endpoint?](https://docs.byteplus.com/en/docs/privatelink/FAQs#.5Li65LuA5LmI5Yib5bu657uI56uv6IqC54K55pe25peg5rOV6YCJ5oup5Y-v55So55qE57uI56uv6IqC54K55pyN5Yqh77yf) for resolution.   <br>   <br><br>* **BytePlus Service**: Supports selecting endpoint services provided by official BytePlus services. For example, to select an endpoint service provided by Torch Object Storage (TOS)Object Storage, choose this option.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">To create an interface endpoint that supports IPv6, ensure the selected endpoint service supports IPv6.</div><br> |Add by service name, com.volces.privatelink.cn\-guangzhou.epsvc\-2fe630gurkl37k5gfuy33\*\*\*\* |
   |Payer account |The billing account for the PrivateLink service is specified by the payer account of the endpoint service and cannot be modified.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If the payer account is the endpoint service account, when the endpoint service is reclaimed due to overdue payments, the associated endpoint will also be deleted. If the publish region of the endpoint service involves cross\-border traffic, the account must have cross\-border qualifications. For details, see Cross\-border service overview.</div><br> |Endpoint Account |
   |**Network Configuration** |||
   |VPC |Select the VPC to which the endpoint belongs from the dropdown. |vpc\-2 |
   |IP address type |Select the IP address type of the endpoint.<br><br><br>* Select only IPv4: Indicates that the endpoint supports only IPv4.<br><br>* Select both IPv4 and IPv6: Indicates that the endpoint supports both IPv4 and IPv6.<br><br>* Select only IPv6: Indicates that the endpoint supports only IPv6.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The PrivateLink IPv6 feature is currently in Beta stage. For trial requests, please contact your account manager.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If you need to enable both IPv4 and IPv6, ensure the following conditions are met:</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">The selected endpoint service supports IPv6.</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">The selected VPC has IPv6 CIDR enabled and contains at least one subnet with IPv6 CIDR configured.</div><br> |IPv4 |
   |Availability zone and subnet |Select the availability zone and subnet for the endpoint.<br><br><br>* You can only select availability zones that are supported by the endpoint service mentioned above.<br><br>* After the subnet is selected, the system will automatically create an endpoint network interface within the subnet.<br><br>   * **IP address allocation method:** <br><br>      * Auto\-assign: The system automatically assigns an unused IP address from the selected subnet.<br><br>      * Custom\-assign: Manually enter an unused IP address from the selected subnet.<br><br>   * **Assign IP address:** <br><br>      * If the IP type is IPv4, assign an IPv4 address.<br><br>      * If the IP type is both IPv4 and IPv6, assign one IPv4 address and one IPv6 address.<br><br>      * If the IP type is IPv6, assign an IPv6 address. |Availability Zone A, subnet01 \| Auto\-assign IP, 192.168.3.0/24 |
   |Security group |Select the security group(s) to be associated with the endpoint's network interface.<br><br><br>* If the above VPC is a shared VPC, the security group must be created by the current account; shared security groups cannot be selected.<br><br>* Ensure that the security group associated with the endpoint network interface allows traffic from `100.64.0.0/10` and `fd00:64::/32`, because health check requests for PrivateLink originate from these two CIDR blocks. |Default\-sg |
   |**Advanced options** |||
   |Private DNS name |Enable Private DNS Name to assign a custom domain name for accessing the endpoint.<br><br>An endpoint can only enable its DNS name if the associated endpoint service has DNS enabled and internet domain verification has passed. After enabled, the private DNS name defaults to the private DNS name configured for the endpoint service. You can access the endpoint service using this private DNS name.<br><br>For detailed actions on enabling and verifying the private DNS name of an endpoint service, see [Modifying or verifying a Private DNS Name](https://docs.byteplus.com/en/docs/privatelink/Modifying-Verifying-private-DNS-names). |Disable |
   |Tag |A tag consists of a key\-value pair and is used for categorizing and searching resources For more information, see [Tag management](https://docs.byteplus.com/en/docs/privatelink/Managing-tags).<br><br>Click **Add tag**, enter the tag key and tag value to add a tag to the interface endpoint. |* Tag key: ep\-key<br><br>* Tag value: ep\-test |
   

5. Depending on the payer account, select the appropriate steps to create the interface endpoint. 

   * The payer account is the Endpoint account

      1. Click **Confirm order** according to the console instructions to review and confirm the Legal.

      2. Click **Agree and buy** to complete the action.

      3. Click **Go to console** to view the created interface endpoint instances.

   * The payer account is the Endpoint Service account

      Click **Buy now** to complete the action.


<span id=".5ZCO57ut5pON5L2c"></span>
## What to do next

After the endpoint is successfully created, it automatically sends a connection request to its associated endpoint service. The endpoint can only access its associated endpoint service via the private connection after this connection request is accepted by the service provider.

If the endpoint cannot successfully access its associated endpoint service after creation, contact the service provider for resolution.

<span id=".55u45YWz5paH5qGj"></span>
## Related documents

[CreateVpcEndpoint](https://docs.byteplus.com/en/docs/privatelink/CreateVpcEndpoint)
