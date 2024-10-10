> 模板版本：v0.2.2

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

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-inappbrowser)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-inappbrowser-reborn Releases](https://github.com/react-native-oh-library/react-native-inappbrowser/releases)，并下载适用版本的 tgz 包。

进入到工程目录并输入以下命令：

> [!TIP] #处替换为tgz包的路径

#### **npm**

```
npm install @react-native-oh-tpl/react-native-inappbrowser-reborn@file:#
```

#### **yarn**

```
yarn add @react-native-oh-tpl/react-native-inappbrowser-reborn@file:#
```

下面的代码展示了这个库的基本使用场景：

> [!TIP] 使用时 import 的库名不变。

```
import React, {useState } from 'react';
import {  StyleSheet, Text, Button ,ScrollView,View,StatusBarStyle,} from 'react-native';
import {InAppBrowser} from 'react-native-inappbrowser-reborn'
import {tryDeepLinking,openLink} from './utils'

export default function BrowserDemo() {
  const [text, setText] = useState('');
  const [url, setUrl] = useState('https://reactnative.dev');

  const onOpenLink = async() => {
    let resut = await openLink(url,{});
    setText(JSON.stringify(resut))
  }

  const onTryDeepLinking = async() => {
    let result = await tryDeepLinking();
    setText(JSON.stringify(result))
    return result;
  }

  const onIsAvailable = async () => {
    let isAvailable = await InAppBrowser.isAvailable();
    return isAvailable
  }

  const close =() => {
    openLink(url, {});
    setTimeout(function(){
      console.info('-----------------')
      InAppBrowser.close();
    },10000)
  }

  const closeAuth =() => {
    tryDeepLinking();
    setTimeout(function(){
      console.info('-----------------')
      InAppBrowser.closeAuth();
    },10000)
  }

  const warmup = () => {
    InAppBrowser.warmup();
  }

  const mayLaunchUrl = () => {
    InAppBrowser.mayLaunchUrl(url,[]);
  }
  
  return (
    <View style={styles.container}>
      <View style={styles.titleArea}>
        <Text style = {styles.title}>BrowserDemo</Text>
      </View>
      <View style = {styles.inputArea}>
        <Text style={styles.baseText}>
          {text}
        </Text>
      </View>
      <ScrollView style={styles.scrollView}>
        <View style={ { flexDirection: 'column'}}>
          <View style ={styles.baseArea}>
             <Text style= {{flex:1}}>onOpenLink</Text>
             <Button title='运行' color='#841584' onPress={onOpenLink}></Button>
          </View>

          <View style ={styles.baseArea}>
             <Text style= {{flex:1}}>onTryDeepLinking</Text>
             <Button title='运行' color='#841584' onPress={onTryDeepLinking}></Button>
          </View>

          <View style ={styles.baseArea}>
             <Text style= {{flex:1}}>onIsAvailable</Text>
             <Button title='运行' color='#841584' onPress={onIsAvailable}></Button>
          </View>

          <View style ={styles.baseArea}>
             <Text style= {{flex:1}}>close</Text>
             <Button title='运行' color='#841584' onPress={close}></Button>
          </View>

          <View style ={styles.baseArea}>
             <Text style= {{flex:1}}>tryDeepLinking</Text>
             <Button title='运行' color='#841584' onPress={tryDeepLinking}></Button>
          </View>

          <View style ={styles.baseArea}>
             <Text style= {{flex:1}}>closeAuth</Text>
             <Button title='运行' color='#841584' onPress={closeAuth}></Button>
          </View>

          <View style ={styles.baseArea}>
             <Text style= {{flex:1}}>warmup</Text>
             <Button title='运行' color='#841584' onPress={warmup}></Button>
          </View>

          <View style ={styles.baseArea}>
             <Text style= {{flex:1}}>mayLaunchUrl</Text>
             <Button title='运行' color='#841584' onPress={mayLaunchUrl}></Button>
          </View>
        </View>
      </ScrollView>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    width: '100%',
    height: '100%',
    flexDirection: 'column',
    alignItems: 'center',
    backgroundColor: '#F1F3F5',
  }, 
  baseText: {
    fontWeight: 'bold',
    textAlign:'center',
    fontSize:16
  },

  titleArea:{
    width:'90%',
    height:'8%',
    alignItems:'center',
    flexDirection:'row',
  },

  title: {
    width:'90%',
    color:'#000000',
    textAlign:'left',
    fontSize: 30,
  },

  scrollView: {
    width:'90%',
    marginHorizontal: 20,
  },

  inputArea: {
    width:'90%',
    height:'10%',
    borderWidth:2,
    borderColor:'#000000',
    marginTop:8,
    justifyContent:'center',
    alignItems:'center',
  },
  baseArea: {
    width:'100%',
    height:60,
    borderRadius:4,
    borderColor:'#000000',
    marginTop:8,
    backgroundColor:'#FFFFFF',
    flexDirection: 'row',
    alignItems:'center',
    paddingLeft:8,
    paddingRight:8
  }

});

import {Alert,Platform,} from 'react-native';
import {InAppBrowser} from 'react-native-inappbrowser-reborn'

export interface options {
  dismissButtonStyle?: 'done' | 'close' | 'cancel',
  preferredBarTintColor?:string,
  preferredControlTintColor?:string
}

export const openLink = async (
url: string,
statusBarStyle: options,
animated = true,
) => {
    let result  = await InAppBrowser.open(
        url,
        {
          dismissButtonStyle:statusBarStyle.dismissButtonStyle,
          preferredBarTintColor:statusBarStyle.preferredBarTintColor,
          preferredControlTintColor:statusBarStyle.preferredControlTintColor
        }
    );
    Alert.alert('Response', JSON.stringify(result));
    return result;
}

export const getDeepLink = (path = '') => {
    const scheme = 'my-demo';
    const prefix =
      Platform.OS === 'android' ? `${scheme}://demo/` : `${scheme}://`;
    return prefix + path;
};

export const tryDeepLinking = async () => {
    const loginUrl = 'https://proyecto26.github.io/react-native-inappbrowser/';
    const redirectUrl = getDeepLink();
    const url = `${loginUrl}?redirect_url=${encodeURIComponent(redirectUrl)}`;
    try {
      if (await InAppBrowser.isAvailable()) {
        const result = await InAppBrowser.openAuth(url, redirectUrl, {
          // iOS Properties
          ephemeralWebSession: false,
        });
        //await sleep(800);
        return result
      } else {
        return 'InAppBrowser is not supported :/'
      }
    } catch (error) {
      console.error(error);
    }
    return 'Something’s wrong with the app'
};
```

## 使用 Codegen

本库已经适配了 `Codegen` ，在使用前需要主动执行生成三方库桥接代码，详细请参考[ Codegen 使用文档](/zh-cn/codegen.md)。

## Link

目前 HarmonyOS 暂不支持 AutoLink，所以 Link 步骤需要手动配置。

首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 harmony

```
在工程根目录的 oh-package.json 添加 overrides字段
{
  ...
  "overrides": {
    "@rnoh/react-native-openharmony" : "./react_native_openharmony"
  }
}
```

### 1.配置Entry

**1.在 entry/src/main/ets/entryability 下创建 BrowserManagerAbility.ets**

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

**2.在 entry/src/main/module.json5注册BrowserManagerAbility**

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

**3.在 entry/src/main/ets/pages 下创建 BrowserManagerPage.ets**

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

**4.在 entry/src/main/resources/base/profile/main_pages.json 添加配置**

```
{
 "src": [
  "pages/Index",
  "pages/BrowserManagerPage"
 ]
}
```

**5.如果需要预热应用内浏览器客户端，使其启动速度显著加快，可以将以下内容添加到BrowserManagerAbility**

```
import { RNInAppBrowserModule } from '@react-native-oh-tpl/react-native-inappbrowser-reborn/ts';

export default class BrowserManagerAbility extends UIAbility {

  onCreate(want: Want, launchParam: AbilityConstant.LaunchParam): void {
    hilog.info(0x0000, 'testTag', '%{public}s', 'Ability onCreate');
    RNInAppBrowserModule.start();
  }
}
```

### 2.引入原生端代码

目前有两种方法：

1. 通过 har 包引入。
2. 直接链接源码。

方法一：通过 har 包引入 (推荐)

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/react-native-inappbrowser-reborn": "file:../../node_modules/@react-native-oh-tpl/react-native-inappbrowser-reborn/harmony/inappbrowser.har"
  }
```

点击右上角的 `sync` 按钮

或者在终端执行：

```
cd entry
ohpm install
```

方法二：直接链接源码

> [!TIP] 如需使用直接链接源码，请参考[直接链接源码说明](https://gitee.com/react-native-oh-library/usage-docs/blob/master/zh-cn/link-source-code.md)

### 3.在 ArkTs 侧引入 RNInAppBrowserPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

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

### 4.运行

点击右上角的 `sync` 按钮

或者在终端执行：

```
cd entry
ohpm install
```

然后编译、运行即可。

## 约束与限制

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-native-inappbrowser-reborn Releases](https://github.com/react-native-oh-library/react-native-inappbrowser/releases)

## API

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name        | Description                                                  | Type     | Required | Platform    | HarmonyOS Support |
| ----------- | ------------------------------------------------------------ | -------- | -------- | ----------- | ----------------- |
| open  | Opens the url with Safari in a modal on iOS using SFSafariViewController, and Chrome in a new custom tab on Android. On iOS, the modal Safari will not share cookies with the system Safari.                      | function | no       | iOS/Android | yes               |
| close       | Dismisses the system's presented web browser. | function | no       | iOS/Android | yes               |
| openAuth |Opens the url with Safari in a modal on iOS using SFAuthenticationSession/ASWebAuthenticationSession, and Chrome in a new custom tab on Android. On iOS, the user will be asked whether to allow the app to authenticate using the given url (OAuth flow with deep linking redirection).                                       | function | no       | iOS/Android | yes               |
| closeAuth | Dismisses the current authentication session.                                  | function | no       | iOS/Android | yes               |
| isAvailable  | Detect if the device supports this plugin.                                           | function | no       | iOS/Android | yes               |
| onStart  | Initialize a bound background service so the application can communicate its intention to the browser. After the service is connected, the client can be used to Warms up the browser to make navigation faster and indicates that a given URL may be loaded in the future. - Android Only.                                           | function | no       | Android | yes               |
| warmup  | Warm up the browser process - Android Only.                                           | function | no       | Android | yes               |
| mayLaunchUrl  | Tells the browser of a likely future navigation to a URL. The most likely URL has to be specified first. Optionally, a list of other likely URLs can be provided. They are treated as less likely than the first one, and have to be sorted in decreasing priority order. These additional URLs may be ignored. All previous calls to this method will be deprioritized - Android Only.                                          | function | no       | Android | yes               |

## 属性
**iOS Options**
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| dismissButtonStyle  | The style of the dismiss button. [done/close/cancel]         | String  | NO | iOS      | yes |
| preferredBarTintColor  | The color to tint the background of the navigation bar and the toolbar. [white/#FFFFFF]         | String  | NO | iOS      | yes |
| preferredControlTintColor  | The color to tint the control buttons on the navigation bar and the toolbar. [gray/#808080]         | String  | NO | iOS      | yes |
| readerMode   | A value that specifies whether Safari should enter Reader mode, if it is available. [true/false]         | Boolean  | NO | iOS      | NO |
| animated    | Animate the presentation. [true/false]        | Boolean  | NO | iOS      | NO |
| modalPresentationStyle     | The presentation style for modally presented view controllers. [automatic/none/fullScreen/pageSheet/formSheet/currentContext/custom/overFullScreen/overCurrentContext/popover]        | String  | NO | iOS      | NO |
| modalTransitionStyle      | The transition style to use when presenting the view controller. [coverVertical/flipHorizontal/crossDissolve/partialCurl]        | String  | NO | IOS      | NO |
| modalEnabled       | Present the SafariViewController modally or as push instead. [true/false]       | Boolean  | NO | iOS      | NO |
| enableBarCollapsing        | Determines whether the browser's tool bars will collapse or not. [true/false]       | Boolean  | NO | iOS      | NO |
| ephemeralWebSession         | Prevent re-use cookies of previous session (openAuth only) [true/false]       | Boolean  | NO | iOS      | NO |
| formSheetPreferredContentSize          | Custom size for iPad formSheet modals [{width: 400, height: 500}]       | Boolean  | NO | iOS      | NO |

**Android  Options**
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| showTitle   | Sets whether the title should be shown in the custom tab. [true/false]         | Boolean  | NO | Android      | NO |
| toolbarColor    | Sets the toolbar color. [gray/#808080]         | String  | NO | Android      | NO |
| secondaryToolbarColor     | Sets the color of the secondary toolbar. [white/#FFFFFF]         | String  | NO | Android      | NO |
| navigationBarColor      | Sets the navigation bar color. [gray/#808080]         | String  | NO | Android      | NO |
| navigationBarDividerColor       | Sets the navigation bar divider color. [white/#FFFFFF]         | String  | NO | Android      | NO |
| enableUrlBarHiding        | Enables the url bar to hide as the user scrolls down on the page. [true/false]         | String  | NO | Android      | NO |
| enableDefaultShare         | Adds a default share item to the menu. [true/false]         | String  | NO | Android      | NO |
| animations          | Sets the start and exit animations. [{ startEnter, startExit, endEnter, endExit }]         | Object  | NO | Android      | NO |
| headers           | The data are key/value pairs, they will be sent in the HTTP request headers for the provided url. [{ 'Authorization': 'Bearer ...' }]         | Object  | NO | Android      | NO |
| forceCloseOnRedirection            | Open Custom Tab in a new task to avoid issues redirecting back to app scheme. [true/false]         | Boolean  | NO | Android      | NO |
| hasBackButton             | Sets a back arrow instead of the default X icon to close the custom tab. [true/false]         | Boolean  | NO | Android      | NO |
| browserPackage              | Package name of a browser to be used to handle Custom Tabs.         | Boolean  | NO | Android      | NO |
| showInRecents               | Determining whether browsed website should be shown as separate entry in Android recents/multitasking view. [true/false]         | Boolean  | NO | Android      | NO |
| includeReferrer           | Determining whether to include your package name as referrer for the website to track. [true/false]       | Boolean  | NO | Android      | NO |


## 遗留问题

- [ ] 打开浏览器时，不能指定浏览器设置阅读模式 [#1](https://github.com/react-native-oh-library/react-native-inappbrowser/issues/1)
- [ ] 打开浏览器，无法使文稿动起来 [#2](https://github.com/react-native-oh-library/react-native-inappbrowser/issues/2)
- [ ] 无法设置浏览器的视图控制器的风格 [#3](https://github.com/react-native-oh-library/react-native-inappbrowser/issues/3)
- [ ] 无法设置浏览器的过度风格 [#4](https://github.com/react-native-oh-library/react-native-inappbrowser/issues/4)
- [ ] 无法设置浏览器的推送方式 [#5](https://github.com/react-native-oh-library/react-native-inappbrowser/issues/5)
- [ ] 浏览器无法设置工具栏进行折叠  [#6](https://github.com/react-native-oh-library/react-native-inappbrowser/issues/6)
- [ ] 浏览器设置是否重复使用前一次会话的cookie  [#7](https://github.com/react-native-oh-library/react-native-inappbrowser/issues/7)
- [ ] 浏览器设置模态框的自定义尺寸  [#8](https://github.com/react-native-oh-library/react-native-inappbrowser/issues/8)

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/proyecto26/react-native-inappbrowser/blob/develop/LICENSE) ，请自由地享受和参与开源。
