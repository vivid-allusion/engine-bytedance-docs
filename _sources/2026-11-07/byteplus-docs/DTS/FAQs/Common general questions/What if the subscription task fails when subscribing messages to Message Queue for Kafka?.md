---
title: "What if the subscription task fails when subscribing messages to Message Queue for Kafka?"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/What_if_the_subscription_task_fails"
---

When configuring the Destination of the DTS data subscription Task as Message Queue for Kafka, task failure usually relates to the Destination Topic configuration, message retention policy, Kafka connection information, network connectivity, permission settings, or source Binlog status. This topic introduces common failure scenarios and corresponding solutions to help quickly identify issues.


* **Scenario one: Task failure caused by Kafka's message cleanup policy**

   * **Issue description:**  The data subscription Task fails after running for a period or encounters issues such as inability to continue consumption or abnormal position after recovery or restart.

   * **Possible cause:**  The message cleanup policy of the Destination Kafka Topic is configured as `DELETE`. With this policy, Kafka automatically deletes historical messages based on retention time or capacity. When the historical position messages relied on by the DTS subscription Task are deleted by Kafka cleanup, the Task may fail to continue processing from the original position, resulting in failure.

   * **Solution:**  It is recommended to check the message cleanup policy and retention time settings of the Destination Kafka Topic to avoid Task recovery failures or unusable positions caused by premature message deletion. If high message traceability and Task recovery capability are required, reasonable extension of the message retention time is recommended. If necessary, recreate the topic and adjust retention parameters, then recreate or recover the subscription task.

* **Scenario two: source end Binlog is cleaned, causing subscription task failure**

   * **Problem description:**  Subscription task suddenly fails during operation, or recovery prompts unable to obtain source end incremental log, nonexistent position, and other abnormalities.

   * **Possible cause:**  Binlog used for subscription on source database has been cleaned, DTS cannot continue reading incremental data from the original position. If source end retention time is too short, log generation speed is too fast, or the task has long delays and backlog, historical Binlog may have been cleaned before task processing.

   * **Solution:**  It is recommended to check the source end Binlog retention policy and appropriately extend the log retention time. Monitor the running status by combining task delay and source end write volume to avoid reading position lagging too far due to backlog. If Binlog has been cleaned and cannot be recovered, usually the subscription task needs to be recreated and the starting position reconfirmed.

* **Scenario three: Kafka connection configuration error causes subscription task failure**

   * **Problem description:**  Task creation or start fails immediately, prompting unable to connect to Kafka, Broker unreachable, connection timeout, authentication failure, and other abnormalities.

   * **Possible cause:**  incorrect connection information for destination Kafka, such as wrong broker address, port, access method, or authentication parameters, causing DTS to fail to establish a proper connection with the Kafka cluster.

   * **Solution:**  verify the following items:

      * Whether the Kafka instance address and port are correctly filled.

      * Whether the network environment of the task can access the destination Kafka.

      * Whether the connection information matches the actual access method of the instance.

      * If authentication is enabled, whether the authentication parameters match those of the Kafka instance.

      After confirming the configuration is correct, you can retest the connection or resubmit the task.

* **Scenario 4: topic does not exist or insufficient permissions cause subscription task failure**

   * **Issue description:**  errors occur during task creation or execution, indicating the topic does not exist, lacks write permission, or the destination refuses to write.

   * **Possible cause:**  the Kafka topic specified at the destination is not pre\-created, or the account used by DTS does not have production write permission for the target topic.

   * **Solution:**  confirm the following key points:

      * Whether the topic name is correctly filled in and if the case matches that of the destination

      * Whether the topic has been created and is in normal state

      * Whether the account number, ACL, or instance authorization policy used by DTS allows writing messages to the topic

      If the topic does not exist, create it on the Kafka side first; if it is a permission issue, configure corresponding write permissions for the DTS task before executing the task again

* **Scenario five: network connectivity failure or restricted network policy causing subscription task failure**

   * **Problem description:**  the task fails when connecting to Kafka or during operation, showing connection timeout, destination unreachable, network abnormal interruption, etc.

   * **Possible cause:**  network link between DTS and destination Kafka is unreachable, or network policy restricts access, such as private network route issues, security group/ACL restrictions, or unstable cross\-region network

   * **Solution:**  for private network scenarios, focus on the following points:

      * Whether DTS and Kafka are in mutually accessible network environments

      * Whether security group, network ACL, allowlist, and other configurations have allowed related access.

      * Whether chain instability issues are caused by cross\-region or cross\-network access.

* **Scenario 6: severe task backlog causing position failure or recovery failure**

   * **Issue description:**  Task experiences long delay and severe backlog, leading to position abnormality, inability to continue subscription, or recovery failure.

   * **Possible cause:**  When the task remains in a high delay or backlog state for a long time, source end logs or destination end messages may expire or be cleared before the task processes them, causing DTS to fail to continue processing data from the original position. Usually related to factors such as fast incremental writing on the source end, insufficient Kafka write capacity, insufficient log retention time, or prolonged task abnormality without recovery.

   * **Solution:**  Recommended to troubleshoot and optimize from the following directions:

      * Extend source end Binlog retention time.

      * Extend Kafka Topic message retention time.

      * Check Kafka instance load and Topic write capacity.

      * Monitor DTS task delay changes and promptly handle abnormal backlogs.

      * Evaluate link throughput capacity and optimize configuration or split subscription tasks if necessary.

      If the position has expired and cannot be recovered, it usually requires recreating the subscription task and reevaluating the start position and historical message retention policy.
