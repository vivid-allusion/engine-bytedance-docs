---
title: "Error Code Table"
product: "BytePlus Effects"
product_code: "effects"
source: "https://docs.byteplus.com/en/docs/effects/docs-error-code-table"
---

<span id="Overview"></span>
## Overview

In case of a license failure, invalid settings, or any other exception, the SDK will return an error code to help you identify the issue.

<span id="Error Codes"></span>
## Error Codes


|**Event** |**Code** |**Description** |**Solution** |
|---|---|---|---|
|BEF_RESULT_SUC |0 |Success. |No action is required. |
|BEF_RESULT_FAIL |\-1 |Internal error. |Check the other error logs at the top of the log. |
|BEF_RESULT_FILE_NOT_FIND |\-2 |File not found. |Check whether the file path in the code is correct. |
|BEF_RESULT_INVALID_INTERFACE |\-3 |Invalid interface. |The API is reserved. Check whether the function is available in the SDK. |
|BEF_RESULT_FILE_OPEN_FAILED |\-4 |Failed to open file. |Check whether the file exists and whether you have read and write access to the target file. |
|BEF_RESULT_INVALID_EFFECT_HANDLE |\-5 |Invalid effect handle. |Check whether it has been successfully initialized. |
|BEF_RESULT_INVALID_EFFECT_MANAGER |\-6 |Invalid EffectManager. |Check whether it has been successfully initialized. |
|BEF_RESULT_INVALID_FEATURE_HANDLE |\-7 |Invalid feature handle. |Check whether it has been successfully initialized. |
|BEF_RESULT_INVALID_FEATURE |\-8 |Invalid feature. |Check whether it has been successfully initialized. |
|BEF_RESULT_INVALID_RENDER_MANAGER |\-9 |Invalid RenderManager. |Check whether it has been successfully initialized. |
|BEF_RESULT_INVALID_ALGORITHM_RESULT |\-11 |Algorithm detection not executed. |This error may occur when special effects such as beautification are not configured. It can be ignored in most cases. |
|BEF_RESULT_INVALID_ALG_FACE_RES |\-12 |Invalid face detection result. |The special effects algorithm does not detect a valid face. |
|BEF_RESULT_ALG_FACE_106_CREATE_FAIL |\-22 |Failed to create the 106 face keypoints detection algorithm. |Check whether the license and model are valid. |
|BEF_RESULT_ALG_FACE_280_CREATE_FAIL |\-23 |Failed to create the 280 face keypoints detection algorithm. |Check whether the license and model are valid. |
|BEF_RESULT_ALG_FACE_PREDICT_FAIL |\-24 |Face attribute prediction failed. |Check whether the input image is correct. |
|BEF_RESULT_ALG_HAND_CREATE_FAIL |\-26 |Failed to create the hand gesture detection algorithm. |Check whether the license and model are valid. |
|BEF_RESULT_ALG_HAND_PREDICT_FAIL |\-27 |Hand gesture prediction failed. |Check whether the input image is correct. |
|BEF_RESULT_INVALID_TEXTURE |\-36 |Invalid texture. |Check whether the input texture is correct. |
|BEF_RESULT_INVALID_IMAGE_DATA |\-37 |Invalid image data. |Check whether the input buffer is correct. |
|BEF_RESULT_INVALID_IMAGE_FORMAT |\-38 |Invalid image format. |Check whether the format of the input image meets the requirements. |
|BEF_RESULT_INVALID_PARAM_TYPE |\-39 |Invalid parameter type. |Check whether the input parameter meets the requirements. |
|BEF_RESULT_INVALID_RESOURCE_VERSION |\-40 |Invalid resource version. |Check whether the resource file is correct. |
|BEF_RESULT_INVALID_PARAM_VALUE |\-47 |Invalid parameter value. |Check whether the input parameter meets the requirements. |
|BEF_RESULT_SMASH_E_INTERNAL |\-101 |Undefined internal error. |Please contact technical support. |
|BEF_RESULT_SMASH_E_NOT_INITED |\-102 |Uninitialized related resources. |Please contact technical support. |
|BEF_RESULT_SMASH_E_MALLOC |\-103 |Memory application failed. |Please contact technical support. |
|BEF_RESULT_SMASH_E_INVALID_PARAM |\-104 |Invalid parameter. |Check whether the input parameter meets the requirements. |
|BEF_RESULT_SMASH_E_ESPRESSO |\-105 |Espresso error. |Please contact technical support. |
|BEF_RESULT_SMASH_E_MOBILECV |\-106 |MobileCV error. |Please contact technical support. |
|BEF_RESULT_SMASH_E_INVALID_CONFIG |\-107 |Invalid configuration. |Check whether the path of the input license file is correct and whether the license file is damaged. |
|BEF_RESULT_SMASH_E_INVALID_HANDLE |\-108 |Invalid handle. |Check whether the path of the input license file is correct and whether the license file is damaged. |
|BEF_RESULT_SMASH_E_INVALID_MODEL |\-109 |Invalid model. |Check whether the path of the input model file is correct and whether the model file is damaged. |
|BEF_RESULT_SMASH_E_INVALID_PIXEL_FORMAT |\-110 |Invalid image format. |Check whether the SDK supports the format of the input image. |
|BEF_RESULT_SMASH_E_INVALID_POINT |\-111 |Invalid point. |Check whether the input or output variable of the API is null. |
|BEF_RESULT_SMASH_E_REQUIRE_FEATURE_NOT_INIT |\-112 |Uninitialized dependent module. |Please contact technical support. |
|BEF_RESULT_SMASH_E_NOT_IMPL |\-113 |Invalid interface. |Check whether the function name and parameter called are correct. |
|BEF_RESULT_INVALID_LICENSE |\-114 |Invalid license. |Check whether the path of the license file is correct and whether the model file is damaged. |
|BEF_RESULT_NULL_BUNDLEID |\-115 |Null application ID/bundle ID. |Check whether the input application ID/bundle ID is null. |
|BEF_RESULT_LICENSE_STATUS_INVALID |\-116 |Invalid license file. |Check whether the license file is correct. |
|BEF_RESULT_LICENSE_STATUS_EXPIRED |\-117 |License file expired. |Check whether the license file is correct and whether it needs to be updated. |
|BEF_RESULT_LICENSE_STATUS_NO_FUNC |\-118 |Mismatched request function. |Check whether the function has been purchased. |
|BEF_RESULT_LICENSE_STATUS_ID_NOT_MATCH |\-119 |Mismatched application ID/bundle ID. |Check whether the application ID/bundle ID in the license file is the same as the application ID/bundle ID of the app. |
|BEF_RESULT_LICENSE_BAG_NULL_PATH |\-120 |Null path of license package. |Check whether the path of the license file is correct. |
|BEF_RESULT_LICENSE_BAG_INVALID_PATH |\-121 |Incorrect path of license package. |Check whether the path input in the SDK is correct. |
|BEF_RESULT_LICENSE_BAG_TYPE_NOT_MATCH |\-122 |Mismatched license package type. |Check whether the license file is correct and whether it is damaged. |
|BEF_RESULT_LICENSE_BAG_INVALID_VERSION |\-123 |Invalid version. |Check whether the license file of an earlier version is used. |
|BEF_RESULT_LICENSE_BAG_INVALID_BLOCK_COUNT |\-124 |Invalid data block. |Check whether the license file is correct and whether it is damaged. |
|BEF_RESULT_LICENSE_BAG_INVALID_BLOCK_LEN |\-125 |Invalid data block length. |Check whether the license file is correct and whether it is damaged. |
|BEF_RESULT_LICENSE_BAG_INCOMPLETE_BLOCK |\-126 |Incomplete data block. |Check whether the license file is correct and whether it is damaged. |
|BEF_RESULT_LICENSE_BAG_UNAUTHORIZED_FUNC |\-127 |Unauthorized function. |Check whether the function has been purchased. |
|BEF_RESULT_SDK_FUNC_NOT_INCLUDE |\-128 |Function unavailable in the SDK. |The function called is unavailable in the SDK. |
|BEF_RESULT_LICENSE_BAG_INVALID_SUB_FUNC |\-129 |Invalid subfunction. |The certificate is incorrect. Please contact technical support. |
|BEF_RESULT_GL_ERROR_OCCUR |\-150 |OpenGL error. |Check whether the API is called in the OpenGL thread. |
|BEF_RESULT_GL_CONTECT |\-151 |Invalid GL context. |Check whether the GL context is correct. |
|BEF_RESULT_GL_TEXTURE |\-152 |Invalid GL texture. |Check whether the GL texture ID is valid. |


<span id="Common Error Codes for Online Licensing (for Windows, macOS, and Linux)"></span>
## Common Error Codes for Online Licensing (for Windows, macOS, and Linux)


|**Code** |**Message** |**Description** |
|---|---|---|
|47824 |invalid request body |Non\-JSON or incomplete request. Check whether content\-type is application/json or whether the json field exists. |
|47825 |illegal API key |Check whether the key value is correct. |
|47826 |broken message |Signature verification failed. Check the signature generation logic, and check whether secret is correct. |
|47829 |invalid business |The business has been closed or deactivated. Please contact business personnel. |
|47830 |insufficient funds |No more licensed devices are available. Please contact business personnel. |
|47831 |business expired |The business has expired. Please contact business personnel. |
|47832 |illegal authMsg |authMsg is damaged. Check whether it is corrupted. |
|47837 |request expired |The request timestamp has expired. Check whether the system time is correct. |
|47835 |client not found |Invalid account. Please contact business personnel. |
|47836 |database query error |Database error. This is an internal error. Please contact technical support. |
|765185 |The license does not support this package's name |Online licenses that take the form of a device name plus a package name, this error indicates that the license does not support this package name. |
