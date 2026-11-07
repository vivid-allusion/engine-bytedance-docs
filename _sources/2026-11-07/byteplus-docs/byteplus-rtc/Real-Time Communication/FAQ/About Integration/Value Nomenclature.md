---
title: "Value Nomenclature"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70114"
---

<span id="question"></span>
## Question

Are there any rules I should follow for the value assignment?

<span id="answer"></span>
## Answer

Yes. Generally, we specify the rules for each variable respectively in the API documentation. In this document, we provide rules for the following types.

<span id="id-type"></span>
### ID type

For ID type, such as userId, roomId, streamId, and so on, follow the specification below.


* 128 characters at maximum for each ID.

* You can only include the following characters in an ID.



|Sign |Description |
|---|---|
|`a` ~ `z` |Lowercase alphabet |
|`A` ~ `Z` |Uppercase alphabet |
|`0` ~ `9` |Arabic numerals |
|`@` |At symbol |
|`_` |Underscore |
|`.` |Dot symbol |



> * The values are case\-sensitive.

> * Privacy Protection Statement: Do not fill in sensitive user information in this field, including but not limited to a mobile phone number, ID number, passport number, real name, and so on.


<span id="video-parameters-resolution-frame-rate-bit-rate"></span>
### Video parameters: resolution, frame rate, bit rate

Refer to [Setting Video Encoder Configuration](https://docs.byteplus.com/en/docs/12/docs-70122).
