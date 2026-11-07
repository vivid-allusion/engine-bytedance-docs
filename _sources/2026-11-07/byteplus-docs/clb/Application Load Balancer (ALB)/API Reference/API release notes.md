---
title: "API release notes"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Release-notes"
---

This topic introduces the API updates of Application Load Balancer (ALB).

## September 2026

|API name |Release note |Associated features |
|---|---|---|
|[DescribeRules](https://docs.byteplus.com/en/docs/clb/ALB-DescribeRules) |New response data **InsertHeaderConfig.**  |Forwarding rule |

## July 2026

|API name |Release note |Associated features |
|---|---|---|
|[CreateRules](https://docs.byteplus.com/en/docs/clb/ALB-CreateRules)<br><br> |* Added value InsertHeader for Rules.N.RuleActions.N.Type.<br><br>* New request parameter: Rules.N.RuleActions.N.InsertHeaderConfig.<br><br>* New error codes: InvalidRules.RuleActions.InsertHeaderConfig.Key.Malformed, InvalidRules.RuleActions.InsertHeaderConfig.Value.Malformed, InvalidRules.RuleActions.InsertHeaderConfig.ValueType.Malformed, Forbidden, ErrServerGroupTypeMountUnSupported. |Forwarding rule |
|[ModifyRules](https://docs.byteplus.com/en/docs/clb/ALB-ModifyRules) |||
|[DescribeRules](https://docs.byteplus.com/en/docs/clb/ALB-DescribeRules) |New response parameter InsertHeaderConfig. ||
|[AddServerGroupBackendServers](https://docs.byteplus.com/en/docs/clb/ALB-AddServerGroupBackendServers) |New error codes added: ErrInvalidServerDomain, ErrDomainServerGroupOnlyOneServer, ErrDomainServerNotSupportIp, ErrDomainServerNotSupportRemote. |Server group |
|[CreateCustomizedCfg](https://docs.byteplus.com/en/docs/clb/CreateCustomizedCfg) |New error codes ErrCustomizedCfgMaxHeaders and ErrCustomizedCfgMaxHeadersRepeat. |Custom configuration |
|[ModifyCustomizedCfgAttributes](https://docs.byteplus.com/en/docs/clb/ModifyCustomizedCfgAttributes) |||
|[ModifyLoadBalancerType](https://docs.byteplus.com/en/docs/clb/ModifyLoadBalancerType) |New error code added: InvalidLoadBalancer.InUse. |ALB instance |

## May 2026

|API name |Release note |Associated features |
|---|---|---|
|[DescribeRules](https://docs.byteplus.com/en/docs/clb/ALB-DescribeRules) |New response parameters added: SourceIpConfig, CookieConfig, CorsConfig. |Forwarding rule<br><br> |
|[CreateRules](https://docs.byteplus.com/en/docs/clb/ALB-CreateRules)<br><br> |* New request parameters added: Rules.N.RuleConditions.N.CookieConfig.Values.N.Key, Rules.N.RuleActions.N.CorsConfig.AllowHeaders.N, Rules.N.RuleActions.N.CorsConfig.AllowMethods.N, Rules.N.RuleConditions.N.SourceIpConfig.Values.N, Rules.N.RuleConditions.N.CookieConfig.Values.N.Value, Rules.N.RuleActions.N.CorsConfig.AllowOrigin.N, Rules.N.RuleActions.N.CorsConfig.ExposeHeaders.N, Rules.N.RuleActions.N.CorsConfig.AllowCredentials, Rules.N.RuleActions.N.CorsConfig.MaxAge<br><br>* New error codes added: InvalidRules.RuleConditions.SourceIpConfig.Values.Malformed, InvalidRules.RuleActions.CorsConfig.AllowMethods.Malformed, InvalidRules.RuleActions.CorsConfig.AllowOrigin.Malformed, InvalidRules.RuleConditions.SourceIpConfig.Duplicated, InvalidRules.RuleConditions.CookieConfig.Values.Duplicated, InvalidRules.RuleActions.CorsConfig.AllowHeaders.Malformed, InvalidRules.RuleActions.CorsConfig.ExposeHeaders.Malformed, InvalidRules.RuleActions.CorsConfig.AllowCredentials.Malformed, InvalidRules.RuleActions.CorsConfig.MaxAge.Malformed, InvalidRules.RuleConditions.CookieConfig.Values.Key.Malformed, InvalidRules.RuleConditions.CookieConfig.Values.Value.Malformed, InvalidRules.RuleConditions.SourceIpConfig.Values.Duplicated, Forbidden ||
|[ModifyRules](https://docs.byteplus.com/en/docs/clb/ALB-ModifyRules)<br><br> |* New request parameters added: Rules.N.RuleActions.N.CorsConfig.AllowCredentials, Rules.N.RuleConditions.N.CookieConfig.Values.N.Key, Rules.N.RuleConditions.N.CookieConfig.Values.N.Value, Rules.N.RuleActions.N.CorsConfig.AllowOrigin.N, Rules.N.RuleActions.N.CorsConfig.AllowMethods.N, Rules.N.RuleActions.N.CorsConfig.AllowHeaders.N, Rules.N.RuleConditions.N.SourceIpConfig.Values.N, Rules.N.RuleActions.N.CorsConfig.ExposeHeaders.N, Rules.N.RuleActions.N.CorsConfig.MaxAge, Rules.N.RuleActions.N.RedirectConfig.Query<br><br>* New error codes added: InvalidRules.RuleActions.CorsConfig.AllowHeaders.Malformed, InvalidRules.RuleConditions.CookieConfig.Values.Key.Malformed, InvalidRules.RuleActions.CorsConfig.MaxAge.Malformed, InvalidRules.RuleActions.CorsConfig.AllowCredentials.Malformed, InvalidRules.RuleActions.CorsConfig.ExposeHeaders.Malformed, InvalidRules.RuleActions.CorsConfig.AllowMethods.Malformed, InvalidRules.RuleActions.CorsConfig.AllowOrigin.Malformed, InvalidRules.RuleConditions.SourceIpConfig.Values.Malformed, InvalidRules.RuleConditions.SourceIpConfig.Duplicated, InvalidRules.RuleConditions.CookieConfig.Values.Duplicated, InvalidRules.RuleConditions.CookieConfig.Values.Value.Malformed, InvalidRules.RuleConditions.SourceIpConfig.Values.Duplicated, InvalidRules.RuleActions.RedirectConfig.Query.Malformed, Forbidden ||
|[DescribeServerGroupAttributes](https://docs.byteplus.com/en/docs/clb/ALB-DescribeServerGroupAttributes) |New response parameter: SlowStartConfig |Server group |
|[DescribeServerGroups](https://docs.byteplus.com/en/docs/clb/ALB-DescribeServerGroups) |New response parameter: SlowStartConfig ||
|[CreateServerGroup](https://docs.byteplus.com/en/docs/clb/ALB-CreateServerGroup)<br><br> |* New request parameters: SlowStartConfig.SlowStartEnabled, SlowStartConfig.SlowStartDuration<br><br>* New error codes: InvalidSlowStartConfig.SlowStartEnabled.Malformed, InvalidSlowStartConfig.SlowStartDuration.Malformed, InvalidScheduler.SlowStartEnabledMismatch, Forbidden ||
|[ModifyServerGroupAttributes](https://docs.byteplus.com/en/docs/clb/ALB-ModifyServerGroupAttributes) |* New request parameters: SlowStartConfig.SlowStartEnabled, SlowStartConfig.SlowStartDuration<br><br>* New error codes: InvalidSlowStartConfig.SlowStartEnabled.Malformed, InvalidSlowStartConfig.SlowStartDuration.Malformed, InvalidScheduler.SlowStartEnabledMismatch, Forbidden ||

## April 2026

|API name |Release note |Associated features |
|---|---|---|
|[CreateServerGroup](https://docs.byteplus.com/en/docs/clb/ALB-CreateServerGroup) |* New request parameters: SlowStartConfig.SlowStartEnabled, SlowStartConfig.SlowStartDuration.<br><br>* New error codes: InvalidSlowStartConfig.SlowStartEnabled.Malformed, InvalidSlowStartConfig.SlowStartDuration.Malformed, InvalidScheduler.SlowStartEnabledMismatch, Forbidden. |Server group<br><br> |
|[ModifyServerGroupAttributes](https://docs.byteplus.com/en/docs/clb/ALB-ModifyServerGroupAttributes) |||
|[DescribeServerGroupAttributes](https://docs.byteplus.com/en/docs/clb/ALB-DescribeServerGroupAttributes) |New parameter data added: SlowStartConfig. ||
|[DescribeServerGroups](https://docs.byteplus.com/en/docs/clb/ALB-DescribeServerGroups) |||

## March 2026

|API name |Release note |Associated features |
|---|---|---|
|[CreateRules](https://docs.byteplus.com/en/docs/clb/ALB-CreateRules) |* New request parameter: Rules.N.RuleConditions.N.SourceIpConfig.Values.N.<br><br>* New request parameter: CorsConfig.<br><br>* Added new value Cors for RuleActions.<br><br>* Added values Cookie and SourceIp for Rules.N.RuleActions.N.Type. |Forwarding rule |
|[DescribeRules](https://docs.byteplus.com/en/docs/clb/ALB-DescribeRules) |||
|[ModifyRules](https://docs.byteplus.com/en/docs/clb/ALB-ModifyRules) |||

## January 2026

|API name |Release note |Associated features |
|---|---|---|
|[ModifyServerGroupBackendServers](https://docs.byteplus.com/en/docs/clb/ModifyServerGroupBackendServers) |New request parameter: Servers.N.InstanceId, which represents the ID of the ECS instance. |Server group |
|[CreateListener](https://docs.byteplus.com/en/docs/clb/ALB-CreateListener) |New request parameter: XRealIpEnabled, which indicates whether the listener is enabled or disabled obtaining the client source IP.<br><br> |Listener |
|[ModifyListenerAttributes](https://docs.byteplus.com/en/docs/clb/ALB-ModifyListenerAttributes) |||
|[DescribeListeners](https://docs.byteplus.com/en/docs/clb/ALB-DescribeListeners) |New response parameter: XRealIpEnabled, which indicates whether the listener enables or disables obtaining the client source IP.<br><br> ||
|[DescribeListenerAttributes](https://docs.byteplus.com/en/docs/clb/ALB-DescribeListenerAttributes) |||
|[DescribeRules](https://docs.byteplus.com/en/docs/clb/ALB-DescribeRules) |New response parameter: RedirectDomain, which indicates the redirect domain.<br><br> |Forwarding rule<br><br> |
|[DeleteRules](https://docs.byteplus.com/en/docs/clb/ALB-DeleteRules) |||
|[ModifyRules](https://docs.byteplus.com/en/docs/clb/ALB-ModifyRules) |New request parameter: Rules.N.RedirectConfig.RedirectDomain, which indicates the redirect domain. ||
|[CreateRules](https://docs.byteplus.com/en/docs/clb/ALB-CreateRules) |||

## July 2025

|API name |Release note |Associated features |
|---|---|---|
|[CreateRules](https://docs.byteplus.com/docs/clb/ALB-CreateRules) |* Modify request parameters: The valid range for `TrafficLimitQps` and `TrafficLimitConfig.QPS` has been adjusted from 100~150,000 to 100~400,000.<br><br>* New request parameter: `QueryStringConfig`, used to specify the query string in the forwarding condition. |Forwarding rule |
|[ModifyRules](https://docs.byteplus.com/docs/clb/ALB-ModifyRules) |||
|[DescribeRules](https://docs.byteplus.com/docs/clb/ALB-DescribeRules) |New response parameter: `QueryStringConfig`, which specifies the query string in forwarding conditions. ||
|[CreateListener](https://docs.byteplus.com/docs/clb/ALB-CreateListener) |* New request parameters:<br><br>   * `CACertificateSource`, which specifies the CA certificate source.<br><br>   * `PcaRootCACertificateId`, used to specify a private root CA certificate as the CA certificate.<br><br>   * `PcaSubCACertificateId`, used to specify a private sub CA certificate as the CA certificate.<br><br>* New error codes related to private CA certificates have been added. |Listener |
|[ModifyListenerAttributes](https://docs.byteplus.com/docs/clb/ALB-ModifyListenerAttributes) |||
|[DescribeListeners](https://docs.byteplus.com/docs/clb/ALB-DescribeListeners) |New response parameters: `CACertificateSource`, `PcaRootCACertificateId`, `PcaSubCACertificateId`, used to display private CA certificate information. ||
|[DescribeListenerAttributes](https://docs.byteplus.com/docs/clb/ALB-DescribeListenerAttributes) |||
|[CreateLoadBalancer](https://docs.byteplus.com/docs/clb/ALB-CreateLoadBalancer) |New request parameter `ClientToken`: Used to ensure request idempotency. |CLB instance |

## June 2025

|API name |Release note |Associated features |
|---|---|---|
|[CreateRules](https://docs.byteplus.com/docs/clb/ALB-CreateRules) |* New request parameters:<br><br>   * `MethodConfig`, which indicates the request method in the forwarding condition.<br><br>   * `FixedResponseConfig`, which indicates the fixed response in the forwarding action. |Forwarding rule |
|[DescribeRules](https://docs.byteplus.com/docs/clb/ALB-DescribeRules) |||
|[ModifyRules](https://docs.byteplus.com/docs/clb/ALB-ModifyRules) |||
|[CreateServerGroup](https://docs.byteplus.com/docs/clb/ALB-CreateServerGroup) |* New request parameter: `CrossZoneEnabled`, which indicates the configuration for the "cross\-zone load balancing" feature.<br><br>* Added error codes related to the new "Cross\-Zone Load Balancing" feature. |Server group |
|[ModifyServerGroupAttributes](https://docs.byteplus.com/docs/clb/ALB-ModifyServerGroupAttributes) |||
|[DescribeServerGroups](https://docs.byteplus.com/docs/clb/ALB-DescribeServerGroups) |New response parameter: `CrossZoneEnabled`, which indicates the configuration for the "cross\-zone load balancing" feature. ||
|[DescribeServerGroupAttributes](https://docs.byteplus.com/docs/clb/ALB-DescribeServerGroupAttributes) |||
|[AddServerGroupBackendServers](https://docs.byteplus.com/docs/clb/ALB-AddServerGroupBackendServers) |Added error codes related to the new "Cross\-Zone Load Balancing" feature. ||
|\-\- |ALB service endpoint and communication protocol update. For details, see [Call method](https://docs.byteplus.com/docs/clb/ALB-Signature-method).<br><br><br>* Service access method change: The previous global service endpoint has been changed to region\-specific service endpoints.<br><br>* Change in communication protocol: Currently only HTTPS is supported. |\-\- |

## April 2025

|API name |Release note |Associated features |
|---|---|---|
|[CreateAcl](https://docs.byteplus.com/docs/clb/ALB-CreateAcl) |New request parameter: `Tags` structure, which represents tags associated with the access control list. |Access control |
|[DescribeAcl](https://docs.byteplus.com/docs/clb/ALB-DescribeAcls) |||
|[DescribeAclAttributes](https://docs.byteplus.com/docs/clb/ALB-DescribeAclAttributes) |||
|[CreateCustomizedCfg](https://docs.byteplus.com/docs/clb/CreateCustomizedCfg) |* New request parameter: `Tags`, which allows filtering listeners by tags when querying the listener list.<br><br>* Modified request parameter: Updated the input rule for the add_header configuration item. The value now supports semicolons (;), meeting the need to specify multiple directives or parameters within certain response headers. |Custom configuration |
|[DescribeCustomizedCfg](https://docs.byteplus.com/docs/clb/DescribeCustomizedCfgs) |* New response parameter: `Tags`, which represents tags associated with the custom configuration.<br><br>* Modified response parameter: Updated the input rule for the add_header configuration item. The value now supports semicolons (;), meeting the need to specify multiple directives or parameters within certain response headers. ||
|[DescribeCustomizedCfgAttributes](https://docs.byteplus.com/docs/clb/DescribeCustomizedCfgAttributes) |||
|[ModifyCustomizedCfgAttributes](https://docs.byteplus.com/docs/clb/ModifyCustomizedCfgAttributes) |Modified request parameter: Updated the input rule for the add_header configuration item. The value now supports semicolons (;), meeting the need to specify multiple directives or parameters within certain response headers. ||
|[CreateHealthCheckTemplate](https://docs.byteplus.com/docs/clb/CreateHealthCheckTemplates) |New request parameters: `Tags` and `ProjectName`, which represents tags associated with the health check template and the project it belongs to, respectively. |Health check template |
|[DescribeHealthCheckTemplates](https://docs.byteplus.com/docs/clb/DescribeHealthCheckTemplates) |New response parameters: `Tags` and `ProjectName`, which represents tags associated with the health check template and the project it belongs to, respectively. ||
|[UploadCertificate](https://docs.byteplus.com/docs/clb/ALB-UploadCertificate) |New request parameter added: `Tags`, which represents tags associated with the certificate. |Certificate |
|[ReplaceCertificate](https://docs.byteplus.com/docs/clb/ReplaceCertificate) |||
|[ReplaceCACertificate](https://docs.byteplus.com/docs/clb/ReplaceCACertificate) |||
|[UploadCACertificate](https://docs.byteplus.com/docs/clb/UploadCACertificate) |||
|[DescribeCACertificates](https://docs.byteplus.com/docs/clb/DescribeCACertificates) |New response parameter: `Tags`, which indicates tags associated with the certificate. ||
|[DescribeCertificates](https://docs.byteplus.com/docs/clb/ALB-DescribeCertificates) |||
|[DescribeAllCertificates](https://docs.byteplus.com/docs/clb/DescribeAllCertificates) |||
|[DescribeServerGroups](https://docs.byteplus.com/docs/clb/ALB-DescribeServerGroups) |The API request rate limit has been updated to "up to 40 API requests per second". |Server group |

## March 2025

|API name |Release note |Associated features |
|---|---|---|
|[CreateLoadBalancer](https://docs.byteplus.com/docs/clb/ALB-CreateLoadBalancer) |New request parameter: `LoadBalancerEdition`, which indicates the version of the ALB instance.<br><br> |CLB instance |
|[DescribeLoadBalancers](https://docs.byteplus.com/docs/clb/ALB-DescribeLoadBalancers) |||
|[DescribeLoadBalancerAttributes](https://docs.byteplus.com/docs/clb/ALB-DescribeLoadBalancerAttributes) |||
|[CreateRules](https://docs.byteplus.com/docs/clb/ALB-CreateRules) |New request parameters and related error codes applicable to Standard Edition ALB instances have been added. |Forwarding rule |
|[ModifyRules](https://docs.byteplus.com/docs/clb/ALB-ModifyRules) |||
|[DescribeRules](https://docs.byteplus.com/docs/clb/ALB-DescribeRules) |New response parameters for Standard Edition ALB instances. ||
|[DescribeServerGroupBackendServers](https://docs.byteplus.com/docs/clb/DescribeServerGroupBackendServers) |New API: Added for querying information about backend servers within a specified server group. |Server group |
|[CreateServerGroup](https://docs.byteplus.com/docs/clb/ALB-CreateServerGroup) |Modified request parameters: Added gRPC to the valid values for `Protocol`, indicating that gRPC can be used as a backend communication protocol. ||

## December 2024

|API name |Release note |Associated features |
|---|---|---|
|[CloneLoadBalancer](https://docs.byteplus.com/docs/clb/CloneLoadBalancer) |Adding new APIs to clone ALB instances. |CLB instance |
|[ModifyLoadBalancerZones](https://docs.byteplus.com/docs/clb/ModifyLoadBalancerZones) |Adding new APIs to modify the availability zone of an ALB instance. ||
|[CreateLoadbalancer](https://docs.byteplus.com/docs/clb/ALB-CreateLoadBalancer) |* New request parameters: `ModificationProtectionStatus` and `ModificationProtectionReason`, which represent the configuration of the ALB instance modification protection feature and the reason for enabling it.<br><br>* New error codes: OperationDenied.DualStackUnsupported and OperationDenied.DualStackUnsupported. ||
|[ModifyLoadBalancerAttributes](https://docs.byteplus.com/docs/clb/ALB-ModifyLoadBalancerAttributes) |||
|[DescribeLoadBalancers](https://docs.byteplus.com/docs/clb/ALB-DescribeLoadBalancers) |New response parameters added: `ModificationProtectionStatus` and `ModificationProtectionReason`. ||
|[DescribeLoadBalancerAttributes](https://docs.byteplus.com/docs/clb/ALB-DescribeLoadBalancerAttributes) |||
|[CreateListener](https://docs.byteplus.com/docs/clb/ALB-CreateListener) |New error code: Forbidden. |Listener |
|[ModifyListenerAttributes](https://docs.byteplus.com/docs/clb/ALB-ModifyListenerAttributes) |* New request parameter: `AccessLogRecordCustomizedHeadersEnabled`, used to configure the "record custom headers in access logs" feature.<br><br>* New error code: InvalidLoadBalancer.InvalidStatus. ||
|[DescribeListeners](https://docs.byteplus.com/docs/clb/ALB-DescribeListeners) |New response parameter: `AccessLogRecordCustomizedHeadersEnabled`. ||
|[DescribeListenerAttributes](https://docs.byteplus.com/docs/clb/ALB-DescribeListenerAttributes) |||
|[CreateServerGroup](https://docs.byteplus.com/docs/clb/ALB-CreateServerGroup) |* New request parameters:<br><br>   * `Protocol`, which indicates the protocol used to forward requests to the backend server. The parameter value can be HTTP or HTTPS.<br><br>   * `HealthCheck.Port`, which indicates the port used to send requests to the backend server.<br><br>* New error code: InvalidProtocol.Malformed. |Server group |
|[ModifyServerGroupAttributes](https://docs.byteplus.com/docs/clb/ALB-ModifyServerGroupAttributes) |New request parameter: `HealthCheck.Port`, which specifies the port used to send requests to the backend server. ||
|[DescribeServerGroups](https://docs.byteplus.com/docs/clb/ALB-DescribeServerGroups) |New response parameters: `Protocol` and `HealthCheck.Port`. ||
|[DescribeServerGroupAttributes](https://docs.byteplus.com/docs/clb/ALB-DescribeServerGroupAttributes) |||
|[DeleteServerGroup](https://docs.byteplus.com/docs/clb/ALB-DeleteServerGroup) |New error code: InvalidServerGroupListener.InUse. ||
|[CreateHealthCheckTemplates](https://docs.byteplus.com/docs/clb/CreateHealthCheckTemplates) |New request parameter: `HealthCheckTemplates.N.HealthCheckPort`, which specifies the port used to send requests to backend servers for health checks. |Health check template |
|[ModifyHealthCheckTemplatesAttributes](https://docs.byteplus.com/docs/clb/ModifyHealthCheckTemplatesAttributes) |||
|[DescribeHealthCheckTemplates](https://docs.byteplus.com/docs/clb/DescribeHealthCheckTemplates) |New response parameter: HealthCheckPort. ||
|[TagResources](https://docs.byteplus.com/docs/clb/ALB-TagResources) |Modified request parameter: Updated `ResourceType`. It now allows lowercase letters, and domain name matching is case\-insensitive. |Tag |
|[UntagResources](https://docs.byteplus.com/docs/clb/ALB-UntagResources) |||
|[ListTagsForResources](https://docs.byteplus.com/docs/clb/ALB-ListTagsForResources) |New API: Added for querying user tags bound to a resource. ||

## September 2024

|API name |Release note |Associated features |
|---|---|---|
|[ModifyLoadBalancerAttributes](https://docs.byteplus.com/docs/clb/ALB-ModifyLoadBalancerAttributes) |* New request parameters:<br><br>   * `WafProtectionEnabled`, `WafInstanceId`, `WafProtectedDomain`, used to enable WAF for ALB.<br><br>   * `GlobalAccelerator` related fields: Represent configurations related to enabling Global Accelerator for an ALB instance.<br><br>* New error codes added. |CLB instance |
|[DescribeLoadBalancers](https://docs.byteplus.com/docs/clb/ALB-DescribeLoadBalancers) |New response parameters: `WafProtectionEnabled`, `WafInstanceId`, used to indicate fields related to whether WAF is enabled for the ALB instance. ||
|[DescribeLoadbalancerAttributes](https://docs.byteplus.com/docs/clb/ALB-DescribeLoadBalancerAttributes) |New response parameters:<br><br><br>* `WafProtectionEnabled` and `WafInstanceId`, used to indicate fields related to whether WAF is enabled for the ALB instance.<br><br>* `GlobalAccelerators` related fields represent the configuration information of the ALB instance regarding the Global Accelerator feature.<br><br>* `SniAutoMatch` indicates whether the instance supports automatically selecting extended certificates. ||
|[CreateListener](https://docs.byteplus.com/docs/clb/ALB-CreateListener) |* Modify request parameter: `DomainExtensions.N.Domain` updated description: If the instance supports automatic extended certificate selection (i.e., `SniAutoMatch` is `on`), then `DomainExtensions.N.Domain` must be passed as an empty string.<br><br>* New error codes added. |Listener |
|[ModifyListenerAttributes](https://docs.byteplus.com/docs/clb/ALB-ModifyListenerAttributes) |||
|[DescribeListenerAttributes](https://docs.byteplus.com/docs/clb/ALB-DescribeListenerAttributes) |Updated the description of the `Domain` response parameter based on the instance's support for automatic extended certificate selection, and added a new `San` response parameter. |Certificate |
|[DescribeCertificates](https://docs.byteplus.com/docs/clb/ALB-DescribeCertificates) |New response parameter `San`, used to display the additional domain list of the certificate. ||
|[DescribeCAcertificate](https://docs.byteplus.com/docs/clb/DescribeCACertificates) |||
|[DescribeAllCertificates](https://docs.byteplus.com/docs/clb/DescribeAllCertificates) |||
|[ReplaceCertificate](https://docs.byteplus.com/docs/clb/ReplaceCertificate) |New error codes added. | |
|[CreateCustomizedCfg](https://docs.byteplus.com/docs/clb/CreateCustomizedCfg) |New request parameter: `proxy_pass_header`, which forces transparent transmission of the selected backend response header. This header will not be overwritten by ALB's identical response headers. |Custom configuration |
|[ModifyCustomizedCfgAttributes](https://docs.byteplus.com/docs/clb/ModifyCustomizedCfgAttributes) |||
|[DescribeCustomizedCfg](https://docs.byteplus.com/docs/clb/DescribeCustomizedCfgs) |New response parameter: `proxy_pass_header`, which forces forwarding of the selected backend response header, which will not be overwritten by an ALB header with the same name. ||
|[DescribeCustomizedCfgAttributes](https://docs.byteplus.com/docs/clb/DescribeCustomizedCfgAttributes) |||

## July 2024

|API name |Release note |Associated features |
|---|---|---|
|[CreateServerGroup](https://docs.byteplus.com/docs/clb/ALB-CreateServerGroup) |* New request parameter: `Tags`, allowing you to add tags when creating a server group.<br><br>* New error codes: Tag\-related error codes. |Server group |
|[DescribeServerGroups](https://docs.byteplus.com/docs/clb/ALB-DescribeServerGroups) |* New request parameter: `TagFilters`, which allows you to filter server groups by tags when querying the server group list.<br><br>* New response parameter: `Tags`, which shows the server group's tag information in the response when querying server group details. ||
|[DescribeServerGroupAttributes](https://docs.byteplus.com/docs/clb/ALB-DescribeServerGroupAttributes) |New response parameter: `Tags`, which shows the server group's tag information in the response when querying server group details. ||
|[CreateListener](https://docs.byteplus.com/docs/clb/ALB-CreateListener) |* Modified request parameter: `DomainExtensions.N.Domain` updated to allow lowercase letters; domain matching is case\-insensitive.<br><br>* New request parameter: `Tags`, which allows tags to be added when creating a listener.<br><br>* New error codes: Tag\-related error codes. |Listener |
|[ModifyListenerAttributes](https://docs.byteplus.com/docs/clb/ALB-ModifyListenerAttributes) |Modified request parameter: `DomainExtensions.N.Domain` updated to allow lowercase letters; domain matching is case\-insensitive. ||
|[DescribeListeners](https://docs.byteplus.com/docs/clb/ALB-DescribeListeners) |* New request parameter: `TagFilters`, which allows filtering listeners by tags when querying the listener list.<br><br>* New response parameter: `Tags`, which shows the server group's tag information in the response when querying server group details. ||
|[DescribeListenerAttributes](https://docs.byteplus.com/docs/clb/ALB-DescribeListenerAttributes) |New response parameter: `Tags`. When querying the details of a specified listener, this parameter displays the tag information of the listener in the response. ||
|[CreateRules](https://docs.byteplus.com/docs/clb/ALB-CreateRules) |* Modified request parameter: `Rules.N.Domain`, now supports case\-insensitive domain names.<br><br>* New request parameter `ForwardGroupConfig`: When adding a forwarding rule to a listener, this parameter enables forwarding traffic to multiple server groups.<br><br>* New error codes added. |Forwarding rule |
|[ModifyRules](https://docs.byteplus.com/docs/clb/ALB-ModifyRules) |* New request parameter `ForwardGroupConfig`: When adding a forwarding rule to a listener, this parameter enables forwarding traffic to multiple server groups.<br><br>* New error codes added. ||
|[DescribeRules](https://docs.byteplus.com/docs/clb/ALB-DescribeRules) |New response parameter: `ForwardGroupConfig`. When adding forwarding rules to a listener, this parameter now supports forwarding traffic to multiple server groups. ||

## June 2024

|API name |Release note |Associated features |
|---|---|---|
|[CreateHealthCheckTemplates](https://docs.byteplus.com/docs/clb/CreateHealthCheckTemplates) |Modify the description of HTTP protocol related fields. |Health check template |
|[DescribeHealthCheckTemplates](https://docs.byteplus.com/docs/clb/DescribeHealthCheckTemplates) |||
|[ModifyHealthCheckTemplatesAttributes](https://docs.byteplus.com/docs/clb/ModifyHealthCheckTemplatesAttributes) |||
|[CreateServerGroup](https://docs.byteplus.com/docs/clb/ALB-CreateServerGroup) ||Server group |
|[DescribeServerGroups](https://docs.byteplus.com/docs/clb/ALB-DescribeServerGroups) |||
|[DescribeServerGroupAttributes](https://docs.byteplus.com/docs/clb/ALB-DescribeServerGroupAttributes) |||
|[ModifyServerGroupAttributes](https://docs.byteplus.com/docs/clb/ALB-ModifyServerGroupAttributes) |||
|\-\- |* Access log delivery to TOS is now an allowlist function.<br><br>* Added a new 403 error code, which is returned when a non\-allowlisted user attempts to use the log delivery to TOS feature. |Access Log |
|\-\- |* The add_header directive now includes the optional configuration item always. When always is used, the newly added custom response header will be included for all response status codes.<br><br>* A usage restriction has been added for add_header: duplicate header names are not supported.<br><br>* Support for more_set_input_headers, which adds the specified field(s) to the request headers. |Custom configuration |

## April 2024

|API name |Release note |Associated features |
|---|---|---|
|[CreateListener](https://docs.byteplus.com/docs/clb/ALB-CreateListener) |Added the following request parameters:<br><br><br>* `CertificateSource` field, which indicates the source of the default server certificate, effective only for HTTPS listeners.<br><br>* `CertCenterCertificateId` field, which indicates the certificate ID in the Certificate Center, effective only for HTTPS listeners when the certificate source is the Certificate Center.<br><br>* `DomainExtensions.N.CertificateSource` field, which indicates the source of the default SNI certificate.<br><br>* `DomainExtensions.N.CertCenterCertificateId` field which indicates the Certificate Center certificate ID, effective only for HTTPS listeners when the certificate source is the Certificate Center. |Listener |
|[ModifyListenerAttributes](https://docs.byteplus.com/docs/clb/ALB-ModifyListenerAttributes) |||
|[DescribeListeners](https://docs.byteplus.com/docs/clb/ALB-DescribeListeners) |* New request parameter: `Protocol` field supports filtering the listener list by listener protocol.<br><br>* New response parameters:<br><br>   * `CertCenterCertificateId` field, which indicates the certificate ID in the Certificate Center, effective only for HTTPS listeners when the certificate source is the Certificate Center.<br><br>   * A new `CertificateSource` field is added to the `DomainExtensions` structure, indicating the default SNI certificate source.<br><br>   * `CertCenterCertificateId` field: Represents the Certificate Center certificate ID. This field is only effective for HTTPS listeners when the certificate source is the Certificate Center. ||
|[DescribeListenerAttributes](https://docs.byteplus.com/docs/clb/ALB-DescribeListenerAttributes) |New response parameters:<br><br><br>* `CertCenterCertificateId` field, which indicates the certificate ID in the Certificate Center, effective only for HTTPS listeners when the certificate source is the Certificate Center.<br><br>* `CertificateSource` field indicates the source of the default SNI certificate.<br><br>* `CertCenterCertificateId` field: Represents the Certificate Center certificate ID. This field is only effective for HTTPS listeners when the certificate source is the Certificate Center. ||
|[ReplaceCertificate](https://docs.byteplus.com/docs/clb/ReplaceCertificate) |New request parameters:<br><br><br>* `CertificateSource` field indicates the source of the new replacement certificate.<br><br>* `CertCenterCertificateId` field represents the certificate ID from the Certificate Center. |Certificate |

## February 2024

|API name |Release note |Associated features |
|---|---|---|
|\-\- |Now supports initiating API calls online via API Explorer, eliminating the need to manage the signature generation process for quick results. See the document of each API for details. |\-\- |

## January 2024

|API name |Release note |Associated features |
|---|---|---|
|[CreateRules](https://docs.byteplus.com/docs/clb/ALB-CreateRules) |The rate limit range for forwarding rules has been adjusted. The valid range for the TrafficLimitQps parameter has been increased from 100–100,000 to 100–150,000. |Forwarding rule |
|[DescribeRules](https://docs.byteplus.com/docs/clb/ALB-DescribeRules) |||
|[ModifyRules](https://docs.byteplus.com/docs/clb/ALB-ModifyRules) |||

##
