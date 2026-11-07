---
title: "CLI Overview"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/edge-function-cli-overview-en"
---

In addition to the console and OpenAPI, you can also use the Edge Functions CLI to manage functions and Edge KV. Compared to the console and OpenAPI, the Edge Functions CLI also supports the following additional features:


* Create one or multiple local functions

* Edit and debug local function code

* Perform CRUD operations and publish one or multiple local functions

* Synchronize local functions with remote functions


Edge Functions CLI allows you to write and debug function code locally, and publish the local function code to the Edge Functions server.

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_ce10bdc6fec1bd4a8f76370054340caa.png) </span>

<span id="basic-concepts"></span>
## Basic concepts

Before using Edge Functions CLI, we recommend that you understand the following basic concepts.

<span id="remote-function"></span>
### Remote function

Functions created on the Edge Functions server. Each remote function has a unique function ID as its identifier.

<span id="local-function"></span>
### Local function

Functions created in your function project. Local functions may not have a function ID. You can associate a local function with a remote function's ID.

<span id="function-project"></span>
### Function project

A Node.js project including a function project configuration file (nest.json) used to manage local functions. You use [nest init](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-init-en) to create a function project.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><a href="https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-init-en">nest init</a> also creates a local function within that function project.</div>


A function project can include one or more local functions, but only one local function can be the default function. You can use [nest functions create](https://docs.byteplus.com/docs/byteplus-cdn/cli-ref-nest-function-en#create) to create a local function in a function project.

<span id="project-configuration"></span>
### Project configuration

Project configuration includes information about the function project's working directory, entry code file directory, information about all local functions in the function project, and Edge KV data. Project configurations can be categorized into function project configurations and global project configurations.


* **Function project configuration**: Stored in the `nest.json` file in the root directory of each function project. The function project configuration file applies to the current project.

* **Global project configuration**: Stored in the `~/.nest.json` file. The global project configuration file applies to all function projects.


Edge Functions CLI first obtains project configurations from the function project configuration file. If this fails, Edge Functions CLI obtains project configurations from the global project configuration file.
