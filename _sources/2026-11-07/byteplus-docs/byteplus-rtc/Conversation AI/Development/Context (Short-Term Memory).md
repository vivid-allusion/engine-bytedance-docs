---
title: "Context (Short-Term Memory)"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1511926"
---

Context management enables AI to have short\-term memory, allowing it to review and reference the most recent N rounds of conversation history within a single session, resulting in more accurate and coherent responses. You can manage context in the following two ways:


* **Set global context**: Establish basic information at the start of the conversation.

* **Dynamically pass in context**: Supplement context in real time during the conversation.


<span id=".5Lyg5YWl5Z-656GA5LiK5LiL5paH"></span>
## Set Global Context

When initiating a conversation, use the `StartVoiceChat` API to set the initial context information for the LLM, which applies to the entire task. Different large model platforms have varying context management mechanisms.

<span id=".5LiK5LiL5paH5py65Yi2"></span>
### Context Mechanism

When using the BytePlus ModelArk models, the logic for generating model conversation context is jointly controlled by system prompts (`SystemMessages`), user prompts (`UserPrompts`), and the number of historical question rounds (`HistoryLength`).

&nbsp;


|Parameter name |Type |Description |
|---|---|---|
|`SystemMessages` |String[] |System prompts. Defines the model's role, behavior guidelines, output format, and other core instructions. |
|`UserPrompts` |Object[] |User prompts. Can be used to enhance the quality of the model's responses. The model will prioritize this content when generating a reply, guiding the model to generate specific outputs or perform specific tasks. Must include both `Role` and `Content` fields, and they must appear in pairs. It is recommended to use this parameter to control user prompts, as it has an automatic prompt eviction mechanism and offers more stable performance. |
|`HistoryLength` |Integer |Number of historical question rounds stored by the model. |
|`UserMessages` |String[] |**Legacy parameter, not recommended for use, retained only for compatibility.** <br><br>User prompts. Can be used to enhance the quality of model responses. When generating replies, the model will prioritize referencing the content here, guiding the model to produce specific outputs or perform specific tasks. |


**UserMessages Description**

`UserMessages` is a legacy parameter retained for backward compatibility and is not recommended for use. The differences from `UserPrompts` are as follows:

&nbsp;


|Dimension |UserPrompts (recommended) |UserMessages (not recommended) |
|---|---|---|
|**Data type** |Object array Object[] |String array String[] |
|**Field requirements** |Must include role and content fields, and user and assistant roles must alternate. |No strict field requirements; stores conversation text directly. |
|**Storage mechanism** |**Automatic eviction**: When the conversation history exceeds the HistoryLength limit, the earliest UserPrompts will be evicted to make room for new conversation history. |**Session\-fixed**: In the current session, the content of `UserMessages` will not be automatically evicted like `UserPrompts`, and will continue to occupy context space until the session ends. |


<span id=".5LiK5LiL5paH6ZW_5bqm6ZmQ5Yi2"></span>
### Context Length Limit

The total context length (calculated in tokens) must not exceed the upper limit of the selected large model (such as 8k). The calculation method depends on the parameter combination you use.


*  **(Recommended) When using UserPrompts:** 

   * Calculation logic: UserPrompts supports automatic eviction. When calculating the total length, only UserPrompts that are still effective in the current conversation are included.

   * Calculation formula:

      ```Plain
      Total tokens = SystemMessages + effective UserPrompts + HistoryLength rounds of conversation
      ```
      

   * Example: Assume HistoryLength is 3 and the model limit is 8k. When an old `UserPrompts` is evicted due to an increase in conversation rounds, it is no longer included in the total length calculation, freeing up space for new conversation history.

*  **(Not recommended) When using UserMessages:** 

   * Calculation logic: UserMessages are permanently retained, and all content must be included when calculating the total length.

   * Calculation formula:

      ```Plain
      Total tokens = SystemMessages + All UserMessages + HistoryLength rounds of conversation
      ```
      

   * Example: Assume HistoryLength is 3 and the model limit is 8k. Because UserMessages are permanently stored, even as the number of conversation rounds increases, previously passed UserMessages content will continue to occupy context space. Therefore, it is necessary to control the length of the content passed in to avoid exceeding the model limit.


<span id=".5Yqo5oCB5Lyg5YWl5LiK5LiL5paH"></span>
## Dynamic Context Input

Custom text information can be input to the LLM as contextual reference for the next response, but it will not trigger an immediate reply. This is suitable for scenarios that require combining real\-time changes or implicit information that users cannot express via voice.

&nbsp;


|Scenario |Description |Example |
|---|---|---|
|Game companion |Generates appropriate responses based on real\-time game data from the user, providing more personalized companionship. |* **Custom text**: "The current user's record is 0\-14, and they are behind in gold."<br><br>* **User voice question**: "What equipment should I buy?"<br><br>* **AI output**: "I observe that you are in a losing situation. It is recommended to buy defensive equipment first to stabilize the game." |
|Health consultation |Generates personalized suggestions based on real\-time physiological data from the user, improving the accuracy of health guidance. |* **Custom text**: "Current user heart rate 130, pale complexion."<br><br>* **User voice question**: "I am not feeling well right now, what should I do?"<br><br>* **AI output**: "Your heart rate has been detected as consistently high. It is recommended to immediately stop exercising and replenish electrolytes." |


<span id=".5a6e546w5pa55byP"></span>
### Implementation

Call the [UpdateVoiceChat](https://docs.byteplus.com/docs/byteplus-rtc/docs-1404671) interface to input context. Refer to the following example:

```JSON
{
  "AppId": "YOUR_AppId",        // Same as StartVoiceChat
  "RoomId": "YOUR_RoomId",      // Same as StartVoiceChat
  "TaskId": "YOUR_TaskId",      // Same as StartVoiceChat
  "Command": "ExternalPromptsForLLM", // Must be this value
  "Message": "The current user's record is 0-14, and they are behind in gold." // Enter the context text to be passed in
}
```
