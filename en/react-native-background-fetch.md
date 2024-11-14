> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-background-fetch</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/transistorsoft/react-native-background-fetch">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20|%20expo%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/transistorsoft/react-native-background-fetch/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-background-fetch)

## Installation and Usage

Find the matching version information in the release address of a third-party library: [@react-native-oh-tpl/react-native-background-fetch Releases](https://github.com/react-native-oh-library/react-native-background-fetch/releases).For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:



<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-background-fetch
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-background-fetch
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React from "react";
import {
  SafeAreaView,
  StyleSheet,
  ScrollView,
  View,
  Text,
  FlatList,
  StatusBar,
  Button,
} from "react-native";
import { Header, Colors } from "react-native/Libraries/NewAppScreen";
import BackgroundFetch from "react-native-background-fetch";
import {
  BackgroundFetchConfig,
  BackgroundFetchStatus,
  TaskConfig,
  NetworkType,
} from "react-native-background-fetch/src/RNBackgroundFetch";

function generateRandomString(length: number): string {
  let result = "";
  const characters =
    "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789";
  const charactersLength = characters.length;
  for (let i = 0; i < length; i++) {
    result += characters.charAt(Math.floor(Math.random() * charactersLength));
  }
  return result;
}

class App extends React.Component {
  constructor(props: {}) {
    super(props);
    this.state = {
      events: [],
    };
  }

  componentDidMount() {
    // Initialize BackgroundFetch ONLY ONCE when component mounts.
    this.initBackgroundFetch();
  }

  async initBackgroundFetch(options?: BackgroundFetchConfig) {
    // BackgroundFetch event handler.
    const onEvent = async (taskId: string) => {
      console.log("[BackgroundFetch] task: ", taskId);
      // Do your background work...
      await this.addEvent(taskId);
      // IMPORTANT:  You must signal to the OS that your task is complete.
      BackgroundFetch.finish(taskId);
    };

    // Timeout callback is executed when your Task has exceeded its allowed running-time.
    // You must stop what you're doing immediately BackgroundFetch.finish(taskId)
    const onTimeout = async (taskId: string) => {
      console.warn("[BackgroundFetch] TIMEOUT task: ", taskId);
      BackgroundFetch.finish(taskId);
    };

    // Initialize BackgroundFetch only once when component mounts.
    let status = await BackgroundFetch.configure(
      { minimumFetchInterval: 20, ...options },
      onEvent,
      onTimeout
    );
  }

  scheduleTask(taskId: string, options?: TaskConfig) {
    BackgroundFetch.scheduleTask({
      taskId,
      delay: 20 * 60 * 1000, // <-- milliseconds
      ...options,
    });
  }

  // Add a BackgroundFetch event to <FlatList>
  addEvent(taskId: string) {
    // Simulate a possibly long-running asynchronous task with a Promise.
    return new Promise((resolve, reject) => {
      this.setState((state) => ({
        events: [
          ...state.events,
          {
            taskId: taskId,
            timestamp: new Date().toString(),
          },
        ],
      }));
      resolve(true);
    });
  }

  render() {
    return (
      <>
        <StatusBar barStyle="dark-content" />
        <SafeAreaView>
          <ScrollView
            contentInsetAdjustmentBehavior="automatic"
            style={styles.scrollView}
          >
            <Header />
            <View style={styles.body}>
              <View style={styles.sectionContainer}>
                <Text style={styles.sectionTitle}>BackgroundFetch Demo</Text>
              </View>
            </View>
          </ScrollView>
          <View style={styles.sectionContainer}>
            <FlatList
              data={this.state.events}
              renderItem={({ item }) => (
                <Text>
                  [{item.taskId}]: {item.timestamp}
                </Text>
              )}
              keyExtractor={(item) => generateRandomString(10)}
            />
          </View>
        </SafeAreaView>
      </>
    );
  }
}

const styles = StyleSheet.create({
  scrollView: {
    backgroundColor: Colors.lighter,
  },
  body: {
    backgroundColor: Colors.white,
  },
  sectionContainer: {
    marginTop: 32,
    paddingHorizontal: 24,
  },
  sectionTitle: {
    fontSize: 24,
    fontWeight: "600",
    color: Colors.black,
  },
  sectionDescription: {
    marginTop: 8,
    fontSize: 18,
    fontWeight: "400",
    color: Colors.dark,
  },
});

export default App;
```

## Use Codegen

If this repository has been adapted to `Codegen`, generate the bridge code of the third-party library by using the `Codegen`. For details, see [Codegen Usage Guide](/en/codegen.md).

## Link

Currently, HarmonyOS does not support AutoLink. Therefore, you need to manually configure the linking.

Open the `harmony` directory of the HarmonyOS project in DevEco Studio.

### Adding the overrides Field to oh-package.json5 File in the Root Directory of the Project

```json
{
  ...
  "overrides": {
    "@rnoh/react-native-openharmony" : "./react_native_openharmony"
  }
}
```

### Introducing Native Code

Currently, two methods are available:

Method 1 (recommended): Use the HAR file.

> [!TIP] The HAR file is stored in the `harmony` directory in the installation path of the third-party library.

Open `entry/oh-package.json5` file and add the following dependencies:

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/react-native-background-fetch": "file:../../node_modules/@react-native-oh-tpl/react-native-background-fetch/harmony/background_fetch.har"
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

### Introducing RNBackgroundFetchPackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
  ...
+ import { RNBackgroundFetchPackage } from "@react-native-oh-tpl/react-native-background-fetch/ts";

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNBackgroundFetchPackage(ctx)
  ];
}
```

### Introducing RNBackgroundFetchExtensionAbility to ArkTS

1. 打开 `entry/src/main/ets`，新建目录及 ArkTS 文件，新建一个目录并命名为 WorkSchedulerExtension。在 WorkSchedulerExtension 目录下，新建一个 ArkTS 文件并命名为 WorkSchedulerExtension.ets，用以实现延迟任务回调接口。

```js
import { workScheduler } from "@kit.BackgroundTasksKit";
import RNBackgroundFetchExtensionAbility from "@react-native-oh-tpl/react-native-background-fetch/src/main/ets/WorkSchedulerExtension/WorkSchedulerExtension";

export default class MyWorkSchedulerExtensionAbility extends RNBackgroundFetchExtensionAbility {
  onWorkStart(workInfo: workScheduler.WorkInfo) {
    super.onWorkStart(workInfo);
  }

  onWorkStop(workInfo: workScheduler.WorkInfo) {
    super.onWorkStop(workInfo);
  }
}
```

2. 在`entry/src/main/module.json5`配置文件中注册 WorkSchedulerExtensionAbility，并设置如下标签：

```json
{
  "module": {
    "extensionAbilities": [
      {
        "name": "MyWorkSchedulerExtensionAbility",
        "srcEntry": "./ets/WorkSchedulerExtension/WorkSchedulerExtension.ets",
        "type": "workScheduler"
      }
    ]
  }
}
```

### Running

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Then build and run the code.

## Constraints

### Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/react-native-background-fetch Releases](https://github.com/react-native-oh-library/react-native-background-fetch/releases)

## API

### BackgroundFetch

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name         | Description                                                                                                                                 | Type     | Params | Required | Platform | HarmonyOS Support |
| ------------ | ------------------------------------------------------------------------------------------------------------------------------------------- | -------- | ------ | -------- | -------- | ----------------- |
| configure    | Initial configuration of BackgroundFetch, including config-options and Fetch-callback. The [[start]] method will automatically be executed. | Function | no     | yes      | all      | partially         |
| scheduleTask | Add an extra fetch event listener in addition to the one initially provided to [[configure]].                                               | Function | no     | no       | all      | partially         |
| start        | Start subscribing to fetch events.                                                                                                          | Function | no     | no       | all      | yes               |
| stop         | Stop subscribing to fetch events.                                                                                                           | Function | no     | no       | all      | yes               |
| finish       | You must execute [[finish]] within your fetch-callback to signal completion of your task.                                                   | Function | no     | no       | all      | yes               |
| status       | Query the BackgroundFetch API status                                                                                                        | Function | no     | no       | all      | yes               |

### BackgroundFetch.configure()

```js
BackgroundFetch.configure(config: BackgroundFetchConfig, onEvent: (taskId:string) => void, onTimeout?:(taskId:string) => void): Promise<BackgroundFetchStatus>;
```

| Name                                          | Description                                                                                                                                                                                                  | Type          | Required | Platform | HarmonyOS Support |
| --------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------- | -------- | -------- | ----------------- |
| `BackgroundFetchConfig.minimumFetchInterval`  | The minimum interval in minutes to execute background fetch events. Defaults to 15 minutes. Minimum is 15 minutes.                                                                                           | `number`      | no       | all      | yes               |
| `BackgroundFetchConfig.stopOnTerminate`       | [Android only] Set false to continue background-fetch events after user terminates the app. Default to true.                                                                                                 | `boolean`     | no       | Android  | no                |
| `BackgroundFetchConfig.startOnBoot`           | [Android only] Set true to initiate background-fetch events when the device is rebooted. Defaults to false.                                                                                                  | `boolean`     | no       | Android  | no                |
| `BackgroundFetchConfig.enableHeadless`        | [Android only] Set true to enable Headless mechanism for handling fetch events after app termination.                                                                                                        | `boolean`     | no       | Android  | no                |
| `BackgroundFetchConfig.forceAlarmManager`     | [Android only] By default, the plugin will use Android's JobScheduler when possible. The JobScheduler API prioritizes for battery-life, throttling task-execution based upon device usage and battery level. | `boolean`     | no       | Android  | no                |
| `BackgroundFetchConfig.requiredNetworkType`   | [Android only] Set detailed description of the kind of network your job requires.                                                                                                                            | `NetworkType` | no       | Android  | partially         |
| `BackgroundFetchConfig.requiresBatteryNotLow` | [Android only] Specify that to run this job, the device's battery level must not be low.                                                                                                                     | `boolean`     | no       | Android  | yes               |
| `BackgroundFetchConfig.requiresStorageNotLow` | [Android only] Specify that to run this job, the device's available storage must not be low.                                                                                                                 | `boolean`     | no       | Android  | yes               |
| `BackgroundFetchConfig.requiresCharging`      | [Android only] Specify that to run this job, the device must be charging (or be a non-battery-powered device connected to permanent power, such as Android TV devices).                                      | `boolean`     | no       | Android  | yes               |
| `BackgroundFetchConfig.requiresDeviceIdle`    | [Android only] When set true, ensure that this job will not run if the device is in active use.                                                                                                              | `boolean`     | no       | Android  | yes               |

### BackgroundFetch.scheduleTask()

```js
BackgroundFetch.scheduleTask(config: TaskConfig): Promise<boolean>;
```

| Name                                     | Description                                                                                                                                                                                                  | Type          | Required | Platform | HarmonyOS Support |
| ---------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------- | -------- | -------- | ----------------- |
| `TaskConfig.taskId`                      | The name of the task.                                                                                                                                                                                        | `string`      | yes      | all      | yes               |
| `TaskConfig.delay`                       | The minimum interval in milliseconds to execute this task.                                                                                                                                                   | `number`      | yes      | all      | yes               |
| `TaskConfig.periodic`                    | Whether this task will continue executing or just a "one-shot".                                                                                                                                              | `boolean`     | no       | all      | yes               |
| `TaskConfig.requiresNetworkConnectivity` | When set true, ensure that this job will run if the device has network connection                                                                                                                            | `boolean`     | no       | all      | no                |
| `TaskConfig.stopOnTerminate`             | [Android only] Set false to continue background-fetch events after user terminates the app. Default to true.                                                                                                 | `boolean`     | no       | Android  | no                |
| `TaskConfig.startOnBoot`                 | [Android only] Set true to initiate background-fetch events when the device is rebooted. Defaults to false.                                                                                                  | `boolean`     | no       | Android  | no                |
| `TaskConfig.enableHeadless`              | [Android only] Set true to enable Headless mechanism for handling fetch events after app termination.                                                                                                        | `boolean`     | no       | Android  | no                |
| `TaskConfig.forceAlarmManager`           | [Android only] By default, the plugin will use Android's JobScheduler when possible. The JobScheduler API prioritizes for battery-life, throttling task-execution based upon device usage and battery level. | `boolean`     | no       | Android  | no                |
| `TaskConfig.requiredNetworkType`         | [Android only] Set detailed description of the kind of network your job requires.                                                                                                                            | `NetworkType` | no       | Android  | partially         |
| `TaskConfig.requiresBatteryNotLow`       | [Android only] Specify that to run this job, the device's battery level must not be low.                                                                                                                     | `boolean`     | no       | Android  | yes               |
| `TaskConfig.requiresStorageNotLow`       | [Android only] Specify that to run this job, the device's available storage must not be low.                                                                                                                 | `boolean`     | no       | Android  | yes               |
| `TaskConfig.requiresCharging`            | [Android only] Specify that to run this job, the device must be charging (or be a non-battery-powered device connected to permanent power, such as Android TV devices).                                      | `boolean`     | no       | Android  | yes               |
| `TaskConfig.requiresDeviceIdle`          | [Android only] When set true, ensure that this job will not run if the device is in active use.                                                                                                              | `boolean`     | no       | Android  | yes               |

### BackgroundFetch.stop()

```js
BackgroundFetch.stop(taskId?: string): Promise<boolean>;
```

| Name     | Description           | Type     | Required | Platform | HarmonyOS Support |
| -------- | --------------------- | -------- | -------- | -------- | ----------------- |
| `taskId` | The name of the task. | `string` | no       | all      | yes               |

### BackgroundFetch.finish()

```js
BackgroundFetch.finish(taskId: string): void;
```

| Name     | Description           | Type     | Required | Platform | HarmonyOS Support |
| -------- | --------------------- | -------- | -------- | -------- | ----------------- |
| `taskId` | The name of the task. | `string` | yes      | all      | yes               |

### BackgroundFetch.status()

```js
BackgroundFetch.status(callback?: (status: BackgroundFetchStatus) => void): Promise<BackgroundFetchStatus>;
```

| Name       | Description                           | Type       | Required | Platform | HarmonyOS Support |
| ---------- | ------------------------------------- | ---------- | -------- | -------- | ----------------- |
| `callback` | Query the BackgroundFetch API status. | `Function` | no       | all      | yes               |

### BackgroundFetchStatus

| Name                                      | Description                                                                                                                                                                   | Type                    | Required | Platform | HarmonyOS Support |
| ----------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------- | -------- | -------- | ----------------- |
| `BackgroundFetchStatus.STATUS_RESTRICTED` | Background fetch updates are unavailable and the user cannot enable them again. For example, this status can occur when parental controls are in effect for the current user. | `BackgroundFetchStatus` | yes      | iOS      | no                |
| `BackgroundFetchStatus.STATUS_DENIED`     | The user explicitly disabled background behavior for this app or for the whole system.                                                                                        | `BackgroundFetchStatus` | yes      | iOS      | no                |
| `BackgroundFetchStatus.STATUS_AVAILABLE`  | Background fetch is available and enabled.                                                                                                                                    | `BackgroundFetchStatus` | yes      | all      | yes               |

## Known Issues

- [ ] configure 接口部分参数不支持 harmonyOS。[issue#2](https://github.com/react-native-oh-library/react-native-background-fetch/issues/2)
- [ ] scheduleTask 接口部分参数不支持 harmonyOS。[issue#4](https://github.com/react-native-oh-library/react-native-background-fetch/issues/4)

## Others

- iOS 可能需要数天的时间才能启动机器学习算法并开始触发常规事件。同时，您应该定期将应用程序带到前台，以使用用户的行为训练 iOS 机器学习算法。之后 iOS 才会定期执行任务。
- Android 中，不需要机器算法介入，configure 函数可以每 15 分钟调用一次，scheduleTask 可以最低每隔 1 分钟调用一次。
- HarmonyOS 中，系统会根据内存、功耗、设备温度、用户使用习惯等统一调度，如当系统内存资源不足或温度达到一定挡位时，系统将延迟调度该任务。假如你设置 20 分钟后执行，第一次任务不一定是 20 分钟就会执行，有可能十几分钟就执行了，往后的任务得起码 2 小时以后才会执行，更多详情请查看下面的链接内容。https://developer.huawei.com/consumer/cn/doc/harmonyos-guides-V5/work-scheduler-V5

## License

This project is licensed under [The MIT License (MIT)](https://github.com/transistorsoft/react-native-background-fetch/blob/master/LICENSE).
