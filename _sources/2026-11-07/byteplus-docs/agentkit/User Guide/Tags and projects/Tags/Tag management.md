---
title: "Tag management"
product: "AgentKit"
product_code: "agentkit"
source: "https://docs.byteplus.com/en/docs/agentkit/Tag_management"
---

As your business grows, the types and volume of AgentKit resources continue to grow, increasing the complexity of resource management. You can address this by adding different tags to AgentKit resources based on their types and purposes. This helps categorize resources, facilitating quick retrieval of AgentKit resources with specific attributes and improving management efficiency.

<span id="ZgXmhB5T"></span>
## Scenarios

**Group management**

You can associate different tags with different environments (such as production and test environments). For example, you can associate a tag, such as the key\-value pair of Test:Agent, with all agent runtimes involved in a test environment. During routine maintenance, you can filter a group of instances with this tag from all instances and then take actions.

**Tag\-based bill splitting**

In team or project management, you can add tags based on group, project, or department (such as CostCenter:Project) to categorize resources. Then, use these tags in the Billing Center for cost allocation management. If you want to use tags for bill splitting, you need to enable specific tags in the billing center console and apply them to detailed bills. For specific operations, refer to [Bill tags](https://docs.byteplus.com/en/docs/byteplus-platform/bill_tags). 

<span id="J6XqoTSu"></span>
## Tag types


* System tag: Tags that are automatically added to resources when they are created are system tags. System tags usually start with `volc:` or `sys:`, can only be viewed and cannot be edited.

* Custom tag: Tags manually added to resources by you are called custom tags. You cannot create custom tags that start with `volc:` or `sys:` in any letter case.

* For design principles and common examples of tags, see [Tag design principles](https://docs.byteplus.com/en/docs/agentkit/Tag_design_principles).


<span id="J1rkCOMG"></span>
## Usage notes


* AgentKit\-related resources that support tags include agent runtimes, tools, memories, MCP services, MCP toolsets, Skills, and Skills spaces.

* If the tag key that you want to associate with the instance is the same as an existing tag key, the new tag value overrides the original value. Proceed with caution.

* A tag consists of a tag key (Key) and a tag value (Value), both of which are case\-sensitive. Value can be empty.

* Keys of multiple tags for the same resource must be unique, and each Key can have only one Value.

* A single operation can add up to 20 tags. A single resource can have a maximum of 50 tags.


<span id="DLHmFV4r"></span>
## Manage tags

In this topic, an agent runtime is used as an example to describe how to associate tags with a resource. To associate tags with other resources, such as a tool or the MCP service, select the target resource in the left\-side navigation pane in the product console.

<span id="ntw3TqU6"></span>
### Create or add tags


<Tabs>
<Tab zoneid="ybJ3evEccf" title="Create or add tags for an existing agent runtime">
<TabTitle>Create or add tags for an existing agent runtime</TabTitle>

1. Log in to [the AgentKit console](https://console.byteplus.com/agentkit). 

2. In the left\-side navigation pane, select "Agent Runtime".

3. In the top menu bar, select the region and project of the target agent runtime.

4. In the agent runtime list, click the name of the target agent runtime.

4. In the "Basic information" section, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ec2861579271445bcb653a7a00ca08df.png) </span> button next to "Tag" **.** 

5. In the pop\-up "Edit tag" dialog box, create or add tags.

6. Click the "Confirm" button to complete the operation.

7. You can view the associated tags of agent runtimes by using either of the following methods.

   * View the "Tag" column on the agent runtime list page.

   * On the agent runtime list page, click the target agent runtime to enter the configuration information page. In the "Basic information" section, view the tags associated with the agent runtime.


</Tab>
<Tab zoneid="U4V6O29onU" title="Create or add tags when you create an agent runtime">
<TabTitle>Create or add tags when you create an agent runtime</TabTitle>

[When you create an agent runtime](https://docs.byteplus.com/en/docs/agentkit/Creating_agent_runtimes_in_console), click the "Add tag" button in the **Advanced configuration** section to create or add tags for the agent runtime.


</Tab>
</Tabs>


<span id="3KhhMhzP"></span>
### Delete a tag

To remove tags from the target resource when they are no longer applicable for managing the resource, refer to the following steps.


1. Log in to [the AgentKit console](https://console.byteplus.com/agentkit). 

2. In the left\-side navigation pane, select "Agent Runtime".

3. In the top menu bar, select the region and project of the target agent runtime.

4. In the agent runtime list, click the name of the target agent runtime.

4. In the "Basic information" section, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ec2861579271445bcb653a7a00ca08df.png) </span> button next to "Tag" **.** 

5. In the pop\-up "Edit tag" dialog box, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9d69d3434e3c325cc5f5f8ee93667c1d.png) </span> button to remove the tag.

6. Click the "Confirm" button to complete the operation.


<span id="hDbFPRlM"></span>
## Related documents

In addition to tags, you can also use [projects](https://docs.byteplus.com/en/docs/agentkit/Managing_projects) to group your resources based on dimensions such as resource usage, permission, and ownership. This helps hierarchical resource management for multiple users and multiple projects.
