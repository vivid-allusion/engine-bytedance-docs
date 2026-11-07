---
title: "Overview"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/behavior-analysis-functions-overview"
---

ByteHouse customizes functions based on user behavior analysis use scenarios, including retention analysis functions, funnel analysis functions, and path analysis functions. Compared to assembling SQL or using ClickHouse native functions, using ByteHouse's self\-developed dedicated functions is more efficient.

<span id="675e8a86"></span>
### Retention analysis functions

Retention analysis functions support the `genArrayIf` function and the `retention2` function, which can observe user retention that meets certain dimensions within each time unit during the selected time range after a period of time. For detailed introduction and usage of retention analysis functions, refer to [Retention analysis function](https://docs.byteplus.com/docs/bytehouse/retention-analysis-function).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/170890570e584614be02932ff6e42a4c~tplv-goo7wpa0wc-image.image) </span>

<span id="d739f755"></span>
### Funnel analysis functions

Funnel analysis functions support `finder Funnel()`, `funnelRep()`, and `funnelRep2()` functions, suitable for observing the funnel tag value summary of users every time unit (day) within the selected time range by a certain time limit. For detailed introduction and usage of funnel analysis functions, refer to [Funnel Analysis Functions](https://docs.byteplus.com/docs/bytehouse/cdw-funnel-analysis-functions).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bcd8a481bfcf4236a890e2e9692ff6bd~tplv-goo7wpa0wc-image.image) </span>

<span id="91753ca0"></span>
### Path analysis functions

Path analysis functions support `pathSplit` and `pathCount` functions, suitable for analyzing user behavior paths within the selected time range. The front\-end display looks roughly as follows. For detailed introduction and usage of path analysis functions, refer to [Path analysis function](https://docs.byteplus.com/docs/bytehouse/path-analysis-function).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/663159848a034b2f8fed18fb902f6bc1~tplv-goo7wpa0wc-image.image) </span>
