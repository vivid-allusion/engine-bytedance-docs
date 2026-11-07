---
title: "Integrate Self-hosted ASR or TTS Model"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1798100"
---

You can integrate self\-hosted ASR and TTS services to meet specific business requirements.

<span id="implementation"></span>
## Implementation

<span id="_1-prerequisites"></span>
### 1. Prerequisites


1. Prepare your self\-hosted ASR or TTS service API. The API must comply with the [Self-hosted model interface protocol spec](https://docs.byteplus.com/en/docs/iga/ai-gateway-self-hosted-protocol).

2. [Submit a ticket](https://console.byteplus.com/workorder/create?step=3&SubProductID=P00000762) to request onboarding your self\-hosted ASR or TTS service to AI Gateway. Then follow [Onboard and call a self-hosted model](https://docs.byteplus.com/en/docs/iga/ai-gateway-self-hosted) to complete the integration.


<span id="_2-configure-the-startvoicechat-api"></span>
### 2. Configure the StartVoiceChat API

> For the complete parameter description, see [StartVoiceChat](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1558163).



<Tabs>
<Tab zoneid="mb77L48GOR" title="Self-hosted ASR">
<TabTitle>Self-hosted ASR</TabTitle>

```JSON
{
    "ASRConfig": {
        "Provider": "ai_gateway",    // required, must be set to `ai_gateway`
        "ProviderParams": {
            "URL": "<AI Gateway endpoint URL>",  // required, the service endpoint URL obtained from AI Gateway
            "APIKey": "sk-xxxxxx",              // required, the access key for AI Gateway
            "ExtraData": {
                "language": "zh-cn",
                "enable_punctuation": true,
                "domain": "medical"
            },
            "ExtraHeader": {
                "custom_header": "value"
            }
        }
    }
}
```



</Tab>
<Tab zoneid="gkSnDEkQvC" title="Self-hosted TTS">
<TabTitle>Self-hosted TTS</TabTitle>

```JSON
{
    "TTSConfig": {
        "Provider": "ai_gateway",    // required, must be set to `ai_gateway`
        "ProviderParams": {
            "URL": "<AI Gateway endpoint URL>",  // required, the service endpoint URL obtained from AI Gateway
            "APIKey": "sk-xxxxxx",              // required, the access key for AI Gateway
            "Voice": "<your_custom_voice>",     // required, your self-hosted voice
            "ExtraData": {
                "language": "zh-cn",
                "enable_punctuation": true,
                "domain": "medical"
            },
            "ExtraHeader": {
                "custom_header": "value"
            },
            "OutputAudioSpeedRate": 1.0,
            "OutputAudioVolume": 1.0,
            "OutputAudioPitchRate": 1.0
        }
    }
}
```



</Tab>
</Tabs>


<span id="example-integrate-botnoi-thai-asr-or-tts"></span>
## Example: Integrate Botnoi Thai ASR or TTS

You can integrate Botnoi's ASR or TTS services with the AI Gateway protocol in Conversation AI.


1. Enable the Botnoi service and obtain the API keys for Botnoi ASR or TTS. For details, see [Botnoi Voice](https://voice.botnoi.ai/developer/api).

2. When calling `StartVoiceChat`, add the Botnoi ASR or TTS configuration under `Config.ASRConfig` or `Config.TTSConfig`. The following examples only show the Botnoi\-related fields. For the complete request body, see [StartVoiceChat](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1558163).

> For Botnoi, the `URL` values are fixed. Use the exact WebSocket endpoints shown below and replace only `APIKey` with your Botnoi ASR or TTS API key.



<Tabs>
<Tab zoneid="YjVRRLa34z" title="Botnoi ASR">
<TabTitle>Botnoi ASR</TabTitle>

```JSON
{
    "ASRConfig": {
        "Provider": "ai_gateway",  // required, must be set to `ai_gateway`
        "ProviderParams": {
            "URL": "ws://prod-asr-ws.botnoigroup.com/realtime?model=asr", // required, fixed value
            "APIKey": "<BOTNOI_ASR_API_KEY>",   // required, Botnoi API key
            "ExtraData": {
                "turn_detection": {
                    "segment_completion_s": 2
                }
            },
            "ExtraHeader": {}
        }
    }
}
```



</Tab>
<Tab zoneid="WRHljXjgE5" title="Botnoi TTS">
<TabTitle>Botnoi TTS</TabTitle>

```JSON
{
    "TTSConfig": {
        "Provider": "ai_gateway",  // required, must be set to `ai_gateway`
        "ProviderParams": {
            "URL": "ws://prod-tts-ws.botnoigroup.com/realtime?model=tts",  // required, fixed value
            "APIKey": "<BOTNOI_TTS_API_KEY>",    // required, Botnoi API key
            "Voice": "1",
            "ExtraData": {},
            "ExtraHeader": {}
        }
    }
}
```



</Tab>
</Tabs>
