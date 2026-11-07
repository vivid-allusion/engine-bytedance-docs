---
title: "SLAM Algorithm"
product: "BytePlus Effects"
product_code: "effects"
source: "https://docs.byteplus.com/en/docs/effects/docs-slam-algorithm"
---

Horizontal plane tracking algorithm (e.g., tabletop, ground) for spatial localization of scenes with horizontal planes, suitable for general AR placement props, and for combining with other CV algorithms.

<span id="f114f525"></span>
# Technical Specifications

Require a phone with a gyroscope.

The recognition speed of slam algorithm will also be different under two different scenes: the spatial scene range is small when the camera moves back and forth, and the construction speed is relatively faster; the 3\-dimensional spatial scene corresponding to the camera rotation is relatively larger when the camera moves left and right, and the 3\-dimensional spatial construction speed becomes relatively slower.

<span id="64f944be"></span>
# C API

For the detailed interface description, refer to the header file：bef_effect_ai_slam.h

<span id="1. Initialize Camera Parameters"></span>
## 1. Initialize Camera Parameters

```C
BEF_SDK_API bef_effect_result_t
bef_ai_slam_init_camera_info(bef_ai_slam_camera_info* info);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|info |bef_ai_slam_camera_info \* |Initialize camera. |


**Return value:** 

Return BEF_RESULT_SUC if succeed, or return error code.

<span id="8912b19e"></span>
## 2. Initialize the SLAM algorithm

```C
BEF_SDK_API bef_effect_result_t
bef_effect_ai_slam_create(bef_ai_slam_handle *handle,
    const char* deviceName,
    const char* modelPath,
    bef_ai_slam_camera_info* camera, 
    bef_ai_slam_imu_info imu,
    bef_ai_slam_version version);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_ai_slam_handle |SLAM algorithm handle. |
|modelPath |const char \* |SLAM algorithm model path. |
|deviceName |const char \* |Device name. |
|Camera |bef_ai_slam_camera_info |Camera parameter after camera initilization. |
|imu |bef_ai_slam_imu_info |IMU attributes setting. |
|version |bef_ai_slam_version |SLAM version. |


**Return value:** 

Return BEF_RESULT_SUC if succeed, or return error code.

<span id="e5c33a9f"></span>
## 3. Authentication

```C
//Offline
BEF_SDK_API bef_effect_result_t
bef_effect_ai_slam_check_license(
    bef_ai_slam_handle handle,
    const char* licensePath);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_ai_slam_handle |SLAM algorithm handle. |
|licensePath |const char \* |License path. |


**Return value:** 

Return BEF_RESULT_SUC if succeed, or return error code.

<span id="1a2d2b97"></span>
## 4. IMU thread inputs IMU information

```C
//ios:
BEF_SDK_API bef_effect_result_t
bef_effect_ai_slam_set_imuinfo(bef_ai_slam_handle handle, 
    const bef_ai_slam_imu_data* imuData);

//android:
BEF_SDK_API bef_effect_result_t
bef_effect_ai_slam_set_detail_imuinfo(bef_ai_slam_handle handle, bef_ai_slam_imu_data_type type,
    double x, double y, double z,
    double timeStamp);
BEF_SDK_API bef_effect_result_t
bef_effect_ai_slam_set_rotation_vector(bef_ai_slam_handle handle,
    const double rb[9], double timeStamp);
```


**Parameters**:


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_ai_slam_handle |SLAM algorithm handle. |
|data |bef_ai_slam_imu_data\* |IMU data. |
|type |bef_ai_slam_imu_data_type\* |IMU data type. |
|x |double |x. |
|y |double |y. |
|z |double |z. |
|timeStamp |double |IMU data timestamp. |
|rb |double \* |Rotation matrix. |


**Return value:** 

Return BEF_RESULT_SUC if succeed, or return error code.

<span id="ff0c59ea"></span>
## 5.Obtain Camera Internal Parameters

```C
BEF_SDK_API bef_effect_result_t
bef_effect_ai_slam_get_intrinsic(bef_ai_slam_handle, 
    int width, int height, 
    bef_ai_slam_camera_intrinsic* intrinsic);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_ai_slam_handle |SLAM algorithm handle. |
|Width |int |Image buffer width. |
|Height |int |Image buffer height. |
|intrinsic |bef_ai_slam_camera_intrinsic \* |Camera intrinsic parameter. |


**Return value**:

Return BEF_RESULT_SUC if succeed, or return error code.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Construct Projection matrix when rendering using camera intrinsic parameters (executed only once)</div>


<div data-tips="true" data-tips-type="warning">Perspective matrix parameter description:</div>


<div data-tips="true" data-tips-type="warning">Camera internal parameter: Focus length on axis x & y (fx, fy); Center on axis x & y (cx, cy);</div>


<div data-tips="true" data-tips-type="warning">Image width & height (w, h); Depth of far & near plane (zF, zN).</div>


<div data-tips="true" data-tips-type="warning"><img src="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/doc-center/c77abec-.png" /></div>


<span id="9f5143c7"></span>
## 6. SLAM Processes Camera Pose

```C
BEF_SDK_API bef_effect_result_t
bef_effect_ai_slam_detect(bef_ai_slam_handle handle,
    const unsigned char* image, 
    int width, int height, 
    int channels,int imageStride, 
    double timeStamp , bef_ai_slam_click_flag flag,
    bef_ai_slam_pose* pose);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_ai_slam_handle |SLAM algorithm handle. |
|image |const unsigned char \* |Image buffer data. |
|width |int |Image buffer width. |
|height |int |Image buffer height. |
|channels |int |Image channel quantity. |
|imageStride |int |Image buffer stride. |
|timeStamp |double |Timestamp of camera capturing image. |
|flag |bef_ai_slam_click_flag |Flag of clicking event. |
|pose |bef_ai_slam_pose\* |Camera pose. |


**Return value:** 

Return BEF_RESULT_SUC if succeed, or return error code.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Construct camera View matrix when rendering using rotation matrix and translational matrix of camera pose. Inverse view matrix when rendering.</div>


<div data-tips="true" data-tips-type="warning"><img src="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/doc-center/c412588-.png" width="350px" /></div>


<span id="fde945bd"></span>
## 7. SLAM Processes Plane Pose

```C
BEF_SDK_API bef_effect_result_t
bef_effect_ai_slam_get_plane_pose(
    bef_ai_slam_handle handle,  
    bef_ai_slam_pose cameraPose,
    int forceFacing, 
    bef_ai_slam_click_flag flag,
    bef_ai_slam_pose* retPose);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_ai_slam_handle |SLAM algorithm handle. |
|cameraPose |bef_ai_slam_pose |Camera pose. |
|forceFacing |int |Whether plane is facing to the camera. |
|Flag |bef_ai_slam_click_flag |Flag of click event. |
|retPose |bef_ai_slam_pose\* |Plane pose. |


**Return value:** 

Return BEF_RESULT_SUC if succeed, or return error code.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">When there's a click event and the plane is under tracking, plane pose can be captured. When placing items, items and plane pose are the same, so we can construct Model matrix using retPose when rendering.</div>


<div data-tips="true" data-tips-type="warning"><img src="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/doc-center/225bc66-.png" width="350px" /></div>


<span id="0e249e53"></span>
## 8. Release SLAM

```C
BEF_SDK_API bef_effect_result_t
bef_effect_ai_slam_destory(bef_ai_slam_handle);
```


**Parameters**:


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_ai_slam_handle |SLAM algorithm handle. |


**Return value:** 

Return BEF_RESULT_SUC if succeed, or return error code.

<span id="Java API"></span>
# Java API

For the detailed interface description, refer to the file: com.bytedance.labcv.effectsdk.BefSlamInfo.java

<span id="ed6f2290"></span>
## 1. Initialize camera parameters

```Java
/**
 * @brief init camera info
* @param camera For camera related information, refer to {@link BefSlamInfo.SlamCameraInfo}
 */
public void initCameraInfo(BefSlamInfo.SlamCameraInfo camera);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|camera |SlamCameraInfo |Initialize camera, refer to {@link BefSlamInfo.SlamCameraInfo}. |


**Return value:** 

Return BEF_RESULT_SUC if succeed, or return error code.

<span id="97bfbff0"></span>
## 2. Initialize the SLAM algorithm

```Java
/**
* @brief initializes slam handle
* @param modelPath slam model path
* @param deviceName Device name, available through Build.MODEL
* @param imuInfo IMU information
* @param cameraInfo For camera information, refer to {@link BefSlamInfo.SlamCameraInfo}
* @param version slam algorithm version, refer to {@link BytedEffectConstants.SlamVersion} for details
* @return successfully returns BEF_RESULT_SUC, other return values refer to {@link BytedEffectConstants}
 */
public int init(String modelPath, String deviceName, BefSlamInfo.SlamImuInfo imuInfo,
                BefSlamInfo.SlamCameraInfo cameraInfo, BytedEffectConstants.SlamVersion version);
```


**Parameters**:


|**Name** |**Type** |**Description** |
|---|---|---|
|modelPath |String |SLAM algorithm model file path. |
|deviceName |String |Device name, available Build.MODEL. |
|imuInfo |SlamImuInfo |IMU attributes setting. |
|cameraInfo |SlamCameraInfo |Camera parameter after camera initialization. |
|version |SlamVersion |SLAM version. |


**Return value:** 

Return BEF_RESULT_SUC if succeed, or return error code.

<span id="d6cf8ee7"></span>
## 3. Authentication

```Java
/**
* @brief check authorization file
* @param context android context app context
* @param licensePath absolute path to the authorization file
* @param onlineLicense Whether to online license
* @return successfully returns BEF_RESULT_SUC, other return values refer to {@link BytedEffectConstants}
 */
public int checklicense(Context context, String licensePath, boolean onlineLicense);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|context |Context |Application context. |
|licensePath |String |License absolute path. |
|onlineLicense |boolean |Whether it is an online license. |


**Return value:** 

Success returns BEF_RESULT_SUC, while failure returns the corresponding error code.

<span id="09a672bc"></span>
## 4. IMU thread inputs IMU information

```Java
/**
* @brief set detailed measurement of imu sensor data
* @param type imu data type, refer to {@link BytedEffectConstants.SlamImuDataType}
* @param data corresponds to type imu data, refer to {@link BefSlamInfo.SlamImuData} for details
* @return successfully returns BEF_RESULT_SUC, other return values refer to {@link BytedEffectConstants}
 */
public int setImuData(BytedEffectConstants.SlamImuDataType type, BefSlamInfo.SlamImuData data);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|type |SlamImuDataTyp |IMU data type. Refer to {@link BytedEffectConstants.SlamImuDataType}. |
|data |SlamImuData |Corresponding type IMU data. Refer to {@link BefSlamInfo.SlamImuData}. |


**Return value:** 

Success returns BEF_RESULT_SUC, while failure returns the corresponding error code.

<span id="9eeb6577"></span>
## 5. Obtain Camera Internal Parameters

```Java
/**
* @brief gets the camera parameters used by the slam algorithm
* @param deviceName Device name, available Build.MODEL
* @param paramPath Absolute path to the device camera internal parameter file
* @param width Image buffer width
* @param height Image buffer height
* @return camera internal parameter information, according to the internal parameter information, the projection projection matrix can be constructed, and the return value refers to {@link BefSlamInfo.SlamCameraIntrinsic}
 */
public BefSlamInfo.SlamCameraIntrinsic getCameraIntrinsic(String deviceName, String paramPath, int width, int height);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|deviceName |String |Device name, available Build.MODEL. |
|paramPath |String |Absolute path to the device camera internal parameter file. |
|Width |int |Image buffer width. |
|Height |int |Image buffer height. |


**Return value:** 

Success returns the camera internal parameter information. According to the internal parameter information, the projection projection matrix can be constructed. The return value refers to {@link BefSlamInfo.SlamCameraIntrinsic}. Failure returns the corresponding error code.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Construct Projection matrix when rendering using camera intrinsic parameters (executed only once)</div>


<div data-tips="true" data-tips-type="warning">Perspective matrix parameter description:</div>


<div data-tips="true" data-tips-type="warning">Camera internal parameter: Focus length on axis x & y (fx, fy); Center on axis x & y (cx, cy);</div>


<div data-tips="true" data-tips-type="warning">Image width & height (w, h); Depth of far & near plane (zF, zN).</div>


<div data-tips="true" data-tips-type="warning"><img src="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/doc-center/9fac2e0-.png" /></div>


<span id="8c5a0c7c"></span>
## 6. SLAM Processes Camera Pose

**The image cache type is bytebuffer:** 

```Java
/**
* @brief Get camera pose
* @param buffer image cache data
* @param image_width width of the image cache
* @param image_height height of the image cache
* @param image_stride image cache step size
* @param image_channlels number of image channels
* @param orientation device orientation, refer to {@link BytedEffectConstants.SlamDeviceOrientation} for details
* @param flag Click event identifier, refer to {@link BefSlamInfo.SlamClickFlag} for details
* @return returns the camera pose obtained by the algorithm, the return value refers to {@link BefSlamInfo.SlamCameraIntrinsic}
 */
public BefSlamInfo.SlamPose slamDetect(ByteBuffer buffer, int image_width,
                      int image_height,
                      int image_stride,
                      int image_channlels,
                      BytedEffectConstants.SlamDeviceOrientation orientation,
                      double time_stamp,
                      BefSlamInfo.SlamClickFlag flag);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|buffer |ByteBuffer |Image buffer data. |
|image_width |int |Image buffer width. |
|image_height |int |Image buffer height |
|image_stride |int |Image buffer stride. |
|image_channels |int |Image channel quantity. |
|orientation |lamDeviceOrientation |Device orientation. Refer to {@link BytedEffectConstants.SlamDeviceOrientation}. |
|timeStamp |double |Timestamp of camera capturing image. |
|flag |SlamClickFlag |Flag of clicking event Refer to {@link BefSlamInfo.SlamClickFlag}. |


**Return value:** 

Success returns the camera pose obtained by the algorithm, the return value refers to {@link BefSlamInfo.SlamCameraIntrinsic}. Failure returns the corresponding error code.

**The image cache is of type byte []:** 

```Java
/**
* @brief Get camera pose
* @param buffer image cache data, data type byte []
* @param image_width width of the image cache
* @param image_height height of the image cache
* @param image_stride image cache step size
* @param image_channlels number of image channels
* @param orientation device orientation, refer to {@link BytedEffectConstants.SlamDeviceOrientation} for details
* @param flag Click event identifier, refer to {@link BefSlamInfo.SlamClickFlag} for details
* @return returns the camera pose obtained by the algorithm, the return value refers to {@link BefSlamInfo.SlamCameraIntrinsic}
 */
public BefSlamInfo.SlamPose slamDetect(byte[] buffer, int image_width,
                        int image_height,
                        int image_stride,
                        int image_channlels,
                        BytedEffectConstants.SlamDeviceOrientation orientation,
                        double time_stamp,
                        BefSlamInfo.SlamClickFlag flag);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|buffer |byte [] |image buffer data. |
|image_width |int |Image buffer width. |
|image_height |int |Image buffer height. |
|image_stride |int |Image buffer stride. |
|image_channels |int |Image channel quantity. |
|orientation |lamDeviceOrientation |Device orientation. Refer to {@link BytedEffectConstants.SlamDeviceOrientation}. |
|timeStamp |double |Timestamp of camera capturing image. |
|flag |SlamClickFlag |Flag of clicking event. Refer to {@link BefSlamInfo.SlamClickFlag}. |


**Return value:** 

Success returns the camera pose obtained by the algorithm, the return value refers to {@link BefSlamInfo.SlamCameraIntrinsic}. Failure returns the corresponding error code,

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Construct camera View matrix when rendering using rotation matrix and translational matrix of camera pose. Inverse view matrix when rendering.</div>


<div data-tips="true" data-tips-type="warning"><img src="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/doc-center/da44329-.png" width="350px" /></div>


<span id="7a27b138"></span>
## 7. SLAM Processes Plane Pose

```Java
/**
* @brief get plane pose
* @param camera_pose camera pose
* @param force_facing whether the plane is facing the camera
* @param flag Click event identifier, refer to {@link BefSlamInfo.SlamClickFlag} for details
* @return returns plane pose information, the return value refers to {@link BefSlamInfo.SlamPose}
 */
public BefSlamInfo.SlamPose getPlanePose(BefSlamInfo.SlamPose camera_pose, int force_facing, BefSlamInfo.SlamClickFlag flag );
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|cameraPose |SlamPose |Camera pose |
|forceFacing |int |Whether plane is facing to the camera |
|flag |SlamClickFlag |Flag of click event |


**Return value:** 

Success returns plane pose information, the return value refers to {@link BefSlamInfo.SlamPose}. Failure returns the corresponding error code.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">When there's a click event and the plane is under tracking, plane pose can be captured. When placing items, items and plane pose are the same, so we can construct Model matrix using retPose when rendering.</div>


<div data-tips="true" data-tips-type="warning"><img src="https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/doc-center/86219bd-.png" width="350px" /></div>


<span id="5f3e711f"></span>
## 8. Release SLAM

```Java
/**
 * @brief destory slam handle
 */
public void destory();
```


**Return value:** 

Success returns BEF_RESULT_SUC, while failure returns the corresponding error code.

<span id="FAQ"></span>
## FAQ

<span id="6d995d5b"></span>
### 1. If there is any exception, check if there are any of the following types of logs

A: It is recommended to first check the log of the following tag output Error type:


* **bef_effect_ai**

* **SMASH_E_LOG**

* **EffectSDK**
