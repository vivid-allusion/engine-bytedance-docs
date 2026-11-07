---
title: "Integrate Akool Avatar"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1848567"
---

You can integrate the Akool avatar service to provide your AI agent with a visual, lifelike avatar. The avatar can synchronize lip movements with spoken audio, creating a more engaging and realistic interaction experience.

## Demo

You can try this feature in the [Web Demo](https://demo.byteplus.com/rtc/solution/aigc).

## Scenarios

|Scenario |Description |
|---|---|
|**AI Assistant** |Uses a human\-like avatar to provide real\-time responses, improve approachability, and enhance the information\-seeking experience. |
|**AI Tutor** |Uses a digital avatar as a virtual teacher to support interactive instruction, improve engagement, and help students better understand learning content. |
|**AI Customer Service** |Provides a friendly visual assistant that can answer inquiries in real time, reduce communication barriers, and support 24/7 service scenarios. |
|**AI Companionship** |Uses a visual avatar to create a stronger emotional connection during real\-time conversations and companionship scenarios. |

## Implementation

### Step 1: Prepare Akool Avatar Resources

1. Log in to your [Akool account - Workspace](https://akool.com/workspace), click the **API** and create an API credential.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/adaa2ad6bce84948a7778fb8e19cc114~tplv-goo7wpa0wc-topic.webp)

2. In your Akool Workspace, click **Avatar**, and choose or create a **Streaming avatar**, and then obtain the avatar ID.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ce9efcb44f774c1bb8f92027378024c7~tplv-goo7wpa0wc-topic.webp)

### Step 2: Configure StartVoiceChat

#### Configuration

When calling the [StartVoiceChat](https://docs.byteplus.com/docs/byteplus-rtc/docs-1558163) API, complete the following key configurations:

1. `SubtitleConfig.SubtitleMode`: Must be set to `1` (audio timestamps not aligned). Setting it to `0` (audio timestamps aligned) is not supported.

2. `Config.AvatarConfig`: Specifies the configuration for the Akool avatar.

   > **Tip**

   > For a complete list of parameters, see [StartVoiceChat](https://docs.byteplus.com/docs/byteplus-rtc/docs-1558163).

   |Parameter |Type |Required |Description |
   |---|---|---|---|
   |`Enabled` |Bool |Yes |Set to `true` to enable the avatar. |
   |`Provider` |String |Yes |Set to `Akool`. |
   |`ProviderParams` |Object |Yes |Akool avatar configuration. |
   |`ProviderParams.ApiKey` |String |Yes |Akool API credential obtained from [Step 1: Prepare Akool Avatar Resources](https://docs.byteplus.com/docs/byteplus-rtc/docs-1848567#step-1-apply-for-digital-human-resources). |
   |`ProviderParams.AvatarId` |String |Yes |Akool avatar ID obtained from [Step 1: Prepare Akool Avatar Resources](https://docs.byteplus.com/docs/byteplus-rtc/docs-1848567#step-1-apply-for-digital-human-resources). |
   |`AvatarUserID` |String |No |User ID of the avatar in the RTC room, used for identification. This field is user\-defined.<br><br><br>* **Default Value**: `AgentConfig.UserId` + _`Avatar`.<br><br>* **Naming Rules**:<br><br>   * Supports uppercase and lowercase letters (A\-Z, a\-z), digits (0\-9), underscores (_), hyphens (\-), periods (.), and the @ symbol. The maximum length is 128 characters.<br><br>   * The value of AvatarUserID must not be the same as `AgentConfig.UserId` (Agent ID) or `TargetUserId` (Real user ID).<br><br><br>> **Warning**<br><br><br>> When sending control commands—such as manually interrupting a response or updating conversation context via the sendUserBinaryMessage API—the target userId must be the **AI Agent ID (AgentConfig.UserId)**.<br><br><br> |

#### Sample

```JSON
{
  "AppId": "661e****543cf",
  "RoomId": "<YOUR_ROOM_ID>",
  "TaskId": "<YOUR_TASK_ID>",
  "AgentConfig": { "...": "..." },
  "Config": {
    "ASRConfig": { "...": "..." },
    "LLMConfig": { "...": "..." },
    "TTSConfig": { "...": "..." },
    "SubtitleConfig": { "SubtitleMode": 1 },
    "AvatarConfig": {
      "Enabled": true,
      "Provider": "Akool",
      "AvatarUserID": "user_avatar",
      "ProviderParams": {
        "ApiKey": "<your_akool_api_key>",
        "AvatarId": "djn****nZk"
      }
    }
  }
}
```
