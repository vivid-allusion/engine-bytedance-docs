---
title: "Observation"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Session_Management"
---

Observation capabilities include metrics monitoring, session details, intent statistics, and link tracking to help you dynamically observe the operation dynamics and performance metrics of intent planning engines and agents for error troubleshooting and performance optimization. This article describes how to view observation data.

# Function introduction

|**Function** |**Introduce** |
|---|---|
|Indicator monitoring |The total number of messages, the number of interactive users, and the average number of session interactions used to query the specified intent planning engine or agent. |
|Conversation details |Used to query the session content of a specified intent planning engine or agent. |
|Intent statistics |Used to query the total number of Queries, interactive users, hit intents Top N, and hit records for the specified intent under the specified intent planning engine. |
|Link tracing |The following data of the agent can be obtained through link tracing:<br><br><br>* Trace: A call chain record of a complete request.<br><br>* Span: An independent unit of operation in a trace, such as a model call, a function call, etc. |

# Indicator monitoring

1. Log into the Marketing Agent console and, at the top of the left navigation bar, select **Marketing Interactive Assistant**.

2. Select **Observation** \> **Metrics Monitoring** in the left navigation bar of Marketing Interactive Assistant.

3. At the top of the page, select **Intent Planning Engine/Agent** and specify the **session time**.

   After the page data is loaded, view the feedback statistics, total messages, interactive users, and average session engagement statistics.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d13eeb96abd242b38745da870a6a610c~tplv-goo7wpa0wc-image.image)

# Conversation details

1. Log into the Marketing Agent console and, at the top of the left navigation bar, select **Marketing Interactive Assistant**.

2. Select **Observations** \> **Session Details** in the left navigation bar of the Marketing Interaction Assistant.

3. At the top of the page, select **Intent Planning Engine/Agent** and specify the **session time**.

   Supports searching for session details by session ID, user ID/nickname, and session content.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a306d7b7d53743b3880ff6febb4dd762~tplv-goo7wpa0wc-image.image)

4. In the session list, you can view the session ID, the intention planning engine/agent, the user ID, and the session content. Click **Details** in the Actions column to view full session information.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/88ca918dcce948ae958a6557b81106b4~tplv-goo7wpa0wc-image.image)

5. (Optional) In the session list, it supports **exporting** the specified session, and supports selecting multiple sessions to export in batches.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a38e321cfe4c4acda615a3126ecd87ef~tplv-goo7wpa0wc-image.image)

# Intent statistics

1. Log into the Marketing Agent console and, at the top of the left navigation bar, select **Marketing Interactive Assistant**.

2. Select **Observations** \> **Intent Statistics** in the left navigation bar of Marketing Interactive Assistant.

3. At the top of the page, select the specified intent planning engine and specify the intent (supports selecting **all intents**) and the query time period.

   Support input query (user request), user ID search.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8ff2175f2dcc4dc090e2dd221fd84083~tplv-goo7wpa0wc-image.image)

4. View all Queries, Interactive Users, Hit Intents for Intents Top N.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/28db98f327d54b3189fa60cb42983414~tplv-goo7wpa0wc-image.image)

   At the bottom of the page, you can view the intent hit history, including time, user ID, Query (user request), hit intent, and intent time. Support for **exporting** hit records.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b2a1e8f92696486aa1cb9efa4a0a67bd~tplv-goo7wpa0wc-image.image)
