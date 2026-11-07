---
title: "What are the procedures involved in a cold start and how long does it take?"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/What_are_the_procedures_involved_in_a_cold_start_and_how_long_does_it_take"
---

* The main processes of a cold start include downloading function code, launching containers, and initializing runtime.

* The size of the code package affects the duration of the cold start. The larger the code package, the longer the time for the cold start. Without binding to a VPC, the average duration of a cold start usually ranges from several tens to hundreds of milliseconds.
