---
title: "API release notes"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/API_release_history"
---

This topic describes the updates of AgentKit APIs.

## October 21, 2026

|Module |API name |Change record |
|---|---|---|
|Sandbox instance |[PauseSession](https://docs.byteplus.com/en/docs/agentkit/PauseSession_-_Pauses_a_sandbox_session_instance) |Add a new API. |
||[ResumeSession](https://docs.byteplus.com/en/docs/agentkit/ResumeSession_-_Resumes_a_sandbox_session_instance) ||

## September 14, 2026

|Module |API name |Change record |
|---|---|---|
|MCP |[ListMCPToolsets](https://docs.byteplus.com/en/docs/agentkit/ListMCPToolsets_-_Batch_queries_MCP_toolset_details) |* Added request parameter: GatewayInstanceId<br><br>* Added response parameters: EnableSharedInternetAccess, GatewayMode |
||[GetMCPService](https://docs.byteplus.com/en/docs/agentkit/GetMCPService_-_Queries_MCP_service_details) |Added response parameters<br><br><br>* EnableSharedInternetAccess<br><br>* GatewayInstanceName<br><br>* BackendAccessType<br><br>* GatewayMode |
||[ListMCPServices](https://docs.byteplus.com/en/docs/agentkit/ListMCPServices_-_Batch_queries_MCP_service_details) |* Added request parameter: GatewayInstanceId<br><br>* Added response parameters: EnableSharedInternetAccess, CanDelete, GatewayMode, InboundAuthorizerConfiguration structure |
||[CreateMCPService](https://docs.byteplus.com/en/docs/agentkit/CreateMCPService_-_Creates_MCP_services) |* Added request parameters: GatewayInstanceId, BackendAccessType, GatewayMode<br><br>* Updated all error code messages |
||[UpdateMCPToolset](https://docs.byteplus.com/en/docs/agentkit/UpdateMCPToolset_-_Modifies_MCP_toolset_configuration) |Added a new error code:<br><br>InvalidParameter.MCPServices, LimitExceeded.MaximumApiKeys, LimitExceeded.MinimumApiKeys, MissingParameter.ApiKeyLocation, MissingParameter.AuthorizerType, MissingParameter.DiscoveryUrl, MissingParameter.IsAllTools, MissingParameter.MCPServiceId, MissingParameter.MCPToolsetId, MissingParameter.Name, InvalidMCPService.NotFound |
||[DeleteMCPService](https://docs.byteplus.com/en/docs/agentkit/DeleteMCPService_-_Deletes_MCP_service) |Added a new error code:<br><br>InvalidResource.NotFound, OperationDenied.ResourceLocked |
||[UpdateMCPTools](https://docs.byteplus.com/en/docs/agentkit/UpdateMCPTools_-_Modifies_API_information_associated_with_an_MCP_service) |* Added request parameter: MCPToolsetId<br><br>* Error codes:<br><br>   * Updated: MissingParameter.MCPToolsetId<br><br>   * Added: MissingParameter.Tools |
||[GetMCPToolset](https://docs.byteplus.com/en/docs/agentkit/GetMCPToolset_-_Queries_MCP_toolset_details) |Added response parameter:<br><br><br>* EnableSharedInternetAccess<br><br>* GatewayInstanceName<br><br>* GatewayInstanceId<br><br>* GatewayMode |
||[DeleteMCPToolset](https://docs.byteplus.com/en/docs/agentkit/DeleteMCPToolset_-_Deletes_MCP_toolset) |Added error code: InvalidResource.NotFound |
||[CreateMCPToolset](https://docs.byteplus.com/en/docs/agentkit/CreateMCPToolset_-_Creates_MCP_toolset) |* Added request parameters: GatewayInstanceId, GatewayMode<br><br>* Error codes:<br><br>   * Added: InvalidMCPService.NotFound, InternalError<br><br>   * Updated: InvalidParameter.MCPServices, LimitExceeded.MaximumApiKeys, LimitExceeded.MinimumMCPServiceIds, LimitExceeded.MinimumSubnetIds, MissingParameter.ApiKeyLocation, MissingParameter.ApiKeys, MissingParameter.AuthorizerType, MissingParameter.DiscoveryUrl, MissingParameter.IsAllTools, MissingParameter.Key, MissingParameter.MCPServiceId, MissingParameter.MCPServiceIds, MissingParameter.Mode, MissingParameter.Name, MissingParameter.NetworkConfiguration, MissingParameter.NetworkConfigurations, MissingParameter.NetworkType, MissingParameter.Path, MissingParameter.VpcId |

## September 9, 2026

|Module |API name |Change record |
|---|---|---|
|Runtime |[CreateRuntime](https://docs.byteplus.com/en/docs/agentkit/CreateRuntime_-_Creates_a_runtime) |Added request parameter:<br><br><br>* GatewayMode<br><br>* Gatewayinstanceld |
||[GetRuntime](https://docs.byteplus.com/en/docs/agentkit/GetRuntime_-_Queries_runtime_details) |Added response parameter:<br><br><br>* GatewayMode<br><br>* Gatewayinstanceld |
||[ListRuntimes](https://docs.byteplus.com/en/docs/agentkit/ListRuntimes_-_Batch_queries_runtime_details) |Added response parameter:<br><br><br>* GatewayMode<br><br>* Gatewayinstanceld<br><br>* RequestModifierConfig structure<br><br>* TosMountConfig structure |

## July 17, 2026

|Module |API name |Change record |
|---|---|---|
|Runtime |[CreateRuntime](https://docs.byteplus.com/en/docs/agentkit/CreateRuntime_-_Creates_a_runtime)<br><br>[UpdateRuntime](https://docs.byteplus.com/en/docs/agentkit/UpdateRuntime_-_Modifies_runtime_configuration) |Added request parameter:<br><br><br>* RequestModifierConfig.FunctionId<br><br>* RequestModifierConfig.Path<br><br>* TosMountConfig.Credentials.AccessKeyId<br><br>* TosMountConfig.Credentials.SecretAccessKey<br><br>* TosMountConfig.EnableTos<br><br>* TosMountConfig.MountPoints.N.BucketName<br><br>* TosMountConfig.MountPoints.N.BucketPath<br><br>* TosMountConfig.MountPoints.N.Endpoint<br><br>* TosMountConfig.MountPoints.N.LocalMountPath<br><br>* TosMountConfig.MountPoints.N.ReadOnly |
||[GetRuntime](https://docs.byteplus.com/en/docs/agentkit/GetRuntime_-_Queries_runtime_details) |Added response parameters: RequestModifierConfig structure, TosMountConfig structure. |
||[ListRuntimeVersions](https://docs.byteplus.com/en/docs/agentkit/ListRuntimeVersions_-_Queries_details_of_all_runtime_versions) |Added a response parameter: TosMountConfig structure. |
||[GetRuntimeReleaseStatus](https://docs.byteplus.com/en/docs/agentkit/GetRuntimeReleaseStatus_-_Queries_runtime_release_status) |Added an error code: InvalidResourceStatus. |
||[GetRuntimeVersion](https://docs.byteplus.com/en/docs/agentkit/GetRuntimeVersion_-_Queries_details_of_a_specific_runtime_version) |Added a response parameter: TosMountConfig structure. |
||[GetRuntimeWebshellEndpoint](https://docs.byteplus.com/en/docs/agentkit/GetRuntimeWebshellEndpoint_-_Obtains_Webshell_URL_of_a_runtime_instance) |Added new APIs. |
|Tool |[CreateTool](https://docs.byteplus.com/en/docs/agentkit/CreateTool_-_Creates_tool)<br><br>[UpdateTool](https://docs.byteplus.com/en/docs/agentkit/UpdateTool_-_Modifies_tool_description?)<br><br>[GetTool](https://docs.byteplus.com/en/docs/agentkit/GetTool_-_Queries_tool_details) |Added request parameter: EnableSnapshot. |
||[ListTools](https://docs.byteplus.com/en/docs/agentkit/ListTools_-_Batch_queries_tool_details) |New response parameter: EnableSnapshot. |
||[CreateSession](https://docs.byteplus.com/en/docs/agentkit/CreateSession_-_Creates_tool_session_instance) |Added request parameter:<br><br><br>* Envs.N.Key<br><br>* Envs.N.Value<br><br>* ImageInfo.Command<br><br>* ImageInfo.Image<br><br>* ImageInfo.Port<br><br>* Metadata.N.Key<br><br>* Metadata.N.Type<br><br>* Metadata.N.Value |
||[DeleteSession](https://docs.byteplus.com/en/docs/agentkit/DeleteSession_-_Deletes_session_instances_of_a_tool) |Added error codes: MissingParameter.ToolId, <br><br>InvalidResource.NotFound |
||[GetSession](https://docs.byteplus.com/en/docs/agentkit/GetSession_-_Queries_tool_session_details) |Added response parameter: Metadata structure. |
||[ListSessions](https://docs.byteplus.com/en/docs/agentkit/ListSessions_-_Batch_queries_tool_session_details) |* Added request parameters: Metadata.N.Key, Metadata.N.Value.<br><br>* Added response parameter: Metadata structure. |

## July 10, 2026

|Module |API name |Change record |
|---|---|---|
|Tool |[CreateTool](https://docs.byteplus.com/en/docs/agentkit/CreateTool_-_Creates_tool)<br><br>[UpdateTool](https://docs.byteplus.com/en/docs/agentkit/UpdateTool_-_Modifies_tool_description?) |Modified a request parameter: ToolType supports the CodeEnv value. |
||[GetTool](https://docs.byteplus.com/en/docs/agentkit/GetTool_-_Queries_tool_details)<br><br>[ListTools](https://docs.byteplus.com/en/docs/agentkit/ListTools_-_Batch_queries_tool_details) |Modified a response parameter: ToolType supports the CodeEnv value. |

## March 6, 2026

|Module |API name |Change record |
|---|---|---|
|Runtime |[CreateRuntime](https://docs.byteplus.com/en/docs/agentkit/CreateRuntime_-_Creates_a_runtime)<br><br>[UpdateRuntime](https://docs.byteplus.com/en/docs/agentkit/UpdateRuntime_-_Modifies_runtime_configuration) |Added a request parameter: AgentSpaceId. |
||[GetRuntime](https://docs.byteplus.com/en/docs/agentkit/GetRuntime_-_Queries_runtime_details)<br><br>[ListRuntimes](https://docs.byteplus.com/en/docs/agentkit/ListRuntimes_-_Batch_queries_runtime_details) |Added a response parameter: AgentSpaceId. |
|A2A |[All](https://docs.byteplus.com/en/docs/agentkit/A2A) |Added APIs for managing A2A agents and A2A agent spaces. |

## February 28, 2026

|Module |API name |Change record |
|---|---|---|
|Runtime |[CreateRuntime](https://docs.byteplus.com/en/docs/agentkit/CreateRuntime_-_Creates_a_runtime) |* Added request parameters: SessionStoreId, Tags.N.Type, NetworkConfiguration.VpcConfiguration.EnableSharedInternetAccess.<br><br>* Updated descriptions of request parameters: RoleName, Tags.N.Value, Tags.N.Key.<br><br>* Updated error code: InvalidDescription.Malformed. |
||[UpdateRuntime](https://docs.byteplus.com/en/docs/agentkit/UpdateRuntime_-_Modifies_runtime_configuration) |* Added request parameters: SessionStoreId, Tags structure: Type.<br><br>* Updated error code description: InvalidDescription.Malformed |
||[ReleaseRuntime](https://docs.byteplus.com/en/docs/agentkit/ReleaseRuntime_-_Updates_runtime_version) |Added request parameters: Description, RollingStep, TargetTrafficWeight. |
||[GetRuntime](https://docs.byteplus.com/en/docs/agentkit/GetRuntime_-_Queries_runtime_details) |Added response parameters: SessionStoreId, Tags structure: Type, NetworkConfigurations.VpcConfiguration.EnableSharedInternetAccess. |
||[GetRuntimeVersion](https://docs.byteplus.com/en/docs/agentkit/GetRuntimeVersion_-_Queries_details_of_a_specific_runtime_version) |Added response parameters: Tags structure: Type, LinkedResources structure. |
||[ListRuntimes](https://docs.byteplus.com/en/docs/agentkit/ListRuntimes_-_Batch_queries_runtime_details) |Added response parameters: SessionStoreId, Tags structure: Type, NetworkConfigurations.VpcConfiguration.EnableSharedInternetAccess. |
||[UpdateRuntimeRelease](https://docs.byteplus.com/en/docs/agentkit/Update_runtime_release_-_Updates_runtime_release)<br><br>[ListRuntimeReleaseRecords](https://docs.byteplus.com/en/docs/agentkit/ListRuntimeReleaseRecords)<br><br>[AbortRuntimeRelease](https://docs.byteplus.com/en/docs/agentkit/AbortRuntimeRelease_-_Cancels_runtime_release)<br><br>[GetRuntimeReleaseStatus](https://docs.byteplus.com/en/docs/agentkit/GetRuntimeReleaseStatus_-_Queries_runtime_release_status)<br><br>[GetRuntimeInstanceLogs](https://docs.byteplus.com/en/docs/agentkit/GetRuntimeInstanceLogs_-_Queries_runtime_logs)<br><br>[ListRuntimeInstances](https://docs.byteplus.com/en/docs/agentkit/ListRuntimeInstances_-_Queries_runtime_instance_information) |Added new APIs. |
|Tool |[CreateTool](https://docs.byteplus.com/en/docs/agentkit/CreateTool_-_Creates_tool) |* Added request parameter:<br><br>   * ModelAgentName.<br><br>   * SkillSpaceId.<br><br>   * Tags.N.Type.<br><br>   * CpuMilli.<br><br>   * NetworkConfiguration.VpcConfiguration.EnableSharedInternetAccess.<br><br>   * TosMountConfig. structure:<br><br>      * EnableTos.<br><br>      * Credentials structure: AccessKeyId, SecretAccessKey.<br><br>      * MountPoints.N structure: BucketName, BucketPath, Endpoint, LocalMountPath, ReadOnly.<br><br>* Added an error code: InvalidModelAgentName.Malformed.<br><br>* Updated error code description: InvalidDescription.Malformed. |
||[UpdateTool](https://docs.byteplus.com/en/docs/agentkit/UpdateTool_-_Modifies_tool_description) |* Added request parameter:<br><br>   * ModelAgentName.<br><br>   * CpuMilli.<br><br>   * MemoryMb.<br><br>   * TosMountConfig. structure:<br><br>      * EnableTos.<br><br>      * Credentials structure: AccessKeyId, SecretAccessKey.<br><br>      * MountPoints.N structure: BucketName, BucketPath, Endpoint, LocalMountPath, ReadOnly.<br><br>* Updated description of request parameter: TosMountConfig.EnableTos.<br><br>* Added error codes: InvalidModelAgentName.Malformed, InvalidParameter.Port, InvalidParameter.ToolType, MissingParameter.ImageUrl.<br><br>* Updated error code description: InvalidDescription.Malformed. |
||[GetTool](https://docs.byteplus.com/en/docs/agentkit/GetTool_-_Queries_tool_details) |* Added response parameter:<br><br>   * ModelAgentName.<br><br>   * SkillSpaceId.<br><br>   * Tags structure: Type.<br><br>   * NetworkConfigurations.VpcConfiguration.EnableSharedInternetAccess.<br><br>   * TosMountConfig. structure:<br><br>      * EnableTos.<br><br>      * Credentials structure: AccessKeyId, SecretAccessKey.<br><br>      * MountPoints.N structure: BucketName, BucketPath, Endpoint, LocalMountPath, ReadOnly.<br><br>* Updated descriptions of response parameters: ReadOnly, EnableTos. |
||[ListTools](https://docs.byteplus.com/en/docs/agentkit/ListTools_-_Batch_queries_tool_details) |Added response parameters: ModelAgentName, Tags structure: Type, NetworkConfigurations.VpcConfiguration.EnableSharedInternetAccess. |
||[AsyncExecCommand](https://docs.byteplus.com/en/docs/agentkit/AsyncExecCommand_-_Asynchronously_executes_a_Shell_command_in_a_tool) |Added new API to asynchronously execute a Shell command in the sandbox environment of a tool. |
||[ViewAsyncCommand](https://docs.byteplus.com/en/docs/agentkit/ViewAsyncCommand_-_Queries_the_execution_result_of_an_asynchronous_command) |Added a new API to query the execution result of an asynchronous command, including the execution status, output, and exit code. |
||[CreateSession](https://docs.byteplus.com/en/docs/agentkit/CreateSession_-_Creates_tool_session_instance) |Added request parameters: TosMountPoints.N structure, InvalidParameter.DuplicateUserSessionId, InvalidParameter.Ttl, InvalidResourceStatus, InvalidResource.NotFound. |
||[GetSession](https://docs.byteplus.com/en/docs/agentkit/GetSession_-_Queries_tool_session_details) |* Added response parameters: TosMountPoints structure, SessionMeta structure.<br><br>* Added an error code: InvalidResource.NotFound. |
||[ListSessions](https://docs.byteplus.com/en/docs/agentkit/ListSessions_-_Batch_queries_tool_session_details) ||
||||
|SessionStore |[AddSessionStore](https://docs.byteplus.com/en/docs/agentkit/AddSessionStore_-_Imports_session_resources)<br><br>[DeleteSessionStore](https://docs.byteplus.com/en/docs/agentkit/DeleteSessionStore_-_Deletes_session_resources)<br><br>[GetSessionStore](https://docs.byteplus.com/en/docs/agentkit/GetSessionStore_-_Queries_session_resource_details)<br><br>[ListSessionStores](https://docs.byteplus.com/en/docs/agentkit/ListSessionStores_-_Batch_queries_session_resource_details) |Added new APIs. |
|Memory |[AddMemoryCollection](https://docs.byteplus.com/en/docs/agentkit/AddMemoryCollection_-_Imports_memories) |Updated error code description: InvalidDescription.Malformed. |
||[UpdateMemoryCollection](https://docs.byteplus.com/en/docs/agentkit/UpdateMemory_-_Modifies_memory_information) |* Updated error code description: InvalidDescription.Malformed.<br><br>* Added error codes: InvalidParameter.InvalidSubnets, InvalidParameter.Mem0VpcConfig, InvalidParameter.UpdateVpcNotAllowed, OperationDenied.TooManyVpcUpdates, InvalidResource.NotFound. |
||[GetMemoryCollection](https://docs.byteplus.com/en/docs/agentkit/GetMemoryCollection_-_Queries_memory_details) |* Added a response parameter: Tags structure: Type.<br><br>* Added an error code: InvalidResource.NotFound. |
||[ListMemoryCollections](https://docs.byteplus.com/en/docs/agentkit/ListMemoryCollections_-_Batch_queries_memory_details) |Added a response parameter: Tags structure: Type. |
|KnowledgeBase |[AddKnowledgeBase](https://docs.byteplus.com/en/docs/agentkit/AddKnowledgeBase_-_Imports_knowledge_bases)<br><br>[UpdateKnowledgeBase](https://docs.byteplus.com/en/docs/agentkit/UpdateKnowledgeBase_-_Updates_knowledge_base) |Updated error code description: InvalidDescription.Malformed. |
|MCP |[CreateMCPService](https://docs.byteplus.com/en/docs/agentkit/CreateMCPService_-_Creates_MCP_services) |* Added request parameter:<br><br>   * RoleName.<br><br>   * Tags.N.Type.<br><br>   * BackendConfiguration.EcsConfiguration.Instances structure: N.InstanceId, N.Ip, N.Port.<br><br>   * BackendConfiguration.VkeConfiguration structure: ClusterId, Namespace, Port, ServiceName.<br><br>   * OutboundAuthorizerConfiguration.Authorizer.IdentityAuthorizer structure: CredentialProviderName, ProviderType.<br><br>* Modified request parameter:<br><br>   * The BackendType parameter supports new values: ECS, VKE.<br><br>   * The OutboundAuthorizerConfiguration.AuthorizerType parameter supports a new value: Identity.<br><br>* Added error codes: LimitExceeded.MaximumPort, LimitExceeded.MinimumPort. |
||[UpdateMCPService](https://docs.byteplus.com/en/docs/agentkit/UpdateMCPService_-_Modifies_MCP_service_configuration) |* Added request parameter:<br><br>   * BackendConfiguration.EcsConfiguration.Instances structure: N.InstanceId, N.Ip, N.Port.<br><br>   * BackendConfiguration.VkeConfiguration structure: ClusterId, Namespace, Port, ServiceName.<br><br>   * OutboundAuthorizerConfiguration.Authorizer.IdentityAuthorizer structure: CredentialProviderName, ProviderType.<br><br>* Modified request parameter:<br><br>   * The BackendType parameter supports new values: ECS, VKE.<br><br>   * The OutboundAuthorizerConfiguration.AuthorizerType parameter supports a new value: Identity.<br><br>* Added error codes: LimitExceeded.MaximumPort, LimitExceeded.MinimumPort. |
||[ListMCPServices](https://docs.byteplus.com/en/docs/agentkit/ListMCPServices_-_Batch_queries_MCP_service_details) |Added a response parameter: Tags structure: Type. |
||[GetMCPService](https://docs.byteplus.com/en/docs/agentkit/GetMCPService_-_Queries_MCP_service_details) |* Added response parameter:<br><br>   * AssociatedMCPToolsets.<br><br>   * RoleName.<br><br>   * Tags structure: Type.<br><br>   * MCPService structure: EcsConfiguration, VkeConfiguration.<br><br>   * OutboundAuthorizerConfiguration structure: IdentityAuthorizer.<br><br>* Modified response parameters:<br><br>   * The BackendType parameter supports new values: ECS, VKE.<br><br>   * The OutboundAuthorizerConfiguration.AuthorizerType parameter supports a new value: Identity. |
||[CreateMCPToolset](https://docs.byteplus.com/en/docs/agentkit/CreateMCPToolset_-_Creates_MCP_toolset) |* Added request parameters: MCPServices.N.IsAllTools, MCPServices.N.MCPServiceId, MCPServices.N.MCPTools.N.Description, MCPServices.N.MCPTools.N.Name, MCPServices.N.MCPTools.N.Tags.N, Mode, Tags.N.Type.<br><br>* Added error codes: MissingParameter.MCPServiceId, MissingParameter.IsAllTools, MissingParameter.MCPServices, MissingParameter.Mode. |
||[ListMCPToolsets](https://docs.byteplus.com/en/docs/agentkit/ListMCPToolsets_-_Batch_queries_MCP_toolset_details) |Added response parameters: IsAllTools, Mode, Tags structure: Type. |
||[GetMCPToolset](https://docs.byteplus.com/en/docs/agentkit/GetMCPToolset_-_Queries_MCP_toolset_details) |Added response parameters: IsAllTools, Mode, Tags structure: Type. |
||[UpdateMCPToolset](https://docs.byteplus.com/en/docs/agentkit/UpdateMCPToolset_-_Modifies_MCP_toolset_configuration) |* Added request parameters: MCPServices.N.IsAllTools, MCPServices.N.MCPServiceId, MCPServices.N.MCPTools.N.Description, MCPServices.N.MCPTools.N.Name, MCPServices.N.MCPTools.N.Tags.N, Mode.<br><br>* Added error codes: MissingParameter.IsAllTools, MissingParameter.MCPServiceId. |
||[ListMCPToolsetTools](https://docs.byteplus.com/en/docs/agentkit/ListMCPToolsetTools_-_Queries_tools_in_an_MCP_toolset) |Added new API to query tools in an MCP toolset. |
|Skill |All |Added APIs for managing a Skill and Skills space. |
|Tags |[TagResources](https://docs.byteplus.com/en/docs/agentkit/TagResources_-_Adds_user_tags) |Added a request parameter: Tags.N.Type. |

## January 10, 2026

|Module |API name |Change record |
|---|---|---|
|AgentKit |All |For the first time, OpenAPI is opened, supporting creating, modifying, and deleting resources by calling OpenAPI. |
