---
title: "Usage"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-usage"
---

This topic describes how to use the SDK for Go and provides sample codes to help you accelerate your development process.

<span id="f44e5318"></span>
## Prerequisites


* A BytePlus account or an IAM user. For more information, see [Signing up for a BytePlus account](https://docs.byteplus.com/en/byteplus-platform/docs/signing-up-your-account) or [Managing IAM users and roles](https://docs.byteplus.com/byteplus-livesaas/docs/managing-iam-users-and-roles).

* You have obtained the AccessKey ID (AK) and Secret Access Key (SK) for authentication.

   * To obtain the AK and SK of a BytePlus account, go to [BytePlus Live console](https://console.byteplus.com/livesaas/liveManagement/) \> User Profile \> **IAM** \> **Key management**.

   * To obtain the AK and SK of an IAM user, complete the following steps:

      1. Go to [BytePlus Live console](https://console.byteplus.com/livesaas/liveManagement/) \> User Profile \> **IAM** \> **Identity management** \> **User**.

      2. Find the user and then click **View details**.

      3. On the **Access key** tab, click **Create new access key**.


<span id="4111dac6"></span>
## Using SDK

Open the `BYTEPLUS-SDK-GOLANG` folder, enter the AK and SK in the `example\demo_livesaas\demo_livesaas_test.go` file.

```Go
package demo_livesaas

import (
        "encoding/json"
        livesaas "github.com/byteplus-sdk/byteplus-sdk-golang/service/livesaas"
        "net/url"
        "strconv"
        "testing"
        "time"
)

const (
        testAk = "your AK"
        testSk = "your SK"
)
```


<span id="9bd47893"></span>
## Sample codes

The following sample codes for using the SDK can help you accelerate your development process.

<span id="03938d30"></span>
### Creating a live\-streaming activity

For more information about the request and response parameters, see [CreateActivityAPIV2](https://docs.byteplus.com/byteplus-livesaas/docs/createactivityapiv2).

```Go
func TestLIVESAAS_CreateActivityAPIV2(t *testing.T) {
   live.DefaultInstance.Client.SetAccessKey(testAk)
   live.DefaultInstance.Client.SetSecretKey(testSk)
   bodyMap := map[string]interface{}{
      "CoverImage":      "your CoverImage",
      "OldId":           "your OldId",
      "CopyStream":      "your CopyStream",
      "LiveTime":        "your LiveTime",
      "Name":            "your Name",
      "ViewUrlPath":     "your ViewUrlPath",
      "TemplateId":      "your TemplateId",
      "SiteTags": []map[string]interface{}{
         {
            "Index": "your Index",
            "Value": "your Value",
         },
      },
      "TextSiteTags": []map[string]interface{}{
         {
            "Index": "your Index",
            "Value": "your Value",
         },
      },
      
   }
   // Serialize the request parameters
   body, _ := json.Marshal(bodyMap)
   // Print the request parameters
   t.Logf(string(body))
   // Call the API operation to create a live-streaming activity with the serialized request parameters
   resp, statusCode, err := live.DefaultInstance.CreateActivityAPIV2(nil, string(body))
   // If an error occurs while calling the API operation, print the error
   if err != nil {
      t.Logf("error occur %v", err)
   }
   // Serialize the response data
   res, _ := json.Marshal(resp)
   // Print the response data
   t.Logf("statusCode = %+v  msgInfo = %+v \n", statusCode, string(res))
}
```


<span id="f08aea45"></span>
### Updating basic configurations of a live\-streaming activity

For more information about the request and response parameters, see [UpdateActivityBasicConfigAPI](https://docs.byteplus.com/byteplus-livesaas/docs/updateactivitybasicconfigapi).

```Go
func TestLIVESAAS_UpdateActivityBasicConfigAPI(t *testing.T) {
   live.DefaultInstance.Client.SetAccessKey(testAk)
   live.DefaultInstance.Client.SetSecretKey(testSk)
   
   bodyMap := map[string]interface{}{
      "ActivityId":                "your ActivityId",
      "Name":                      "your Name",
      "LiveTime":                  "your LiveTime",
      "ColorThemeIndex":           "your ColorThemeIndex",
      "IsCoverImageEnable":        "your IsCoverImageEnable",
      "CoverImageUrl":             "your CoverImageUrl",
      "CoverImageUrlDefault":      "your CoverImageUrlDefault",
      "IsPcBackImageEnable":       "your IsPcBackImageEnable",
      "PcBackImageUrl":            "your PcBackImageUrl",
      "PcBackImageUrlDefault":     "your PcBackImageUrlDefault",
      "IsMobileBackImageEnable":   "your IsMobileBackImageEnable",
      "MobileBackImageUrl":        "your MobileBackImageUrl",
      "MobileBackImageUrlDefault": "your MobileBackImageUrlDefault",
      "IsPreviewVideoEnable":      "your IsPreviewVideoEnable",
      "PreviewVideoUrl":           "your PreviewVideoUrl",
      "PreviewVideoVid":           "your PreviewVideoVid",
      "PreviewVideoVidDefault":    "your PreviewVideoVidDefault",
      "IsPeopleCountEnable":       "your IsPeopleCountEnable",
      "IsHeaderImageEnable":       "your IsHeaderImageEnable",
      "HeaderImageUrl":            "your HeaderImageUrl",
      "IsWatermarkImageEnable":    "your IsWatermarkImageEnable",
      "WatermarkImageUrl":         "your WatermarkImageUrl",
      "IsThumbUpEnable":           "your IsThumbUpEnable",
      "ThumbUpUrl":                "your ThumbUpUrl",
      "ThumbUpUrlDefault":         "your ThumbUpUrlDefault",
      "IsShareIconEnable":         "your IsShareIconEnable",
      "ShareIconUrl":              "your ShareIconUrl",
      "ShareIconUrlDefault":       "your ShareIconUrlDefault",
      "IsCommentTranslateEnable":  "your IsCommentTranslateEnable",
      "Announcement":              "your Announcement",
      "IsAnnouncementEnable":      "your IsAnnouncementEnable",
      "BackgroundColor":           "your BackgroundColor",
      "InteractionColor":          "your InteractionColor",
      "FontColor":                 "your FontColor",
      "IsPCHeaderImageEnable":     "your IsPCHeaderImageEnable",
      "PCHeaderImageUrl":          "your PCHeaderImageUrl",
      "IsCountdownEnable":         "your IsCountdownEnable",
      "IsAutoStartEnable":         "your IsAutoStartEnable",
      "IsPageLimitEnable":         "your IsPageLimitEnable",
      "PageLimitType":             "your PageLimitType",
      "IsLanguageEnable":          "your IsLanguageEnable",
      "LanguageType":              []int32{"your LanguageType"},
      "SiteTags": []map[string]interface{}{
         {
            "Index": "your Index",
            "Value": "your Value",
         },
      },
      "AutoStartType":             "your AutoStartType",
      "IsPlayerTopEnable":         "your IsPlayerTopEnable",
      "PlayerTopType":             []int64{"your PlayerTopType"},
      "IsReplayAutoOnlineEnable":  "your IsReplayAutoOnlineEnable",
      "PreviewVideoId":            "your PreviewVideoId",
      "AccountId":                 "your AccountId",
      "PreviewVideoReviewStatus":  "your PreviewVideoReviewStatus",
      "DefaultSubtitleLanguage":   "your DefaultSubtitleLanguage",
      "SourceSubtitleLanguage":    "your SourceSubtitleLanguage",
      "OpenLiveAvextractorTask":   "your OpenLiveAvextractorTask",
      "IsTimeShift":               "your IsTimeShift",
      "PreviewVideoCoverImage":    "your PreviewVideoCoverImage",
      "PreviewVideoMediaName":     "your PreviewVideoMediaName",
      "IsPreviewPromptEnable":     "your IsPreviewPromptEnable",
      "PreviewPrompt":             "your PreviewPrompt",
      "IsReservationEnable":       "your IsReservationEnable",
      "ReservationTime":           "your ReservationTime",
      "ReservationText":           "your ReservationText",
      "WatermarkPosition":         "your WatermarkPosition",
      "IsReplayBulletChat":        "your IsReplayBulletChat",
      "PresenterChatColor":        "your PresenterChatColor",
      "IsLiveBulletChat":          "your IsLiveBulletChat",
      "IsBackgroundBlur":          "your IsBackgroundBlur",
      "FeedbackMessage":           "your FeedbackMessage",
      "IsFeedbackEnable":          "your IsFeedbackEnable",
      "IsThumbUpNumberEnable":     "your IsThumbUpNumberEnable",
      "SmsLanguage":               "your SmsLanguage",
      "MobileChatBackgroundColor": "your MobileChatBackgroundColor",
      "MobileBackgroundColor":     "your MobileBackgroundColor",
      "ConfigVersion":             "your ConfigVersion",
      "LiveZone":                  "your LiveZone",
      "RiskWarningSetting": map[string]interface{}{
         "IsRiskWarningEnable":   "your IsRiskWarningEnable",
         "RiskWarningTitle":      "your RiskWarningTitle",
         "RiskWarningContent":    "your RiskWarningContent",
         "RiskWarningButtonText": "your RiskWarningButtonText",
      },
      "TextSiteTags": []map[string]interface{}{
         {
            "Index": "your Index",
            "Value": "your Value",
         },
      },
      "IsSDKPlayEnable": "your IsSDKPlayEnable",
      "SDKPlayStatus":   "your SDKPlayStatus",
   }
   
   // Serialize the request parameters   
   body, _ := json.Marshal(bodyMap)
   // Print the request parameters
   t.Logf(string(body))
   // Call the API operation to update the basic configurations of a live-streaming activity with the serialized request parameters
   resp, statusCode, err := live.DefaultInstance.UpdateActivityBasicConfigAPI(nil, string(body))
   // If an error occurs while calling the API operation, print the error
   if err != nil {
      t.Logf("error occur %v", err)
   }
   // Serialize the response data
   res, _ := json.Marshal(resp)
   // Print the response data
   t.Logf("statusCode = %+v  msgInfo = %+v \n", statusCode, string(res))
}
```


<span id="367b7cb4"></span>
### Getting the list of all live\-streaming activities

For more information about the request and response parameters, see [ListActivityAPI](https://docs.byteplus.com/byteplus-livesaas/docs/listactivityapi).

```Go
func TestLIVESAAS_ListActivityAPI(t *testing.T) {
   live.DefaultInstance.Client.SetAccessKey(testAk)
   live.DefaultInstance.Client.SetSecretKey(testSk)
   bodyMap := map[string]interface{}{
       "PageNo":        "your PageNo",
       "PageItemCount": "your PageItemCount",
       "Name":          "your Name",
       "Status":        "your Status",
       "LiveTime":      "your LiveTime",
       "IsLockPreview": "your IsLockPreview",
       "SiteTagNews": map[string]interface{}{
          "Value": "your Value",
          "Name":  "your Name",
          "Index": "your Index",
       },
   }
   // Serialize the request parameters   
   body, _ := json.Marshal(bodyMap)
   // Print the request parameters
   t.Logf(string(body))
   // Call the API operation to get the list of all live-streaming activities with the serialized request parameters 
   resp, statusCode, err := live.DefaultInstance.ListActivityAPI(nil, string(body))
   // If an error occurs while calling the API operation, print the error
   if err != nil {
      t.Logf("error occur %v", err)
   }
   // Serialize the response data  
   res, _ := json.Marshal(resp)
   // Print the response data
   t.Logf("statusCode = %+v  msgInfo = %+v \n", statusCode, string(res))
}
```


<span id="6de038ab"></span>
### Getting the secret key for a live\-streaming activity

For more information about the request and response parameters, see [GetTemporaryLoginTokenAPI](https://docs.byteplus.com/byteplus-livesaas/docs/gettemporarylogintokenapi).

```Go
func TestLIVESAAS_GetTemporaryLoginTokenAPI(t *testing.T) {
   live.DefaultInstance.Client.SetAccessKey(testAk)
   live.DefaultInstance.Client.SetSecretKey(testSk)
   query := url.Values{}
   query.Set("ActivityId", "your ActivityId")
   
   // Print the request parameters
   t.Logf("ActivityId = %+v", query.Get("ActivityId"))
   // Call the API operation to get the secret key for a live-streaming activity with the serialized request parameters      
   resp, statusCode, err := live.DefaultInstance.GetTemporaryLoginTokenAPI(query)
   // If an error occurs while calling the API operation, print the error
   if err != nil {
      t.Logf("error occur %v", err)
   }
   // Serialize the response data   
   res, _ := json.Marshal(resp)
   // Print the response data
   t.Logf("statusCode = %+v  msgInfo = %+v \n", statusCode, string(res))
}
```


<span id="ee7deaf0"></span>
### Getting the authorization token of a Viewer SDK

For more information about the request and response parameters, see [GetSDKTokenAPI](https://docs.byteplus.com/en/byteplus-livesaas/docs/getsdktokenapi).

```Go
func TestLIVESAAS_GetSDKTokenAPI(t *testing.T) {
   live.DefaultInstance.Client.SetAccessKey(testAk)
   live.DefaultInstance.Client.SetSecretKey(testSk)

   bodyMap := map[string]interface{}{
      "ActivityId": "your ActivityId",
      "Mode":       "your Mode",
      "Nickname":   "your Nickname",
      "UserIdStr":  "your UserIdStr",
   }
   // Serialize the request parameters    
   body, _ := json.Marshal(bodyMap)
   // Print the request parameters
   t.Logf(string(body))
   // Call the API operation to get the authorization token of a Viewer SDK with the serialized request parameters         
   resp, statusCode, err := live.DefaultInstance.GetSDKTokenAPI(nil, string(body))
   // If an error occurs while calling the API operation, print the error
   if err != nil {
      t.Logf("error occur %v", err)
   }
   // Serialize the response data   
   res, _ := json.Marshal(resp)
   // Print the response data
   t.Logf("statusCode = %+v  msgInfo = %+v \n", statusCode, string(res))
}
```
