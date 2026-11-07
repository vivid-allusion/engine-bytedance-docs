---
title: "Announcement on AI MediaKit Storage Policy Update"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-storage-policy-update"
---

Effective **September 23, 2026**, AI MediaKit will update its storage policy for temporary input files and output artifacts. This announcement outlines these changes and explains the actions you must take to ensure uninterrupted service.

## What's changing

### Temporary input file storage policy

Temporary copies of your input files, which AI MediaKit fetches to perform tasks, will no longer be retained long\-term. Instead, they will be automatically deleted within 15 days after task processing ends, whether the task succeeds or fails.

### Output artifact storage policy

The validity of download links for output artifacts will change. Previously, these links could be renewed by calling [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details) API. Going forward, they will have a fixed 24\-hour validity from the moment of generation and will no longer be renewable.

### Impact on you

Starting September 23, 2026, temporary input file copies will be automatically deleted within 15 days after task processing ends, whether the task succeeds or fails. Output artifact download links will become inaccessible 24 hours after generation. You must download your artifacts from the default public URLs within 24 hours of generation.

### Actions required

Please review and update your business logic before September 23, 2026, to ensure the smooth operation of your services.

* Review and adjust artifact download logic: If your application currently relies on the [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details) API to automatically renew artifact links, you must update your logic. Please ensure that you download and store artifacts in your own storage service within 24 hours of their generation.

* (Recommended) Configure event notifications: To receive task results reliably and in real time, we highly recommend configuring [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification). This allows you to immediately receive artifact information upon task completion and trigger your subsequent workflows, effectively mitigating any impact from this storage policy update.

If you have any questions about this update, please feel free to [submit a ticket](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00001112) or contact your account manager.

Thank you for your understanding and continued support.
