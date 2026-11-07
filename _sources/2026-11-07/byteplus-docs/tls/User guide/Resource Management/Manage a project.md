---
title: "Manage a project"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Managing_projects"
---

In Torch Log Service (TLS), project is the basic unit for managing resources. If you have multiple Identity and Access Management (IAM) users, projects, or products, you can create multiple projects in TLS for isolating log resources and implementing access control. This topic describes how to create and manage projects in the TLS console.

<span id="前提条件"></span>
## Before you begin

Create a BytePlus account and complete enterprise real\-name authentication. For more information, refer to [Sign Up and Verify BytePlus account](https://docs.byteplus.com/en/docs/byteplus-platform/docs-signing-up-your-account).

<span id="创建日志项目"></span>
## Create a project

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Each BytePlus account can have up to 100 projects under a region.</div>



1. Log on to the [TLS console](https://console.byteplus.com/tls).

2. In the top navigation bar, select the region where the TLS is located.

3. In the left\-side navigation pane, choose **Resource management** \> **Project**.

4. Click **Create project**.

5. Specify the project name and description.

   
   |Parameter |Description |
   |---|---|
   |Project name |Specify a name for the project. This parameter is required. |
   |Description |Specify a brief description of the project. This parameter is optional. |
   |Affiliated Project |From the drop\-down list, select an IAM project for the project. If you have not created an IAM project or no suitable IAM project is available, click **Create Project** to create an IAM project.<br><br>In BytePlus Identity and Access Management (IAM), IAM projects serve as resource groups with different ACL policies. IAM offers a policy management feature that allows you to categorize cloud resources across Regions into projects and create different ACL policies for these projects for flexible resource management.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">If you do not specify an IAM project, TLS adds the project to the IAM project named <code>default</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">After you create a project, you can change the IAM project to which the project belongs in <strong>IAM</strong>.</div><br> |
   |Tag |Click **Add Tag**, then type a tag key and a tag value. Tags help identify and categorize cloud resources such as projects and topics, making it easier to search and aggregate resources. For more information, refer to [Tag Overview](https://docs.byteplus.com/docs/tls/tag_overview). |
   

6. Click **OK**.


<span id="查看私网地址等信息"></span>
## View the information about a project

After creating a project, you can view its basic information on the project overview page. You can also go to the details page of the project to view the private endpoint of the project.


1. In the top navigation bar, select the region where the TLS is located.

2. In the left\-side navigation pane, choose **Resource management** \> **Project**.

3. On the **Project** page, view the basic information of the project.

   you can view all projects of the current account. You can view the information, such as project name, project ID, number of topics, description and tags. You can also modify the basic settings of a project, such as the name, tags, and description of the project.

4. Select the target project, then click the project name.

   The **Basic information** section displays the name, ID, VPC Address, Public Network Address, description, and tags of the project. The Public Network Address and VPC Address are the entrances for accessing the project over the internet and the corresponding private network separately.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Service endpoints vary based on regions. When you access a project in a region, we recommend that you copy the endpoint corresponding to the network type that you want to use in the <strong>Basic information</strong> section.   </div>
   

<span id="删除日志项目"></span>
## Delete a project

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Before deleting a project, you must delete all topics from the project.</div>



1. In the top navigation bar, select the region where the TLS is located.

2. In the left\-side navigation pane, choose **Resource management** \> **Project**.

3. Find the target project, then click **Delete** in the **Actions** column.

4. In the dialog box that appears, confirm the information about the project that you want to delete, then click **OK**.
