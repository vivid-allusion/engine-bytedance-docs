---
title: "Data Masking"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Data_Masking"
---

This article introduces how to use the data masking feature, including sensitivity classification of datasets, configuration of masking rules, and the effects of masking application.

<span id="328805c2"></span>
# Feature overview

Data masking refers to applying masking rules to fields containing sensitive information. After enabling this feature, the corresponding fields will be masked, transformed, or obfuscated according to the specified rules, thereby protecting the privacy of sensitive data in the workplace and meeting the company's compliance requirements.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This feature is a value\-added module. To experience it, please <a href="https://docs.byteplus.com/docs/DataWind/Contact_Us">Contact Us</a>.</div>


<span id="2078dc5d"></span>
## Feature overview


|Feature modules |Feature introduction |User roles |
|---|---|---|
|Sensitivity classification |When saving a new data set or editing an existing data set, the system will require sensitivity classification for the data set, including "sensitive" and "non\-sensitive" categories, which must be determined proactively by the data set creator. |Administrator, data set creator |
|Masking rule configuration |After a data set is defined as "sensitive", masking rule configuration is required for the data set. The data set creator adds all sensitive fields and selects the corresponding masking rule from the "masking rule" dropdown list. |Administrator, data set creator |
|Masked data set application |After a data set is defined as "sensitive", masking effects and operational masking restrictions will appear when the data set is used in modules such as visual query, dashboard, and visual modeling. |Data set creator<br><br>Users and viewers with permission for the data set |
|Masked display |After desensitization rules are configured and applied to a dataset, the dataset will be displayed in a desensitized form during presentation. Fields configured for desensitization will appear distorted or blurred, and similar effects. |All viewers with permission to view charts and dashboards created based on the dataset |


<span id="d849a59e"></span>
## Feature value

In the information age, our requirements for data security are becoming increasingly stringent. Whether through government\-issued laws and regulations or industry\-specific guidelines, all require security for various types of sensitive data, such as personal information. Data masking can help reduce the risk of sensitive data leakage and provide an additional layer of protection for privacy data. By adding the data masking feature, the need for manual data masking in traditional business scenarios can be greatly reduced, improving data delivery efficiency and increasing satisfaction among stakeholders. At the same time, it enables data processors, analysts, and viewers to use data in accordance with enterprise information security requirements, further promoting the construction of enterprise information security.

<span id="69270f84"></span>
## Feature advantages


* Flexible configuration of masking rules: Users can configure masking for specific fields based on data sensitivity, supporting various masking rules such as full masking, name masking, email masking, and contact information masking.

* Freely controllable scope of masking effectiveness: Users can set the scope of data masking according to specific business needs, configuring it for sensitive user ranges to better suit business requirements.


<span id="221da655"></span>
# Quick start

When saving a new dataset or editing an existing dataset, you can configure data masking rules.

<span id="0aaad57a"></span>
## Create a dataset

When saving a dataset, you need to select the "Confidentiality Level" option to determine whether the dataset contains sensitive information. If the dataset contains sensitive fields, set the level to "Sensitive"; otherwise, set it to "Not Sensitive".


* After selecting the sensitive option, you must promptly add masking rules for sensitive fields under the "Data Masking" tab in the dataset details page; otherwise, an error prompt as shown below will appear.

* If you select the not sensitive option, no further configuration is required. All data fields will not be masked, and the displayed field values will be the original values.


<span id="a139b73d"></span>
## Edit a dataset


1. Click "Data Preparation" \- "Dataset", select a dataset, enter the dataset details page, and click "Data Masking".

2. Click "Add Masking Field", select the fields to be masked, and click "OK".

3. Add the corresponding masking rules to the fields that require masking. The system provides preset matching rule items for all sensitive fields, supporting various masking rules such as full masking, name masking, email masking, and contact information masking. Both preset and custom masking rules are supported.

4. Set the scope of data masking, add users or user groups, and configure the rules for the scope of effect. The following two configuration methods are supported:

   * Applicable members are subject to rule control; users other than members are not subject to rule control.

   * Applicable members are not subject to rule control; users other than members are subject to rule control.

5. You can add multiple masking fields. After adding them, click "OK". After saving, you can view the masking results under the "Data Preview" tab.

6. Refresh to view the masked data, as shown below.


<span id="0feab05f"></span>
# Function description

<span id="0f6a390d"></span>
## Dataset status


|Dataset status |Description |
|---|---|
|Unclassified |After a dataset completes the deployment of data desensitization, the status of all existing datasets will be 'Unclassified'. The dataset creator must classify each dataset under their ownership one by one. When a dataset is in the 'Unclassified' status, a corresponding icon will be added to the left directory list and after the title on the details page for marking. The page will also display an abnormal reminder, prompting timely completion of the classification operation. |
|Sensitive but not desensitized |After a dataset is marked as 'Sensitive' during the sensitivity classification step. The dataset will be defined as 'Sensitive but not desensitized'. The dataset creator must select the sensitive fields and configure the desensitization rules for the dataset. When a dataset is in the 'Sensitive but not desensitized' status, a corresponding icon will be added to the left directory list and after the title on the details page for marking. The page will also display an abnormal reminder, prompting timely completion of the classification operation. |
|Sensitive and desensitized |After the dataset creator selects the sensitive fields and configures the desensitization rules for the dataset, it will be marked as 'Sensitive and desensitized'. When a dataset is in the 'Sensitive and desensitized' status, a corresponding icon will be added to the left directory list and after the title on the details page for marking. |
|Not sensitive |After a dataset is marked as 'Not sensitive' during the sensitivity classification step, it will be classified as a 'Not sensitive' dataset. |


**Impact on associated datasets**：


* When there is at least one masked child dataset, the logical dataset inherits the "sensitive and masked" status.

* The masked fields of the logical dataset are the union of all masked fields from the child datasets.

* All adjustments to data masking rules in child datasets are synchronized to the logical dataset.


<span id="ccee167b"></span>
## Data masking rules

<span id="8ce4a5f2"></span>
### Preset masking rules


|Desensitization rules |Rule description |Rule details |
|---|---|---|
|Name desensitization |Applicable to desensitization of name fields. |Keep the first character unmasked; mask the remaining part with \* |
|Email desensitization |Applicable to desensitization of email fields. |Retain the actual information after the @ in the email address, and mask the preceding part with \*, including special characters; if there is no @, mask the entire value. |
|Masking of contact information |Applicable to masking mobile phone number and landline number fields. |Keep the first 3 characters unmasked, and mask the remaining part with \* |
|General rules for Chinese identification numbers |Applicable to masking fields for various types of identification numbers, such as organization code, bank card number, business license number, and business registration number. |Keep the first 3 characters unmasked, and mask the remaining part with \* |
|Masking of Chinese citizen ID |Applicable to masking ID fields for Mainland China, Hong Kong, Macau, and Taiwan regions. |Keep the first 3 characters unmasked, and mask the remaining part with \* |
|Full masking |Mask all information in the field. |Mask all information in the field |


<span id="753f1b2e"></span>
### Custom masking rules


|Masking rules |Rule details |
|---|---|
|Masking of middle characters |Keep the first M characters and the last N characters, and replace the remaining characters with \* |
|Masking of head and tail characters |Keep characters from position M to position N, and replace the remaining characters with \* |
|Masking before special characters |Replace characters before special character X with \*<br><br>Special characters include: " ¥ $ ' & ( ) + \- ‘ / . ; : = ? @ % [ ] \ _ |
|Masking after special characters |Replace characters after special character X with \*<br><br>Special characters include: " ¥ $ ' & ( ) + \- ‘ / . ; : = ? @ % [ ] \ _ |


<span id="69392b37"></span>
## Scope of data masking

<span id="c8e790a1"></span>
### Scope of effect

The scope of effect supports configuring a denylist or allowlist.


* Applicable members are subject to the rules, while users outside the members are not subject to the rules.

* Applicable members are not subject to the rules, while users outside the members are subject to the rules.


<span id="c7f1aee0"></span>
### Effective members

It is supported to add users or department\-level user groups as effective members.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">In an on\-premises environment, data masking can also be configured to take effect based on "role", in addition to "user" and "user group".</div>


<span id="7db25da9"></span>
## Data masking application effects

<span id="2a811bdd"></span>
### Visualization query effects

<span id="286d7ab9"></span>
#### Description of masking status

When a dataset contains sensitive data, the following indicators are displayed for different statuses

<span id="a760d26e"></span>
#### Functional differences of masked datasets

Supported: Sensitive fields can be used as dimensions, measures, and filters; all chart and analysis functions are supported for normal use.

Not supported: For specific unsupported features, see the following content.


* When rendering tables and charts, data in sensitive fields is masked.

* When a sensitive field is used as a dimension, the "field value alias", "geographical role", and "create group" functions are not supported.

* When a sensitive field is used as a measure, the "create group" function is not supported.

* When a sensitive field is used as a chart measure, only the aggregation methods "count", "count distinct (fast)", "count distinct", "maximum", and "minimum" are supported, and the "set data format" function is not supported.

* When a sensitive dimension field is used as a filter, only "exact filter" is supported, and the dimension values of the field are also masked.

* Calculated fields: When a field expression contains sensitive fields, the sensitive fields are displayed in red, and the expression inherits the rules of the masked fields.

   * When the expression is not processed at all, execution follows the data source field rules.

   * When the expression is processed, execution follows the fully masked field rules.


<span id="456ca4fb"></span>
### Dashboard effects


* When the global filter contains sensitive fields, the values of sensitive dimensions are masked.

* For data download and dashboard export functions, all data in sensitive fields is masked. The left side of the figure below shows downloaded data, and the right side shows the dashboard.

* For dashboard subscription, monitoring, and embedding functions, the results are displayed in their masked form.


<span id="617c6008"></span>
### Visual modeling effects

The data set output from visual modeling does not inherit the masking field controls of the input data set. After being output as a new data set, the classification status is "unclassified", and the user who creates it must reconfigure the masking fields. The configuration operations are consistent with the content described earlier in this document.
