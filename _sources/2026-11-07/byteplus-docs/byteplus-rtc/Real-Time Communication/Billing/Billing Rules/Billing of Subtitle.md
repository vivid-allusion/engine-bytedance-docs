---
title: "Billing of Subtitle"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-2608589"
---

Subtitle billing applies when you use BytePlus RTC to generate real\-time speech transcription and optional translation for speech in an RTC room or a WTN stream.

## Billable items

Additional costs are incurred when you use the subtitle service:

* **Subtitle service fee**: Billed separately for real\-time transcription and real\-time translation, based on the cumulative billable duration within a calendar day. For detailed billing rules, see [Subtitle service fee](https://docs.byteplus.com/en/docs/12/115191#subtitle-service-fee).

* **Audio and video call fees for the subtitle bot**: When a real\-time subtitle task is initiated, the subtitle bot subscribes to the streams that require subtitle generation. For RTC room subtitles, the bot joins the RTC room and subscribes to the relevant audio streams. For WTN subtitles, the bot subscribes to the target WTN audio and video stream. The bot's call costs follow the same rules as those for standard RTC calls. For detailed billing rules, see [Billing of Audio and Video Calls](https://docs.byteplus.com/docs/byteplus-rtc/docs-69871).

## Subtitle service fee

### Billing formula

Subtitle fee = Real\-time transcription fee + Real\-time translation fee

* Real\-time transcription fee = Transcription unit price x Transcription duration

* Real\-time translation fee = Translation unit price x Translation duration

### Pricing

|Service |Unit price (USD / 1000 minutes) |
|---|---|
|Real\-time transcription |19.99 |
|Real\-time translation |9.99 |

### Calculating the billing duration

The subtitle service calculates billing duration based on the effective audio duration processed by the subtitle task. Transcription and translation durations are counted separately.

* **Transcription duration**: The cumulative duration of billable source audio processed for speech\-to\-text.

* **Translation duration**: The cumulative duration of billable source audio translated into target languages.

The following rules apply:

* Billing counts only **effective audio duration**. If the source user is muted or there is no valid audio input, that period is not billed.

* Translation depends on transcription. When translation is enabled, the same effective audio duration is billed for transcription first, and then billed again for translation.

* Translation duration is calculated **per target language**. If the same source audio is translated into multiple target languages at the same time, the translation duration is multiplied by the number of target languages.

* Usage is aggregated separately for each calendar day. If the total daily usage for transcription or translation is less than 1 minute, it is rounded up and billed as 1 minute.

### Billing examples

A user streams English audio in an RTC room for 10 minutes:

* For the first 5 minutes, only real\-time transcription is enabled.

* For the next 5 minutes, real\-time translation into 3 target languages is enabled.

The billable duration is calculated as follows:

* **Transcription duration**: 10 minutes

* **Translation duration**: 5 x 3 = 15 minutes

The fee is:

* Transcription fee = 19.99 / 1000 x 10 = 0.1999 USD

* Translation fee = 9.99 / 1000 x 15 = 0.1499 USD

Total subtitle fee = 0.3498 USD

## Payment method

Pay\-as\-you\-go: You are billed for your actual subtitle usage after it occurs. Charges are settled according to your BytePlus RTC billing cycle and deducted from your account balance.
