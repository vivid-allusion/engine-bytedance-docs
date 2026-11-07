---
title: "Fitness Assistant"
product: "BytePlus Effects"
product_code: "effects"
source: "https://docs.byteplus.com/en/docs/effects/docs-fitness-assistant"
---

<span id="C interface"></span>
# C interface

<span id="Function list"></span>
## Function list

<span id="1. Create handles for motion recognition"></span>
### 1. Create handles for motion recognition

```C
BEF_SDK_API bef_effect_result_t
bef_effect_ai_action_recognition_create(
        const char * model_path
        bef_effect_handle_t * handle
        );
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|model_path |const char \* |Model path |
|handle |bef_effect_handle_t \* |Create action recognition handle. |


**Return value: BEF_SDK_API bef_effect_result_t**

Return BEF_RESULT_SUC when succeed, and the corresponding error code when fail. For more details, refer to **bef_effect_ai_public_define.h**.

<span id="2. Destroy action recognition handles"></span>
### 2. Destroy action recognition handles

```C
BEF_SDK_API void
bef_effect_ai_action_recognition_destroy(
        bef_effect_handle_t handle
        );
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_effect_handle_t |Destroy the created action recognition handle. |


**Return value: BEF_SDK_API void**

<span id="3. Set motion recognition templates"></span>
### 3. Set motion recognition templates

```C
BEF_SDK_API bef_effect_result_t
bef_effect_ai_action_recognition_set_template(
        bef_effect_handle_t handle
        const char * template_path
        );
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_effect_handle_t |Created action recognition handle. |
|template_path |const char \* |Model path. |


**Return value: BEF_SDK_API bef_effect_result_t**

Return BEF_RESULT_SUC when succeed, and the corresponding error code when fail. For more details, refer to **bef_effect_ai_public_define.h**.

<span id="4. Action recognition: starting pose detection"></span>
### 4. Action recognition: starting pose detection

```C
BEF_SDK_API bef_effect_result_t
bef_effect_ai_action_recognition_start_pose_detect(
        bef_effect_handle_t handle
        const unsigned char * image
        bef_ai_pixel_format pixel_format
        int image_width
        int image_height
        int image_stride
        bef_ai_rotate_type orientation
        bef_ai_action_recognition_start_pose_type type
        bef_ai_action_recognition_start_pose_result * result
        );
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_effect_handle_t |Created action_recognition handle. Created skeleton handle. |
|image |const unsigned char \* |Image base address. Data pointer of the input image. |
|pixel_format |bef_ai_pixel_format |Pixel format of input image. Format of the input image. |
|image_width |int |Input image width, in pixels. |
|image_height |int |Input image height, in pixels. |
|image_stride |int |Input image stride in each row, in pixels. |
|orientation |bef_ai_rotate_type |Input image orientation. Refer to bef_rotate_type in **bef_effect_ai_public_define.h** |
|type |bef_ai_action_recognition_start_pose_type |Pose type. |
|result |bef_ai_action_recognition_start_pose_result \* |result |


**Return value: BEF_SDK_API bef_effect_result_t**

Return BEF_RESULT_SUC when succeed, and the corresponding error code when fail. For more details, refer to **bef_effect_ai_public_define.h**.

<span id="5. Action recognition counting"></span>
### 5. Action recognition counting

```C
BEF_SDK_API bef_effect_result_t
bef_effect_ai_action_recognition_count(
        bef_effect_handle_t handle
        const unsigned char * image
        bef_ai_pixel_format pixel_format
        int image_width
        int image_height
        int image_stride
        bef_ai_rotate_type orientation
        int confirm_time
        bef_ai_action_recognition_result * action_recognition_result
        );
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_effect_handle_t |Created action_recognition handle. Created skeleton handle. |
|image |const unsigned char \* |Image base address. Data pointer of the input image. |
|pixel_format |bef_ai_pixel_format |Pixel format of input image. Format of the input image. |
|image_width |int |Input image width, in pixels. |
|image_height |int |Input image height, in pixels. |
|image_stride |int |Input image stride in each row, in pixels. |
|orientation |bef_ai_rotate_type |Input image orientation. Refer to bef_rotate_type in **bef_effect_ai_public_define.h** |
|confirm_time |int |Count confirmation time. |
|action_recognition_result |bef_ai_action_recognition_result \* |No nullptr |


**Return value: BEF_SDK_API bef_effect_result_t**

Return BEF_RESULT_SUC when succeed, and the corresponding error code when fail. For more details, refer to **bef_effect_ai_public_define.h**.

<span id="6. Android authorization for body key points"></span>
### 6. Android authorization for body key points

```C
BEF_SDK_API bef_effect_result_t
bef_effect_ai_action_recognition_check_license(
        JNIEnv * env
        jobject context
        bef_effect_handle_t handle
        const char * licensePath
        );
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|env |JNIEnv \* |JNIEnv environment. |
|context |jobject |Android Context object. |
|handle |bef_effect_handle_t |Created action recognition handle. |
|licensePath |const char \* |licensePath. |


**Return value: BEF_SDK_API bef_effect_result_t**

Return BEF_RESULT_SUC when succeed, and BEF_RESULT_INVALID_LICENSE when license code is illegal. Return corresponding error codes for other failures. For more details, refer to **bef_effect_ai_public_define.h**.

<span id="7. iOS authorization for body key points"></span>
### 7. iOS authorization for body key points

```C
BEF_SDK_API bef_effect_result_t
bef_effect_ai_action_recognition_check_license(
        bef_effect_handle_t handle
        const char * licensePath
        );
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_effect_handle_t |Created action recognition handle. |
|licensePath |const char \* |License path. |


**Return value: BEF_SDK_API bef_effect_result_t**

Return BEF_RESULT_SUC when succeed, and BEF_RESULT_INVALID_LICENSE when license code is illegal. Return corresponding error codes for other failures. For more details, refer to **bef_effect_ai_public_define.h**.

<span id="8. Threshold adjustment"></span>
### 8. Threshold adjustment

The interface can adjust the threshold to achieve the effect of reducing the difficulty of recognition.

```C
BEF_SDK_API bef_effect_result_t
bef_effect_ai_action_recognition_set_template_threshold(bef_effect_handle_t handle, float threshold);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_effect_handle_t |Created action_recognition handle. |
|threshold |float |Threshold of template. |


**Return value:** 

Return BEF_RESULT_SUC when succeed, and BEF_RESULT_INVALID_LICENSE when license code is illegal. Return corresponding error codes for other failures. For more details, refer to **bef_effect_ai_public_define.h**.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">For more information on threshold ranges, refer to the<a href="https://docs.byteplus.com/effects/docs/fitness-assistant#appendix-threshold-adjustment-range"> appendix</a> in this doc.</div>


<span id="Structure"></span>
## Structure

<span id="1. bef_ai_action_recognition_result"></span>
### 1. bef_ai_action_recognition_result

Action counting results


|**Name** |**Type** |**Description** |
|---|---|---|
|keypoints |bef_ai_tt_key_point[BEF_AI_ACTION_RECOGNITION_MAX_POINT_NUM] |Bone info detected. |
|feed_body_part |bef_ai_action_recognition_feedback_body_part |Body part feedback. |
|feedback_keypoints |bef_ai_tt_key_point[BEF_AI_ACTION_RECOGNITION_MAX_POINT_NUM \*2] |Feedback of bone info detected. |
|feedback_kp_count |int |Number of feedback for bones detected. Actual length of feedback_keypoints. |
|recognize_succeed |bool |Whether the count is successful or not. For "true", it means that the count is successful, and you can increase the count on the interface. |
|is_feedback_valid |bool |Whether the feedback is valid or not. For "true", it means that the feedback is valid, and the feedback can be displayed on the interface. |


<span id="2. bef_ai_action_recognition_start_pose_result"></span>
### 2. bef_ai_action_recognition_start_pose_result

Initial pose detection results


|**Name** |**Type** |**Description** |
|---|---|---|
|is_detected |bool |Whether the initial pose detection has passed. For "true", it means that the detection has passed and you can start counting. |


<span id="Enumeration type"></span>
## Enumeration type

<span id="1. bef_ai_action_recognition_feedback_body_part"></span>
### 1. bef_ai_action_recognition_feedback_body_part

Body part feedback


|**Name** |**Description** |
|---|---|
|BEF_AI_ACTION_RECOGNITION_FeedbackNone | |
|BEF_AI_ACTION_RECOGNITION_FeedbackLeftArm |Left arm. |
|BEF_AI_ACTION_RECOGNITION_FeedbackRightArm |Right arm. |
|BEF_AI_ACTION_RECOGNITION_FeedbackLeftLeg |Left leg. |
|BEF_AI_ACTION_RECOGNITION_FeedbackRightLeg |Right leg. |


<span id="2. bef_ai_action_recognition_start_pose_type"></span>
### 2. bef_ai_action_recognition_start_pose_type

Initial pose category


|**Name** |**Description** |
|---|---|
|BEF_AI_ACTION_RECOGNITION_Stand |Stand. |
|BEF_AI_ACTION_RECOGNITION_Lying |Lie. |
|BEF_AI_ACTION_RECOGNITION_Sitting |Sitting posture. |


<span id="Macro definition"></span>
## Macro definition


|**Name** |**Value** |**Description** |
|---|---|---|
|BEF_AI_ACTION_RECOGNITION_MAX_POINT_NUM |18 |Maximum number of bone points. |


<span id="Java interface"></span>
# Java interface

<span id="com.bytedance.labcv.effectsdk.ActionRecognition"></span>
### com.bytedance.labcv.effectsdk.ActionRecognition

API action count

<span id="1. Initialization algorithm"></span>
### 1. Initialization algorithm

```Java
int
init(
        Context context
        String modelPath
        String licensePath
        );
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|context |Context |Android Context object. |
|modelPath |String |Model path. |
|licensePath |String |License file path. |


**Return value: int**

<span id="2. Set motion recognition templates"></span>
### 2. Set motion recognition templates

```Java
int
setTemplate(
        String templatePath
        );
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|templatePath |String |Model path. |


**Return value: int**

<span id="3. Action recognition: starting pose detection"></span>
### 3. Action recognition: starting pose detection

```Java
BefActionRecognitionInfo.PoseDetectResult
detectPose(
        ByteBuffer buffer
        BytedEffectConstants.PixlFormat pixelFormat
        int width
        int height
        int stride
        BefActionRecognitionInfo.ActionRecognitionPoseType poseType
        BytedEffectConstants.Rotation orientation
        );
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|buffer |ByteBuffer |Data. |
|pixelFormat |BytedEffectConstants.PixlFormat |Format. |
|width |int |Width. |
|height |int |Height. |
|stride |int |Image stride |
|poseType |BefActionRecognitionInfo.ActionRecognitionPoseType |Pose type. |
|orientation |BytedEffectConstants.Rotation |For image rotation direction, refer to Rotation for details. |


**Return value: BefActionRecognitionInfo. PoseDetectResult**

For pose detection results, refer to PoseDetectResult for details.

<span id="4. Action recognition counting"></span>
### 4. Action recognition counting

```Java
BefActionRecognitionInfo
detect(
        ByteBuffer buffer
        BytedEffectConstants.PixlFormat pixelFormat
        int width
        int height
        int stride
        BytedEffectConstants.Rotation orientation
        int confirmTime
        );
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|buffer |ByteBuffer |Data |
|pixelFormat |BytedEffectConstants.PixlFormat |Format |
|width |int |Width |
|height |int |Height |
|stride |int |Image stride |
|orientation |BytedEffectConstants.Rotation |For image rotation direction, refer to Rotation for details. |
|confirmTime |int |Confirm duration for counting |


**Return value: BefActionRecognitionInfo**

Action count results, refer to **BefActionRecognitionInfo** for details.

<span id="48435deb"></span>
### 5. Threshold adjustment

```Java
int
setThreshold(float threshold)
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|threshold |float |Threshold of template. |


**Return value:** 

Return algorithm threshold.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">For more information on threshold ranges, refer to the<a href="https://docs.byteplus.com/effects/docs/fitness-assistant#appendix-threshold-adjustment-range"> appendix</a> in this doc.</div>


<span id="6. Destruction algorithm"></span>
### 6. Destruction algorithm

```Java
void
destroy(
        );
```


**Return value: void**

<span id="com.bytedance.labcv.effectsdk.BefActionRecognitionInfo"></span>
### com.bytedance.labcv.effectsdk.BefActionRecognitionInfo

Action counting and detection results


|**Name** |**Type** |**Description** |
|---|---|---|
|keyPoints |BefPublicDefine.BefKeyPoint[] |Bone info detected |
|feedbackPart |int |Body part feedback |
|feedbackKeyPoints |BefPublicDefine.BefKeyPoint[] |Feedback of bone info detected |
|recognizeSucceed |boolean |Whether the count is successful or not. For "true", it means that the count is successful, and you can increase the count on the interface. |
|isFeedbackValid |boolean |Whether the feedback is valid or not. For "true", it means that the feedback is valid, and the feedback can be displayed on the interface. |


<span id="com.bytedance.labcv.effectsdk.BefActionRecognitionInfo.PoseDetectResult"></span>
### com.bytedance.labcv.effectsdk.BefActionRecognitionInfo.PoseDetectResult

Initial pose detection results


|**Name** |**Type** |**Description** |
|---|---|---|
|isDetected |boolean |Whether the initial pose detection has passed. For "true", it means that the detection has passed and you can start counting. |


<span id="com.bytedance.labcv.effectsdk.BefActionRecognitionInfo"></span>
### com.bytedance.labcv.effectsdk.BefActionRecognitionInfo

Action counting and detection results


|**Name** |**Type** |**Description** |
|---|---|---|
|keyPoints |BefPublicDefine.BefKeyPoint[] |Bone info detected |
|feedbackPart |int |Body part feedback |
|feedbackKeyPoints |BefPublicDefine.BefKeyPoint[] |Feedback of bone info detected |
|recognizeSucceed |boolean |Whether the count is successful or not. For "true", it means that the count is successful, and you can increase the count on the interface. |
|isFeedbackValid |boolean |Whether the feedback is valid or not. For "true", it means that the feedback is valid, and the feedback can be displayed on the interface. |


<span id="4d562a1e"></span>
# Appendix: Threshold adjustment range

**Android:** 


|**Action** |**Minimum Threshold** |**Maximum Threshold** |
|---|---|---|
|Jumping Jack |0.3 |0.5 |
|Squat |0.3 |0.48 |
|Plank |0.3 |0.55 |
|Push\-up |0.3 |0.52 |
|Sit\-up |0.3 |0.46 |
|High\-Knee run |0.3 |0.5 |
|Lunge |0.3 |0.5 |
|Hip Bridge |0.3 |0.49 |
|Jumping Lunge |0.3 |0.53 |
|Kneeling Push\-up |0.3 |0.52 |


**iOS：** 


|**Action** |**Minimum Threshold** |**Maximum Threshold** |
|---|---|---|
|Jumping Jack |0.3 |0.5 |
|Squat |0.3 |0.48 |
|Plank |0.3 |0.55 |
|Push\-up |0.3 |0.52 |
|Sit\-up |0.3 |0.46 |
|High\-Knee run |0.3 |0.5 |
|Lunge |0.3 |0.5 |
|Hip Bridge |0.3 |0.5 |
|Jumping Lunge |0.3 |0.52 |
|Kneeling Push\-up |0.3 |0.53 |
