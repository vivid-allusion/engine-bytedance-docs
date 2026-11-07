---
title: "Knowledge Compilation"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/knowledge-compilation"
---

Knowledge compilation is a set of business domain\-oriented knowledge processing capabilities, which supports the compilation of original documents in the knowledge base into consumable structured products in the knowledge compilation space, including ontology semantics, Knowledge Graph, LLM Wiki and other forms. Through the process of "Building Compilation Space \> Describing Business Objectives \> AI Intelligent Generation Compilation Scheme \> Review and Tuning Scheme \> Release Assets \> Packaging as Agent Skill", Intelligence efficiently builds business knowledge into a consumable knowledge base for Agents, and transforms the traditional manual construction + review and confirmation process into a new way of AI construction + review and confirmation. While improving the efficiency of knowledge construction, it relies on manual review to ensure the quality of knowledge content is controllable.

# Operation steps

## Step 1: Create a new knowledge compilation space

You can divide different knowledge compilation spaces by business and handle matching knowledge compilation requirements within the spaces.

1. Log into the Marketing Agent console and select **Enterprise Knowledge Engine** in the left navigation bar.

2. In the left navigation bar of the Enterprise Knowledge Engine, select **Knowledge Management** \> **Knowledge Compilation**.

3. Click on the **knowledge compilation space** on the right side of the page.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dec5af432c624bfba22d7a8ae1cb13c8~tplv-goo7wpa0wc-image.image)

4. In the **New Knowledge Compilation Space** dialog box, customize the **space name** and **description**, and click **Create**.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9b61029056494a3198fb343268e60708~tplv-goo7wpa0wc-image.image)

   Once created, you can view the space in the list of spaces.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/518ed8952f2a4eb9b10a78a7f671412c~tplv-goo7wpa0wc-image.image)

## Step 2 : Compiling Knowledge

1. On the **knowledge compilation** page, click the specified space name to enter the compilation space session page.

   On the conversation page, you need to add knowledge base knowledge and describe the compilation target in natural language to perform knowledge compilation functions.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5db186cc5f204a57950fd18f2246ddca~tplv-goo7wpa0wc-image.image)

2. Add knowledge by **reference knowledge** areas on the right side of the page.

   You can directly add knowledge base or specific documents from the **Select Document** tab, which is a one\-time addition method, and the new documents in the subsequent knowledge base will not be automatically imported; or enter the **Continuous Import** tab, bind the knowledge base, and then automatically import the knowledge in the library, and continue to discover new documents.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1aeb79212b7047a0a1f3d3e3edbc09c6~tplv-goo7wpa0wc-image.image)

3. Enter the compile target in natural language in the conversation box and send.

   * The system provides templates such as ontology semantic construction and Knowledge Graph construction by default, which you can choose on demand.

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b2d4c9f4210b495c82e835da75cce811~tplv-goo7wpa0wc-image.image)

   * Support Calling Skill and quoting Knowledge Data.

4. Taking the default **ontology semantic construction template** of the system as an example, the compilation knowledge flow is as follows:

   1. Select the **ontology semantic build template** and quote the knowledge by @.

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4a4532157d894f7c80af64b8b3963e00~tplv-goo7wpa0wc-image.image)

   2. After sending, wait for the knowledge compilation to generate a Schema proposal, and click **Edit** to go to the Schema details page.

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f8d2b971312a417ab100119b20a4d7ed~tplv-goo7wpa0wc-image.image)

   3. View the Schema content. If it does not meet expectations, you can edit the content yourself. After confirming that it is correct, click **Publish and start extraction** in the lower right corner of the page.

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0ebb04fd82db44d2a601d374bd2dcee0~tplv-goo7wpa0wc-image.image)

      Create a brand new asset for the first time, and you can choose to update existing assets when you update it repeatedly.

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5ffa02b10d8c4ea49c2e0b2770a291d6~tplv-goo7wpa0wc-image.image)

   4. After waiting for the knowledge compilation to generate an ontology instance, click **Review**.

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2142686d3e9546f9b0d9c5c01bcb66c4~tplv-goo7wpa0wc-image.image)

   5. On the **Build Results: Instances** page, review **object instances** and **relationship instances**.

      * Supports one\-by\-one or approval all to review of all instances.

      * Support editing attribute details. After editing, you need to click Save Draft to review.

         ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/33e736ffaf9147588ce38e0efd9ca4d0~tplv-goo7wpa0wc-image.image)

   6. After the review is completed, the knowledge compilation is required in the text box to build an ontology map.

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0f370d35da6a469da6d5b71f841b3ca0~tplv-goo7wpa0wc-image.image)

   7. View the graph and select any graph node to view the corresponding object, relationship, and attribute information.

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7aa2ac5640b74b5fb2e079e649fd7cd3~tplv-goo7wpa0wc-image.image)

      On the right side of the page, support viewing attribute settings, support viewing instance list, and view the graph after selecting the instance for focused exploration.

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d1be8611b32d4dd6ad0f29aefe522aac~tplv-goo7wpa0wc-image.image)

   8. After confirming that the content is correct, click **Publish** in the upper right corner of the page.

## Step 3: Publish Resource to Acquisite Skills

After the knowledge compilation is completed, all the resources in the current session can be published online. The published resources can be encapsulated as skill packages (unpublished resources cannot be encapsulated). Later, you can import the skill packages into other agents to consume the compiled knowledge.

1. On the right side of the knowledge compilation session details page, confirm that the Schema, instance, graph and other resources have been published, and click **Take online** for unpublished resources.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8e7060fa6db943da9a70b3f304a15973~tplv-goo7wpa0wc-image.image)

2. Wait for the skill build to complete and download the skill.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/984153a0cac0468d93d1c061dad5b920~tplv-goo7wpa0wc-image.image)

   Skill will be added to the agent to achieve the corresponding knowledge query function.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6a24e44816b94b569e903685ae514c55~tplv-goo7wpa0wc-image.image)

# Manage Assets or Skills

Unified management of assets and Skills is supported within the specified knowledge compilation space.

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b5524a1e6ae94038a666e312f3b559b0~tplv-goo7wpa0wc-image.image)

* On the **asset management** page, the following asset management operations are supported

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d8557b0a35b14e69b5d200e312d92309~tplv-goo7wpa0wc-image.image)

   |**Operation** |**Description** |
   |---|---|
   |Search for assets |At the top of the page, you can enter the asset name, setting type, publishing status, and search for assets.<br><br>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fd1ac21e137847b9b610db4156275b82~tplv-goo7wpa0wc-image.image) |
   |View asset history |1. In the **Operation** column for the specified asset, click the Version History icon.<br><br>   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1f20b2b7e45e4ae69a1f13ea571a3331~tplv-goo7wpa0wc-image.image)<br><br>2. On the right side of the historical version page, you can switch between versions to view details.<br><br>   The released version supports taking offline, and the unreleased version supports being released.<br><br>   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b463e5b2129146189f9d3b27e402f8b5~tplv-goo7wpa0wc-image.image) |
   |Online/offline assets |In the **Operation** column for the specified asset, click **Take** **Online** / **Take** **Offline**.<br><br>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/702c6a55ac0a46a3b063714b8a8350a6~tplv-goo7wpa0wc-image.image) |
   |Delete assets |In the **Operation** column for the specified asset, select  **· ·**  \> \*\*Delete \*\*.<br><br>> **注意**<br><br><br>> Once the asset is deleted, it cannot be recovered. Please proceed with caution.<br><br><br>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e2dd27865fde49bbb7d8ab509f1aa7c1~tplv-goo7wpa0wc-image.image) |

* On the **Skill Management** page, you can view the official skills for knowledge compilation, as well as the custom skills you packaged through knowledge compilation.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f7a77c9db58d4fd6b03396a2849e0040~tplv-goo7wpa0wc-image.image)

   * Click on the Skill Card to view the Skill details.

   * Custom Skills support go\-online, go\-offline or delete.

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/eb76e06130f74ed9a1922a4c0692e6a3~tplv-goo7wpa0wc-image.image)

# Configure scheduled tasks

Support for configuring and managing scheduled tasks within a specified knowledge compilation space.

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6f7b55705ec34980936c46631775cabc~tplv-goo7wpa0wc-image.image)

## Create a scheduled task

1. Go to the **Scheduled Tasks** page and click **New Scheduled Tasks** in the upper right corner of the page.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8d2b02ab0743419b80f6705a2857bb1d~tplv-goo7wpa0wc-image.image)

2. In the new session, the scheduled task content is described in natural language to support adding Skills and Knowledge.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f720f2b64af54e4fb29c60308b3d33aa~tplv-goo7wpa0wc-image.image)

   For example, as shown in the figure below, create an ontology semantic construction task that runs at 0 o'clock every day:

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d7522f1fd9304a328793495e0d383717~tplv-goo7wpa0wc-image.image)

## Manage scheduled tasks

On the **Scheduled Tasks** page, the following management operations are supported for the existing scheduled tasks.

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1237a151bcb14986b12d79822a19f40b~tplv-goo7wpa0wc-image.image)

* Click on the task card to redirect to view the task details.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/61f48ed95b59413190591652feca9c94~tplv-goo7wpa0wc-image.image)

* Click the switch in the upper right corner of the task card to choose to turn the task on or off.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/34ed2e94439a4f6fba2c2a6e277f2882~tplv-goo7wpa0wc-image.image)

* In the lower right corner of the task card, it supports viewing the running record of the task, editing the task information (including name, status, user instructions and running time), and deleting the task.

   > **注意**

   > Once the task is deleted, it cannot be restored. Please proceed with caution.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4f5f12410cae408382534e1f7081e2d9~tplv-goo7wpa0wc-image.image)

# Manage space

In the knowledge compilation list, **edit** or **delete** the knowledge compilation space is supported.

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9c4771828e5c4ca3b9a429b1c39a0784~tplv-goo7wpa0wc-image.image)

* Edit: Support modifying the space name and description.

* Delete: Delete the current space. Once deleted, it cannot be restored. Please proceed with caution.
