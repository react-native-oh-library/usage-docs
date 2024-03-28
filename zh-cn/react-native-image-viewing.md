> 模板版本：v0.1.2

<p align="center">
  <h1 align="center"> <code>react-native-image-viewing</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/facebook/prop-types/blob/v15.8.1/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!tip] [Github 地址][https://github.com/jobtoday/react-native-image-viewing]

## 安装与使用

<!-- tabs:start -->

进入到工程目录并输入以下命令：

#### **npm**

```bash
npm install react-native-image-viewing@0.2.2
```

#### **yarn**

```bash
yarn add react-native-image-viewing@0.2.2
```

快速使用：

```js
import ImageView from "react-native-image-viewing";

const images = [
  {
    uri: "https://images.unsplash.com/photo-1571501679680-de32f1e7aad4",
  },
  {
    uri: "https://images.unsplash.com/photo-1573273787173-0eb81a833b34",
  },
  {
    uri: "https://images.unsplash.com/photo-1569569970363-df7b6160d111",
  },
];

const [visible, setIsVisible] = useState(false);

<ImageView
  images={images}
  imageIndex={0}
  visible={visible}
  onRequestClose={() => setIsVisible(false)}
/>
```

约束与限制
-------------------------------------------------------------------------------------------------------------------------------

### 兼容性

在下述版本验证通过:

1. RNOH：0.72.5; SDK：HarmonyOS NEXT DP2; IDE：DevEco Studio 4.1.3.700; ROM：204.1.0.72(SP2DEVC00E72R1P1);

API列表
-------------------------------------------------------------------------------------------------------


| Name                   | Description                                                                                 | Type                                                        | Required | HarmonyOS Support |
| ---------------------- | ------------------------------------------------------------------------------------------- | ----------------------------------------------------------- | -------- | ----------------- |
| images                 | Array of images to display                                                                  | ImageSource[]                                               | Yes      | Yes               |
| keyExtractor           | Uniqely identifying each image                                                              | (imageSrc: ImageSource, index: number) => string            | No       | Yes               |
| imageIndex             | Current index of image to display                                                           | number                                                      | Yes      | Yes               |
| visible                | Is modal shown or not                                                                       | boolean                                                     | No       | Yes               |
| onRequestClose         | Function called to close the modal                                                          | function                                                    | Yes      | Yes               |
| onImageIndexChange     | Function called when image index has been changed                                           | function                                                    | No       | Yes               |
| onLongPress            | Function called when image long pressed                                                     | function (event: GestureResponderEvent, image: ImageSource) | No       | Yes               |
| delayLongPress         | Delay in ms, before onLongPress is called: default                                          | number                                                      | No       | Yes               |
| animationType          | Animation modal presented with: default                                                     | none, fade, slide                                           | No       | Yes               |
| presentationStyle      | Modal presentation style: default: fullScreen Android: Use overFullScreen to hide StatusBar | fullScreen, pageSheet, formSheet, overFullScreen            | No       | Yes               |
| backgroundColor        | Background color of the modal in HEX                                                        | string                                                      | No       | Yes               |
| swipeToCloseEnabled    | Close modal with swipe up or down: default                                                  | boolean                                                     | No       | Yes               |
| doubleTapToZoomEnabled | Zoom image by double tap on it: default                                                     | boolean                                                     | No       | Yes               |
| HeaderComponent        | Header component, gets current imageIndex as a prop                                         | component, function                                         | No       | Yes               |
| FooterComponent        | Footer component, gets current imageIndex as a prop                                         | component, function                                         | No       | Yes               |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/facebook/prop-types/blob/v15.8.1/LICENSE) ，请自由地享受和参与开源。
