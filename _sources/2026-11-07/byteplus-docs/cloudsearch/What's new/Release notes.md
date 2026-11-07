---
title: "Release notes"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/release_notes"
---

This topic describes the features and version updates of the cloud search service across different kernel versions.

**2026**

## October 2026

|**Feature** |**Feature description** |Release date |**Release regions** |**Related documentation** |
|---|---|---|---|---|
|Support storage\-compute separation architecture |The PaaS edition instance supports a storage\-compute separation architecture based on TOS object storage, decoupling compute nodes from storage resources. Storage is billed per usage. Compute resources can scale elastically and independently, improving resource utilization, reducing storage costs, and flexibly adapting to business load changes. |2026\-10\-26 |All |[Create an instance](https://docs.byteplus.com/en/docs/cloudsearch/creating-instance) |
|Support availability zone migration |When resources are insufficient in the instance’s availability zone, you can use the availability zone migration feature to smoothly move the instance within the same region from one availability zone to another to alleviate single\-AZ resource pressure. |2026\-10\-26 |All |[Migrate availability zone](https://docs.byteplus.com/en/docs/cloudsearch/Availability_zone_migration) |
|Support index encryption |For indexing sensitive data such as storage PII (personally identifiable information), static encryption is provided based on KMS to meet security compliance requirements. |2026\-10\-26 |All |[Index management](https://docs.byteplus.com/en/docs/cloudsearch/index_management) |
|Cold data nodes support RL0 storage |The cold data node now supports RL0 storage type, focusing more on read performance. It suits cold data scenarios with low write frequency and helps reduce storage costs. |2026\-10\-26 |all |[Create an instance](https://docs.byteplus.com/en/docs/cloudsearch/creating-instance) |
|Kibana supports a Chinese UI |Kibana interface now supports Chinese, allowing you to switch to the Chinese interface to view and use related features, reducing language barriers and improving ease of use and experience. |2026\-10\-26 |All |[Modify Kibana/Dashboards parameters](https://docs.byteplus.com/en/docs/cloudsearch/Modifying-Kibana-parameters) |

## August 2026

|**Feature** |**Feature description** |Release date |**Release regions** |**Related documentation** |
|---|---|---|---|---|
|Logstash supports public network data push |Supports pushing data to Logstash via the public network. You can configure public network access links through DNAT to forward data sent from external data sources to Logstash, meeting the scenario requirements for external systems to push data to Logstash. |2026\-08\-20 |All |[Configure Logstash access to the public network using DNAT](https://docs.byteplus.com/en/docs/cloudsearch/Use_DNAT_to_configure_Logstash_access_from_the_public_network) |

## July 2026

|**Feature** |**Feature description** |Release date |**Release regions** |**Related documentation** |
|---|---|---|---|---|
|Configure SAML authentication to implement single sign\-on |By using SAML authentication, you can integrate Elasticsearch and OpenSearch instances into the enterprise identity system, enabling users to access through single sign\-on. |2026\-07\-22 |All |[Configure SAML authentication to implement single sign-on](https://docs.byteplus.com/en/docs/cloudsearch/Configure_SAML_authentication_to_implement_single_sign-on) |
|Supports updating instance SSL certificates |To avoid business impact from SSL certificate expiration, the system sends an early reminder before the certificate expires. You can update the instance SSL certificate accordingly. |2026\-07\-22 |All |[Update instance SSL certificates](https://docs.byteplus.com/en/docs/cloudsearch/Update_instance_SSL_certificates) |
|Support instance log export |Supports exporting instance logs locally for easier archiving, offline analysis, and troubleshooting, which helps assist instance operations. |2026\-07\-22 |All |[Query logs](https://docs.byteplus.com/en/docs/cloudsearch/querying-logs) |
|Public network IP allowlist configuration optimization |The public network IP allowlist configuration process is optimized. When enabling public network access for an instance, the allowlist configures automatically without separate settings later, reducing instance status changes, simplifying operations, and improving public network access configuration efficiency. |2026\-07\-22 |All |[Configure instance public network access](https://docs.byteplus.com/en/docs/cloudsearch/enabling-public-access) |
|Cloud Monitor metrics support node deselection |Cloud Monitor adds node deselection capability, allowing users to cancel or retain monitoring data display for specified nodes with one click, helping them quickly focus on target nodes and improve monitoring analysis and troubleshooting efficiency. |2026\-07\-22 |All |[View monitoring data](https://docs.byteplus.com/en/docs/cloudsearch/viewing-monitoring) |

## May 2026

|**Feature** |**Feature description** |Release date |**Release regions** |**Related documentation** |
|---|---|---|---|---|
|Supports log export via OpenAPI |Supports exporting specified logs by time range, keyword, node, log level, component, and file type through OpenAPI calls for troubleshooting, audit analysis, and automated operations scenarios. |2026\-05\-22 |All |[ListLogs](https://docs.byteplus.com/en/docs/cloudsearch/ListLogs) |
|Support global domain names |After turning on the global domain name, it can be resolved to the corresponding IP address in all regions of BytePlus, meeting cross\-region access and global interconnection needs.<br><br>> **tip**<br><br><br>> The global domain name feature is being gradually released. To use it, please [submit a ticket](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000255) to contact technical support.<br> |2026\-05\-22 |All |[Enable global domain name](https://docs.byteplus.com/en/docs/cloudsearch/Enable_global_domain_name) |

## April 2026

|**Feature** |**Feature description** |Release date |**Release regions** |**Related documentation** |
|---|---|---|---|---|
|Dynamic control of availability zone storage type |Support dynamic control of storage type admission by availability zone during instance creation, automatically filtering restricted types to avoid unsupported configurations that cause errors, improving creation success rate. |2026\-04\-28 |All |[Create an instance](https://docs.byteplus.com/en/docs/cloudsearch/creating-instance) |
|Logstash metadata migration pipeline supports comparison functionality |Support comparing metadata between source and target in the Logstash metadata migration pipeline, automatically identifying differences in index, mapping, and configuration. |2026\-04\-28 |All |[Metadata migration pipeline comparison](https://docs.byteplus.com/en/docs/cloudsearch/Comparison_feature_of_metadata_migration_pipelines) |
|Logstash metadata migration pipeline configuration optimization |The metadata migration pipeline supports skipping specified index templates and template configurations on demand, enhancing flexibility and control during migration. |2026\-04\-28 |All |[Create pipeline](https://docs.byteplus.com/en/docs/cloudsearch/Create_a_pipeline) |
|Logstash logs support sort operations |Support sorting Logstash logs in ascending or descending order based on time, enabling more efficient identification of key events and exception information. |2026\-04\-28 |All |[Query logs](https://docs.byteplus.com/en/docs/cloudsearch/Query_logs) |

## February 2026

|**Feature** |**Feature description** |Release date |**Release regions** |**Related documentation** |
|---|---|---|---|---|
|Node bandwidth prompts and specification check |When you create or upgrade an instance, the system prompts users about newly added bandwidth packages based on node specification support for Volumes performance and actual available throughput. This guides users to select the appropriate target bandwidth, maximizing Volumes performance and improving resource utilization. |2026\-02\-28 |All |* [Create an instance](https://docs.byteplus.com/en/docs/cloudsearch/creating-instance)<br><br>* [Upgrade an instance](https://docs.byteplus.com/en/docs/cloudsearch/upgrading)<br><br>* [Volumes basic bandwidth reference](https://docs.byteplus.com/en/docs/cloudsearch/Volumes_base_bandwidth_reference) |

## January 2026

|**Feature** |**Feature description** |Release date |**Release regions** |**Related documentation** |
|---|---|---|---|---|
|Support OpenSearch version 3.3.0 instances |Supports creating and using OpenSearch version 3.3.0 instances for enhanced performance capabilities. |2026\-01\-30 |All |[Product specifications](https://docs.byteplus.com/en/docs/cloudsearch/specifications) |
|Support resource calculator |You can estimate the required resource scale based on the provided experimental data and adjust it during actual deployment according to the test results. |2026\-01\-30 |All |[Resource calculator](https://docs.byteplus.com/en/docs/cloudsearch/Resource_calculator) |
|Enable user\-defined elastic public IP |When enabling public network access for instance, and Cerebro, you can associate a custom elastic public IP. |2026\-01\-30 |All |* [Configure instance public network access](https://docs.byteplus.com/en/docs/cloudsearch/enabling-public-access)<br><br>* [Configure Cerebro public network access](https://docs.byteplus.com/en/docs/cloudsearch/Configure_Cerebro_public_network_access) |
|Support recovering snapshots from TOS |Supports recovering instance data using snapshot files stored in TOS buckets, facilitating data recovery across environments or during data migration. |2026\-01\-30 |All |[Recover data using snapshot](https://docs.byteplus.com/en/docs/cloudsearch/recovering_data_using_a_snapshot) |
|Create scenario\-based instances |When creating an instance, recommend version and specification configurations based on user application scenarios to improve instance selection efficiency. |2026\-01\-30 |All |[Create an instance](https://docs.byteplus.com/en/docs/cloudsearch/creating-instance) |

**2025**

## December 2025

|**Feature** |**Feature description** |Release date |**Release regions** |**Related documentation** |
|---|---|---|---|---|
|New ContextSearch launched |* Redesigned homepage for faster search, template\-based scenario creation, and sample scenario experience.<br><br>* Supports video search. After uploading content, the system automatically extracts semantic features for similarity retrieval based on video content.<br><br>* Supports serverless capabilities, eliminating the need for resource planning or management, reducing operation complexity and costs.<br><br>* Models and inference services are decoupled from cloud search instances for more flexible use.<br><br>* Supports Doubao 1.6 large model.<br><br>* Knowledge base and picture search scenarios support viewing slice details and deleting slices.<br><br>* Knowledge base scenarios support displaying reference documents in output results.<br><br><br>> **tip**<br><br><br>> ContextSearch operates as an independent product. To use it, go to the [ContextSearch console](https://console.byteplus.com/context-search/).<br> |2025\-12\-30 |All |[ContextSearch](https://docs.byteplus.com/en/docs/contextsearch/Release_notes) |
|Logstash supports extension files |Users can upload required driver files through the extended file configuration feature. |2025\-12\-30 |All |[Configure extension files](https://docs.byteplus.com/en/docs/cloudsearch/Configuring_extension_files) |
|Logstash logs support node filtering |Supports filtering logs by node to quickly locate problem nodes, enhancing log analysis efficiency and troubleshooting capabilities. |2025\-12\-30 |All |[Query logs](https://docs.byteplus.com/en/docs/cloudsearch/Query_logs) |
|Logstash pipeline status optimization |Provides all status transition logic and diagrams for various types of pipelines. |2025\-12\-30 |All |[Pipeline status](https://docs.byteplus.com/en/docs/cloudsearch/Pipeline_status) |
|Logstash instance creation optimization |When creating an instance, prompt the compatible Elasticsearch or OpenSearch instance versions for each Logstash version. |2025\-12\-30 |All |[Create a Logstash instance](https://docs.byteplus.com/en/docs/cloudsearch/Create_a_Logstash_instance) |
|Instance creation optimized |Support more instance specifications, defaulting to higher performance storage types. |2025\-12\-30 |All |[Create an instance](https://docs.byteplus.com/en/docs/cloudsearch/creating-instance) |
|Index monitoring optimization |When the number of indexes and shards is too large, provide index cleanup and shard setting suggestions to ensure normal index metric collection and display. |2025\-12\-30 |All |[View monitoring data](https://docs.byteplus.com/en/docs/cloudsearch/viewing-monitoring) |

## November 2025

|**Feature** |**Feature description** |Release date |**Release regions** |**Related documentation** |
|---|---|---|---|---|
|Vector index uses DiskANN + RaBitQ engine by default |Cloud Search introduces the DiskANN algorithm into OpenSearch, achieving an optimal combination of performance and capacity types. It iterates with higher performance and lower cost through RaBitQ quantization technology, enabling lower\-cost vector storage and retrieval at larger data scales. |2025\-11\-28 |All |Use DiskANN + RaBitQ engine |
|Fully managed Logstash data migration |Fully managed Logstash supports cross\-cluster data migration. Simplify configuration process; the system automatically handles data collection, transformation, and loading, ensuring an efficient, reliable, and complete migration. |2025\-11\-28 |All |[Migrates data across clusters using Logstash](https://docs.byteplus.com/en/docs/cloudsearch/migrating-data-across-Logstash) |

## October 2025

|**Feature** |**Feature description** |Release date |**Release regions** |**Related documentation** |
|---|---|---|---|---|
|ContextSearch ** ** launched |AI search is decoupled from OpenSearch instances; it can be used without linking to an OpenSearch instance or linked to multiple OpenSearch instances.<br><br>> **tip**<br><br><br>> ContextSearch operates as an independent product. To use it, go to the [ContextSearch console](https://console.byteplus.com/context-search/).<br> |2025\-10\-31 |All |[ContextSearch](https://docs.byteplus.com/en/docs/contextsearch/Release_notes) |
|Launch of the new Cerebro |A single Cerebro supports managing multiple Elasticsearch and OpenSearch instances. |2025\-10\-31 |All |[Manage Cerebro](https://docs.byteplus.com/en/docs/cloudsearch/Cerebro_management) |

## September 2025

|**Feature** |**Feature description** |Release date |**Release regions** |**Related documentation** |
|---|---|---|---|---|
|No\-code scenarios support image and text search |Image and text search supports queries based on multiple data types, including text, images, and combined image\-text. Users can create professional image and text search services through intuitive operations without understanding the underlying engine. |2025\-09\-18 |All |[Image and text search scenario](https://docs.byteplus.com/en/docs/cloudsearch/Image_and_text_search_scenario) |
|Index management optimization |* Supports search configuration management.<br><br>* Supports user\-defined authorization duration.<br><br>* Supports manual deauthorization.<br><br>* Supports switching authorized users.<br><br>* Compression supports ZSTD.<br><br>* supports turning the index off and on. |2025\-09\-18 |All |[Index management](https://docs.byteplus.com/en/docs/cloudsearch/index_management)<br><br><br>* [Index template management](https://docs.byteplus.com/en/docs/cloudsearch/Managing_index_templates) |

## August 2025

|**Feature** |**Feature description** |Release date |**Release regions** |**Related documentation** |
|---|---|---|---|---|
|Support fully managed Logstash service |Cloud Search Logstash is a server\-side data processing pipeline developed by BytePlus based on the open\-source data collection engine Logstash. It dynamically collects data from multiple sources, transforms the format, and then stores the data in the specified location. This feature requires applying for whitelist access. |2025\-08\-20 |All |Logstash user guide |
|Kibana public network access optimization |After enabling Kibana public network access, users will be prompted to modify the whitelist to ensure normal Kibana public network access. |2025\-08\-20 |All |* [Configure Kibana/Dashboards public network access](https://docs.byteplus.com/en/docs/cloudsearch/enabling-public-access-tool)<br><br>* [Configure Kibana/Dashboards public IP allowlist](https://docs.byteplus.com/en/docs/cloudsearch/public-IPallowlist-for-tool) |
|Automatic snapshot backup supports selecting specific indexes |Supports selecting snapshot targets during automatic snapshot backup creation to reduce resource consumption. |2025\-08\-20 |All |* [Automatically create snapshot](https://docs.byteplus.com/en/docs/cloudsearch/creating_snapshots_automatically)<br><br>* [Automatically create a snapshot](https://docs.byteplus.com/en/docs/cloudsearch/automatic-snapshots) |

## July 2025

|**Feature** |**Feature description** |Release date |**Release regions** |**Related documentation** |
|---|---|---|---|---|
|Supports controlling data migration speed |For tasks involving data migration in the task center, control the data migration speed by adjusting the following parameters:<br><br><br>* ClusterRoutingAllocationNodeConcurrentIncomingRecoveries<br><br>* ClusterRoutingAllocationNodeConcurrentOutgoingRecoveries<br><br>* ClusterRoutingAllocationNodeConcurrentRecoveries<br><br>* ClusterRoutingAllocationNodeInitialPrimariesRecoveries<br><br>* IndicesRecoveryMaxBytesPerSec |2025\-07\-16 |All |* [Create an instance](https://docs.byteplus.com/docs/cloudsearch/creating-instance)<br><br>* [Upgrade an instance](https://docs.byteplus.com/docs/cloudsearch/upgrading)<br><br>* [Shrink data node](https://docs.byteplus.com/docs/cloudsearch/reducing-data-nodes)<br><br>* [Add dedicated master node](https://docs.byteplus.com/docs/cloudsearch/adding-master-nodes)<br><br>* [View system parameters](https://docs.byteplus.com/docs/cloudsearch/View_system_parameters)<br><br>* [View task progress](https://docs.byteplus.com/docs/cloudsearch/task-progress) |
|Support viewing task migration progress |For tasks involving data migration, view the migration progress bar in the task center. |2025\-07\-16 |All |[View task progress](https://docs.byteplus.com/docs/cloudsearch/task-progress) |
|Supports rollback of failed tasks |After plugin upgrade, parameter modification, or kernel version upgrade tasks fail, you can roll back the task to the previous normal state in the task center. |2025\-07\-16 |All |* [View instance details](https://docs.byteplus.com/docs/cloudsearch/instance-details)<br><br>* [Manage system built-in plugins](https://docs.byteplus.com/docs/cloudsearch/manage-built-in-plugins)<br><br>* [Manage user-defined plugins](https://docs.byteplus.com/docs/cloudsearch/install-user-defined-plugins)<br><br>* [Uninstall user-defined plugins](https://docs.byteplus.com/docs/cloudsearch/uninstall-user-defined-plugins)<br><br>* [Modify parameter configuration](https://docs.byteplus.com/docs/cloudsearch/system-parameters) |
|Supports canceling snapshot creation and recovery tasks |You can manually cancel tasks in the task center during snapshot creation and restoration using snapshots. |2025\-07\-16 |All |* [manual snapshot creation](https://docs.byteplus.com/docs/cloudsearch/manual-snapshots)<br><br>* [Recover data using snapshot](https://docs.byteplus.com/docs/cloudsearch/recovering_data_using_a_snapshot) |
|Supports customizing snapshot speed |You can manually set the snapshot creation speed when creating a snapshot. |2025\-07\-16 |All |[manual snapshot creation](https://docs.byteplus.com/docs/cloudsearch/manual-snapshots) |
|Support customizing snapshot recovery speed |Set the snapshot recovery speed manually when creating a snapshot recovery task. |2025\-07\-16 |All |[Recover data using snapshot](https://docs.byteplus.com/docs/cloudsearch/recovering_data_using_a_snapshot) |
|Supports modifying the public access domain names for Kibana and Cerebro |Allow customization of public access domain names for Kibana and Cerebro. |2025\-07\-16 |All |* [Configure Kibana/Dashboards public network access](https://docs.byteplus.com/docs/cloudsearch/enabling-public-access-tool)<br><br>* [Configure Cerebro public network access](https://docs.byteplus.com/docs/cloudsearch/public-access-Cerebro) |
|ES 6.7 instances support Kibana query status persistence |For ES 6.7 instances, previous queries remain in the browser cache after quitting Kibana, allowing reuse upon next login. |2025\-07\-16 |All |[Log in to Kibana/Dashboards](https://docs.byteplus.com/docs/cloudsearch/logging-tool) |
|Supports index management in PaaS model and Serverless Mode |The PaaS model supports index management, index template management, and lifecycle policy management.<br><br>The Serverless Mode supports index template management and lifecycle policy management. |2025\-07\-16 |All |* [Index management](https://docs.byteplus.com/en/docs/cloudsearch/Managing_indexes)<br><br>* [Index template management](https://docs.byteplus.com/docs/cloudsearch/Managing_index_templates)<br><br>* [Lifecycle policy management](https://docs.byteplus.com/docs/cloudsearch/Managing_lifecycle_policies) |
|Add monitoring data metrics |Monitoring data supports shard count by node dimension, including dedicated master nodes, Cold, Hot, and Warm nodes data metrics. |2025\-07\-16 |All |[View monitoring data](https://docs.byteplus.com/docs/cloudsearch/viewing-monitoring) |
|Supports RaBitQ algorithm |Officially released DiskANN vector engine + RaBitQ quantization technology to enable lower\-cost vector storage and retrieval capabilities. |2025\-07\-16 |All |Using the DiskANN vector engine |

## March 2025

|**Feature** |**Feature description** |Release date |**Release regions** |**Related documentation** |
|---|---|---|---|---|
|Add ES version |Added ES 6.8.23 version. |2025\-03\-16 |All |[Create an instance](https://docs.byteplus.com/docs/cloudsearch/creating-an-instance-2) |
|Add storage type |Create instance adds ESSD\-TL0 storage type. |2025\-03\-16 |All |[Create an instance](https://docs.byteplus.com/docs/cloudsearch/creating-an-instance-2) |
|Data plane audit log |OpenSearch version 2.9.0 supports data plane audit log. |2025\-03\-16 |All |[Enable data plane auditing](https://docs.byteplus.com/docs/cloudsearch/enabe-data-plane-audit) |
|Data node restart |Data nodes support selecting one or more nodes for restart. |2025\-03\-16 |All |[Restart instance or node](https://docs.byteplus.com/en/docs/cloudsearch/restarting) |

**2024**

## December 2024

|**Feature** |**Feature description** |Release date |**Release regions** |**Related documentation** |
|---|---|---|---|---|
|Instance downgrade optimization |Instance supports storage downgrade:<br><br><br>* Supports storage specification downgrade of data nodes<br><br>* Supports storage type downgrade in the order of FlexPL \-\> PL0<br><br>* Supports storage bandwidth package size downgrade and turn off |2024\-12\-15 |All |[Downgrade instance](https://docs.byteplus.com/docs/cloudsearch/downgrading) |

## October 2024

|**Feature** |**Feature description** |Release date |**Release regions** |**Related documentation** |
|---|---|---|---|---|
|Configure alarms with one click |Cloud Search has preconfigured alarm templates in the Cloud Monitor console. We recommend using the one\-click alarm feature to set alarm policies for all Cloud Search instance resources in all regions |2024\-10\-15 |All |[Configure alarms with one click](https://docs.byteplus.com/docs/cloudsearch/one_click_alarm) |
|Configure public network access |Enable public network access for instances or visualization tools, currently supporting two configuration methods. First, the system automatically allocates dedicated bandwidth for public network access based on the public network bandwidth you set; second, it associates an existing Elastic Public IP. |2024\-10\-15 |All |* [Configure instance public network access](https://docs.byteplus.com/docs/cloudsearch/enabling-public-access)<br><br>* [Configure Kibana/Dashboards public network access](https://docs.byteplus.com/docs/cloudsearch/enabling-public-access-tool)<br><br>* [Configure Cerebro public network access](https://docs.byteplus.com/docs/cloudsearch/public-access-Cerebro) |
|System default bucket |No longer automatically creates buckets by enabling Cold data nodes; instead, the system automatically creates a TOS Bucket for storing snapshots and snapshots can be searched when creating the first snapshot or transferring snapshots from TOS.<br><br>The system default Bucket charges based on actual usage. |2024\-10\-15 |All |* [System default bucket fee](https://docs.byteplus.com/en/docs/cloudsearch/billing-items#MmfqjsCX)<br><br>* [snapshot overview](https://docs.byteplus.com/docs/cloudsearch/Backup-overview) |
|Snapshot management |On the snapshot management page, you can create, recover, and transfer snapshots for all instances under the current account and region. |2024\-10\-15 |All |* [Automatic snapshot creation](https://docs.byteplus.com/docs/cloudsearch/creating_snapshots_automatically)<br><br>* [Manual snapshot creation](https://docs.byteplus.com/docs/cloudsearch/creating_a_snapshot_manually)<br><br>* [Save snapshot to TOS](https://docs.byteplus.com/docs/cloudsearch/Save_snapshot_to_TOS)<br><br>* [Recover data using snapshot](https://docs.byteplus.com/docs/cloudsearch/recovering_data_using_a_snapshot) |

## September 2024

|**Feature** |**Feature description** |Release date |**Release regions** |**Related documentation** |
|---|---|---|---|---|
|FlexPL bandwidth package |When the instance's data node uses the FlexPL storage type and the storage specifications are set to 500GiB or above, you can purchase bandwidth packages to increase disk bandwidth. |2024\-09\-15 |All |* [Create an instance](https://docs.byteplus.com/docs/cloudsearch/creating-an-instance-2)<br><br>* [Upgrade an instance](https://docs.byteplus.com/docs/cloudsearch/upgrading) |
|Automatically assign public network access |Enable public network access for instances and visualization tools. The system automatically allocates dedicated bandwidth for public network access based on your configured bandwidth. |2024\-09\-15 |All |* [Create an instance](https://docs.byteplus.com/docs/cloudsearch/creating-an-instance-2)<br><br>* [Configure instance public network access](https://docs.byteplus.com/docs/cloudsearch/enabling-public-access)<br><br>* [Configure Kibana/Dashboards public network access](https://docs.byteplus.com/docs/cloudsearch/enabling-public-access-tool)<br><br>* [Configure Cerebro public network access](https://docs.byteplus.com/docs/cloudsearch/public-access-Cerebro) |
|Instance upgrade optimization |During upgrade, only the following two cases will cause the instance to restart. Other upgrade operations only change the instance:<br><br><br>* Upgrade instance node specification.<br><br>* Increase the number of nodes for single\-node instance. |2024\-09\-15 |All |[Upgrade an instance](https://docs.byteplus.com/docs/cloudsearch/upgrading) |
|System built\-in plugin optimization |* System built\-in plugin list optimized to show not installed plugins first for easier searching.<br><br>* Not installed system plugin, supports installation, upgrade, and uninstall operations. |2024\-09\-15 |All |* [View system built-in plugins](https://docs.byteplus.com/docs/cloudsearch/built-in-plugins)<br><br>* [manage system built-in plugins](https://docs.byteplus.com/docs/cloudsearch/manage-built-in-plugins) |

## August 2024

|**Feature** |**Feature description** |Release date |**Release regions** |**Related documentation** |
|---|---|---|---|---|
|Plugin version management |Cloud Search supports version management of user\-defined plugins, mainly reflected in the following points:<br><br><br>* Each plugin supports uploading 5 different versions of plugin files<br><br>* Supports selecting extension version for installation, upgrade, or uninstallation. |2024\-08\-15 |All |* [Upload custom plugin file](https://docs.byteplus.com/docs/cloudsearch/custom-plugins)<br><br>* [Manage custom plugins](https://docs.byteplus.com/docs/cloudsearch/install-user-defined-plugins)<br><br>* [Uninstall custom plugins](https://docs.byteplus.com/docs/cloudsearch/uninstall-user-defined-plugins) |
|Automatically create TOS bucket |Enabling cold data nodes in the Cloud Search service instance automatically creates a TOS bucket to store searchable snapshots.<br><br>Storage space is billed based on actual usage. |2024\-08\-15 |All |* [Create an instance](https://docs.byteplus.com/docs/cloudsearch/creating-instance)<br><br>* [Upgrade an instance](https://docs.byteplus.com/docs/cloudsearch/upgrading)<br><br>* [Searchable snapshot overview](https://docs.byteplus.com/docs/cloudsearch/Searchable_snapshot_overview) |

## July 2024

|**Feature** |**Feature description** |Release date |**Release regions** |**Related documentation** |
|---|---|---|---|---|
|Intelligent operation |The intelligent operation function provides health checks for instances, nodes, indexes, and other dimensions.<br><br>Instance health diagnosis automatically generates diagnostic results that reflect potential risks and help track the latest instance status. |2024\-07\-15 |All |* [Diagnose instance health status](https://docs.byteplus.com/docs/cloudsearch/perform-diagnostics)<br><br>* [View diagnosis report](https://docs.byteplus.com/docs/cloudsearch/view-diagnosis-reports) |
|OpenSearch instance supports index dimension monitoring metrics |OpenSearch version 2.9.0 instances support viewing monitoring data at the index dimension. |2024\-07\-15 |All |[View monitoring data](https://docs.byteplus.com/docs/cloudsearch/viewing-monitoring) |
|Snapshots can be searched |Cloud Search supports snapshots that can be searched, based on snapshots to build searchable snapshot indexes. After generating a searchable snapshot index, you can delete the original index while the searchable snapshot index still provides retrieval capabilities. |2024\-07\-15 |All |* [Manually create searchable snapshots](https://docs.byteplus.com/docs/cloudsearch/Manually_create_searchable_snapshots)<br><br>* [Create searchable snapshots through ISM](https://docs.byteplus.com/docs/cloudsearch/Create_searchable_snapshots_through_ISM) |

## June 2024

|**Feature** |**Feature description** |Release date |**Release regions** |**Related documentation** |
|---|---|---|---|---|
|Analytical service node exposure |Analytical services support configuring resources separately for compute nodes, query nodes, and write nodes. |2024\-06\-15 |All |Create analysis services |
|Customizes prediction entry weights |When configuring category prediction terms, support custom relevance weights for terms.<br><br>When documents meet the configured prediction terms, their matching scores will adjust based on the weights, such as increasing, decreasing, or remaining unchanged. |2024\-06\-15 |All |[Add category prediction term](https://docs.byteplus.com/docs/cloudsearch/configure-category-prediction-terms) |
|Tag filter |The instances list adds a Tag column and supports filtering target instances by tag key and tag value. |2024\-06\-15 |All |[Set instance tags](https://docs.byteplus.com/docs/cloudsearch/configure-instance-tag) |
|View Kibana logs |When querying logs, you can view logs from Data, Master, and Kibana nodes. |2024\-06\-15 |All |[Query logs](https://docs.byteplus.com/docs/cloudsearch/querying-logs) |
|Monitoring metrics |Adjusts instance monitoring metric categories and adds several monitoring metrics. |2024\-06\-15 |All |[View monitoring data](https://docs.byteplus.com/docs/cloudsearch/viewing-monitoring) |
|Instance directory layout restructuring |The instance details page has been redesigned from multiple tabs into a directory style for a cleaner layout and easier use. |2024\-06\-15 |All |Several |

## May 2024

|**Feature** |**Feature description** |Release date |**Release regions** |**Related documentation** |
|---|---|---|---|---|
|Add monitoring item |* AI nodes and SQL analysis nodes connect to Cloud Monitor, adding several monitoring items.<br><br>* Increases HTTP connections, network packet counts, and several other monitoring items, with added metric descriptions. |2024\-05\-15 |All |[View monitoring data](https://docs.byteplus.com/docs/cloudsearch/viewing-monitoring) |
|Export instances |Provides instance export function on the Instances page. When exporting, you can customize the instance's list fields and the list scope. |2024\-05\-15 |All |[Export instances](https://docs.byteplus.com/docs/cloudsearch/export-instance-data) |
|Modify network configuration |Allow modifying the virtual private cloud and subnet used by the instance in scenarios such as network adjustment or insufficient IP quantity. |2024\-05\-15 |All |[Modify instance network configuration](https://docs.byteplus.com/docs/cloudsearch/modify-network-configuration) |
|Note added for data node volume shrinkage |Add a notification when scaling down data nodes.<br><br>Users should ensure CPU usage is below 80%, memory usage below 70%, and disk usage below 75% after scaling down; otherwise, scaling down is not recommended. |2024\-05\-15 |All |[Shrink data node](https://docs.byteplus.com/docs/cloudsearch/reducing-data-nodes) |
|Project permission control |The console navigation bar adds project switching to control IAM user project permissions. |2024\-05\-15 |All |Several |
|V1 instance interface reminder |When creating a V1 instance, add a reminder to recommend creating a V2 instance to guide enabling the more comprehensive V2 instance. |2024\-05\-15 |All |[Create an instance](https://docs.byteplus.com/en/docs/cloudsearch/creating-instance) |

## April 2024

|**Feature** |**Feature description** |Release date |**Release regions** |**Related documentation** |
|---|---|---|---|---|
|Supports storage type upgrade |When upgrading an instance, if the data node uses **ESSD\-PL0** storage type and requires higher storage performance, it can be upgraded to **FlexPL** storage type. |2024\-04\-15 |All |[Upgrade an instance](https://docs.byteplus.com/docs/cloudsearch/upgrading) |
|Customize Kibana/Dashboard parameters |You can modify Kibana/Dashboards parameters according to business needs, such as session persistence, validity duration, and interface request timeout. |2024\-04\-15 |All |[Modify Kibana/Dashboards parameters](https://docs.byteplus.com/docs/cloudsearch/Modifying-Kibana-parameters) |
|Cold data node |The cold data node can be configured to use object storage as the storage medium. Its primary use is to store and process infrequently accessed cold data, such as logs and historical records that are seldom queried.<br><br>The cold data node can store searchable snapshots. |2024\-04\-15 |All |[Create an instance](https://docs.byteplus.com/docs/cloudsearch/creating-an-instance-2) |
|SQL analysis acceleration |The SQL analysis node supports enabling analysis acceleration, which improves query speed after activation. |2024\-04\-15 |All |* Create analysis services<br><br>* Enable analysis acceleration |
|Add availability zone |Supports adding the number of availability zones to an instance. To improve instance high availability, you can add availability zones. This mainly applies to `single AZ to dual AZ`, `single AZ to triple AZ`, and `dual AZ to triple AZ` scenarios. |2024\-04\-15 |All |[Add availability zone](https://docs.byteplus.com/docs/cloudsearch/add-availability-zone) |
|Search management |Provides search management functions for unified maintenance of IK participle, synonyms, and category prediction. |2024\-04\-15 |All |See respective function documentation |
|Visual configuration of IK tokenization |Provides two ways to configure IK participle: visualization configuration and file upload. |2024\-04\-15 |All |Visual configuration of IK tokenization |
|Synonym/participle test |Offers participle and synonym testing functions. After configuring the participle and synonyms, you can run tests directly to see the results. |2024\-04\-15 |All |* [Participle test](https://docs.byteplus.com/docs/cloudsearch/test-synonym-term)<br><br>* Synonym test |
|Refresh data |Any changes to synonyms or analyzer thesaurus, including adding, editing, or deleting entries, apply only to newly created indexes.<br><br>For existing indexes, changes apply only to newly added data. To apply changes to existing data within these indexes, refresh the index data using the data refresh function. |2024\-04\-15 |All |* [Execute data refresh](https://docs.byteplus.com/docs/cloudsearch/refresh-data)<br><br>* [Stop data refresh](https://docs.byteplus.com/docs/cloudsearch/cancel-data-refresh) |
|Category prediction intervention |Support adding category forecast terms to improve search accuracy through manual intervention |2024\-04\-15 |All |* [Install category prediction plugin](https://docs.byteplus.com/docs/cloudsearch/install-category-prediction-plugin)<br><br>* [Add category prediction term](https://docs.byteplus.com/docs/cloudsearch/configure-category-prediction-terms)<br><br>* Category prediction |

## March 2024

|**Feature** |**Feature description** |Release date |**Release regions** |**Related documentation** |
|---|---|---|---|---|
|Single\-node instance expansion |Single\-node instance supports upgrading<br><br>The single\-node instance used for testing is recommended to be upgraded to 3 nodes or more for production use. |2024\-03\-15 |All |[Upgrade an instance](https://docs.byteplus.com/docs/cloudsearch/upgrading) |
|Increase in number of nodes |The number of data nodes can be set from 1 to 100; if more data nodes are needed, you can request an increase to 200. |2024\-03\-15 |All |[Create an instance](https://docs.byteplus.com/docs/cloudsearch/creating-an-instance-2) |
|offline 1 core 2 GiB specification instance |Offline 1 core 2 GiB low\-spec instances, as small instances are prone to CPU overload or OOM issues |2024\-03\-15 |All |[Product specifications](https://docs.byteplus.com/docs/cloudsearch/specifications) |
|Data processing tasks |Cloud Search supports integration with Flink streaming computing, allowing you to create data processing tasks on the Cloud Search side.<br><br>Data processing tasks are mainly used for log processing and analysis scenarios to help enterprises quickly identify and resolve issues, improving operational efficiency. |2024\-03\-15 |All |* Create a data processing task<br><br>* Manage data processing tasks<br><br>* View data processing results |

**2023**

## December 2023

|**Feature** |**Feature description** |Release date |**Release regions** |**Related documentation** |
|---|---|---|---|---|
|Supports adding dedicated masternode |If no dedicated master node is purchased when creating the instance, you can later add a dedicated master node to the instance by changing the configuration according to business needs. |2023\-12\-15 |All |[Add dedicated master node](https://docs.byteplus.com/docs/cloudsearch/adding-master-nodes) |
|Kibana and Dashboards have separate default HTTPS addresses |The visualization platform Kibana or Dashboards has an independent HTTPS address by default, unaffected by the instance’s transport protocol. |2023\-12\-15 |All |None. |

## November 2023

|**Feature** |**Feature description** |Release date |**Release regions** |**Related documentation** |
|---|---|---|---|---|
|Supports open\-source OpenSearch |Supports OpenSearch instances of version 2.9.0 and above. |2023\-11\-15 |All |[Create an instance](https://docs.byteplus.com/docs/cloudsearch/creating-an-instance-2) |
|Multi\-specification Kibana nodes |The system provides one free Kibana node with 1 core and 2 GiB, but when creating or modifying an instance, you can adjust the Kibana node specification. Billing will be based on the new Kibana node specification. |2023\-11\-15 |All |* [Create an instance](https://docs.byteplus.com/docs/cloudsearch/creating-an-instance-2)<br><br>* [Upgrade an instance](https://docs.byteplus.com/docs/cloudsearch/upgrading)<br><br>* [Downgrade instance](https://docs.byteplus.com/docs/cloudsearch/downgrading) |
|Support security audit |Cloud Search provides two types of audit logs: control panel audit log and data plane audit log.<br><br><br>* Control panel audit log is enabled by default, recording instance changes and queries under the current account to the operation audit service.<br><br>* Data plane audit log requires manual activation, recording data access events such as reading and writing indexes, modifying Mappings and Settings, and viewing cluster health to the instance itself. |2023\-11\-15 |All |* [Control panel audit log](https://docs.byteplus.com/docs/cloudsearch/control-plane-auditing)<br><br>* [Enable data plane audit log](https://docs.byteplus.com/docs/cloudsearch/enabe-data-plane-audit)<br><br>* [Query data plane audit log](https://docs.byteplus.com/docs/cloudsearch/query-data-plane-audit-logs) |
|Add API interface |Add APIs for single\-step instance creation, single\-step instance modification, allowlist configuration, and changing pay\-as\-you\-go to subscription billing. |2023\-11\-15 |All |* [CreateInstanceInOneStep](https://docs.byteplus.com/docs/cloudsearch/CreateInstanceInOneStep)<br><br>* [ModifyNodeSpecInOneStep](https://docs.byteplus.com/docs/cloudsearch/ModifyNodeSpecInOneStep)<br><br>* [ModifyChargeCode](https://docs.byteplus.com/docs/cloudsearch/ModifyChargeCode) |

## October 2023

|**Feature** |**Feature description** |Release date |**Release regions** |**Related documentation** |
|---|---|---|---|---|
|Switch transport protocol |Supports switching the instance’s transport protocol according to business needs by enabling or disabling HTTPS to toggle the protocol. |2023\-10\-15 |All |[Switch instance transport protocol](https://docs.byteplus.com/docs/cloudsearch/changing-transfer-protocol) |
|Adds Tag to instance |Supports adding key\-value style tags to instances for easier identification and management. |2023\-10\-15 |All |[Create an instance](https://docs.byteplus.com/docs/cloudsearch/creating-an-instance-2) |
|Increase node count |The maximum number of nodes is currently 100, and the number of instance nodes can be adjusted according to business needs. |2023\-10\-15 |All |* [Create an instance](https://docs.byteplus.com/docs/cloudsearch/creating-an-instance-2)<br><br>* [Upgrade an instance](https://docs.byteplus.com/docs/cloudsearch/upgrading)<br><br>* [Downgrade instance](https://docs.byteplus.com/docs/cloudsearch/downgrading) |

## September 2023

|**Feature** |**Feature description** |Release date |**Release regions** |**Related documentation** |
|---|---|---|---|---|
|Add instance specifications |Add multiple instance specifications to support more business scenarios. |2023\-09\-15 |All |[V2 instance specification](https://docs.byteplus.com/docs/cloudsearch/specifications#2b828379) |
|Data backup |* Optimizes the automatic backup strategy to support automatically creating snapshots at specified times.<br><br>* Supports manual backup by creating snapshots of the instance's full data or selected indexes for backup. |2023\-09\-15 |All |* [Snapshot overview](https://docs.byteplus.com/docs/cloudsearch/Backup-overview)<br><br>* [Automatic snapshot creation](https://docs.byteplus.com/docs/cloudsearch/automatic-snapshots)<br><br>* [manual snapshot creation](https://docs.byteplus.com/docs/cloudsearch/manual-snapshots)<br><br>* [Recover data using snapshot](https://docs.byteplus.com/docs/cloudsearch/snapshots-restore-data) |

## August 2023

|**Feature** |**Feature description** |Release date |**Release regions** |**Related documentation** |
|---|---|---|---|---|
|Supports public network resolution |Supports enabling public network resolution for the instance or Kibana's private network address to meet special scenarios such as development and testing in non\-production environments. After enabling public network resolution, users can access the instance via the private network address through dedicated lines. |2023\-08\-15 |All |* [Configure instance private network address public network resolution](https://docs.byteplus.com/docs/cloudsearch/enabling-DNS)<br><br>* [Configure Kibana/Dashboards private network address public network resolution](https://docs.byteplus.com/docs/cloudsearch/enabling-DNS-tool) |

## July 2023

|**Feature** |**Feature description** |Release date |**Release regions** |**Related documentation** |
|---|---|---|---|---|
|Supports deploying instances in dual availability zones |Provides a cross\-availability zone disaster recovery deployment mode, generally used for production task scenarios. |2023\-07\-15 |All |[Create an instance](https://docs.byteplus.com/docs/cloudsearch/creating-an-instance-2) |
|Supports installing system built\-in plugins |Some system built\-in plugins are not installed. If you need to use plugin features, you can install plugins manually. |2023\-07\-15 |All |[Install system built-in plugins](https://docs.byteplus.com/docs/cloudsearch/manage-built-in-plugins#146cb8a0) |
|Supports installing user\-defined plugins |Supports uploading and installing user\-defined plugins on Cloud Search instances.<br><br>> **tip**<br><br><br>> User\-defined plugins may affect instance stability. Ensure the plugin's availability and security.<br> |2023\-07\-15 |All |[Upload user-defined plugin file](https://docs.byteplus.com/docs/cloudsearch/custom-plugins) |

## June 2023

|**Feature** |**Feature description** |Release date |**Release regions** |**Related documentation** |
|---|---|---|---|---|
|Instance upgrade |Supports dynamic adjustment of instance configuration, including node specification, storage specifications, and number of nodes. |2023\-06\-15 |All |[Upgrade an instance](https://docs.byteplus.com/docs/cloudsearch/upgrading) |
|Instance downgrade |Supports downgrading instance node specifications. |2023\-06\-15 |All |[Downgrade instance](https://docs.byteplus.com/docs/cloudsearch/downgrading) |
|Remove data nodes |Support data node volume shrinkage to reduce the number of data nodes in the cluster. |2023\-06\-15 |ALL |[Shrink data node](https://docs.byteplus.com/docs/cloudsearch/reducing-data-nodes) |
|Instance IP allowlist |Cloud Search instances support private network access by default, allowing all devices within the same VPC environment to access the instance; if Cloud Search instance enables public network access, all public network devices can also access the instance.<br><br>It is recommended to configure an IP whitelist for the instance to restrict IP addresses that can access the instance. |2023\-06\-15 |All |* [Configure instance private network IP allowlist](https://docs.byteplus.com/docs/cloudsearch/IPallowlist-for-instance)<br><br>* [Configure instance public network IP allowlist](https://docs.byteplus.com/docs/cloudsearch/public-IPallowlist-for-instance) |
|Kibana public network IP allowlist |Kibana nodes support private network access by default, allowing all devices within the same VPC environment to access Kibana; enabling public network access also allows all public network devices to access Kibana.<br><br>We recommend configuring an IP whitelist for Kibana to restrict instance access by IP address. |2023\-06\-15 |All |* [Configure Kibana/Dashboards IP allowlist](https://docs.byteplus.com/docs/cloudsearch/IPallowlist-for-tool)<br><br>* [Configure Kibana/Dashboards Public IP allowlist](https://docs.byteplus.com/docs/cloudsearch/public-IPallowlist-for-tool) |
|Hot and cold update synonym dictionary |The synonym file uploaded for the first time requires cold enable to take effect.<br><br>The synonym file hot enabled does not require restarting the instance and can use the system built\-in plugin (analysis\-dynamic\-synonym) to dynamically load the synonym dictionary. |2023\-06\-15 |All |Offline |
|Hot and cold updated participle dictionary |The first uploaded IK participle file requires cold enable to take effect.<br><br>The IK participle file hot enabled loads the participle thesaurus during runtime without restarting the instance. |2023\-06\-15 |All |* Upload IK tokenizer dictionary files<br><br>* Experiencing IK tokenization capabilities |

## April 2023

|**Feature** |**Feature description** |Release date |**Release regions** |**Related documentation** |
|---|---|---|---|---|
|Support coordinating node |Instances support coordinating nodes, which can be enabled when creating or changing the instance configuration.<br><br>Coordinating nodes only receive and distribute query requests and process statistical query results. They relieve pressure on data nodes to ensure Cloud Search cluster stability. |2023\-04\-15 |All |* [Create an instance](https://docs.byteplus.com/docs/cloudsearch/creating-instance)<br><br>* [Modify the instance configuration](https://docs.byteplus.com/en/docs/cloudsearch/modifying-instance)<br><br>* [Restart instance or node](https://docs.byteplus.com/en/docs/cloudsearch/restarting) |

**2022**

## August 2022

|**Feature** |**Feature description** |Release date |**Release regions** |**Related documentation** |
|---|---|---|---|---|
|Supports instance deletion protection |Cloud Search service instances support deletion protection to prevent accidental instance deletion. |2022\-08\-15 |All |* [Create an instance](https://docs.byteplus.com/docs/cloudsearch/creating-instance)<br><br>* [Configure delete protection for an instance](https://docs.byteplus.com/en/docs/cloudsearch/deletion-protection) |

## June 2022

|**Feature** |**Feature description** |Release date |**Release regions** |**Related documentation** |
|---|---|---|---|---|
|Subscription supported |Cloud Search service instances support subscription billing. |2022\-06\-15 |All |[Subscription](https://docs.byteplus.com/docs/cloudsearch/subscription) |
|Supports pay\-as\-you\-go billing and change to subscription |Supports converting pay\-as\-you\-go Cloud Search instances to subscription billing |2022\-06\-15 |All |[Change from pay-as-you-go to subscription](https://docs.byteplus.com/docs/cloudsearch/changing-billing-method) |
|Support automatic renewal |Add support to turn on or turn off automatic renewal on the **Instance information** page of subscription instances. |2022\-06\-15 |All |[Renew the instance.](https://docs.byteplus.com/docs/cloudsearch/renewal) |
|Supports network upgrade |Supports upgrading the private IP address of existing instances to a private network address within your VPC. |2022\-06\-15 |All |Network security upgrade |
|Supports binding public network address EIP |Supports binding EIP to public address; you can enable or disable public network access based on business needs. |2022\-06\-15 |All |* [Configure instance public network access](https://docs.byteplus.com/en/docs/cloudsearch/enabling-public-access)<br><br>* [Configure Kibana/Dashboards public network access](https://docs.byteplus.com/en/docs/cloudsearch/enabling-public-access-tool) |
|HTTP protocol supports public network access |Supports public network access for Cloud Search service instances and Kibana nodes using the HTTP protocol. |2022\-06\-15 |All |[Create an instance](https://docs.byteplus.com/docs/cloudsearch/creating-instance) |

## May 2022

|**Feature** |**Feature description** |Release date |**Release regions** |**Related documentation** |
|---|---|---|---|---|
|Cloud Search |Cloud Search service launched for the first time. |2022\-05\-15 |All |[What is Cloud Search](https://docs.byteplus.com/en/docs/cloudsearch/what-is-cloudsearch) |
