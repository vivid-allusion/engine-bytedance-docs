---
title: "Create permission policies"
product: "Agent Identity"
product_code: "identity"
source: "https://docs.byteplus.com/en/docs/identity/Create_permission_policies"
---

Permission policies are based on the **Cedar declarative authorization language**, providing you with a comprehensive permission management solution that covers the entire `User -> Agent -> Tool` chain. It is designed to address core challenges such as difficulty in permission tracing, coupling of permission logic with business code, and high barriers to policy configuration.

Through this guide, you will learn how to create and manage permission policies, define granular access rules using either the visual editor or Cedar code, and ensure policy accuracy with the simulation validation feature.

<span id="bdcc9088"></span>
## Core values


* **End\-to\-end permission tracing**: Supports recording and validating multi\-level permission transfers from users to agents and then to tools, ensuring that the source of each operation's permission is clear and traceable.

* **Business logic decoupling**: Achieves separation of permission validation from business logic through deep integration with the permission gateway, supports chained authentication, and does not require modifications to your business code.

* **Accessible policy configuration**: Provides a visual policy editor and a professional Cedar code editor, making it easy for both business and development personnel to get started.


<span id="87e67fca"></span>
## Basic concepts


|Noun |Explanation |
|---|---|
|**Cedar language** |A declarative permissions policy language used to define "who (Principal) can perform what action (Action) on what (Resource)", featuring concise syntax and reliable security. |
|**Policy space (Policy Space)**  |A logical container for managing permissions policies. You can create different policy spaces by project or business scenario (such as "financial reimbursement scenario") to achieve policy isolation and categorization. |
|**Chained authorization** |In the "User → Agent → Tool" invocation chain, permissions are validated step by step at each level to ensure that every operation in the chain is authorized. |


<span id="ec13cd19"></span>
## Prerequisites

You have enabled the agent identity and permission management platform service and completed authorization. For details, see [Enable Agent Identity and complete authorization](https://docs.byteplus.com/docs/identity/89601).

<span id="a4948917"></span>
## Step 1: Access and create a policy space

Policy space is the first step in managing and organizing permission policies.


1. Log in to the BytePlus Agent Identity Console.

2. In the left navigation bar, select **Permission Control \> Permission Policy**.

3. Click Create a permission policy space, fill in the **Space Name**, **Description**, and select **Project** and **Tag**.

4. Click **Confirm**.


<span id="55e8c632"></span>
## Step 2: Create permission policies

After creating a policy space, you can start defining specific permission rules within it.


1. In the policy space list, click the name or ID of the target policy space to enter its details page.

2. On the details page, click **Create a Policy**.

3. Edit the policy name and description.

4. Configure the specific policy content.

   The system provides two methods for creating policies: **visual editing** and **Cedar statement editing**.

   
   <Tabs>
   <Tab zoneid="cglLyW5gDU" title="Visual editing">
   <TabTitle>Visual editing</TabTitle>
   
   * **Parameter configuration**:
   
      * **Effect**: Select **Allow** or **Deny**. This determines whether the policy authorizes (`permit`) or prohibits (`forbid`).
   
      * **User**: Select **User pool** and specific **User** from the dropdown list. This is the object to which the policy grants or denies authorization.
   
      * **Intermediate Agent**: Click  **+ Add Agent** to simulate the "User → Agent → Tool" invocation chain. Up to 5 levels of Agent can be added.
   
      * **Resource**: Select the resource type (such as Agent, knowledge base, knowledge base document, and so on) from the dropdown list, and specify the resource ID.
   
   * **Real\-time preview**: During configuration, the preview window on the right displays the generated Cedar policy code in real time.
   
   
   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/60ed05b9685d4f4fbed8a70fa545241b) </span>
   
   
   </Tab>
   <Tab zoneid="lqkDU8cSv2" title="Cedar statement editing">
   <TabTitle>Cedar statement editing</TabTitle>
   
   To achieve more flexible and complex permission control, write policy code directly using Cedar language.
   
   Manually write your Cedar policy in the code editor. The editor provides code highlighting, syntax prompts, and real\-time error checking to help you write efficiently.
   
   **Example**: `permit(principal == user::"alice", action == Action::"invoke", resource == agent::"trip_agent");`
   
   
   </Tab>
   </Tabs>
   

5. Click **OK** to validate and save the policy.


<span id="df8aa136"></span>
## Step 3: Manage and view policies

After creation, you can view and manage all policies in the list on the policy space details page.


* **Filter and sort**: Use the search box at the top to perform a fuzzy search by "Policy ID/TRN/Description," or click the table header to sort the list.

* **View policy content**: Click the  **+**  icon on the left side of the policy row to expand and view the complete Cedar code for the policy.

* **Delete policy**: Click the **Delete** button in the action column, and remove the policy after confirmation.


<span id="805e06c2"></span>
## Step 4: Simulate permission validation

To ensure that policies work as expected, you can use the permission simulation feature to test permission rules before actual calls occur.


1. In the upper right corner of the policy list, click **Simulate permission validation**.

2. In the pop\-up **Check permission** window, configure a complete call chain:

   * **User**: Select the user to validate.

   * **Intermediate Agent**: Add 1 to 5 intermediate Agents as needed.

   * **Resource**: Select the target resource to access.

3. Click **OK**, and the system will match all policies in the current space according to your configured call chain and return the validation result:

   * **Pass**: If the request is allowed, the system will display "Permission granted" and list the matched `permit` policy names.

   * **Deny**: If the request is denied, the system will display "Permission denied" and list the matched `forbid` policies or indicate "No policy matched."


<span id="7b97ab2a"></span>
## Frequently asked questions

<span id="872a3891"></span>
### **Why is my policy not effective?** 

Please check whether the **resource type** in the policy is exactly the same as the resource type in the actual business scenario. For example, if the policy defines KnowledgeBase, but the actual access is to a knowledge base document (Document), the policy will not match.

<span id="0fa08e4b"></span>
### **What should I do if saving the Cedar statement fails?** 

Please ensure that your Cedar code strictly follows the syntax format of `permit/forbid(principal == ..., action == ..., resource == ...);`. Any syntax error will cause the save to fail. You can correct errors according to the editor's real\-time error prompts.
