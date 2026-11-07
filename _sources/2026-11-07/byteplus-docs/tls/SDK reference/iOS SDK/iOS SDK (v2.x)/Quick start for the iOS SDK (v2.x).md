---
title: "Quick start for the iOS SDK (v2.x)"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Quick-start-for-the-iOS-SDK-v2-x"
---

This article describes how to quickly use the TLS iOS SDK to collect logs.

## Prerequisites

* The TLS iOS SDK has been installed. It is recommended to use the latest version of the iOS SDK. For detailed steps, see [Install the iOS SDK (v2.x)](https://docs.byteplus.com/en/docs/tls/Install-iOS-SDK-v2-x).

* The business party's short\-term STS credentials have been obtained.

## Notice

* A successful `add` only means that the log has reached the local receiving boundary, not that it has been written to the server.

* The remote result is returned via the `SendResult` callback.

* In production environments, temporary credentials should be used, and the persistence mode should be selected based on business reliability requirements.

## Code examples

This example demonstrates how to create a Producer, send logs with a unique event ID, handle asynchronous results, and safely shut down, with relevant code snippets provided.

1. Create a target and configure authentication.

   1. Create a target.

      ```Swift
      import Foundation
      import VolcengineTLSProducer
      
      let destination = Destination(
          endpoint: "YOUR_ENDPOINT",
          region: "YOUR_REGION",
          projectID: "YOUR_PROJECT_ID",
          topicID: "YOUR_TOPIC_ID"
      )
      
      let configuration = try ProducerConfiguration(
          destination: destination
      )
      ```

   2. Configure authentication.

      `runtimeCredentials` represents the business party's runtime credential provider. It is recommended to use temporary credentials in production environments. Hardcoding long\-term AK/SK in source code or configuration files increases the risk of credential leakage.

      ```Swift
      let credentials = Credentials(
          accessKeyID: runtimeCredentials.accessKeyID,
          accessKeySecret: runtimeCredentials.accessKeySecret,
          securityToken: runtimeCredentials.sessionToken
      )
      ```

2. Open the Producer.

   `open` may create a persistence directory and restore the WAL, so it is an asynchronous interface. Synchronous waiting will block the main thread. The call should be placed in an asynchronous or background path.

   ```Swift
   let producer = try await Producer.open(
       configuration: configuration,
       credentials: credentials
   ) { result in
       switch result.status {
       case .success:
           print("sent requestID=\(result.requestID ?? "-")")
       case .failure:
           print("send failed code=\(result.error?.errorCode ?? "unknown")")
       }
   }
   ```

3. Write logs.

   A successful `add` means the log has been received locally, not that it has been written to the server. The server result is returned via the `onSendResult` callback.

   ```Swift
   let eventID = UUID().uuidString
   let event = LogEvent(contents: [
       "event_id": .string(eventID),
       "level": .string("info"),
       "message": .string("hello tls"),
       "retryable": .bool(true),
       "count": .signedInt(1)
   ])
   
   try producer.add(event)
   ```

   Use `.immediate` when you need to flush batches as soon as possible. It still does not wait for a network response.

   ```Swift
   try producer.add(event, mode: .immediate)
   ```

4. Update temporary credentials (optional).

   After the STS credentials are refreshed, atomically replace the entire set of credentials.

   ```Swift
   try producer.updateCredentials(
       Credentials(
           accessKeyID: newAccessKeyID,
           accessKeySecret: newAccessKeySecret,
           securityToken: newSessionToken
       )
   )
   ```

5. Shut down normally.

   In a normal and controlled exit path, call this after stopping the addition of new logs.

   A successful `close` means local threads have stopped safely, but does not guarantee that all logs have been delivered remotely. In the event of a crash, forced termination, or the system directly ending the process, there may be no opportunity to call it. The persistence mode can be used to recover unconfirmed logs.

   ```Swift
   try await producer.close(timeout: 5)
   ```

6. To verify log writing and complete the closed loop from callback to server query, see [Verify log writing](https://github.com/volcengine/ve-tls-ios-sdk/blob/v2.0.1/docs/getting-started/verify-ingestion.md) for details.
