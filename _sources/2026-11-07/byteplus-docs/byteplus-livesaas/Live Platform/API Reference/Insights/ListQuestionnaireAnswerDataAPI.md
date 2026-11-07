---
title: "ListQuestionnaireAnswerDataAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-listquestionnaireanswerdataapi"
---

Call this API to get the submitted answers for a specific questionnaire, with a maximum of 10,000 results per query.

<span id="Request"></span>
## Request

<span id="Details"></span>
### Details


* API operation: `ListQuestionnaireAnswerDataAPI`

* Request method: GET

* Request URI: `http://livesaas.byteplusapi.com/Action=ListQuestionnaireAnswerDataAPI&Version=2020-06-01`

* Quota: 120 queries per minute per account


<span id="Query string parameters"></span>
### Query string parameters

Not all shared request parameters are included in the following table. For a complete list, see [Shared request parameters](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-parameters#f1706967).


|**Parameter Name** |**Required** |**Data Type** |**Description** |
|---|---|---|---|
|Action |Yes |String |API operation. |
|Version |Yes |String |The version of this API operation. Current version: `2020-06-01`. |
|ActivityId |Yes |Integer |ID of the live\-streaming activity. |
|QuestionnaireId |Yes |Integer |Questionnaire ID. |
|PageNo |No |Integer |The page number of the results to return. When you use this parameter, the response is paginated. |
|PageItemCount |No |Integer |The number of results to return per page. |
|Source |Yes |Integer |Data source. For more details, refer to [Analyzing data with segments](https://docs.byteplus.com/en/byteplus-livesaas/docs/analyzing-data-with-segments).<br><br><br>* \-1: All<br><br>* 0: Default address<br><br>* 1: Address A<br><br>* 2: Address B<br><br>* 3: Address C<br><br>* 4: Address D |


<span id="Sample request"></span>
### Sample request

```JSON
Get http://livesaas.byteplusapi.com/Action=ListQuestionnaireAnswerDataAPI&Version=2020-06-01&ActivityId=1231231231&Soucre=0&QuestionnaireId=123
```


<span id="Response"></span>
## Response

<span id="Response schema"></span>
### Response schema


|**Parameter Name** |**Data Type** |**Description** |
|---|---|---|
|PageItemCount |Integer |Number of returned items on each page. |
|PageNo |Integer |Page number. |
|TotalItemCount |Integer |Total number of questionnaires. |
|Questions |Array |Question description. |
|Questionnaires |Array |Questionnaire data. |


<span id="Question"></span>
#### Question


|**Parameter Name** |**Data Type** |**Description** |
|---|---|---|
|QuestionId |Integer |Question ID. |
|Question |String |Question description. |
|IsRequire |Integer |Indicates whether the question is required:<br><br><br>* 0: Optional<br><br>* 1: Required |
|QuestionTag |String |Question type:<br><br><br>* blank_filling: Fill\-in\-the\-blank questions<br><br>* personal_info: Personal information<br><br>* select: Multiple choice question |
|QuestionSubType |String |Subtype of the question:<br><br><br>* phone_number: Phone number<br><br>* email: Email<br><br>* nickname: Nickname<br><br>* text: Text input<br><br>* radio: A single\-choice question<br><br>* checkbox: A multiple\-choice question that allows for one or more selections |
|Options |Array |The options for the question. |


<span id="Option"></span>
#### Option


|**Parameter Name** |**Data Type** |**Description** |
|---|---|---|
|OptionId |Integer |Option ID. |
|OptionName |String |The text of the option. |


<span id="Questionnaire"></span>
#### Questionnaire


|**Parameter Name** |**Data Type** |**Description** |
|---|---|---|
|QuestionAnswers |Array |Answers to a question. |
|SendTime |Integer |The timestamp when the user submitted the answer. |
|UserInfo |Array |User information. |


<span id="QuestionAnswer"></span>
#### QuestionAnswer


|**Parameter Name** |**Data Type** |**Description** |
|---|---|---|
|QuestionId |Integer |Question ID. |
|Question |String |Question description. |
|Answer |String |Answers to a question. |


<span id="PlayUserInfo"></span>
#### PlayUserInfo


|**Parameter Name** |**Data Type** |**Description** |
|---|---|---|
|UserId |String |User ID. |
|NickName |String |Nickname. |
|Extra |String |User information. |
|Telephone |String |Phone number. |
|Email |String |Email. |
|Country |String |Country. |
|Province |String |Province. |


<span id="Sample response"></span>
### Sample response

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
