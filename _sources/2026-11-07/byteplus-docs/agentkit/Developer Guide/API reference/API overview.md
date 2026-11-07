---
title: "API overview"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/API_overview"
---

AgentKit provides the following APIs.

## Agent runtime

|API name |Feature |
|---|---|
|[CreateRuntime](https://docs.byteplus.com/en/docs/agentkit/CreateRuntime_-_Creates_a_runtime) |Creates an agent runtime. |
|[UpdateRuntime](https://docs.byteplus.com/en/docs/agentkit/UpdateRuntime_-_Modifies_runtime_configuration) |Modifies agent runtime configuration. |
|[ReleaseRuntime](https://docs.byteplus.com/en/docs/agentkit/ReleaseRuntime_-_Updates_runtime_version) |Updates the version of an agent runtime. |
|[DeleteRuntime](https://docs.byteplus.com/en/docs/agentkit/DeleteRuntime_-_Deletes_runtime) |Deletes an agent runtime. |
|[GetRuntime](https://docs.byteplus.com/en/docs/agentkit/GetRuntime_-_Queries_runtime_details) |Queries the details of an agent runtime. |
|[GetRuntimeVersion](https://docs.byteplus.com/en/docs/agentkit/GetRuntimeVersion_-_Queries_details_of_a_specific_runtime_version) |Queries the details of a specific agent runtime version. |
|[ListRuntimes](https://docs.byteplus.com/en/docs/agentkit/ListRuntimes_-_Batch_queries_runtime_details) |Queries details of all agent runtime versions. |
|[ListRuntimeVersions](https://docs.byteplus.com/en/docs/agentkit/ListRuntimeVersions_-_Queries_details_of_all_runtime_versions) |Queries details of multiple runtimes using custom filter conditions. |
|[GetRuntimeInstanceLogs](https://docs.byteplus.com/en/docs/agentkit/GetRuntimeInstanceLogs_-_Queries_runtime_logs) |Queries runtime logs. |
|[ListRuntimeInstances](https://docs.byteplus.com/en/docs/agentkit/ListRuntimeInstances_-_Queries_runtime_instance_information) |Queries runtime instance information. |
|[UpdateRuntimeRelease](https://docs.byteplus.com/en/docs/agentkit/Update_runtime_release_-_Updates_runtime_release) |You can call this operation to update the runtime release (update release traffic percentage). |
|[AbortRuntimeRelease](https://docs.byteplus.com/en/docs/agentkit/AbortRuntimeRelease_-_Cancels_runtime_release) |Cancels runtime release. |
|[ListRuntimeReleaseRecords](https://docs.byteplus.com/en/docs/agentkit/ListRuntimeReleaseRecords) |You can call this operation to batch query runtime release record​ details using custom filter conditions. |
|[GetRuntimeReleaseStatus](https://docs.byteplus.com/en/docs/agentkit/GetRuntimeReleaseStatus_-_Queries_runtime_release_status) |You can call this operation to query the runtime release status. |
|[GetRuntimeWebshellEndpoint](https://docs.byteplus.com/en/docs/agentkit/GetRuntimeWebshellEndpoint_-_Obtains_Webshell_URL_of_a_runtime_instance) |Obtains the Webshell URL of a runtime instance. |

## Sandbox template and sandbox tool

|API name |Feature |
|---|---|
|[CreateTool](https://docs.byteplus.com/en/docs/agentkit/CreateTool_-_Creates_tool) |Creates a sandbox template. |
|[UpdateTool](https://docs.byteplus.com/en/docs/agentkit/UpdateTool_-_Modifies_tool_description) |Modifies the description of a sandbox template. |
|[DeleteTool](https://docs.byteplus.com/en/docs/agentkit/DeleteTool_-_Deletes_tool) |Deletes a sandbox template. |
|[GetTool](https://docs.byteplus.com/en/docs/agentkit/GetTool_-_Queries_tool_details) |Queries sandbox template details. |
|[ListTools](https://docs.byteplus.com/en/docs/agentkit/ListTools_-_Batch_queries_tool_details) |Batch queries sandbox template details using custom filter conditions. |
|[InvokeTool](https://docs.byteplus.com/en/docs/agentkit/InvokeTool_-_Executes_command_in_a_tool) |Executes commands in a sandbox template. |
|[AsyncExecCommand](https://docs.byteplus.com/en/docs/agentkit/AsyncExecCommand_-_Asynchronously_executes_a_Shell_command_in_a_tool) |Executes a shell command asynchronously in a sandbox instance. |
|[ViewAsyncCommand](https://docs.byteplus.com/en/docs/agentkit/ViewAsyncCommand_-_Queries_the_execution_result_of_an_asynchronous_command) |Queries the execution result of an asynchronous command. |
|[CreateSession](https://docs.byteplus.com/en/docs/agentkit/CreateSession_-_Creates_tool_session_instance) |Creates a session instance for a sandbox instance. |
|[DeleteSession](https://docs.byteplus.com/en/docs/agentkit/DeleteSession_-_Deletes_session_instances_of_a_tool) |Deletes the session instance of a sandbox instance. |
|[GetSession](https://docs.byteplus.com/en/docs/agentkit/GetSession_-_Queries_tool_session_details) |Queries session details of a sandbox instance. |
|[ListSessions](https://docs.byteplus.com/en/docs/agentkit/ListSessions_-_Batch_queries_tool_session_details) |Batch queries tool session details using custom filter conditions. |
|[SetSessionTtl](https://docs.byteplus.com/en/docs/agentkit/SetSessionTtl_-_Configures_TTL_for_session_instance) |Configures TTL for a session instance. |
|[GetSessionLogs](https://docs.byteplus.com/en/docs/agentkit/GetSessionLogs_-_Views_tool_session_logs) |Views session logs. |
|[PauseSession](https://docs.byteplus.com/en/docs/agentkit/PauseSession_-_Pauses_a_sandbox_session_instance) |Suspends a sandbox session instance. |
|[ResumeSession](https://docs.byteplus.com/en/docs/agentkit/ResumeSession_-_Resumes_a_sandbox_session_instance) |Restores a sandbox session instance. |

## A2A Center

|API name |Feature |
|---|---|
|[CreateA2aSpace](https://docs.byteplus.com/en/docs/agentkit/CreateA2aSpace_-_Creates_an_A2A_agent_space) |Create an A2A agent space. |
|[UpdateA2aSpace](https://docs.byteplus.com/en/docs/agentkit/UpdateA2aSpace_-_Updates_an_A2A_agent_space) |Update an A2A agent space. |
|[ListA2aSpaces](https://docs.byteplus.com/en/docs/agentkit/ListA2aSpaces_-_Batch_queries_A2A_agent_spaces) |Batch query A2A agent spaces. |
|[GetA2aSpace](https://docs.byteplus.com/en/docs/agentkit/GetA2aSpace_-_Queries_details_of_an_A2A_agent_space) |Queries details of an A2A agent space. |
|[DeleteA2aSpace](https://docs.byteplus.com/en/docs/agentkit/DeleteA2aSpace_-_Deletes_an_A2A_agent_space) |Delete an A2A agent space. |
|[CreateA2aAgent](https://docs.byteplus.com/en/docs/agentkit/CreateA2aAgent_-_Creates_an_A2A_agent) |Create an A2A agent. |
|[UpdateA2aAgent](https://docs.byteplus.com/en/docs/agentkit/UpdateA2aAgent_-_Updates_an_A2A_agent) |Update an A2A agent. |
|[ListA2aAgents](https://docs.byteplus.com/en/docs/agentkit/ListA2aAgents_-_Batch_queries_A2A_agents) |Batch query A2A agents. |
|[GetA2aAgent](https://docs.byteplus.com/en/docs/agentkit/GetA2aAgent_-_Queries_details_of_an_A2A_agent) |Query details of an A2A agent. |
|[DeleteA2aAgent](https://docs.byteplus.com/en/docs/agentkit/DeleteA2aAgent_-_Deletes_an_A2A_agent) |Delete an A2A agent. |
|[ListA2aAgentVersions](https://docs.byteplus.com/en/docs/agentkit/ListA2aAgentVersions_-_Batch_queries_A2A_agent_versions) |Batch query A2A agent versions. |
|[GetA2aAgentVersion](https://docs.byteplus.com/en/docs/agentkit/GetA2aAgentVersion_-_Queries_version_details_of_an_A2A_agent) |Query version details of an A2A agent. |
|[DeleteA2aAgentVersion](https://docs.byteplus.com/en/docs/agentkit/DeleteA2aAgentVersion_-_Deletes_an_A2A_agent_version) |Deletes an A2A agent Version. |
|[SearchAgentCards](https://docs.byteplus.com/en/docs/agentkit/SearchAgentCards_-_Queries_agents_via_intent_recognition) |Queries agents based on semantic retrieval. |

## SessionStore

|API name |Feature |
|---|---|
|[AddSessionStore](https://docs.byteplus.com/en/docs/agentkit/AddSessionStore_-_Imports_session_resources) |Imports session resources. |
|[DeleteSessionStore](https://docs.byteplus.com/en/docs/agentkit/DeleteSessionStore_-_Deletes_session_resources) |You can call this operation to delete session resources. |
|[GetSessionStore](https://docs.byteplus.com/en/docs/agentkit/GetSessionStore_-_Queries_session_resource_details) |You can call this operation to query details of a session resource. |
|[ListSessionStores](https://docs.byteplus.com/en/docs/agentkit/ListSessionStores_-_Batch_queries_session_resource_details) |You can batch query session resource details using custom filter conditions. |

## Memory

|API name |Feature |
|---|---|
|[AddMemoryCollection](https://docs.byteplus.com/en/docs/agentkit/AddMemoryCollection_-_Imports_memories) |Imports memories. |
|[UpdateMemoryCollection](https://docs.byteplus.com/en/docs/agentkit/UpdateMemory_-_Modifies_memory_information) |Modifies memory description and strategy information. |
|[DeleteMemoryCollection](https://docs.byteplus.com/en/docs/agentkit/DeleteMemoryCollection_-_Deletes_memory) |Deletes a memory. |
|[GetMemoryCollection](https://docs.byteplus.com/en/docs/agentkit/GetMemoryCollection_-_Queries_memory_details) |Queries memory details. |
|[GetMemoryConnectionInfo](https://docs.byteplus.com/en/docs/agentkit/GetMemoryConnectionInfo_-_Queries_memory_LTM_retrieval_strategy_details) |You can call this API to query the LTM extraction strategy details of a memory. |
|[ListMemoryCollections](https://docs.byteplus.com/en/docs/agentkit/ListMemoryCollections_-_Batch_queries_memory_details) |Batch queries memory details using custom filter conditions. |

## Knowledge base

|API name |Feature |
|---|---|
|[AddKnowledgeBase](https://docs.byteplus.com/en/docs/agentkit/AddKnowledgeBase_-_Imports_knowledge_bases) |Imports knowledge bases. |
|[UpdateKnowledgeBase](https://docs.byteplus.com/en/docs/agentkit/UpdateKnowledgeBase_-_Updates_knowledge_base) |Updates knowledge bases. |
|[DeleteKnowledgeBase](https://docs.byteplus.com/en/docs/agentkit/DeleteKnowledgeBase_-_Deletes_knowledge_base) |Deletes a knowledge base. |
|[GetKnowledgeBase](https://docs.byteplus.com/en/docs/agentkit/GetKnowledgeBase_-_Queries_knowledge_base_information) |Queries knowledge base information. |
|[GetKnowledgeConnectionInfo](https://docs.byteplus.com/en/docs/agentkit/GetKnowledgeConnectionInfo_-_Queries_knowledge_details) |You can call this API to query knowledge base details. |
|[ListKnowledgeBases](https://docs.byteplus.com/en/docs/agentkit/ListKnowledgeBases_-_Batch_queries_knowledge_base_details) |Batch queries knowledge base details using custom filter conditions. |

## Gateway MCP

|API name |Feature |
|---|---|
|[CreateMCPService](https://docs.byteplus.com/en/docs/agentkit/CreateMCPService_-_Creates_MCP_services) |Creates an MCP service. |
|[UpdateMCPService](https://docs.byteplus.com/en/docs/agentkit/UpdateMCPService_-_Modifies_MCP_service_configuration) |Modifies MCP service configuration. |
|[UpdateMCPTools](https://docs.byteplus.com/en/docs/agentkit/UpdateMCPTools_-_Modifies_API_information_associated_with_an_MCP_service) |Modifies information of the API associated with an MCP service. |
|[DeleteMCPService](https://docs.byteplus.com/en/docs/agentkit/DeleteMCPService_-_Deletes_MCP_service) |Deletes an MCP service. |
|[GetMCPService](https://docs.byteplus.com/en/docs/agentkit/GetMCPService_-_Queries_MCP_service_details) |Queries MCP service details. |
|[ListMCPServices](https://docs.byteplus.com/en/docs/agentkit/ListMCPServices_-_Batch_queries_MCP_service_details) |Batch queries MCP service details. |
|[CreateMCPToolset](https://docs.byteplus.com/en/docs/agentkit/CreateMCPToolset_-_Creates_MCP_toolset) |Creates an MCP toolset. |
|[UpdateMCPToolset](https://docs.byteplus.com/en/docs/agentkit/UpdateMCPToolset_-_Modifies_MCP_toolset_configuration) |Modifies MCP toolset configuration. |
|[DeleteMCPToolset](https://docs.byteplus.com/en/docs/agentkit/DeleteMCPToolset_-_Deletes_MCP_toolset) |Deletes an MCP toolset. |
|[GetMCPToolset](https://docs.byteplus.com/en/docs/agentkit/GetMCPToolset_-_Queries_MCP_toolset_details) |Batch queries MCP service details using custom filter conditions. |
|[ListMCPToolsets](https://docs.byteplus.com/en/docs/agentkit/ListMCPToolsets_-_Batch_queries_MCP_toolset_details) |Batch queries MCP toolset details using custom filter conditions. |
|[ListMCPToolsetTools](https://docs.byteplus.com/en/docs/agentkit/ListMCPToolsetTools_-_Queries_tools_in_an_MCP_toolset) |Query tools in an MCP toolset. |

## Gateway Skill

|API name |Feature |
|---|---|
|[CreateSkill](https://docs.byteplus.com/en/docs/agentkit/CreateSkill_-_Create_a_Skill) |Creates a Skill. |
|[UpdateSkill](https://docs.byteplus.com/en/docs/agentkit/UpdateSkill_-_Updates_Skill) |Updates a Skill. |
|[PublishSkillToSkillSpace](https://docs.byteplus.com/en/docs/agentkit/PublishSkillToSkillSpace_-_Publishes_Skill_to_a_Skills_space) |Publishes a Skill to a Skills space. |
|[RemoveSkillFromSkillSpace](https://docs.byteplus.com/en/docs/agentkit/RemoveSkillFromSkillSpace_-_Removes_Skill_from_a_Skills_space) |Removes a Skill from a Skills space. |
|[GetSkill](https://docs.byteplus.com/en/docs/agentkit/GetSkill_-_Queries_Skill_details) |Queries Skill details. |
|[ListSkills](https://docs.byteplus.com/en/docs/agentkit/ListSkills_-_Batch_queries_details_of_multiple_Skills) |Queries details of multiple Skills at one time. |
|[GetSkillVersion](https://docs.byteplus.com/en/docs/agentkit/GetSkillVersion_-_Queries_details_of_a_Skill_version) |Queries details of a Skill version. |
|[ListSkillVersions](https://docs.byteplus.com/en/docs/agentkit/ListSkillVersions_-_Batch_queries_Skill_version_information) |Queries version information of multiple Skills at one time. |
|[GetSkillInfo](https://docs.byteplus.com/en/docs/agentkit/GetSkillInfo_-_Queries_the_version_details_of_a_Skill_added_to_a_Skills_space) |Queries version details of a Skill in a specific space. |
|[ListSkillSpacesBySkill](https://docs.byteplus.com/en/docs/agentkit/ListSkillSpacesBySkill_-_Queries_details_of_the_Skills_spaces_to_which_a_Skill_has_been_added) |Queries details of the Skills space to which a Skill is added. |
|[ListSkillsBySkillSpace](https://docs.byteplus.com/en/docs/agentkit/ListSkillsBySkillSpace_-_Queries_version_details_of_a_Skill_in_a_specific_space) |Queries version details of Skills added to a Skills space. |
|[GetSharingSkill](https://docs.byteplus.com/en/docs/agentkit/GetSharingSkill_-_Queries_preset_Skill_details) |Queries preset Skill details. |
|[ListSharingSkills](https://docs.byteplus.com/en/docs/agentkit/ListSharingSkills_-_Batch_queries_shared_Skill_details) |Batch queries preset Skill details. |
|[GetSharingSkillVersion](https://docs.byteplus.com/en/docs/agentkit/GetSharingSkillVersion_-_Queries_preset_Skill_version_details) |Queries preset Skill version details. |
|[ListSharingSkillVersions](https://docs.byteplus.com/en/docs/agentkit/ListSharingSkillVersions_-_Batch_queries_preset_Skill_version_information) |Batch queries version information of preset Skills. |
|[ListSkillSpacesBySharingSkill](https://docs.byteplus.com/en/docs/agentkit/ListSkillSpacesBySharingSkill_-_Queries_details_of_the_Skills_spaces_to_which_a_Skill_has_been_added) |Queries details of the Skills space to which a preset Skill has been added. |
|[DeleteSkill](https://docs.byteplus.com/en/docs/agentkit/DeleteSkill_-_Deletes_a_Skill) |Deletes a Skill. |
|[CreateSkillSpace](https://docs.byteplus.com/en/docs/agentkit/CreateSkillSpace_-_Creates_a_Skills_space) |Creates a Skills space. |
|[UpdateSkillSpace](https://docs.byteplus.com/en/docs/agentkit/UpdateSkillSpace_-_Updates_Skills_space) |Updates a Skills space. |
|[GetSkillSpace](https://docs.byteplus.com/en/docs/agentkit/GetSkillSpace_-_Queries_details_of_a_Skills_space) |Query details of a Skills space. |
|[ListSkillSpaces](https://docs.byteplus.com/en/docs/agentkit/ListSkillSpaces_-_Batch_queries_Skills_space_details) |Batch queries Skills space details. |
|[ListSkillsBySpaceId](https://docs.byteplus.com/en/docs/agentkit/ListSkillsBySpaceId_-_Queries_basic_information_about_added_skills_via_Skills_space) |Queries the basic information of a Skill added to a Skills space by Skills space name. |
|[DeleteSkillSpace](https://docs.byteplus.com/en/docs/agentkit/DeleteSkillSpace_-_Deletes_Skills_space) |Deletes a Skills space. |

## Tag

|API name |Feature |
|---|---|
|[TagResources](https://docs.byteplus.com/en/docs/agentkit/TagResources_-_Adds_user_tags) |Adds custom tags. |
|[UntagResources](https://docs.byteplus.com/en/docs/agentkit/UntagResources_-_Deletes_user_tags) |Deletes custom tag. |
|[ListTagsForResources](https://docs.byteplus.com/en/docs/agentkit/ListTagsForResources_-_Queries_resources_with_tags) |Queries resources with tags. |
