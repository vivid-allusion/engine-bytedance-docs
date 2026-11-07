---
title: "Getting started with BytePlus Recommend APIs"
product: "BytePlus Recommend"
product_code: "recommend"
source: "https://docs.byteplus.com/en/docs/recommend/reference-getting_started_with_byteplus_recommend_apis"
---

BytePlus Recommend APIs are HTTP\-based RESTful APIs that use user signatures for authorization. API request and response bodies are formatted in JSON. This topic walks you through the process of calling BytePlus Recommend APIs:


1. Understanding limits and quotas

2. Signing up for an account

3. Completing authentication

4. Creating your first call


<span id="c1f6fb6f"></span>
## Understanding limits and quotas

Each project has a default capacity limit, which can be increased by contacting the BytePlus Recommend team. If you anticipate a notable upcoming increase in usage, you can ask the BytePlus Recommend team to adjust the limit a few days in advance.


|**Quota** |**Value** |
|---|---|
|DAU (Daily Active User Count) |500,000 |
|MAU (Montly Active User Count) |2,000,000 |
|Daily New Item Count |2,000 |
|Daily UserEvent Data Size |30GB |
|Prediction QPS (Queries Per Second) |100 |
|Model in Parallel Training |1 |
|Saved Model Count |5 |


<span id="acae5833"></span>
## Signing up for an account

Before calling the BytePlus Recommend APIs, you need to sign up for an account by referring to [Signing up for a BytePlus account](https://docs.byteplus.com/en/byteplus-platform/docs/signing-up-your-account).

<span id="5341b240"></span>
## Completing authentication

BytePlus Recommend API authentication will sign API requests to prove your identity legitimacy and avoid malicious interception \*\* of the requests during their transfers. For more information on signature calculation and authentication steps, refer to BytePlus Recommend API authentication.

<span id="55effe1c"></span>
## Creating your first call

APIs require specific request structures to make API calls. For more information, refer toAPI HTTP request.
