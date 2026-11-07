---
title: "What can I do if the K8s API server has high load due to a large number of ListWatch requests?"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/troubleshooting_log_collection"
---

In K8s log collection scenarios, if the K8s API server receives a large number of ListWatch requests, issues such as high CPU load, high memory load, and high request latency may occur. The possible causes are as follows:


* Exceptions such as network errors exist in K8s. LogCollector listens on container events through the K8s ListWatch mechanism. LogCollector executes ListWatch once when it starts, and re\-executes ListWatch if a network exception occurs. If such exceptions often occur, it may cause LogCollector to frequently trigger the ListWatch process. In this case, we recommend that you verify whether K8s has such exceptions.

* If a large number of LogCollectors such as more than 1,000 LogCollectors are deployed in a large cluster, we recommend that you implement rate limiting for ListWatch on the API server side. This can avoid excessive load caused by a large number of ListWatch requests to the API server.
