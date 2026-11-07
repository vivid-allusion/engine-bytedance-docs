---
title: "Endpoint overview"
product: "PrivateLink"
product_code: "privatelink"
source: "https://docs.byteplus.com/en/docs/privatelink/Endpoint-01"
---

## Introduction​

Endpoint is a private service access point deployed by a service consumer within their own VPC for private access to services provided by a service provider.

## Endpoint type

Endpoints are categorized into the following types:

* **Interface endpoint**: A private access point within a VPC. Cloud resources can securely access the endpoint service (including BytePlus services and user\-owned services) via its node domain name.

   > Explanation

   * > A Managed Endpoint is an interface\-type endpoint created by an [Official BytePlus service](https://docs.byteplus.com/en/docs/privatelink/Overview-endpoint-services).

   * > The service consumer can only modify the tags of a managed endpoint; all other edit operations are unsupported.

* **Gateway endpoint**: An endpoint that restricts the scope of access from cloud resources within a VPC to the endpoint service (currently supporting only Torch Object Storage (TOS)). It supports configuring policies to control traffic and is suitable for on\-demand access to TOS scenarios.

## Interface endpoint domain name

Interface endpoints support multiple domain name formats. The default format is typically used. To use other specific domain formats, ensure the endpoint service has the corresponding capability enabled.

The different interface endpoint domain names are detailed in the following table.

|Domain type |Format description |Application scenario |
|---|---|---|
|Default domain name |*EndpointID*.*ServiceID*.*RegionID*.privatelink.volces.com |Suitable for scenarios where there is no need to distinguish between services via the endpoint's domain name.<br><br>> **tip**<br><br><br>> The default domain name supports HTTP access only; HTTPS access is not supported.<br> |
|Private DNS (custom domain name) |No specific format is required; any valid internet domain name is acceptable. |Suitable for scenarios where you need to use your original business domain name or require HTTPS protocol access.​​ |

## Endpoint connection status

|Endpoint connection status |Explanation |Supported endpoint connection operations |
|---|---|---|
|Pending Connection |Indicates that the endpoint has initiated a connection request and is pending acceptance by the endpoint service. In this state, the connection status for all Availability Zones of this endpoint is Pending Connection. |* [Accept endpoint connection](https://docs.byteplus.com/en/docs/privatelink/Accepting-Rejecting-endpoint-connection)<br><br>* [Reject endpoint connection](https://docs.byteplus.com/en/docs/privatelink/Accepting-Rejecting-endpoint-connection#.5ouS57ud57uI56uv6IqC54K56L-e5o6l) |
|Connected |Indicates that all Availability Zones within the endpoint have successfully established a connection with the endpoint service and can communicate normally. |* When there is only 1 service resource in an Availability Zone:<br><br>   * [Reject endpoint connection](https://docs.byteplus.com/en/docs/privatelink/Accepting-Rejecting-endpoint-connection#.5ouS57ud57uI56uv6IqC54K56L-e5o6l)<br><br>* When both the old and a new service resource coexist in the same Availability Zone (This scenario occurs during a smooth migration of service resources):<br><br>   * Disconnect the old service resource |
|Partial connection |Indicates that some Availability Zones within the endpoint have successfully established a connection with the endpoint service and can communicate normally. In this state, the connection status for the endpoint's Availability Zones simultaneously includes Connected and Pending Connection. |* [Accept endpoint connection](https://docs.byteplus.com/en/docs/privatelink/Accepting-Rejecting-endpoint-connection)<br><br>* [Reject endpoint connection](https://docs.byteplus.com/en/docs/privatelink/Accepting-Rejecting-endpoint-connection#.5ouS57ud57uI56uv6IqC54K56L-e5o6l)<br><br>* [Modify endpoint connection bandwidth](https://docs.byteplus.com/en/docs/privatelink/Adjusting-endpoint-connection-rate-limiting#.6LCD5pW057uI56uv6IqC54K56L-e5o6l6ZmQ6YCf) |
|Rejected |Indicates that the Endpoint Service has rejected connection requests from all Availability Zones of the endpoint. |* [Accept endpoint connection](https://docs.byteplus.com/en/docs/privatelink/Accepting-Rejecting-endpoint-connection)<br><br>* [Modify endpoint connection bandwidth](https://docs.byteplus.com/en/docs/privatelink/Adjusting-endpoint-connection-rate-limiting#.6LCD5pW057uI56uv6IqC54K56L-e5o6l6ZmQ6YCf) |
|Failed |Indicates that all Availability Zones of the endpoint have failed to establish a connection with the endpoint service and cannot communicate. In this state, the connection status for all of the endpoint's Availability Zones is Connection failed, or the statuses across all zones simultaneously include Connection Failed, Rejected, and/or Pending Connection. |* [Accept endpoint connection](https://docs.byteplus.com/en/docs/privatelink/Accepting-Rejecting-endpoint-connection)<br><br>* [Reject endpoint connection](https://docs.byteplus.com/en/docs/privatelink/Accepting-Rejecting-endpoint-connection#.5ouS57ud57uI56uv6IqC54K56L-e5o6l)<br><br>* [Modify endpoint connection bandwidth](https://docs.byteplus.com/en/docs/privatelink/Adjusting-endpoint-connection-rate-limiting#.6LCD5pW057uI56uv6IqC54K56L-e5o6l6ZmQ6YCf) |
|Partially failed connection |Indicates that some Availability Zones of the endpoint have failed to establish a connection with the endpoint service and cannot communicate. In this state, the connection status for all Availability Zones within the endpoint simultaneously includes Rejected, Connected, or Connection Failed. |* [Accept endpoint connection](https://docs.byteplus.com/en/docs/privatelink/Accepting-Rejecting-endpoint-connection)<br><br>* [Reject endpoint connection](https://docs.byteplus.com/en/docs/privatelink/Accepting-Rejecting-endpoint-connection#.5ouS57ud57uI56uv6IqC54K56L-e5o6l)<br><br>* [Modify endpoint connection bandwidth](https://docs.byteplus.com/en/docs/privatelink/Adjusting-endpoint-connection-rate-limiting#.6LCD5pW057uI56uv6IqC54K56L-e5o6l6ZmQ6YCf) |
|Service delete |Indicates that the Endpoint Service associated with the endpoint has been deleted. |\- |
|Updating |Indicates that within the endpoint, the connection status for one or more Availability Zones is Establishing connection or Disconnecting. |\- |

## Health check

PrivateLink performs pre\-configured health checks. The checks include:

* The availability of endpoint network interface's IP address.

* The health status of the service resource in the endpoint service.

The endpoint network interface's service status is marked as normal only if both checks pass; otherwise, it is marked as abnormal. If the status is abnormal, troubleshoot the issue. For guidance, see [Why is the endpoint network interface's service status abnormal](https://docs.byteplus.com/en/docs/privatelink/FAQs).

Endpoints provide service via a domain name. If a network interface in one Availability Zone of a multi\-AZ endpoint fails, the system automatically removes that network interface's IP from the endpoint's DNS records. When users access the endpoint domain name, traffic is routed to the IPs of the healthy network interfaces, enabling cross\-AZ disaster recovery and ensuring **High availability**.

> **tip**

> When an endpoint establishes a connection with an endpoint service for the first time, health checks may experience a delay. It is recommended to wait for approximately 3 minutes before confirming if the service status is abnormal.

## Configuration procedures

* The configuration workflow for an interface endpoint is as follows:

   1. [Create interface endpoint](https://docs.byteplus.com/en/docs/privatelink/Endpoint-02): Create the endpoint instance to establish a connection to the endpoint service.

   2. [View interface endpoint](https://docs.byteplus.com/en/docs/privatelink/Viewing-endpoint-details): Check the endpoint network interface's service status to confirm successful configuration and obtain the endpoint's domain name.

   3. [Access endpoint service](https://docs.byteplus.com/en/docs/privatelink/Getting-Started-02#.5q2l6aqk5LiJ77ya5rWL6K-V6L-e6YCa5oCn): Use the endpoint's domain name to access the endpoint service.

* The configuration of a gateway endpoint is simple, requiring only the creation of a gateway endpoint for the endpoint service of the BytePlus official service type. For detailed configuration steps, see [Creating a gateway endpoint](https://docs.byteplus.com/en/docs/privatelink/Endpoint-03).
