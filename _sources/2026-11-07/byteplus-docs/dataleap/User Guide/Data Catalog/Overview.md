---
title: "Overview"
product: "DataLeap"
product_code: "dataleap"
source: "https://docs.byteplus.com/en/docs/dataleap/data-catalog-overview"
---

<span id="_1-整体概述"></span>
## Overall Overview

The Data Catalog uses a graphical full\-link data sheet management tool that provides field and partition\-level metadata lineage display. It also retrieves comprehensive data production linkage information through data lineage, helping you solve difficulties in finding and understanding data.

The Data Catalog is now connected to various types of metadata such as LAS, EMR Hive, and ByteHouse. You can find these metadata, view and understand their details, or query their lineage. In addition, the Data Catalog also offers distinctive features such as Data Album, Lineage Graph, Metadata Ingestion, and Table management.

<span id="_2-名词解释"></span>
## Definitions


* **Metadata**

   Also known as intermediary data or relay data, metadata is data about data primarily describing data attributes. It supports functions such as indicating storage locations, historical data, resource finding, and file records.

* **Product line**

   There are also discussions about business lines; a product line is a way to divide businesses and organize personnel. For data consumers, it serves as a method of data classification and access. Different themes can be divided under a product line. For example, new retail businesses usually consist of transaction, marketing, and behavior domains.

* **Business domain**

   It's another method of data division relative to product lines. Product lines are classified vertically, whereas business domains span across product lines and are classified horizontally.

* **Theme**

   It is a subset of the theme domain and is also referred to as the data domain; here, it is collectively referred to as the theme domain. Multiple themes can form a theme domain, which can also be further decomposed and refined into different themes.

   * Theme is an abstract concept that involves synthesizing, classifying, and analyzing data in enterprise information systems at a higher level, with each theme generally corresponding to a macro analysis area.

   * The theme domain is the boundary of a theme determined after analyzing a deeper theme or parts of themes. To ensure the vitality of the entire system, theme domains need to be abstractly refined and maintained and updated over the long term, but they should not change easily.

   * When dividing theme domains, it is necessary to ensure that the domain can cover all current business requirements and can include new business seamlessly into the existing domains, as well as expanding new themes.

      For example, "Sales Analysis" is an analysis area involving products, suppliers, customers, and warehouses; hence the data warehouse themes are set as product theme, supplier theme, customer theme, and warehouse theme, while "Sales Analysis" can serve as a theme domain.

* **DDL**

   Data Definition Language (DDL), commonly used for creating, modifying, and deleting objects.
