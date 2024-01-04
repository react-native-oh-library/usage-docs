> 模板版本：v0.0.1

<p align="center">
  <h1 align="center"> <code>rn-placeholder</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/mfrachet/rn-placeholder">
        <img src="https://img.shields.io/badge/platforms-ios%20|%20android%20|%20web%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/mfrachet/rn-placeholder/blob/master/LICENSE.md">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **yarn**

```bash
yarn add rn-placeholder
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

```js
import {
  Placeholder,
  PlaceholderMedia,
  PlaceholderLine,
  Fade,
} from "rn-placeholder";

const App = () => (
  <Placeholder
    Animation={Fade}
    Left={PlaceholderMedia}
    Right={PlaceholderMedia}
  >
    <PlaceholderLine width={80} />
    <PlaceholderLine />
    <PlaceholderLine width={30} />
  </Placeholder>
);
```

## 属性

**组件 Placeholder**

It's the wrapper around all of the other components. Using alone will not produce anything interesting. You have put some line or media inside to make it powerful.It accepts all the props of a React Native View plus:

| 名称      | 说明                                                | 类型          | 是否必填 | 原库平台 | 鸿蒙支持 |
| --------- | --------------------------------------------------- | ------------- | -------- | -------- | -------- |
| Animation | An optional component that animates the placeholder | Animations    | no       | All      | Yes      |
| Left      | An optional component to display on the left        | ComponentType | no       | All      | Yes      |
| Right     | An optional component to display on the right       | ComponentType | no       | All      | Yes      |

**_Animations_**
| 名称 | 说明 | 类型 | 是否必填 | 原库平台 | 鸿蒙支持 |
| --------- | -------------------------------------------------- | ------------- | -------- | -------- | -------- |
| Fade | AThis is the base animation that makes the placeholder become clearer on a specified interval| ComponentType | no | All | Yes |
| ShineOverlay | This applies a tiny overlay from left to right of the placeholder. It's pretty neat but it has the drawback to only work without style customization: only on white background with gray lines |ComponentType| no | All | Yes |
| Shine | The shine animation is an attempt to overcome the overlay problem of the ShineOverlay animation by animating only the differnt part of the placeholder | ComponentType | no | All | Yes |
| Loader | A simple placeholder animation based on the standard loader (ActivityIndicator) of each platforms | ComponentType | no | All | Yes |
| Progressive | I'm feel a bit guilty about that but I've stolen the idea from a design system and I can't remember which one. But I like the way it behaves | ComponentType | no | All | Yes |
| Tweaking existing animations | It's possible to tweak a specific animation by passing it additional props. However keep in mind that it's important to spread the props from the Animation render function. Else you will be in strange behaviors| ComponentType | no | All | Yes |

**组件 PlaceholderLine**

A PlaceholderLine is one of the two basic and visual components of a placeholder.

| 名称     | 说明                                                                   | 类型    | 是否必填 | 原库平台 | 鸿蒙支持 |
| -------- | ---------------------------------------------------------------------- | ------- | -------- | -------- | -------- |
| height   | The line height, default is 12                                         | number  | no       | All      | Yes      |
| color    | The line color, default is #efefef                                     | string  | no       | All      | Yes      |
| width    | The line width in percent, default is 100(%)                           | number  | no       | All      | Yes      |
| noMargin | Defines if a line should have a margin bottom or not, default is false | boolean | no       | All      | Yes      |
| style    | Customize the style of the underlying View component                   | object  | no       | All      | Yes      |

**组件 PlaceholderMedia**

A PlaceholderMedia is the second of the two basic and visual components of a placeholder. It can be used a single placeholder like following:

| 名称    | 说明                                                     | 类型   | 是否必填 | 原库平台 | 鸿蒙支持 |
| ------- | -------------------------------------------------------- | ------ | -------- | -------- | -------- |
| size    | The media size (height / width), default is 40           | number | no       | All      | Yes      |
| isRound | Defines if the media is rounded or not, default is false | string | no       | All      | Yes      |
| color   | The media color, default is #efefef                      | number | no       | All      | Yes      |
| style   | Customize the style of the underlying View component     | object | no       | All      | Yes      |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/mfrachet/rn-placeholder/blob/master/LICENSE.md) ，请自由地享受和参与开源。
