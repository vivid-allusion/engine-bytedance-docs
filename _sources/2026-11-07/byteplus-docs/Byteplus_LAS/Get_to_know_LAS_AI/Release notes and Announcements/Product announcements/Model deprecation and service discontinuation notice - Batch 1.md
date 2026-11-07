---
title: "Model deprecation and service discontinuation notice - Batch 1"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/model-deprecation-and-service-discontinuation-notice-batch-1-e85418810b915df0"
---

# Model deprecation and service discontinuation notice – Batch 1

Dear BytePlus LAS users,

Thank you for your continued support of BytePlus Lake AI Service (LAS).

To promote technological upgrades and provide services with better performance and greater cost efficiency, we have decided to adjust and discontinue certain operators on the platform.

## Schedule

|Stage |Date (UTC+8) |Action and impact |
|---|---|---|
|Notification |October 10, 2026 |Check whether you are using any operator or model listed in this notice and switch to the recommended replacement. |
|Service degradation |October 15, 2026 |Traffic to the affected operators may be restricted, and new calls may be rejected. |
|Service termination |October 22, 2026 |The affected operators and model versions will be officially discontinued, and requests will be rejected. |

## Affected LAS operators and migration recommendations

The following LAS operators and model versions will be affected. Complete the migration before service termination to prevent service interruptions.

|Affected model versions |LAS operator |Migration recommendation |
|---|---|---|
|`seed-1-8-251228` |Multimodal Deep Thinking (Doubao\-Seed\-1.8)<br><br>[Fine-grained video understanding](https://docs.byteplus.com/docs/Byteplus_LAS/Fine-grained_video_understanding) |Switch to `doubao-seed-2-0-pro-260215`. |
|`dola-seed-2-0-mini-260215` |[Fine-grained video understanding](https://docs.byteplus.com/docs/Byteplus_LAS/Fine-grained_video_understanding)<br><br>[Multimodal Deep Thinking (Doubao-Seed-2.0)](https://docs.byteplus.com/docs/Byteplus_LAS/Multimodal-Deep-Thinking-Doubao-Seed-2-0) |Switch to `doubao-seed-2-0-mini-260428`. |
|`dola-seed-2-0-lite-260228` |[Fine-grained video understanding](https://docs.byteplus.com/docs/Byteplus_LAS/Fine-grained_video_understanding)<br><br>[Multimodal Deep Thinking (Doubao-Seed-2.0)](https://docs.byteplus.com/docs/Byteplus_LAS/Multimodal-Deep-Thinking-Doubao-Seed-2-0) |For the Seed 2.0 Lite model, specify a newer model version and provide the ModelArk API key and Base URL directly. This allows the LAS operator to invoke the newer Seed 2.0 Lite model through ModelArk.<br><br><br>1. Obtain the ModelArk API key and Base URL.<br><br>2. Update the request parameters of the corresponding LAS operator:<br><br>   1. Switch to a newer Doubao Seed 2.0 model, such as `doubao-seed-2-1-lite-260915` or `doubao-seed-2-1-pro-260915`.<br><br>   2. Replace the LAS API key and Base URL used by the LAS operator with the ModelArk API key and Base URL.<br><br><br>> **Note**<br><br><br>> After the switch, subsequent charges for the corresponding LAS operator will appear on your ModelArk bill.<br> |

If you encounter technical issues during migration, [submit a ticket](https://console.byteplus.com/workorder/create?ref=L2xhcy9yZWdpb246bGFzK2FwLXNvdXRoZWFzdC0xL25leHQvaG9tZQ%3D%3D) to contact BytePlus technical support.

We apologize for any inconvenience caused by this service adjustment and appreciate your understanding.

BytePlus LAS Team
