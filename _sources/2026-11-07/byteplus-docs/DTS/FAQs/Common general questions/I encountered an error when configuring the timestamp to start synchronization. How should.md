---
title: "I encountered an error when configuring the timestamp to start synchronization. How should I handle it?"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/I_encountered_an_error_when"
---

Errors encountered when configuring the timestamp to start synchronization may be caused by the following reasons.


1. Incorrect timestamp selected

2. Allowlist access limit

3. Abnormal database connection


Solutions are as follows.


1. Check and ensure that the correct timestamp is selected (for example, select the current day's time).

2. Add the relevant IP to the allowlist based on the error prompt.

3. Check the database connection status and, if necessary, do so manually. Resume task.
