<!-- {% raw %} -->
> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-qr-decode-image-camera</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/deepanrajkumar/react-native-qr-decode-image-camera">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/deepanrajkumar/react-native-qr-decode-image-camera/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-qr-decode-image-camera)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-qr-decode-image-camera](https://github.com/react-native-oh-library/react-native-qr-decode-image-camera/releases)，并下载适用版本的 tgz 包。

进入到工程目录并输入以下命令：

> [!TIP] # 处替换为 tgz 包的路径

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-qr-decode-image-camera@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-qr-decode-image-camera@file:#
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。
> 示例中：launchImageLibrary 方法需引入Harmony OS 的react-native-image-picker库，跳转 [react-native-image-picker](https://gitee.com/react-native-oh-library/usage-docs/blob/master/zh-cn/react-native-image-picker.md)查看使用方法。

```js
import React, {useState} from 'react';
import {View, Text, Button} from 'react-native';
import {QRreader, QRscanner} from 'react-native-qr-decode-image-camera';
import {TestSuite, TestCase, Tester} from '@rnoh/testerino';
import { launchImageLibrary } from 'react-native-image-picker';
export const QRreaderExp = () => {
  const [reader, setReader] = useState<any>('');
  const [scanned, setScanned] = useState<boolean>(false);
  const [flashMode, setFlashMode] = useState<boolean | null>(null); //初始值必须为null;
  const [textInfo, setTextInfo] = useState<string>('');

  return (
    <Tester>
      <TestSuite name="qr-decode-image-camera">
        <TestCase
          itShould="QRReader"
          tags={['C_API']}
          initialState={undefined as any}
          arrange={({setState}) => {
            return (
              <View>
                <Button
                  onPress={() => {
                    launchImageLibrary({ mediaType: 'photo', selectionLimit: 1 }, (data) => {
                      if (data.assets?.length) {
                        const path = {
                          uri:data.assets[0].originalPath
                        }
                        QRreader(path)
                        .then(res => {
                          setReader(res?.[0]?.originalValue);
                          setState(res?.[0]?.originalValue);
                        })
                        .catch(error => {
                          console.log(error);
                        });
                      }
                    })
                  }}
                  title="点击选择二维码照片 "
                />
                <Text style={{fontSize: 20}}>{reader}</Text>
              </View>
            );
          }}
          assert={async ({expect, state}) => {
            expect(state).to.be.eq(reader);
          }}
        />
        <TestCase
          itShould="QRScaner"
          tags={['C_API']}
          initialState={undefined as any}
          arrange={({setState}) => {
            return (
              <View >
                <Button
                  onPress={() => {
                    setTextInfo('');
                    setScanned(true); // 开启摄像头
                  }}
                  title="点击扫码 "
                />
                {scanned && (
                  <QRscanner
                    onRead={e => {
                      console.log(e?.nativeEvent?.result, 'click onRead');
                      setTextInfo(e?.nativeEvent?.result);
                      setState(e?.nativeEvent?.result);
                      setScanned(false);
                    }}
                    flashMode={flashMode} //闪光灯
                    renderTopView={() => (
                      <View
                        style={{
                          height: 50,
                          justifyContent: 'center',
                          alignItems: 'center',
                          backgroundColor: '#0000004D',
                        }}>
                        <Text style={{fontSize: 18, color: 'green'}}>
                          将二维码放入框内，即可自动扫描
                        </Text>
                      </View>
                    )}
                    renderBottomView={() => (
                      <View
                        style={{
                          height: 100,
                          justifyContent: 'center',
                          alignItems: 'center',
                          backgroundColor: '#0000004D',
                        }}>
                        <Text
                          style={{fontSize: 18, color: 'red'}}
                          onPress={() => {
                            setFlashMode(!flashMode);
                            console.log('click 点击开启/关闭闪光灯');
                          }}>
                          点击开启/关闭闪光灯
                        </Text>
                      </View>
                    )}
                  />
                )}
                <Text style={{fontSize: 20, color: 'red'}}>{textInfo}</Text>
              </View>
            );
          }}
          assert={async ({expect, state}) => {
            expect(state).to.be.eq(textInfo);
          }}
        />
      </TestSuite>
    </Tester>
  );
};

```
## 使用 Codegen

本库已经适配了 `Codegen` ，在使用前需要主动执行生成三方库桥接代码，详细请参考[ Codegen 使用文档](/zh-cn/codegen.md)。

## Link

目前 HarmonyOS 暂不支持 AutoLink，所以 Link 步骤需要手动配置。

首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 `harmony`

### 引入原生端代码

目前有两种方法：

1. 通过 har 包引入（在 IDE 完善相关功能后该方法会被遗弃，目前首选此方法）；
2. 直接链接源码。

方法一：通过 har 包引入

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/react-native-qr-decode-image-camera": "file:../../node_modules/@react-native-oh-tpl/react-native-qr-decode-image-camera/harmony/qr_decode_image_camera.har"
  }
```

点击右上角的 `sync` 按钮

或者在终端执行：

```bash
cd entry
ohpm install
```

方法二：直接链接源码

> [!TIP] 如需使用直接链接源码，请参考[直接链接源码说明](/zh-cn/link-source-code.md)

### 在 ArkTs 侧引入 RNQrDecodeImageCameraPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
...
+ import { RNQrDecodeImageCameraPackage } from "@react-native-oh-tpl/react-native-qr-decode-image-camera/ts";

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNQrDecodeImageCameraPackage(ctx)
  ];
}
```
### 在 ArkTs 侧引入 Fabric 组件
找到 function buildCustomRNComponent()，一般位于 entry/src/main/ets/pages/index.ets 或 entry/src/main/ets/rn/LoadBundle.ets，添加：

```diff
...
+ import { NativeScan } from "@react-native-oh-tpl/react-native-qr-decode-image-camera"

@Builder
export function buildCustomRNComponent(ctx: ComponentBuilderContext) {
...
+ if (ctx.componentName === NativeScan.NAME) {
+   NativeScan({
+     ctx: ctx.rnComponentContext,
+     tag: ctx.tag   
+   })
+ }
...
}
...
```
### 运行

点击右上角的 `sync` 按钮

或者在终端执行：

```bash
cd entry
ohpm install
```

然后编译、运行即可。

## 约束与限制

### 兼容性
要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-native-qr-decode-image-camera](https://github.com/react-native-oh-library/react-native-qr-decode-image-camera/releases)


### 权限要求
在 entry 目录下的module.json5中添加相机权限

打开 entry/src/main/module.json5，添加：

```diff
...
"requestPermissions": [
+  {
+    "name": "ohos.permission.CAMERA",
+    "reason": "$string:Qr_decode_image_cameraAbility_desc",
+    "usedScene": {
+      "abilities": [
+        "NativeScan"
+      ],
+      "when":"inuse"
+    }
+  }
]
```

## 静态方法

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。
>
> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。
>
详情请查看[react-native-qr-decode-image-camera官方文档](https://github.com/deepanrajkumar/react-native-qr-decode-image-camera)
 | Name                          | Description                                          | Type    | Required | Platform    | HarmonyOS Support |
 | ----------------------------- | ---------------------------------------------------- | ------- | -------- | ----------- | ----------------- |
 | QRreader | 调用此方法，调起图库，选择选择二维码图片进行图片解码，异步返回结果 | funtion | no       | IOS/Android | yes               |
## 属性
### QRscanner 

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。
>
> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。
>

| Name                          | Description                                          | Type    | Required | Platform    | HarmonyOS Support |
| ----------------------------- | ---------------------------------------------------- | ------- | -------- | ----------- | ----------------- |
| isRepeatScan | whether to allow repeated scanning | boolean | no       | IOS/Android | no               |
| zoom | Camera focal length range 0-1 | number | no       | IOS/Android | yes               |
| flashMode |Turn on the flashlight |boolean | no       | IOS/Android | yes               |
| onRead |scan callback |funtion | yes       | IOS/Android | yes|
| maskColor |mask layer color |string | no       | IOS/Android | yes|
| borderColor |border color |string | no       | IOS/Android | yes|
| cornerColor |Color of corner of scan frame |string | no       | IOS/Android | yes|
| borderWidth |border width of scan frame |number | no       | IOS/Android | yes|
| cornerBorderWidth |border width of scan frame corner |number | no       | IOS/Android | yes|
| cornerBorderLength |	width and height of the corner of the scan frame |number | no       | IOS/Android | yes|
| rectHeight |	Scan frame height |number | no       | IOS/Android | yes|
| rectWidth |	Scan Frame Width |number | no       | IOS/Android | yes|
| finderX |scan frame X axis offset |number | no       | IOS/Android | yes|
| finderY |scan frame Y axis offset |number | no       | IOS/Android | yes|
| isCornerOffset |whether the corners are offset |boolean | no       | IOS/Android | yes|
| cornerOffsetSize |offset |number | no       | IOS/Android | yes|
| bottomHeight |Reserved height at the bottom |number | no       | IOS/Android | yes|
| scanBarAnimateTime |scan line time |number | no       | IOS/Android | yes|
| scanBarColor |scan line color |string | no       | IOS/Android | yes|
| scanBarImage |scan line image |any | no       | IOS/Android | yes|
| scanBarHeight |scan line height |number | no       | IOS/Android | yes|
| scanBarMargin |scanline left and right margin |number | no       | IOS/Android | yes|
| hintText |hintText |string | no       | IOS/Android | yes|
| hintTextStyle |hint string style |object | no       | IOS/Android | yes|
| hintTextPosition |hintTextPosition |number | no       | IOS/Android | yes|
| renderTopView |render top View |funtion | no       | IOS/Android | yes|
| renderBottomView |render bottom View|funtion | no       | IOS/Android | yes|
| isShowScanBar |whether to show scan lines|boolean | no       | IOS/Android | yes|
| topViewStyle |render top container style|object | no       | IOS/Android | yes|
| bottomViewStyle |render bottom container style|object | no       | IOS/Android | yes|
## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/deepanrajkumar/react-native-qr-decode-image-camera/blob/master/LICENSE) ，请自由地享受和参与开源。

<!-- {% endraw %} -->