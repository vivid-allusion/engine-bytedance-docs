---
title: "Configuring React Native projects in iOS"
product: "BytePlus Video Editor"
product_code: "video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/video-editor-sdk/150-configuring-react-native-projects-in-ios"
---

Configure a React Native (RN) project by adding buttons for shooting, drafts, and video collaboration.

<span id="51c0d84b"></span>
# **Prerequisities**

Before you begin with creating RN projects, ensure that the following requirements have been met:


* Downloaded Xcode.

* Retrieve your SDK package from your BytePlus representatives. For more information, refer to the [iOS package deliverables list](https://docs.byteplus.com/docs/video-editor-sdk/150-ios-package-deliverables-list).

* Set up your RN environment. For more information, refer to the [RN developers guide](https://reactnative.dev/docs/set-up-your-environment?platform=ios).

* Completed the steps in: [Creating React Native projects in iOS](https://docs.byteplus.com/docs/video-editor-sdk/150-creating-react-native-projects-in-ios).


<span id="6ac02285"></span>
# Code description

These are the main codes used when configuring the RN project.


* **RNEffectModule** is a class for interaction between React Native (RN) and native iOS code. It handles button clicks and communication with iOS.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d1558f32997944829b356ceb5021843b~tplv-goo7wpa0wc-image.image) </span>

* **reacNativeWithActionName** is a method for handling button clicks. It determines which button was clicked based on the parameters passed (Record, Draft, Duet).

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a72684216814472d9e2403518b9ac01d~tplv-goo7wpa0wc-image.image) </span>


<span id="b3492f3b"></span>
# Full sample code

The code defines a RN application with:


* A `Section` component for displaying content.

* An `App` component that:

   * Sets up the main application layout.

   * Integrates with a native module for iOS interactions.

   * Displays a status bar and buttons for user interaction.


```JavaScript
/**
 * Sample React Native App
 * https://github.com/facebook/react-native
 *
 * @format
 */

import React from 'react';
import type {PropsWithChildren} from 'react';
import {
  SafeAreaView,
  ScrollView,
  StatusBar,
  StyleSheet,
  Text,
  useColorScheme,
  View,
  Button,
  NativeModules, // RN and native interaction model
} from 'react-native';

import {
  Colors,
  DebugInstructions,
  Header,
  LearnMoreLinks, 
  ReloadInstructions,
} from 'react-native/Libraries/NewAppScreen';

import {
  RNLocalize,
} from 'react-native-localize';

type SectionProps = PropsWithChildren<{
  title: string;
}>;
<StatusBar barStyle="light-content" backgroundColor="#7b1fa2" />
function Section({children, title}: SectionProps): React.JSX.Element {
  const isDarkMode = useColorScheme() === 'dark';
  return (
    <View style={styles.sectionContainer}>

    </View>
  );
}

function App(): React.JSX.Element {
  const isDarkMode = useColorScheme() === 'dark';

  const backgroundStyle = {
    backgroundColor: isDarkMode ? Colors.darker : Colors.lighter,
  };
  // Construct the native interaction model
  const RNEffectModule = NativeModules.RNEffectModule;

  return (
    <SafeAreaView style={backgroundStyle}>
      <StatusBar
        barStyle={'light-content'}
        backgroundColor={backgroundStyle.backgroundColor}
      />
      <ScrollView
        contentInsetAdjustmentBehavior="automatic"
        style={backgroundStyle}>
        <Header />
        <View
          style={{
            backgroundColor: isDarkMode ? Colors.black : Colors.white,
          }}>

        </View>
        <View>
            
            <Button
                 // Record button
                 title="Record"
                 onPress={() => RNEffectModule.reactNativeWithActionName("Record")}
                 color="#f54343"
             />
            <Button
                  // Drafts button 
                  title="Draft" 
                  onPress={() => RNEffectModule.reactNativeWithActionName("Draft")}
                  backgroundColor="#999999"
             />
             <Button
                 // Duet button
                  title="Duet"
                  onPress={() => RNEffectModule.reactNativeWithActionName("Duet")}
                  backgroundColor="#666666"
              />
       </View>

      </ScrollView>
    </SafeAreaView>
  );
}

const styles = StyleSheet.create({
  sectionContainer: {
    marginTop: 32,
    paddingHorizontal: 24,
  },
  sectionTitle: {
    fontSize: 24,
    fontWeight: '600',
  },
  sectionDescription: {
    marginTop: 8,
    fontSize: 18,
    fontWeight: '400',
  },
  highlight: {
    fontWeight: '1700',
  },
});

export default App;
```
