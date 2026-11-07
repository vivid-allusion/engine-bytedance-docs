---
title: "ListQuestionnaireAnswerDataAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-listquestionnaireanswerdataapi-zh-CN"
---

调用此 API 获取指定问卷的已提交答案，每次查询最多返回 10,000 条结果。

<span id="Request"></span>
## 请求

<span id="Details"></span>
### 详情


* API 操作：`ListQuestionnaireAnswerDataAPI`

* 请求方式：GET

* 请求 URI：`http://livesaas.byteplusapi.com/Action=ListQuestionnaireAnswerDataAPI&Version=2020-06-01`

* 配额：每个账号每分钟最多 120 次查询


<span id="Query string parameters"></span>
### 查询字符串参数

下表未包含所有通用请求参数。完整列表请参见[通用请求参数](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-parameters#f1706967)。


|**参数名称** |**是否必填** |**数据类型** |**接口行为** |
|---|---|---|---|
|Action |是 |字符串 |API 操作。 |
|Version |是 |字符串 |此 API 操作的版本。当前版本：`2020-06-01`。 |
|ActivityId |是 |整数 |直播活动的 ID。 |
|QuestionnaireId |是 |整数 |问卷 ID。 |
|PageNo |否 |整数 |返回结果的页码。使用此参数时，返回结果为分页数据。 |
|PageItemCount |否 |整数 |每页返回的结果数量。 |
|Source |是 |整数 |数据来源。更多详情请参见[按分段分析数据](https://docs.byteplus.com/en/byteplus-livesaas/docs/analyzing-data-with-segments)。<br><br><br>* \-1：全部<br><br>* 0：默认地址<br><br>* 1：地址 A<br><br>* 2：地址 B<br><br>* 3：地址 C<br><br>* 4：地址 D |


<span id="Sample request"></span>
### 请求示例

```JSON
Get http://livesaas.byteplusapi.com/Action=ListQuestionnaireAnswerDataAPI&Version=2020-06-01&ActivityId=1231231231&Soucre=0&QuestionnaireId=123
```


<span id="Response"></span>
## 返回调用结果

<span id="Response schema"></span>
### 返回结构


|**参数名称** |**数据类型** |**接口行为** |
|---|---|---|
|PageItemCount |整数 |每页返回的条目数量。 |
|PageNo |整数 |页码。 |
|TotalItemCount |整数 |问卷总数。 |
|Questions |数组 |问题描述。 |
|Questionnaires |数组 |问卷数据。 |


<span id="Question"></span>
#### 问题


|**参数名称** |**数据类型** |**接口行为** |
|---|---|---|
|QuestionId |整数 |问题 ID。 |
|Question |字符串 |问题描述。 |
|IsRequire |整数 |表示该问题是否为必填项：<br><br><br>* 0：可选<br><br>* 1：必填 |
|QuestionTag |字符串 |问题类型：<br><br><br>* blank_filling：填空题<br><br>* personal_info：个人信息<br><br>* select：多选题 |
|QuestionSubType |字符串 |问题子类型：<br><br><br>* phone_number：手机号<br><br>* email：邮箱<br><br>* nickname：昵称<br><br>* text：文本输入<br><br>* radio：单选题<br><br>* checkbox：可多选题 |
|Options |数组 |该问题的选项。 |


<span id="Option"></span>
#### 选项


|**参数名称** |**数据类型** |**接口行为** |
|---|---|---|
|OptionId |整数 |选项 ID。 |
|OptionName |字符串 |选项文本。 |


<span id="Questionnaire"></span>
#### 问卷


|**参数名称** |**数据类型** |**接口行为** |
|---|---|---|
|QuestionAnswers |数组 |问题的答案。 |
|SendTime |整数 |用户提交答案的时间戳。 |
|UserInfo |数组 |用户信息。 |


<span id="QuestionAnswer"></span>
#### 问题答案


|**参数名称** |**数据类型** |**接口行为** |
|---|---|---|
|QuestionId |整数 |问题 ID。 |
|Question |字符串 |问题描述。 |
|Answer |字符串 |问题的答案。 |


<span id="PlayUserInfo"></span>
#### PlayUserInfo


|**参数名称** |**数据类型** |**接口行为** |
|---|---|---|
|UserId |字符串 |用户 ID。 |
|NickName |字符串 |昵称。 |
|Extra |字符串 |用户信息。 |
|Telephone |字符串 |手机号。 |
|Email |字符串 |邮箱。 |
|Country |字符串 |国家。 |
|Province |字符串 |省份。 |


<span id="Sample response"></span>
### 返回示例

```JSON
{
     "ResponseMetadata" :{
         "RequestId":"202201201826170101501312091D1C09D2",
         "Action":"ListQuestionnaireAnswerDataAPI",
         "Version":"2020-06-01",
         "Service":"livesaas",
         "Region":"ap-singapore-1" 
    },
     "Result":{
          "PageItemCount":1,
          "PageNo":1,
          "TotalItemCount":1,
          "Questions":[
              {
                     "QuestionId":1, 
                     "Question":"a", 
                     "IsRequire":1, 
                     "QuestionTag":"blank_filling",
                     "QuestionSubTag:"text",
                     "Options": []
              }
          ],
          "Questionnaires":[
              {
                     "QuestionAnswers":[
                          {
                                "QuestionId": 1, 
                                "Question":"abc", 
                                "Answer":"bva" 
                          }
                     ],
                      "SendTime":1111,
                      "UserInfo": {
                          "UserId":12,
                          "NickName":"abv" 
                     }
               }
          ]
    }
}
```
