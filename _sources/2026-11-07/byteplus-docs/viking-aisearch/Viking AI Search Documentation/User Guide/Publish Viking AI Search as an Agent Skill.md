---
title: "Publish Viking AI Search as an Agent Skill"
product: "Viking AI Search"
product_code: "viking-aisearch"
source: "https://docs.byteplus.com/en/docs/viking-aisearch/Configure_and_publish_AI_Search_Skill"
---

Viking AI Search is the one\-stop AI search, recommendation, and conversational search SaaS service from BytePlus. This guide explains how to package the search, conversational search, and recommendation services you have configured in the console as an **Agent Skill**, so end users can invoke your services directly from AI Agents such as OpenClaw, Trae, Claude Code, and Codex.

&nbsp;


---



<span id="eaab062e"></span>
# Feature overview

An **Agent Skill** is a standardized AI\-capability packaging format. It bundles the search, conversational search, and recommendation services that you configure in the Viking AI Search console into a distributable, installable Skill package.

After publishing the Skill, you can guide end users to install it so they can search your catalog and receive personalized recommendations directly from their personal AI tools &mdash; reaching users anywhere, with no integration barrier.

<span id="6cb1713a"></span>
## Core value


* **For businesses (B\-side):**  No development effort is required. Release the Skill in one click from the console and extend your reach to C\-end consumers. The Skill wraps your existing API services; no additional cost is incurred unless the Skill is invoked.

* **For end users (C\-side):**  Once the Skill is installed, users can search your items and receive personalized recommendations from any supported AI Agent (ArkClaw, OpenClaw, Trae, and others).


<span id="038f6eeb"></span>
# Use cases


|**Scenario** |**Description** |
|---|---|
|E\-commerce brand |Publish product search and personalized recommendation as a Skill so consumers can search, browse, and discover products directly inside an AI Agent. |
|Content platform |Package content search, conversational search, and recommendation as a Skill, letting users retrieve accurate content through natural conversation. |
|Stock media platform |Publish the stock library as a Skill so creators can pull assets into their AI workflow without leaving the Agent. |


<span id="ca0974f3"></span>
# Prerequisites

Before publishing a Skill, complete the following preparation:


1. **Create an application:**  At least one application must exist in the Viking AI Search console. See [Create Application](https://docs.byteplus.com/docs/viking-aisearch/Create_Application).

2. **Import and bind datasets:**  The application must be bound to an item dataset and a user event dataset. See [Create Item Dataset - Image & Text Data](https://docs.byteplus.com/docs/viking-aisearch/Create_item_dataset_image_text), [Create User Event Dataset](https://docs.byteplus.com/docs/viking-aisearch/Create_User_Behavior_Dataset).

3. **Create an API Key:**  At least one API Key must exist under the application. See [Manage API Key](https://docs.byteplus.com/docs/viking-aisearch/Manage_API_Key).



---



<span id="771d70d8"></span>
# Procedure

<span id="18d59a84"></span>
## Step 1: Open the Skill configuration page


1. Sign in to the Viking AI Search console.

2. Select the target application in the left navigation pane and open the **Experience Center** page.

3. In the top\-right of the page, locate the **Configure Viking AI Search Skill** area and click the button.


<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/e697cdc139174cabbff4a50063463681) </span>

The configuration drawer has two tabs at the top ** "Search & Conversation and Recommendation"**  corresponding to the two Skill capability types. You can enable one tab or both.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/ed8b9d866fba4662ade18723e70dbe6a" width="800px" /></div>


&nbsp;

<span id="f11d7c03"></span>
## Step 2: Configure Search & Conversation

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/fa0ea738ecff4b61a4c3394c5f6f58ae" width="700px" /></div>


<span id="9c91b705"></span>
### **Select the scene to apply in the Skill**


1. Click the **Search** dropdown and select a **search scene** from the list.

2. The dropdown lists every search scene created under the current application.

3. The selected scene&rsquo;s full strategy configuration (recall method, ranking rules, truncation policy, etc.) is applied to the Skill search service.

4. The application&rsquo;s current default search scene is pre\-selected.

5. **Select the Strategy applied in the Skill**


<span id="3d200e93"></span>
### Select the dataset that the Skill operates on


1. Click the **Dataset** dropdown and select the item dataset to associate with the Skill.

2. Items in this dataset form the candidate pool for both search and conversational search.

3. The dropdown lists every item dataset bound to the current application.


<span id="c81e0c69"></span>
###  (Optional) Configure the item\-detail page link


1. Enter a product or content URL template in the **Details page** field. Once configured, search results returned in the Agent include clickable links back to your site.

2. Click  **+ {{Dynamic parameter}}**  to the right of the field to insert variables from dataset fields into the URL.

3. Example: `https://www.example.com/product/{{item_id}}` — the system replaces `{{item_id}}` with each result's actual item ID at display time.

4. Multiple dynamic parameters can be combined, for example `https://www.example.com/{{category}}/{{item_id}}`.


<span id="5aeec28c"></span>
### (Optional) Select the API Key to embed in the Skill


1. In the **API Key** list, click **Select** on the row of the key you want to use. 

   1. The list shows every API Key under the current application, including name, masked key value, and creation time.

   2. The selected key is marked as checked.

2. The selected key is written into the generated Skill package, so end users do not need to configure authentication separately after installing the Skill.

3. If no key exists yet, click **Create API Key** below the list to create one.

4. If you prefer not to embed the key, skip this step. End users can configure the API Key as an environment variable when installing the Skill.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/9ae2b71a4e6d48d78eed2af72e0757f0" width="377px" /></div>


&nbsp;

<span id="5bd57168"></span>
## Step 3: Configure Recommendation

Switch to the **Recommendation** tab and complete the following configuration:

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/a61973c7c6804c05928ebd7ad9416ea6" width="386px" /></div>


<span id="83a2a221"></span>
### Select the scene to apply in the Skill


* Click the **Recommendation** dropdown and select a **recommendation scene** from the list.

* The dropdown lists every recommendation scene created under the current application.

* The selected scene's full strategy configuration is applied to the Skill's recommendation service.

* The application's current default recommendation scene is pre\-selected.


<span id="0593c3c9"></span>
### (Optional) Configure the item\-detail page link

Behavior is identical to Search and Conversation, including dynamic\-parameter templates such as `{{item_id}}` and `{{category}}`.

<span id="dae62f7d"></span>
### (Optional) Select the API Key to embed in the Skill

Behavior is identical to Search and Conversation. If you do not embed a key, end users can supply one via an environment variable at install time.

&nbsp;

<span id="e40593c1"></span>
## Step 4: Generate and download the Skill package


1. After the configuration is complete, click **Generate Skill package** at the bottom of the drawer.

2. The system validates the configuration (required fields, API Key association, etc.). Once validation passes, the Skill package is built and downloaded to your local machine as a ZIP file.

3. Share the ZIP package with your end users so they can install it into their AI Agent or Vibe Coding tool — OpenClaw, Trae, Claude Code, and others.


&nbsp;


---



<span id="0564444e"></span>
# Next steps

After distributing the Skill package, instruct end users to install it into their preferred AI Agent.
