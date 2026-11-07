---
title: "Integrating VE SDK using Jetpack Compose"
product: "BytePlus Video Editor"
product_code: "video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/video-editor-sdk/160-integrating-ve-sdk-using-jetpack-compose"
---

Video Editor SDK provides built\-in UI components for the camera and editor modules, which make it easier for you to initialize the SDK in Jetpack Compose. If the host project is not built with `FragmentActivity`, the APIs for runtime permissions in Android are not available for use. Therefore, you need to develop these APIs on your own. Also, you can develop advanced features and UI components based on your development requirements. This section introduces sample codes associated with Video Editor SDK initialization in Jetpack Compose.

<span id="68be99d4"></span>
# Prerequisities

Ensure you have imported the required dependencies.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If you are using <code>ComponentActivity</code> as your host instead of <code>FragmentActivity</code>, the Android runtime permission\-related interfaces provided in <code>EOQuickInitHelper</code> cannot be used. You can refer to the source code of <code>EOQuickInitHelper.kt</code>and implement them. For more information on requesting runtime permissions in Android, refer <a href="https://developer.android.com/training/permissions/requesting">here</a>.</div>


<span id="a8f2bb8e"></span>
# Initializing the SDK and Application

In Jetpack Compose or other UI toolkits, the initialization procedure of the application and the gradle configuration of Video Editor SDK components have no differences.

<span id="91469e1d"></span>
## The recorder page

The implementation of the recorder page is as follows:

```Java
class HostActivity : FragmentActivity() {

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContent {
            SampleEffectStudioRecommendTheme {
                // A surface container using the 'background' color from the theme 
                Surface(
                    modifier = Modifier.fillMaxSize(),
                    color = MaterialTheme.colorScheme.background
                ) {
                    Main("Android")
                }
            } 
        }
    }

}

@Composable
fun Main(name: String, modifier: Modifier = Modifier) {
    Box(
        modifier = Modifier.fillMaxSize(),
        ) {
        val activity = LocalContext.current as FragmentActivity
        Button(onClick = {
            EOQuickInitHelper.prepareAndInit(activity) {
                EOQuickInitHelper.startRecorder(activity)
            }
        }, modifier = Modifier.align(Alignment.Center)) {
            Text(
                text = "Start Recorder",
                modifier = modifier
            )
        }
    }
}
```


<span id="415d545f"></span>
## The export page

The implementation of the export function based on Jetpack Compose remains the same as when you build the export module with native Android methods.
