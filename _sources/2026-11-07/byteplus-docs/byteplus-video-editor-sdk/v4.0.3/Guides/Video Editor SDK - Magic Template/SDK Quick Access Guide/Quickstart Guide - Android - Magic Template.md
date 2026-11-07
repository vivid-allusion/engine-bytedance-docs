---
title: "Quickstart Guide - Android - Magic Template"
product: "BytePlus Video Editor (Archive)"
product_code: "byteplus-video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/byteplus-video-editor-sdk/docs-quickstart-guide-android-magic-template"
---

<span id="Development preparations"></span>
## **Development preparations**

<span id="System requirements"></span>
### **System requirements**

The Android SDK version must be 21 or later, and the device version must be 5.0 or higher.

<span id="Development environment"></span>
### **Development environment**

1、minSdkVersion: 21

2、targetSdkVersion: 29

3、buildToolsVersion: "29.0.2"

4、AndroidStudio: 4.1

<span id="Quick integration of the Magic Template SDK"></span>
## **Quick integration of the Magic Template** **SDK**

This SDK provides only the operation objects and relevant APIs required for template editing. It does not include the user interfaces (UIs). You can develop the UIs based on your business requirements.

1、Create the **libs** directory in the app project and place the **CutSameIF.aar** package into the **libs** directory.

<span>![图片](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/0b587c5aad99412ba64a6ee91fd7cbc6~tplv-em5hxbkur4-noop.image) </span>

2、In the **build.gradle** file of the app project, add an AAR reference.

```Groovy
android {

  .......

}

repositories {

    flatDir {

        dirs 'libs'

    }

}

dependencies {

    implementation fileTree(dir: 'libs', include: ['*.jar'])

    api(name: 'CutSameIF', ext: 'aar')

}
```


3、In the **build.gradle** file in the app project, specify the architectures that are compatible with the NDK.

**Note:**  The Magic Template SDK supports the armeabi\-v7a and arm64\-v8a architectures. You can add the corresponding ABI as needed.

```Groovy
android {

  ndk {

    abiFilters = ['armeabi-v7a','arm64-v8a']

  }

}
```


4、Specify the third\-party open\-source dependency libraries.

```Kotlin
//retrofit

implementation 'com.squareup.retrofit2:adapter-rxjava2:2.9.0'

implementation 'com.squareup.retrofit2:converter-gson:2.9.0'
```


5、Initialize the SDK to ensure that the features can be properly used.

```Kotlin
CutSameSolution.init(

    context = this,

    authorityConfig = AuthorityConfig.Builder()

        .appId("com.cutsame.demo")

        .licensePath(getLicenseFilePath())

        .authorityListener(object : AuthorityConfig.AuthorityListener{

            override fun onSuccess() {

                Log.d(TAG, "success")

            }

            override fun onError(errorCode: Int, errorMsg: String) {

                Log.d(TAG, "onError $errorCode $errorMsg")

            }

        }).build(),



    templateFetcherConfig = TemplateFetcherConfig.Builder()

        .host("http://xx.xxxx.net")

        .pageSize(20)

        .build(),



    effectFetcherConfig =  EffectFetcherConfig.Builder()

        .host("http://xx.xxxx.net")

        .modelPath("/api/modellistinfo")

        .effectLitPath("/api/effectlist")

        .build()

)
```


<span id="Quick integration of the Magic Template User Interface SDK"></span>
## **Quick integration of the Magic Template User Interface SDK**

The SDK provides default UIs to help you quickly launch your app.

<span id="Source code integration"></span>
### **Source code integration**

1、 Copy the CutSameUIIF module of the demo to the project.

<span>![图片](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/ddfc3827e1a1456a90189a7b3e097607~tplv-em5hxbkur4-noop.image) </span>

2、Place the **CutSameIF.aar** package into the **libs** directory of the CutSameUIIF module.

3、In the **build.gradle** file under the directory of the CutSameUIIF module, add an AAR reference.

```Groovy
android {

  .......

}



repositories {

    flatDir {

        dirs 'libs'

    }

}



dependencies {

    implementation fileTree(dir: 'libs', include: ['*.jar'])

    api(name: 'CutSameIF', ext: 'aar')

}
```


4、In the **build.gradle** file of the app project, add an AAR reference.

```Groovy
android {

  .......

}



repositories {

    flatDir {

        dirs 'libs','../CutSameUIIF/libs'

    }

}



dependencies {

    implementation fileTree(dir: 'libs', include: ['*.jar'])

}
```


<span id="AAR integration"></span>
### **AAR** **integration**

1、Create the **libs** directory in the app project and place the **CutSameIF.aar** and**CutSameUIIF.aar** packages into the **libs** directory.

<span>![图片](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/7134b3f4f66b472abb550ed4e7f7004e~tplv-em5hxbkur4-noop.image) </span>

2、In the **build.gradle** file of the app project, add an AAR reference.

```Groovy
android {

  .......

}



repositories {

    flatDir {

        dirs 'libs'

    }

}



dependencies {

    implementation fileTree(dir: 'libs', include: ['*.jar'])

    api(name: 'CutSameIF', ext: 'aar')

    api(name: 'CutSameUIIF', ext: 'aar')

}
```


3、Specify the official component dependency libraries and third\-party open\-source dependency libraries.

```Apache
mplementation "com.android.support:appcompat-v7:27.1.1"

implementation 'com.android.support.constraint:constraint-layout:2.0.4'

implementation 'com.android.support:design:27.1.1'

implementation 'com.android.support:swiperefreshlayout:27.1.1'

implementation 'android.arch.lifecycle:extensions:1.1.1'

implementation 'com.airbnb.android:lottie:2.7.0'

implementation "com.github.bumptech.glide:glide:4.8.0"
```
