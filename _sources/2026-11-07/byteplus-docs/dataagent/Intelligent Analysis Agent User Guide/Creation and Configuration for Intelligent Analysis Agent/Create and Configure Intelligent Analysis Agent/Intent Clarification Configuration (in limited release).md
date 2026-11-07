---
title: "Intent Clarification Configuration (in limited release)"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Intent_Clarification_Configuration_in_limited_release"
---

This article provides configuration guidance related to intent clarification when creating and configuring the Intelligent Analysis Agent.

<span id="8f2d2cbd"></span>
# Background information

Intent clarification rules help the Intelligent Analysis Agent improve its interaction capabilities and task execution accuracy when handling complex, ambiguous, or incomplete user input. When a user submits a question, the Intelligent Analysis Agent automatically determines whether the user's intent is clear based on the match between the user's input and the intent clarification rules, and follows up with clarification questions for ambiguous queries.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a51599b365a14621870e57e85518b045~tplv-goo7wpa0wc-image.image) </span>

<span id="3176dfc1"></span>
# Configure intent clarification rules

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The current intent clarification configuration features are in limited release and have not been fully launched. To use this feature, contact Volcano Engine technical support to enable this feature in the limited release phase.</div>



1. Go to the agent configuration page. For detailed steps, see [Entry point](https://docs.byteplus.com/docs/dataagent/Overview_of_Creation_and_Configuration_Procedures#1b6ae60c).

2. Click "Intent clarification configuration" in the left navigation bar to enter the intent clarification configuration page. After enabling the intent clarification switch, you can configure intent clarification rules.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b836c025d0154127919dee71e6e42f13~tplv-goo7wpa0wc-image.image) </span>


|Parameters |Configuration instructions |
|---|---|
|Maximum clarification attempts |During a single conversation, the agent will ask clarification questions based on the set "maximum clarification attempts", which can be set to a maximum of three times. |
|Reference case settings |The Intelligent Analysis Agent provides two reference cases. You can also customize "reference cases" based on subsequent application scenarios of the agent to help the model better determine whether the user's intent is ambiguous.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When asking questions, it is recommended to include key elements such as time and metrics. You can add cases of possible ambiguous scenarios related to the time dimension, metric dimension, and more, based on potential application scenarios of the agent.</div><br> |
