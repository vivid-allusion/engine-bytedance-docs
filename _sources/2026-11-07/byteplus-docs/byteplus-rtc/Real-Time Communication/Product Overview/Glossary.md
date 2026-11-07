---
title: "Glossary"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70120"
---


|Term |Description |Rules |
|---|---|---|
|RTC |All the services provided by RTC, including but not limited to audio and video calling capabilities, video capturing, and cloud media processing. |/ |
|App ID |The unique identifier for each app, randomly generated on the console. Users must launch audio and video instances using the same `App ID` to ensure they can have audio and video calls in the same room. |/ |
|Token |The authentication key that users must provide when joining an RTC room. See [Authentication with Token](https://docs.byteplus.com/en/docs/12/docs-70121) for instructions on how to obtain and use a token. |/ |
|Private key |The private key is used to generate the `Token`. Please keep it safe and do not disclose it. |/ |
|Business ID |`Business ID` can be used to segment business scenarios (roles, policies, etc.) within the application, which is detailed in [Setting Configurations for Scenarios](https://docs.byteplus.com/en/docs/12/docs-70135). After setting a `Business ID`, you can view quality and usage data divided by `Business ID` on the console. You can also contact the technical support team to configure specific parameters for each scenario. |See [Value Nomenclature](https://docs.byteplus.com/en/docs/12/docs-70114). |
|Room ID |Users with the same `App ID` and `Room ID` can join the same audio and video call. |See [Value Nomenclature](https://docs.byteplus.com/en/docs/12/docs-70114). |
|User ID |The unique identifier for each user. User IDs must be unique within a room. If two users have the same `User ID`, the user who enters the room later will remove the user who entered the room earlier. |See [Value Nomenclature](https://docs.byteplus.com/en/docs/12/docs-70114). |
|Stream ID |The unique identifier for each audio and video stream. There might be more than one Stream ID from the same user in the same room. |See [Value Nomenclature](https://docs.byteplus.com/en/docs/12/docs-70114). |
|Publish   |Publish audio or video streams to the room the user has joined. |/ |
|Subscribe   |Subscribe to audio or video streams from other users in the room the user has joined. |/ |
