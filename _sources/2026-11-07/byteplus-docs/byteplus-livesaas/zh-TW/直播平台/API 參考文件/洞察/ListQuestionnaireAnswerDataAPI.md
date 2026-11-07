---
title: "ListQuestionnaireAnswerDataAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-listquestionnaireanswerdataapi-zh-TW"
---

呼叫此 API 以取得特定問卷的提交答案，每次查詢最多可獲得 10,000 答案。

<span id="Request"></span>
## 請求

<span id="Details"></span>
### 詳細資訊


* API 操作：`ListQuestionnaireAnswerDataAPI`

* 請求方法：GET

* 請求 URI：`http://livesaas.byteplusapi.com/Action=ListQuestionnaireAnswerDataAPI&Version=2020-06-01`

* 配額：每個帳戶每分鐘最多 120 次查詢


<span id="Query string parameters"></span>
### 查詢字串參數

下表未包含所有共用請求參數。完整列表請參閱 [共用請求參數](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-parameters#f1706967)。


|**參數名稱** |**必填** |**資料型態** |**說明** |
|---|---|---|---|
|Action |是 |字串 |API 操作。 |
|Version |是 |字串 |此 API 操作的版本。目前版本：`2020-06-01`。 |
|ActivityId |是 |整數 |直播活動的 ID。 |
|QuestionnaireId |是 |整數 |問卷 ID。 |
|PageNo |否 |整數 |要返回結果的頁碼。使用此參數時，回應將進行分頁。 |
|PageItemCount |否 |整數 |每頁返回的結果數量。 |
|Source |是 |整數 |資料來源。更多詳細資訊請參閱 [以分段分析資料](https://docs.byteplus.com/en/byteplus-livesaas/docs/analyzing-data-with-segments)。<br><br><br>* \-1：全部<br><br>* 0：預設地址<br><br>* 1：地址 A<br><br>* 2：地址 B<br><br>* 3：地址 C<br><br>* 4：地址 D |


<span id="Sample request"></span>
### 範例請求

```JSON
Get http://livesaas.byteplusapi.com/Action=ListQuestionnaireAnswerDataAPI&Version=2020-06-01&ActivityId=1231231231&Soucre=0&QuestionnaireId=123
```


<span id="Response"></span>
## 回應

<span id="Response schema"></span>
### 回應結構


|**參數名稱** |**資料型態** |**說明** |
|---|---|---|
|PageItemCount |整數 |每頁返回的項目數。 |
|PageNo |整數 |頁碼。 |
|TotalItemCount |整數 |問卷總數。 |
|Questions |陣列 |問題描述。 |
|Questionnaires |陣列 |問卷資料。 |


<span id="Question"></span>
#### 問題


|**參數名稱** |**資料型態** |**說明** |
|---|---|---|
|QuestionId |整數 |問題 ID。 |
|Question |字串 |問題描述。 |
|IsRequire |整數 |表示此問題是否必填：<br><br><br>* 0：選填<br><br>* 1：必填 |
|QuestionTag |字串 |問題類型：<br><br><br>* blank_filling：填空題<br><br>* personal_info：個人資訊<br><br>* select：多選題 |
|QuestionSubType |字串 |問題子類型：<br><br><br>* phone_number：電話號碼<br><br>* email：電子郵件<br><br>* nickname：暱稱<br><br>* text：文字輸入<br><br>* radio：單選題<br><br>* checkbox：可選一個或多個選項的多選題 |
|Options |陣列 |此問題的選項。 |


<span id="Option"></span>
#### 選項


|**參數名稱** |**資料型態** |**說明** |
|---|---|---|
|OptionId |整數 |選項 ID。 |
|OptionName |字串 |選項文字。 |


<span id="Questionnaire"></span>
#### 問卷


|**參數名稱** |**資料型態** |**說明** |
|---|---|---|
|QuestionAnswers |陣列 |問題的答案。 |
|SendTime |整數 |使用者提交答案的時間戳。 |
|UserInfo |陣列 |使用者資訊。 |


<span id="QuestionAnswer"></span>
#### 問題答案


|**參數名稱** |**資料型態** |**說明** |
|---|---|---|
|QuestionId |整數 |問題 ID。 |
|Question |字串 |問題描述。 |
|Answer |字串 |問題的答案。 |


<span id="PlayUserInfo"></span>
#### PlayUserInfo


|**參數名稱** |**資料型態** |**說明** |
|---|---|---|
|UserId |字串 |使用者 ID。 |
|NickName |字串 |暱稱。 |
|Extra |字串 |使用者資訊。 |
|Telephone |字串 |電話號碼。 |
|Email |字串 |電子郵件。 |
|Country |字串 |國家。 |
|Province |字串 |省份。 |


<span id="Sample response"></span>
### 範例回應

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
