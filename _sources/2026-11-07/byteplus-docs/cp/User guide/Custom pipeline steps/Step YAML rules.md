---
title: "Step YAML rules"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Step_YAML_rules"
---

Rules for writing Inputs and Outputs parameters in custom steps YAML

<span id="inputs"></span>
## Inputs

Inputs are used for configuration of step input information and support configuring multiple step parameters. The table below describes the meaning and rules of each step input parameter.


|**Name** |**Required** |**Sample value** |**Descriptions** |
|---|---|---|---|
|name |Yes |ENV_ID |Parameter name. "name" is the unique identifier for the input parameters of the current step, and duplicate names are not allowed. Supports injecting the current input parameter into a script using the `export KEY=$(inputs.name)` syntax.<br><br>Supports uppercase and lowercase English letters, numbers, and the hyphen ("\-"); length must be between 2 and 50 characters. |
|displayName |Yes |environment |Parameter display name. Used for displaying parameter names; must not be empty or have duplicate names.<br><br>Supports uppercase and lowercase Chinese and English letters, numbers, and hyphens (\-); length must be between 2 and 50 characters. |
|description |no |This is description information. |Description information. Display a question mark next to displayName, and show the description when the question mark is hovered over.<br><br>Limited to 200 characters; supports Chinese and English characters, as well as special characters. |
|type |Yes |string |Parameter types Optional values are:<br><br><br>* string: Applicable when uiConfig.type is set to Input, Select, CodeEditor, Password, or Text.<br><br>* array: Applicable in scenarios where uiConfig.type is CheckBoxGroup. |
|defaultValue |no |Development environment |Default value.<br><br><br>* Caution: When entering a default value, it must match the type. When type is string, defaultValue is a value of type string; when type is array, defaultValue is a value of type array.<br><br>* When validateRule is defined, defaultValue must comply with the rules specified by validateRule. |
|required |Yes |true |Required<br><br><br>* true: Required. Display a small red star to the left of displayName. When saving the Step, the system will verify whether the current parameter has been filled in.<br><br>* false: Optional. |
|uiConfig |no | *\-*  |UI component configuration for the frontend interface.<br><br>If uiConfig is not set, the Input text box is used by default. |


<span id="uiconfig"></span>
## uiConfig


|**Name** |**Required** |Sample value |**Descriptions** |
|---|---|---|---|
|type |Yes |Input |UI component types. Optional values are:<br><br><br>* Input: Text box.<br><br>* Select: Drop\-down list<br><br>* CheckBoxGroup: Check box.<br><br>* CodeEditor: Command line, supports Bash commands by default.<br><br>* Password: Text box in which input is displayed as asterisks.<br><br>* Text: Fixed text, displays a section of read\-only text. When using fixed text, you must also specify defaultValue. This value will be displayed directly in the Step form. |
|dataSource |no |```yaml```<br>```uiConfig:```<br>```  type: CheckBoxGroup```<br>```  dataSource:```<br>```    value:```<br>```      - label: a```<br>```        value: a```<br>```      - label: b```<br>```        value: b```<br>```      - label: c```<br>```        value: c```<br> |Data source, used to define the selectable values for this component.<br><br>Only applicable to the Select and CheckBoxGroup components. |
|validateRule |no |```yaml```<br>```# Length validations```<br>```uiConfig:```<br>```      type: Input```<br>```      validateRule:```<br>```        - max: 5```<br>```          min: 2```<br>```          message: ```<br>```Regular expression validation```<br>```uiConfig:```<br>```      type: Input```<br>```      validateRule:```<br>```        - pattern: ^a```<br>```          message: ```<br> |Validation rules currently support length validation and regular expression validation.<br><br>Only applicable to Input and Password components. |


<span id="outputs"></span>
## Outputs

Outputs is used for configuring step output parameters and supports configuring multiple step output parameters. The following table describes the meaning and rules of each parameter in the output of every step.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Outputs can be referenced by downstream tasks. For details, refer to <a href="https://docs.byteplus.com/en/docs/cp/Deliver_pipeline_artifacts_through_the_output_of_custom_steps">Passing pipeline outputs through Custom steps using output</a>.</div>



|**Name** |**Required** |**Sample value** |**Descriptions** |
|---|---|---|---|
|name |Yes |bugs |Parameter name.<br><br>Supports English letters (uppercase and lowercase), numbers, and the "\-" hyphen; length must be between 2 and 50 characters. |
|displayName |Yes |Defect count |The parameter display name. Used to display the artifact name in pipeline run details; the name must not be empty or duplicated.<br><br>Supports uppercase and lowercase English letters, Chinese characters, numbers, and the hyphen (“\-”); length must be between 2 and 50. |
|type |Yes |string |Parameter type (defaults to string). |
|description |no |This is a piece of descriptive information. |Description information. Display a question mark next to displayName, and show the description when the question mark is hovered over.<br><br>Limited to 200 characters; supports uppercase and lowercase letters in both Chinese and English, as well as special characters. |
|defaultValue |no |1 |Default value. |


<span id=".56S65L6L"></span>
## Example:

The following YAML examples of various UI components and validation rules are presented to you.

<span id=".6L6T5YWl5qGGLWlucHV0"></span>
### Text box Input

```yaml
name: field1
displayName: 
type: string
defaultValue: custom step
required: true
uiConfig:
  type: Input
```


<span id=".5LiL5ouJ5Y2V6YCJ5qGGLXNlbGVjdA=="></span>
### Dropdown radio box: Select

```yaml
name: field2
displayName: 
type: string
defaultValue: b
required: true
uiConfig:
  type: Select
  dataSource:
    value:
      - label: a
        value: a
      - label: b
        value: b
```


<span id=".5aSN6YCJ5qGGLWNoZWNrYm94Z3JvdXA="></span>
### Check boxes CheckBoxGroup

```yaml
name: field3
displayName: 
type: array
required: true
defaultValue:
  - b
uiConfig:
  type: CheckBoxGroup
  dataSource:
    value:
      - label: a
        value: a
      - label: b
        value: b
      - label: c
        value: c
```


<span id=".5ZG95Luk6KGMLWNvZGVlZGl0b3I="></span>
### The command line CodeEditor

```yaml
name: field4
displayName: command
type: string
defaultValue: echo 'custom step'
required: true
uiConfig:
  type: CodeEditor
```


<span id=".5a-G56CB5qGGLXBhc3N3b3Jk"></span>
### Password field (Password)

```yaml
name: field5
displayName: 
type: string
defaultValue: 
required: true
uiConfig:
  type: Password
```


<span id=".5Zu65a6a5paH5pysLXRleHQ="></span>
### Fixed text text

```yaml
name: field6
displayName: 
type: string
defaultValue: 
required: true
uiConfig:
  type: Text
```


&nbsp;

<span id=".6ZW_5bqm5qCh6aqM"></span>
### Length validation

```yaml
- name: field1
  displayName: 
  type: string
  defaultValue: aaaa
  required: true
  uiConfig:
    type: Input
    validateRule:
      - max: 5
        min: 2
        message: 
```


<span id=".5q2j5YiZ5qCh6aqM"></span>
### Regular expression validation

```yaml
- name: field1
  displayName: 
  type: string
  defaultValue: aaaa
  required: true
  uiConfig:
    type: Input
    validateRule:
      - pattern: ^a
        message: 
```
