---
title: "Knowledge Graph"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Knowledge_Graph"
---

The main Knowledge Graph in the knowledge base displays the logical relationship between knowledge (such as concept subordination, attribute association, causal connection) through visual association to achieve knowledge structuring and deep mining. It is suitable for scenarios where complex knowledge associations need to be clarified and related information can be efficiently located. It is especially suitable for cross\-domain knowledge integration, complex problem traceability analysis, and intelligent recommendation of related knowledge. You can usually use the Knowledge Graph to view correlations between knowledge, recall test questions, and tune the accuracy of answers. This article shows you how to create and use an agent Knowledge Graph in an enterprise knowledge engine.

<span id="769d7cb5"></span>
# Building Knowledge Graph


1. Log into the Marketing Agent console and select **Enterprise Knowledge Engine** in the left navigation bar.

2. In the left navigation bar of the Enterprise Knowledge Engine, select **Knowledge Management** \> **Knowledge Graph**.

3. Click the plus icon, **create a new main map** , fill in the relevant parameters, and click **Save**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f7e9c0d415d844d6a5165d7a35c43969~tplv-goo7wpa0wc-image.image) </span>

   
   |Parameter |Parameter description |
   |---|---|
   |Graph name |Enter graph name |
   |Describe |Please enter a map description, within 200 words |
   |Linked Knowledge Base |Select the knowledge base to which the graph is associated, and the graph will be built based on this knowledge base |
   |Type of entity to be extracted |By default, select all, and you can delete unnecessary entity types as needed to adapt to different business scenarios.<br><br><br>* Entity: Subject Knowledge Graph is the core part of business subject\-centered knowledge modeling in the enterprise knowledge engine. By abstracting information (such as attributes, events, relationships, etc.) in multi\-source data such as documents and databases into "entities", and establishing associations between entities (such as subordination, similarity, causation, etc.), a structured graph knowledge network is formed. Its core is to break the traditional document center knowledge management model, with customers, products, employees and other business entities as the core, to achieve centralized management and integration of knowledge.<br><br>* Entity types: The current entity types supported by the Entity Knowledge Graph cover the core business scenarios of enterprises, including:<br><br>   * Organizer \*\*\*\* : such as customers, employees, suppliers, partners, etc.<br><br>   * Geographical location (geo): such as office location, storage center, sales area, etc.<br><br>   * Events: such as product launches, customer complaints, project milestones, etc.<br><br>   * Category: such as knowledge base classification, product function catalog, process node, etc.<br><br>   * Business object (person): such as investment products (stocks, funds), commodities, technical solutions, etc |
   |Knowledge Graph Building Strategy |You can choose to update the graph in full or incrementally.<br><br><br>* Full update: When the knowledge in the knowledge base is updated, the Knowledge Graph will be fully reconstructed to cover the original graph. It is suitable for scenarios where the initial database is built, the consistency requirements are extremely high, and the update frequency is low.<br><br>* Incremental update: When the knowledge in the knowledge base is updated, the Knowledge Graph will detect changes based on the original graph, and update the newly added, edited, and deleted knowledge. It is suitable for scenarios where data changes frequently and requires real\-time response. |
   

4. Once created, click **Build Knowledge Graph**. The map is now being built, and progress can be viewed through the build progress.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/58f71f33a60f499c8538431af5ea7c9d~tplv-goo7wpa0wc-image.image) </span>

5. Once the build is complete, you can view the Knowledge Graph for that knowledge base.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/85d6efa1fc69442f8418f18cf96fb2ee~tplv-goo7wpa0wc-image.image) </span>


<span id="5d6dbc2a"></span>
# View the Knowledge Graph

The first search box in the Knowledge Graph filters for information containing keywords, and the second search box further looks for specific entity points in the filtered results. It is convenient for users to find and confirm modeling results, perform recall testing and tuning.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0a9304eb65b7496ca6aaf882c4ac76f6~tplv-goo7wpa0wc-image.image) </span>

<span id="2d09a29f"></span>
# Editing Knowledge Graph


* Clicking on a node in the graph will display the properties of that node, and you can click the edit button of the **description** or **entity ID** to modify the content of the properties.

* Click on the **Edit Body Graph** in the upper right corner to modify the relevant information of the Knowledge Graph.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/297dabadf06d41c089729726ae9ad1e9~tplv-goo7wpa0wc-image.image) </span>

* Click **View entity configuration** in the upper right corner, enter the entity structured metadata management page, and click **New structured metadata** to add new entity data.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c53b66b5237844afb0276b5711837b6c~tplv-goo7wpa0wc-image.image) </span>
