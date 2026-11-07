---
title: "Generating credentials"
product: "API Gateway"
product_code: "apig"
source: "https://docs.byteplus.com/en/docs/apig/Generating_credentials"
---

This article describes how to create consumer\-based information for authentication.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

A consumer has been created. For more details, please refer to [Creating a consumer ](https://docs.byteplus.com/en/docs/apig/Creating_a_consumer).

<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limits


* Key Auth plugin

   * A consumer by default supports 5 API Key.

* HMAC Plugin

   * A consumer can only correspond to 1 AK/SK.

   * AK/SK cannot be deregistered after generating, please save it properly to prevent leakage.


<span id=".55Sf5oiQIEhNQUMg5o-S5Lu25omA6ZyA55qEIEFLL1NL"></span>
## Generate credentials

<span id=".55Sf5oiQIEhNQUMg5o-S5Lu25omA6ZyA55qEIEFLL1NL"></span>
### Generate/upload KeyAuth plugin credentials


1. Log in to the [API Gateway console](https://console.byteplus.com/veapig).

2. In the top navigation bar, select the target region.

3. In the left navigation bar select **consumer management \> consumer list ** .

4. In the consumer list, click the target consumer name to go to the consumer details page.

5. In the credentials area, click **Generate API Key**.

6. In the pop\-up dialog, select **Auto\-create** or **Upload** API Key.

7. Click **Confirm** to view the generated or uploaded API Key.


<span id=".55Sf5oiQIEhNQUMg5o-S5Lu25omA6ZyA55qEIEFLL1NL"></span>
### Generate HMAC plugin credentials


1. Log in to the [API Gateway console](https://console.byteplus.com/veapig).

2. In the top navigation bar, select the target region.

3. In the left navigation bar select **consumer management \> consumer list ** .

4. In the consumer list, click the target consumer name to go to the consumer details page.

5. In the credential region, click **Generate AK/SK ** .

6. In credentials, you can view the generated AK/SK.


&nbsp;

&nbsp;
