---
title: "Managing projects"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Managing_projects"
---

<span id="OaTzgrqv"></span>
## **Overview**

When you use AgentKit, each creation may generate corresponding resources, such as agent runtimes, tools, memories, MCP services, and MCP toolsets. Project management is a resource management method provided by the platform. This method allows you to group and manage resources based on businesses or projects. With Identity and Access Management (IAM), you can grant permissions to users by project (i.e., a group of resources) to ensure resource isolation and data security. You can also view resource bills by project to facilitate the calculation of cloud resource costs.

 For more information on projects, refer to[ Managing projects](https://docs.byteplus.com/en/docs/byteplus-platform/docs-project-management).

<span id="2tMSVJuQ"></span>
## **Usage notes**


* AgentKit\-related resources that support project management include agent runtimes, tools, memories, MCP services, and MCP toolsets.

* A resource can belong to only one project.

* For a newly created resource, if you have not associated it with a project, it will be associated with the "default" project.

* After you associate the resource with a project, only users with permissions on the project can use the resource.

* Associations between resources do not change due to project assignments.

* To associate resources across multiple projects, you need to have permissions for all projects that contain the resources to be associated. For example, if you want to associate an agent runtime in Project A with a tool in Project B, you need permissions for both Project A and Project B. For .

* When you create and manage resources using an IAM user, the IAM user must have corresponding permissions granted by the root account. 


<span id="5KWYweJ3"></span>
## **Project management workflow**

The general workflow for project management is as follows (this topic uses an agent runtime as an example). To associate other newly created resources, such as tools, memories, MCP services, and MCP toolsets, with a project, select the target resource in the left\-side navigation pane.


1. [Create a project](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-a-project): Create a project to manage agent runtimes within it.

2. [Add the project permission for an IAM user](https://docs.byteplus.com/en/docs/byteplus-platform/docs-editing-a-project): Grant project permission for the IAM user.

3. [Create an agent runtime](https://docs.byteplus.com/en/docs/agentkit/Creating_agent_runtimes_in_console): Use the IAM user to create an agent runtime and associate it with the project.

4. (Optional) [Move the agent runtime into/out of a project](https://docs.byteplus.com/en/docs/byteplus-platform/docs-editing-a-project): You can move the agent runtime into or out of a project if its associated project needs to be changed.


<span id="S7T3Z8Fo"></span>
## View resource details of projects

<span id="NVSO4HRQ"></span>
### View projects that resources belong to

On the agent runtime list page, click the target agent runtime to go to the overview page. In the **Basic information** section of the **Configuration information** tab, you can view information of the project associated with the agent runtime.

<span id="tnrO5aKI"></span>
### Search for resources by project


1. Log in to the [AgentKit console](https://console.byteplus.com/agentkit).

2. In the top menu bar, select the region and choose the project based on the description below.

   * Select All Resources to view all resources under this account.

   * Select a specific project to view all its associated resources.

   * Select Manage projects to go to the project list and manage the projects.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When you log in with the root account or an IAM user, the system defaults to displaying all resources under that account.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the IAM user is not granted permissions, after you select "All Resources", the system does not display all resources under the account. Follow the interface instructions to switch to another project or contact the root account to obtain the required permissions.   </div>
   


<span id="PysLORtL"></span>
## Related documents

You can also use [tags](https://docs.byteplus.com/en/docs/agentkit/Tag_management) to categorize AgentKit resources for refined resource management.
