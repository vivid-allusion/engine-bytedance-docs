---
title: "Accessing TOS with Flutter SDK"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Access-tos-with-flutter-sdk"
---

Currently, the community supports TOS with the Flutter SDK, which is published on the pub.dev repository. You can use the Flutter SDK to access TOS for uploading and downloading resources. This article uses Android Studio as an example to explain the steps for accessing TOS with the Flutter SDK.

<span id="48fdf76b"></span>
## Prerequisites


* Flutter is installed. For details, refer to [Install Flutter](https://book.flutterchina.club/chapter1/install_flutter.html#.XzEtMy0xLeWuieijhWZsdXR0ZXI=).

* The Flutter and Dart plugins are installed in Android Studio. For details, refer to [Android Studio setup and usage](https://book.flutterchina.club/chapter1/install_flutter.html#.XzEtMy0yLWlkZemFjee9ruS4juS9v-eUqA==).


<span id="8910813c"></span>
## Procedure


1. Configure long\-term access credentials locally.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For detailed steps on obtaining Access Key ID and Secret Access Key, see <a href="https://docs.byteplus.com/docs/byteplus-platform/docs-managing-an-accesskey">Access Key Management</a>.   </div>
   

   
   <Tabs>
   <Tab zoneid="NrrFm4VXi1" title="macOS">
   <TabTitle>macOS</TabTitle>
   
   The steps to configure long\-term access credentials on macOS are as follows:
   
   
   1. Open Terminal and run the following command to open the file:
   
   
   ```Shell
   nano ~/.bash_profile
   ```
   
   
   
   2. Add the AK/SK information at the end of the file:
   
   
   ```Shell
   export TOS_ACCESS_KEY=AKTPYmI1Z****
   export TOS_SECRET_KEY=T1dJM01UU****
   ```
   
   
   
   3. Save the file and exit the editor.
   
   4. Run the following command to apply the configuration:
   
   
   ```Shell
   source ~/.bash_profile
   ```
   
   
   
   5. Run the following commands to verify the configuration:
   
   
   ```Shell
   echo $TOS_ACCESS_KEY
   echo $TOS_SECRET_KEY
   ```
   
   
   
   If the configuration is successful, the output will be similar to the following example:
   
   
   ```Shell
   AKTPYmI1Z****
   T1dJM01UU****
   ```
   
   
   
   </Tab>
   <Tab zoneid="edb8zYuuUa" title="Linux">
   <TabTitle>Linux</TabTitle>
   
   The steps to configure long\-term access credentials on Linux are as follows:
   
   
   1. Open the terminal and run the following command to open the file:
   
   
   ```Shell
   sudo vim /etc/profile
   ```
   
   
   
   2. Add the AK/SK information at the end of the file:
   
   
   ```Shell
   export TOS_ACCESS_KEY=AKTPYmI1Z****
   export TOS_SECRET_KEY=T1dJM01UU****
   ```
   
   
   
   3. Save the file and exit the editor.
   
   4. Run the following command to apply the configuration:
   
   
   ```Shell
   source /etc/profile
   ```
   
   
   
   5. Run the following commands to verify the configuration:
   
   
   ```Shell
   echo $TOS_ACCESS_KEY
   echo $TOS_SECRET_KEY
   ```
   
   
   If the configuration is successful, the output will be similar to the following example:
   
   ```Shell
   AKTPYmI1Z****
   T1dJM01UU****
   ```
   
   
   
   </Tab>
   <Tab zoneid="XoyGR9QWr7" title="Windows">
   <TabTitle>Windows</TabTitle>
   
   The steps to configure long\-term access credentials on Windows are as follows:
   
   
   1. Open the command\-line tool and run the following commands to set the AK/SK information:
   
   
   ```Shell
   set TOS_ACCESS_KEY=AKTPYmI1Z****
   set TOS_SECRET_KEY=T1dJM01UU****
   ```
   
   
   
   2. Run the following commands to permanently save the environment variables:
   
   
   ```Shell
   setx TOS_ACCESS_KEY "%TOS_ACCESS_KEY%"
   setx TOS_SECRET_KEY "%TOS_SECRET_KEY%"
   ```
   
   
   
   3. Restart the command\-line tool, then run the following commands to verify the configuration:
   
   
   ```Shell
   echo %TOS_ACCESS_KEY%
   echo %TOS_SECRET_KEY%
   ```
   
   
   If the configuration is successful, the output will be similar to the following example:
   
   ```Shell
   AKTPYmI1Z****
   T1dJM01UU****
   ```
   
   
   
   </Tab>
   </Tabs>
   

2. Run the following command to install the TOS Flutter SDK.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For detailed information about the TOS Flutter SDK, see <a href="https://pub.dev/packages/tos">tos package</a>.   </div>
   

   ```Dart
   flutter pub add tos
   ```
   

3. Access TOS using the Flutter SDK.

   Modify `region` and `endpoint` in the code below according to your needs, then run the code.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When setting the <code>endpoint</code> parameter, add <code>https://</code> before the domain name, for example,<code>https://tos-ap-southeast-1.bytepluses.com</code>.For detailed information about Endpoint, see <a href="https://docs.byteplus.com/docs/tos/docs-region-and-endpoint">Regions and endpoints</a>.</div>


```Dart
import 'dart:io' show Platform;
import 'package:tos/enum.dart';
import 'package:tos/exception.dart';
import 'package:tos/tos.dart';

void main() async {
    Map<String, String> envVars = Platform.environment;
    TosClient client = TosClientBuilder()
        .ak(envVars['TOS_ACCESS_KEY'] ?? '')
        .sk(envVars['TOS_SECRET_KEY'] ?? '')
        .region('ap-southeast-1')
        .endpoint('https://tos-ap-southeast-1.bytepluses.com')
        .build();

    var output = await client.listBuckets(ListBucketsInput());
    print(output.requestId);
    for(var bucket in output.buckets){
        print(bucket.name);
    }
    client.close();
}
```


If the bucket name is returned, it means accessing TOS with the Flutter SDK succeeded.

<span id="28c274df"></span>
## Related operations

You can also compile code independently to create buckets, delete objects, and perform other operations using the Flutter SDK. For more interface documentation, see [tos library](https://pub.dev/documentation/tos/latest/tos/).
