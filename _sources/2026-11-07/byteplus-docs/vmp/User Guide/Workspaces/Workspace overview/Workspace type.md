---
title: "Workspace type"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/workspaces-types"
---

The workspace of Vital Managed Service for Prometheus (VMP) is an abstract integration of data and collection rules, which provides users with standard cloud Prometheus capabilities. You can create different workspaces in VMP, where data in different workspaces is isolated from each other.

VMP offers different types of workspaces, which are shown in the following table.


|Comparison item |Common workspace |Local workspace |Aggregation query workspace |
|---|---|---|---|
|Glossary |A cloud standard workspace provided by VMP, which offers you standard Prometheus capabilities managed on the cloud. |Supports associating self\-built Prometheus clusters or the Prometheus clusters of other cloud providers in the VMP console, achieving centralized metric queries. |Aggregates the monitoring data of multiple workspaces to facilitate you in viewing data in a centralized manner. |
|Access address |Provides Remote Write and Query URLs, allowing writing and reading workspace data. |None |Provides a Query URL, allowing only reading workspace data. |
|Explore |Supports |Does not support |Supports |
|Monitoring dashboard |Supports |Does not support |Supports |
|Application scenarios |Provides standard Prometheus capabilities, and offers data writing and query addresses, which allows writing and querying monitoring data. |Supports associating self\-built Prometheus clusters, the Prometheus clusters of other cloud providers, or VMP workspaces within other BytePlus accounts and other regions over public or private networks. |Supports the aggregation of multiple workspaces, including general and local workspaces. Provides a query address, enabling centralized data query from multiple workspaces. |


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Local workspaces do not provide an access address and cannot directly query metrics through Explore or monitoring dashboards. If you need to query the metrics of a local workspace, you can add it to an Aggregation query workspace before querying.</div>


&nbsp;
