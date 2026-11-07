---
title: "Guide for troubleshooting performance issues caused by excessive logical sessions"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/Guide_for_troubleshooting_performance_issues_caused_by_excessive_logical_sessions"
---

When the number of logical sessions in a MongoDB instance continuously accumulates and exceeds the server's allowed upper limit, the server will reject new session creations, preventing business requests from executing normally. This topic describes troubleshooting methods, emergency handling, and alert configurations for issues with excessive logical sessions, helping you quickly identify the problem and restore business.

<span id="6vLCKoEt"></span>
## Background

When the number of logical sessions continuously increases, it primarily leads to the following consequences:


* Continuous resource consumption: Even if business traffic has not increased, the session count continues to climb, and memory usage steadily increases, impacting overall performance.

* Difficult operational recovery: Once sessions accumulate to the server's upper limit, they cannot be automatically Reclaimed. Manual intervention, such as a restart or expand, is required for recovery.


The MongoDB server imposes an upper limit on the number of logical sessions (default 1 million). When the session count reaches this upper limit, new requests will return a `TooManyLogicalSessions` error. When the session count reaches 100,000, though far from hitting the hard limit, it already indicates resource leaks or an unsuitable architecture; continued growth will lead to service unavailability. It is recommended to proactively investigate when the number of sessions reaches 100,000.

<span id="yrolDP4r"></span>
## Root cause diagnosis

<span id="9gfv2dg7"></span>
### Root cause

Too many logical sessions essentially means that sessions created by the application are not released promptly. The MongoDB driver automatically manages implicit sessions when performing a single operation. However, after the application explicitly calls `startSession()` (e.g., for multi\-document transactions), the application is responsible for the session's lifecycle. If not closed before the request ends, the session will continue to occupy server resources until the limit is reached.

<span id="QdEmA47n"></span>
### Quick diagnosis


* View console monitoring data

   Log in to the MongoDB console, go to the Alerts and monitoring page of the target instance, view the logical sessions metric, and confirm the current value and growth trend. For specific procedures, refer to [Viewing monitoring data](https://docs.byteplus.com/en/docs/mongodb/view-monitoring-data).

* Run a command to view active sessions

   ```JSON
   // View all active sessions for the current instance
   db.adminCommand({ listSessions: { allUsers: true } })
   
   // View the total number of current sessions
   db.adminCommand({ listSessions: { allUsers: true } }).sessions.length
   ```
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Executing the above command requires the <code>listSessions</code> permission. If you don't have the necessary permissions, contact your administrator to grant them or view monitoring data through the console.   </div>
   

   Example of returned results after execution

   ```JSON
   {
     "sessions" : [
       { "id" : { "id" : UUID("...") }, "username" : "test", "lastUse" : ISODate("...") },
       ...
     ],
     "totalOpen" : 3521
   }
   ```
   

   Focus on the number of sessions returned in the `sessions` array and the `lastUse` timestamp, which helps determine if there are many idle sessions that have not been used for a long time.

* Check application\-side code for session leaks

   Review the following items one by one.

   
   |**Check items** |**Description** |
   |---|---|
   |Is `MongoClient `globally reused? |Check if there are multiple `new MongoClient()` instances in the code. MongoClient should be created once during application startup and shared globally, instead of being created new in each request. |
   |Is `startSession()` matched with `endSession()`? |Check all `startSession()` calls to confirm if `endSession()` is executed in finally/defer cleanup logic. Omitted cleanup on exception paths is the most common source of session leaks. |
   |For transaction exceptions, is `abortTransaction()` called before `endSession()`? |Check the cleanup order in the `catch` block: `abortTransaction()` should interrupt the transaction first, then `endSession()` should release the session. Directly closing the session can cause transactions to not end properly and lead to long\-term occupation of server resources. |
   |Do scheduled tasks or batch processes frequently create clients? |For scenarios such as scheduled tasks and batch processing, verify whether a new MongoClient is created for each data batch or task execution. The correct practice is to reuse the same client within the lifecycle of a task or job. |
   |Is there a sudden increase in business traffic or many slow queries? |Compare monitoring curves to confirm if session growth synchronizes with business peaks; view slow query logs to confirm if numerous time\-consuming actions are prolonging session holding time. |
   


<span id="dQACAQ8y"></span>
## Architecture principles

<span id="aieoghgz"></span>
### Client reuse principles

Each process reuses the same `MongoClient` instance; do not create a new client for each request. `MongoClient` internally maintains a connection pool; frequent creation will lead to a surge in connections, exhausting server resources.

<span id="U2xxh08T"></span>
### Session Closure Principle

Explicitly calling `startSession()` requires calling `endSession() `to release the session before the request ends. If a transaction error occurs, first call `abortTransaction()`, then end the session. Use mechanisms like `try-with-resources` (Java), `using` (C#), and `defer` (Go) to ensure release.

<span id="RfJrHS2x"></span>
## Solution

<span id="x4garx4s"></span>
### Fix Code

If troubleshooting reveals a session leak in the code, fix it as follows.


|**Item** |**Solution** |
|---|---|
|MongoClient not reused |Instead, create it once during application startup and reuse it globally, preventing new creations for each request. |
|`startSession() `not accompanied by `endSession()` |Add `finally`/`defer` cleanup logic to ensure proper release even on exception paths.<br><br> |
|Transaction exception not aborted first |First execute `abortTransaction()` in the `catch` block, then close the session. |
|Scheduled tasks frequently create clients |Ensure the same client is reused throughout the task's lifecycle; do not create a new client for each data batch. |


After the fix, observe if the session count gradually decreases.

<span id="V5wdfgXK"></span>
### Emergency Recovery

If troubleshooting confirms no code issues and the session count remains high, it indicates that the business workload has exceeded the current instance's capacity. Try the following methods in order:


* Restart application instances

   After application instances run for an extended period, their held database connections and sessions may continuously accumulate. Restarting can release all connections and sessions, helping the session count to drop rapidly. If multiple instances are deployed, restart them one by one to avoid simultaneous operations that could lead to business interruption or traffic overload.

* Upgrade instance specifications

   If business traffic continues to grow and current specifications can no longer meet the demand, you can appropriately increase memory and CPU. For specific procedures, refer to Modifying instance specifications.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Upgrading instance specifications will incur additional costs. Refer to <a href="https://docs.byteplus.com/en/docs/mongodb/billing-item-price?lang=zh">Billing items and prices</a> for details, and assess your business requirements accordingly.</div>


If the problem persists after trying the above methods, submit a ticket to contact technical support.

<span id="olQZW4Es"></span>
## Monitoring and alerts

To promptly detect abnormal growth in the logical session count, configure the following alert rules. For specific procedures, refer to [Setting up alerts](https://docs.byteplus.com/en/docs/mongodb/set-alert?lang=zh) and [Creating alert policies](https://docs.byteplus.com/en/docs/cloudmonitor/Creating-an-alarm-strategy?lang=zh).


|**Threshold** |**Level** |**Recommended Actions** |
|---|---|---|
|\> 10w |Notification |After triggering, initiate a code investigation to check for session leaks. |
|\> 50w |Warning |Once triggered, immediate intervention is required to perform emergency handling. |
