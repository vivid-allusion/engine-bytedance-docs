---
title: "Will requests be interrupted during the process of function release?"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/Will_requests_be_interrupted_during_the_process_of_function_release"
---

No. During the function release process, older version instances will continue to operate until all existing requests (including those received during the upgrade process) are fully processed before they are scaled down and terminated.
