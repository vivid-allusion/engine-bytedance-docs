---
title: "Applicable scenarios"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/applicable-scenarios"
---

Database Workshop DBW offers a one\-stop database management solution covering the entire lifecycle, including daily queries, security control, process\-based changes, intelligent operations, and AI assistance. It helps enterprises achieve unified cross\-environment access, proactive risk management, and efficient collaboration, significantly enhancing R&D efficiency and data security compliance. This article describes the applicable scenarios for DBW.

<span id="tOu22oBl"></span>
## Scenario 1: Daily SQL queries and data validation


* **Business pain points**: R&D, data analysis, or operations personnel often face issues such as scattered query entry points and complex account and password management when troubleshooting, verifying data, or performing regression testing. Manually recording query processes makes them difficult to reproduce, and switching between different tools incurs high costs.

* **Solution**: Provides a unified data interaction platform that integrates deeply with instance access and permission systems. Supports visual table structure management, data preview, and SQL execution to lower the barrier for queries. With password\-free login (requires enabling security control) and a unified entry point, it establishes a standardized daily data interaction method, significantly improving troubleshooting efficiency.


<span id="q7NsU8TP"></span>
## Scenario 2: Minimum privilege control and traceable collaboration for production access


* **Business pain point**: Query and O&M operations in the production environment must balance efficiency and compliance. In the traditional model, permission granting relies on manual workflows. This poses a high risk of unauthorized access and misoperations, making it difficult to accurately reconstruct operation records after the fact.

* **Solution**: Provide a comprehensive security control system. Supports multi\-level permission management for administrators, regular users, and user groups, implementing the principles of least privilege and on\-demand authorization. By combining operation auditing with execution logging capabilities, it ensures that all production operations are fully traceable, effectively reducing security and compliance risks.


<span id="tvrNKVAD"></span>
## Scenario 3: Process\-driven Control of Database Changes


* **Business pain point**: Business iterations are accompanied by frequent DDL/DML changes and data fixes. Executing changes via direct database connection lacks process control. This makes operations uncontrollable and difficult to review, and is highly likely to introduce stability risks during tight change windows.

* **Solution**: Provide a ticketing system that covers both regular changes and lock\-free schema changes (OnlineDDL). Supports integration with customizable approval workflows (e.g., multi\-level approval by DBAs and Owners), upgrading "black\-box changes" to "process\-driven delivery." Supports pre\-check, scheduled execution, and manual execution to enhance change controllability and collaboration efficiency.


<span id="jXqGjp8p"></span>
## Scenario 4: Pre\-release SQL audit and specification enforcement


* **Business pain point**: SQL quality heavily relies on individual experience, lacking a unified checkpoint. Unreasonable SQL statements often surface only after deployment, leading to slow queries or full table scans, with extremely high remediation costs.

* **Solution**: Provides SQL audit tickets and intelligent review capabilities. Before submitting a change, the system automatically performs syntax checks, performance evaluations, and specification validations to help identify high\-risk statements. Moves risk identification forward, completing quality checks before deployment to ensure online database stability.


<span id="uGtXk5sN"></span>
## Scenario 5: Performance troubleshooting and stability management


* **Business pain point**: When online requests slow down, lock waits occur, or connection counts surge, troubleshooting information is scattered across various logs and monitoring tools. The troubleshooting path is long, lacking a unified view, making it easy to fall into a cycle of trial and error.

* **Solution**: Provides one\-stop O&M observability and diagnostic capabilities. Includes modules such as slow log analysis, full SQL insights, transaction and lock analysis, session management, and one\-click diagnostics. Establishes a systematic troubleshooting portal and an evidence chain to help DBAs quickly pinpoint the root cause and reduce the Mean Time To Recovery (MTTR).


<span id="M6GU3E5k"></span>
## Scenario 6: Continuous O&M for Capacity and Performance


* **Business pain point**: With business growth, resource scaling, index governance, and periodic maintenance become increasingly labor\-intensive. Highly reliant on manual inspections and empirical judgment, delayed responses can easily lead to performance degradation or resource waste.

* **Solution**: Provides rich automated O&M and autonomous capabilities. Supports automatic scaling for instance specifications and storage (including automatic expansion for local disks), automatic index creation, database health checks, and scheduled task management. Shifts O&M from "reactive firefighting" to "continuous governance," reducing manual effort and enhancing the predictability of performance and capacity management.


<span id="L78gzNe3"></span>
## Scenario 7: Security Compliance Auditing and Risk Identification


* **Business pain points**: Enterprises need to meet internal audit and compliance check requirements, continuously monitoring high\-risk operations. Lack of a unified audit portal makes it difficult to quickly locate abnormal operations and responsibility boundaries, leading to delayed risk discovery.

* **Solution**: Provide database audit and log management capabilities. Supports creating traceable records for key operations, with over 100 built\-in security rules to accurately identify high\-risk behaviors. Combines security rule sets with the permission system to enhance security governance and compliance capabilities, supporting rapid audits and incident reviews.


<span id="m80z29K0"></span>
## Scenario Eight: Controlled Data Import/Export and Delivery


* **Business pain points**: Data backfilling, repairs, or result exports lack process control and boundary constraints, easily leading to security risks such as data leaks, sensitive information outflow, or untraceable operations.

* **Solution**: Provide data import/export and task management capabilities. Supports full database export, SQL result set export, and CSV/SQL format import. All operations require ticket approval and are linked with permissions and audit capabilities, ensuring the data flow process is controllable, traceable, and auditable, balancing delivery efficiency with security and compliance.


<span id="7brF9PrR"></span>
## Scenario 9: Unified Access and Management for Multiple Databases and Environments


* **Business Pain Points**: Enterprises use multiple database types and environments (development/testing/production) simultaneously. Disparate tools lead to high learning costs, inconsistent account systems and access methods, and complex maintenance.

* **Solution**: Centralized management of multiple instance types (including cloud instances and self\-built external instances) is supported. A unified workspace entry and consistent permission management method are provided to eliminate tool fragmentation. Regardless of where instances are deployed, unified security control and operation audit can be performed through Database Workshop DBW.


<span id="Rcv0AFbh"></span>
## Scenario 10: AI\-Assisted Development and Intelligent Troubleshooting


* **Business Pain Points**: Slow onboarding for new hires, difficulty in accumulating experience, and frequent recurrence of repetitive issues. SQL writing and complex troubleshooting heavily rely on individual skills, leading to poor consistency in team collaboration.

* **Solution**: The DB AI assistant (DBCopilot) and Knowledge base capabilities are provided. Supports natural language to SQL conversion, intelligent index recommendations, slow SQL diagnosis and suggestions, and self\-service querying. Converts expert experience into reusable knowledge assets, enhances self\-service and standardization levels, reduces learning costs, and comprehensively improves overall team efficiency.
