---
title: "Using application templates"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Using_scenario-based_templates"
---

AgentKit Agent Gallery supports the convenient deployment of agent templates. Developers can complete basic parameter configuration via one\-click deployment, quickly generate an agent runtime instance, and perform **online tests**. This allows users to experience the full workflow of the AgentKit platform while quickly exploring agent cases in industry scenarios. In addition, open\-source code is provided as a companion resource, enabling developers to quickly carry out secondary development based on their own needs.

<span id="pzHino3P"></span>
## Template details

In the Agent Gallery, click an application card to access the application template details page.

On the application template details page, you can view the **template overview**, **scenario cases**, **technical architecture and feature modules**, **operation steps**, **resource cleanup methods, associated models, and cloud products**.

<span id="bw5hIHR6"></span>
## Viewing code

Templates are hosted as open source on GitHub, providing abundant code resources to help developers freely use, modify, and apply them to various scenarios. Click "Code" on the application card to go to the GitHub repository.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_efc113dfa1955203a3dfa15f4fc5906c.png) </span>

<span id="UbZeujW5"></span>
## One\-click deployment


* Supported templates

   Only specific templates support one\-click deployment. Refer to the console for actual availability.

   > Multiple deployments are supported. Click "Redeploy" on the application card to deploy the application again.

   > <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_57db3a6ed35b85c178ee0cdaa6091156.png) </span>   
   

* Procedure

   Click "One\-click deploy". On the "Agent deployment" page, you only need to modify the **Name** and **IAM role** parameters, and select **Associated components, Creation method, and Associated project**. Then, check "The product is in public preview/beta stage, I have read and agree to the [Product and Service Testing Agreement](https://docs.byteplus.com/en/docs/legal/docs-customer-agreement)", and click "Create" to deploy the application. For detailed parameter descriptions, refer to [Creating agent runtime](https://docs.byteplus.com/en/docs/agentkit/Creating_agent_runtimes_in_console).

   > For detailed procedures of each agent, refer to the Procedure section in the template details.   
   

   * Testing agents

   After successful deployment, an agent instance will be generated in the agent runtime list. Click "Online test" in the "Actions" column of the agent instance to verify whether the agent can work as expected. You can also view information in the Session, Events, and Trace sections.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Only applications created via one\-click deployment support ChatUI (intelligent conversation interface) testing. For applications deployed by other methods, follow the <strong>test instructions</strong> in the <strong>README.md</strong> file of the corresponding application templates.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If you deploy the same template multiple times and run an <strong>online test</strong> from the Agent Gallery, <strong>the most recently deployed agent</strong> is used by default.   </div>
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ff54142aec953cff72f634fc88dd3ce9.png) </span>

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_db471a86f9d60213c3c4b4fcd65eb870.png) </span>


<span id="4pKkYmhn"></span>
## Observe agents

After the test succeeds, you can view the runtime monitoring data, session analysis, trace analysis, model monitoring data, and log analysis of the agent on the "Observability" page. For details, refer to [Observability](https://docs.byteplus.com/en/docs/agentkit/Observability-).
