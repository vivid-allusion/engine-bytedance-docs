---
title: "Events and Error Codes"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1928198"
---

You can monitor agent task status and agent status through the callback mechanism, and obtain error information to quickly locate issues.

## VoiceChat Events

When listening to `VoiceChat` events in server\-side ([Obtain Conversation AI Task Events](https://docs.byteplus.com/docs/byteplus-rtc/docs-1798101)), the returned event information is as follows.

|Parameter name |Type |Description |Example value |
|---|---|---|---|
|AppId |String |The unique identifier of the audio/video application. |`661e****543cf` |
|BusinessId |String |Business identifier. |`biz1` |
|RoomId |String |Room ID, the unique identifier of the room. |`room1` |
|TaskId |String |Agent task ID. |`task1` |
|UserID |String |Speaker UserId. |`user1` |
|RoundID |Int64 |Dialogue round. Counting starts from `0`. |`0` |
|EventTime |Int64 |The Unix timestamp (ms) when the event occurred on the RTC server. |`1611736812853` |
|EventType |Int64 |Task status type.<br><br><br>* `0`: Agent task status changed.<br><br>* `1`: Agent task encountered an error. |`0` |
|RunStage |String |Status details.<br><br><br>* `preParamCheck`: Parameter validation error.<br><br>* `taskStart`: Task started.<br><br>* `beginAsking`: Room user started speaking.<br><br>* `asrFinish`: The system has determined that the user has finished their current speaking turn.<br><br>* `llmOutput`: The large model has generated and output the first token.<br><br>* `answerStart`: Agent started speaking.<br><br>* `answerFinish`: Agent finished speaking.<br><br>* `interrupted`: Agent speaking was interrupted.<br><br>* `reasoningStart`: The large model started deep reasoning.<br><br>* `llmIncomplete`: The LLM response ended before normal completion. Check `ExtraInfo.FinishReason` for the cause.<br><br>* `asr`: ASR processing stage.<br><br>* `llm`: LLM processing stage.<br><br>* `tts`: TTS processing stage.<br><br>* `taskStop`: Task ended.<br><br>* `taskUsage`: Usage statistics. This event is sent after `taskStop`, and usage details are returned via the `ExtraInfo` field. |`llmOutput` |
|ErrorInfo |[ErrorInfo](https://docs.byteplus.com/docs/byteplus-rtc/docs-1928198#db695389) |Detailed information about task errors. Appears only when `EventType` is `1`. |\- |
|ExtraInfo |String |Additional information, in JSON string format.<br><br><br>* When `RunStage` is `taskUsage`, this field contains detailed resource usage for the task (such as TTS, LLM usage), and the specific returned information depends on the API version you use.<br><br>* When `RunStage` is `llmIncomplete`, this field contains `FinishReason`:<br><br>   * `contentFilter`: The LLM response triggered content filtering. Conversation AI removes the affected round from the LLM context used in subsequent rounds.<br><br>   * `length`: The LLM stopped because it reached a model output or context length limit. The round remains in the LLM context. |`{"UUID":"..."}`<br><br>`{\"FinishReason\":\"contentFilter\"}`<br><br>`{\"FinishReason\":\"length\"}` |

##### ErrorInfo

|Parameter name |Type |Description |Example value |
|---|---|---|---|
|Errorcode |Int |Error status code. For detailed definitions, see [Error Codes](https://docs.byteplus.com/docs/byteplus-rtc/docs-1928198#80233b4b) |`1001` |
|Reason |String |Detailed error reason. |* `quota exceeded for types [...]`: Dependent service quota exceeded. This is usually because the free quota for ASR, TTS, or LLM has been exhausted, or the purchased resource package has been used up.<br><br>* `requested resource not granted`: Resource not authorized or not enabled. The RTC service does not have permission to call the configured AI service, or the AI service itself has not been successfully enabled. |

## Error Codes

The following table summarizes the error codes that may be returned when performing the following operations, helping you to locate and resolve issues:

* When calling the `StartVoiceChat` API [Obtain AI Status](https://docs.byteplus.com/docs/byteplus-rtc/docs-1415216).

* When configuring VoiceChat event callbacks [Obtain Conversation AI Task Events](https://docs.byteplus.com/docs/byteplus-rtc/docs-1798101) through the console.

|Error codes |Description |Possible causes and solutions |
|---|---|---|
|1000001 |Task initialization failed |**Cause**: Internal system error, resulting in failure to start the task.<br><br>**Solution**: Please try again later. If the issue persists, contact technical support. |
|1000002 |Unknown parameter |**Cause**: The `StartVoiceChat` request contains undefined parameter fields.<br><br>**Solution**: Carefully verify whether the request parameters are consistent with [StartVoiceChat](https://docs.byteplus.com/docs/byteplus-rtc/docs-1558163), and remove or correct any invalid parameters. |
|1003001 |ASR instantiation failed |**Cause**: Incorrect ASR service configuration or internal error.<br><br>**Solution**: Check whether `ASRConfig` fields `Provider` and `ProviderParams` are filled in correctly. |
|1003002 |ASR request failed |**Cause**: Failed to send request to ASR service.<br><br>**Solution**: Check the network connection. If the issue persists, contact technical support. |
|1003003 |Failed to read ASR response |**Cause**: Network error or timeout occurred while receiving a response from the ASR service.<br><br>**Solution**: Check network stability. |
|1003004 |Failed to parse ASR response |**Cause**: The data format returned by the ASR service does not meet expectations.<br><br>**Solution**: If using a custom ASR, check whether its return format complies with the protocol. |
|1003005 |Too many ASR reconnection failures |**Cause**: The connection to the ASR service was interrupted multiple times and could not be restored.<br><br>**Solution**: Check the stability of the ASR service and the network status. |
|1003006 |Failed to establish ASR connection |**Cause**: Unable to establish a connection with the ASR service.<br><br>**Solution**: 1. Confirm that the ASR service is enabled. 2. Check whether authentication information such as `ASRConfig.ProviderParams` `AppId`, `AccessToken`, and other authentication information is correct and valid. 3. Check the network firewall policy. |
|1004001 |LLM instantiation failed |**Cause**: Incorrect LLM service configuration or internal error.<br><br>**Solution**: Check whether parameters such as `LLMConfig` `Mode`, `EndPointId`, `APIKey`, and other parameters are correct. |
|1004002 |LLM request failed |**Cause**: Failed to send request to LLM service.<br><br>**Solution**: Check the network connection. If the issue persists, contact technical support. |
|1004003 |Failed to read LLM response |**Cause**: Network error or timeout occurred while receiving a response from the LLM service.<br><br>**Solution**: Check network stability. |
|1004004 |Failed to process LLM response |**Cause**: The data format returned by the LLM service does not meet expectations.<br><br>**Solution**: If using a third\-party LLM, check whether its return format complies with the [API standard](https://docs.byteplus.com/docs/byteplus-rtc/docs-1399966#cae507df). |
|1004005 |Failed to establish LLM connection |**Cause**: Unable to establish a connection with the LLM service.<br><br>**Solution**: 1. Confirm that the LLM service is enabled. 2. Check whether the authentication information such as `LLMConfig` `URL`, `APIKey`, and others is correct. 3. Check the network firewall policy. |
|1004006 |Function Calling request failed |**Cause**: Failed to call the business\-side URL configured in `FunctionCallingConfig.ServerMessageUrl`.<br><br>**Solution**: Check whether the business\-side service is functioning properly and whether the URL is accessible from the public network. |
|1004007 |Function Calling response request failed |**Cause**: The business\-side service returned a non\-2xx HTTP status code.<br><br>**Solution**: Check the business\-side service logic and ensure that callbacks are responded to correctly. |
|1004008 |Comfort message processing failed |**Cause**: Failed to play the comfort message during the Function Calling process.<br><br>**Solution**: Check whether the TTS configuration is correct. |
|1004009 |Failed to obtain tools from MCP |**Cause**: Failed to request the tool list from the MCP Server.<br><br>**Solution**: Check whether the MCP Server address is correct and whether the service is available. |
|1004010 |Failed to call MCP tools |**Cause**: An error occurred when calling MCP tools.<br><br>**Solution**: Check the implementation logic of internal tools in the MCP Server. |
|1005001 |TTS instantiation failed |**Cause**: Incorrect TTS service configuration or internal error.<br><br>**Solution**: Check whether `TTSConfig` `Provider` and `ProviderParams` are correctly configured. |
|1005002 |TTS request failed |**Cause**: Failed to send a request to the TTS service.<br><br>**Solution**: Check the network connection. If the issue persists, please contact technical support. |
|1005003 |Failed to read TTS response |**Cause**: A network error or timeout occurred when receiving a response from the TTS service.<br><br>**Solution**: Check network stability. |
|1005004 |Failed to process TTS response |**Cause**: The data format returned by the TTS service does not meet expectations.<br><br>**Solution**: If using a custom TTS, check whether its return format complies with the protocol. |
|1005005 |Failed to establish connection with TTS |**Cause**: Unable to establish a connection with the TTS service.<br><br>**Solution**: 1. Confirm that the TTS service has been enabled. 2. Check whether the authentication information such as appid and token in `TTSConfig.ProviderParams` is correct and valid. 3. Check the network firewall policy. |
|1006001 |Failed to establish connection with Avatar |**Cause**: Unable to establish a connection with the Avatar service.<br><br>**Solution**: Check whether parameters such as AvatarAppID and AvatarToken in `AvatarConfig` are correct. |
|1006002 |Avatar service internal error |**Cause**: An unknown error occurred on the Avatar service side.<br><br>**Solution**: Please contact technical support. |
