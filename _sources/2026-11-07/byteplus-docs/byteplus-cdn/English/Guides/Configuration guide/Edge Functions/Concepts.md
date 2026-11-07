---
title: "Concepts"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-concepts"
---

This document contains the basic concepts of Edge Functions.

<span id="edge-node"></span>
## Edge node

Edge nodes refer to clusters of servers that process data and provide computing services at the network edge. Edge nodes are located close to data sources and end users, and are widely distributed. BytePlus CDN and Edge Functions share edge nodes.

<span id="function"></span>
## Function

Functions in Edge Functions are event\-driven. A function includes function configuration and function code.

<span id="trigger"></span>
## Trigger

Triggers are part of the function configuration. When specific conditions are met, triggers will fire events. Edge Functions support domain name triggers and Cron triggers.


* Domain name trigger: When a user accesses the domain associated with the function via an HTTP or HTTPS request, and the user request matches the function forwarding rules of the domain, the domain name trigger will fire a fetch event. You need to listen for and handle the fetch event in your code.

* Cron trigger: Periodically fires a cron event. You need to listen for and handle the cron event in your code.


<span id="environment-variable"></span>
## Environment variable

You can adjust the behavior of functions without updating the code through environment variables. Environment variables are typically used to store sensitive information such as API keys or environment\-specific configuration information such as URLs for external services. Environment variables are part of the function configuration. Therefore, each time you change environment variables, you need to republish the function for the new environment variables to take effect.

<span id="versions"></span>
## Versions

Each time you publish a function, Edge Functions automatically generates a version for the function. This version includes a snapshot of the function code and function configuration, but does not include triggers. You can manage function code and function configuration through versions.

<span id="canary-release"></span>
## Canary release

A canary release refers to publishing a new version of a function to a portion of edge nodes before publishing it to all edge nodes. You can verify the functionality and performance of the function through these edge nodes. If it meets expectations, you can then publish it to all edge nodes.

<span id="full-release"></span>
## Full release

A full release refers to publishing a function to all edge nodes at once.

<span id="runtime"></span>
## Runtime

The runtime of Edge Functions is the function execution environment on BytePlus's global edge nodes.

<span id="runtime-api"></span>
## Runtime API

The Runtime API is a set of APIs for developers to interact with the runtime of Edge Functions.

<span id="edge-kv"></span>
## Edge KV

Edge KV provides distributed storage services for key\-value pair data.

<span id="namespace"></span>
## Namespace

In Edge KV, a namespace is a logical partition used for categorized management of key\-value pairs. You can create separate namespaces for key\-value pairs of different applications or modules.

<span id="key-value-pair"></span>
## Key\-value pair

Key\-value pairs are the basic units of Edge KV data. The key of a key\-value pair is unique within a namespace.
