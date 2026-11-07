---
title: "Integrating VE SDK for Android using Flutter"
product: "BytePlus Video Editor"
product_code: "video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/video-editor-sdk/docs-integrating-ve-sdk-using-flutter_1_1_0"
---

Easily integrate the Video Editor SDK into your Flutter app for Android to unlock powerful features such as camera functionality, comprehensive editing tools, seamless draft management with the draft box feature, efficient export capabilities, and robust business modules. Achieve seamless video editing experiences tailored to your app's needs with just a few lines of code.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a032c13c5f7f46e49f16ca6e84954e35~tplv-goo7wpa0wc-image.image) </span>

<span id="7dac8f6a"></span>
# Development environment

The following table shows the required Android development environment for BytePlus Video Editor SDK:


|**Development Environment** |**Version** |
|---|---|
|Gradle |7.5.1 |
|Android Gradle Plugin |7.3.1 |
|kotlin |1.5.30 |
|minSdk |21 |
|targetSdk |33 |
|compileSdk |33 |
|Java Version |11 |


The following table shows the required Flutter development environment and tools for BytePlus Video Editor SDK:


|**Development Environment** |**Version** |
|---|---|
|Flutter |3.16+ |
|Android Studio/VSCode |Latest version |


<span id="25f8fdda"></span>
# Step 1: Creating a flutter project

Follow these steps to create a new flutter project. If you already have an existing one, skip this step.

**To create a flutter project:** 


1. Select your development platform from the [Flutter website](https://docs.flutter.dev/get-started/install) and follow the instructions to create your Flutter app.

   Sample code:

   ```Kotlin
   //  create create command
   // --org org name 
   //--platforms android,ios 
   flutter create --org com.volcengin.effectone --platforms android,ios effectone_flutter_sample //创建demo项目
   flutter run //Run the demo module.
   ```
   

2. Ensure that your Flutter project follows this directory:

   ```Bash
   ├── README.md
   ├── analysis_options.yaml
   ├── android
   ├── build
   ├── ios
   ├── lib
   ├── pubspec.lock
   ├── pubspec.yaml
   └── test
   ```
   


<span id="eaf093ef"></span>
# Step 2: Initialize Video Editor SDK

Refer to [Getting started with VE SDK—Android](https://docs.byteplus.com/docs/video-editor-sdk/docs-getting-started-with-android_1_1_0#706d2e38) to complete the initialization. After completion, use **flutter run** to install and run the demo. If no errors are reported, you have successfully initialized the Video Editor SDK.

**Sample initialization code:** 

```Kotlin

class EffectOneApp : Application() {

    override fun onCreate() {
        super.onCreate()
        EOQuickInitHelper.licenseFileName = "your license file name"
        EOQuickInitHelper.initApplication(this)
    }
}
```


<span id="6662f6a8"></span>
# Step 3: Dart sample code

```Dart
import 'package:flutter/material.dart';
import 'package:flutter/services.dart';

void main() {
  runApp(const MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  // This widget is the root of your application.
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Flutter Demo',
      theme: ThemeData(
        // This is the theme of your application.
        //
        // TRY THIS: Try running your application with "flutter run". You'll see
        // the application has a purple toolbar. Then, without quitting the app,
        // try changing the seedColor in the colorScheme below to Colors.green
        // and then invoke "hot reload" (save your changes or press the "hot
        // reload" button in a Flutter-supported IDE, or press "r" if you used
        // the command line to start the app).
        //
        // Notice that the counter didn't reset back to zero; the application
        // state is not lost during the reload. To reset the state, use hot
        // restart instead.
        //
        // This works for code too, not just values: Most code changes can be
        // tested with just a hot reload.
        colorScheme: ColorScheme.fromSeed(seedColor: Colors.deepPurple),
        useMaterial3: true,
      ),
      home: const MyHomePage(title: 'Flutter Demo Home Page'),
      routes: <String, WidgetBuilder>{
        "export": (context) => MyExportPage(title: 'Flutter Demo Export Page')
      },
    );
  }
}

class MyExportPage extends StatefulWidget {
  const MyExportPage({super.key, required this.title});

  // This widget is the home page of your application. It is stateful, meaning
  // that it has a State object (defined below) that contains fields that affect
  // how it looks.

  // This class is the configuration for the state. It holds the values (in this
  // case the title) provided by the parent (in this case the App widget) and
  // used by the build method of the State. Fields in a Widget subclass are
  // always marked "final".

  final String title;

  @override
  State<MyExportPage> createState() => _MyExportPageState();
}

class _MyExportPageState extends State<MyExportPage> {

  void _exportCounter() {
    setState(() {
      print('export');
      callNativeMethodWithMethodName("export");
    });
  }

  static const platform = MethodChannel("effectOne.export");
  Future<void> callNativeMethodWithMethodName(String methodName) async {
    try {
      await platform.invokeMethod(methodName);
    } on PlatformException catch (e) {
      print("Failed to call native method: ${e.message}");
    }
  }

  @override
  Widget build(BuildContext context) {
    // This method is rerun every time setState is called, for instance as done
    // by the _incrementCounter method above.
    //
    // The Flutter framework has been optimized to make rerunning build methods
    // fast, so that you can just rebuild anything that needs updating rather
    // than having to individually change instances of widgets.
    return Scaffold(
      appBar: AppBar(
        // TRY THIS: Try changing the color here to a specific color (to
        // Colors.amber, perhaps?) and trigger a hot reload to see the AppBar
        // change color while the other colors stay the same.
        backgroundColor: Theme.of(context).colorScheme.inversePrimary,
        // Here we take the value from the MyHomePage object that was created by
        // the App.build method, and use it to set our appbar title.
        title: Text(widget.title),
      ),

      body: Center(
        // Center is a layout widget. It takes a single child and positions it
        // in the middle of the parent.

        child: Column(
          // Column is also a layout widget. It takes a list of children and
          // arranges them vertically. By default, it sizes itself to fit its
          // children horizontally, and tries to be as tall as its parent.
          //
          // Column has various properties to control how it sizes itself and
          // how it positions its children. Here we use mainAxisAlignment to
          // center the children vertically; the main axis here is the vertical
          // axis because Columns are vertical (the cross axis would be
          // horizontal).
          //
          // TRY THIS: Invoke "debug painting" (choose the "Toggle Debug Paint"
          // action in the IDE, or press "p" in the console), to see the
          // wireframe for each widget.
          mainAxisAlignment: MainAxisAlignment.center,
          children: <Widget>[
            TextButton(
              onPressed: _exportCounter,
              child: Text("Export"),
            ),
          ],
        ),
      ),
      // This trailing comma makes auto-formatting nicer for build methods.
    );
  }
}

class MyHomePage extends StatefulWidget {
  const MyHomePage({super.key, required this.title});

  // This widget is the home page of your application. It is stateful, meaning
  // that it has a State object (defined below) that contains fields that affect
  // how it looks.

  // This class is the configuration for the state. It holds the values (in this
  // case the title) provided by the parent (in this case the App widget) and
  // used by the build method of the State. Fields in a Widget subclass are
  // always marked "final".

  final String title;

  @override
  State<MyHomePage> createState() => _MyHomePageState();
}

class _MyHomePageState extends State<MyHomePage> {

  void _recorderCounter() {
    setState(() {
      print('camera');
      callNativeMethodWithMethodName("record");
    });
  }
  void _draftCounter() {
    setState(() {
      callNativeMethodWithMethodName("draft");
    });
  }
  static const platform = MethodChannel("effectOne.flutter");
  Future<void> callNativeMethodWithMethodName(String methodName) async {
    try {
      await platform.invokeMethod(methodName);
    } on PlatformException catch (e) {
      print("Failed to call native method: ${e.message}");
    }
  }

  @override
  Widget build(BuildContext context) {
    // This method is rerun every time setState is called, for instance as done
    // by the _incrementCounter method above.
    //
    // The Flutter framework has been optimized to make rerunning build methods
    // fast, so that you can just rebuild anything that needs updating rather
    // than having to individually change instances of widgets.
    return Scaffold(
      appBar: AppBar(
        // TRY THIS: Try changing the color here to a specific color (to
        // Colors.amber, perhaps?) and trigger a hot reload to see the AppBar
        // change color while the other colors stay the same.
        backgroundColor: Theme.of(context).colorScheme.inversePrimary,
        // Here we take the value from the MyHomePage object that was created by
        // the App.build method, and use it to set our appbar title.
        title: Text(widget.title),
      ),

      body: Center(
        // Center is a layout widget. It takes a single child and positions it
        // in the middle of the parent.

        child: Column(
          // Column is also a layout widget. It takes a list of children and
          // arranges them vertically. By default, it sizes itself to fit its
          // children horizontally, and tries to be as tall as its parent.
          //
          // Column has various properties to control how it sizes itself and
          // how it positions its children. Here we use mainAxisAlignment to
          // center the children vertically; the main axis here is the vertical
          // axis because Columns are vertical (the cross axis would be
          // horizontal).
          //
          // TRY THIS: Invoke "debug painting" (choose the "Toggle Debug Paint"
          // action in the IDE, or press "p" in the console), to see the
          // wireframe for each widget.
          mainAxisAlignment: MainAxisAlignment.center,
          children: <Widget>[
            TextButton(
              onPressed: _recorderCounter,
              child: Text("Recorder"),
            ),

            TextButton(
              onPressed: () {
                print('draft box');
                _draftCounter();
              },
              child: Text('Draft'),
            ),
          ],
        ),
      ),
      // This trailing comma makes auto-formatting nicer for build methods.
    );
  }
}
```


<span id="d1f17e17"></span>
# Step 4: Initialize `Sample Activity`

Register two native methods, "record" and "draft," which respectively correspond to starting the recording page and launching the draft page.

```Kotlin

private const val METHOD_CHANNEL_NAME = "effectOne.flutter"
private const val METHOD_NAME_DRAFT = "draft"
private const val METHOD_NAME_RECORD = "record"
class MainActivity: FlutterFragmentActivity() {
    private var authResult = false
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        EOQuickInitHelper.prepareAndInit() { result, str ->
            this.authResult = result
        }
    }

    override fun configureFlutterEngine(flutterEngine: FlutterEngine) {
        GeneratedPluginRegistrant.registerWith(flutterEngine)
        MethodChannel(flutterEngine.dartExecutor.binaryMessenger, METHOD_CHANNEL_NAME)
            .setMethodCallHandler { call: MethodCall, _ ->
                when (call.method) {
                    METHOD_NAME_DRAFT -> {
                        if (authResult) {
                            EOQuickInitHelper.startDraft(this@MainActivity)
                        }
                    }

                    METHOD_NAME_RECORD -> {
                        if (authResult) {
                            EOQuickInitHelper.startRecorder(this@MainActivity)
                        }
                    }

                }

            }
    }
}
```


<span id="5b54bbbd"></span>
# Step 5: Configuring the export feature


1. Create a new `ExportActivity`. For more information, refer to [Exporting videos](https://docs.byteplus.com/docs/video-editor-sdk/docs-getting-started-with-android_1_1_0#bebd5939) and [Export video activity configuration](https://docs.byteplus.com/docs/video-editor-sdk/docs-getting-started-with-android_1_1_0#1737852f).

   EO uses the following `com.volcengine.effectone.Launch.EOExport` and intends to direct the data to the right `Activity`.

2. Within `ExportActivity`, create`ExportFragment : FlutterFragment().`

3. Route it to the Dart sample code's `MyExportPage` and register `NativeMethod: export` in `ExportFragment`.

   ```Kotlin
   class ExportActivity: FragmentActivity() {
       private lateinit var eoExportManager: EOExportManager
       private var exportActionView: View? = null
       override fun onCreate(savedInstanceState: Bundle?) {
           super.onCreate(savedInstanceState)
           setContentView(R.layout.activity_export);
           // Create and attach a FlutterFragment if one does not exist.
           val flutterFragment = ExportFragment()
           getSupportFragmentManager()
               .beginTransaction()
               .add(
                   R.id.flutter_container,
                   flutterFragment,
                   "TAG_FLUTTER_FRAGMENT"
               )
               .commit();
       }
   
   }
   
   private const val METHOD_CHANNEL_EXPORT = "effectOne.export"
   private const val METHOD_NAME_EXPORT = "export"
   class ExportFragment : FlutterFragment() {
       private lateinit var eoExportManager: EOExportManager
       override fun getInitialRoute(): String {
           return "export"
       }
   
       override fun onViewCreated(view: View, savedInstanceState: Bundle?) {
           super.onViewCreated(view, savedInstanceState)
           eoExportManager = EOExportManager.init(requireActivity()) { suc ->
               if (!suc) {
                   requireActivity().finish()
               }
           }
       }
       //导出的核心方法
       private fun runExportAction() {
           val saveDir =
               Environment.getExternalStoragePublicDirectory(Environment.DIRECTORY_DCIM).absolutePath
           val dateFormat = SimpleDateFormat("yyyyMMdd-HHmmss", getDefault())
           val exportFileName = "sample-${dateFormat.format(Date())}.mp4"
   
           val exportFilePath = "$saveDir${File.separator}$exportFileName"
           //>>>> step2 导出
           eoExportManager.exportVideo(
               outputPath = exportFilePath,
               outputSetting = EOOutputVideoSettings(),
               exportListener = EOExportDefaultListener()
           )
       }
   
       override fun configureFlutterEngine(flutterEngine: FlutterEngine) {
           super.configureFlutterEngine(flutterEngine)
           MethodChannel(flutterEngine.dartExecutor.binaryMessenger, METHOD_CHANNEL_EXPORT)
               .setMethodCallHandler { call: MethodCall, _ ->
                   when (call.method) {
                       METHOD_NAME_EXPORT -> {
                           Toast.makeText(requireActivity(), "export start", Toast.LENGTH_SHORT).show()
                           runExportAction()
                       }
                   }
   
               }
       }
   
   }
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you need to utilize other functionalities of <code>EOExportManager</code>, such as frame extraction or previewing, you can refer to the <a href="https://docs.byteplus.com/docs/video-editor-sdk/docs-android-export-function-apis_1_1_0">Export function APIs</a> and the <code>EffectOneExportViewModel</code> in the demo project.   </div>
   

<span id="0cfbe3d0"></span>
# Step 6: Run the project

```Groovy
flutter clean 
flutter run 
```
