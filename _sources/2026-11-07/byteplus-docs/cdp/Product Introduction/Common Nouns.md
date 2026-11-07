---
title: "Common Nouns"
product: "BytePlus CDP"
product_code: "cdp"
source: "https://docs.byteplus.com/en/docs/cdp/Common_Nouns"
---

In the usage of the Customer Data Platform product, various specialized terms are involved to help users better understand and use the product. Here are explanations of the relevant product terms:

<span id="_1-产品定位相关概念"></span>
# 1. Concepts related to product positioning

Differences between CDP products and other marketing tools:


|Concept |Explanatory notes |
|---|---|
|Customer Data Platform (CDP) |Data source: Aggregate enterprise omni\-channel data, including first\-party, second\-party, and third\-party data, breaking the data silos between systems, establishing a unified system for people, goods, relationships, labels, and portrait systems.<br><br>Output<br><br>Application scenario: Mainly used for the back\-end marketing and operation of enterprises |
|DMP (Data Management Platform) |The data source: DMP's data mainly comes from the media's own data and third\-party agencies' data, with its main touchpoints being those provided by the media, covering a large amount of monitoring and broadcasting data from the advertising delivery end and advertising interaction behavior data.<br><br>Application scenario: DMP is positioned to serve advertisements. |
|CRM (Customer Relationship Management System) |The data source: mainly stores relatively static customer data, with data touchpoints mainly from conversion and after\-sales touchpoints, focusing on customers and potential customers, collecting data on their interactions with the business during the purchase of goods and services.<br><br>Application Scenarios: Business data management related to transactions |
|SCRM (Social Customer Relationship Management) |Data Source: SCRM touchpoints mainly online, focused on social own media, belonging to marketing automation tools. CDP and SCRM have a downstream relationship, with CDP providing audience packages for the SCRM system to apply.<br><br>Application Scenarios: Mainly used for user operations on social platforms |


<span id="_2-产品功能相关概念"></span>
# 2. Concepts related to product functions

<span id="_2-1-数据融合"></span>
## 2.1 Data Fusion


|Functional Modules |Concept |Explanation |
|---|---|---|
|ID Mapping |BaseID |BaseID, the benchmark ID, is the OneID that the system uses to identify the user's identity. |
||Subject |Translation<br><br>Subject in CDP, the target object of ID\-Mapping OneID, such as people, cars, etc. |
|Visual modeling |Data Modeling |According to a certain data processing logic, the process of cleansing, processing, and generating metadata is called data modeling. |
||Data Connection |Build the configuration capability to connect with various data sources and achieve the primary function of data reading |
||Canvas |Organize various functional modules into a visual representation of a data processing flow according to directed processes. |
||Operator |Integrative capability for data reading, processing, algorithms, and data output in the canvas, corresponding to each processing node in the canvas |
||Connections between operators |Directed relationship between operators, referring to the channel of data flow between two operators |
||Task |The process of loading data from the input data source, undergoing data processing and cleansing, and eventually loading and outputting to the target data source. |
||Real\-time task |The data changes of the input data source can be instantly reflected in the output data; the data from the data source is updated in real\-time, and the data flow is visually modeled for high\-demand scenarios on timeliness. For example: Real\-time reports for live broadcasts, immediate recommendations based on user behavior. |
||Offline task |The data source data is updated at the daily/hourly level (i.e., updated daily/hourly) and the data processing process is a visualization modeling task executed on a scheduled basis or manually. |
||Dataset |A dataset is a data model composed of one or more tables, serving as the foundation for applications like labeling and clustering. |
||Execution record |Each task generates an execution record upon each run, which can be triggered manually by users or automatically by the system based on periodic configurations. |
||Processing flow |Displays the current model's data processing nodes and logic flow. |
||Full extraction |Extracts full data from the data source table, requiring setting extraction ranges through field values. |
||Incremental filtering |Based on the partition field, extract incremental data from the data source table, which is only supported by non\-partitioned tables. You need to specify the field used to determine the increment. |
||Field Settings |Support selecting reserved fields, setting field types, field names, and field sorting. |
||Connection |Data Join, supporting left, right, inner joins/outer joins, and cross\-source connections. |
||Aggregation |Select aggregation fields and methods, change the aggregation method, and set the name of the field after aggregation. |
||Computed Column |Use Spark functions to process upstream fields to add new fields. You can also add a business date field to tables without business dates. |
||Filter Rows |Select fields, confirm filter conditions, and support two layers of AND/OR logic relationships. |
||Data Split |The split operator will split the data according to this ratio into two parts. This value represents the proportion of the first part of the data to the input data. |
||String Indexing |A type conversion operator that maps the value of the specified attribute to a numerical index, allowing operators that can only process numerical data to also process attributes. This operator is generally used for data preprocessing. Additionally, it is not suitable for columns containing continuous data, such as ID columns. |
||Replace Missing Values |Used for replacing missing values. Replacement strategies include median replacement, mean replacement, etc. This algorithm requires the data in the specified column to be numerical data. |
||Deduplication |Remove duplicate options in the selected columns, where duplication refers to all values in the selected columns being the same |
||Binarization |Convert numerical features into binary features 0 or 1, dividing quantitative features into "yes" or "no" to eliminate redundant information |
||Column normalization |Normalize one column or multiple columns of a table, scaling the original data to the required range. After the original data is normalized, each indicator is at the same level, suitable for comprehensive comparative evaluation. |
||Principal Component Analysis |Principal Component Analysis (PCA) is the most widely used data reduction algorithm. The main idea of PCA is to map n\-dimensional features to k dimensions, where these k dimensions are brand new orthogonal features also known as principal components, reconstructed from the original n\-dimensional features. Only numerical data with a regular role can be operated on, and the output is usually an intermediate result that needs to be used as input for other operators. (See configuration interpretation) |
||Cartesian Product |The Cartesian product refers to the Cartesian product of two sets X and Y, also known as the direct product, denoted as X × Y. The first object is a member of X, and the second object is one of all possible ordered pairs of Y's members. |
||Discrete Cosine Transform |The Discrete Cosine Transform (DCT) transforms a real\-valued time\-domain sequence of length N into a real\-valued frequency domain sequence of length N. |
||Row Normalization |Normalization processing of data to address comparability between data indicators. After the original data undergoes normalization processing, each indicator is at the same magnitude, suitable for comprehensive comparative evaluation. |
||Singular Value Decomposition |A way of data dimensionality reduction that simplifies numerical data by projecting data onto a lower\-dimensional space by selecting higher singular values. |
||Feature Hashing |A simple dimensionality reduction method that compresses high\-dimensional feature vectors into lower\-dimensional ones while preserving as much of the original feature representation as possible. |
||One\-hot Encoding |A type conversion operator that maps a single column into a 0/1 vector, with at most one value being 1. |
||Calculate Weight |Calculates the weight of a given attribute. |
||Classification |Logistic Regression, Decision Tree |
||Clustering |K\-Means Clustering |
||Evaluation |Binary Classification Evaluation, Multi\-class Evaluation, Clustering Evaluation, Regression Evaluation |


<span id="_2-2-标签体系"></span>
## 2.2 Labeling System


|Concept |Explanation |
|---|---|
|Tag |A business\-meaningful, enumerable value created based on behavioral or attribute data, defined by business logic or model capabilities. |
|Tag System |A structured framework composed of tags, used to present and manage elements such as tag quantity, classification, and hierarchical relationships. |
|Full Tags (Mautag) |The complete set of tags covering the total number of users under the group, updated daily. |
|Text type tag value |Used for text\-type value tags, commonly used for labels like names, usernames, cities, etc. |
|Integer type tag value |Used for integer\-type value tags, commonly used for labels like age, click counts, visit counts, etc. |
|Decimal type tag value |Used for decimal\-type value tags, commonly used for labels like costs, percentages, etc. |
|Multi\-value type tag value |Used when there are multiple values for a tag, commonly used for labels like interests, favorite topics, etc. |
|Date type tag value |Used for date\-type value tags, specific to dates, commonly used for labels like birthdates, etc. |
|Date and Time Label Value |Used for labels with date and time type values, precise to hours, minutes, and seconds. Commonly used for labels such as update date. |
|AIPL Model |A means brand awareness audience; I means brand interest audience; P means brand purchase audience; L means brand loyalty audience |
|5A Model |Philip Kotler introduced a marketing model in "Marketing 4.0," consisting of A1: Aware (passively receives information), A2: Appeal (increases brand impression), A3: Ask (actively seeks information out of curiosity), A4: Act (takes action), A5: Advocate (loyal customers who promote the brand) |
|RFM Model |The model evaluates the Recency (R), Frequency (F), and Monetary Value (M) of each user, categorizing them into 8 customer types: Important Value Customers, Important Recall Customers, Important Developing Customers, Important Retention Customers, Potential Customers, New Customers, General Maintenance Customers, and Lost Customers.<br><br>R: Recency, reflecting a customer's activity level.<br><br>F: Frequency, reflecting a customer's loyalty.<br><br>Consumption amount (Monetary) reflects a customer's contribution. |
|Select "AND" for the criteria |If all rules or combination rules are met, it will be considered as meeting the labeling rules. |
|Select "OR" for the criteria |If any rule or combination rule is met, it will be considered as meeting the labeling rules. |
|Does not contain |Users who do not meet the criteria within the data range of the current dataset. |
|Contains |Users who meet the criteria within the data range of the current dataset. |
|Global does not contain |Exclude users with this label value from all users (including those not labeled with this tag) (For example: if there are 100 users in total, with 10 labeled "elderly" as follows: "yes" 4 people, "no" 5 people, "other" 1 person. Select this tag globally not including "yes", i.e. select 96 people.) |
|Divide the tag values based on discrete numerical values |Directly use the indicator calculation result value as the tag value |
|Divide the tag values based on numerical ranges |Set user segmentation tags based on the threshold range of the indicator calculation result value |


<span id="_2-3-用户分群"></span>
## 2.3 Segmentation


|Concept |Explanatory notes |
|---|---|
|Population ID type |Grouping file output based on what ID type |
|Cluster name |Cluster Package Name, the object within the cluster may be a person or an item |
|Output Subject |In the "Cluster Subject Transformation" section, enter the clustering file of Subject 1 to transform output for another subject's clustering |
|Encryption Method |SHA256/MD5 Encryption |
|Unpacking |* Random Unpacking:<br><br>1. Randomly select the specified number of people from the target audience;<br><br>2. Can randomly split into multiple packages;<br><br>3. The final result is: Master Package + N random sub\-packages, each sub\-package has a unique audience ID.<br><br>   \-Proportional unpacking:<br><br>4. Evenly split into N sub\-packages;<br><br>   2.The final result includes the original package plus N sub\-packages, where each sub\-package contains unique user IDs and an equal number of users. |
|Group Size |The number of individuals included when a segmentation file is generated through audience selection. |
|Static Segmentation |Cluster update frequency: One\-time |
|Dynamic Clustering |Cluster update frequency: daily/on demand |
|Lookalike Audience Expansion |Expands the seed segment by identifying similar individuals to enlarge the target audience as needed. |


<span id="_2-4-用户洞察"></span>
## 2.4 User Insights


|Functional Module |Concept |Explanation |
|---|---|---|
|Group Insights |Market TGI |When the value is greater than 100, it indicates that the clustering package has a relatively strong tendency or preference; the larger the value, the stronger the tendency and preference; when it is less than 100, it indicates a weaker tendency (compared to the average); when it equals 100, it indicates an average level.<br><br>Calculation Formula: (Identifiable tagged users in the segment / Total users in the segment) ÷ (Identifiable tagged users in the project / Total users in the project) \* 100 |
||Tag Proportion |In the cluster package, the proportion of the tag values in the current cluster package.The higher the proportion, the greater the absolute number of users with the tag in the segment.<br><br>Formula: Number of users with label values in the cluster package / Number of users in the cluster package \* 100% |
||TGI Tag |If the value of a label in the subgroup package is greater than 100, it indicates a relatively stronger tendency or preference for that label; the larger the value, the stronger the tendency and preference. If the value is less than 100, it indicates a weaker tendency compared to the average; if it equals 100, it represents an average level.<br><br>Calculation Formula: (Identifiable tagged users in the segment / Total users with the tag in the segment) ÷ (Identifiable tagged users in the project / Total users with the tag in the project) \* 100 |
||Effective Label Coverage |In the subgroup package, the label value is the percentage of the total number of labels in the current subgroup package.<br><br><span id="translation"></span><br>## Translation<br><br>The higher the proportion, the more absolute number of people there are in the subgroup package.<br><br>Calculation formula: Number of users with tag values in the segmented package / Total number of users with tags in the segmented package \* 100% |
||Drilling analysis |Expand the next layer of data in the current dimension |
||Cross\-analysis |Insight into the relationship of individual groups in two portrait dimensions |
|Life Cycle Analysis |Total number of users |Total number of people on the day |
||Daily ring ratio |(Total number of people that day / Total number of people the previous day \- 1) x100% |
||Daily additions |Users who were not in the total assets yesterday, but were in that day |
||Churn of the day |Users who were in the total assets yesterday, but were not there that day |
|Multidimensional feature analysis |Comprehensive score for feature combination |An index that best reflects the effect of tag combinations, with results ranging from 0 to 1. The larger the number, the better the effect. The scoring calculation logic is precision \* 0.8 + recall \* 0.2, weighted calculation of the two to get the result. |
||Recall rate |The proportion of the population with feature combinations that meet the filtering conditions in the positive samples, in the overall positive sample population. For example, if there are 100 people in the positive sample who meet this feature, and the total positive sample is 1000 people, then the recall rate is (100/1000) \*100% = 10% |
||Precision |The proportion of the group of people in the positive sample who meet the screening criteria, in the total positive and negative samples. For example: if there are 400 people in the positive sample who meet this feature, and 100 people in the negative sample who meet this feature, then the precision is 400 / (400+100) \*100% = 80% |
||The number of people in the positive sample |The group of people in the positive sample who meet this feature |
||The number of people after expansion |Based on the expansion of the group of people in the positive sample |


<span id="_2-5-权限"></span>
## 2.5 Permissions


|Concept |Explanatory note |
|---|---|
|Project |It is an independent "space" used by the product. Except for sharing server hardware resources, all other resources between projects are independently isolated, such as user permissions and data resources are different in Project A and Project B. |
|User |The user of the product needs to be created in the Portal console, with information such as projects, accounts, emails, and phone numbers. |
|User Group |A group of users with special business meanings, belonging only to a user group of a specific project, needs to be created independently in CDP Project Center\-Authorization Management. |
|Module |Refers to the functional modules of the CDP product, corresponding to their respective menus. Authorization to Use Modules in Project Center |
|Resource |Resources produced by users in CDP, such as labels, datasets, audience packs, insight reports, and visual modeling tasks. Support resource authorization in Project Center (authorization for user segmentation and user insights is performed on the details page). |
