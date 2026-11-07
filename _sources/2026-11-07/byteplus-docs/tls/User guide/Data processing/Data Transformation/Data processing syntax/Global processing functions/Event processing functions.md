---
title: "Event processing functions"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/event_processing_functions"
---

This topic describes the syntax and format of event processing functions and offers sample scenarios.

<span id="e-output-函数"></span>
## e_output function

This function outputs data to a target topic with a specified alias. The alias is the value of **Target name** specified when you create a transformation task.

<span id="函数语法-格式"></span>
### Function syntax and format

```python
e_output(topic="topic alias")
```


The following table describes the parameters.


|Parameter |Type |Required |Default Value |Value Range |Description |
|---|---|---|---|---|---|
|topic |String |Yes |/ |/ |Specify a topic alias. |


<span id="函数示例"></span>
### Sample function


* Scenario: The function judges whether to output a log to the topic with the alias target\-1 based on the value of the field `is_output` in the log.

* Transformation rule:

   ```python
   c_if(v("is_output"), e_output("target-1"))
   ```
   

* Sample log:

   ```json
   [
       {
           "is_output":1,
           "content":"hello world"
       },
       {
           "is_output":0,
           "content":"test content"
       }
   ]
   ```
   

* Transformation result:

   ```json
   [
       {
           "is_output":1,
           "content":"hello world"
       }
   ]
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The function outputs the first log to the topic with the alias target\-1 but it does not output the second log.   </div>
   

<span id="7d03500c"></span>
## e_auto_output function

This function distributes logs dynamically to different topics. For example, the value of the log field **service** is **tos** , **kafka** , you can specify the e_auto_output function to dynamically distribute the log to the topic named **tos** , **kafka** according to the value of the **service**. If the topic named **tos** and **kafka** do not exist, the system will create the topics first.

<span id="7b35bf6a"></span>
### Function syntax and format

```python
e_auto_output(project='projectname',topic='topicname',tags='tag',index='index')
```


The parameters are described as follows:

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">If projects or topics with the same name already exist, the system will not create them repeatedly.</div>


* <div data-tips="true" data-tips-type="tip">When dynamically creating projects or topics based on field values, the field values must conform to the resource naming requirements, otherwise an error will be reported when using the e_auto_output function. For detailed instructions, please refer to <a href="https://docs.byteplus.com/docs/tls/Limits#2c1ff6c3">Resource Naming Limit </a>.</div>




|Parameter |Type |Required |Default Value |Value Range |Description |
|---|---|---|---|---|---|
|project |String |Yes |/ |/ |Set the project name. |
|topic |String |Yes |/ |/ |Set the topic name. |
|tags |String |No |/ |/ |Set the topic tag as `key: value`, separated by a half\-width comma (,). For example, `tags = 'a: b, c: d'` means adding two sets of tags `a: b` and `c: d` for the topic. |
|index |String |No |full_text |full_text |Sets the indexes of the topic.<br><br><br>* full_text: enable full\-text indexes.<br><br>* Empty string: disable full\-text indexes. |


<span id="e2dbcf2f"></span>
### Sample function

Function example 1:


* Scenario: Extract the value from the **service** field, then dynamically distribute the log to the corresponding topic according to the value, and enable full\-text indexes for the topic. If the project and topic do not exist, the system creates them based on the values you specify in the function.

* Processing rules:

   ```python
   e_auto_output(project='myproject',topic=v('service'))
   ```
   

* Sample log:

   ```JSON
   // log 1
   {
     "service": "tos",
     "week": "Monday,Tuesday,Wednesday"
   }
   // log 2
   {
     "service": "kafka",
     "week": "Monday,Tuesday,Wednesday"
   }
   ```
   

* Processing result:

   * Distribute log 1 to the topic named **tos** under the project named **myproject**.

      ```JSON
      {
        "service": "tos",
        "week": "Monday,Tuesday,Wednesday"
      }
      ```
      

   * Distribute log 2 to the topic named **kafka** under the project named **myproject**.

      ```JSON
      {
        "service": "kafka",
        "week": "Monday,Tuesday,Wednesday"
      }
      ```
      


Function example 2:


* Scenario: Extract the value from the **project\-name** field and the **topic\-name** field, then distribute the log to the corresponding topic according to the value, and add labels `key1: value1` and `key2: value2` for the topic, and enable full\-text indexes. If the project and topic do not exist, the system creates them based on the values you specify in the function.

* Processing rules:

   ```python
   e_auto_output(v('project-name'),v('topic-name'),tags='key1:value1,key2:value2')
   ```
   

* Sample log:

   ```json
   // log 1
   {
     "project-name": "myproject01",
     "topic-name": "accesslog01",
     "week": "Monday,Tuesday,Wednesday"
   }
   // log 2
   {
     "project-name": "myproject02",
     "topic-name": "accesslog02",
     "week": "Monday,Tuesday,Wednesday"
   }
   ```
   

* Processing result:

   * Distribute log 1 to the topic named **accesslog01** under the project named **myproject01**, and add labels `key1: value1`, `key2: value2`, and enable full\-text indexes.

      ```JSON
      {
        "project-name": "myproject01",
        "topic-name": "accesslog01",
        "week": "Monday,Tuesday,Wednesday"
      }
      ```
      

   * Distribute log 1 to the topic named **accesslog02** under the project named **myproject02**, and add labels `key1: value1`, `key2: value2`, and enable full\-text indexes.

      ```JSON
      {
        "project-name": "myproject02",
        "topic-name": "accesslog02",
        "week": "Monday,Tuesday,Wednesday"
      }
      ```
      


Function example 3:


* Scenario: Extract the value from the **project\-name** field and **topic\-name** field, then distribute the log to the corresponding topic according to the value, and disable the full\-text indexes of the topic. If the project and topic do not exist, the system creates them based on the values you specify in the function.

* Processing rules:

   ```python
   e_auto_output(v('project-name'),v('topic-name'),index='')
   ```
   

* Sample log:

   ```json
   // log 1
   {
     "project-name": "myproject01",
     "topic-name": "accesslog01",
     "week": "Monday,Tuesday,Wednesday"
   }
   // log 2
   {
     "project-name": "myproject02",
     "topic-name": "accesslog02",
     "week": "Monday,Tuesday,Wednesday"
   }
   ```
   

* Processing result:

   * Distribute log 1 to the topic named **accesslog01** under the project named **myproject01** and disable full\-text indexes of the topic.

      ```JSON
      {
        "project-name": "myproject01",
        "topic-name": "accesslog01",
        "week": "Monday,Tuesday,Wednesday"
      }
      ```
      

   * Distribute log 1 to the topic named **accesslog02** under the project named **myproject02** and disable full\-text indexes of the topic.

      ```JSON
      {
        "project-name": "myproject02",
        "topic-name": "accesslog02",
        "week": "Monday,Tuesday,Wednesday"
      }
      ```
      


<span id="e-split-函数"></span>
## e_split function

This function uses a delimiter to split a specific field into multiple logs.

<span id="函数语法-格式"></span>
### Function syntax and format

```python
e_split(field, sep=",", quote='"', lstrip=Ture, jmes=None, output=None)
```


Splitting rules:


* Rule 1: If the **jmes** parameter is configured, the function converts the values of a log field into a JSON list, then uses the value extracted through a JMES expression as the value in the next step. In this case, the values specified for the sep and quote parameters do not take effect. If the **jmes** parameter is not specified, the function splits a field based on Rule 2.

* Rule 2: If the value obtained in the previous step is a list or a string in JSON list format, the function performs splitting according to the list and the processing ends. In this case, the values specified for the sep and quote parameters are invalid. If the obtained value is not a JSON list or JSON list string, the function splits your field according to Rule 3.

* Rule 3: The function uses **sep**, **quote**, and **lstrip** to parse the value obtained in the previous step into multiple values through CSV. Then, the function splits the parsed values and the processing ends.


The following table describes the parameters.


|Parameter |Type |Required |Default Value |Value Range |Description |
|---|---|---|---|---|---|
|field |String |Yes |/ |/ |Specify the name of a field to be split. |
|sep |String |No |， |/ |Specify a delimiter. |
|quote |String |No |" |/ |Specify a quote. |
|lstrip |Boolean |No |True |/ |Specify whether to remove spaces on the left of a value. The default value is True. This parameter only takes effect when your string is split. |
|jmes |String |No |None |/ |Convert field values into JSON objects, use a JMES expression to extract specific values, and perform splitting operations. |
|output |String |No |None |/ |Set a field name. By default, this name overwrites the existing fields in a log. |


<span id="函数示例"></span>
### Sample function


* Scenario: The function splits the values of the field `city` into multiple logs.

* Transformation rule:

   ```python
   e_split("city")
   ```
   

* Sample log:

   ```json
   {
       "content":"hello world",
       "city":"shanghai,hangzhou,chengdu"
   }
   ```
   

* Transformation result:

   ```json
   [
       {
           "content":"hello world",
           "city":"shanghai"
       },
       {
           "content":"hello world",
           "city":"hangzhou"
       },
       {
           "content":"hello world",
           "city":"chengdu"
       }
   ]
   ```
   


<span id="e-drop-函数"></span>
## e_drop function

This function discards logs that meet specific conditions.

<span id="函数语法-格式"></span>
### Function syntax and format

```python
e_drop(condition=conditions)
```


The following table describes the parameters.


|Parameter |Type |Required |Default Value |Value Range |Description |
|---|---|---|---|---|---|
|condition |Boolean |No |True |/ |Specify whether to discard a log. |


<span id="函数示例"></span>
### Sample function


* Scenario: The function judges whether to discard a log based on the value of the log field `city`.

* Transformation rule:

   ```python
   c_if(op_eq(v("city"), "shanghai"), e_drop())
   ```
   

* Sample log:

   ```json
   [
       {
           "content":"hello world",
           "city":"shanghai"
       },
       {
           "content":"hello world",
           "city":"hangzhou"
       }
   ]
   ```
   

* Transformation result:

   ```json
   {
       "content":"hello world",
       "city":"hangzhou"
   }
   ```
   


<span id="e-keep-函数"></span>
## e_keep function

This function retains logs that meet specific conditions.

<span id="函数语法-格式"></span>
### Function syntax and format

```python
e_keep(condition=conditions)
```


The following table describes the parameters.


|Parameter |Type |Required |Default Value |Value Range |Description |
|---|---|---|---|---|---|
|condition |Boolean |No |True |/ |Specify whether to retain a log. |


<span id="函数示例"></span>
### Sample function


* Scenario: The function judges whether to retain a log based on the value of the log field `city`.

* Transformation rule:

   ```python
   c_if(op_eq(v("city"), "shanghai"), e_keep())
   ```
   

* Sample log:

   ```json
   [
       {
           "content":"hello world",
           "city":"shanghai"
       },
       {
           "content":"hello world",
           "city":"hangzhou"
       }
   ]
   ```
   

* Transformation result:

   ```json
   {
       "content":"hello world",
       "city":"shanghai"
   }
   ```
