---
title: "Managing Android highlight clippings"
product: "BytePlus Video Editor"
product_code: "video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/video-editor-sdk/150-managing-android-highlight-clippings"
---

Highlight clipping is a technique used to manage the exposure of the brightest parts of an image or video, ensuring that they do not exceed the display's capability, which would result in a loss of detail and a washed\-out appearance. The highlight clipping process:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/971e8a1cefdb486ba3873e44705672af~tplv-goo7wpa0wc-image.image) </span>

This article introduces how to integrate and initialize highlight clippings in Android in the following steps:


1. Setting up the development environment.

2. Configuring the Maven repository.

3. Configuring dependencies.

4. Initializing the SDK.

5. Matching templates.

6. Creating videos.


<span id="434d8f31"></span>
# Step 1: Setting up development environments

For more information on the development environment, refer to [Development environment](https://docs.byteplus.com/docs/video-editor-sdk/150-getting-started-with-android#13ddd4bf).

<span id="2e30c31b"></span>
# Step 2: Configuring the Maven repositories

To access the SDK, you must configure the Maven repository in your project's build configuration file. This step ensures that your project can download the necessary SDK dependencies.

```Groovy
maven {
    url "https://artifact.bytedance.com/repository/thrall_ck/"
    credentials {
        username = MAVEN_USER_NAME // Your Maven username 
        password = MAVEN_PASS_WORD // Your Maven repository password
    }
    authentication {
        digest(BasicAuthentication)
    }
}
```


<span id="558a3f18"></span>
# Step 3: Adding dependencies

Add the SDK to your project by adding dependencies to your build configuration file.

```Kotlin
implementation "com.volcengine.effectone:ck-highlight:${version}"  
```


<span id="6be1f08a"></span>
# Step 4: Preparing model files

Before initializing the SDK, you need to ensure that the model files are downloaded to your local system and the parent directory path of the model files is identified:

```Kotlin
// The directory where the model files are stored  
File modelFileDir = new File("path/to/model/files");
String modelFileDirPath = modelFileDir.getAbsolutePath();
```


<span id="3873a897"></span>
# Step 5: Implementing Template Providers

Create a class that implements the `ITemplateProvider` interface to provide the SDK with a list of templates:

```Kotlin
interface ITemplateProvider {
    // The SDK user must implement this interface to retrieve templates
    fun provideTemplateList(): List<EOMomentTemplate>
}
```


Implement `ITemplateProvider` and return `List<EOMomentTemplate>`.

<span id="f672df15"></span>
# Step 7: Configuring authorizations

You have to configure authorization permissions before initializing the SDK.

```Kotlin
// Initialize the EO Authorization SDK
EOAuthorizationSDKInit.init(context);
```


<span id="a3b24c97"></span>
# Step 6: Initializing the SDK

Initialize the SDK using the following full sample code:

```Kotlin
HighLightSDKInit.init(
    context,
    HLSDKConfig.Builder()
        // Set the path for the authorization file
        .setLicensePath(EOAuthorizationInternal.getVELicensePath() ?: "")
        // Set the provider for the template list
        .setTemplateProvider(new HLMTemplateProvider())
        // Set the path for the model files
        .modelPath(modelFileDirPath)
        // Set the frame extraction quality: LOW, MID, HIGH
        .setImageQuality(ImageQuality.LOW)
        // Set the maximum number of template matches
        .setMaxMatchCount(3)
        .build()
);
```


<span id="52e85cd2"></span>
# Step 7: Retrieving matching highlight clipping templates

The process involves running the template matching operation on the I/O thread to ensure that it doesn't block the main thread of your application.

```Kotlin
// Execute the template matching process on the I/O thread
val matchedInfo = withContext(Dispatchers.IO) {
    // Convert media items into a format recognizable by the SDK
    val list = mediaList.map { it.toRecognizeMedia() }
    // Use the SDK to analyze and recognize the media content
    val recognizeMedias = HighLightSDKInit.recognizeMedias(list)  
    // Retrieve the template provider that will supply available templates
    val templateProvider = HighLightSDKInit.getTemplateProvider()
    
    // Initiate the template matching process
    HighLightSDKInit.getTemplateFinder().findSuitedTemplate(
        recognizeMedias, // The recognized media content
        templateProvider // The provider that offers templates
    )
}
```


The `matchedInfo` variable will contain information about the templates that best match the recognized media content. This information can then be used to proceed with video generation using the editing SDK.

<span id="5031fe32"></span>
# Step 8: Creating videos

For more information on creating videos, refer to [Managing Magic Template objects in Android](https://docs.byteplus.com/docs/video-editor-sdk/150-managing-magic-template-objects-in-android).

<span id="79f5c188"></span>
# Highlight clipping data classes

These are the Highlight clipping data classes.

<span id="dc3fbc16"></span>
## EOTemplateMatchedInfo

This data class is used to encapsulate the result of the template matching process. It contains a template that has been matched and a list of media items that were used in the matching process along with their recognition results.

```Kotlin
data class EOTemplateMatchedInfo(
    // The template that was matched
    val template: EOMomentTemplate,
    // A list of items that include the input media and their recognition results
    val mediaList: List<EOTemplateMatchedItem>
)
```


**Parameters**


|**Parameter** |**Type** |**Description** |
|---|---|---|
|`template` |EOMomentTemplate |The matched template information |
|`mediaList` |List |List of items containing input media and their highlights results |


<span id="d4940940"></span>
## EOTemplateMatchedItem

This data class represents a single item within the list of matched media items. It includes the recognized media and the results of the extraction process, which may include classification and aesthetic scoring.

```Kotlin
data class EOTemplateMatchedItem(
    // The recognized media item
    val media: EORecognizeMedia,
    // The extraction results including classification and aesthetic scoring
    val extractorResult: EOExtractorResult
)
```


**Parameters**


|**Parameter** |**Type** |**Description** |
|---|---|---|
|`media` |EORecognizeMedia |The recognized media |
|`extractorResult` |EOExtractorResult |The classification and aesthetic scoring of the recognized media |


<span id="80eb176d"></span>
## EORecognizeMedia

This class defines the structure for media items that are to be recognized by the SDK.

```Kotlin
data class EORecognizeMedia(
    // Unique identifier for the media item
    val id: String,
    // Local file path to the media item
    val path: String,
    // Type of media: 1 for Image, 2 for Video (see HLMediaType for definitions)
    val type: Int,
    // Width of the media item in pixels
    val width: Int,
    // Height of the media item in pixels
    val height: Int,
    // Duration of the media item in seconds (set to 0 for images)
    val duration: Int = 0,
    // Date when the media item was created, in Unix timestamp format
    val date: Int = 0,
)
```


**Parameters**


|**Parameter** |**Type** |**Sample Value** |**Description** |
|---|---|---|---|
|`id` |String |"12345xyz" |Unique identifier for the media item |
|`path` |String |"/storage/videos/vacation.mp4" |Local file path to the media item |
|`type` |Int |2 |Type of media:<br><br><br>* **1** : Image<br><br>* **2** : Video |
|`width` |Int |1920 |Width of the media item in pixels |
|`height` |Int |1080 |Height of the media item in pixels |
|`duration` |Int |120 (2 minutes) |Duration of the media item in seconds (set to 0 for images) |
|`date` |Int |1609459200 (January 1, 2021) |Creation date of the media item in Unix timestamp format |
