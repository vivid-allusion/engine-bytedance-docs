---
title: "Why does the task status remain unchanged after the task is terminated and deleted?"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/why_does"
---

When terminating and deleting a task, the verification tasks associated with the task itself will be terminated first. If the number of verification tasks exceeds 100, they may not all be released in one go. In such cases, you need to manually delete some of the verification tasks associated with the task first before proceeding with the termination or deletion operation. Refer to [Deleting verification tasks](https://docs.byteplus.com/en/docs/DTS/viewing_data_validation#.5ZCO57ut5pON5L2c) for details.
