---
title: "Insight overview"
product: "Observability Platform"
product_code: "Observability_Platform"
source: "https://docs.byteplus.com/en/docs/Observability_Platform/gaishu"
---

AI application insight is an intelligent analysis module powered by large language models (LLMs). Based on the insight rules that you configure, this feature can be used to analyze and evaluate the historical sessions of an AI application in bulk. This helps you quickly identify low\-quality sessions and quantitatively evaluate application performance across large volumes of multi\-turn conversations. It also helps you continuously improve the service quality and user satisfaction of the AI application. This module is applicable to scenarios such as inspecting the quality of AI applications in bulk, troubleshooting specific issues, and analyzing session satisfaction.

<span id="RW6MirxF"></span>
## Glossary


* **Insight rule**: A rule that defines the objectives of AI session analysis, the criteria for evaluation, and the output requirements.

* **Insight task**: A task that batch analyzes the AI sessions that match the specified time range and filter conditions, based on a specified insight rule.

* **Insight result**: The evaluation result that is generated for each AI session based on an insight rule. An insight result includes a tag and the rationale for the evaluation.


<span id="oresHd2l"></span>
## Applicable scenario


* **Inspect the quality of AI applications** ** in bulk**: When a large volume of multi\-turn conversation data exists in the target workload, manual quality inspection is costly. In this case, you can use AI application insight to analyze historical sessions in bulk. This way, you can quickly obtain the overall quality distribution and clues to issues, and reduce inspection costs.

* **Troubleshoot specific issues**: When you need to focus on a specific category of sessions, such as sessions of a specific agent service, sessions of a specific user ID, or sessions with high token usage, you can configure filter conditions in an insight task to narrow the analysis scope. Then, only the sessions that match the conditions are analyzed. This reduces interference from irrelevant data and helps you identify issues faster.

* **Analyze session satisfaction**: When you need to evaluate whether an AI application effectively meets user requirements, you can use the built\-in "session satisfaction" rule to evaluate historical sessions. Based on the criteria that are defined in the "session satisfaction" rule, such as the role and the evaluation basis, the system analyzes historical sessions and generates a tag and the rationale for the evaluation. This helps you quickly learn about the overall satisfaction distribution and identify the types of issues that cause user dissatisfaction.


<span id="gjCtD990"></span>
## Usage Process


1. [Select an insight rule](https://docs.byteplus.com/en/docs/Observability_Platform/guize): An insight rule defines the role that is used in session analysis, the evaluation basis, the criteria for evaluating multi\-turn conversations, and the output rules. An insight rule determines how the system analyzes sessions and which tags and rationales for the evaluation the system outputs.

2. [Create an insight task](https://docs.byteplus.com/en/docs/Observability_Platform/renwu): The system analyze specified sessions in bulk based on an insight rule, an analysis time range, agent services, and data filter conditions.

3. **View insight results**: After the task is complete, the system automatically generates an insight report for each session. In the report, you can view the number and percentage of each tag, filter the sessions that require attention, and learn about clues to issues based on the attribute values of tags and the rationale for each evaluation. In addition, for the sessions that require further verification, you can go to the "[LLM session analysis](https://docs.byteplus.com/en/docs/Observability_Platform/LLM_session_analysis)" page to view details. Then, you can optimize the system prompt, the knowledge base, tool calls, or the product workflow accordingly, and verify the optimization results via subsequent insight tasks.
