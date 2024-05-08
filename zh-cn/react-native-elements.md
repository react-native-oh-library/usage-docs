> 模板版本：v0.2.0

<p align="center">
  <h1 align="center"> <code>react-native-elements</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/react-native-elements/react-native-elements">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/react-native-elements/react-native-elements/blob/next/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>


> [!TIP] [Github 地址](https://github.com/react-native-elements/react-native-elements)



## 安装与使用


进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install @rneui/base@4.0.0-rc.8
npm install @rneui/themed@4.0.0-rc.8
```

#### **yarn**

```bash
yarn add @rneui/base@4.0.0-rc.8
yarn add @rneui/themed@4.0.0-rc.8
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React from 'react';
import { View, ScrollView, StyleSheet } from 'react-native';
import { Avatar } from '@rneui/themed';
import { Text } from '@rneui/base';

type AvatarData = {
  image_url: string;
};

const styles = StyleSheet.create({
  titleStyle: {
    fontWeight: 'bold',
    fontSize: 24,
  },
  subTitleStyle: {
    fontWeight: 'bold',
    fontSize: 18,
  },
  normalTitle: {
    fontWeight: 'bold',
    fontSize: 15,
  }
});

const dataList: AvatarData[][] = 
[
  [
    {
      image_url: 'https://api.uifaces.co/our-content/donated/xZ4wg2Xj.jpg',
    },
    {
      image_url: 'https://randomuser.me/api/portraits/men/36.jpg',
    },
    {
      image_url: 'https://cdn.pixabay.com/photo/2019/11/03/20/11/portrait-4599553__340.jpg',
    }
  ],
  [
    {
      image_url: 'https://cdn.pixabay.com/photo/2014/09/17/20/03/profile-449912__340.jpg',
    },
    {
      image_url: 'https://cdn.pixabay.com/photo/2020/09/18/05/58/lights-5580916__340.jpg',
    },
    {
      image_url: 'https://cdn.pixabay.com/photo/2016/11/21/12/42/beard-1845166_1280.jpg',
    }
  ]
];

type AvatarComponentProps = {};

const Avatars: React.FunctionComponent<AvatarComponentProps> = () => {
  return (
    <>
      <Text style={styles.titleStyle}>Avatars</Text>
      <ScrollView>
        <Text style={styles.subTitleStyle}>Photo Avatars</Text>
        {dataList.map((chunk, chunkIndex) => (
          <View
            style={{
              flexDirection: 'row',
              justifyContent: 'space-around',
              marginBottom: 30,
            }}
            key={chunkIndex}
          >
            {chunk.map((l, i) => (
              <Avatar
                size={64}
                rounded
                source={l.image_url ? { uri: l.image_url } : {}}
                key={`${chunkIndex}-${i}`}
              />
            ))}
          </View>
        ))}
        <Text style={styles.subTitleStyle}>Icon Avatars</Text>
        <View
          style={{
            flexDirection: 'row',
            justifyContent: 'space-around',
            marginBottom: 30,
          }}
        >
          <Avatar
            size={64}
            rounded
            icon={{ name: 'pencil', type: 'font-awesome' }}
            containerStyle={{ backgroundColor: '#6733b9' }}
          />
          <Avatar
            size={64}
            rounded
            icon={{ name: 'rocket', type: 'font-awesome' }}
            containerStyle={{ backgroundColor: '#00a7f7' }}
          />
          <Avatar
            size={64}
            rounded
            icon={{ name: 'heartbeat', type: 'font-awesome' }}
            containerStyle={{ backgroundColor: '#eb1561' }}
          />
        </View>
        <View
          style={{
            flexDirection: 'row',
            justifyContent: 'space-around',
            marginBottom: 30,
          }}
        >
          <Avatar
            size={64}
            rounded
            icon={{
              name: 'users',
              type: 'font-awesome',
              color: '#cdde20',
            }}
            containerStyle={{
              borderColor: 'grey',
              borderStyle: 'solid',
              borderWidth: 1,
            }}
          />
          <Avatar
            size={64}
            rounded
            icon={{ name: 'bank', type: 'font-awesome', color: '#009688' }}
            containerStyle={{
              borderColor: 'grey',
              borderStyle: 'solid',
              borderWidth: 1,
            }}
          />
          <Avatar
            size={64}
            rounded
            icon={{ name: 'apple', type: 'font-awesome', color: '#ff5606' }}
            containerStyle={{
              borderColor: 'grey',
              borderStyle: 'solid',
              borderWidth: 1,
            }}
          />
        </View>

        <Text style={styles.subTitleStyle}>Letter Avatars</Text>
        <View
          style={{
            flexDirection: 'row',
            justifyContent: 'space-around',
            marginBottom: 30,
          }}
        >
          <Avatar
            size={64}
            rounded
            title="Fc"
            containerStyle={{ backgroundColor: '#3d4db7' }}
          />
          <Avatar
            size={64}
            rounded
            title="P"
            containerStyle={{ backgroundColor: 'coral' }}
          />
          <Avatar
            size={64}
            rounded
            title="Rd"
            containerStyle={{ backgroundColor: 'purple' }}
          />
        </View>

        <Text style={styles.subTitleStyle}>Badged Avatars</Text>
        <View
          style={{
            flexDirection: 'row',
            justifyContent: 'space-around',
            marginBottom: 40,
          }}
        >
          <Avatar
            size={64}
            rounded
            icon={{ name: 'pencil', type: 'font-awesome' }}
            containerStyle={{ backgroundColor: 'orange' }}
          >
            <Avatar.Accessory size={24} />
          </Avatar>
          <Avatar
            size={64}
            rounded
            source={{ uri: 'https://randomuser.me/api/portraits/women/57.jpg' }}
            containerStyle={{ backgroundColor: 'grey' }}
          >
            <Avatar.Accessory size={23} />
          </Avatar>
        </View>
      </ScrollView>
    </>
  );
};

export default Avatars;
```

### 在 ArkTs 侧引入和注册字体文件

步骤一：
    复制字体文件到  `entry/src/main/ets/assets/fonts` 目录下(如使用了外部字体文件，需要将*.ttf文件复制过来)

步骤二：
    打开 `entry/src/main/ets/pages/Index.ets`，添加以下代码

```ts
    import font from '@ohos.font';
    //...
    //特别注意：FontAwesome 系列中字体的 familyName 需要通过代码逻辑自行理解
    const fonts: font.FontOptions[] = [
      {
        familyName: 'StintUltraCondensed-Regular',
        familySrc: '/assets/fonts/StintUltraCondensed-Regular.ttf'
      },
      {
        familyName: 'FontAwesome',
        familySrc: '/assets/fonts/FontAwesome.ttf'
      },
      {
        familyName: 'FontAwesome5_Brands',
        familySrc: '/assets/fonts/FontAwesome5_Brands.ttf'
      },
      {
        familyName: 'FontAwesome5_Regular',
        familySrc: '/assets/fonts/FontAwesome5_Regular.ttf'
      },
      {
        familyName: 'FontAwesome5_Solid',
        familySrc: '/assets/fonts/FontAwesome5_Solid.ttf'
      }
    ]

    @Entry
    @Component
    struct Index {
        //...
        aboutToAppear() {
            //...

            //注册字体文件
            for (const customFont of fonts) {
                font.registerFont(customFont)
            }
        }
        //...
    }
```
#### 提醒：自定义字体也需要用同样的方法在此注册

## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

1. RNOH: 0.72.20; SDK: HarmonyOS NEXT Developer Beta1; IDE: DevEco Studio 5.0.3.200; ROM: 3.0.0.18;

## 组件

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name           | Description                                                  | Required | Platform    | HarmonyOS Support |
| -------------- | ------------------------------------------------------------ | -------- | ----------- | ----------------- |
| Avatars        | 通常用于用户头像UI，可以使用图片，图标和文本。               | no       | ios/android | partially         |
| Button         | 按钮组件，可以显示文本、图标，也可以同时显示两者。           | no       | ios/android | partially         |
| Cards          | 卡片可以包含图像、按钮、文本等。卡片主要用于提供信息。       | no       | ios/android | yes               |
| Badge          | 通常用于向用户传达数值或指示物品的状态。                     | no       | ios/android | yes               |
| BottomSheet    | 从屏幕底部显示内容。这将从屏幕底部打开。                     | no       | ios/android | no                |
| Checkbox       | 复选框，可用于用户选择选项或切换设置的操作。                 | no       | ios/android | yes               |
| Chips          | 可以显示文本、图标，也可以同时显示两者。                     | no       | ios/android | yes               |
| Dialogs        | 弹窗组件。                                                   | no       | ios/android | yes               |
| Divider        | 分隔符组件。                                                 | no       | ios/android | yes               |
| FAB            | 浮动操作按钮（FAB）在屏幕上执行主要或最常见的操作。它出现在所有屏幕内容的前面，通常为圆形，中心有一个图标。 | no       | ios/android | yes               |
| Image          | 替代标准React Native Image组件的插件，该组件显示带有占位符的图像，并平滑地转换图像加载。 | no       | ios/android | yes               |
| Inputs         | 输入框。                                                     | no       | ios/android | partially         |
| LinearProgress | 进度指示器，向用户通知正在进行的进程的状态。                 | no       | ios/android | yes               |
| ListItem       | 用于显示信息行，如联系人列表、播放列表或菜单                 | no       | ios/android | partially         |
| Icon           | 图标组件。                                                   | no       | ios/android | partially         |
| Overlay        | 浮动在上方的视图。                                           | no       | ios/android | yes               |
| PricingCard    | 用于以美观的方式显示功能和定价表。                           | no       | ios/android | yes               |
| Rating         | 评级用于收集用户评分数据。                                   | no       | ios/android | no                |
| Switch         | 用于指示开关状态。                                           | no       | ios/android | yes               |
| SearchBar      | 搜索框组件。                                                 | no       | ios/android | partially         |
| Slider         | 滑块组件。                                                   | no       | ios/android | no                |
| Skeleton       | 加载数据之前内容的占位符预览。                               | no       | ios/android | yes               |
| SocialIcon     | 社交图标是在线和社交媒体网络的视觉提示。                     | no       | ios/android | yes               |
| SpeedDial      | 按下时，浮动动作按钮可以拨号的形式显示三到六个。             | no       | ios/android | yes               |
| Tab            | 页签组件。                                                   | no       | ios/android | yes               |
| TabView        | TabView使选项卡可滑动。                                      | no       | ios/android | yes               |
| Text           | 文本组件。                                                   | no       | ios/android | yes               |
| ThemeProvider  | 主题。                                                       | no       | ios/android | no                |
| Tile           | 像卡片这样的平铺，是显示单个主题的相关内容的一种便捷方式。   | no       | ios/android | yes               |
| Tooltip        | 当用户点击某个元素时，工具提示会显示信息性文本。             | no       | /           | no                |

## 遗留问题

## 其他

## 开源协议

本项目基于 [MIT License (MIT)](https://github.com/react-native-elements/react-native-elements/blob/next/LICENSE) ，请自由地享受和参与开源。