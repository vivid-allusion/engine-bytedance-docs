---
title: "Creating a gateway endpoint"
product: "PrivateLink"
product_code: "privatelink"
source: "https://docs.byteplus.com/en/docs/privatelink/Endpoint-03"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenarios

An Endpoint establishes a secure, private connection between a Virtual Private Cloud (VPC) and an Endpoint Service. Create a Gateway Endpoint when a service consumer needs to access the official private address provided by the BytePlus Torch Object Storage (TOS) service, then implement access control over which VPC resources can reach the TOS service. 

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* Ensure a VPC has been created in the target region. For detailed actions, see [Creating a Virtual Private Cloud](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC).

* Ensure an Endpoint Service already exists. If no endpoint service is available, please contact your account manager.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedures


1. Log in to the [terminal console](https://console.byteplus.com/pl/endpoints) using the service consumer's account.

2. Accounts that have not completed cross\-service role authorization must follow the steps below to grant the required role.

   1. On the **Cross\-service access request** page, click **Authorize**.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">The authorized role will be displayed in the role list of the Identity and Access Management (IAM) platform. Deleting the authorized role may cause cross\-service access failures. Proceed with caution.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">If the authorization role is deleted and you need to continue using the PrivateLink service, you must re\-authorize the role.      </div>
      

   2. In the left\-side navigation pane, click **Endpoint** again.

3. In the top menu bar, select the target project and region.

4. Select the **Gateway Endpoint** tab, click **Create Endpoint**, and see the table below for configuration of relevant parameters.

   
   |Parameter |Explanation |Example |
   |---|---|---|
   |**Basic information** |||
   |Regions |Select the region of endpoint. |China (Shanghai) |
   |Name |Enter the name of endpoint. |endpoint\-1 |
   |Topic |Select the type of endpoint.<br><br>A gateway endpoint is a virtual gateway that supports configuring access policies to restrict traffic to the endpoint service. Suitable for scenarios requiring on\-demand access to [TOS services](https://docs.byteplus.com/en/docs/tos/docs-what-is-tos). |Gateway |
   |Project |Select the project to which the endpoint belongs.<br><br><br>* If no project is specified, it means the endpoint belongs to the default project default.<br><br>* Endpoints cannot be shared across different projects. Once a project is selected, the created endpoint will be accessible only to users with permissions for that project.<br><br>* For more information on the features of the PrivateLink project, see [Project management](https://docs.byteplus.com/en/docs/privatelink/Managing-projects). |default |
   |**Endpoint Service** |||
   |Endpoint Service |Select the Endpoint Service to which the endpoint should connect. Gateway Endpoints currently only support the TOS service. Endpoint Services that are already associated with an Interface Endpoint cannot be selected.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When creating an endpoint using an IAM user, you may not be able to select an available endpoint service; see <a href="https://docs.byteplus.com/en/docs/privatelink/FAQs#.5Li65LuA5LmI5Yib5bu657uI56uv6IqC54K55pe25peg5rOV6YCJ5oup5Y-v55So55qE57uI56uv6IqC54K55pyN5Yqh77yf">why endpoint services are unavailable when creating an endpoint?</a>.</div><br> |com.volces.privatelink.cn\-guangzhou.tos |
   |**Network Configuration** |||
   |VPC |Select the VPC to which the endpoint belongs. Select the VPC to which the endpoint will belong (the list displays all VPCs in the current region). |vpc\-2 |
   |Access policy |Configure the Access Policy for TOS from the endpoint's VPC.<br><br><br>* The Default Policy allows all traffic accessing this gateway endpoint.<br><br>* To restrict traffic, configure a custom policy, see [Gateway endpoint access policy example](https://docs.byteplus.com/en/docs/privatelink/Permission-management-02#.56S65L6L5LiJ77ya572R5YWz57uI56uv6IqC54K56K6_6Zeu562W55Wl56S65L6L). <br><br>* To restrict accessible VPCs at the bucket level, you can configure both the endpoint policy and IAM policy separately.  |{<br><br> "Statement" : [<br><br> {<br><br> "Effect": "Allow",<br><br> "Principal": "\*",<br><br> "Action": "\*",<br><br> "Resource": "\*",<br><br> }<br><br> ]<br><br>} |
   |**Advanced option** |||
   |Tags |A tag consists of a key\-value pair and is used for categorizing and searching resources For more information, see [Tag management](https://docs.byteplus.com/en/docs/privatelink/Managing-tags).<br><br>Click **Add tag**, input the Tag key and Tag value to add a tag to the gateway endpoint. |* Tag key: ep\-key<br><br>* Tag value: ep\-test |
   

5. Click **Buy now** to complete the action.


<span id=".55u45YWz5paH5qGj"></span>
## Related documents

[CreateVpcGatewayEndpoint](https://docs.byteplus.com/en/docs/privatelink/CreateVpcGatewayEndpoint)
