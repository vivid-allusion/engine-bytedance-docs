---
title: "What should I do if echo leakage or 'self-questioning and answering' occurs?"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-2222050"
---

If you are using the 3.60 RTC SDK, try the following methods to resolve the issue:


1. When creating the engine with `createRTCEngine`, pass the private parameter `"rtc.fg_config":"aigc_media_360=true"` through the `parameters` field.

2. Call `setAudioScenario` to set the audio scenario to the Conversation AI scenario (for example, on Android, use `AICLIENT`).
