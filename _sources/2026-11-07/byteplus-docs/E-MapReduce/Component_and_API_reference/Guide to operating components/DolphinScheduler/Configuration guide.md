---
title: "Configuration guide"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Configuration_guide"
---

Through the Volcano Engine E\-MapReduce (EMR) console, you can elegantly and conveniently modify the runtime configuration parameters of DolphinScheduler. This document introduces some key configurations of DolphinScheduler.

<span id="_1-使用前提"></span>
## 1 Prerequisites


1. An EMR cluster containing the DolphinScheduler component has been created. For details, see [Create clusters (version 3.18.0 and earlier)](https://docs.byteplus.com/docs/E-MapReduce/105456).


<span id="_2-配置入口"></span>
## 2 Configuration entry


1. Log in to the [EMR console](https://console.volcengine.com/emr/region:emr_fe+cn-beijing/project/default/home).

2. In the left navigation pane, click **Cluster Management \> Cluster List \> DolphinScheduler Cluster Details \> Service List \> DolphinScheduler \> Service Parameters,**  to enter the service parameter configuration interface.


For detailed parameter configuration operations, see: [Manage service configuration parameters](https://docs.byteplus.com/docs/E-MapReduce/105412)

<span id="_3-common-配置"></span>
## 3 Common configuration

The configuration file dolphin_scheduler\-common is mainly used to configure Hadoop/YARN\-related configuration items, as shown in the following table:


|Parameter |Default value |Description |
|---|---|---|
|data_basedir_path |/tmp/dolphinscheduler |Local working directory for storing temporary files |
|hdfs_root_user |hdfs |If the storage type is HDFS, you need to configure a user with the corresponding operation permissions. |
|hadoop_security_authentication_startup_state |false |Whether Hadoop enables Kerberos authentication (If needed, you may [submit a ticket](https://console.volcengine.com/workorder/create/) to consult EMR support personnel.) |
|java_security_krb5_conf_path |/opt/krb5.conf |Kerberos configuration directory |
|login_user_keytab_username |hdfs\-mycluster@ESZ.COM |Kerberos login user |
|login_user_keytab_path |/opt/hdfs.headless.keytab |Kerberos login user keytab |
|kerberos_expire_time |2 |Kerberos expiration time. Accepts an integer. Unit: hours |
|development_state |false |Whether in development mode |
|dolphin_scheduler_network_interface_preferred |NONE |Network interface name |
|dolphin_scheduler_network_priority_strategy |default |IP acquisition strategy; default prioritizes internal network |
|resource_manager_httpaddress_port |8088 |Port of ResourceManager |
|datasource_encryption_enable |false |Whether to enable datasource encryption |
|datasource_encryption_salt |!@#$%^&\* |Salt used for datasource encryption |
|data_quality_jar_name |dolphinscheduler\-data\-quality\-dev\-SNAPSHOT.jar |Configure the jar package used for data quality |
|support_hive_oneSession |false |Set whether hive SQL is executed in the same session |
|sudo_enable |true |Whether to enable sudo |
|alert_rpc_port |50052 |RPC port of Alert Server |
|zeppelin_rest_url |http://localhost:8080 |zeppelin RESTful API endpoint address |


<span id="_4-api-server-配置"></span>
## 4 API Server configuration


|Parameter |Default value |Description |
|---|---|---|
|server_port |12345 |API service communication port |
|server_servlet_session_timeout |120m |Session timeout |
|server_servlet_context_path |/dolphinscheduler/ |Request path |
|spring_servlet_multipart_max_file_size |1024MB |Maximum upload file size |
|spring_servlet_multipart_max_request_size |1024MB |Maximum request size |
|server_jetty_max_http_post_size |5000000 |Maximum Jetty service request size |
|spring_banner_charset |UTF\-8 |Request encoding |
|spring_jackson_time_zone |UTC |Set time zone |
|spring_jackson_date_format |"yyyy\-MM\-dd HH:mm:ss" |Set time format |
|spring_messages_basename |i18n/messages |i18n configuration |
|traffic_control_global_switch |false |Global traffic control switch |
|traffic_control_max_global_qps_rate |300 |Global maximum requests per second |
|traffic_control_tenant_switch |false |Tenant traffic control switch |
|traffic_control_default_tenant_qps_rate |10 |Default tenant maximum requests per second limit |
|traffic_control_customize_tenant_qps_rate | |Custom tenant maximum requests per second limit |


<span id="_5-master-server-配置"></span>
## 5 Master Server configuration


|Parameter |Default value |Description |
|---|---|---|
|master_listen_port |5678 |Master listening port |
|master_fetch_command_num |10 |Number of commands fetched by master |
|master_pre_exec_threads |10 |Number of tasks prepared for execution by master, used to limit concurrent commands |
|master_exec_threads |100 |Number of master worker threads, used to limit the number of concurrent process instances |
|master_dispatch_task_number |3 |Number of tasks dispatched per batch by master |
|master_host_selector |lower_weight |Master host selector, used to select an appropriate worker to execute tasks. Available options: random, round_robin, lower_weight. |
|master_heartbeat_interval |10 |Master heartbeat interval, Unit: seconds |
|master_task_commit_retry_times |5 |Task retry count |
|master_task_commit_interval |1000 |Task submission interval, Unit: milliseconds |
|master_state_wheel_interval |5 |Polling status check interval |
|master_max_cpu_load_avg |\-1 |Maximum average CPU load for master. The master service can only schedule tasks when the system CPU load average is lower than this value. The default value is \-1. At runtime, it will be set to twice the number of CPU cores of the current machine. |
|master_reserved_memory |0.3 |Master reserved memory. The master service can only schedule tasks when the available system memory is higher than this value. Unit: GB |
|master_failover_interval |10 |Failover interval, Unit: minutes |
|master_kill_yarn_job_when_task_failover |true |Whether to kill the yarn job when a task instance fails over. |
|master_registry_disconnect_strategy_strategy |stop |Strategy adopted after the master loses connection with the registry. The default value is stop. Available options: stop, waiting. |
|master_registry_disconnect_strategy_max_waiting_time |100s |Reconnect time after the master loses connection with the registry; this value takes effect when the strategy is set to waiting. This value indicates that when the master loses connection with the registry, it will attempt to reconnect within the specified time. If reconnection fails within the given time, the master will stop itself. During reconnection, the master will discard the currently running workflow. A value of 0 means it will wait indefinitely. |
|master_master_worker_group_refresh_interval |10s |Interval for periodically synchronizing workerGroup from the database to memory. |


<span id="_6-worker-server-配置"></span>
## 6 Worker Server configuration


|Parameter |Default value |Description |
|---|---|---|
|worker_listen_port |1234 |Worker listening port |
|worker_exec_threads |100 |Number of worker threads, used to limit the number of concurrent task instances. |
|worker_heartbeat_interval |10 |Worker heartbeat interval. Unit: seconds. |
|worker_host_weight |100 |Worker host weight when assigning tasks. |
|worker_tenant_auto_create |true |The worker uses the system user corresponding to the tenant to execute job submissions. If the system does not have this user, it will be automatically created when this parameter is set to true. |
|worker_max_cpu_load_avg |\-1 |The worker service can only be assigned tasks when the system cpuload average is below this value. The default value is \-1, which will be set at runtime to twice the number of CPU cores on the current machine. |
|worker_reserved_memory |0.3 |The worker service can only be assigned tasks when the available system memory is above this value. Unit: G. |
|worker_alert_listen_host |localhost |alert listening host |
|worker_alert_listen_port |50052 |alert listening port |
|worker_registry_disconnect_strategy_strategy |stop |The strategy adopted after the worker loses contact with the registry. The default value is stop. Available values include stop and waiting. |
|worker_registry_disconnect_strategy_max_waiting_time |100s |The reconnection time after the worker loses contact with the registry. This value takes effect when the strategy is set to waiting. This value indicates that when the worker loses contact with the registry, it will attempt to reconnect within the given time. If reconnection fails within the given time, it will stop itself. During reconnection, the worker will discard and kill tasks that are currently being executed. A value of 0 means it will wait indefinitely. |
|worker_task_execute_threads_full_policy |REJECT |If set to REJECT, when the number of tasks in the worker's waiting queue reaches exec\-threads, the worker will reject any new incoming tasks, and the primary node will redistribute the task. If set to CONTINUE, the worker will accept the task and place it in the waiting queue, where it will wait for an idle thread to execute the task. |


<span id="_7-alert-server-配置"></span>
## 7 Alert Server configuration


|Parameter |Default value |Description |
|---|---|---|
|server_port |50053 |Alert Server listening port |
|alert_port |50052 |alert listening port |


<span id="_8-quartz-配置"></span>
## 8 Quartz configuration


|Parameter |Default value |Description |
|---|---|---|
|spring_quartz_properties_org_quartz_threadPool_threadPriority |5 |Set thread priority (maximum is 10, minimum is 1, default is 5). |
|spring_quartz_properties_org_quartz_jobStore_isClustered |TRUE |Indicates whether Quartz is deployed in a clustered configuration. Clustered Quartz can improve performance through load balancing and provides better fault tolerance. If the application is set to false in a cluster, an error will occur. |
|spring_quartz_properties_org_quartz_jobStore_class |org.quartz.impl.jdbcjobstore.JobStoreTX |All Quartz data, such as the details of jobs and triggers, are saved in memory or a database. There are two implementations: JobStoreTX (manages transactions independently) and JobStoreCMT (transactions managed by the application server, that is, global transactions JTA). |
|spring_quartz_properties_org_quartz_scheduler_instanceId |AUTO |It is recommended to set to AUTO in cluster mode to avoid ID conflicts between different instances. |
|spring_quartz_properties_org_quartz_jobStore_tablePrefix |QRTZ_ |Table prefix |
|spring_quartz_properties_org_quartz_jobStore_acquireTriggersWithinLock |TRUE |Whether a lock is required when triggering a job. |
|spring_quartz_properties_org_quartz_scheduler_instanceName |DolphinScheduler |Each instance in the cluster must have a unique instanceId, but should have the same instanceName. |
|spring_quartz_properties_org_quartz_threadPool_class |org.quartz.simpl.SimpleThreadPool |The implementation class of the thread pool (fixed\-size thread pool, which can meet the needs of almost all users). |
|spring_quartz_properties_org_quartz_jobStore_useProperties |FALSE |Indicates the form of all values in JobDataMaps of JDBCJobStore. If true, they are stored as "key\-value" text; if false, they are stored as serialized objects in the BLOB field. In the context of DolphinScheduler, serialization is required. |
|spring_quartz_properties_org_quartz_threadPool_makeThreadsDaemons |TRUE |Set whether to use daemon threads. |
|spring_quartz_properties_org_quartz_threadPool_threadCount |25 |Specifies the number of threads, at least 1 (generally set to an integer between 1 and 100). |
|spring_quartz_properties_org_quartz_jobStore_misfireThreshold |60000 |The maximum tolerable trigger timeout (before the trigger is considered "misfired"). If exceeded, it is considered a missed trigger. The default is 60 seconds. |
|spring_quartz_properties_org_quartz_scheduler_makeSchedulerThreadDaemon |TRUE |Specifies whether the main thread of the scheduler is a background thread. |
|spring_quartz_properties_org_quartz_jobStore_driverDelegateClass |org.quartz.impl.jdbcjobstore.StdJDBCDelegate |Similar to the dialect in Hibernate, used to handle differences between databases. StdJDBCDelegate can meet the needs of most databases. |
|spring_quartz_properties_org_quartz_jobStore_clusterCheckinInterval |5000 |The frequency of check\-in to the database (Unit: milliseconds), checks whether other instances failed to check in at their scheduled time. This can identify a failed instance, and the current Scheduler will take over the execution of failed and recoverable jobs based on the check\-in operation. The Scheduler will also update its own status record. |
