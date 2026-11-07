---
title: "Existing agent migration FAQ"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Existing_agent_migration_FAQ"
---

<span id="mFH6ajuo"></span>
## Q1 · After migration, can I still use my original interfaces and call methods?

Yes, you can. We provide two migration methods. You can choose based on your project's needs, balancing low migration effort with zero changes to the existing call methods.


<columns>
<columnsItem zoneid="bLeZasx8Im">

**Standard migration (recommended by default)** 


* Suitable for most projects

* Provides a unified set of standard interfaces after migration

* Lowest migration effort, fastest to get started

</columnsItem>
<columnsItem zoneid="W9HgaLLPhr">

**Compatible migration**


* Suitable for projects already using an official Server

* Provides standard interfaces while fully preserving your original interfaces and call methods

* No changes required for existing callers

</columnsItem>
</columns>


<span id="9XZCw7Wt"></span>
## Q2 · Can applications built on Bedrock AgentCore be migrated smoothly?

Yes. Migration automatically identifies the underlying agent logic in your application and integrates it with the platform, while preserving the original health check and call interfaces. This allows existing callers to transition smoothly with minimal rework.

<span id="AIq7O5cI"></span>
## Q3 · Can I switch to a large model provided by the platform after migration?

Yes, and it is entirely your choice. By default, migration does not modify your model configuration. If you want to switch to a platform\-recommended model, enable model replacement during migration and provide the model information.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Model replacement only adjusts the runtime configuration and does not modify your business code, making it easy to switch or roll back.</div>


<span id="vklyt0sQ"></span>
## Q4 · Will migration affect my external protocols or frontend interactions?

No, nothing will be degraded. Migration follows an "enhance only, never degrade" principle:


* **System collaboration interface (A2A):**  Fully preserved. External systems require no changes to their call methods.

* **Frontend interaction interface (AG\-UI):**  Fully preserved. Streaming output and interaction experience are not affected.

* **Platform responsibilities:**  Application hosting, deployment, authentication, configuration, and runtime monitoring, plus an additional set of unified standard interfaces.


The platform currently supports the system collaboration interface (A2A) by default. Some enhanced frontend interaction capabilities are still being refined. Feel free to reach out if you have special requirements.


|**Interface type** |**Migration outcome** |
|---|---|
|System collaboration (A2A) |The original call methods are fully preserved. No changes required for external systems. |
|Frontend interaction (AG\-UI) |The original interaction interfaces remain unchanged. Streaming output and tool call experience are not affected. |


<span id="Z7PwDrfp"></span>
## Q5 · My application needs to collaborate with other systems (A2A). How is this handled during migration?


|**Your situation** |**Migration method** |
|---|---|
|Built on Google ADK |A standard collaboration service is automatically generated, ready to use out of the box. |
|Built on veADK with authentication required |A collaboration service is automatically generated with the original authentication capabilities preserved. |
|Need more granular collaboration configuration |Custom configuration of the collaboration service is supported. |
|Need the collaboration service deployed independently |Supported. Post\-migration integration is more flexible. |


**Note:**  Migration automatically ensures the collaboration interface remains stable and accessible, so external systems can continue to access without any adjustments.

<span id="EZC3W3KG"></span>
## Q6 · Will migration affect real\-time frontend interaction experience (AG\-UI)?

No. Migration adds hosting and O&M capabilities on top of the original frontend interaction interfaces, keeping the interaction experience unchanged.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">System collaboration (A2A) can be configured automatically during migration. For frontend interaction (AG\-UI), the interfaces and interaction methods are confirmed with you before migration proceeds, to ensure a seamless transition.</div>



|**What migration does** |**What is guaranteed** |
|---|---|
|Adds hosting, authentication, monitoring, and deployment capabilities on top of the original interaction interfaces |Frontend interface call methods remain unchanged |
|Adapts to the frontend interaction capabilities of your framework |Streaming output, tool calls, state updates, and other real\-time experiences are fully preserved |
|Provides an additional set of standard interfaces as a supplement |Your original frontend interaction entry points are not replaced |


**The full interaction experience is preserved, including:** 


* Message start, end, and error notifications

* Real\-time streaming text output

* Real\-time feedback during tool calls

* Real\-time UI state updates

* Custom extended interaction events


**How different situations are handled:** 


* Already using standard frontend interaction capabilities: Preserved as\-is. No changes required.

* Using a mainstream framework but not yet integrated with frontend interaction: Automatically integrated during migration.

* Only basic calls, no real\-time interaction needed yet: Basic capabilities are provided first, and your frontend interaction expectations are confirmed with you.

* Heavy custom interactions or frontend dependencies on specific data formats: Each item is confirmed with you before processing, to avoid any impact on your existing frontend.
