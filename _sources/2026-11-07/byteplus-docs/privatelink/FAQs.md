---
title: "FAQs"
product: "PrivateLink"
product_code: "privatelink"
section: "Document"
source: "https://docs.byteplus.com/en/docs/privatelink/FAQs"
---

<span id=".56eB572R6L-e5o6l5piv5ZCm5pSv5oyB6Leo5Zyw5Z-f6K6_6Zeu77yf"></span>
## Does PrivateLink support cross\-region access?

PrivateLink itself does not support cross\-region access, but cross\-region access can be achieved when used with Cloud Enterprise Network (CEN).

<span id="rFWrtWJ6"></span>
## Does PrivateLink support HTTPS protocol access?

The endpoint domain name of PrivateLink itself does not support access via the HTTPS protocol. However, you can configure a private DNS name to enable HTTPS access.

The configuration process is as follows: [Enable private DNS name for the endpoint service](https://docs.byteplus.com/en/docs/privatelink/Modifying-Verifying-private-DNS-names#.5L-u5pS556eB5pyJRE5T5ZCN56ew) \-\-\> [Enable private DNS name for the endpoint](https://docs.byteplus.com/en/docs/privatelink/Modifying-basic-information-on-endpoints#.5ZCv55SoL-WFs-mXreengeaciUROU-WQjeensA==)

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">When enabling the private DNS name for the endpoint service, the domain name you specify must support HTTPS access.</div>


<span id=".5Yib5bu657uI56uv6IqC54K55pe277yM6L6T5YWl57uI56uv6IqC54K55pyN5Yqh5ZCN56ew77yM5Li65LuA5LmI5pi-56S66aqM6K-B5aSx6LSl77yf"></span>
## When creating an endpoint, why does entering the endpoint service name result in a validation failure?

The endpoint service validation fails in the following situations:


* The account you are using for the operation does not have permission to access this endpoint service. If you wish to continue to attach the endpoint service, please contact the endpoint service's owner account to add permission to your action account. For detailed actions, see [Adding the service allowlist](https://docs.byteplus.com/en/docs/privatelink/Managing-allowlists-for-endpoint-services#.5re75Yqg5pyN5Yqh55m95ZCN5Y2V).

* The region of the endpoint service is different from the region of the endpoint. Please modify the region of the endpoint or re\-enter the endpoint service name to ensure the endpoint and the endpoint service are in the same region.

* The payer account for the endpoint service is the endpoint service Account, and the Account is already overdue.

* The specified endpoint service has been deleted or does not exist.


<span id=".5Li65LuA5LmI5Yib5bu657uI56uv6IqC54K55pe25peg5rOV6YCJ5oup5Y-v55So55qE57uI56uv6IqC54K55pyN5Yqh77yf"></span>
## Why can't I select an available endpoint service when creating an endpoint?

The inability to select an available endpoint service when creating an endpoint may be due to the following reasons:


* You are using an IAM user account. You need to contact the root user to create the following custom policy and grant it globally to the IAM user.

   ```Plain Text
   {
     "Statement": [
       {
         "Effect": "Allow",
         "Action": [
           "privatelink:DescribeVpcEndpointServicesByEndUser"
         ],
         "Resource": [
           "*"
         ]
       }
     ]
   }
   ```
   

* If the account that owns the endpoint is different from the account that owns the endpoint service, and the endpoint service has not been authorized for the root user you are using, please contact the service provider to add your account to the service allowlist as described in [Adding a service allowlist](https://docs.byteplus.com/en/docs/privatelink/Managing-allowlists-for-endpoint-services#.5re75Yqg5pyN5Yqh55m95ZCN5Y2V).


<span id=".5Li65LuA5LmI57uI56uv6IqC54K5572R5Y2h55qE5pyN5Yqh54q25oCB5pi-56S65byC5bi477yf6K-l5aaC5L2V5aSE55CG77yf"></span>
## How should I handle the abnormal service status displayed for the endpoint network interface?

Please follow the steps below to troubleshoot the **endpoint** and the **endpoint service** sequentially.


|Troubleshooting target |Troubleshooting actions |Notes |
|---|---|---|
|\- |Determine if this is a newly established connection |When an endpoint establishes a connection with an endpoint service for the first time, health checks may experience a delay. It is recommended to wait for approximately 3 minutes before confirming if the service status is normal. |
|Endpoint |Check endpoint connection status |View the connection status on the endpoint list page. If the status is not **Connected**, contact the endpoint service provider to complete the connection configuration. For more status details, see [Endpoint overview](https://docs.byteplus.com/en/docs/privatelink/Endpoint-01). |
||Check whether the security group allows traffic |* IPv4: Ensure that the endpoint security group allows ICMP protocol from the `0.0.0.0/0` or `100.64.0.0/10` CIDR block. If not, add an inbound rule that allows the `100.64.0.0/10` CIDR block.<br><br>* IPv6: Ensure that the endpoint security group allows ICMPv6 protocol from the `::/0` or `fd00:64::/32` CIDR block. If not, add an inbound rule that allows the `fd00:64::/32` CIDR block. |
||Check whether the endpoint network interface is reachable |1. Go to the endpoint details page, click the **Availability Zone and network interface** tab, and view the IP address of the target endpoint network interface.<br><br>2. Log in to an ESC instance within the same VPC as the network interface, and run the `ping` (or `ping6`) command to confirm whether the IP address of the network interface is reachable.<br><br>   * Ping succeeds: Endpoint network interface is reachable.<br><br>   * Ping fails: Contact the endpoint service provider to check the configuration. |
|Endpoint service |Check the connection status with the endpoint |Go to the Endpoint Service details page, and check the target endpoint status under the **Endpoint connection** tab.<br><br><br>* **Connected** status: Connection established.<br><br>* If the status is not **Connected**: See [Accepting an endpoint connection](https://docs.byteplus.com/en/docs/privatelink/Accepting-Rejecting-endpoint-connection) to complete the establishment of the endpoint connection. |
||Check the health check status of service resource |1. Go to the endpoint service details page, click the **Service Resource** tab, and then click the name of the target service resource.<br><br>2. On the **Listener** tab, view the health check status.<br><br>3. If the status shows **exception**, see the [Health check exception troubleshooting guide](https://docs.byteplus.com/en/docs/clb/Troubleshooting-health-check-exceptions) to identify the cause. |


If the issue persists after following the troubleshooting steps above, please submit a ticket for further assistance.

<span id="YnXwebvy"></span>
## Why can't IAM users view monitoring data?

If an IAM user is granted only PrivateLink permissions but not the necessary CloudMonitor permissions, they will not be able to view monitoring data for the endpoint service or endpoint. Please use the root user to which the IAM user belongs and  to add the system\-preset CloudMonitor policy permissions for the IAM user based on actual needs.


|Policy name |Supported action |
|---|---|
|CloudMonitorFullAccess |Management permissions for CloudMonitor. With this policy, the IAM user can both view monitoring data and use features of the CloudMonitor. |
|CloudMonitorReadOnlyAccess |Access permissions for CloudMonitor. With this policy, the IAM user can view monitoring data only. |


<span id="JvLRO2p0"></span>
## Why can't an IAM user create a gateway endpoint?

Because the IAM user you are using is only authorized for a project, and the DescribeVpcGatewayEndpointServices API requires global authorization. Please contact the root user to create the following custom policy and add authorization to grant global authorization to this IAM user.

```Plain Text
{
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "privatelink:DescribeVpcGatewayEndpointServices"
      ],
      "Resource": [
        "*"
      ]
    }
  ]
}
```


<span id=".57uI56uv6IqC54K56L-e5o6l55qE572R57uc6YCf546H5aaC5L2V5o-Q6auY77yf"></span>
## How can I improve the network speed of the endpoint connection?

The default network rate for an endpoint connection is 10 Gbps. If this does not meet your needs, see [Adjusting an endpoint connection rate limiting](https://docs.byteplus.com/en/docs/privatelink/Adjusting-endpoint-connection-rate-limiting#.6LCD5pW057uI56uv6IqC54K56L-e5o6l6ZmQ6YCf).

Please note that the actual rate is also limited by the bandwidth of the endpoint service's resources. If adjusting endpoint connection rate limiting still does not improve the network rate, for on\-demand adjustments, see [Endpoint service bandwidth](https://docs.byteplus.com/en/docs/privatelink/Overview-endpoint-services#.57uI56uv6IqC54K55pyN5Yqh5bim5a69).

<span id="RzgEjS7B"></span>
## Why can't the private DNS feature of an endpoint be enabled?

The Private DNS feature for endpoints cannot be enabled. Possible reasons:


* The endpoint service associated with the endpoint does not have the private DNS feature enabled. Please contact the service provider to enable the private DNS feature.

* The endpoint service associated with the endpoint has Private DNS enabled, however the configured public domain name has not passed domain verification. Please see [Verifying a private DNS name](https://docs.byteplus.com/en/docs/privatelink/Modifying-Verifying-private-DNS-names#.6aqM6K-B56eB5pyJRE5T5ZCN56ew) to complete verification.


<span id="d2pUCTq9"></span>
## How does a Kubernetes (K8s) cluster use an already deployed endpoint service?

Within the VPC where the K8s cluster resides, create an interface endpoint for the target endpoint service. For more details, please see [Implementing private access between VPCs across accounts](https://docs.volcengine.com/docs/6980/155852).

<span id="N3QRsbUT"></span>
##
