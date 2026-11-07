---
title: "Overview"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/DevMind-Storage-Lens-Overview"
---

Storage Lens is an analytics feature that provides insight into TOS resource usage and activity. You can use it to generate summary insights, such as total storage usage, the total number of objects, and bytes of historical object versions or incomplete multipart uploads. This topic provides an overview of the features supported by Storage Lens and explains what you should know when using them.

<span id="9RQooQN5"></span>
## Features

Storage Lens offers dashboards that visualize insights and trends in your storage data. With these dashboards, you can monitor storage capacity growth trends and find out the fastest\-growing buckets and prefixes. This allows you to see if storage growth meets your expectations and helps you identify cost\-optimization opportunities. The supported features are as follows:


* Data statistics: Provides daily data statistics that can be broken down by dimensions such as region, storage type, bucket, and prefix. Key metrics include total storage, object count, current version bytes, current version object count, historical version bytes, and number of historical version objects.

* Data export: Supports the daily export of data from the dashboard to a specified bucket, enabling you to perform statistical analyses on the exported data using your own tools.


<span id="UgCrHx5G"></span>
## Notes


* You can create up to 50 dashboards per account.

* The first time you create a dashboard, it may take up to 48 hours before you can view the corresponding data metrics. Subsequent data updates occur daily and display statistics from the previous day.

* By default, the owner of an account has full permissions. Identity and Access Management (IAM) users have no permissions by default. If an IAM user needs to perform any of the following operations, the account owner must grant the user the appropriate permissions using an [IAM](https://docs.byteplus.com/en/docs/tos/docs-overview_6) or [bucket policy](https://docs.byteplus.com/en/docs/tos/docs-overview_5).

   
   |Category |Operation |Permissions |
   |---|---|---|
   |Log application |Create log applications |`tls:CreateApp` |
   ||View log applications |`tls:DescribeApp`、`tls:DescribeApps` |
   |Storage Lens |Configure Storage Lens dashboards |`tls:CreateTosLensTask` |
   ||View Storage Lens dashboard details |`tls:DescribeTosLensTasks`、`tls:DescribeTosLensTask` |
   ||Delete Storage Lens dashboards |`tls:DeleteTosLensTask` |
   ||Modify Storage Lens dashboards |`tls:ModifyTosLensTask` |
   |Log analysis |View log analysis instances |`tls:DescribeCloudLensInstances` |
   ||View log analysis instance status |`tls:DescribeCloudLensInstanceStatus` |
   ||Modify log analysis instance status |`tls:ModifyCloudLensInstanceStatus` |
   ||View associated TLS topics |`tls:DescribeCloudLensTargetTopics` |
   ||View log analysis overview |`tls:DescribeCloudLensOverview` |
   


<span id="TUr413ez"></span>
## Metric categories

Storage Lens offers two types of metrics: free and advanced. The details are as follows:


* **Free metrics**: Include total storage, total number of objects, historical version bytes, number of historical version objects, number of unmerged multipart uploads bytes, number of unmerged multipart uploads objects, current version bytes, and number of current version objects. You can generate and visualize insights at the region, storage type, or bucket level.

* **Advanced features**: Provide activity metrics and data aggregation by prefix. The details are as follows:

   * Activity metrics: Offer granular visibility into your cloud resources. The supported metrics are bytes uploaded and number of deleted bytes.

   * Prefix aggregation: Displays data by prefix. Supported metrics include total storage, total number of objects, current version bytes, number of current version objects, historical version bytes, number of historical version objects, number of unmerged multipart uploads bytes, and number of unmerged multipart uploads objects.
