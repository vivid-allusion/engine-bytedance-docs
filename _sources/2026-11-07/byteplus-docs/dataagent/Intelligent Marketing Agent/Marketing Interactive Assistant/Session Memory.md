---
title: "Session Memory"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Session_Memory"
---

The session memory is used to store the user memory of the autonomous planning agent, and flexibly extracts the user's event memory or portrait memory by configuring different memory extraction strategies.

* Event memory: based on user behavior details, memory formed after semantic processing and aggregation, used to record user\-specific attributes and behavior information, and provide original data source support for portrait memory.

* Portrait memory: Memory inferred from large models based on tags, user behavior details, or event memory, including information such as user style, characteristics, and preferences.

# Create a new session memory

1. Log into the Marketing Agent console and select **Marketing Interactions** in the left navigation bar.

2. In the left navigation bar of the Marketing Interaction Assistant, select **Session Memory**.

3. In the upper right corner of the Session Memory page, click **New Memory**, and in the pop\-up window, customize the input memory name and description.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b4a1729b577c45aca6dae1d6671ce433~tplv-goo7wpa0wc-image.image)

   Click **OK** when the configuration is complete, and you can view the newly created session memory on the Memory page.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/53074e2db622496fa61bf500239461dc~tplv-goo7wpa0wc-image.image)

# Configuring Session Memory Policy

After creating a new memory bank, you need to enter the memory bank details page to configure the memory policy. The policy includes global memory policy and domain memory policy.

* Global memory strategy: universal event memory and portrait memory.

* Domain memory strategy: Differentiate autonomous planning agents. Agents need to choose to write specific domain memories and precipitate them into event memories and portrait memories only for current business scenarios.

Configuration instructions:

1. On the **session memory** page, click the specified memory card to go to the memory details page.

2. On the **Memory Policy** tab, select New **Global Memory Policy** or **Domain Memory Policy**.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ddc73466c2d349398e513d3341ac8ab1~tplv-goo7wpa0wc-image.image)

3. When you first create a new policy, you create the event memory policy first, and then the portrait memory policy.

   1. Event memory policy configuration item:

      * Name: A custom name that identifies the current event memory policy.

      * Description: A custom description that describes the purpose of the current memory.

      * Model: Select a large model for memory retrieval.

      * Memory extraction rules: Specify memory extraction rules through natural language, i.e. large model cue words.

      * Memory valid period configuration: you can choose **permanent**, **one week**, **one month** or **custom** (the upper limit is 3650 days).

   2. Image memory policy configuration item:

      * Character name: A custom name that identifies the current portrait memory policy.

      * Presentation name: The name displayed in the memory list.

      * Linked event memory: Linked event memory is used to extract feature information such as user preferences.

      * Description: A custom description that describes the purpose of the current memory.

      * Model: Select a large model for memory retrieval.

      * Default: Memory default value.

      * Memory extraction rules: Specify memory extraction rules through natural language, i.e. large model cue words.

      * Memory valid period configuration: you can choose **permanent**, **one week**, **one month** or **custom** (the upper limit is 3650 days).

4. (Optional) The stock memory policy can be viewed in the list, and it is supported to choose to enable or disable the policy, edit the policy, or delete the policy according to the actual situation.

   > **注意**

   > Once the policy is deleted, it cannot be restored. Please proceed with caution.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0fb7f0c6761e489a9f42f17581d8e593~tplv-goo7wpa0wc-image.image)

# Using session memory

When building an autonomous planning agent, turn on long\-term memory and configure session memory and policies. Please see for details [New Autonomous Planning Agent](https://docs.byteplus.com/docs/dataagent/New_Autonomous_Planning_Agent).

# View user memory

1. On the **session memory** page, click the specified memory card to go to the memory details page.

2. On the User Memory tab, you can view the global memory or domain memory for a given user, including portrait memory and event memory.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/714c2d4b225647d7ade0cbe07face912~tplv-goo7wpa0wc-image.image)
