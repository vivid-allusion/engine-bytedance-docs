---
title: "Managing agent versions"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Managing_A2A_agent_versions"
---

The platform provides version management for A2A agents, making it easy for you to view the configuration of the current A2A agent version at any time. This topic describes how to create, view, or delete the version information of an A2A agent.

<span id="yzGip2G7"></span>
## Background information

As A2A agents iterate continuously, protocol declarations, service addresses, capability descriptions, and runtime configurations may change. If version boundaries are unclear, the agent service provider cannot track the change history, and callers cannot confirm which version of the agent they are accessing. This can easily cause an issue where the configuration has been updated but the caller still obtains old version information.

<span id="wOg8rEdX"></span>
## Prerequisites

An A2A agent has been registered. [Learn more](https://docs.byteplus.com/en/docs/agentkit/Registering_A2A_agents)

<span id="EOJZQZpd"></span>
## Create a version

To create a new A2A agent version, specify the new version number through the `version` parameter when updating the JSON file. Once the new version is created, the platform automatically sets it as the default version, and subsequent agent calls will use this version by default. [Learn more](https://docs.byteplus.com/en/docs/agentkit/Updating_A2A_agent_JSON_file)

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Only A2A agents registered with source as <strong>Custom</strong> support creating versions. <a href="https://docs.byteplus.com/en/docs/agentkit/Registering_A2A_agents">Learn more</a></div>


<span id="rCwUNteR"></span>
## View version information

You can view the JSON code of the full configurations for each A2A agent version (such as agent name, protocol version, and provider).


1. Log in to the [AgentKit console](https://console.byteplus.com/agentkit). 

2. In the left\-side navigation pane, select "Basic Components \> A2A Center".

3. From the A2A agent space drop\-down list, select the target agent space.

4. Click the target agent name and select the "Version management" tab. You can view the default version currently used by the agent and the versions that have been created.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">When the agent registration source is <strong>Custom</strong>, you can view the information about all its versions.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">When the agent registration source is <strong>Agent Runtime</strong>, you can only view the latest information.   </div>
   

5. By clicking the "View" button in the "Actions" column of the target version, you can view the JSON code information for the full configurations (such as agent name, protocol version, and provider) of the corresponding agent version.


<span id="bQXcjMuC"></span>
### Delete versions

You can delete historical versions of A2A agents that are no longer used to prevent invalid versions from affecting daily O&M and troubleshooting.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">You can only delete A2A agent versions whose registration source is <strong>Custom</strong>.</div>


* <div data-tips="true" data-tips-type="warning">Deletion is irreversible. Please evaluate carefully before deleting versions that have been used in production or have carried critical traffic.</div>


1. Log in to the [AgentKit console](https://console.byteplus.com/agentkit). 

2. In the left\-side navigation pane, select "Basic Components \> A2A Center".

3. From the A2A agent space drop\-down list, select the target agent space.

4. Click the target agent name and select the "Version management" tab.

5. Click the "Delete" button in the "Actions" column of the target version.

6. On the confirmation page, click the "Delete" button to complete the operation.
