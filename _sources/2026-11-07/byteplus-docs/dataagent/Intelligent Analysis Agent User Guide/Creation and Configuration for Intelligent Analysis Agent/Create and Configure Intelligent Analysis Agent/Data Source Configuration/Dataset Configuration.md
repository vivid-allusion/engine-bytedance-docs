---
title: "Dataset Configuration"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Dataset_Configuration"
---

The intelligent analysis Agent's queries will be based on the data from the dataset configured in this step. Users can customize the scope of datasets that the intelligent analysis Agent queries, allowing the intelligent analysis Agent to better serve current business needs. This article provides guidance on configuring datasets that the intelligent analysis Agent can query when creating and configuring the intelligent analysis Agent.

<span id="b5702e05"></span>
# Prerequisites

Before configuring the intelligent analysis Agent's dataset, you need to first create the corresponding data as a DataAgent dataset and complete the data preparation process. For details, see: [Data Preparation Overview](https://docs.byteplus.com/docs/dataagent/Data_Preparation_Overview).

<span id="d0ccf91d"></span>
# Access the dataset configuration page

After entering the intelligent analysis Agent management configuration page, click "Dataset configuration" in the left navigation bar to access the dataset configuration page.

Starting from version 3.17, adding a dataset and initiating initialization will enable dataset vectorization by default. For details, see below: [Dataset initialization](https://docs.byteplus.com/docs/dataagent/Dataset_Configuration#97de00dc).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/da44cdeae0b343b69f1418e090e221d2~tplv-goo7wpa0wc-image.image) </span>

<span id="7a84f8e5"></span>
# Add a dataset

<span id="08f81c6a"></span>
## Select a dataset

You can click "Add dataset" on the page to add datasets you have permission for.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b865f6e6f8954528bb928e291107191d~tplv-goo7wpa0wc-image.image) </span>

<span id="ee287af0"></span>
## AI configuration recommendations

The intelligent analysis Agent provides the "Optimize dataset configuration" feature. By uploading some questions, the AI will offer recommendations for dataset configuration. When using this feature,


1. Click the "Optimize dataset configuration" button, follow the interface prompts to download the question template, fill in the "Dataset name" and possible "Questions", then click "Batch upload questions". The product will help optimize dataset configuration based on the user's possible questions about the dataset.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8c284fbc7f9647a48d4192b0c13e75a8~tplv-goo7wpa0wc-image.image) </span>


2. After a successful upload, click "Confirm". Once the optimization recommendations are generated, click "View".


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e7ade39877cd4d1784596311cccb2412~tplv-goo7wpa0wc-image.image) </span>

<span id="64ec9aee"></span>
# Configure a dataset

<span id="de051635"></span>
## Configure a semantic model

<span id="145f6357"></span>
### Configuration key points


|Segmentation |Key points |
|---|---|
|Configuration purpose |The semantic model allows you to redefine the dataset name, field names, and other information based on the dataset for use by agents. This is primarily to help the model better understand what data is contained in the dataset and the business semantics of these fields, thereby improving the accuracy of automatic dataset selection and question answering by the agent.<br><br>For example, in actual business scenarios, users may use certain conventional jargon to refer to specific fields or field values. You can configure this jargon as synonyms for field names or field values. |
|Notes |* If the semantic model name, field names, and so on are not redefined, the definitions from the dataset will be used.<br><br>* Once fields are enabled or disabled, newly added fields in the dataset will not be automatically included in the current semantic model. You can manually enable them as needed. |


<span id="dd5f3232"></span>
### Operation guidance


1. Click "Semantic model" on the dataset configuration page.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/947fd39898d7486ba5b87d75a7c64e98~tplv-goo7wpa0wc-image.image) </span>


2. Click "Set model basic information" to add a name, description, and features to the semantic model.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/521cc071d5e848a1a9c32a8445f6e736~tplv-goo7wpa0wc-image.image) </span>

The relevant parameter configuration instructions are as follows:


|Parameters |Configuration instructions |
|---|---|
|Semantic model name |Supports user\-defined semantic model names. If not specified, the name will default to the dataset name. |
|Semantic model description |Supports adding a description for the semantic model. If not specified, the description will default to the dataset description. |
|Features |The feature values of the semantic model are used to define the key features that distinguish the current dataset from other datasets. Users can separate multiple values with commas or line breaks.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">Features affect the priority of dataset recall in the Agent Table.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">It is recommended that the length of a single feature does not exceed 5 characters, and the total number of features does not exceed 10.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">Feature examples: aaa, bbb, ccc</div><br> |



3. Click "Configure" to enter the semantic model field configuration interface, where you can configure semantic models for fields in the dataset. The top of the field configuration interface displays the names and types of the fields in the dataset.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a3b4d5e31e54440e9d3dc01892b2320d~tplv-goo7wpa0wc-image.image) </span>

There are some differences in the configuration parameters for fields of different data types. The descriptions of each configuration parameter are as follows.


* General configuration parameters

   
   |Parameters |Configuration instructions |
   |---|---|
   |Agent field name |Users can customize the agent field name. When the query description matches this name, the agent will prioritize using this field for the query. If left blank, the field name will remain consistent with the dataset field name.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The agent field name can be left blank and should not be modified unless necessary, because any modification will directly overwrite the original field name in the dataset.</div><br> |
   |Field name synonyms |Users can set one or more synonyms for the field name. When the query description matches any of these synonyms, the agent will prioritize using this field for the query. Separate multiple synonyms with commas or line breaks. |
   |Field description |Users can add a description for the agent field to help with understanding the field. If left blank, the description will remain consistent with the dataset field description. |
   |Default recall |If "Default recall" is selected, this field will be transmitted as a prompt to the large model every time a question is asked. |
   

* Text field\-specific configuration parameters

   
   |Parameters |Configuration instructions |
   |---|---|
   |Field value recall |For text fields, the field value recall button is enabled by default. You can disable it as needed. Once disabled, the field value will not be recalled. |
   |Field value denylist |Field values that should not be recalled |
   |High\-frequency field value instructions |For high\-frequency text fields, you can configure the scope of the field's meaning. The configuration example is as follows.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/abb16d2cc2df4755ba0c0b56f6c46372~tplv-goo7wpa0wc-image.image) </span> |
   

* Numeric field\-specific configuration parameters

   
   |Parameters |Configuration instructions |
   |---|---|
   |Default calculation method |Select the default calculation method for numeric field values in the dropdown menu. Currently supported: sum, count, count distinct, average, maximum, minimum.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fe83aa3217664ae090518152afcbc9a9~tplv-goo7wpa0wc-image.image) </span> |
   

4. Enable fields that require the use of semantic models.

   You can search and enable the semantic model configuration for each required field in the dataset individually, or click "Batch enable status" at the bottom of the field list to enable the semantic model configuration for all fields in the dataset.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ddb0fa5f16704c79ba332f32a6624629~tplv-goo7wpa0wc-image.image) </span>

<span id="e8571b9f"></span>
## Configure the knowledge base

<span id="227e1756"></span>
### Configuration key points


|Segmentation |Key points instructions |
|---|---|
|Configuration purpose |The agent supports configuring a knowledge base for the dataset. Users can add industry slang, insider terms, inaccurate expressions, or ambiguous expressions to the knowledge base, enabling the large model to better understand the questions posed by users. |
|Caution |Dataset editing or higher permissions are required to add entries. |


<span id="d39db947"></span>
### Operation guide


1. Click "Knowledge Base" in the dataset configuration to enter the enterprise knowledge engine configuration page.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7a3a93820a7a4980874b39d722b80ee1~tplv-goo7wpa0wc-image.image) </span>


2. Click "Knowledge Base" to configure the knowledge base.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e726c271c3d4442db78d4f90fbdf2edf~tplv-goo7wpa0wc-image.image) </span>

The descriptions of the relevant parameter configurations are as follows:


|Parameters |Configuration instructions |
|---|---|
|Matching threshold |Adjust the vector matching degree between business terms and questions. The minimum is 0, the maximum is 1, and 1 indicates precise matching.<br><br>(Users unfamiliar with large models are advised not to adjust this setting) |
|Knowledge recall limit |Controls the maximum number of knowledge items that can be recalled at one time from the current dataset, preventing excessive recall from interfering with the large model.<br><br>(This can be configured, but it is not recommended to set too high a value. A range of 2 to 5 is preferable.) |



3. Click "Add Knowledge" to add more knowledge to the knowledge base.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/145a275ca86d4aaa9a48d1d48c512193~tplv-goo7wpa0wc-image.image) </span>

The knowledge of the dataset is usually used to describe a data range formed by combining dataset fields. The descriptions and examples of relevant parameter configurations are as follows:


|Parameters |Configuration instructions |Configuration example |
|---|---|---|
|Business terms |Common business expressions such as unique terms, jargon, and frequently used terminology names. When the recall rule is 'Follow knowledge base configuration', business terms are used as keywords to recall the corresponding knowledge item. |For example, for a dataset of population profiles, when it is necessary to break down population fields according to the profile:<br><br><br>* Urban white\-collar population: city field (Beijing, Shanghai, Guangzhou) + age field (20~50) + income field (20,000~60,000) |
|Connectors |Used to connect business terms and explanations, including two types: 'indicates' and 'none'. The purpose of connectors is mainly to make the entire sentence more fluent. You can decide whether a connector is needed based on the fluency of the previewed knowledge sentence. ||
|Explanation |* Enter the definition, explanatory notes, and so on for the knowledge. This is the core part of the knowledge. The explanation must be precise and easy to understand to help the large model interpret it more accurately. For example, the explanation for the business term 'search performance criteria' is 'Definition: Orders/traffic counted as search'.<br><br>* Supports referencing fields in the dataset using '`[ ]`'. ||
|Synonyms |Synonyms of business terms serve the same purpose as business terms. For example, synonyms for age distribution include age profile, age composition, and age structure. ||
|Preview |You can use the preview to check whether the overall knowledge is fluent. This is the final knowledge provided to the model, which includes the concatenation of business terms, connectors, and explanations. ||
|Recall rules |Includes following knowledge base configuration, default recall, and custom rules.<br><br><br>* Following knowledge base configuration means matching knowledge based on the similarity of business terms or synonyms.<br><br>* Default recall means this knowledge item will be transmitted to the large model as a prompt every time a question is asked.<br><br>* Custom rules refer to keyword matching rules based on user questions. You can set keywords to be included or excluded, and multiple keywords can be entered. The relationship between multiple keywords is 'AND'. ||
|Fields participating in recall |Field name recall refers to whether this knowledge participates in field recall. Participation is achieved by recalling based on the field name within the knowledge. For example, the knowledge name: Sales performance represents sales amount and profit margin. If this knowledge participates in recall, it will recall the fields sales amount and profit margin. ||
|Field values participating in recall |Field value recall refers to whether this knowledge participates in field recall. Participation is achieved by recalling based on the field value within the knowledge. For example, the knowledge name: Douxi represents Douyin, Xigua, and Jinri Toutiao. If this knowledge participates in recall, it will recall the "product name" field based on values such as Douyin, Xigua, and Jinri Toutiao. ||


<span id="3236e21b"></span>
## Configure filtering


1. The user clicks "Filter Configuration" to enter the dataset filter configuration interface, where the data used by the agent can be filtered based on dimension fields or metric fields in the dataset.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b236f70f81ca494b90fc8ad6f34506d5~tplv-goo7wpa0wc-image.image) </span>


2. Set the filter conditions for the dataset used by the agent. The user can use dimension filtering, metric filtering, or date filtering according to the required data situation.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/85d125594ea44a808021bb507a56b10f~tplv-goo7wpa0wc-image.image) </span>


|Filter conditions |Applicable scenarios |Operation guide |
|---|---|---|
|Dimension filtering |Data needs to be filtered according to dimension fields. For the distinction between dimension and metric fields, see [Dimensions and Metrics](https://docs.byteplus.com/docs/dataagent/Dimensions_and_Metrics). |[Dimension Filtering](https://docs.byteplus.com/docs/dataagent/Dimension_Filtering) |
|Metric filtering |Data needs to be filtered according to metric fields. For the distinction between dimension and metric fields, see [Dimensions and Metrics](https://docs.byteplus.com/docs/dataagent/Dimensions_and_Metrics). |[Metric Filtering](https://docs.byteplus.com/docs/dataagent/Metric_Filtering) |
|Date filtering |Data needs to be filtered according to date\-type fields. |[Date Filter](https://docs.byteplus.com/docs/dataagent/Date_Filter) |


<span id="00d02787"></span>
## Configure dataset readiness

Click "Dataset Readiness Configuration" to enter the dataset readiness configuration interface, where you can set the synchronization date and time for dataset readiness. After setting, click "Save".


* When a proactive push is triggered in Lark, it will check whether the T\-N time partition data is ready. If the partition data is ready, the push will begin.

* Example: Set to T\-2. On 2020\-10\-05, after completing data synchronization for "2020\-10\-03", the relevant proactive push will begin.


<span id="38d512e8"></span>
## Import semantic models and knowledge bases from other agents

The intelligent analysis agent supports directly importing semantic model and knowledge base configurations from other agents. When you add a dataset to an agent and configure its semantic model and knowledge base, you can later create a new agent and use the same dataset. If the field semantic model and knowledge base configurations are similar to the previous ones, you can directly import the corresponding configurations into the new agent.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Only users with administrator permissions can perform import operations.</div>


* <div data-tips="true" data-tips-type="warning">If the semantic model of the imported dataset contains fields identical to those configured in the current dataset's semantic model, the imported semantic model will overwrite the existing configuration for those fields.</div>


1. The new agent already includes datasets that have been added and configured in other agents.

2. On the dataset page of the new agent, click the "Import from other agents" button in the upper right corner of the page.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/721dc08644944e7a896a3abaa594b79e~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fce020627d1d4c7e859669904b29a9af~tplv-goo7wpa0wc-image.image) </span>


3. In the pop\-up window, select the agent and dataset containing the semantic model and knowledge base to import, and select the semantic model or knowledge base to import.

   * Import semantic model:

      * The semantic model configuration for each field in the source agent's dataset (agent field name, synonyms, recall switch, and more) will be synchronized to the dataset in the current agent.

      * The basic model information set in the source agent's dataset (semantic model name, features, and more) will not be synchronized to the current agent. Therefore, after importing, the basic model information for the current agent's dataset needs to be manually set as required.

   * Import knowledge base:

      * Each piece of knowledge added to the source agent's dataset (business name, connector, description, and more) will be synchronized to the dataset in the current agent.

      * The knowledge base configuration (matching threshold, knowledge recall limit) set in the source agent's data will not be synchronized to the current agent. Therefore, after importing, you need to manually configure the knowledge base settings for the current agent's dataset as needed.

4. After selecting, click "OK" to complete the import.


<span id="18f3596c"></span>
# View dataset list and status

After completing the dataset configuration, you can view the list of datasets available for querying by the current agent and check the application status of each dataset on the dataset configuration page.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/40b9ccc924104ee78e0c86f7353e5221~tplv-goo7wpa0wc-image.image) </span>

<span id="97de00dc"></span>
## Dataset initialization

After adding a dataset, the system will automatically initialize the dataset and perform dataset vectorization. During or after initialization, you can click the "Initializing" or "Completed" status in the status column, then click "View details" to jump to the initialization configuration page and view the configuration details.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/021790b5291c407e928d964abaa01328~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/11c4c783f97641929b3ef716ff48c2d5~tplv-goo7wpa0wc-image.image) </span>

The initialization configuration interface is shown below:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/244e2f70ba82447ba1d11e8537035c71~tplv-goo7wpa0wc-image.image) </span>

Dataset initialization may also have two statuses: incomplete and failed. You can retry the initialization configuration according to the prompts on the interface:


* **Incomplete**: Initialization has not started yet. You need to click the "Incomplete" status, then click "Go to initialization configuration", and follow the prompts to complete the dataset initialization settings.

* **Failed**: The current dataset initialization has failed. You can click the "Failed" status and, according to the pop\-up prompt, contact a user with editor permissions or higher to complete the initialization configuration.


<span id="de702636"></span>
## Enable/disable dataset vectorization

After dataset initialization is completed, dataset vectorization is enabled by default. If the dataset does not need to be queried or used by the current agent in the future, you can click "Completed" in the status column, jump to the initialization configuration page, and disable vectorization.

After disabling, the dataset configuration will be retained, but the corresponding dataset will no longer be queried or used by the agent in subsequent operations.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0ac6cfb9642d4c9d967ce1d65c059490~tplv-goo7wpa0wc-image.image) </span>

<span id="22044633"></span>
## Enable/disable dataset application scenarios

After the dataset is created, intelligent Q&A and in\-depth research are enabled by default. You can enable or disable the corresponding switches in the list as needed.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/72f43a41f2ea4cc3a58acc88b0bdb69f~tplv-goo7wpa0wc-image.image) </span>

<span id="8fdfa336"></span>
# Delete dataset


* Supports deletion of added datasets.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c263f730095646f784f257eb7788f10c~tplv-goo7wpa0wc-image.image) </span>


* If the current dataset has been used in recommended questions, you must modify the recommended questions before you can delete the current dataset.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a8817837a31b4dc69e733df659a6e524~tplv-goo7wpa0wc-image.image) </span>
