---
title: "Configure Conversation Opening"
product: "Viking AI Search"
product_code: "viking-aisearch"
source: "https://docs.byteplus.com/en/docs/viking-aisearch/Configure_Conversation_Opening"
---

To ensure a natural and engaging start to the user journey, the platform allows you to configure **Smart Welcome Messages** and **Personalized Recommendations** that trigger as soon as a user enters the Dialogue Assistant page.

Based on your instructions, the AI Assistant can generate a brief welcome message at the start of each session. If personalized recommendations are configured, the assistant will also leverage user profiles and historical interaction data to provide tailored content suggestions, significantly boosting first\-turn engagement.

You can configure the dialogue opening settings in **Application \> Experience Center \> Conversational Search Experience**. We offer two options: **Welcome Message ** and **Initial Item Recommendations** at dialogue opening.

<span id="4a4e1a39"></span>
# Configure Personalized Welcome Messages and Starter Questions

The welcome message requires no complex pre\-configuration. After importing and activating an item dataset, you can see the default welcome message template on the Conversational Search Experience tab. You can customize welcome messages using the console to achieve the following effects:


* **Configure Welcome Message generation instructions:**  Tailor the AI’s greeting to align with your specific **Role Settings** and **Brand Identity**. This ensures the first touchpoint feels consistent with your platform’s voice.

* **Personalized Welcome Message:**  If you have already configured the recommendation configurations and there is an active behavior dataset within the app, the user's historical behavior data will be used to build a **preference profile** and **historical interaction records**. The assistant will automatically add personalized information to the welcome message based on this data.


**After each Welcome Message, the system follows up with a Starter Question:**  Suggested questions generated from your item data can be clicked to trigger Conversational Search, helping them familiarize themselves with the interaction and solving the "cold start" engagement problem.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/1abdcd0101c948cbb343136152d01a40" width="542px" /></div>


&nbsp;

<span id="635e31a1"></span>
## Configure Welcome Message generation instructions

You can modify the welcome message generation logic and style by adjusting the 'Role and Style' and 'Opening Settings' in the Conversational Search experience configuration panel to better fit your business needs.


* **Role Setting (Agent Persona):**  By default, the system\-generated welcome message uses the role settings, including the role name, personality traits, language style, and other elements, to ensure the welcome message aligns with the defined persona. If you want to include brand elements, persona information, and assistant personality in the welcome message, you can optimize the  **'Agent Persona'**  instructions accordingly. See details: [Configure Conversational Search Assistant instructions](https://docs.byteplus.com/docs/393/Configure_Conversational_Search_Assistant_instructions)

* **Welcome Message:**  This instruction defines the generation structure and writing requirements of the welcome message. You can adjust the instructions based on your business needs to make the welcome content more specific and compliant with business standards.


<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/19e7676483ba4241b72c57d8bdee8a8e) </span>

&nbsp;

The welcome message setting includes the following dynamic parameters by default. These dynamic parameters are implicitly available for use in your instructions, but you can refer to them in natural language to guide the model on how to use this information:


|**Dynamic parameters** |**Source** |**Usage example** |
|---|---|---|
|**User nickname** |This value is passed in the user.nickname parameter when calling the conversation API. |You can refer to this parameter as "user nickname", for example:<br><br>> When a user nickname is available, greet with "Hello `[user nickname]`, nice to see you~" |
|**Current time** |The system automatically provides the current time as context for the model during API calls, using ISO standard date\-time format, including the UTC+8 time zone. |You can refer to this parameter as current time, for example:<br><br>> If the `current time` is evening in Beijing time, ask the user if they want a snack and use this opportunity to recommend one |


**Example of e\-commerce scenario welcome message instruction:** 

```Markdown
# Welcome Message Generation Requirements

The user has just opened the conversation interface. You are required to generate a concise welcome message (under 150 words) that includes a **[Greeting]**, **[Self-Introduction]**, and **[Interaction Guidance]**.

### 1. [Greeting] Writing Standards
- **Format:** Use a Markdown Level 1 Header (`# `) and start with a randomized emoji to set a vibrant tone.
- **Personalization:** - If `User Nickname` is provided: `#[Nickname], Good [Time of Day]!`
    - If `User Nickname` is empty: `#Hi, Good [Time of Day] ~`
- **Time-Sensitive Logic:** Automatically determine the appropriate greeting based on the current time (e.g., "Morning," "Afternoon," "Evening," etc.).

### 2. [Self-Introduction] Requirements
- Provide a brief, natural self-introduction based on your **Role Persona**. 
- Clearly communicate who you are and what specific capabilities you offer to the user.

### 3. [Interaction Guidance] Requirements
- Proactively invite the user to start a conversation.
- The invitation must align with your role's identity and service scope (e.g., inviting them to ask for recommendations or technical advice).
```


<span id="4918a786"></span>
## Personalized welcome message

When your application has linked and activated behavioral data, the recommendation engine aggregates user behavior based on the user ID in the behavioral data to create user preference profiles and key behavior histories (see: [Prerequisites and setup](https://docs.byteplus.com/docs/393/Configuration_Setup)). At this point, the AI Search Conversational Search Assistant automatically retrieves these profiles to refine personalized welcome messages, such as responding to the user's previous browsing interests or recalling past inquiries and purchase behaviors to naturally guide recommendations to more relevant content.

Using personalized welcome messages requires no additional configuration in the console but requires you to:


* **Have a linked and activated User Event dataset in the application:**  The behavioral data is in the "active" state and includes sufficient behavior records (generally, at least one behavior record associated with the user ID is required to generate a profile for a single user).

* **Pass the user ID when calling the Conversational Search API:**  When calling the Conversational Search API, use the user._user_id parameter to pass the user's ID. The user ID must match the user ID in the behavioral data to ensure the system correctly identifies the user.


<span id="a26a10ba"></span>
## Starter Questions

By default, the system will suggest questions to the user at the start of each session. You can control the number of suggested questions returned each time and configure custom questions to insert specific recommended questions into the recommendations.

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/92e3d4410f8542429072aa6ca8d29c70) </span>

&nbsp;

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Starter Question generation mechanism</div>


<div data-tips="true" data-tips-type="default">To ensure recommended questions closely relate to your search and candidate recommendation data and can be fully answered, questions are pre\-generated offline during the data import and processing phase. They update dynamically each day with your candidate item data.</div>


<div data-tips="true" data-tips-type="default">When initially importing item data and linking it to the application, starter questions are not generated immediately. The first set will be ready <strong>the following day after your data linkage takes effect</strong>, allowing you to experience the recommended questions</div>


<span id="71da0c4f"></span>
### Set the number of recommended questions returned

You can adjust the maximum number of starter questions returned each time in [Starter Questions] / [Maximum number of questions]. By default, 4 questions are recommended, and you can adjust up to 8 questions.

<span id="b2c7b51c"></span>
### Configure the Custom Question Pool

In addition to the automated questions generated from your item data, you can import **Custom Questions** to meet specific business or marketing objectives. You can edit custom questions in [Starter Questions] \> [Custom starter questions], and the system will automatically parse these entries and merge them into the global recommendation pool, ensuring they are recalled alongside the AI\-generated questions every time the conversation starts.

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/3f2e3cb7de704df1a4f48b3fb8622cdf) </span>

&nbsp;

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default"><strong>Personalized recommended question recall</strong></div>


<div data-tips="true" data-tips-type="default">When you configure recommendation configurations in the application (see: <a href="https://docs.byteplus.com/docs/viking-aisearch/92206">Introduction to AI Recommendation</a>), recommended questions will also use user interest profiles extracted from behavioral data for personalization. Suggested questions returned to different users will better align with their interaction interests on the platform.</div>


<span id="fca16e2e"></span>
# Configure personalized recommendations when starting a conversation

**If you have already configured and activated the [Homepage Recommendation] configuration in the application**, you can enable the **Initial Item Recommendations** switch in the Conversational Search experience settings. Once enabled, the assistant will attempt to perform a **Personalized Recommendation** every time a new session begins. By integrating these suggestions into the welcome message and follow\-up prompts, the assistant significantly increases item exposure and discovery within the Conversational Search interface.

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/1f0616a8174f46a48ca8cca76eecb4e3) </span>

&nbsp;

<span id="53da1bb4"></span>
## Enable conversation start recommendation switch

Find the [Initial item recommendations] switch in the Conversational Search experience panel and enable this feature. After enabling the switch, you need to select the configuration for the initial recommendations. The system will automatically use the selected recommendation configuration to provide personalized item recommendations at the start of conversations based on user profiles.

&nbsp;

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="default">Currently, only the <strong>Main Page Recommendation </strong>configuration is supported as the opening recommendation engine for the Conversational Search assistant. For an explanation of the recommendation configurations, please refer to <a href="https://docs.byteplus.com/docs/viking-aisearch/92194">Features Overview</a>.</div>


<span id="ccdbee8f"></span>
# Triggering the Conversation Start via API

You need to use the **`opening_remarks`** (Boolean) parameter when calling the Conversational Search API to control whether to trigger the welcome message feature. For the first call in each new session, set `opening_remarks = True`. The system will send a welcome message or a welcome message with recommended items at the start of the conversation. 

For more details, see [API Request](https://docs.byteplus.com/docs/viking-aisearch/Integrated_Conversational_Search#bd446e16).
