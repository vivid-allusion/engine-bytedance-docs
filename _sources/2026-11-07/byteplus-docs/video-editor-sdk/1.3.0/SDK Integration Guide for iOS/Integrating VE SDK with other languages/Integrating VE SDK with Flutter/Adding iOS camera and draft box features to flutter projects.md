---
title: "Adding iOS camera and draft box features to flutter projects"
product: "BytePlus Video Editor"
product_code: "video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/video-editor-sdk/130-adding-ios-camera-and-draft-box-features-to-flutter-projects"
---

You can follow the next few steps, configure the sample codes, and add them into your project to add the camera and draft box features to your Flutter project.

<span id="2c0dfe60"></span>
# **Prerequisities**

Before adding the iOS camera and draft box features, you have to complete the following:


* Add the dependencies using Cocoapods. For details, refer to [Managing dependencies using Cocoapods](https://docs.byteplus.com/docs/video-editor-sdk/27306).

* Retrieve your SDK package from your BytePlus representatives. For more information, refer to the [Managing dependencies using Cocoapods](https://docs.byteplus.com/docs/video-editor-sdk/27306).

* You have Android Studio installed on your system.

* You have Flutter version 3.16 or newer installed on your system.


<span id="370f8815"></span>
# Step 2.1: Navigate to `main.dart`


1. Open the Video Editor SDK Flutter demo project.

2. Click **iOS** \> **lib** \> **`main.dart`**.


<span id="1ca5e007"></span>
# Step 2.2: Create a button.

To create a button, configure the following code and add it to your project:

```Dart
 mainAxisAlignment: MainAxisAlignment.center,
          children: [
            TextButton(
              onPressed: _recorderCounter,
              child: Text("Recorder"),
            ),

            TextButton(
              onPressed: () {
                _draftCounter();
              },
              child: Text('Draft')
```


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/70cba026304f47d4bffe7d149cb8b94e~tplv-goo7wpa0wc-image.image) </span>

<span id="2aea9bdc"></span>
# Step 2.3: Build communication models between Flutter and native platforms

You can build a communication model between Flutter and native platforms by adding the following channel name to your `main.dart`:

```Dart
effectOne.Flutter 
```


This is the sample code for reference:

```Dart
}
  static const platform = MethodChannel("effectOne.Flutter");
  Future<void> callNativeMethodWithMethodName(String methodName) async {
    try {
      await platform.invokeMethod(methodName);
    } on PlatformException catch (e) {
      print("Failed to call native method: ${e.message}");
    }
  } 
```


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0e01a7ae45ee496399cdfcfff78bd9d7~tplv-goo7wpa0wc-image.image) </span>

<span id="11177f88"></span>
# Step 2.4: Adding communication interactions

Add the following code to `main.dart` to add communication interactions:

```Dart
 void _recorderCounter() {
    setState(() {
      callNativeMethodWithMethodName("recoder");
    });
  }
  void _draftCounter() {
    setState(() {
      callNativeMethodWithMethodName("draft");
    });
  } 
```


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/67805311178149ad8c145c85664ac3d3~tplv-goo7wpa0wc-image.image) </span>

<span id="7bbced06"></span>
# Full sample code

This is the `main.dart` full sample code for reference:

```Dart
import 'package:Flutter/material.dart';
import 'package:Flutter/services.dart';

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
        colorScheme: ColorScheme.fromSeed(seedColor: Colors.deepPurple),
        useMaterial3: true,
      ),
      home: const MyHomePage(title: 'Flutter Demo Home Page'),
    );
  }
} 

class MyHomePage extends StatefulWidget {
  const MyHomePage({super.key, required this.title});

  final String title;

  @override
  State createState() => _MyHomePageState();
}

class _MyHomePageState extends State<MyHomePage> {

  void _recorderCounter() {
    setState(() {
      callNativeMethodWithMethodName("recoder");
    });
  }
  void _draftCounter() {
    setState(() {
      callNativeMethodWithMethodName("draft");
    });
  }
  static const platform = MethodChannel("effectOne.Flutter");
  Future<void> callNativeMethodWithMethodName(String methodName) async {
    try {
      await platform.invokeMethod(methodName);
    } on PlatformException catch (e) {
      print("Failed to call native method: ${e.message}");
    }
  }

  @override
  Widget build(BuildContext context) {
 
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
          
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            TextButton(
              onPressed: _recorderCounter,
              child: Text("Recorder"),
            ),

            TextButton(
              onPressed: () {
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
