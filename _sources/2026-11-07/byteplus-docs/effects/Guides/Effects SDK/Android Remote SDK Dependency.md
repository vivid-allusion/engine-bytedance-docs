---
title: "Android Remote SDK Dependency"
product: "BytePlus Effects"
product_code: "effects"
source: "https://docs.byteplus.com/en/docs/effects/docs-mac-access-guide-v430-and-later"
---

<span id="Development Environment"></span>
# 1. Supported Versions

Version 4.7.1 and later (including 4.7.1)

<span id="828ec3b7"></span>
## 2. Add the SDK Maven Repository to Your Project (Sample for Reference)

Add Maven repository configuration in your project\-level `build.gradle`. Contact technical support to obtain `MAVEN_USER_NAME` and `MAVEN_PASS_WORD`.

```Plain
allprojects {
    repositories {
        google()
        jcenter()
        mavenCentral()
        // vehook_add_maven don't delete this line
        maven { url "https://jitpack.io" }
        maven { url 'https://maven.byted.org/repository/android_public/' }
        maven {
            url "https://artifact.bytedance.com/repository/thrall_ck/"
            credentials {
                username = MAVEN_USER_NAME
                password = MAVEN_PASS_WORD
            }
            authentication {
                digest(BasicAuthentication)
            }
        }
    }
}
allprojects {
    repositories {
        flatDir {
            dirs project(':library_core').file('libs')
        }
    }
}
```


<span id="d1fc94de"></span>
## 3. Update SDK Dependency in library_core: Switch from Local AAR to Remote Dependency (Sample for Reference)

Comment out or remove the local AAR dependency. Add remote dependency. Refer to Appendix: maven_version Changelog for the `maven_version` value.

```Plain
dependencies {
    if (project.effect_source == 'true'){
        api project(':effect-sdk')
    } else {
        api "com.bytedance:effectsdk:maven_version"
        // api fileTree(include: ['*.jar', '*.aar'], dir: 'libs')
    }
    // api(name: 'vesdk-9.1.2.111-tob', ext: 'aar')
    // api(name: 'NLEMediaJava790-release', ext: 'aar')
}
```


<span id="83bfc94e"></span>
## Appendix: maven_version Changelog


|SDK Version |maven_version |
|---|---|
|4.9.0 |com.bytedance:effectsdk:cv_tob4.9.0_202609141039_ce02d0e5981 |
|4.8.1 |com.bytedance:effectsdk:cv_tob4.8.1_202605131705_f3c616cca7d |
|4.8.0 |com.bytedance:effectsdk:cv_tob4.8.0_202512261520_75559b669cf |
|4.7.3 |com.bytedance:effectsdk:cv_tob4.7.3_202510271120_2e88395de69 |
|4.7.1 |com.bytedance:effectsdk:cv_tob4.7.1_202505221904_31c81745f5a |
