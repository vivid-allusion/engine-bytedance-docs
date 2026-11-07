---
title: "Create an AI Search Application"
product: "Viking AI Search"
product_code: "viking-aisearch"
source: "https://docs.byteplus.com/en/docs/viking-aisearch/Create_an_AI_Search_Application"
---

To build a Viking AI\-powered application from scratch, follow this step\-by\-step tutorial.

This guide walks you through the entire initial setup, from creating an application and importing datasets to configuring fields and testing core features. Following these instructions will help you master the basic configuration and successfully deploy your solution.

&nbsp;

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/0309c75a34634d489db4542bd427a8f0" width="800px" /></div>


&nbsp;

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="default">To enable recommendation features, upload a user event dataset alongside your item dataset. For detailed specifications on user event dataset, refer to "Step 4: Configure user event dataset fields" below or the  <a href="https://docs.byteplus.com/docs/viking-aisearch/Create_User_Behavior_Dataset">Create User Event Dataset</a> section of the help documentation.</div>



---



<span id="d11f9944"></span>
# Application Creation and Dataset Configuration

<span id="482de0e7"></span>
## Process Overview

After activating Viking AI Search, complete the following workflow to upload necessary item data: 


1. Create an application

2. Import item datasets

3. Define field configurations. 

4. To enable and evaluate recommendation capabilities, upload and configure the corresponding user event dataset. 


&nbsp;

<video src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/f6ae8bf11b984d5aa39e44670ed4b17d" controls></video>


<span id="516987e7"></span>
### Step 1: Create application

Create your Viking AI Search application. This serves as the foundation for all subsequent data upload and configuration.

<span id="f48dd6ae"></span>
### Step 2: Import item dataset

After creating your application, upload your item dataset to activate the engine's capabilities.

This video demonstrates how to create a new item dataset and import your data to walk you through the end\-to\-end workflow.

<span id="e35c2272"></span>
### Step 3: Configure Item Dataset Fields

Review the system\-generated data configuration, define field purposes, assign unique identifiers, and validate the configuration before finalizing the setup.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="default">Processing may take several minutes depending on the data volume.</div>


&nbsp;

<span id="351c8e1e"></span>
#### Data requirements:


* **Unique identifier** — Each record must include a unique string ID to serve as the primary key for indexing and retrieval.

* **Schema consistency** — Use consistent data types for fields with the same name across multiple datasets to prevent ingestion errors.

* **Nested data** — The system supports hierarchical structures up to 3 layers deep, enabling efficient indexing and retrieval of complex nested attributes.

* **Image data upload** — Multiple image fields of String or Array<String\> type are supported; content must be image URLs (or URL lists). Ensure URLs are publicly accessible.

* **Image processing** — Pass images via URLs within a dedicated JSON Object. To ensure optimal performance, keep file sizes under 5 MB.


&nbsp;

&nbsp;

<video src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/252e0fd9d7f54b6c87fd31ecf3d883df" controls></video>


<span id="f41a5fcb"></span>
### Step 4: Configure user event dataset fields

Upload your user event dataset and define the fields. You may also link to an existing user event dataset.

This step is a prerequisite for enabling recommendation features.

&nbsp;

&nbsp;

<span id="71c7b97a"></span>
### Step 5: Test features

After uploading your data, click **Experience** to enter the interactive staging environment.

The experience portal provides the following features for testing your application:


* **Core capabilities:**  Toggle among the Search, Recommendation, and Conversational Search modules to test the engine.

* **Development tools:**  Access API code snippets, manage datasets, and review real\-time call logs.

* **Simulation and tuning:**  Preview results in a simulated UI and apply strategies to fine\-tune your ranking logic.


&nbsp;

&nbsp;

This concludes the quick\-start guide for application creation. For detailed information on specific feature configuration or API integration, refer to the respective configuration sections in the help documentation.

&nbsp;


---



*Learn more about Viking AI Search product capabilities at * [Viking AI Search Engine: Integrated Enterprise Search, Recommendation, and Q&A Intelligent Engine](https://www.volcengine.com/product/AI-Search-Rec)
