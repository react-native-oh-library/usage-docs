<!-- {% raw %} -->
> 模板版本：v0.2.0

<p align="center">
  <h1 align="center"> <code>react-native-image-gallery</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/react-native-oh-library/react-native-image-gallery">
        <img src="https://img.shields.io/badge/platforms-android%20%7C%20ios%20%7C%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="">
        <img src="https://img.shields.io/badge/license-ISC-green.svg" alt="License" />
    </a>
</p>

>   [!tip]  
>
> [Github 地址](https://github.com/react-native-oh-library/react-native-image-gallery/tree/sig)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-image-gallery Releases](https://github.com/react-native-oh-library/react-native-image-gallery/releases)，并下载适用版本的 tgz 包

进入到工程目录并输入以下命令：

<!-- tabs:start -->

>  [!TIP] 
>
> 处替换为 tgz 包的路径

#### **npm**

```bash
npm i @react-native-oh-tpl/react-native-image-gallery@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-image-gallery@file:#
```

<!-- tabs:end -->

快速使用：

> [!WARNING] 使用时 import 的库名不变。

```js
import Gallery from 'react-native-image-gallery';

  render() {
    return (
      <Gallery
        style={{ flex: 1, backgroundColor: 'black' }}
        images={[
          { source: require('yourApp/image.png'), dimensions: { width: 150, height: 150 } },
          { source: { uri: 'http://i.imgur.com/XP2BE7q.jpg' } },
          { source: { uri: 'http://i.imgur.com/5nltiUd.jpg' } },
          { source: { uri: 'http://i.imgur.com/6vOahbP.jpg' } },
          { source: { uri: 'http://i.imgur.com/kj5VXtG.jpg' } }
        ]}
      />
    );
  }
```

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-native-image-gallery Releases](https://github.com/react-native-oh-library/react-native-image-gallery/releases)

#### 属性

| Prop   | Description | Type  | Default | Platform | HarmonyOS Support |
| --------------------- | --------------------- | -------- | -------- |----------|-------------------|
`images` | Your array of images | `array` | Required | all      | yes               |
`initialPage` | Image displayed first | `number` | `0`|    all      | yes               |
`imageComponent` | Custom function to render your images, 1st param is the image props, 2nd is its dimensions | `function` | `<Image>` component|    all      | yes               |
`errorComponent` | Custom function to render the page of an image that couldn't be displayed | `function` | A `<View>` with a stylized error|    all      | yes               |
`flatListProps` | Props to be passed to the underlying `FlatList` | `object` | `{windowSize: 3}`|     all     | yes               |
`pageMargin` | Blank space to show between images | `number` | `0`|     all     | yes               |
`onPageSelected` | Fired with the index of page that has been selected | `function`|          |    all      | yes               |
`onPageScrollStateChanged` | Called when page scrolling state has changed, see [scroll state and events](#scroll-state-and-events) | `function`|     |  all        | yes               |
`onPageScroll` | Scroll event, see [scroll state and events](#scroll-state-and-events) | `function`|      |    all      | yes               |
`scrollViewStyle` | Custom style for the `FlatList` component | `object` | `{}`|     all     | yes               |
`onSingleTapConfirmed` | Fired after a single tap | `function`|   |      all    | yes               |
`onLongPress` | Fired after a long press | `function`|     |      all    | yes               |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The ISC License (ISC)](https://choosealicense.com/licenses/isc) ，请自由地享受和参与开源。

<!-- {% endraw %} -->