> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-dropdownalert</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/react-native-oh-library/react-native-dropdownalert">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/react-native-oh-library/react-native-dropdownalert/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-dropdownalert)

## Installation and Usage

Find the matching version information in the release address of a third-party library and download an applicable .tgz package: [@react-native-oh-tpl/react-native-dropdownalert Releases](https://github.com/react-native-oh-library/react-native-dropdownalert/releases).

Go to the project directory and execute the following instruction:

> [!TIP] Replace the content with the path of the .tgz package at the comment sign (#).

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-dropdownalert@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-dropdownalert@file:#
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React, { useRef, useState } from "react";
import {
  StyleSheet,
  Text,
  View,
  FlatList,
  SafeAreaView,
  TouchableOpacity,
  ImageSourcePropType,
  ColorValue,
} from "react-native";
import DropdownAlert, {
  DropdownAlertData,
  DropdownAlertType,
  DropdownAlertColor,
  DropdownAlertProps,
} from "react-native-dropdownalert";

type ListItem = {
  name: string,
  alertData?: DropdownAlertData,
  alertProps?: DropdownAlertProps,
  color: ColorValue,
};

type ListItemIndex = {
  item: ListItem,
  index: number,
};

function App(): React.JSX.Element {
  const defaultSelected: ListItem = {
    name: "Default",
    color: DropdownAlertColor.Default,
  };
  const [selected, setSelected] = useState(defaultSelected);
  const [processing, setProcessing] = useState(false);
  let alert = useRef(
    (_data?: DropdownAlertData) =>
      new Promise() < DropdownAlertData > ((res) => res)
  );
  let dismiss = useRef(() => {});
  const reactNativeLogoSrc: ImageSourcePropType = {
    uri: "https://reactnative.dev/docs/assets/favicon.png",
  };

  const items: ListItem[] = [
    {
      name: "Warn",
      alertData: {
        type: DropdownAlertType.Warn,
        title: "Warn",
        message:
          "The device battery is low. It will go into low power mode in 5 minutes.",
      },
      color: DropdownAlertColor.Warn,
    },
    {
      name: "Info",
      alertData: {
        type: DropdownAlertType.Info,
        title: "Info",
        message:
          "The system goes offline from midnight to 3 AM for regular maintenance.",
      },
      color: DropdownAlertColor.Info,
    },
    {
      name: "Success",
      alertData: {
        type: DropdownAlertType.Success,
        title: "Success",
        message: "The order is complete and details sent to email.",
      },
      color: DropdownAlertColor.Success,
    },
    {
      name: "Error",
      alertData: {
        type: DropdownAlertType.Error,
        title: "Error",
        message:
          "Something went wrong. Please contact support if error persists.",
      },
      color: DropdownAlertColor.Error,
    },
    {
      name: "Custom",
      alertData: {
        type: "",
        title: "Custom",
        message:
          "This demonstrates the ability to customize image, interval and style.",
        source: reactNativeLogoSrc,
        interval: 5000,
      },
      alertProps: {
        alertViewStyle: styles.alertView,
      },
      color: styles.alertView.backgroundColor,
    },
    {
      name: "Cancel",
      alertData: {
        type: DropdownAlertType.Info,
        title: "Info",
        message:
          "This demonstrates an info alert with a cancel button. Tap cancel button to dismiss.",
      },
      alertProps: {
        dismissInterval: 0,
        showCancel: true,
        onDismissPressDisabled: true,
      },
      color: "teal",
    },
    {
      name: "Bottom",
      alertData: {
        type: DropdownAlertType.Info,
        title: "Info",
        message: "This demonstrates an info alert with bottom alert position.",
      },
      alertProps: {
        alertPosition: "bottom",
        infoColor: "green",
      },
      color: "green",
    },
  ];

  function _renderItem(listItemIndex: ListItemIndex): React.JSX.Element {
    const { item } = listItemIndex;
    return (
      <TouchableOpacity
        style={[styles.item, { backgroundColor: item.color }]}
        onPress={() => _onSelect(item)}
        disabled={processing}
      >
        <Text style={styles.name}>{item.name}</Text>
      </TouchableOpacity>
    );
  }

  function _onSelect(item: ListItem): void {
    setSelected(item);
    setTimeout(async () => {
      setProcessing(true);
      await alert.current(item.alertData);
      setProcessing(false);
    }, 10);
  }

  return (
    <View style={styles.view}>
      <SafeAreaView>
        <FlatList
          keyExtractor={(_item, index) => `${index}`}
          data={items}
          initialNumToRender={items.length}
          renderItem={_renderItem}
        />
      </SafeAreaView>
      <DropdownAlert
        alert={(func) => (alert.current = func)}
        dismiss={(func) => (dismiss.current = func)}
        {...selected.alertProps}
      />
    </View>
  );
}

const styles = StyleSheet.create({
  view: {
    flex: 1,
    justifyContent: "center",
    backgroundColor: "#F4F3E9",
  },
  item: {
    padding: 12,
    margin: 4,
    borderRadius: 8,
    borderColor: "black",
    borderWidth: StyleSheet.hairlineWidth,
  },
  name: {
    fontSize: 18,
    fontWeight: "bold",
    textAlign: "center",
    color: "whitesmoke",
  },
  alertView: {
    padding: 8,
    backgroundColor: "#6441A4",
  },
});

export default App;
```

## Constraints

### Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/react-native-dropdownalert Releases](https://github.com/react-native-oh-library/react-native-dropdownalert/releases)

## DropdownAlert

### DropdownAlertType

DropdownAlertType 是 DropdownAlert 库导出的一个枚举对象，列举了弹框的类型。

#### DropdownAlertType Property

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name    | Description  | Type   | **Required** | Platform | HarmonyOS Support |
| ------- | ------------ | ------ | ------------ | -------- | ----------------- |
| Info    | 值为 info    | string | no           | All      | yes               |
| Warn    | 值为 warn    | string | no           | All      | yes               |
| Error   | 值为 error   | string | no           | All      | yes               |
| Success | 值为 success | string | no           | All      | yes               |

### DropdownAlertDismissAction

DropdownAlertDismissAction 是 DropdownAlert 库导出的一个枚举对象，列举了弹框消失的动作类型。

#### DropdownAlertDismissAction Property

| Name         | Description       | Type   | **Required** | Platform | HarmonyOS Support |
| ------------ | ----------------- | ------ | ------------ | -------- | ----------------- |
| Automatic    | 值为 automatic    | string | no           | All      | yes               |
| Cancel       | 值为 cancel       | string | no           | All      | yes               |
| Pan          | 值为 pan          | string | no           | All      | yes               |
| Programmatic | 值为 programmatic | string | no           | All      | yes               |
| Press        | 值为 press        | string | no           | All      | yes               |

### DropdownAlertColor

DropdownAlertColor 是 DropdownAlert 库导出的一个枚举对象，列举了弹框的颜色

#### DropdownAlertColor Property

| Name    | Description    | Type   | **Required** | Platform | HarmonyOS Support |
| ------- | -------------- | ------ | ------------ | -------- | ----------------- |
| Info    | 值为'#2b73b6'  | string | no           | All      | yes               |
| Warn    | 值为'#cd853f'  | string | no           | All      | yes               |
| Error   | 值为'#cc3232'  | string | no           | All      | yes               |
| Success | 值为'#32a54a'  | string | no           | All      | yes               |
| Default | 值为''#000000' | string | no           | All      | yes               |

### DropDownAlertImage

DropDownAlertImage 是 DropdownAlert 库导出的一个枚举对象，列举了弹框的图片资源。

#### DropDownAlertImage Property

| Name    | Description                                                              | Type                | **Required** | Platform | HarmonyOS Support |
| ------- | ------------------------------------------------------------------------ | ------------------- | ------------ | -------- | ----------------- |
| Info    | Info 时使用的图片资源，使用源库的资源 require('./assets/info.png')       | ImageSourcePropType | no           | All      | yes               |
| Warn    | Warn 时使用的图片资源，使用源库的资源 require('./assets/warn.png')       | ImageSourcePropType | no           | All      | yes               |
| Error   | Error 时使用的图片资源，使用源库的资源 require('./assets/error.png')     | ImageSourcePropType | no           | All      | yes               |
| Success | Success 时使用的图片资源，使用源库的资源 require('./assets/success.png') | ImageSourcePropType | no           | All      | yes               |
| Cancel  | Cancel 时使用的图片资源，使用源库的资源 require('./assets/cancel.png')   | ImageSourcePropType | no           | All      | yes               |

### DropdownAlertToValue

DropdownAlertToValue 是 DropdownAlert 库导出的一个枚举对象，有两种值 Alert 和 Dismiss。

#### DropdownAlertToValue Property

| Name    | Description | Type   | **Required** | Platform | HarmonyOS Support |
| ------- | ----------- | ------ | ------------ | -------- | ----------------- |
| Alert   | 值为 1      | number | no           | All      | yes               |
| Dismiss | 值为 0      | number | no           | All      | yes               |

### DropDownAlertTestID

DropDownAlertTestID 是 DropdownAlert 库导出的一个枚举对象，列举了弹框的测试 ID。

#### DropDownAlertTestID Property

| Name         | Description       | Type   | **Required** | Platform | HarmonyOS Support |
| ------------ | ----------------- | ------ | ------------ | -------- | ----------------- |
| AnimatedView | 值为 animatedView | string | no           | All      | yes               |
| SafeView     | 值为 safeView     | string | no           | All      | yes               |
| TextView     | 值为 textView     | string | no           | All      | yes               |
| Alert        | 值为 alert        | string | no           | All      | yes               |
| Image        | 值为 image        | string | no           | All      | yes               |
| Title        | 值为 title        | string | no           | All      | yes               |
| Message      | 值为 message      | string | no           | All      | yes               |
| Cancel       | 值为 cancel       | string | no           | All      | yes               |
| CancelImage  | 值为 cancelImage  | string | no           | All      | yes               |

### DropdownAlertData

DropdownAlertData 是 DropdownAlert 库导出的一个 class 对象，定义了弹框的数据内容，如标题、提示信息等。

#### DropdownAlertData Property

| Name     | Description                             | Type                | **Required** | Platform | HarmonyOS Support |
| -------- | --------------------------------------- | ------------------- | ------------ | -------- | ----------------- |
| type     | 弹窗类型，传入 DropdownAlertType 的枚举 | DropdownAlertType   | no           | All      | yes               |
| title    | 弹窗的消息标题                          | string              | no           | All      | yes               |
| message  | 弹窗的消息正文                          | string              | no           | All      | yes               |
| source   | 弹窗的图片类型                          | ImageSourcePropType | no           | All      | yes               |
| interval | 自动消失的时间，单位毫秒值              | number              | no           | All      | yes               |
| resolve  | 弹窗被处理的触发的事件                  | function            | no           | All      | yes               |

### DropdownAlertPosition

DropdownAlertData 是 DropdownAlert 库导出的一个 class 对象，定义了弹框弹出位置，有顶部弹出和底部弹出两种。

#### DropdownAlertPosition Property

| Name   | Description            | Type              | **Required** | Platform | HarmonyOS Support |
| ------ | ---------------------- | ----------------- | ------------ | -------- | ----------------- |
| Top    | 顶部弹出，值为'top'    | DropdownAlertType | no           | All      | yes               |
| Bottom | 底部弹出，值为'bottom' | string            | no           | All      | yes               |

### DropdownAlert components

DropdownAlert 是 DropdownAlert 库导出的核心组件，定义了弹框所有属性，与 DropdownAlertProps 属性一致。

#### DropdownAlert Property

| Name                             | Description                                                                                                                                                        | Type                           | **Required** | Platform | HarmonyOS Support |
| -------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------ | ------------ | -------- | ----------------- |
| imageSrc                         | 弹框未指定图片资源的时候使用的默认自定义图片                                                                                                                       | ImageSourcePropType            | no           | All      | yes               |
| infoImageSrc                     | 弹框未指定类型为 Info 时，使用的自定义图片                                                                                                                         | ImageSourcePropType            | no           | All      | yes               |
| warnImageSrc                     | 弹框未指定类型为 Warn 时，使用的自定义图片                                                                                                                         | ImageSourcePropType            | no           | All      | yes               |
| errorImageSrc                    | 弹框未指定类型为 Error 时，使用的自定义图片                                                                                                                        | ImageSourcePropType            | no           | All      | yes               |
| successImageSrc                  | 弹框未指定类型为 Success 时，使用的自定义图片                                                                                                                      | ImageSourcePropType            | no           | All      | yes               |
| cancelImageSrc                   | 弹框未指定类型为 Cancel 时，使用的自定义图片                                                                                                                       | ImageSourcePropType            | no           | All      | yes               |
| infoColor                        | 弹框未指定类型为 Info 时，使用的自定义颜色                                                                                                                         | ColorValue                     | no           | All      | yes               |
| warnColor                        | 弹框未指定类型为 Warn 时，使用的自定义颜色                                                                                                                         | ColorValue                     | no           | All      | yes               |
| errorColor                       | 弹框未指定类型为 Error 时，使用的自定义颜色                                                                                                                        | ColorValue                     | no           | All      | yes               |
| successColor                     | 弹框未指定类型为 Success 时，使用的自定义颜色                                                                                                                      | ColorValue                     | no           | All      | yes               |
| activeStatusBarBackgroundColor   | 弹框出现时，将状态栏置为设置的颜色，需要配合 updateStatusBar=true 才生效                                                                                           | ColorValue                     | no           | Android  | yes               |
| inactiveStatusBarBackgroundColor | 弹框消失时，将状态栏置为设置的颜色，需要配合 updateStatusBar=true 才生效                                                                                           | ColorValue                     | no           | Android  | yes               |
| dismissInterval                  | 弹窗自动消失的时间毫秒值                                                                                                                                           | number                         | no           | All      | yes               |
| titleNumberOfLines               | 弹窗标题的最大行数，                                                                                                                                               | number                         | no           | All      | yes               |
| messageNumberOfLines             | 弹窗正文的最大行数，超过则省略                                                                                                                                     | number                         | no           | All      | yes               |
| elevation                        | 视图的高度，此属性可以为视图添加一个投影，并且会影响视图层叠的顺序。此属性仅支持 Android5.0 及以上版本。                                                           | number                         | no           | Android  | no                |
| zIndex                           | z 轴的值                                                                                                                                                           | number                         | no           | All      | no                |
| panResponderDismissDistance      | 下滑弹窗消失距离                                                                                                                                                   | number                         | no           | All      | yes               |
| animatedViewStyle                | 此属性可接收一个 ViewStyle 对象，用于设置弹窗内部的 Animated.View 的样式。                                                                                         | ViewStyle                      | no           | All      | no                |
| alertViewStyle                   | 此属性可接收一个 ViewStyle 对象，用于设置弹窗的样式。                                                                                                              | ViewStyle                      | no           | All      | yes               |
| safeViewStyle                    | 此属性可接收一个 ViewStyle 对象，用于设置弹窗内部的 safeView 的样式。                                                                                              | ViewStyle                      | no           | All      | yes               |
| textViewStyle                    | 此属性可接收一个 ViewStyle 对象，用于设置弹窗文字的样式。                                                                                                          | ViewStyle                      | no           | All      | yes               |
| cancelViewStyle                  | 此属性可接收一个 ViewStyle 对象，用于设置弹窗内部取消按钮的样式。                                                                                                  | ViewStyle                      | no           | All      | yes               |
| titleTextStyle                   | 此属性可接收一个 TextStyle 对象，用于设置弹窗标题的样式。                                                                                                          | TextStyle                      | no           | All      | yes               |
| messageTextStyle                 | 此属性可接收一个 TextStyle 对象，用于设置弹窗正文的样式。                                                                                                          | TextStyle                      | no           | All      | yes               |
| imageStyle                       | 此属性可接收一个 ImageStyle 对象，用于设置弹窗内图片的样式。                                                                                                       | ImageStyle                     | no           | All      | yes               |
| cancelImageStyle                 | 此属性可接收一个 ImageStyle 对象，用于设置弹窗内取消按钮所用图片的样式。                                                                                           | ImageStyle                     | no           | All      | yes               |
| onDismissAutomatic               | 弹窗关闭触发的函数，支持的关闭方式为自动关闭                                                                                                                       | function                       | no           | All      | yes               |
| onDismissCancel                  | 弹窗关闭触发的函数，支持的关闭方式为点击 cancel                                                                                                                    | function                       | no           | All      | yes               |
| onDismissPress                   | 弹窗关闭触发的函数，支持的关闭方式为点击弹窗                                                                                                                       | function                       | no           | All      | yes               |
| onDismissPanResponder            | 弹窗关闭触发的函数，支持的关闭方式为向下滑动，仅在 alertPosition 为“bottom”时生效                                                                                  | function                       | no           | All      | yes               |
| onDismissProgrammatic            | 弹窗关闭触发的函数，支持的关闭方式为程序式关闭，也是默认的值，如果非上面四种关闭方式，则默认触发此关闭函数。                                                       | function                       | no           | All      | no                |
| showCancel                       | 是否显示弹窗的 cancel 模块                                                                                                                                         | boolean                        | no           | All      | yes               |
| onDismissPressDisabled           | 是否允许通过点击关闭弹窗                                                                                                                                           | boolean                        | no           | All      | yes               |
| panResponderEnabled              | 是否允许通过向下滑动关闭弹窗，仅在 alertPosition 为“bottom”时生效                                                                                                  | boolean                        | no           | All      | yes               |
| translucent                      | 指定状态栏是否透明。设置为 true 时，应用会延伸到状态栏之下绘制（即所谓“沉浸式”——被状态栏遮住一部分）。常和带有半透明背景色的状态栏搭配使用，此属性仅支持 Android。 | boolean                        | no           | Android  | no                |
| updateStatusBar                  | 是否更新状态栏                                                                                                                                                     | boolean                        | no           | All      | yes               |
| activeStatusBarStyle             | 弹框出现时，将状态栏置为设置的样式，需要配合 updateStatusBar=true 才生效                                                                                           | StatusBarStyle                 | no           | Android  | yes               |
| inactiveStatusBarStyle           | 弹框消失时，将状态栏置为设置的样式，需要配合 updateStatusBar=true 才生效                                                                                           | StatusBarStyle                 | no           | Android  | yes               |
| renderImage                      | 函数式返回的图片                                                                                                                                                   | render function                | no           | All      | yes               |
| renderCancel                     | 函数式返回的取消                                                                                                                                                   | render function                | no           | All      | yes               |
| renderTitle                      | 函数式返回的弹窗消息标题                                                                                                                                           | render function                | no           | All      | yes               |
| renderMessage                    | 函数式返回的弹窗消息正文                                                                                                                                           | render function                | no           | All      | yes               |
| titleTextProps                   | 消息标题文字样式                                                                                                                                                   | TextProps                      | no           | All      | yes               |
| messageTextProps                 | 消息正文文字样式                                                                                                                                                   | TextProps                      | no           | All      | yes               |
| animatedViewProps                | 此属性可接收一个 ViewProps 对象，用于设置弹窗对象内部的 Animated.View 的属性。                                                                                     | ViewProps                      | no           | All      | yes               |
| alertTouchableOpacityProps       | 弹窗透明度样式设置                                                                                                                                                 | TouchableOpacityProps          | no           | All      | yes               |
| safeViewProps                    | 此属性可接收一个 ViewProps 对象，用于设置弹窗对象内部的 safeView 的属性。                                                                                          | ViewProps                      | no           | All      | yes               |
| textViewProps                    | 此属性可接收一个 ViewProps 对象，用于设置弹窗对象内部的文本展示区域的属性。                                                                                        | ViewProps                      | no           | All      | yes               |
| imageProps                       | 此属性可接收一个 ImageProps 对象，用于设置弹窗对象内部的图片的属性。                                                                                               | ImageProps                     | no           | All      | yes               |
| cancelTouchableOpacityProps      | 此属性可接收一个 TouchableOpacityProps 对象，用于设置弹窗对象内部的取消按钮的属性。                                                                                | TouchableOpacityProps          | no           | All      | yes               |
| cancelImageProps                 | 此属性可接收一个 ImageProps 对象，用于设置弹窗对象内部的取消按钮图片的属性。                                                                                       | ImageProps                     | no           | All      | yes               |
| alert                            | 弹窗弹出触发事件                                                                                                                                                   | function                       | no           | All      | yes               |
| dismiss                          | 弹窗消失触发事件                                                                                                                                                   | function                       | no           | All      | yes               |
| springAnimationConfig            | 弹簧效果参数                                                                                                                                                       | Animated.SpringAnimationConfig | no           | All      | yes               |
| children                         | 弹窗子元素                                                                                                                                                         | ReactNode                      | no           | All      | yes               |
| alertPosition                    | 设置弹窗弹出的位置，top 从屏幕顶部弹出，或者设置为 bottom 从屏幕底部弹出。默认值为 top。                                                                           | string                         | no           | All      | yes               |

## Known Issues

## Others

- DropdownAlert 组件的 animatedViewStyle 属性不生效，设置之后弹窗变为黑色，与 iOS/Android 一致 [issue#314](https://github.com/testshallpass/react-native-dropdownalert/issues/314)
- DropdownAlert 组件的 zindex 属性不生效，层级关系并未体现，与 iOS/Android 一致 [issue#315](https://github.com/testshallpass/react-native-dropdownalert/issues/315)
- DropdownAlert 组件的 translucent 属性不生效，没有显示出状态栏半透明的效果，与 Android 一致 [issue#316](https://github.com/testshallpass/react-native-dropdownalert/issues/316)
- DropdownAlert 组件绑定的 onDismissProgrammatic 函数无法触发，与 iOS/Android 一致 [issue#317](https://github.com/testshallpass/react-native-dropdownalert/issues/317)
- DropdownAlertData 组件的 resolve 属性不生效，将弹窗关闭之后，所设置的函数并未被触发，与 iOS/Android 一致 [issue#318](https://github.com/testshallpass/react-native-dropdownalert/issues/318)

## License

This project is licensed under [The MIT License (MIT)](https://github.com/react-native-oh-library/react-native-dropdownalert/blob/master/LICENSE).
