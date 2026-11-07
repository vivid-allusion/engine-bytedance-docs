---
title: "3D Face Mesh Algorithm"
product: "BytePlus Effects"
product_code: "effects"
source: "https://docs.byteplus.com/en/docs/effects/docs-3d-face-mesh-algorithm"
---

The 3D face can be obtained on top of the base 2D face keypoints, can get the 3D face keypoints.

<span id="Technical Specifications"></span>
# Technical Specifications


|**Category** |**Supported Formats** |
|---|---|
|Platform |* Android<br><br>* iOS |
|Input format |* RGBA8888<br><br>* BGRA8888 |
|Memory footprint |<42M （test device OPPO R11） |
|Detection speed |<5ms（test device OPPO R11） |


<span id="C API"></span>
# C API

Detailed description view header file: bef_effect_ai_facefitting.h

<span id="1. Create 3d mesh algorithm handle"></span>
## 1. Create 3D mesh algorithm handle

```C
BEF_SDK_API
bef_effect_result_t bef_effect_ai_facefitting_create(bef_ai_facefitting_handle *handle);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_ai_facefitting_handle\* |3D face mesh algorithm handle. |


```C
BEF_SDK_API
bef_effect_result_t bef_effect_ai_facefitting_init(bef_ai_facefitting_handle handle, const char *model_path);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_ai_facefitting_handle |3D face mesh algorithm handle. |
|model_path |const char \* |Model path. |


**Return value:** 

Success returns BEF_RESULT_SUC. Failure returns the corresponding error code. For more information on the error code, refer to bef_effect_ai_public_define.h

<span id="2.3d face mesh execution"></span>
## 2. 3D face mesh execution

```C
/**
 * Input face id and 106 keypoint info, return mesh info
 * @param handle
 * @param args  input
 * @param ret   output, this part of memory space is managed by sdk, will allocate space internally
 * @return
 */
BEF_SDK_API
bef_effect_result_t bef_effect_ai_do_fitting_3dmesh(bef_ai_facefitting_handle handle, bef_ai_facefitting_args* args, bef_ai_facefitting_result* ret);

// pack input
typedef struct {
    bef_ai_facefitting_landmark_info face_landmark_info[BEF_FITTING_MAX_FACE];
    int face_landmark_info_count;                   //the number of input faces
    int view_width;
    int view_height;
    float cameraParams[3];          // focal_length, centerx, centery
} bef_ai_facefitting_args;

//pack output
typedef struct {
    bef_ai_facefitting_mesh_info face_mesh_info[BEF_FITTING_MAX_FACE];
    int face_mesh_info_count;               //Return the number of meshes. Use face_mesh_info_count to take the first few contents of face_mesh_info, DO NOT go out of bounds!
    bef_ai_facefitting_mesh_config face_mesh_config;
} bef_ai_facefitting_result;

//Corresponds to the model file, the content does not change, the sdk manages the memory allocation and release
typedef struct {
    int version_code;                           // the version number of model
    float* uv;                            // uv coordinates of the standard expanded image, the sdk manages the memory allocation and release
    int uv_count;                               // the length of uv array
    unsigned short* flist;                // Index array of 3d model vertices (faces), the sdk manages the memory allocation and release
    int flist_count;                            // the length of flist array
    unsigned short* landmark_triangle;    // the triangle array after landmark does the triangulation, the sdk manages the memory allocation and release
    int landmark_triangle_count;                // the length of landmark array

    int num_vertex;                             // = uv_count/2 = vertex_count/3    the number of vertex elements, uv is the expanded 2d coordinate of the standard 3d model
    int num_flist;                              // = flist_count / 3                the number of flists
    int num_landmark_triangle;                  // = landmark_triangle_count / 2    the number of triangles
    int mum_landmark;                           // = landmark_count / 3             the number of landmrk
    int num_param;                              // = param_count                    the number of parameters
} bef_ai_facefitting_mesh_config;

// pack landmark
typedef struct {
    int id;                     //  Face id
    bef_ai_fpoint * landmark106;         // 106 point array required
    bool eye_lv2;              //  True eyes using secondary network optional
    bool eyebrow_lv2;          //  True eyebrows using secondary network optional
    bool lips_lv2;             //  True mouth using secondary network optional
    bool iris_lv2;             //True iris optional using secondary network
    bef_ai_fpoint * eye_left;       //   Left eye key point optional
    bef_ai_fpoint * eye_right;      //  Right eye keypoint optional
    bef_ai_fpoint * eyebrow_left;   // Left eyebrow key points optional
    bef_ai_fpoint * eyebrow_right;  //  Right eyebrow key points optional
    bef_ai_fpoint * lips;           // Lips key point optional
    bef_ai_fpoint * left_iris;      //  Left iris keypoint optional
    bef_ai_fpoint * right_iris;     // Right iris keypoint optional
} bef_ai_facefitting_landmark_info;


//  Manager memory by sdk, interpretation of count and num: count represents the length of the array, num represents how many elements the array has, for example, a 2d coordinate point (x, y) array [x, y, x, y, x, y, x, x, y ] ===> count = 8, num = 4
typedef struct {
    int id;                     // The id returned by the face sdk is used to indicate which face the mesh belongs to
    float* vertex;        // The vertex of the 3d model, the memory allocation and release are managed by the sdk
    int vertex_count;           //  The length of the vertex array
    float* landmark;      // An array of landmark coordinate values of the image coordinates projected by the 3D model. Memory allocation and release are managed by sdk
    int landmark_count;         // Length of the landmark array
    float* param;         //  Solve the optimized parameters, [scale, rotatex, rotatey, rotatez, tx, ty, alpha0, alpha1...], manager memory by sdk
    int param_count;            //  The length of the param array
    float mvp[16];              //  Change vertex to matrix with ndc coordinates
    float model[16];            // Model matrix including rotation, translation and scaling of the original model, used under orthogonal projection
    float * normal;       //  The normal in the model space, the length is the same as the vertex_count, and the memory allocation and release are managed by the sdk
    float * tangent;      // The tangent in the model space, the length is the same as the vertex_count, and the memory allocation and release are managed by the sdk
    float * bitangent;    // The subtangent in the model space, the length is the same as the vertex_count, and the memory allocation and release are managed by the sdk
    float rvec[3];              //  Rotation vector of opencv solvepnp output
    float tvec[3];              // Translation vector of opencv solvepnp output
} bef_ai_facefitting_mesh_info;
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_image_quality_enhancement_handle |3D face mesh algorithm handle |
|args |const bef_ai_facefitting_args\* |The result of face algorithm as input. |
|ret |bef_ai_facefitting_result\* |3D face mesh algorithm output. |


**Return value:** 

Success returns BEF_RESULT_SUC. Failure returns the corresponding error code. For more information on the error code, refer to bef_effect_ai_public_define.h

<span id="3.Release algorithm handle"></span>
## 3. Release algorithm handle

```C
BEF_SDK_API bef_effect_result_t
bef_effect_result_t bef_effect_ai_facefitting_release(bef_ai_facefitting_handle handle);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_effect_ai_facefitting_release |3D face mesh algorithm handle. |


**Return value:** 

Success returns BEF_RESULT_SUC. Failure returns the corresponding error code. For more information on the error code, refer to bef_effect_ai_public_define.h

<span id="4.3d face mesh algorithm authorization"></span>
## 4. 3D face mesh algorithm authorization

```C
// license detection
BEF_SDK_API bef_effect_result_t
bef_effect_ai_facefitting_check_license(
    bef_ai_facefitting_handle handle, 
    const char* license_path);

BEF_SDK_API bef_effect_result_t
bef_effect_ai_facefitting_check_license(JNIEnv *env, jobject context, bef_ai_facefitting_handle handle, const char* licensePath);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_ai_facefitting_handle |3D face mesh algorithm handle. |
|licensePath |const char \* |License file path. |


**Return value:** 

Success returns BEF_RESULT_SUC. Failure returns the corresponding error code. For more information on the error code, refer to bef_effect_ai_public_define.h

<span id="5.3d face mesh algorithm allocate and release result"></span>
## 5. 3D face mesh algorithm allocate and release result

```C
BEF_SDK_API bef_effect_result_t
bef_effect_ai_facefitting_malloc_result(bef_ai_facefitting_handle handle, bef_ai_facefitting_result ** result);

BEF_SDK_API bef_effect_result_t
bef_effect_ai_facefitting_free_result(bef_ai_facefitting_handle handle, bef_ai_facefitting_result * result);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_ai_facefitting_handle |3D face mesh algorithm handle. |
|result |bef_ai_facefitting_result \* |Algorithm result structure. |


<span id="6.3d face mesh algorithm set parameter"></span>
## 6. 3D face mesh algorithm set parameter

```C
typedef enum {
    BEF_AI_FACEFITTING_Solver_Lambda = 1,      // Solver parameter
    BEF_AI_FACEFITTING_Solver_MaxIter = 2,
    BEF_AI_FACEFITTING_Solver_Eps = 3,
    BEF_AI_FACEFITTING_Solver_Ratio = 4,
    BEF_AI_FACEFITTING_Solver_Smooth = 5,
    BEF_AI_FACEFITTING_Solver_Camera_Type = 6,
    BEF_AI_FACEFITTING_Config_Cal_TB = 7,
    BEF_AI_FACEFITTING_Eyelash_Flag = 8,
    BEF_AI_FACEFITTING_Use_Semantic_Lmk = 9,
    BEF_AI_FACEFITTING_Mouth_BS_Limit = 10
} bef_ai_facefitting_param_type;

BEF_SDK_API
bef_effect_result_t bef_effect_ai_facefitting_set_param(bef_ai_facefitting_handle handle, bef_ai_facefitting_param_type type, float value);
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|handle |bef_ai_facefitting_handle |3D face mesh algorithm handle. |
|type |bef_ai_facefitting_param_type |Parameter type. |
|value |float |The value of parameter. |


<span id="Java API"></span>
# Java API

**Interface Description**

Detailed description view file：com.bytedance.labcv.effectsdk.FaceFitting.java

<span id="1. Initialize 3d face mesh algorithm handle"></span>
## 1. Initialize 3D face mesh algorithm handle

```Java
int init(Context context, String modelPath, String licensePath, boolean onlineLicense) 
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|context |String |Java context. |
|licensePath |String |License file absolute path. |
|onlineLicense |boolean |If it is an online license. |


**Return value:** 

Returns BEF_RESULT_SUC successfully, otherwise returns the corresponding error code.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning"><code>InitConfig</code> can refer to <code>com.bytedance.labcv.effectsdk.FaceFitting.java</code>, and its definition is consistent with the C interface <code>bef_effect_ai_facefitting</code>.</div>


<span id="2.3d face mesh algorithm processing"></span>
## 2. 3D face mesh algorithm processing

```Java
public int detect(BefFaceInfo faceInfo, int viewWidth, int viewHeight, float cameraParams[])
```


**Parameters:** 


|**Name** |**Type** |**Description** |
|---|---|---|
|faceInfo |BefFaceInfo |Face info. |
|viewWidth |int |View width. |
|viewHeight |int |View height. |
|cameraParams |float[] |Camera parameter. |


<span id="3.Release 3d face mesh handle"></span>
## 3. Release 3D face mesh handle

```Java
public void destroy()
```


<span id="4.Get the result of 3d face mesh algorithm"></span>
## 4. Get the result of 3D face mesh algorithm

```Java
public FaceFittingResult getFaceFittingResult()

 public static class FaceFittingMeshInfo {
        public FaceFittingMeshInfo() {
        }

        public int getId() {
            return id;
        }

        public float[] getVertex() {
            return vertex;
        }

        public int getVertex_count() {
            return vertex_count;
        }

        public float[] getLandmark() {
            return landmark;
        }

        public int getLandmark_count() {
            return landmark_count;
        }

        public float[] getParam() {
            return param;
        }

        public int getParam_count() {
            return param_count;
        }

        public float[] getMvp() {
            return mvp;
        }

        public float[] getModel() {
            return model;
        }

        public float[] getNormal() {
            return normal;
        }

        public float[] getTangent() {
            return tangent;
        }

        public float[] getBitangent() {
            return bitangent;
        }

        public float[] getRvec() {
            return rvec;
        }

        public float[] getTvec() {
            return tvec;
        }

        int id;                     // The id returned by the face sdk is used to indicate which face the mesh belongs to
        float[] vertex;        // The vertex of the 3d model, the memory allocation and release are managed by the sdk
        int vertex_count;           //  The length of the vertex array
        float[] landmark;      // An array of landmark coordinate values of the image coordinates projected by the 3D model. Memory allocation and release are managed by sdk
        int landmark_count;         // Length of the landmark array
        float[] param;         // Solve the optimized parameters, [scale，rotatex, rotatey, rotatez, tx, ty, alpha0, alpha1 ......], manager memory by sdk
        int param_count;            // The length of the param array
        float mvp[];              // change vertex to matrix with ndc coordinates
        float model[];            // Model matrix including rotation, translation and scaling of the original model, used under orthogonal projection
        float [] normal;       // The normal in the model space, the length is the same as the vertex_count, and the memory allocation and release are managed by the sdk
        float [] tangent;      // The tangent in the model space, the length is the same as the vertex_count, and the memory allocation and release are managed by the sdk
        float [] bitangent;    // The subtangent in the model space, the length is the same as the vertex_count, and the memory allocation and release are managed by the sdk
        float rvec[];              // Rotation vector of opencv solvepnp output
        float tvec[];              // Translation vector of opencv solvepnp output
    };

    public static class FaceFittingMeshConfig {
        public FaceFittingMeshConfig() {
        }

        public int getVersion_code() {
            return version_code;
        }

        public float[] getUv() {
            return uv;
        }

        public int getUv_count() {
            return uv_count;
        }

        public short[] getFlist() {
            return flist;
        }

        public int getFlist_count() {
            return flist_count;
        }

        public short[] getLandmark_triangle() {
            return landmark_triangle;
        }

        public int getLandmark_triangle_count() {
            return landmark_triangle_count;
        }

        public int getNum_vertex() {
            return num_vertex;
        }

        public int getNum_flist() {
            return num_flist;
        }

        public int getNum_landmark_triangle() {
            return num_landmark_triangle;
        }

        public int getMum_landmark() {
            return mum_landmark;
        }

        public int getNum_param() {
            return num_param;
        }

        int version_code;                           // The version number of the model
        float[] uv;                            // The uv coordinates of the standard expanded image, memory allocation and release are managed by sdk
        int uv_count;                               // The length of the uv array
        short[] flist;                // The index array (face) of the vertex of the 3d model, the memory allocation and release are managed by the sdk
        int flist_count;                            // Length of the flist array
        short[] landmark_triangle;    // Landmark triangulates the triangular array, and the sdk manages memory allocation and release
        int landmark_triangle_count;                // Length of the landmark array

        int num_vertex;                             // = uv_count/2 = vertex_count/3    represents the number of vertex elements, uv is the expanded 2d coordinate of the standard 3d model
        int num_flist;                              // = flist_count / 3                Number of flist
        int num_landmark_triangle;                  // = landmark_triangle_count / 2    number of triangles
        int mum_landmark;                           // = landmark_count / 3            number of landmrk
        int num_param;                              // = param_count
    };

    public static class FaceFittingResult {
        public FaceFittingResult() {
            config = null;
            faceFittingMeshInfo = new FaceFittingMeshInfo[FaceFittingMaxFaceCount];
        }

        public FaceFittingMeshInfo[] getFaceFittingMeshInfo() {
            return faceFittingMeshInfo;
        }

        public int getFaceCount() {
            return faceCount;
        }

        public FaceFittingMeshConfig getConfig() {
            return config;
        }

        FaceFittingMeshInfo faceFittingMeshInfo[];
        int faceCount;
        FaceFittingMeshConfig config;
    };
```


<span id="FAQ"></span>
## FAQ

<span id="2225b70a"></span>
### 1. If there is any exception, check if there are any of the following types of logs

A: It is recommended to first check the log of the following tag output Error type:


* bef_effect_ai

* SMASH_E_LOG

* EffectSDK
