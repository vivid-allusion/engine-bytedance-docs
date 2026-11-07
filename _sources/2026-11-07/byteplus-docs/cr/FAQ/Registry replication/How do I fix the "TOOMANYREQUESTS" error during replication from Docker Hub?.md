---
title: "How do I fix the \"TOOMANYREQUESTS\" error during replication from Docker Hub?"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/How-do-I-address-the-error-TOOMANYREQUESTS-reported-during-Docker-Hub-registry-replication"
---

## Issue description

When replicating an instance from Docker Hub to CR, the following `TOOMANYREQUESTS` error may appear. Detailed error message:

`http status code: 429, body: { "errors": [ { "code": "TOOMANYREQUESTS", "message": "You have reached your pull rate limit. You may increase the limit by authenticating and upgrading: https://www.docker.com/increase-rate-limit" } ] }`

## Solution

This error is caused by Docker Hub pull rate limits for free accounts. Solutions:

* **Adjust your pull strategy.**

   The following methods are recommended:

   * Use exact regular expression matching instead of fuzzy matching to avoid pulling unnecessary images.

   * Set the interval to more than six hours to prevent rate limiting caused by frequent image pulls.

* **Upgrade to a Docker Pro or Docker Team account.**

For details, see [https://www.docker.com/increase-rate-limit](https://www.docker.com/increase-rate-limit).
