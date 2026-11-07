---
title: "Exposure Deduplication"
product: "Viking AI Search"
product_code: "viking-aisearch"
source: "https://docs.byteplus.com/en/docs/viking-aisearch/Remove_items_exposed_to_users"
---

*Viking AI Search is an enterprise\-grade generative\-AI search product. It combines multimodal semantic understanding from large language models with ByteDance's long\-standing experience in information retrieval, giving you an out\-of\-the\-box platform to build multimodal image\-and\-text search and recommendation experiences. Try the full capability set: * [Viking AI Search — Unified Search, Recommendation & Q&A Engine](https://www.volcengine.com/product/viking-ai)


---



<span id="71d00e2d"></span>
# What This Feature Does

The platform ships a flexible **Exposure Deduplication** capability. Two independently configurable rules let you stand up a robust deduplication pipeline entirely through the console — no code required:


* **Exposed\-Item Deduplication** — filters items the user has actually seen, based on real exposure events.

* **Delivered\-Item Deduplication** — a safety net that prevents the same item from being re\-served during the short window when exposure events are still in flight.


Use this feature in **home\-feed recommendation, content\-stream recommendation**, or any scenario where repeated items degrade user experience.

<span id="c85b61df"></span>
## Key Benefits


1. **True deduplication** — only items genuinely seen by the user are filtered. Items cached but not yet delivered are never suppressed by mistake.

2. **Cross\-channel extensibility** — you may inject custom deduplication lists (e.g., items the user has already purchased, or items interacted with in another channel) via API and reuse them across recommendation scenarios.



---



<span id="7490e724"></span>
# Configuration Guide

<span id="06b94525"></span>
## Set Exposure User Event Source


1. Go to **Experience Configuration → Recommendation Experience** and expand "**Related user event scenes" ** under the left\-hand Recommendation Strategy panel.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/1088911867be4258b2df7c6fe02483fe" width="338px" /></div>



&nbsp;

2. In the "**Related user event scenes"**  dropdown, select the page that matches this recommendation scenario.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">\*Caution</div>


<div data-tips="true" data-tips-type="warning">Adding or removing a user event scene does not backfill historical exposure data — it applies to new events only.</div>


&nbsp;

<span id="90e00dcf"></span>
## Configure deduplication rules


3. Expand **Remove Duplicate Recommendations** in the Recommendation Strategy panel and configure both rules below. Both must be set correctly for the end\-to\-end behavior to take effect.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/acfe10833f124ed2acd478882008d831" width="282px" /></div>



|**Rule** |**Field** |**Allowed Range** |**Description** |
|---|---|---|---|
|Exposed\-Item Deduplication |Time window |Min: 1 hour<br><br>Max: No limit |The platform automatically collects exposure events within the window and excludes those items from recommendation results. If exposures within the window exceed the cap, items are taken newest\-first until the cap is reached<br><br>Data sources: see [Exposure Data Sources](https://docs.byteplus.com/docs/viking-aisearch/92283#c67c3441).<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Important</div><br><br><br><br>1. <div data-tips="true" data-tips-type="default">If exposures within the window are fewer than the cap, all of them are used.</div><br><br><br>2. <div data-tips="true" data-tips-type="default">If Max Items is greater than the number of recommendable items, the response may return empty.</div><br> |
||Max Items |Min: 0<br><br>Max: 10,000 ||
|Remove recently recommended |Time window |Min: 1 minute<br><br>Max: No limit |Safety\-net rule that compensates for latency in exposure reporting. <br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="default">Recommend setting this ≥ your behavior\-data reporting latency</div><br> |
||Max Items |Min: 0<br><br>Max: 30,000 ||



4. New rules take effect on the very next recommendation request in the Experience page. 

5. After validating, click "**Sync Changes to API"**  in the top\-right corner; the change is propagated to the live API.


&nbsp;


---



<span id="c67c3441"></span>
## Item Exposure Data Sources

Exposure data for each user may come from **two sources**, automatically merged by event time when a request is served.

<span id="604d7d77"></span>
### Method 1: Automatic Extraction (Recommended)

If you are already reporting exposure events through the Behavior Dataset, the platform extracts events from the **last 7 days** incrementally. No integration work is required:


* Items are written to the user's exposure list in real time, based on the "**Related user event scenes" ** configured for the scenario.

* Subsequent requests automatically exclude those items.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="default">Ingestion, processing, extraction, and update each introduce millisecond\-level latency. To keep deduplication reliable, configure a <strong>Delivered\-Item Deduplication window of at least 1 minute</strong> for every scenario.</div>


&nbsp;

<span id="dc3944b2"></span>
### Method 2: Manual upload via Deduplication API

If you do not report exposure events, or need deduplication logic that spans multiple Behavior Source Pages, call the Deduplicate API to push a custom list of items.

Reference: [Deduplicate - Item Deduplication](https://docs.byteplus.com/docs/viking-aisearch/92269).

&nbsp;

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Caution</div>


<div data-tips="true" data-tips-type="warning">Before calling the API, you <strong>must</strong> configure "<strong>Related user event scenes"</strong> on the corresponding recommendation strategy. Otherwise the API returns an error. </div>


<div data-tips="true" data-tips-type="warning">For configuration details, see <a href="https://docs.byteplus.com/docs/viking-aisearch/92283">Exposure Deduplication</a>. </div>


&nbsp;

&nbsp;

&nbsp;
