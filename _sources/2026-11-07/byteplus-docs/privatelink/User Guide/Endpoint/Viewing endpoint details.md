---
title: "Viewing endpoint details"
product: "PrivateLink"
product_code: "privatelink"
source: "https://docs.byteplus.com/en/docs/privatelink/Viewing-endpoint-details"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenarios

After the endpoint is created, you can view its detailed information.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [Endpoint console](https://console.byteplus.com/pl/endpoints) using the service consumer's account.

2. In the top menu bar, select the target project and region.

3. Select **Interface endpoint** or **Gateway endpoint** tab, and click the name of the target endpoint.

4. You can view relevant information about an endpoint by switching between different tabs.

   * The interface endpoint is detailed in the following table.

      
      |Tab |Notes |
      |---|---|
      |Overview |View the basic information and billing details of the target endpoint.<br><br><br>* Basic information: Includes name, endpoint domain, and other information. You can also modify the endpoint's name and description.<br><br>   * **Instance status**: Indicate the status of the endpoint.<br><br>   * **Connection status**: Indicate the connection status between the endpoint and the endpoint service. [Learn more](https://docs.byteplus.com/en/docs/privatelink/Endpoint-01#.57uI56uv6IqC54K56L-e5o6l54q25oCB)<br><br>* Billing information: Includes billing methods, creation time, and other details. |
      |Availability Zone and network interface |View information for all Availability Zones where the target endpoint has established connections to the endpoint service. You can also edit the Availability Zones from here.<br><br><br>* **Status**: Indicates the connection status of the endpoint network interface and the VPC endpoint service.Status:<br><br>* **Service status**: Indicates the health check status of the endpoint.<br><br>   The system automatically detects the IP status of the endpoint network interface and the health status of the service resource in the VPC endpoint service. When both are normal, the service status displays as normal. Otherwise, it shows abnormal.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When an endpoint establishes its initial connection to the endpoint service, health check latency may occur. It is recommended to wait for 3 minutes before confirming whether the service status is abnormal.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When both the VPC endpoint service and endpoint support IPv4 and IPv6 simultaneously, the system monitors the service status for both the IPv4 and IPv6 addresses. Otherwise, the system only monitors the service status for IPv4 and IPv6 addresses.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The PrivateLink IPv6 feature is currently in Beta testing. For trial requests, please contact your account manager.   </div><br>    |
      |Security Group |View all security groups currently associated with the target endpoint. You can also change the security groups for the target endpoint from this tab. |
      |Monitoring |You can view the monitoring data of the target endpoint. For detailed introduction, see [Viewing monitoring data](https://docs.byteplus.com/en/docs/privatelink/Monitor-01). |
      

   * For a Gateway Endpoint, this page shows basic information (Name, ID, etc.) and the configured access policies. It also supports modifying the Name, Description, and Access Policies.


<span id=".55u45YWz5paH5qGj"></span>
## Related documents


* [DescribeVpcEndpoints](https://docs.byteplus.com/en/docs/privatelink/DescribeVpcEndpoints)

* [DescribeVpcEndpointAttributes](https://docs.byteplus.com/en/docs/privatelink/DescribeVpcEndpointAttributes)
