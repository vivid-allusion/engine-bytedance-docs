---
title: "Access restrictions priority"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/access-control-priorities_en"
---

When you use multiple access restriction features on BytePlus CDN, they are evaluated in a specific priority order. This document lists the exact execution sequence of these restrictions and clarifies that a request rejection at any stage stops further evaluation. Understanding this hierarchy is essential for correctly configuring your security policies and predicting their behavior. BytePlus CDN provides a series of access restrictions with different priorities. When CDN processes user requests, the order of these access restrictions taking effect is as follows:


1. Geographic Restrictions

2. Disabled HTTP Methods

3. IP Restrictions

4. Referer Restrictions

5. UA Restrictions

6. Origin Restrictions

7. Custom Restrictions

8. URL Authentication

9. Remote Authentication

10. Data Rate Throttling


If an access restriction rejects a user request, the remaining restrictions are not applied to that request.
