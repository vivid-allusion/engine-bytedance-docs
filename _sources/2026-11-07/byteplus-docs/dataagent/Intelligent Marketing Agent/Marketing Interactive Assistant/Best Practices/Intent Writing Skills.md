---
title: "Intent Writing Skills"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Intent_Writing_Skills"
---

This article shows you how to write the name and description of an intent when creating a new one. The intention is that the intelligent master control is used to identify the core configuration unit of the user request, and its name and description directly affect the recognition accuracy of the system. Writing the name and description of the intention can improve the accuracy of the intelligent master control to identify user requests and reduce misjudgments and missed judgments. It is suitable for situations where it is necessary to clarify the requirements boundaries and cover the specific usage scenarios of users when creating new intentions.

<span id="9165d1ec"></span>
# What constitutes a good intention?

Intent description is the core basis for intelligent master control to determine user intentions. A good intention master control needs to meet


* **Clear boundaries:**  The first task of intent description is to "delineate the scope" and prevent the model from misjudging what is "similar but not" to be included, or omitting what "should be". The core is to answer two questions:  **"What does the intention specifically cover?" "What does it definitely not cover?"** 

   * Forward description: Adopt the triple qualification method of "subject + scene + content type". For example, when defining the "internal management system of the company", it is not just expressed as "internal system", but also clearly "main body (internal employees) + scene (daily work) + content type (attendance, leave, performance, etc.) ".

   * Reverse description: explicitly list the "exclusions". For scenarios that are easily confused, state directly "situations that are not part of the intent." For example, "compliance knowledge" is intended to add: "Exclude compliance consulting at the customer level (such as the customer asking'can I complain if I lost money buying stocks') ".

* **Concrete Scenario:**  Intent descriptions should not stay in "broad and empty categories" (such as "internal systems"), but should be broken down into "specific scenarios that users will actually encounter" so that the total control can correspond to real questions. The core is to "disassemble abstract intentions into specific demand scenarios that users can perceive".

   * Disassemble sub\-scenarios by "user behavior link": For example, "internal office platform operation" can be disassembled by "system type": OA system operation, personnel system operation; further subdivided by "operation purpose": reimbursement application, customer addition, attendance inquiry.

   * Each sub\-scenario adds "problem direction": for example, "OA system operation" can add: "Initiate approval, query approval progress, handle errors (such as login failure) ".

* **Generalized and controllable:**  "Generalized" refers to having the master control identify "different expressions of the same requirement" (e.g. "leave process" and "how to apply for leave" are the same requirement), while "controllable" refers to not including "irrelevant expressions". The core is "balancing coverage and accuracy".

   * Supplemental "multi\-style examples": Each sub\-scenario contains at least three types of examples, such as advice around ETF rates.

      * Verbal expressions (such as "How do you charge for buying an ETF? Will it be more expensive than buying a fund?")

      * Written statements (e.g. "What items are included in the transaction fees of ETFs? What is the usual range of commission rates for different brokers?")

      * Indirect expression (e.g. "Every time you buy an ETF of 100 yuan, the handling fee is deducted by 5 yuan, which feels a little expensive. Is there something wrong?")

   * Use "keywords + semantic constraints" to determine the generalization boundary: for example, the intention of "securities trading rules" can clearly "include keywords such as'T + 1 ',' daily limit ',' entrusted time ', and the semantics revolve around'rule consultation', excluding'market analysis' and'buying and selling advice '."

* **Model readable:**  Intent descriptions are ultimately for "big language models" to view, avoiding vague expressions that "humans can understand but the model cannot". When it comes to colloquial abbreviations, technical terms, industry slang, etc., it is necessary to maintain the corresponding terminology library so that the model can understand the intent description.

   * Clear keywords: do not use the expression "money\-related rules", but use "compensation and benefits distribution rules, reimbursement review rules" (keywords: compensation and benefits, reimbursement review).

   * Avoid vague words: Do not use expressions such as "approximately" and "relevant" (e.g., do not use "compliance\-related issues", but use "compliance code of practice, compliance penalty rules").

   * Professional terminology database maintenance: For example, the "Science and Technology Innovation Board Access Conditions" can supplement "that is, the assets and trading experience requirements for individual investors to open an account on the Science and Technology Innovation Board" to avoid the machine missing the judgment due to the deviation of terminology understanding.


<span id="860dc486"></span>
# How to Write Intention


|**Composing dimension** |**Core requirements** |**Example (take "Q & A \- compliance class" as an example)**  |**Precautions** |
|---|---|---|---|
|Clarify "core areas" |Adopt a "forward definition + reverse exclusion" approach to clarify intent boundaries to prevent crossovers with other intents (for example, for "compliance classes", it needs to be clearly identified as "practitioner compliance", not "client compliance consulting") |* Positive: securities practitioners code of conduct, regulatory compliance;<br><br>* Reverse: compliance risk consulting that does not cover the client level (for example, the client asking "Can I complain if I lost money on a stock purchase" does not fall into this category) |Avoid using vague expressions, such as "compliance\-related issues", as it is not clear "whose compliance" and "what kind of compliance", which can easily lead to miscalculation |
|Disassemble "Scene Subitem" |Disassemble by "user identity (employee/customer) + demand scenario (work/business/life) + problem type (rules/operations/concepts) " to cover the core scenario |* Sub\-item 1: Prohibition of professional conduct (e.g. prohibition of insider trading);<br><br>* Sub\-item 2: Customer suitability management operations.<br><br>* Sub\-item 3: compliance with penalties |High\-frequency scenarios are neither omitted nor included in extraneous scenarios (e.g., "compliance class" does not include "employee attendance") |
|Supplementary "Question Example" |Equip each sub\-item with 3\-5 high\-frequency, specific question examples, covering "spoken + written" expressions, to improve the ability to generalize matching |Verbal: "Can I tell the client that this stock will definitely go up?"; Written: "What compliance requirements do practitioners need to follow to recommend securities products?" |Examples should avoid duplication and extremes, and avoid using "niche scenarios + technical terms" as examples (e.g., without writing "FATCA provisions for cross\-border compliance") |
|Define "exclusion scenarios" |Make clear scenarios that do not belong to the intent to reduce mismatches (especially when multiple intents have similarities). |Exclusion scenarios: 1. Client\-level compliance consulting (e.g., client asking "What should I do if my account is frozen"); 2. Internal administrative systems (e.g. attendance) |"Fuzzy scenarios" are not avoided, and explicit exclusions can reduce subsequent debugging costs |
|Unified "expression style", "technical term" interpretation |Use short sentences with "complete and unambiguous subject\-verb\-object", and maintain a terminology library for interpretation of colloquial abbreviations and technical terms |Uniformly use the expression "XX range includes XX, typical problems such as XX", and avoid using expressions such as "compliance means you can't do bad things, such as don't insider trading" |Do not mix "spoken + written" styles, and do not use vague words such as "probably", "maybe", "etc." |
