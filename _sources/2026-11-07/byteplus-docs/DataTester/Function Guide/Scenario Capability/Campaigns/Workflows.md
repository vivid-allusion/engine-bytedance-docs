---
title: "Workflows"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/Workflows"
---

Workflows is an advanced way for DataTester to orchestrate automated reach activities. Using Workflows, you can automate reach reminders to users at specific points in their behavioral journey for purposes such as user development and conversion. This article provides you with the operational essentials of the Workflows feature.

<span id="_1-概述"></span>
# Feature Overview

Workflows provide you with visual user access to the process configuration interface.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1837478b9953414abb6d4374eb535657~tplv-goo7wpa0wc-image.image) </span>

In the Workflows, you can:


* Set the conditions for the user to enter the process.

* Through push action, trigger conditions, flow control flow combination of user operations.

* Define the transformation goals for the process.


<span id="_2-进入流程画布"></span>
# Enter the Workflows

You can enter the Workflows from the Campaigns/Workflows navigated by the system.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b09cc26617ee407abbbeb6eb2aa83082~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-创建流程"></span>
# Create process

Click the "Create Process" button in the upper right corner of the workflows list and follow the steps below to complete the process creation.

<span id="_3-1-设置用户进入流程的条件。"></span>
## Set entry conditions

Click the **Entry Condition** Settings box in the Workflows to set the conditions for the user to enter the process.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/af922195585241c8ab2f0e5ffcf19627~tplv-goo7wpa0wc-image.image) </span>

The system supports **Scheduled type** and **Triggered type** two types of entry conditions:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9944b3278a6e4934b4a00cb0b8819c94~tplv-goo7wpa0wc-image.image) </span>


* **Timed conditions:**  It will automatically start at a set point in time to screen eligible audience users and add them to the process.

   * Scheduled type includes **scheduled type \- single** and **scheduled type \- repeat**.

   * **Timed type \- repeated** can choose to participate in the limit: if you choose to participate once, the user can only enter the process once; if you choose not to limit, the user will enter the process in each cycle.

* **Trigger Condition:**  The user's behavior is monitored and users who meet the behavior criteria are automatically added to the process.


<span id="_3-2-设置受众用户，您可以使用行为、属性、分群等条件，筛选出希望进入流程的用户。"></span>
## Set audience users


1. Set up a push crowd.

   Support selecting **segmented users** or **all users**. Only the trigger process supports the selection of all users; when selecting a sub\-group, it supports the use of behavior, attributes, grouping and other conditions to filter out users who wish to enter the process.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a8b0b90a86464f6287e42171f2c3f878~tplv-goo7wpa0wc-image.image) </span>

The filter criteria of the segmented population support setting multiple, and support the logical relationship of "and", "or" two layers of filter conditions.

2. Set the push range. The push scope is used to test the sent content, and the test user scope can be set at **General Settings** \> **Test Whitelist**. You can choose to push official/test users on the task configuration page.

3. After completing the configuration, you can click **Estimated Users** at the bottom to estimate the number of users who can enter the process under the condition of estimating the current audience range. When consistent with the experimental expectations, you can click **OK** to complete a process node configuration.

<span id="_3-3-添加节点"></span>
## Set Node Policy


1. Configure node policies by clicking the **Policy** button on the Workflows page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c0cd1eac3c4543a8a162ff31527ad53d~tplv-goo7wpa0wc-image.image) </span>

2. Configure the node on the pop\-up page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/54a5eb2fba5a4c7198266233731c55a2~tplv-goo7wpa0wc-image.image) </span>

   The system supports three different types of nodes:

   * **Push action** nodes: This type of node is used to send reach content to users, such as push;

   * **Trigger condition** node: Using trigger conditions, you can judge the user's behavior or attributes to determine how the subsequent process will be executed;

   * **Process Control** Node: A specific node used to increase wait time or jump to a process.

      The configuration interface example is as follows.

   
   |Push action node |Trigger condition node |Process control node |
   |---|---|---|
   |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/22624c5ec682474593eadbca3f455595~tplv-goo7wpa0wc-image.image) </span><br><br>Currently supported push channels and configuration points for each channel can be found [Push Channel Management](https://docs.byteplus.com/docs/DataTester/Push-Channel-Management). |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/eda9f00e0873447dab07cd0ef546ee8c~tplv-goo7wpa0wc-image.image) </span><br><br>Support the use of public attributes or user behavior as triggered conditions, and you can select the triggered condition type and condition details according to the interface. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b203fdb7c562444b9f573c4fb60cade4~tplv-goo7wpa0wc-image.image) </span><br><br>You can choose to wait for a certain amount of time or jump to a specified node according to the interface. |
   

3. You can configure multiple process control nodes according to business needs to achieve flexible operational reach goals, as shown in the figure below.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5165844ada1044fea5a75ed00471f324~tplv-goo7wpa0wc-image.image) </span>


<span id="e3ea6048"></span>
## Set up node shunting


1. Click the flow button in the workflows page to add the experimental version to the corresponding node for offload settings.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f09baa5a627a452d8676064888b36a83~tplv-goo7wpa0wc-image.image) </span>

2. Configure the number of experimental versions and the traffic allocation ratio of each version on the pop\-up page, and click **OK** when done.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/abd47f76632b47f88003e22716bf352c~tplv-goo7wpa0wc-image.image) </span>

3. After returning to the workflows, you can continue to configure the push policy for the offloaded nodes. If no push is required, it can be configured as a blank control.

4. Once the configuration is complete, you can view and confirm the offload details in the workflows.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7cc57f3650224a5d8855a2d378363768~tplv-goo7wpa0wc-image.image) </span>


<span id="_3-4-设置转化目标"></span>
## Set conversion goals

Configure conversion targets in the pop\-up window by clicking Set Target Number in the upper left corner of the Workflows page. The conversion goal is mainly used to determine and measure whether the users in the process have completed the conversion action as expected.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2d714850670e47b8b0d7b29bc00ba3e0~tplv-goo7wpa0wc-image.image) </span>

For each process, you can set a primary goal and multiple secondary goals.

Note: Goal completion does not have to end the process after push, primary goal completion. Therefore, there may be a phenomenon that after the user enters the process, the primary goal is completed and the process is ended without reaching the push node.

<span id="_3-5-完成保存"></span>
## Other workflow settings


* Click the Modify Name button in the upper left corner to set the name of the created workflows.

* Click on the top to set whether you need to turn on Do Not Disturb mode for the process, and then you can set the Do Not Disturb time period and anti\-disturb policy.

* Click "Initiate Approval" in the upper right corner to save the process and submit it to the administrator for approval. After the administrator approves, when the process start time is reached, the process will automatically start running.


<span id="_4-流程画布报表"></span>
# Workflows Report

Click on the workflow name to enter the workflow data report page to view the effect data.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cde3cba0731f4788bebad82d770953df~tplv-goo7wpa0wc-image.image) </span>


* Overview Data Indicator Description

   * Cumulative number of entries: the number of users entering the process.

   * Cumulative trigger times: the number of people who triggered the push.

   * Successful push count: Push count sent successfully.

   * Actual reach: Actual reach of push.

   * Clicks: The number of clicks on push messages.

   * Target completion count: The number of users who have completed the set goal, including users who have not been pushed but have completed the goal.

* Node data indicator description

   * Target completion count: The number of users who complete the target after the push node (Note: If there are multiple push nodes, only the first push node has the target completion count).

   * Target completion rate: target completion number/cumulative entry number (if target conversion is not set, the meaning here is "cumulative trigger number of nodes/cumulative entry number").
