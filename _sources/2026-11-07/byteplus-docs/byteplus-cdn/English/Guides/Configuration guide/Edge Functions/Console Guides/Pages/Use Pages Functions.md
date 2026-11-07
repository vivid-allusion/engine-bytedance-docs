---
title: "Use Pages Functions"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/use-pages-functions_en"
---

This document describes how to use Functions in Pages and explains how Functions routes are generated.

<span id="what-are-pages-functions"></span>
## What Are Pages Functions

Pages supports lightweight dynamic capabilities through the `/functions` directory in your project. In addition to serving static sites, you can use Functions to handle simple API requests or dynamic logic.

<span id="route-generation-rules"></span>
## Route Generation Rules

Functions routes are generated automatically from the `/functions` directory in the project.

For example:


* `functions/api/hello.js` is generated as the `/functions/api/hello` route.


<span id="where-to-view-functions-routes"></span>
## Where to View Functions Routes

On the **Deployments** tab, click a **Deployment ID** to enter the **Deployment Details** page.

If the current deployment contains a `/functions` directory, you can view the corresponding Functions route configuration on the **Functions** tab.

If the project does not contain a `/functions` directory, no function routes are displayed on that tab.

<span id="notes"></span>
## Notes


* The file path in the `/functions` directory determines the access path of the Functions route.

* Functions route information is based on the current deployment content. When the deployment content changes, the displayed route configuration also changes.
