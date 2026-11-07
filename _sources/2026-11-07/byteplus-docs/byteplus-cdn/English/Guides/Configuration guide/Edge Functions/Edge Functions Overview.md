---
title: "Edge Functions Overview"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-overview-of-edge-function"
---

Edge Functions provide function services and edge KV services.


* Function service is a serverless computing service on BytePlus's global edge nodes. You can write JavaScript code for functions, then publish the functions to deploy the JavaScript code on global edge nodes for processing user requests.

* Edge KV service is a distributed key\-value storage service on BytePlus's global edge nodes. Edge KV is suitable for scenarios with low\-frequency writes and high\-frequency reads.


<span id="application-scenarios"></span>
## Application scenarios

<span id="edge-side-rendering"></span>
### Edge\-side rendering

You can use Edge Functions to build an edge gateway for edge\-side rendering. Compared to server\-side rendering, edge\-side rendering reduces the user's first screen loading time and lightens the server\-side workload.

For example, when a user needs to access a web page. When the user's request reaches the edge gateway, the edge gateway first retrieves static HTML from the origin server or CDN cache and returns it to the user. At this point, the client browser begins parsing the HTML and generating the DOM tree, while fetching rendering resources from the edge gateway. The edge gateway retrieves static resources (such as .css files, .js files, or image files) from the CDN cache or origin server, and simultaneously retrieves dynamic resources from the origin server through asynchronous requests. The edge gateway prioritizes returning static resources to the user, appends the retrieved dynamic resources to the static resources, and then streams the completed HTML back to the user.

<span id="processing-user-requests-at-the-edge"></span>
### Processing user requests at the edge

You can use Edge Functions to build a high\-performance, highly available edge gateway to perform custom processing of user requests, such as merging or modifying user requests, implementing CORS, authenticating user requests, and more.

<span id="ci-cd"></span>
### CI/CD

You can use Edge Functions to build edge CI/CD pipelines for APIs or websites, enabling functionalities such as data processing, A/B testing, returning personalized content based on user characteristics, request redirection, error fallback and degradation, health checks, concurrent request racing, performance testing, and more.
