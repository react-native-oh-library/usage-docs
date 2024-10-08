> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-navigation-header-buttons</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/vonovak/react-navigation-header-buttons">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/vonovak/react-navigation-header-buttons/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/vonovak/react-navigation-header-buttons)

## 安装与使用

<!-- tabs:start -->
进入到工程目录并输入以下命令：

#### **npm**

```bash
npm i react-navigation-header-buttons@12.0.0
```

#### **yarn**

```bash
yarn add react-navigation-header-buttons@12.0.0
```


在tsconfig.json文件中添加如下代码:
```json
"compilerOptions": {
  ...
    "paths": {
    ...
      "react-navigation-header-buttons":[
        "./node_modules/react-navigation-header-buttons/lib/module/index.js"
      ]
    },
  }

```
在metro.config.js文件中添加如下代码:
```js
const config = {
...
  resolver: {
    unstable_enablePackageExports: true,
  },
};
module.exports = mergeConfig(
  ...
  config,
);

```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import * as React from 'react';
import MaterialIcons from '@expo/vector-icons/MaterialIcons';
import {
  HeaderButtons,
  Item,
  HiddenItem,
  OverflowMenu,
  Divider,
  ItemProps,
  HiddenItemProps,
  HeaderButtonProps,
  HeaderButton,
} from 'react-navigation-header-buttons';
import { Text } from 'react-native';

const MaterialHeaderButton = (props: HeaderButtonProps) => (
  <HeaderButton IconComponent={MaterialIcons} iconSize={23} {...props} />
);

const EditItem = ({ onPress }: Pick<ItemProps, 'onPress'>) => {
  return <Item title="edit" onPress={onPress} />;
};

const ReusableHiddenItem = ({ onPress }: Pick<HiddenItemProps, 'onPress'>) => (
  <HiddenItem title="hidden2" onPress={onPress} disabled />
);

export function UsageWithIcons({ navigation }) {
  React.useLayoutEffect(() => {
    navigation.setOptions({
      title: 'Demo',
      headerRight: () => (
        <HeaderButtons HeaderButtonComponent={MaterialHeaderButton}>
          <Item
            title="search"
            iconName="search"
            onPress={() => alert('search')}
          />
          <EditItem onPress={() => alert('Edit')} />
          <OverflowMenu
            OverflowIcon={({ color }) => (
              <MaterialIcons name="more-horiz" size={23} color={color} />
            )}
          >
            <HiddenItem title="hidden1" onPress={() => alert('hidden1')} />
            <Divider />
            <ReusableHiddenItem onPress={() => alert('hidden2')} />
          </OverflowMenu>
        </HeaderButtons>
      ),
    });
  }, [navigation]);

  return <Text>demo!</Text>;
}
```

## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

1. RNOH：0.72.26; SDK：HarmonyOS NEXT Developer Beta1 5.0.0.25; IDE：DevEco Studio 5.0.3.300SP2; ROM:3.0.0.24(Canary3);

## 属性

### HeaderButtons

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。



| Name            | Description     | Type                                                                                                                     | Required | Platform | HarmonyOS Support    | 
| --------------- | -------- | ------------------------------------------------------------------------------------------------------------------------------- | ------- | -------- | ----------- | 
| HeaderButtonComponent            | component that renders the buttons, HeaderButton by default  |`ComponentType`| no   | iOS/Android       | yes | 
| children            | 	whatever you want to render inside  |`ReactNode`| yes   | iOS/Android       | yes | 
| left            | 	whether the HeaderButtons are on the left from header title  |boolean| no   | iOS/Android       | yes | 
| preset            | headers are typically rendered in Stack Navigator, however, you can also render them in a Tab Navigator header. Pass 'tabHeader' if button margins are missing.  |`’tabHeader’/‘stackHeader’`| no   | iOS/Android       | yes | 



### Item

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。



| Name            | Description     | Type                                                                                                                     | Required | Platform | HarmonyOS Support    | 
| --------------- | -------- | ------------------------------------------------------------------------------------------------------------------------------- | ------- | -------- | ----------- | 
| title            | 	title for the button, required  |string| no   | iOS/Android       | yes | 
| onPress            | 	function to call on press |function| no   | iOS/Android       | yes | 
| iconName            | 	icon name, used together with the IconComponent prop  |string| no   | iOS/Android       | yes | 
| style            | style to apply to the touchable element that wraps the button  |` ViewStyle`| no   | iOS/Android       | yes | 
| buttonStyle            | style to apply to the text / icon |` ViewStyle`| no   | iOS/Android       | yes | 

### OverflowMenu

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。



| Name            | Description     | Type                                                                                                                     | Required | Platform | HarmonyOS Support    | 
| --------------- | -------- | ------------------------------------------------------------------------------------------------------------------------------- | ------- | -------- | ----------- | 
| OverflowIcon            | React element or component for the overflow icon  |` ReactElement / ComponentType`| no   | iOS/Android       | yes | 
| style            | 	optional styles for overflow button|`ViewStyle`| no   | iOS/Android       | yes | 
| onPress            | 	function that is called when overflow menu is pressed.  |function| no   | iOS/Android       | yes | 
| left              | whether the OverflowMenu is on the left from header title |boolean| no   | iOS/Android       | yes |
| children              | the overflow items|`ReactNode`| yes   | iOS/Android       | yes |
| preset              |	headers are typically rendered in Stack Navigator, however, you can also render them in a Tab Navigator header. Pass 'tabHeader' if button margins are missing. |` 'tabHeader' / 'stackHeader'`| no   | iOS/Android       | yes |

### HiddenItem

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。



| Name            | Description     | Type                                                                                                                     | Required | Platform | HarmonyOS Support    | 
| --------------- | -------- | ------------------------------------------------------------------------------------------------------------------------------- | ------- | -------- | ----------- | 
| title            |title for the button, required  |string| no   | iOS/Android       | yes | 
| style            | style to apply to the touchable element that wraps the text|`ViewStyle`| no   | iOS/Android       | yes | 
| titleStyle            | style to apply to the text |`TextStyle`| no   | iOS/Android       | yes | 
| onPress            |function to call on press  |function| no   | iOS/Android       | yes | 
| disabled              | disabled 'item' is greyed out and onPress is not called on touch |boolean| no   | iOS/Android       | yes |


### HeaderButton

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。



| Name            | Description     | Type                                                                                                                     | Required | Platform | HarmonyOS Support    | 
| --------------- | -------- | ------------------------------------------------------------------------------------------------------------------------------- | ------- | -------- | ----------- | 
| title            |title for the button, required  |string| no   | iOS/Android       | yes | 
| style            | style to apply to the touchable element that wraps the text|`ViewStyle`| no   | iOS/Android       | yes | 
| onPress            |function to call on press  |function| no   | iOS/Android       | yes | 
| renderButton              |You can fully customize what it renders inside of the PlatformPressable using the renderButton |ReactNode | no   | iOS/Android       | yes |
## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/vonovak/react-navigation-header-buttons/blob/master/LICENSE) ，请自由地享受和参与开源。
