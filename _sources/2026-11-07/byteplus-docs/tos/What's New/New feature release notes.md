---
title: "New feature release notes"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/New-feature-release-notes"
---

This topic describes the release notes for TOS features. New features will be released in each region.

> **tip**

> Some features of TOS are in the beta stage. If you want to use it, please contact the customer manager.

## September 2026

|Feature |Description |Release date |Supported regions |Related documentation |
|---|---|---|---|---|
|DevMind |Added DevMind, which integrates usage statistics, log analysis, Storage Lens, and Insight Assistant. These modules help you analyze bucket data from multiple angles to evaluate usage, troubleshoot issues, and govern storage. |2026\-09\-15 |All regions |[Overview](https://docs.byteplus.com/en/docs/tos/DevMind-overview) |
|SenseFlow |Added TOS SenseFlow, a multi\-model workspace.<br><br>> **tip**<br><br><br>> SenseFlow is currently in closed beta and is only available in China (Hong Kong). Please contact your account manager for access.<br> |2026\-09\-15 |China (Hong Kong) |[What is SenseFlow](https://docs.byteplus.com/en/docs/tos/What-is-SenseFlow) |
|TOS Agent |Added TOS Agent, an intelligent service that offers natural language interactions.<br><br>> **tip**<br><br><br>> This feature is currently in closed beta. Please contact your account manager for access.<br> |2026\-09\-15 |All regions |[Overview](https://docs.byteplus.com/en/docs/tos/TOS-Overview) |
|ObjectSet |TOS now supports ObjectSet. |2026\-09\-15 |All regions |[Overview](https://docs.byteplus.com/en/docs/tos/-Overview) |

## April 2026

|Feature |Description |Release date |Region |Related Documents |
|---|---|---|---|---|
|Accelerator |The accelerator has added a read/write caching mode.<br><br>> tips<br><br><br>> This feature is currently in closed beta. Please contact your account manager for access.<br> |2026\-04\-24 |Asia Pacific (Johor) |[TOS accelerator](https://docs.byteplus.com/en/docs/tos/TOS_Accelerator_fee)<br><br>[Overview](https://docs.byteplus.com/en/docs/tos/Overview11)<br><br>[Creating TOS accelerators](https://docs.byteplus.com/en/docs/tos/Creating-tos-accelerators) |
|FSX |New FSX compatibility priority mode. |2026\-04\-21 |All |[FSX compatibility priority mode](https://docs.byteplus.com/en/docs/tos/FSX_compatibility_priority_mode?lang=en) |
|QoS policy |A new priority\-based QoS policy has been added, introducing multi\-level priority and minimum quota design to improve overall resource utilization. |2026\-04\-17 |All |[Overview](https://docs.byteplus.com/en/docs/tos/Qos-policy-overview)<br><br>[Creating QoS policies](https://docs.byteplus.com/en/docs/tos/Create-a-qos-policy)<br><br>[Use cases for QoS policies](https://docs.byteplus.com/en/docs/tos/Qos-policy-use-cases) |
|Hierarchical namespace |HNS buckets support back\-to\-origin rules. |2026\-04\-17 |All |[Supported console features (HNS buckets)](https://docs.byteplus.com/en/docs/tos/Console-function-list-hierarchical-buckets)<br><br>[API list (HNS buckets)](https://docs.byteplus.com/en/docs/tos/API-list-hierarchical-bucket) |
|Bucket inventory |The bucket inventory now includes a new typical condition filtering configuration. |2026\-04\-17 |All |[Bucket inventory](https://docs.byteplus.com/en/docs/tos/Bucket-inventory) |
|Image processing |Image processing supports drawing points and lines, and mosaics on images. |2026\-04\-17 |All |[Draw](https://docs.byteplus.com/en/docs/tos/Draw)<br><br>[Mosaic](https://docs.byteplus.com/en/docs/tos/Mosaic) |
|Data subscription |The new data subscription feature allows you to automatically and securely synchronize AIGC outputs from Model Ark to your TOS buckets in near real time. |2026\-04\-17 |Asia Pacific (Johor) |[Overview](https://docs.byteplus.com/en/docs/tos/data_subscription_overview) |
|FSX |A new version 1.3.2.790 has been added, providing POSIX semantic compatibility. |2026\-04\-17 |All |[Overview](https://docs.byteplus.com/en/docs/tos/Overview) |
|Audio processing<br><br> |A new Java SDK for audio transcoding has been added, supporting quick access to audio format conversion capabilities via API. |2026\-04\-03 |All |[Create audio transcoding template (Java SDK)](https://docs.byteplus.com/en/docs/tos/2306568)<br><br>[List audio transcoding templates (Java SDK)](https://docs.byteplus.com/en/docs/tos/2306564)<br><br>[Delete audio transcoding template (Java SDK)](https://docs.byteplus.com/en/docs/tos/2306569)<br><br>[Create audio transcoding task (Java SDK)](https://docs.byteplus.com/en/docs/tos/2306565)<br><br>[Query audio transcoding task (Java SDK)](https://docs.byteplus.com/en/docs/tos/2306563) |
|Video processing<br><br> |A new Java SDK for video transcoding has been added, supporting quick access to video format conversion capabilities via API. |2026\-04\-03 |All |[Create video transcoding template (Java SDK)](https://docs.byteplus.com/en/docs/tos/2306572)<br><br>[List video transcoding templates (Java SDK)](https://docs.byteplus.com/en/docs/tos/2306570)<br><br>[Delete video transcoding template (Java SDK)](https://docs.byteplus.com/en/docs/tos/2306571)<br><br>[Create video transcoding task (Java SDK)](https://docs.byteplus.com/en/docs/tos/2306573)<br><br>[Query video transcoding tasks (Java SDK)](https://docs.byteplus.com/en/docs/tos/2306575) |
|Workflow<br><br> |A new Java SDK for workflows has been added, supporting media processing tasks through code orchestration and management. |2026\-04\-03 |All |[Create workflow (Java SDK)](https://docs.byteplus.com/en/docs/tos/2306567)<br><br>[Query workflow (Java SDK)](https://docs.byteplus.com/en/docs/tos/2306566)<br><br>[Delete workflow (Java SDK)](https://docs.byteplus.com/en/docs/tos/2306574) |

## March 2026

|Feature |Description |Release date |Region |Related Documents |
|---|---|---|---|---|
|tosfsspec |tosfsspec is a Python library that adheres to the pythonic file systems specification ([fsspec](https://github.com/fsspec)). This enables developers to read from and write to TOS as conveniently and efficiently as they would with a local file system. |2026\-03\-23 |All |[Overview](https://docs.byteplus.com/en/docs/tos/tosfsspec_overview) |

## February 2026

|Feature |Description |Release date |Region |Related Documents |
|---|---|---|---|---|
|QoS policy |Fetch parameter description has been newly added to the QoS policy. |2026\-02\-09 |All |[QoS policy overview](https://docs.byteplus.com/en/docs/tos/Qos-policy-overview)<br><br>[Create QoS policy](https://docs.byteplus.com/en/docs/tos/Create-a-qos-policy) |
|Hierarchical namespace |* Supports CORS to enable cross\-region resource sharing.<br><br>* Supports static website hosting and enables access to static websites.<br><br>* Supports the FetchObject interface, enabling the retrieval and storage of resources from a specified URL. |2026\-02\-09 |All |[Console feature list (HNS buckets)](https://docs.byteplus.com/en/docs/tos/Console-function-list-hierarchical-buckets)<br><br>[API list (HNS buckets)](https://docs.byteplus.com/en/docs/tos/API-list-hierarchical-bucket) |
|View video information |The new rotation field has been added to the video information parameter, supporting the setting of the clockwise rotation angle. |2026\-02\-09 |All |[View video information](https://docs.byteplus.com/en/docs/tos/docs-viewing-video-information) |
|File decompression |A new point cloud compression API interface has been added, which supports compressing point cloud data files to save costs.<br><br>> **tip**<br><br><br>> The interface is currently in invitation\-only preview. Please contact your account manager to request access.<br> |2026\-02\-09 |All |[PointCloudCompress](https://docs.byteplus.com/en/docs/tos/PointCloudCompress) |

## January 2026

|Feature |Description |Release date |Region |Related Documents |
|---|---|---|---|---|
|TOS PyTorch Connector  |TOS PyTorch Connector is a high\-performance data read\-write tool provided by TOS for AI training scenarios.  |2026\-01\-30 |All |[TOS PyTorch Connector Overview](https://docs.byteplus.com/en/docs/tos/TOS_PyTorch_Connector_Overview?lang=en) |
|TOS Browser |* Added the function to sort by file name, optimizing the file search experience. <br><br>* Supports displaying the HNS bucket recycle bin. |2026\-01\-26 |All |[Install TOS Browser](https://docs.byteplus.com/en/docs/tos/Install-tos-browser) |
|Accelerator |The accelerator function has been changed from invitation\-only testing to official release. |2026\-01\-06 |China (Beijing),<br><br>China (Guangzhou),<br><br>China (Shanghai), Asia Pacific (Johor) |[Creating TOS accelerators](https://docs.byteplus.com/en/docs/tos/Creating-tos-accelerators) |

## December 2025

|Feature |Description |Release date |Region |Related Documents |
|---|---|---|---|---|
|Lifecycle management |Lifecycle rule creation supports NOT configuration. |2025\-12\-31 |All |* [Configuring lifecycle rules based on last modified time](https://docs.byteplus.com/en/docs/tos/docs-setting-lifecycle-rules)<br><br>* [Configuring lifecycle rules based on last access time](https://docs.byteplus.com/en/docs/tos/Lifecycle-rules-based-on-last-accesstime)<br><br>* [PutBucketLifecycle](https://docs.byteplus.com/en/docs/tos/reference-putbucketlifecycle)<br><br>* [GetBucketLifecycle](https://docs.byteplus.com/en/docs/tos/reference-getbucketlifecycle) |
|Bucket inventory |Bucket inventory support exporting inventory reports at one time and executing inventory rules immediately. |2025\-12\-31 |All |* [Bucket inventory](https://docs.byteplus.com/en/docs/tos/Bucket-inventory)<br><br>* [PutBucketInventory](https://docs.byteplus.com/en/docs/tos/PutBucketInventory)<br><br>* [GetBucketInventory](https://docs.byteplus.com/en/docs/tos/GetBucketInventory)<br><br><br> |
|Audio and video transcoding |* Added an API interface for submitting audio and video transcoding tasks.<br><br>* The audio transcoding output file formats supported are mp3, wav, aac, m4a, flac, ac3, opus, and oga. |2025\-12\-31 |All |* [AudioConvert](https://docs.byteplus.com/en/docs/tos/AudioConvert)<br><br>* [CreateTranscodeJob](https://docs.byteplus.com/en/docs/tos/CreateTranscodeJob) |
|QoS policy |The QoS policy conditions support access points and projects. |2025\-12\-31 |All |[Qos policy overview](https://docs.byteplus.com/en/docs/tos/Qos-policy-overview) |
|Log management |New parameters such as StorageTier, MRAPAlias, and Payer have been added to help you analyze and track requests from multiple regional access points and requests where the requester pays. |2025\-12\-18 |All |[Log analysis](https://docs.byteplus.com/en/docs/tos/Log-analysis)<br><br> |
|FSX |The newly added version 1.3.0.370 supports Rocky Linux operating systems 9.1 to 9.5. |2025\-12\-04 |All |[Overview](https://docs.byteplus.com/en/docs/tos/Overview) |
|tosutil |Added the `-bfs` parameter to cp (download objects) and cp (copy objects) commands. This parameter allows you to use the hierarchical listing method to download or copy objects in parallel and set the concurrency level for those listings. |2025\-12\-03 |All |* [Download objects (cp)](https://docs.byteplus.com/docs/tos/Download-object-cp)<br><br>* [Copy objects (cp)](https://docs.byteplus.com/docs/tos/Copy-object-cp) |
|Hierarchical namespace |* Supports single\-region access points, providing dedicated access domains for storage buckets.<br><br>* Supports TOS accelerator. |2025\-12\-03 |All |[Console feature list (HNS buckets)](https://docs.byteplus.com/docs/tos/Console-function-list-hierarchical-buckets) |
|Data processing fee |Added introductions of the video transcoding fees, audio transcoding fees, and audio/video AIGC metadata extraction fees. |2025\-12\-03 |All |[Data Processing Fee](https://docs.byteplus.com/docs/tos/docs-data-processing-fee) |
|Data retrieval |The newly added data retrieval function provides you with full\-scenario, multi\-modal data retrieval capabilities for your data stored in TOS. |2025\-12\-03 |All |[Data retrieval](https://docs.byteplus.com/docs/tos/Create_dataset) |
|Workflow |The workflow function has graduated from invitation\-only preview to general availability. |2025\-12\-03 |All |* [CreateWorkflow](https://docs.byteplus.com/docs/tos/CreateWorkflow)<br><br>* [GetWorkflow](https://docs.byteplus.com/docs/tos/GetWorkflow)<br><br>* [DeleteWorkflow](https://docs.byteplus.com/docs/tos/DeleteWorkflow)<br><br>* [GetWorkflowExecution](https://docs.byteplus.com/docs/tos/GetWorkflowExecution)<br><br>* [ListWorkflowExecution](https://docs.byteplus.com/docs/tos/ListWorkflowExecution) |
|Image processing |Added images set as grayscale and images intelligent compression processing API interfaces. |2025\-12\-03 |All |* [GrayScale](https://docs.byteplus.com/docs/tos/GrayScale)<br><br>* [ImageSlim](https://docs.byteplus.com/docs/tos/ImageSlim) |
|Media processing |Added audio and video file remuxing, querying the status of audio and video asynchronous tasks, extracting audio and video AIGC metadata, and concatenating audio segments API interfaces. |2025\-12\-03 |All |* [CreateRemuxJob](https://docs.byteplus.com/docs/tos/CreateRemuxJob)<br><br>* [QueryMediaJob](https://docs.byteplus.com/docs/tos/QueryMediaJob)<br><br>* [GetAIGCMetadata](https://docs.byteplus.com/docs/tos/GetAIGCMetadata)<br><br>* [AudioConcat](https://docs.byteplus.com/docs/tos/AudioConcat) |

## November 2025

|Feature |Description |Release date |Region |Related Documents |
|---|---|---|---|---|
|FSX Client |A new mount parameter, tos_symlink_mode, has been introduced to configure the symbolic link mode. |2025\-11\-24 |All |[Mount parameters](https://docs.byteplus.com/docs/tos/FSX-mount-parameter-description) |
|Mirroring rules |Supports configuring the origin server for mirroring rule with both a primary site and a standby site. |2025\-11\-14 |All |[Configuring mirroring rules](https://docs.byteplus.com/docs/tos/docs-setting-back-to-origin-rules) |
|FSX client |* Supports installing and using the FSX client on operating systems with ARM64 architecture.<br><br>* Improved compatibility in symbolic link scenarios. |2025\-11\-05 |All |[Operating environment](https://docs.byteplus.com/docs/tos/Overview#e82382a8) |

## October 2025

|Feature |Description |Release date |Region |Related Documents |
|---|---|---|---|---|
|Bucket inventory |Supports exporting the access tier of Intelligent Tiering objects via the bucket inventory feature. |2025\-10\-20 |All |[Bucket inventory](https://docs.byteplus.com/docs/tos/Bucket-inventory) |
|Intelligent Tiering |Supports viewing the billed capacity and original capacity of the frequent access tier of Intelligent Tiering, infrequent access tier of Intelligent Tiering, and flashback archive tier of Intelligent Tiering on the Overview and Usage Statistics pages. |2025\-10\-20 |All |[Usage Statistics](https://docs.byteplus.com/docs/tos/docs-usage-statistics) |

## September 2025

|Feature |Description |Release date |Region |Related Documents |
|---|---|---|---|---|
|Retention policy |Supports configuring retention policies to ensure that objects cannot be deleted or overwritten by anyone within a specified period, enabling write\-once\-read\-many (WORM) data storage behavior. |2025\-09\-26 |All |* [Configure Retention Policy (WORM)](https://docs.byteplus.com/docs/tos/Configure-retention-policy)<br><br>* [PutBucketObjectLockConfiguration](https://docs.byteplus.com/docs/tos/Putbucketobjectlockconfiguration)<br><br>* [GetBucketObjectLockConfiguration](https://docs.byteplus.com/docs/tos/Getbucketobjectlockconfiguration)<br><br>* [PutObjectRetention](https://docs.byteplus.com/docs/tos/Putobjectretention)<br><br>* [GetObjectRetention](https://docs.byteplus.com/docs/tos/Getobjectretention) |
|tosutil |Added the \-f parameter to specify whether to skip the confirmation prompt when overwriting local files. |2025\-09\-26 |All |[Download object (cp)](https://docs.byteplus.com/docs/tos/Download-object-cp) |
|FSX |Supports mounting buckets or specific directories via FSX without authentication. |2025\-09\-24 |All |[FSX Configuration and Mounting](https://docs.byteplus.com/docs/tos/FSX-configuration-and-mounting) |
|tosutil |Supports configuring HTTP proxies, allowing access to the TOS (Tianyi Object Storage) service through a proxy. |2025\-09\-23 |All |[Configure HTTP Proxy](https://docs.byteplus.com/docs/tos/Configure-http-proxy) |
||Supports generating presigned URLs using the presign command. |2025\-09\-23 |All |[Generate Pre-Signed URL (presign)](https://docs.byteplus.com/docs/tos/Generate-pre-signed-url-presign) |
|Multi\-AZ redundancy |Supports multi\-AZ redundancy. After enabling this feature, TOS will store your data across multiple availability zones within the same region, ensuring that other availability zones can continue to provide you with stable storage service in case of a failure in any single zone. |2025\-09\-24 |Asia Pacific (Johor) |[Multi-AZ redundancy](https://docs.byteplus.com/docs/tos/Multi-az-redundancy) |
|Event notifications |Supports delivering event changes to the Kafka message queue, enabling you to monitor resource changes within TOS. |2025\-09\-09 |All |* [Delivering event notifications to Message Queue for Kafka](https://docs.byteplus.com/docs/tos/Delivering-event-notification-to-message-queue-for-kafka)<br><br>* [PutBucketNotificationV2](https://docs.byteplus.com/docs/tos/PutBucketNotificationV2)<br><br>* [GetBucketNotificationV2](https://docs.byteplus.com/docs/tos/GetBucketNotificationV2) |
||Hierarchical namespace now supports event notifications. |2025\-09\-09 |All |[Console feature list (HNS buckets)](https://docs.byteplus.com/docs/tos/Console-function-list-hierarchical-buckets) |
||New event types added to event notifications include: tos:ObjectCreated:Modify, tos:ObjectCreated:Append, tos:ObjectRename, tos:ObjectRemoved:TrashMoved, and tos:LifecycleExpiration:TrashMoved. |2025\-09\-09 |All |[Event notification overview](https://docs.byteplus.com/docs/tos/Event-notification-overview) |
|Image processing experience center |Supports using features such as image cropping and watermarking directly in the TOS console, providing visual management of image processing configurations through a graphical interface. |2025\-09\-09 |All |[Image Processing Experience Center](https://docs.byteplus.com/docs/tos/Image-processing-experience-center) |
|Presigned URLs |Supports generating presigned URLs using custom domains bound to a bucket. |2025\-09\-09 |All |[Viewing file details](https://docs.byteplus.com/en/docs/tos/docs-viewing-file-details) |
|Object expiration time |Supports adding or modifying an object's expiration time via the SetObjectExpires API. |2025\-09\-09 |All |* [SetObjectExpires](https://docs.byteplus.com/docs/tos/SetObjectExpires)<br><br>* [Set expiration times](https://docs.byteplus.com/docs/tos/Set-expiration-times)<br><br>* [Set object-level expiration time（Java SDK）](https://docs.byteplus.com/docs/tos/Set-object-level-expiration-time-java-sdk)<br><br>* [Set object-level expiration time（Go SDK）](https://docs.byteplus.com/docs/tos/Set-object-level-expiration-time-go-sdk)<br><br>* [Set object-level expiration time（Python SDK）](https://docs.byteplus.com/docs/tos/Set-object-level-expiration-time-python-sdk) |
|TOS Browser |* Supports setting an expiration timestamp when sharing files or folders; the sharing link will automatically expire upon reaching the specified time.<br><br>* Supports viewing the total size of files pending download in the task progress management panel. |2025\-09\-03 |All |[Basic file operations](https://docs.byteplus.com/docs/tos/Basic-file-operations) |

## August 2025

|Feature |Description |Release date |Region |Related documents |
|---|---|---|---|---|
|Hierarchical namespace |Introducing the new bucket with hierarchical namespace enabled, also known as an HNS bucket. HNS buckets combine the capabilities of a hierarchical namespace with the scalability of a flat object structure, enabling seamless interoperability between object and file semantics. This allows truly unified data access through multiple protocols, enhancing data utilization efficiency. |2025\-08\-07 |Asia Pacific (Johor) |* [What is hierarchical namespace](https://docs.byteplus.com/docs/tos/What-is-hierarchical-namespace)<br><br>* [Console feature list (HNS buckets)](https://docs.byteplus.com/docs/tos/Console-function-list-hierarchical-buckets)<br><br>* [API list (HNS buckets)](https://docs.byteplus.com/docs/tos/API-list-hierarchical-bucket)<br><br>* [SDK overview (HNS buckets)](https://docs.byteplus.com/docs/tos/Sdk-overview-hierarchical-bucket)<br><br>* [Tool overview (HNS buckets)](https://docs.byteplus.com/docs/tos/Tool-overview-hierarchical-bucket) |
|TLS version |Supports setting the allowed range of TLS versions, enabling you to use specific versions of the TLS protocol for secure communication. |2025\-08\-07 |All |* [Set TLS version](https://docs.byteplus.com/docs/tos/Set_TLS_version)<br><br>* [PutBucketHttpsConfig](https://docs.byteplus.com/docs/tos/Putbuckethttpsconfig)<br><br>* [GetBucketHttpsConfig](https://docs.byteplus.com/docs/tos/Getbuckethttpsconfig) |
|Preview files |Supports previewing image, audio, and video files directly in the TOS console. |2025\-08\-07 |All |[Preview files](https://docs.byteplus.com/docs/tos/Preview-files) |
|Upload files |Added the `if-match` and `if-none-match` parameters to perform ETag\-based conditional checks when uploading files. |2025\-08\-07 |All |* [CopyObject](https://docs.byteplus.com/docs/tos/reference-copyobject)<br><br>* [PutObject](https://docs.byteplus.com/docs/tos/reference-putobject)<br><br>* [CompleteMultipartUpload](https://docs.byteplus.com/docs/tos/reference-completemultipartupload) |

## July 2025

|Feature |Description |Release date |Region |Related documents |
|---|---|---|---|---|
|FSX |The FSX client has transitioned from the invitation\-only beta testing phase to full production release. |2025\-07\-21 |All |[FSX overview](https://docs.byteplus.com/docs/tos/Overview) |
|Server\-Side encryption |SSE\-TOS and SSE\-KMS encryption methods are supported in the Asia Pacific(Johor) ,Asia Pacific (Jakarta),China (Beijing),China (Shanghai) and China (Hong Kong) regions. |2025\-07\-11 |Asia Pacific(Johor) ,Asia Pacific (Jakarta),China (Beijing),China (Shanghai),China (Hong Kong) |* [Server-Side Encryption Overview](https://docs.byteplus.com/docs/tos/Server-side-encryption-overview)<br><br>* [Set Server-side Encryption for the Bucket](https://docs.byteplus.com/docs/tos/Set-server-side-encryption-for-the-bucket) |
|Request pay |The Requester Pay feature is supported, allowing you to transfer the cost of data access to the requester. When this feature is enabled, the user initiating the data request is responsible for the associated data transfer and request fees, while the bucket owner is charged only for storage and other applicable fees. |2025\-07\-11 |All |* [Enable Requester Pay](https://docs.byteplus.com/docs/tos/Using-requester-pays)<br><br>* [PutBucketRequestPayment](https://docs.byteplus.com/docs/tos/PutBucketRequestPayment)<br><br>* [GetBucketRequestPayment](https://docs.byteplus.com/docs/tos/GetBucketRequestPayment) |

## June 2025

|Feature |Description |Release date |Region |Related documents |
|---|---|---|---|---|
|Storage type |The storage types have been expanded to include Cold Archive and Deep Cold Archive. |2025\-06\-23 |All |[Storage Type](https://docs.byteplus.com/docs/tos/docs-storage-type) |
|Mirroring rule |The mirror\-based back\-to\-origin supports configuring and adding prefixes/suffixes, as well as replacing the filename prefix. |2025\-06\-03 |All |[Creating a Mirroring Back-to-Origin Rule](https://docs.byteplus.com/docs/tos/docs-setting-back-to-origin-rules) |

## May 2025

|Feature |Description |Release date |Region |Related documents |
|---|---|---|---|---|
|Storage type |Cold Archive and Deep Cold Archive storage types are newly added to TOS.<br><br>> **tip**<br><br><br><br>* > Cold Archive Storage is supported only in China (Beijing), China (Shanghai), and China (Guangzhou).<br><br><br>* > Deep Cold Archive Storage is only supported in China (Beijing), China (Shanghai), and China (Guangzhou), and all are in the invitation\-only testing phase. If you need to use this storage type, please contact your account manager.<br> |2025\-05\-22 |China (Beijing), China (Shanghai), China (Guangzhou) |[Storage Type](https://docs.byteplus.com/docs/tos/docs-storage-type) |
|QoS policy |The QoS policy feature has transitioned from invitation\-only testing to official release. |2025\-05\-12 |All |* [QoS Policy Overview](https://docs.byteplus.com/docs/tos/Qos-policy-overview)<br><br>* [Creating a QoS Policy](https://docs.byteplus.com/docs/tos/Create-a-qos-policy)<br><br>* [QoS Policy Use Cases](https://docs.byteplus.com/docs/tos/Qos-policy-use-cases) |
|Log management |It supports retrieving and analyzing relevant logs in the TOS console and setting the log retention time. Additionally, some data reports are pre\-configured to facilitate your viewing of information related to storage buckets and files. |2025\-05\-06 |All |* [Log Analysis](https://docs.byteplus.com/docs/tos/Log-analysis)<br><br>* [Log Report](https://docs.byteplus.com/docs/tos/Log-report) |

## April 2025

|Feature |Description |Release date |Region |Related documents |
|---|---|---|---|---|
|QoS policy |The parameters of `NotResource` and `NotPrincipal` are newly added, which are used to specify the resources and accounts that are not subject to the constraints of the QoS policy. |2025\-04\-02 |All |* [QoS Policy Overview](https://docs.byteplus.com/docs/tos/Qos-policy-overview)<br><br>* [Creating a QoS Policy](https://docs.byteplus.com/docs/tos/Create-a-qos-policy)<br><br>* [QoS Policy Use Cases](https://docs.byteplus.com/docs/tos/Qos-policy-use-cases) |
|Bucket policy |The `NotAction` parameter supports being used in conjunction with `"Effect": "Allow"`, indicating that all operations other than those specified by NotAction are permitted. |2025\-04\-02 |All |* [Templates and Parameters](https://docs.byteplus.com/docs/tos/docs-templates-and-parameters)<br><br>* [Customizing a Bucket Policy in the JSON View](https://docs.byteplus.com/docs/tos/docs-customizing-a-bucket-policy-in-the-json-view)<br><br>* [Typical Authorization Scenarios for NotPrincipal, NotResource, and NotAction](https://docs.byteplus.com/docs/tos/Typical-authorization-scenarios-for-notprincipal-notresource-and-notaction) |
|Data processing |The pipeline symbol (\|) is used to connect multiple data processing tasks. There's no need to manually transfer intermediate results. TOS will execute the data processing tasks in the order defined by the pipeline. |2025\-04\-02 |All |[Pipeline](https://docs.byteplus.com/docs/tos/Pipeline) |
||It supports using image styles to uniformly process multiple types of images, achieving the goal of simplifying operations.<br><br>> **tip**<br><br><br>> The image style function is in the invitation\-based testing state. If you need to use it, please contact your account manager.<br> |2025\-04\-02 |All |* [Creating an Image Style](https://docs.byteplus.com/docs/tos/docs-creating-an-image-style)<br><br>* [Using an Image Style](https://docs.byteplus.com/docs/tos/docs-using-an-image-style) |
||It supports the use of the original image protection function to prevent the original images from being stolen by anonymous users.<br><br>> **tip**<br><br><br>> The original image protection function is in the invitation\-based testing state. If you need to use it, please contact your account manager.<br> |2025\-04\-02 |All |[Original Image Protection](https://docs.byteplus.com/docs/tos/docs-original-image-protection) |
||It supports accessing private m3u8 files, effectively protecting the content security of m3u8 files while meeting your needs for accessing m3u8 files. |2025\-04\-02 |All |* [Accessing Private m3u8 Files](https://docs.byteplus.com/docs/tos/Accessing-private-m3u8-files)<br><br>* [Pm3u8](https://docs.byteplus.com/docs/tos/Pm3u8) |
||The Q parameter for quality transformation is effective for original images in jpeg \- 2000, avif, and heic formats. |2025\-04\-02 |All |[Quality Change](https://docs.byteplus.com/docs/tos/docs-quality-change) |
||It supports performing format conversion operations on original images in heic format. |2025\-04\-02 |All |[Format Conversion](https://docs.byteplus.com/docs/tos/docs-format-conversion) |
||It supports performing video processing operations on videos with the webm video encapsulation format and VP8 or VP9 video encoding formats. |2025\-04\-02 |All |[Media Processing Overview](https://docs.byteplus.com/docs/tos/docs-overview_7) |
|Monitoring and alerting |It supports monitoring the data status of TOS resources and creating alarm policies. When the data of the monitored cloud product resources reaches the triggering conditions of the alarm, the system will push alarm notifications in the manner specified by you. |2025\-04\-02 |All |[Monitoring Overview](https://docs.byteplus.com/docs/tos/Monitoring-overview) |
|Custom domain name |It supports setting the access protocol for the custom domain name. |2025\-04\-02 |All |* [Seting a Custom Domain Name](https://docs.byteplus.com/docs/tos/Set-up-a-custom-domain-name)<br><br>* [PutBucketCustomDomain](https://docs.byteplus.com/docs/tos/Putbucketcustomdomain)<br><br>* [GetBucketCustomDomain](https://docs.byteplus.com/docs/tos/Getbucketcustomdomain) |
|Rename |It supports the RenameObject function. You can enable the RenameObject function and use the RenameObject interface to rename objects. |2025\-04\-02 |All |* [Use RenameObject](https://docs.byteplus.com/docs/tos/Use-renameobject)<br><br>* [RenameObject](https://docs.byteplus.com/docs/tos/Renameobject)<br><br>* [PutBucketRename](https://docs.byteplus.com/docs/tos/Putbucketrename)<br><br>* [GetBucketRename](https://docs.byteplus.com/docs/tos/Getbucketrename)<br><br>* [DeleteBucketRename](https://docs.byteplus.com/docs/tos/Deletebucketrename) |
|Batch processing |It supports batch execution of operations such as data replication for objects, replacement of object ACLs, restoration of objects, and processing of object tags. |2025\-04\-02 |All |[Batch Processing](https://docs.byteplus.com/docs/tos/Batch-processing1) |
|Symbolic link |It supports the creation of symbolic link objects. You can quickly access frequently used target objects through symbolic link objects. |2025\-04\-02 |All |[Create Symbolic Link](https://docs.byteplus.com/docs/tos/Create-Symbolic-link) |
|Statistics folder |It supports counting the number of objects and the total size of objects in a folder. |2025\-04\-30 |All |[Statistics a Folder](https://docs.byteplus.com/docs/tos/Statistics-folder) |
|Query bucket |It supports querying bucket configuration through the GetBucketInfo interface. |2025\-04\-30 |All |[GetBucketInfo](https://docs.byteplus.com/docs/tos/Getbucketinfo) |
|Share files |It supports sharing files and folders. |2025\-04\-30 |All |[Sharing Files](https://docs.byteplus.com/docs/tos/Sharing-files) |
|Bucket policy |It supports setting conditions such as volc:ViaConsole, volc:RequestTagKeys for bucket policy. |2025\-04\-30 |All |[Templates and Parameters](https://docs.byteplus.com/docs/tos/docs-templates-and-parameters) |

## March 2025

|Feature |Description |Release date |Region |Related documents |
|---|---|---|---|---|
|Server\-side encryption |TOS supports server\-side encryption of files during the file upload process. |2025\-03\-07 |All |* [Server-Side Encryption Overview](https://docs.byteplus.com/docs/tos/Server-side-encryption-overview)<br><br>* [Set Server-side Encryption for the Bucket](https://docs.byteplus.com/docs/tos/Set-server-side-encryption-for-the-bucket) |

## January 2025

|Feature |Description |Release date |Region |Related documents |
|---|---|---|---|---|
|Lifecycle rules |Add the functionality of setting lifecycle rules based on the last access time of objects. After setting is completed, if an object remains unaccessed for a predetermined number of days, TOS will automatically convert the storage type of that object according to the rules you have set. |2025\-01\-07 |All |* [Configure lifecycle rules based on last access time](https://docs.byteplus.com/docs/tos/Lifecycle-rules-based-on-last-accesstime)<br><br>* [Which Operations will Update the LastAccessTime of an Object?](https://docs.byteplus.com/docs/tos/Which-operations-update-the-lastaccesstime)<br><br>* [PutBucketLifecycle](https://docs.byteplus.com/docs/tos/reference-putbucketlifecycle)<br><br>* [GetBucketLifecycle](https://docs.byteplus.com/docs/tos/reference-getbucketlifecycle)<br><br>* [PutBucketAccessMonitor](https://docs.byteplus.com/docs/tos/PutBucketAccessMonitor)<br><br>* [GetBucketAccessMonitor](https://docs.byteplus.com/docs/tos/GetBucketAccessMonitor) |
|File list |Support sorting files by file name, file size, and file modification time. |2025\-01\-07 |All |[Sorting Files](https://docs.byteplus.com/docs/tos/Sorting-files) |
|FSX |Add FSX client, through which you can mount TOS buckets to Linux systems, allowing the buckets to function as a local file system for the Linux system. |2025\-01\-13 |All |[Overview](https://docs.byteplus.com/docs/tos/Overview) |
|C SDK |Add C SDK. |2025\-01\-13 |All |[C SDK Introduction](https://docs.byteplus.com/docs/tos/C-sdk-introduction1) |
|Harmony SDK |Add Harmony SDK. |2025\-01\-13 |All |[Harmony SDK Introduction](https://docs.byteplus.com/docs/tos/Overview-of-harmony-sdk) |

## December 2024

|Feature |Description |Release date |Region |Related documents |
|---|---|---|---|---|
|Bucket inventory |Support setting bucket inventory rules to regularly export specified object information. |2024\-12\-11 |All |* [Bucket Inventory](https://docs.byteplus.com/docs/tos/Bucket-inventory)<br><br>* [PutBucketInventory](https://docs.byteplus.com/docs/tos/PutBucketInventory)<br><br>* [GetBucketInventory](https://docs.byteplus.com/docs/tos/GetBucketInventory)<br><br>* [ListBucketInventory](https://docs.byteplus.com/docs/tos/ListBucketInventory)<br><br>* [DeleteBucketInventory](https://docs.byteplus.com/docs/tos/DeleteBucketInventory) |

## November 2024

|Feature |Description |Release date |Region |Related documents |
|---|---|---|---|---|
|Bucket tag |Support setting tags for buckets with similar characteristics to facilitate labeling and categorization. |2024\-11\-18 |All |[Tagging buckets](https://docs.byteplus.com/en/docs/tos/Set-bucket-tag) |
|QoS policy |Introducing the QoS policy feature, you can manage the flow control capability of multiple business access resource groups through QoS policies, ensuring that various businesses do not interfere with each other when accessing the same storage resources, and operate efficiently.<br><br>> **tip**<br><br><br>> The QoSPolicy feature is currently in the invitation testing phase. If you need to use this feature, please contact your account manager.<br> |2024\-11\-18 |All |* [QoS Policy Overview](https://docs.byteplus.com/docs/tos/Qos-policy-overview)<br><br>* [Creating a QoS Policy](https://docs.byteplus.com/docs/tos/Create-a-qos-policy)<br><br>* [QoS Policy Use Cases](https://docs.byteplus.com/docs/tos/Qos-policy-use-cases) |
|Cross region replication |Support automatically copying files from one bucket to another bucket in a different region. |2024\-11\-18 |All |* [Cross Region Replication Overview](https://docs.byteplus.com/docs/tos/Cross-region-replication-overview)<br><br>* [Cross Region Replication within the Same Account](https://docs.byteplus.com/docs/tos/Cross-regional-replication-within-the-same-account)<br><br>* [Cross Region Replication across Account](https://docs.byteplus.com/docs/tos/Cross-region-replication-across-account) |
|Upload callback |TOS supports upload callbacks, carrying callback parameters in the request. After the upload is completed, the server sends a synchronous POST callback request to the third\-party application server specified in CallBack. |2024\-11\-18 |All |[Upload Callback](https://docs.byteplus.com/docs/tos/Upload-callback) |
|Static website |Support uploading the content of a static website to a storage bucket and configuring static website rules. |2024\-11\-18 |All |[Seting a Static Website](https://docs.byteplus.com/docs/tos/Set-up-a-static-website) |
|Custom domain name |Support for binding custom domain names to buckets, allowing access to files within the bucket using the custom domain name. |2024\-11\-18 |All |* [Seting a Custom Domain Name](https://docs.byteplus.com/docs/tos/Set-up-a-custom-domain-name)<br><br>* [Managing HTTPS Certificates](https://docs.byteplus.com/docs/tos/Manage-https-certificates) |
|Capture object |Support fetching resources from a specified URL and storing the resource in a specified bucket. |2024\-11\-18 |All |* [FetchObject](https://docs.byteplus.com/docs/tos/Fetchobject)<br><br>* [PutFetchTask](https://docs.byteplus.com/docs/tos/Putfetchtask)<br><br>* [GetFetchTask](https://docs.byteplus.com/docs/tos/Getfetchtask) |
|Object expiration date |Support setting the expiration time of an object through the API, and the object will be automatically deleted after expiration. |2024\-11\-18 |All |* [SetObjectMeta](https://docs.byteplus.com/docs/tos/reference-setobjectmeta)<br><br>* [GetObject](https://docs.byteplus.com/docs/tos/reference--getobject)<br><br>* [HeadObject](https://docs.byteplus.com/docs/tos/reference-headobject)<br><br>* [PutObject](https://docs.byteplus.com/docs/tos/reference-putobject)<br><br>* [CreateMultipartUpload](https://docs.byteplus.com/docs/tos/reference-createmultipartupload)<br><br>* [PostObject](https://docs.byteplus.com/docs/tos/reference-postobject)<br><br>* [AppendObject](https://docs.byteplus.com/docs/tos/reference-appendobject)<br><br>* [CopyObject](https://docs.byteplus.com/docs/tos/reference-copyobject) |
|Bucket ACL |* Add default inheritance bucket ACL feature. When this feature is enabled, the ACL policy of newly uploaded objects will default to be consistent with the bucket ACL policy.<br><br>* Add default inheritance bucket ACL function, after enabling this function, the ACL policy of newly uploaded objects will default to be consistent with the bucket ACL policy. |2024\-11\-18 |All |* [Overview](https://docs.byteplus.com/docs/tos/docs-overview_4)<br><br>* [Configuring an Object ACL](https://docs.byteplus.com/docs/tos/docs-configuring-an-object-acl)<br><br>* [Creating a Bucket](https://docs.byteplus.com/docs/tos/docs-create-a-bucket)<br><br>* [Uploading a File](https://docs.byteplus.com/docs/tos/docs-uploading-a-file)<br><br>* [PutObjectACL](https://docs.byteplus.com/docs/tos/reference-putobjectacl)<br><br>* [GetObjectACL](https://docs.byteplus.com/docs/tos/reference-getobjectacl)<br><br>* [PutBucketACL](https://docs.byteplus.com/docs/tos/reference-putbucketacl)<br><br>* [GetBucketACL](https://docs.byteplus.com/docs/tos/reference-getbucketacl) |
||Support for selecting three types of bucket access permissions, specifically including read permission, write permission, and object listing/multipart listing permission. |2024\-11\-18 |All |* [Overview](https://docs.byteplus.com/docs/tos/docs-overview_4)<br><br>* [Configuring a Bucket ACL](https://docs.byteplus.com/docs/tos/docs-configuring-a-bucket-acl)<br><br>* [PutBucketACL](https://docs.byteplus.com/docs/tos/reference-putbucketacl)<br><br>* [GetBucketACL](https://docs.byteplus.com/docs/tos/reference-getbucketacl) |
|Back\-to\-origin rule |Support triggering mirror\-based and redirect\-based back\-to\-origin through HeadObject requests. |2024\-11\-18 |All |* [Creating a Mirroring Back-to-Origin Rule](https://docs.byteplus.com/docs/tos/docs-setting-back-to-origin-rules)<br><br>* [Creating a Redirection Back-to-Origin Rule](https://docs.byteplus.com/docs/tos/Create-a-redirection-back-to-origin-rule) |
|IAM policy |When granting account or role permissions using IAM, the effective time has been changed from 10 minutes to 1 minute. |2024\-11\-18 |All |[Configuring an IAM Policy](https://docs.byteplus.com/docs/tos/docs-configuring-an-iam-policy) |

##  October 2024

|Feature |Description |Release date |Region |Related documents |
|---|---|---|---|---|
|Tool |Add tosutil, TOS Browser, and TOS Import tools. |2024\-10\-25 |All |* [Tosutil overview](https://docs.byteplus.com/en/docs/tos/overview)<br><br>* [TOS Browser overview](https://docs.byteplus.com/en/docs/tos/Overview3)<br><br>* [TOS Import overview](https://docs.byteplus.com/en/docs/tos/Overview4) |

## August 2024

|Feature |Description |Release date |Region |Related documents |
|---|---|---|---|---|
|Bucket policy |Improve user experience by providing instructions for filling in keys and values with additional conditions. |2024\-08\-08 |All |[Templates and Parameters](https://docs.byteplus.com/docs/tos/docs-templates-and-parameters) |
|SDK |Add Java SDK, Go SDK, C++ SDK, Python SDK, Node.js SDK. |2024\-08\-08 |All |* [Java SDK Introduction](https://docs.byteplus.com/docs/tos/Java_sdk_introduction)<br><br>* [Go SDK Introduction](https://docs.byteplus.com/docs/tos/Go-sdk-introduction)<br><br>* [C++ SDK Introduction](https://docs.byteplus.com/docs/tos/C-sdk-introduction)<br><br>* [Python SDK Introduction](https://docs.byteplus.com/docs/tos/Python-sdk-introduction)<br><br>* [Node.js SDK Introduction](https://docs.byteplus.com/docs/tos/Node-js-sdk-introduction) |
