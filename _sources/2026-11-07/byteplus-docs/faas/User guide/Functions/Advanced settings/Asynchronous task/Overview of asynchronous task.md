---
title: "Overview of asynchronous task"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/Overview_of_asynchronous_task"
---

Asynchronous task is a new function execution mechanism launched by FaaS, which responds to call requests in an asynchronous mode, returning the RequestId immediately after completing the event scheduling, without blocking client resources. Additionally, asynchronous tasks support tracking and saving the status at various stages of the task, providing rich task control and observability features. This document introduces the supported operating modes, usage scenarios, and usage processes of asynchronous tasks.

<span id="mode-selection"></span>
## Mode selection

FaaS supports users executing asynchronous tasks in either **Webserver mode** or **non\-Webserver mode**. Both modes differ only in business operation modes, with no significant differences in applicable business scenarios, allowing you to choose based on actual needs.


* **Webserver mode**: Similar to the conventional synchronous mode, users provide an HTTP Server on the business side to handle requests and return a response after the request is executed. The difference lies in that: upon receiving a task submission request from the client, FaaS does not wait synchronously for the HTTP Server response but immediately returns a 202 Accepted to the client. It then asynchronously schedules the request in the background, sends it to the HTTP Server, waits for a response, and determines whether the task was successful based on the response status code (status codes of 400 or higher indicate task failure).

* **Non\-Webserver mode**: Executes a one\-time script task, with the process voluntarily exiting after task completion or exiting due to a script error. FaaS determines the success of the task based on the exit status of the script (exit status code 0 indicates success, others indicate failure). Specifically, in the scenario where a task times out, FaaS will forcibly terminate the process and mark the task as failed.


<span id="usage-scenario"></span>
## Usage scenario

Async tasks are primarily suitable for tasks with long execution times or compute\-intensive tasks. They can resolve issues such as continuous resource occupation by the caller and the need for high stability in the calling chain during synchronous calls. The specific applicable scenarios are as follows:


* Audio and video, image processing: Generating thumbnails, adding watermarks, content moderation, transcoding, etc.

* Scheduled tasks: Regularly fetching data, web scraping, etc.

* Offline calculations: Asynchronously refreshing statuses, offline queries, etc.

* ETL large volume data processing: Data cleaning, transformation, analysis, etc.

* CI/CD: Building images asynchronously, and more.

* AI inference scenarios: Generating images, generating videos, and more.

* AI training scenarios: Data collection, data preprocessing, feature engineering, model training, and more.

* High\-performance computing scenarios: industrial simulation, etc.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Async tasks introduce additional system overhead and are not suitable for scenarios that are highly sensitive to latency and require high QPS:</div>



* <div data-tips="true" data-tips-type="warning">Extremely sensitive to request processing latency, requiring an average latency of less than 100 milliseconds.</div>


* <div data-tips="true" data-tips-type="warning">Needs to initiate calls hundreds of times per second or even more frequently.</div>



<span id="usage-process"></span>
## Usage process

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_87d6cea8628cc4f9461d2a11a7be275c.png) </span>


1. [Enable async task](https://docs.byteplus.com/en/docs/faas/Configuring_async_tasks)

   1. Create async task functions.

   2. Release the function and configurations online.

2. [Submit task](https://docs.byteplus.com/en/docs/faas/Submit_task)

   * Supports configuration triggers, submitting tasks via HTTP(S) calls or other event\-driven methods.

   * Support testing through functions and simulating trigger tasks.

3. [Monitor task execution](https://docs.byteplus.com/en/docs/faas/Task_monitoring)

   Support tracking the execution status of tasks, querying task executions from the past 30 days or the latest 1000 tasks, and providing comprehensive monitoring metrics and logging capabilities.
