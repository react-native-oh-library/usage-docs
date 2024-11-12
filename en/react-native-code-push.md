> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-code-push</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/microsoft/react-native-code-push">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20windows%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/microsoft/react-native-code-push/blob/master/LICENSE.md">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [Github address](https://github.com/react-native-oh-library/react-native-code-push)

## Pre-preparation

### code-push-cli

1. Clone the [code-push-cli](https://github.com/react-native-oh-library/code-push-cli) to the local host.
2. Run the `npm install` command in the code-push-cli directory.
3. Run the `npm run start` command in the code-push-cli directory to generate the `bin` directory.
4. npm install -g <code-push-cli directory>
5. Restart a terminal and run the `code-push -v` command. If the version number is displayed, the installation is successful.

Common commands for code-push-cli are as follows:

```
code-push -v
code-push login
code-push app list //List all apps under the account.
code-push app add <apppname> harmony react-native // Creating an Application
code-push release <AppName> <bundle.harmony.js> "< version number > "--description "<v1.0.0 test update >" -m //Packet sending command. Add -m to forcibly update the version. The asterisk (*) indicates all versions, for example, code-push release CodePush_Local ./bundle.harmony.js "*" --description "v1.0.0 Test Update"
```

### code-push-server

1. Clone the [code-push-server](https://github.com/react-native-oh-library/code-push-server) to the local host.
2. Run the `npm install` command in the code-push-server directory.
3. Install the MySQL and Redis.
4. Modifying the `code-push-server/src/core/config.ts` Configuration File
5. Run the `npm run dev` command in the code-push-server directory to generate the `bin` directory.
6. Run the `npm run start` command in the code-push-server directory to start the service.

## Installation and Usage

Find the matching version information in the release address of a third-party library and download an applicable .tgz package: [@react-native-oh-tpl/react-native-code-push Releases](https://github.com/react-native-oh-library/react-native-code-push/releases).

Go to the project directory and execute the following instruction:

> [!TIP] Replace the content with the path of the .tgz package at the comment sign (#).

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-code-push@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-code-push@file:#
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React, { Component } from "react";
import { View, Text, StyleSheet, TouchableOpacity } from "react-native";
import CodePush from "react-native-code-push";
class App extends Component<any, any> {
  constructor(props: any) {
    super(props);
    this.state = {
      syncMessage: "",
      progress: {},
    };
  }
  componentDidMount() {
    console.log("开始检查更新");
    this.syncImmediate(); //开始检查更新
  }
  syncImmediate() {
    CodePush.sync(
      {
        updateDialog: {
          appendReleaseDescription: true, //是否显示更新description，默认为false
          descriptionPrefix: "更新内容：", //更新说明的前缀。 默认是” Description:
          mandatoryContinueButtonLabel: "立即更新", //强制更新的按钮文字，默认为continue
          mandatoryUpdateMessage: "", //- 强制更新时，更新通知. Defaults to “An update is available that must be installed.”.
          optionalIgnoreButtonLabel: "稍后", //非强制更新时，取消按钮文字,默认是ignore
          optionalInstallButtonLabel: "后台更新", //非强制更新时，确认文字. Defaults to “Install”
          optionalUpdateMessage: "有新版本了，是否更新？", //非强制更新时，更新通知. Defaults to “An update is available. Would you like to install it?”.
          title: "更新提示", //要显示的更新通知的标题. Defaults to “Update available”.
        },
      },
      this.codePushStatusDidChange.bind(this),
      this.codePushDownloadDidProgress.bind(this)
    );
  }

  codePushStatusDidChange(syncStatus: string | number) {
    switch (syncStatus) {
      case CodePush.SyncStatus.CHECKING_FOR_UPDATE:
        this.setState({ syncMessage: "Checking for update." });
        break;
      case CodePush.SyncStatus.DOWNLOADING_PACKAGE:
        this.setState({
          syncMessage: "Downloading package.",
          progressModalVisible: true,
        });
        break;
      case CodePush.SyncStatus.AWAITING_USER_ACTION:
        this.setState({ syncMessage: "Awaiting user action." });
        break;
      case CodePush.SyncStatus.INSTALLING_UPDATE:
        this.setState({
          syncMessage: "Installing update.",
          progressModalVisible: true,
        });
        break;
      case CodePush.SyncStatus.UP_TO_DATE:
        this.setState({ syncMessage: "App up to date.", progress: false });
        break;
      case CodePush.SyncStatus.UPDATE_IGNORED:
        this.setState({
          syncMessage: "Update cancelled by user.",
          progress: false,
        });
        break;
      case CodePush.SyncStatus.UPDATE_INSTALLED:
        this.setState({
          syncMessage: "Update installed and will be applied on restart.",
          progress: false,
        });
        break;
      case CodePush.SyncStatus.UNKNOWN_ERROR:
        this.setState({
          syncMessage: "An unknown error occurred.",
          progress: false,
        });
        break;
    }
  }

  codePushDownloadDidProgress(progress: any) {
    this.setState({ progress });
  }

  render() {
    return (
      <View style={styles.container}>
        <Text style={styles.welcome}>欢迎使用热更新--test!</Text>
        <Text>SyncStatus: {this.state.syncMessage}</Text>
        <Text>{this.state.progressModalVisible.toString()}</Text>
        <TouchableOpacity onPress={this.syncImmediate.bind(this)}>
          <Text style={styles.syncButton}>Press for dialog-driven sync</Text>
        </TouchableOpacity>
      </View>
    );
  }
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    alignItems: "center",
    backgroundColor: "#F5FCFF",
    paddingTop: 10,
  },
  welcome: {
    fontSize: 20,
    textAlign: "center",
    margin: 10,
  },
  syncButton: {
    color: "green",
    fontSize: 17,
  },
});

let codePushOptions = { checkFrequency: CodePush.CheckFrequency.MANUAL };

export default CodePush(codePushOptions)(App);
```

## Use Codegen

If this repository has been adapted to `Codegen`, generate the bridge code of the third-party library by using the `Codegen`. For details, see [Codegen Usage Guide](/en/codegen.md).

## Link

Currently, HarmonyOS does not support AutoLink. Therefore, you need to manually configure the linking.

Open the `harmony` directory of the HarmonyOS project in DevEco Studio.

### 1. Adding the overrides Field to oh-package.json5 File in the Root Directory of the Project

```json
{
  ...
  "overrides": {
    "@rnoh/react-native-openharmony" : "./react_native_openharmony"
  }
}
```

### 2. Introducing Native Code

Currently, two methods are available:

Method 1 (recommended): Use the HAR file.

> [!TIP] The HAR file is stored in the `harmony` directory in the installation path of the third-party library.

Open `entry/oh-package.json5` file and add the following dependencies:

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/react-native-code-push": "file:../../node_modules/@react-native-oh-tpl/react-native-code-push/harmony/codePush.har"
  }
```

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Method 2: Directly link to the source code.

> [!TIP] For details, see [Directly Linking Source Code](/en/link-source-code.md).

### 3. Introducing CodePushPackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
  ...
+ import { CodePushPackage } from "@react-native-oh-tpl/react-native-code-push/ts";

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new CodePushPackage(ctx)
  ];
}
```

### 4. Introduce the comparingVersion method on the ArkTs side

Open `entry/src/main/ets/pages/index.ets` and invoke the comparingVersion method to compare the code-push version number to clear historical sandbox resources during installation.

```diff
+ import { comparingVersion } from "@react-native-oh-tpl/react-native-code-push";

@Entry
@Component
struct Index {

  aboutToAppear() {
+     comparingVersion(context);
  }
}
```

### 5. Running

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Modifying the `entry\src\main\ets\pages\Index.ets` file.

```diff
...
+ import common from '@ohos.app.ability.common';
+ import BuildProfile from 'BuildProfile';
+ let context = getContext(this) as common.UIAbilityContext;
+ interface CodePushConfig{
+  Staging:String;
+  Production:String;
+  ServerUrl:String;
+  PublicKey:String;
+ }
struct Index {
  @StorageLink('RNOHCoreContext') private rnohCoreContext: RNOHCoreContext | undefined = undefined
  @State shouldShow: boolean = false
  private logger!: RNOHLogger
+ bundlePath:string = 'bundle.harmony.js'
aboutToAppear() {
     ...
+   this.setCodeConfig()
    this.shouldShow = true
    stopTracing()
  }
+ setCodeConfig(){
+    const CodePushConfig: CodePushConfig = {
+      Staging:BuildProfile.Staging,
+      Production:BuildProfile.Production,
+      ServerUrl:BuildProfile.ServerUrl,
+      PublicKey:BuildProfile.PublicKey
+    }
+    AppStorage.SetOrCreate('CodePushConfig',CodePushConfig)
+  }
build() {
   Column() {
    ...
    RNApp({
    jsBundleProvider:new TraceJSBundleProviderDecorator(
            new AnyJSBundleProvider([
              new MetroJSBundleProvider(),
              // NOTE: to load the bundle from file, place it in
              // `/data/app/el2/100/base/com.rnoh.tester/files/bundle.harmony.js`
              // on your device. The path mismatch is due to app sandboxing on HarmonyOS
+              new FileJSBundleProvider(context.filesDir + '/Bundles/' + this.bundlePath),
              new FileJSBundleProvider('/data/storage/el2/base/files/bundle.harmony.js'),
              new ResourceJSBundleProvider(this.rnohCoreContext.uiAbilityContext.resourceManager, 'hermes_bundle.hbc'),
              new ResourceJSBundleProvider(this.rnohCoreContext.uiAbilityContext.resourceManager, 'bundle.harmony.js')
            ]),
            this.rnohCoreContext.logger),
    })

   }

}
```

Open `entry/build-profile.json5` and add configuration

```diff
{
  "apiType": 'stageMode',
  "buildOption": {
    "externalNativeOptions": {
      "path": "./src/main/cpp/CMakeLists.txt",
      "arguments": "",
      "cppFlags": "-s",
    },
+    "arkOptions": {
+      "buildProfileFields": {
+        "Staging": "", //Test Environment Key
+        "Production": "",//Production Environment Key
+        "ServerUrl": "",//Server address
+        "PublicKey": "PublicKey"
      }
    }
  },
  "targets": [
    {
      "name": "default",
      "runtimeOS": "HarmonyOS"
    },
    {
      "name": "ohosTest",
    }
  ]
}
```

Then build and run the code.

## Constraints

### Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/react-native-code-push Releases](https://github.com/react-native-oh-library/react-native-code-push/releases)

## API

| Name              | Description                                                                                                                                                                                                                                                                               | Type     | Required | Platform    | HarmonyOS Support |
| ----------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | -------- | ----------- | ----------------- |
| sync              | Sync method, automatic mode update                                                                                                                                                                                                                                                        | function | yes      | Android IOS | yes               |
| getUpdateMetadata | Retrieve the metadata of the currently installed updates (RemotePackage). When using the sync method, there is no need to call this method as sync will automatically call it                                                                                                             | function | no       | Android iOS | yes               |
| restartApp        | Restart the app. When using the sync method, there is no need to call this method because sync will automatically call it                                                                                                                                                                 | function | no       | Android iOS | yes               |
| getCurrentPackage | Get application version information. When using the sync method, there is no need to call this method because sync will automatically call it                                                                                                                                             | function | no       | Android iOS | yes               |
| getConfiguration  | Get application configuration information, appVersion (version number), deploymentKey (deploymentKey), serverless URL (server address), and client UniqueId (unique identifier). When using the sync method, there is no need to call this method because sync will automatically call it | function | no       | Android iOS | yes               |

**updateDialog**

When using the **CodePush.updateDialog** method, the following parameters are optional, representing the updated dialog box and default to null

| Name                         | Description                                                                                                 | Type    | Required | Platform    | HarmonyOS Support |
| ---------------------------- | ----------------------------------------------------------------------------------------------------------- | ------- | -------- | ----------- | ----------------- |
| appendReleaseDescription     | Whether to display update description, default is false                                                     | boolean | no       | Android iOS | yes               |
| descriptionPrefix            | Update the prefix of the description. The default is "Description:                                          | string  | no       | Android iOS | yes               |
| mandatoryContinueButtonLabel | The button text for forced updates defaults to continue                                                     | string  | no       | Android iOS | yes               |
| mandatoryUpdateMessage       | Update notifications when forced to update Defaults to “An update is available that must be installed.”     | string  | no       | Android iOS | yes               |
| optionalIgnoreButtonLabel    | When updateDialog is not forced to update, the cancel button text defaults to ignore                        | string  | no       | Android iOS | yes               |
| optionalInstallButtonLabel   | When non mandatory updates occur, confirm the text Defaults to “Install”                                    | string  | no       | Android iOS | yes               |
| optionalUpdateMessage        | Update notifications when not mandatory Defaults to “An update is available. Would you like to install it?” | string  | no       | Android iOS | yes               |
| title                        | The title of the update notification to be displayed Defaults to “Update available”.                        | string  | no       | Android iOS | yes               |

**SyncStatus**

When using **CodePush.SyncStatus**, the codePushStatus DidChange callback function retrieves the application status

| Name                 | Description                                                                                                                                                                                       | Type   | Required | Platform    | HarmonyOS Support |
| -------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------ | -------- | ----------- | ----------------- |
| UP_TO_DATE           | A value of 0 indicates that the application has been fully updated to the configured deployment,                                                                                                  | number | no       | Android iOS | yes               |
| UPDATE_INSTALLED     | A value of 1 indicates that an available update has been installed and will run immediately after the syncStatus ChangedCallback function returns or during the next application recovery/restart | number | no       | Android iOS | yes               |
| UNKNOWN_ERROR        | Value 3, unknown error detected during synchronization operation                                                                                                                                  | number | no       | Android iOS | yes               |
| CHECKING_FOR_UPDATE  | Value is 5, checking if there are any updates to the CodePush server                                                                                                                              | number | no       | Android iOS | yes               |
| AWAITING_USER_ACTION | The value is 6, there are updates available, and a confirmation dialog box is displayed to the end user. (Applicable only when used with updateDialog)                                            | number | no       | Android iOS | yes               |
| DOWNLOADING_PACKAGE  | A value of 7, available updates downloaded from CodePush server                                                                                                                                   | number | no       | Android iOS | yes               |
| INSTALLING_UPDATE    | Value is 8, available updates have been downloaded and will be installed                                                                                                                          | number | no       | Android iOS | yes               |

**installMode**

When using **CodePush.InstallMode**, the following parameters are optional: installMode

| Name            | Description        | Type   | Required | Platform    | HarmonyOS Support |
| --------------- | ------------------ | ------ | -------- | ----------- | ----------------- |
| IMMEDIATE       | Directly update    | number | no       | Android iOS | yes               |
| ON_NEXT_RESTART | Next update launch | number | no       | Android iOS | yes               |
| ON_NEXT_RESUME  | Next update launch | number | no       | Android iOS | yes               |
| ON_NEXT_SUSPEND | Next update launch | number | no       | Android iOS | yes               |

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/microsoft/react-native-code-push/blob/master/LICENSE.md).
