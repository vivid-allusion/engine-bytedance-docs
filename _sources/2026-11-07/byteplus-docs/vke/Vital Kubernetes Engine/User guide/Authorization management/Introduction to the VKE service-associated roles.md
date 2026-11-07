---
title: "Introduction to the VKE service-associated roles"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Service-linked-roles-for-Vital-Kubernetes-Engine"
---

This topic describes the permissions contained within the roles associated with the services on VKE.

<span id="Ljuc5Hwv"></span>
## Background information

When using VKE, the IAM service creates a service\-associated role named **ServiceRoleForVKE**. The ServiceRoleForVKE role allows VKE to access resources within other BytePlus cloud products (e.g., ECS, CLB, and VPC). The policy attached to ServiceRoleForVKE contains multiple actions. This topic explains the meaning of each action.

<span id=".5LqR5pyN5Yqh5Zmo55u45YWz5p2D6ZmQ"></span>
## ECS\-related permissions


|**Permission name (Action)**  |**Description** |
|---|---|
|ecs:Describe\* |Query information about ECS. |
|ecs:Get\* |Query the operation and maintenance information about ECS. |
|ecs:CreateInstances |Create one or more ECS instances. |
|ecs:DeleteInstance |Delete an ECS instance. |
|ecs:DeleteVolume |Delete a volume. |
|ecs:AttachVolume |Mount a volume on an ECS instance. |
|ecs:DetachVolume |Detach a cloud disk from an ECS instance. |
|ecs:ExtendVolume |Scale out a volume. |
|ecs:ReplaceSystemVolume |Reinstall the system or replace the system volume for an ECS instance. |
|ecs:ModifyInstanceAttribute |Modify information about a specified ECS instance. |
|ecs:StartInstance |Start an ECS instance. |
|ecs:StopInstance |Stop an ECS instance. |
|ecs:BindAssumeRole |Bind Identity and Access Management (IAM) roles to one or more ECS instances. |
|ecs:UnbindAssumeRole |Unbind IAM roles from one or more ECS instances. |
|ecs:ListAssumeRoles |Obtain IAM roles that are already bound to one or more ECS instances. |
|ecs:DeleteTags |Remove labels from one or more ECS instances. |
|ecs:DescribeTags |Query information about labels already bound to one or more ECS instances. |
|ecs:CreateTags |Bind labels to one or more ECS instances. |
|ecs:DeleteInstancesWithEipAddresses |Delete an ECS instance bound to an elastic IP address (EIP). |
|ecs:CreateCommand |Create a custom Cloud Assistant Agent command. |
|ecs:ModifyCommand |Modify the content of a custom Cloud Assistant Agent command. |
|ecs:DeleteCommand |Delete a specified custom command. |
|ecs:DescribeCommands |Query the list of Cloud Assistant Agent commands. |
|ecs:RunCommand |Create batch jobs and immediately execute them on one or more ECS instances. |
|ecs:InvokeCommand |Create a batch job. |
|ecs:StopInvocation |Stop a running Cloud Assistant Agent command. |
|ecs:DescribeInvocations |Query the execution list and status of batch jobs. |
|ecs:DescribeInvocationInstances |Query the list of batch job execution objects. |
|ecs:DescribeInvocationResults |View the execution results of one or more batch jobs. |
|ecs:DescribeCloudAssistantStatus |Query the installation status of Cloud Assistant Agent on an instance. |


<span id=".56eB5pyJ572R57uc55u45YWz5p2D6ZmQ"></span>
## VPC\-related permissions


|**Permission name (Action)**  |**Description** |
|---|---|
|vpc:Describe\* |Query VPC information. |
|vpc:CreateSecurityGroup |Create a new security group. |
|vpc:CreateNetworkInterface |Create a secondary elastic network interface (ENI). |
|vpc:CreateRouteTable |Create a route table. |
|vpc:CreateRouteEntry |Add a custom route entry to a route table. |
|vpc:AllocateEipAddress |Apply for an elastic IP address (EIP). |
|vpc:AuthorizeSecurityGroupIngress |Add an inbound rule to a security group. |
|vpc:AuthorizeSecurityGroupEgress |Add an outbound rule to a security group. |
|vpc:RevokeSecurityGroupIngress |Delete an inbound security group rule. |
|vpc:RevokeSecurityGroupEgress |Delete an outbound security group rule. |
|vpc:ModifyNetworkInterfaceAttributes |Modify information about primary and secondary ENIs. |
|vpc:AttachNetworkInterface |Mount a secondary ENI on an ECS instance. |
|vpc:DetachNetworkInterface |Detach a secondary ENI from a specified ECS instance. |
|vpc:DeleteSecurityGroup |Delete a specified security group. |
|vpc:DeleteNetworkInterface |Delete a specified secondary ENI. |
|vpc:DeleteRouteTable |Delete a route table. |
|vpc:DeleteRouteEntry |Delete a route entry. |
|vpc:AssociateRouteTable |Associate a subnet with a specified route table. |
|vpc:AssociateEipAddress |Bind an EIP to a cloud resource. |
|vpc:DisassociateEipAddress |Disassociate an EIP from a cloud resource. |
|vpc:DisassociateRouteTable |Remove a route table from a subnet. |
|vpc:ReleaseEipAddress |Release an EIP. |
|vpc:AddBandwidthPackageIp |Add an EIP or IPv6 Internet bandwidth to a shared bandwidth package. |
|vpc:RemoveBandwidthPackageIp |Remove an EIP or IPv6 Internet bandwidth from a shared bandwidth package. |
|vpc:AssignIPv6Addresses |Allocate a private IPv6 address to a specified primary or secondary ENI. |
|vpc:UnassignIPv6Addresses |Delete a private IPv6 address of a specified ENI. |
|vpc:TagResources |Add user labels to resources. |
|vpc:UntagResources |Remove user labels from resources. |
|vpc:ListTagsForResources |Query label information that meets the specified criteria. |
|vpc:DisassociateTrunkInterface |Disassociate a trunk ENI from a specified branch ENI. |
|vpc:AssociateTrunkInterface |Associate a trunk ENI with a branch ENI. |


<span id=".6LSf6L295Z2H6KGh55u45YWz5p2D6ZmQ"></span>
## CLB\-related permissions


|**Permission name (Action)**  |**Description** |
|---|---|
|clb:Describe\* |Query information about Cloud Load Balancer (CLB). |
|clb:CreateLoadBalancer |Create a CLB instance. |
|clb:CreateRules |Add forwarding rules for a specified HTTP/HTTPS listener. |
|clb:CreateServerGroup |Create a back\-end server group. |
|clb:CreateListener |Create a listener for a specified CLB instance. |
|clb:AddServerGroupBackendServers |Add back\-end servers to a specified back\-end server group. |
|clb:ModifyLoadBalancerAttributes |Modify a specified CLB instance. |
|clb:ModifyListenerAttributes |Modify a specified listener. |
|clb:ModifyServerGroupAttributes |Modify a specified back\-end server group. |
|clb:ModifyRules |Replace the back\-end server group corresponding to the forwarding rule in a specified HTTP/HTTPS listener, or modify the description of the forwarding rule. |
|clb:RemoveServerGroupBackendServers |Remove back\-end servers from a specified back\-end server group. |
|clb:DeleteLoadBalancer |Delete a CLB instance. |
|clb:DeleteServerGroup |Delete a back\-end server group. |
|clb:DeleteListener |Delete a listener. |
|clb:DeleteRules |Delete forwarding rules in a specified HTTP/HTTPS listener. |
|clb:TagResources |Add user labels to CLB resources. |
|clb:UntagResources |Remove user labels from CLB resources. |
|clb:ListTagsForResources |Query label information of CLB resources that meet specified criteria. |


<span id=".5bqU55So5Z6L6LSf6L295Z2H6KGh55u45YWz5p2D6ZmQ"></span>
## ALB\-related permissions


|**Permission name (Action)**  |**Description** |
|---|---|
|alb:Describe\* |Query information about Application Load Balancer (ALB). |
|alb:CreateLoadBalancer |Create an ALB instance. |
|alb:CreateServerGroup |Create a server group. |
|alb:CreateListener |Create a listener. |
|alb:CreateRules |Add forwarding rules for a listener. |
|alb:AddServerGroupBackendServers |Add back\-end servers to a specified server group. |
|alb:ModifyLoadBalancerAttributes |Modify a specified ALB instance. |
|alb:ModifyServerGroupBackendServers |Modify back\-end servers in a specified server group. |
|alb:ModifyServerGroupAttributes |Modify the details of a specified server group. |
|alb:ModifyListenerAttributes |Modify a specified listener. |
|alb:ModifyRules |Modify forwarding rules. |
|alb:RemoveServerGroupBackendServers |Delete the back\-end servers of a specified server group. |
|alb:DeleteLoadBalancer |Delete an ALB instance. |
|alb:DeleteServerGroup |Delete a server group. |
|alb:DeleteListener |Delete a listener. |
|alb:DeleteRules |Delete forwarding rules. |
|alb:TagResources |Add user labels to ALB resources. |
|alb:UntagResources |Delete user labels for ALB resources. |


<span id=".bmF0Lee9keWFs-ebuOWFs-adg-mZkA=="></span>
## NAT Gateway\-related permissions


|**Permission name (Action)**  |**Description** |
|---|---|
|natgateway:CreateNatGateway |Create a NAT Gateway instance. |
|natgateway:CreateSnatEntry |Create a new Source Network Address Translation (SNAT) rule. |
|natgateway:Describe\* |Query information about NAT Gateway. |
|natgateway:DeleteNatGateway |Delete a specified NAT Gateway instance. |
|natgateway:DeleteSnatEntry |Delete a specified SNAT rule. |


<span id=".6ZWc5YOP5LuT5bqT55u45YWz5p2D6ZmQ"></span>
## CR\-related permissions


|**Permission name (Action)**  |**Description** |
|---|---|
|cr:List\* |View information about Container Registry (CR). |
|cr:Get\* |Query information about CR. |


<span id=".5paH5Lu25a2Y5YKo55u45YWz5p2D6ZmQ"></span>
## NAS\-related permissions


|**Permission name (Action)**  |**Description** |
|---|---|
|FileNAS:List\* |Query information about NAS. |


<span id=".5pel5b-X5pyN5Yqh55u45YWz5p2D6ZmQ"></span>
## TLS\-related permissions


|**Permission name (Action)**  |**Description** |
|---|---|
|tls:CreateProject |Create a log project. |
|tls:CreateTopic |Create a log topic. |
|tls:CreateIndex |Create an index. |
|tls:CreateRule |Create collection configurations. |
|tls:CreateHostGroup |Create a host group. |
|tls:Describe\* |Query information about logs. |
|tls:GetLogCollectorConfig |The collection endpoint periodically obtains collection configurations from Torch Log Service (TLS). |
|tls:LogCollectorHeartbeat |Report the collection endpoint heartbeat. |
|tls:PutLogs |Upload logs to a specified log topic. |
|tls:ModifyRule |Modify collection configurations. |
|tls:ApplyRuleToHostGroups |Associate collection configurations with the host group list. |
|tls:DeleteRuleFromHostGroups |Disassociate collection configurations from the host group list. |
|tls:DeleteRule |Delete collection configurations. |
|tls:ModifyIndex |Modify index configurations. |


<span id=".5a-56LGh5a2Y5YKo55u45YWz5p2D6ZmQ"></span>
## TOS\-related permissions


|**Permission name (Action)**  |**Description** |
|---|---|
|tos:ListBuckets |List all Torch Object Storage (TOS) buckets. |


<span id=".5by55oCn5Z2X5a2Y5YKo55u45YWz5p2D6ZmQ"></span>
## EBS\-related permissions


|**Permission name (Action)**  |**Description** |
|---|---|
|storage_ebs:Describe\* |Query information about EBS, which is also known as the volume. |
|storage_ebs:CreateVolume |Create a volume. |
|storage_ebs:AttachVolume |Mount a volume on an ECS instance. |
|storage_ebs:DetachVolume |Detach a cloud disk from an ECS instance. |
|storage_ebs:ExtendVolume |Scale out a volume. |
|storage_ebs:DeleteVolume |Delete a pay\-as\-you\-go data volume. |
|storage_ebs:CreateTags |Add labels to one or more cloud disks. |
|storage_ebs:DeleteTags |Remove user labels from one or more cloud disks. |
|storage_ebs:DescribeTags |Query volumes with bound labels. |


<span id=".6YCa55So55yL5p2_55u45YWz5p2D6ZmQ"></span>
## General dashboard\-related permissions


|**Permission name (Action)**  |**Description** |
|---|---|
|algalon:List\* |Query information related to the general dashboard (Algalon). |
|algalon:CreateDatasource |Create a general dashboard data source. |
|algalon:UpdateDatasource |Update a general dashboard data source. |
|algalon:DeleteDatasource |Delete a general dashboard data source. |


<span id=".5a655Zmo5pyN5Yqh55u45YWz5p2D6ZmQ"></span>
## VKE\-related permissions


|**Permission name (Action)**  |**Description** |
|---|---|
|vke:List\* |Query information about VKE. |
|vke:CreateAddon |Install add\-ons for a specified cluster. |
|vke:ListClusters |Query the details of clusters that meet the criteria. |
|vke:ListAddons |Query the details of installed add\-ons that meet the criteria. |
|vke:CreateDatasource |Create a data source for a general dashboard related to VKE. |
|vke:ListDatasources |Obtain the list of data sources for general dashboards related to VKE. |
|vke:ForwardKubernetesApi |Proxy and forward the native Kubernetes API. |
|vke:ForwardKubernetesReadApi |Proxy and forward Kubernetes\-native API ‌read operations. |
|vke:ForwardKubernetesWriteApi |Proxy and forward Kubernetes\-native API ‌write operations. |
|vke:DeleteAddon |Remove a specified add\-on from a specified cluster. |
|vke:ListKubernetesObservability |Query information about the cloud\-native observability feature of VKE. |
|vke:ListOperationEvents |Query the operation and maintenance event information of VKE clusters. |


<span id=".6K6_6Zeu5o6n5Yi255u45YWz5p2D6ZmQ"></span>
## IAM\-related permissions


|**Permission name (Action)**  |**Description** |
|---|---|
|iam:List\* |Query information about IAM. |
|iam:CreateRole |Create a role for an account. |
|iam:CreatePolicy |Create a user\-defined policy. |
|iam:UpdatePolicy |Update a specified user\-defined policy. |
|iam:AttachRolePolicy |Add a specified policy to a specified role. |
|iam:DetachRolePolicy |Unbind a role from a policy. |
|iam:DeleteRole |Delete a specified role. |
|iam:DeletePolicy |Delete a specified custom policy. |
|iam:CreateServiceLinkedRole |Create a service\-associated role for an account to complete cross\-service access authorization for a specified service. |


<span id=".5LqR55uR5o6n55u45YWz5p2D6ZmQ"></span>
## Cloud Monitor\-related permissions


|**Permission name (Action)**  |**Description** |
|---|---|
|Volc_Observe:PutEvents |Report cloud service events. |


<span id=".5omY566hLXByb21ldGhldXMt55u45YWz5p2D6ZmQ"></span>
## VMP\-related permissions


|**Permission name (Action)**  |**Description** |
|---|---|
|vmp:RemoteWrite |Store the collected data in a Vital Managed Service for Prometheus (VMP) workspace. |
|vmp:ListDatasources |Query the list of dashboard data sources. |
|vmp:DeleteDatasource |Delete a dashboard data source. |
|vmp:ListDatasource |Query a dashboard data source. |
|vmp:UpdateDatasource |Update a dashboard data source. |
|vmp:CreateDatasource |Create a dashboard data source. |
|vmp:ListWorkspaces |Query the list of workspaces. |
|vmp:CreateWorkspace |Create a workspace. |
|vmp:GetWorkspace |Obtain the details of a specified workspace. |
|vmp:QueryMetrics |Query instantaneous metric data. |
|vmp:QueryMetricsRange |Query metric data within a specific time range. |
|vmp:GetSeries |Obtain metric time series information. |
|vmp:GetLabels |Obtain metric time series labels. |
|vmp:GetLabelValues |Obtain the label values of metric time series. |


<span id=".5by55oCn5Ly457yp55u45YWz5p2D6ZmQ"></span>
## AS\-related permissions


|**Permission name (Action)**  |**Description** |
|---|---|
|auto_scaling:CreateScalingGroup |Create a scaling group of the Auto Scaling (AS) service. |
|auto_scaling:ModifyScalingGroup |Modify the basic information and the associated subnet of a specified scaling group. |
|auto_scaling:EnableScalingGroup |Start a specified scaling group. |
|auto_scaling:DisableScalingGroup |Disable a specified scaling group. |
|auto_scaling:DeleteScalingGroup |Delete a specified scaling group. |
|auto_scaling:DescribeScalingGroups |Obtain information about scaling groups. |
|auto_scaling:CreateScalingConfiguration |Create a scaling configuration. |
|auto_scaling:ModifyScalingConfiguration |Modify specified scaling configurations. |
|auto_scaling:EnableScalingConfiguration |Bind specified scaling configurations to a scaling group. |
|auto_scaling:DescribeScalingConfigurations |Query information about the scaling configuration. |
|auto_scaling:DescribeScalingInstances |Query ECS instance information in a scaling group. |
|auto_scaling:AttachInstances |Manually add one or more ECS instances to a scaling group. |
|auto_scaling:DetachInstances |Remove one or more ECS instances from a scaling group. |
|auto_scaling:RemoveInstances |Delete ECS instances in a scaling group. |
|auto_scaling:CreateLifecycleHook |Create a lifecycle hook. |
|auto_scaling:DescribeLifecycleActivities |Query lifecycle hooks. |
|auto_scaling:CompleteLifecycleActivity |Manually end the suspended state of a lifecycle activity. |
|auto_scaling:DescribeScalingActivities |Query scaling logs. |
|auto_scaling:TagResources |Add user labels to multiple scaling groups. |
|auto_scaling:UntagResources |Remove user labels from a scaling group. |
|auto_scaling:ListTagResources |Query the user labels of a scaling group. |


<span id=".5aSn5pWw5o2u5paH5Lu25a2Y5YKo55u45YWz5p2D6ZmQ"></span>
## CloudFS\-related permissions


|**Permission name (Action)**  |**Description** |
|---|---|
|cfs:ListFs |Query the list of Cloud File System (CloudFS) instances. |
|cfs:ListNs |Query the list of namespaces for a data lake instance. |
