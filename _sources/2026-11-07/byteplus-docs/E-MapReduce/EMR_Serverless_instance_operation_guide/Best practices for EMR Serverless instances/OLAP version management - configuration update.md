---
title: "OLAP version management/configuration update"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/olap_version_management_or_configuration_update"
---

<span id="4dc6ba1a"></span>
## Version management

The core objective of EMR Serverless OLAP version management is **to fully leverage the optimization, performance improvements, and enhanced stability offered by new versions through well\-planned version upgrades and configuration updates, while ensuring business stability**. Practical implementation should focus on four key dimensions: version selection, upgrade strategy, rollback assurance, and configuration standards, taking into account the characteristics of the StarRocks/Doris engines and specific business scenarios.

<span id="b9c2aa78"></span>
## Version selection

Version selection must balance the need for new features and business compatibility. The core principle is to use the latest minor version for minor upgrades, and to validate major versions before adoption. The specific selection logic is as follows:

<span id="3428fdef"></span>
### Version type adaptation scenarios

The positioning differences between various version types are clear. Selection should be based on core business requirements:


|Version types |Core features |Use cases |Selection recommendations |
|---|---|---|---|
|**Minor version** (such as StarRocks 3.2.12, Doris 2.1.8) |Based on the same major version, mainly focused on **bug fixes**, compatible with basic features (SQL syntax, interfaces, data formats) |1. Production environments need to fix known bugs (such as query exceptions, performance bottlenecks)<br><br>2. Need to continue using the current major version architecture to avoid compatibility risks<br><br>3. Stability is prioritized; no major new feature requirements |**Highly recommended**: Upgrade the production environment to the **latest minor version** of the current major version as a priority to promptly fix vulnerabilities and performance issues |
|**Major version** (such as StarRocks 3.3, Doris 3.0) |Includes **core features and architectural evolution** (such as new storage engines, optimized query plans), and may involve compatibility changes |1. Business requires exclusive features of the new version (for example, vector engine optimization in StarRocks 3.3)<br><br>2. Long\-term need for architecture upgrades, and can accept the cost of compatibility verification<br><br>3. Validate first in test / pre\-release environments, and plan to gradually migrate to the production environment |**Choose cautiously**: Consider only when business clearly requires new features, and must first complete full compatibility verification in the **test cluster** |


<span id="afc92409"></span>
### Important notes


* Do not use newly released major versions from the community directly in production environments: new major versions may have undisclosed stability issues. Wait for 1–2 minor version iterations before evaluation.

* Avoid skipping multiple major versions during upgrades (for example, StarRocks 3.1 → 3.3). It is recommended to upgrade step by step, such as "3.1 → latest minor version of 3.2 → 3.3", to reduce cross\-version compatibility risks.


<span id="324f698c"></span>
## Version upgrade Note

<span id="81985865"></span>
### Version compatibility

**Minor version upgrade** (It is recommended to upgrade to the latest minor version within the current major version)


* Scope: All minor versions within the same major version remain compatible, as community minor versions generally evolve through bugfixes.

* Compatibility coverage: Includes SQL syntax, client interfaces (JDBC/ODBC), table structures, and data formats.

* Non\-guaranteed compatibility: Program business logic behaviors (such as changes in specific query performance).

* Avoid performing version upgrades during business peak periods, as some tasks may fail and require retries.


**Major version upgrade** (Requires thorough validation in a test cluster and confirmation of business compatibility before proceeding with the upgrade)


* Note: Full compatibility between major versions is not guaranteed. The following changes may occur:

   * SQL syntax adjustments or deprecation.

   * Interface changes or parameter adjustments.

   * Changes to default values of configuration items.

   * Query execution plan optimization causes performance fluctuations and other issues.

* Upgrade recommendations:

   * Before upgrading, be sure to carefully read the release notes for the corresponding open\-source engine version to understand potential impacts.

   * Conduct thorough business compatibility verification on the test cluster.

   * Avoid performing version upgrades during business peak periods, as some tasks may fail and require retries.


<span id="e6757977"></span>
#### Whether rollback is possible

EMR Serverless OLAP supports one\-click rollback for engine upgrades, but this is only available in the following scenarios:


|Engine type |Version type |Rollback support status |Key points for rollback operations |
|---|---|---|---|
|**StarRocks** |Minor version |Supports one\-click rollback |Stop all write tasks before rollback (such as Stream Load, Broker Load) to avoid data conflicts |
||Major version |Supports one\-click rollback, but must follow the community version roadmap |* Strictly follow the community Release Notes (for example, rollback from 3.3 must go to 3.2.3+; cannot rollback to 3.2.0\-3.2.2 to prevent metadata loss)<br><br>* After rollback, re\-verify metadata integrity (for example, run `SHOW TABLES` to confirm table structure is normal) |
|**Doris** |Minor version |* Integrated storage and compute supports one\-click rollback;<br><br>* Storage and compute separation does not support one\-click rollback |* Integrated storage and compute: Initiate rollback directly through the EMR console, restart the instance after rollback<br><br>* Storage and compute separation: No one\-click rollback; data must be backed up in advance. During rollback, redeploy the target version and restore the data. |
||Major version |Neither supports one\-click rollback |— |


<span id="cd843a52"></span>
## Configuration updates

<span id="4926a27a"></span>
### Update method

It is recommended to update all engine parameters only through the **Instance Parameters \- Parameter Configuration** entry provided by the EMR console, ensuring parameter configuration is traceable and persistent. Directly modifying engine parameters via SQL commands is prohibited, as this will result in configurations not being persistently effective. After instance restart, parameters will not take effect, impacting business. EMR is not responsible for issues caused by such parameter changes.

<span id="b542f269"></span>
### Update recommendations

Exercise caution when changing instance parameters. It is recommended to follow the process below to modify instance parameters:


1. Refer to the official documentation to confirm the parameter's effective scope, Unit, valid values, and more. Improper parameter modifications may cause processes to fail to start normally after a restart, resulting in business loss.

2. For parameter modifications not clearly specified in step 1, after modification, it is recommended to perform restart verification at the single FE/BE node level. Once the corresponding service starts normally, proceed with the remaining nodes.

3. Use the **Instance Parameters \- Parameter Configuration** entry provided by the EMR console to ensure parameter configuration updates are traceable, rollback\-capable, and persistent.
