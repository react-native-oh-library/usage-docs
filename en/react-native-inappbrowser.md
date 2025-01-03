> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-inappbrowser-reborn</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/proyecto26/react-native-inappbrowser">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
        <a href="https://github.com/proyecto26/react-native-inappbrowser/blob/develop/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-inappbrowser)

## Installation and Usage

Find the matching version information in the release address of a third-party library: [@react-native-oh-tpl/react-native-inappbrowser-reborn Releases](https://github.com/react-native-oh-library/react-native-inappbrowser/releases).For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:



#### **npm**

```
npm install @react-native-oh-tpl/react-native-inappbrowser-reborn
```

#### **yarn**

```
yarn add @react-native-oh-tpl/react-native-inappbrowser-reborn
```

The following code shows the basic use scenario of the repository:

> [!TIP] The name of the imported repository remains unchanged.

```tsx
import React, { useState } from "react";
import {
  StyleSheet,
  Text,
  Button,
  ScrollView,
  View,
  StatusBarStyle,
} from "react-native";
import { InAppBrowser } from "react-native-inappbrowser-reborn";
import { tryDeepLinking, openLink } from "./utils";

export default function BrowserDemo() {
  const [text, setText] = useState("");
  const [url, setUrl] = useState("https://reactnative.dev");

  const onOpenLink = async () => {
    let resut = await openLink(url, {});
    setText(JSON.stringify(resut));
  };

  const onTryDeepLinking = async () => {
    let result = await tryDeepLinking();
    setText(JSON.stringify(result));
    return result;
  };

  const onIsAvailable = async () => {
    let isAvailable = await InAppBrowser.isAvailable();
    return isAvailable;
  };

  const close = () => {
    openLink(url, {});
    setTimeout(function () {
      console.info("-----------------");
      InAppBrowser.close();
    }, 10000);
  };

  const closeAuth = () => {
    tryDeepLinking();
    setTimeout(function () {
      console.info("-----------------");
      InAppBrowser.closeAuth();
    }, 10000);
  };

  const warmup = () => {
    InAppBrowser.warmup();
  };

  const mayLaunchUrl = () => {
    InAppBrowser.mayLaunchUrl(url, []);
  };

  return (
    <View style={styles.container}>
      <View style={styles.titleArea}>
        <Text style={styles.title}>BrowserDemo</Text>
      </View>
      <View style={styles.inputArea}>
        <Text style={styles.baseText}>{text}</Text>
      </View>
      <ScrollView style={styles.scrollView}>
        <View style={{ flexDirection: "column" }}>
          <View style={styles.baseArea}>
            <Text style={{ flex: 1 }}>onOpenLink</Text>
            <Button
              title="runing"
              color="#841584"
              onPress={onOpenLink}
            ></Button>
          </View>

          <View style={styles.baseArea}>
            <Text style={{ flex: 1 }}>onTryDeepLinking</Text>
            <Button
              title="runing"
              color="#841584"
              onPress={onTryDeepLinking}
            ></Button>
          </View>

          <View style={styles.baseArea}>
            <Text style={{ flex: 1 }}>onIsAvailable</Text>
            <Button
              title="runing"
              color="#841584"
              onPress={onIsAvailable}
            ></Button>
          </View>

          <View style={styles.baseArea}>
            <Text style={{ flex: 1 }}>close</Text>
            <Button title="runing" color="#841584" onPress={close}></Button>
          </View>

          <View style={styles.baseArea}>
            <Text style={{ flex: 1 }}>tryDeepLinking</Text>
            <Button
              title="runing"
              color="#841584"
              onPress={tryDeepLinking}
            ></Button>
          </View>

          <View style={styles.baseArea}>
            <Text style={{ flex: 1 }}>closeAuth</Text>
            <Button title="runing" color="#841584" onPress={closeAuth}></Button>
          </View>

          <View style={styles.baseArea}>
            <Text style={{ flex: 1 }}>warmup</Text>
            <Button title="runing" color="#841584" onPress={warmup}></Button>
          </View>

          <View style={styles.baseArea}>
            <Text style={{ flex: 1 }}>mayLaunchUrl</Text>
            <Button
              title="runing"
              color="#841584"
              onPress={mayLaunchUrl}
            ></Button>
          </View>
        </View>
      </ScrollView>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    width: "100%",
    height: "100%",
    flexDirection: "column",
    alignItems: "center",
    backgroundColor: "#F1F3F5",
  },
  baseText: {
    fontWeight: "bold",
    textAlign: "center",
    fontSize: 16,
  },

  titleArea: {
    width: "90%",
    height: "8%",
    alignItems: "center",
    flexDirection: "row",
  },

  title: {
    width: "90%",
    color: "#000000",
    textAlign: "left",
    fontSize: 30,
  },

  scrollView: {
    width: "90%",
    marginHorizontal: 20,
  },

  inputArea: {
    width: "90%",
    height: "10%",
    borderWidth: 2,
    borderColor: "#000000",
    marginTop: 8,
    justifyContent: "center",
    alignItems: "center",
  },
  baseArea: {
    width: "100%",
    height: 60,
    borderRadius: 4,
    borderColor: "#000000",
    marginTop: 8,
    backgroundColor: "#FFFFFF",
    flexDirection: "row",
    alignItems: "center",
    paddingLeft: 8,
    paddingRight: 8,
  },
});

import { Alert, Platform } from "react-native";
import { InAppBrowser } from "react-native-inappbrowser-reborn";

export interface options {
  dismissButtonStyle?: "done" | "close" | "cancel";
  preferredBarTintColor?: string;
  preferredControlTintColor?: string;
}

export const openLink = async (
  url: string,
  statusBarStyle: options,
  animated = true
) => {
  let result = await InAppBrowser.open(url, {
    dismissButtonStyle: statusBarStyle.dismissButtonStyle,
    preferredBarTintColor: statusBarStyle.preferredBarTintColor,
    preferredControlTintColor: statusBarStyle.preferredControlTintColor,
  });
  Alert.alert("Response", JSON.stringify(result));
  return result;
};

export const getDeepLink = (path = "") => {
  const scheme = "my-demo";
  const prefix =
    Platform.OS === "android" ? `${scheme}://demo/` : `${scheme}://`;
  return prefix + path;
};

export const tryDeepLinking = async () => {
  const loginUrl = "https://proyecto26.github.io/react-native-inappbrowser/";
  const redirectUrl = getDeepLink();
  const url = `${loginUrl}?redirect_url=${encodeURIComponent(redirectUrl)}`;
  try {
    if (await InAppBrowser.isAvailable()) {
      const result = await InAppBrowser.openAuth(url, redirectUrl, {
        // iOS Properties
        ephemeralWebSession: false,
      });
      //await sleep(800);
      return result;
    } else {
      return "InAppBrowser is not supported :/";
    }
  } catch (error) {
    console.error(error);
  }
  return "Something's wrong with the app";
};
```

## Use Codegen

If this repository has been adapted to `Codegen`, generate the bridge code of the third-party library by using the `Codegen`. For details, see [Codegen Usage Guide](/en/codegen.md).

## Link

Currently, HarmonyOS does not support AutoLink. Therefore, you need to manually configure the linking.

Open the `harmony` directory of the HarmonyOS project in DevEco Studio.

```
Adding the overrides Field to oh-package.json5 File in the Root Directory of the Project
{
  ...
  "overrides": {
    "@rnoh/react-native-openharmony" : "./react_native_openharmony"
  }
}
```

### 1. Configuring Entry

1. Create **BrowserManagerAbility.ets** in **entry/src/main/ets/entryability**.

```
import { AbilityConstant, UIAbility, Want } from '@kit.AbilityKit';
import { hilog } from '@kit.PerformanceAnalysisKit';
import { window } from '@kit.ArkUI';

export default class BrowserManagerAbility extends UIAbility {

  onCreate(want: Want, launchParam: AbilityConstant.LaunchParam): void {
    hilog.info(0x0000, 'testTag', '%{public}s', 'Ability onCreate');
  }

  onDestroy(): void {
    hilog.info(0x0000, 'testTag', '%{public}s', 'Ability onDestroy');
  }

  onWindowStageCreate(windowStage: window.WindowStage): void {
    // Main window is created, set main page for this ability
    hilog.info(0x0000, 'testTag', '%{public}s', 'Ability onWindowStageCreate');

    windowStage.loadContent('pages/BrowserManagerPage', (err) => {
      if (err.code) {
        hilog.error(0x0000, 'testTag', 'Failed to load the content. Cause: %{public}s', JSON.stringify(err) ?? '');
        return;
      }
      hilog.info(0x0000, 'testTag', 'Succeeded in loading the content.');
    });
  }

  onWindowStageDestroy(): void {
    // Main window is destroyed, release UI related resources
    hilog.info(0x0000, 'testTag', '%{public}s', 'Ability onWindowStageDestroy');
  }

  onForeground(): void {
    // Ability has brought to foreground
    hilog.info(0x0000, 'testTag', '%{public}s', 'Ability onForeground');
  }

  onBackground(): void {
    // Ability has back to background
    hilog.info(0x0000, 'testTag', '%{public}s', 'Ability onBackground');
  }
}

```

2. Register **BrowserManagerAbility** in **entry/src/main/module.json5**.

```
"abilities":[{
    "name": "BrowserManagerAbility",
    "srcEntry": "./ets/entryability/BrowserManagerAbility.ets",
    "description": "$string:EntryAbility_desc",
    "icon": "$media:icon",
    "startWindowIcon": "$media:startIcon",
    "startWindowBackground": "$color:start_window_background",
    "visible": true,
  }
...
]
```

3. Create **BrowserManagerPage.ets** in **entry/src/main/ets/pages**.

```
import { BrowserPage } from '@react-native-oh-tpl/react-native-inappbrowser-reborn/Index'

@Entry
@Component
struct ChromeTabsManagerPage {
  build() {
    Row(){
      Column(){
        BrowserPage();
      }
      .width('100%')
    }
    .height('100%')
  }

}
```

4. Add the following configuration to **entry/src/main/resources/base/profile/main_pages.json**:

```
{
 "src": [
  "pages/Index",
  "pages/BrowserManagerPage"
 ]
}
```

5. If you want to warm up the browser client in your application to accelerate its startup, add the following content to **BrowserManagerAbility**:

```
import { RNInAppBrowserModule } from '@react-native-oh-tpl/react-native-inappbrowser-reborn/ts';

export default class BrowserManagerAbility extends UIAbility {

  onCreate(want: Want, launchParam: AbilityConstant.LaunchParam): void {
    hilog.info(0x0000, 'testTag', '%{public}s', 'Ability onCreate');
    RNInAppBrowserModule.start();
  }
}
```

### 2. Introducing Native Code

Currently, two methods are available:

Method 1 (recommended): Use the HAR file.

> [!TIP] The HAR file is stored in the `harmony` directory in the installation path of the third-party library.

Open `entry/oh-package.json5` file and add the following dependencies:

```
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/react-native-inappbrowser-reborn": "file:../../node_modules/@react-native-oh-tpl/react-native-inappbrowser-reborn/harmony/inappbrowser.har"
  }
```

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```
cd entry
ohpm install
```

Method 2: Directly link to the source code.

> [!TIP] For details, see [Directly Linking Source Code](https://gitee.com/react-native-oh-library/usage-docs/blob/master/en/link-source-code.md).

### 3. Introducing RNInAppBrowserPackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
  ...
+ import { RNInAppBrowserPackage } from '@react-native-oh-tpl/react-native-inappbrowser-reborn/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNInAppBrowserPackage(ctx),
  ];
}
```

### 4. Running

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```
cd entry
ohpm install
```

Then build and run the code.

## Constraints

### Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/react-native-inappbrowser-reborn Releases](https://github.com/react-native-oh-library/react-native-inappbrowser/releases)

## API

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name         | Description                                                  | Type     | Required | Platform    | HarmonyOS Support |
| ------------ | ------------------------------------------------------------ | -------- | -------- | ----------- | ----------------- |
| open         | Opens the url with Safari in a modal on iOS using SFSafariViewController, and Chrome in a new custom tab on Android. On iOS, the modal Safari will not share cookies with the system Safari. | function | no       | iOS/Android | yes               |
| close        | Dismisses the system's presented web browser.                | function | no       | iOS/Android | yes               |
| openAuth     | Opens the url with Safari in a modal on iOS using SFAuthenticationSession/ASWebAuthenticationSession, and Chrome in a new custom tab on Android. On iOS, the user will be asked whether to allow the app to authenticate using the given url (OAuth flow with deep linking redirection). | function | no       | iOS/Android | yes               |
| closeAuth    | Dismisses the current authentication session.                | function | no       | iOS/Android | yes               |
| isAvailable  | Detect if the device supports this plugin.                   | function | no       | iOS/Android | yes               |
| onStart      | Initialize a bound background service so the application can communicate its intention to the browser. After the service is connected, the client can be used to Warms up the browser to make navigation faster and indicates that a given URL may be loaded in the future. - Android Only. | function | no       | Android     | yes               |
| warmup       | Warm up the browser process - Android Only.                  | function | no       | Android     | yes               |
| mayLaunchUrl | Tells the browser of a likely future navigation to a URL. The most likely URL has to be specified first. Optionally, a list of other likely URLs can be provided. They are treated as less likely than the first one, and have to be sorted in decreasing priority order. These additional URLs may be ignored. All previous calls to this method will be deprioritized - Android Only. | function | no       | Android     | yes               |

## Properties

**iOS Options**
| Name                          | Description                                                  | Type    | Required | Platform | HarmonyOS Support |
| ----------------------------- | ------------------------------------------------------------ | ------- | -------- | -------- | ----------------- |
| dismissButtonStyle            | The style of the dismiss button. [done/close/cancel]         | String  | NO       | iOS      | yes               |
| preferredBarTintColor         | The color to tint the background of the navigation bar and the toolbar. [white/#FFFFFF] | String  | NO       | iOS      | yes               |
| preferredControlTintColor     | The color to tint the control buttons on the navigation bar and the toolbar. [gray/#808080] | String  | NO       | iOS      | yes               |
| readerMode                    | A value that specifies whether Safari should enter Reader mode, if it is available. [true/false] | Boolean | NO       | iOS      | NO                |
| animated                      | Animate the presentation. [true/false]                       | Boolean | NO       | iOS      | NO                |
| modalPresentationStyle        | The presentation style for modally presented view controllers. [automatic/none/fullScreen/pageSheet/formSheet/currentContext/custom/overFullScreen/overCurrentContext/popover] | String  | NO       | iOS      | NO                |
| modalTransitionStyle          | The transition style to use when presenting the view controller. [coverVertical/flipHorizontal/crossDissolve/partialCurl] | String  | NO       | IOS      | NO                |
| modalEnabled                  | Present the SafariViewController modally or as push instead. [true/false] | Boolean | NO       | iOS      | NO                |
| enableBarCollapsing           | Determines whether the browser's tool bars will collapse or not. [true/false] | Boolean | NO       | iOS      | NO                |
| ephemeralWebSession           | Prevent re-use cookies of previous session (openAuth only) [true/false] | Boolean | NO       | iOS      | NO                |
| formSheetPreferredContentSize | Custom size for iPad formSheet modals [{width: 400, height: 500}] | Boolean | NO       | iOS      | NO                |

**Android Options**
| Name                      | Description                                                  | Type    | Required | Platform | HarmonyOS Support |
| ------------------------- | ------------------------------------------------------------ | ------- | -------- | -------- | ----------------- |
| showTitle                 | Sets whether the title should be shown in the custom tab. [true/false] | Boolean | NO       | Android  | NO                |
| toolbarColor              | Sets the toolbar color. [gray/#808080]                       | String  | NO       | Android  | NO                |
| secondaryToolbarColor     | Sets the color of the secondary toolbar. [white/#FFFFFF]     | String  | NO       | Android  | NO                |
| navigationBarColor        | Sets the navigation bar color. [gray/#808080]                | String  | NO       | Android  | NO                |
| navigationBarDividerColor | Sets the navigation bar divider color. [white/#FFFFFF]       | String  | NO       | Android  | NO                |
| enableUrlBarHiding        | Enables the url bar to hide as the user scrolls down on the page. [true/false] | String  | NO       | Android  | NO                |
| enableDefaultShare        | Adds a default share item to the menu. [true/false]          | String  | NO       | Android  | NO                |
| animations                | Sets the start and exit animations. [{ startEnter, startExit, endEnter, endExit }] | Object  | NO       | Android  | NO                |
| headers                   | The data are key/value pairs, they will be sent in the HTTP request headers for the provided url. [{ 'Authorization': 'Bearer ...' }] | Object  | NO       | Android  | NO                |
| forceCloseOnRedirection   | Open Custom Tab in a new task to avoid issues redirecting back to app scheme. [true/false] | Boolean | NO       | Android  | NO                |
| hasBackButton             | Sets a back arrow instead of the default X icon to close the custom tab. [true/false] | Boolean | NO       | Android  | NO                |
| browserPackage            | Package name of a browser to be used to handle Custom Tabs.  | Boolean | NO       | Android  | NO                |
| showInRecents             | Determining whether browsed website should be shown as separate entry in Android recents/multitasking view. [true/false] | Boolean | NO       | Android  | NO                |
| includeReferrer           | Determining whether to include your package name as referrer for the website to track. [true/false] | Boolean | NO       | Android  | NO                |

## Known Issues

- [ ] Failed to enable/disable the reading mode for the browser: [#1](https://github.com/react-native-oh-library/react-native-inappbrowser/issues/1)
- [ ] Failed to make the browser window open with an animation: [#2](https://github.com/react-native-oh-library/react-native-inappbrowser/issues/2)
- [ ] Failed to set the style of the web view controller for the browser: [#3](https://github.com/react-native-oh-library/react-native-inappbrowser/issues/3)
- [ ] Failed to set the browser's transition style: [#4](https://github.com/react-native-oh-library/react-native-inappbrowser/issues/4)
- [ ] Failed to set the browser's push mode: [#5](https://github.com/react-native-oh-library/react-native-inappbrowser/issues/5)
- [ ] Failed to collapse the toolbar for the browser: [#6](https://github.com/react-native-oh-library/react-native-inappbrowser/issues/6)
- [ ] Failed to specify whether to reuse the cookie of the previous session for the browser: [#7](https://github.com/react-native-oh-library/react-native-inappbrowser/issues/7)
- [ ] Failed to customize the size of the modal box for the browser: [#8](https://github.com/react-native-oh-library/react-native-inappbrowser/issues/8)

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/proyecto26/react-native-inappbrowser/blob/develop/LICENSE).
