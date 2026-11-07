---
title: "Upload SDK error codes"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-upload-sdk-error-codes"
---

To quickly diagnose and resolve issues when using the Upload SDK, this guide provides a comprehensive list of common SDK and gateway error codes. You can use this reference to understand the meaning of each error and find corresponding troubleshooting solutions.

<span id="812027a5"></span>
## SDK error codes


|**Error code** |**Enum** |**Description** |
|---|---|---|
|\-60000 |ResponeParseFailed |The HTTP body was invalid, and the SDK failed to parse the JSON data as expected. This may be caused by network interception. |
|\-59999 |ResponeIsEmpty |The network request was not sent. Possible reasons include no network connection. It is recommended to switch networks. |
|\-39996 |OpenFileError |The SDK failed to open the file. Possible reasons include:<br><br><br>* The file was not found.<br><br>* The file size is 0.<br><br>* Android Q permission issues.<br><br>* Incorrect file path on iOS. |
|\-39991 |EXternCrcIsNotMatch |When uploading the segments of a large file, the CRC (Cyclic Redundancy Check) of the segments failed. This may be caused by network interception. |
|\-39987 |UserCancelCode |The upload was canceled by the user using the `stop` method. |
|\-39982 |GenSignatureFailed |STS2 signature error. Check if the Access Key (AK), Secret Key (SK), Session Token, and Space Name are set correctly. |
|\-39977 |FilePathisNull |The file path for uploading was not set. |
|\-39970 |InvalidHttpCode |The HTTP code was not 200. Refer to the gateway error codes below for specific reasons. |
|\-39968 |DiskResumeFileNotMatch |The file being uploaded for resumable upload does not match the previous upload. |


<span id="95335014"></span>
## Gateway error codes


|**Error Code** |**Status Code** |**Error Code Name** |**Error Code Meaning** |
|---|---|---|---|
|100003 |401 |MissingAuthenticationToken |Necessary authentication information was missing. |
|100005 |401 |MissingSignature |Missing signature. |
|100006 |403 |InvalidTimestamp |The request expired or the timestamp in the request was in the future. |
|100009 |401 |InvalidAccessKey |The Access Key (AK) is invalid. Please check the AK. |
|100010 |401 |SignatureDoesNotMatch |The signature was incorrect. |
|100012 |403 |LackPolicy |The request was made by a sub\-account without the required permissions. |
|100013 |403 |AccessDenied |The operation was performed by a sub\-account without the required permissions. |
|100018 |429 |FlowLimitExceeded |The request frequency exceeded the limit. |
|100024 |400 |InvalidAuthorization |Incorrect format for the `Authorization` header. Please check the `Authorization` parameter. |
|100025 |400 |InvalidCredential |Incorrect format for the `Credential` parameter in the `Authorization` header. Please check the `Credential` parameter. |
|100026 |401 |InvalidSecretToken |Invalid STS2 Token. |
