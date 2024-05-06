模板版本：v0.2.0

<p align="center">
  <h1 align="center"> <code>react-native-canvas</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/iddan/react-native-canvas/blob/v0.1.39/license.txt">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>




> [!TIP] [Github 地址](https://github.com/iddan/react-native-canvas)

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-canvas@0.1.39
```

#### **yarn**

```bash
yarn add react-native-canvas@0.1.39
```

[!TIP] 如果依赖未完全安装，请执行：
```bash
npm install --save-dev @type/react-native-canvas@0.1.39
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

```tsx
import React, { useRef, useEffect } from 'react';
import { View, StyleSheet, Text, ScrollView } from 'react-native';
import Canvas, { Image as CanvasImage, CanvasRenderingContext2D, Path2D } from 'react-native-canvas';

const CanvasDemo = () => {

  const canvasRef = useRef<Canvas>(null);

  useEffect(() => {
    const canvas = canvasRef.current;
    if (canvas) {
      canvas.width = 300;
      canvas.height = 500;
      const context = canvas.getContext('2d') as CanvasRenderingContext2D;

      // 绘制背景
      context.fillStyle = 'gray';
      context.fillRect(0, 0, 1000, 1000);

      //绘制矩形
      context.fillStyle = 'blue';
      context.fillRect(10, 10, 100, 100);

      //绘制椭圆
      const ellipse = new Path2D(canvas);
      ellipse.ellipse(200, 60, 50, 30, 0, 0, 2 * Math.PI);
      context.fillStyle = 'green';
      context.fill(ellipse);

      //绘制线条
      context.beginPath();
      context.moveTo(10, 150);
      context.lineTo(150, 150);
      context.strokeStyle = 'red';
      context.stroke();

      // 绘制文字
      context.font = 'bold 24px Arial';
      context.fillStyle = 'orange';
      context.fillText('Hello World', 20, 200);

      //绘制图片
      const image = new CanvasImage(canvas);
      image.src = 'https://upload.wikimedia.org/wikipedia/commons/6/63/Biho_Takashi._Bat_Before_the_Moon%2C_ca._1910.jpg';
      image.addEventListener('load', () => {
        context.drawImage(image, 10, 250, 100, 100);
      });
    }
  }, []);

  return (
    <ScrollView>
      <View style={styles.container}>
        <Text style={styles.title}>Canvas Demo Start</Text>
        <Canvas ref={canvasRef} style={styles.canvas} />
        <Text style={styles.title}>Canvas Demo End</Text>
      </View>
    </ScrollView>
  );
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
    alignItems: 'center',
    justifyContent: 'center',
    paddingVertical: 50,
  },
  title: {
    fontSize: 24,
    fontWeight: 'bold',
    marginBottom: 20,
  },
  canvas: {
    width: 300,
    height: 500,
    backgroundColor: 'blue',
  },
});

export default CanvasDemo;
```

##  Link

本库鸿蒙侧实现依赖@react-native-oh-tpl/react-native-webview 的原生端代码，如已在鸿蒙工程中引入过该库，则无需再次引入，可跳过本章节步骤，直接使用。

如未引入请参照[@react-native-oh-tpl/react-native-webview 文档的 Link 章节](https://gitee.com/zhanghao2519/usage-docs/blob/master/zh-cn/react-native-webview.md)进行引入

## 兼容性

在以下版本验证通过

1. RNOH：0.72.20; SDK：HarmonyOS NEXT Developer Preview2; IDE：DevEco Studio 5.0.3.200; ROM：205.0.0.18;

## 属性

| Name           | Description                                                  | Type     | Required | Platform    | HarmonyOS Support |
| -------------- | ------------------------------------------------------------ | -------- | -------- | ----------- | ----------------- |
| `heigth`       | Reflects the height of the canvas in pixels.                 | number   | yes      | Android IOS | YES               |
| `width`        | Reflects the width of the canvas in pixels.                  | number   | yes      | Android IOS | YES               |
| `getContext()` | Standard CanvasRenderingContext2D. [MDN](https://developer.mozilla.org/en/docs/Web/API/CanvasRenderingContext2D). Only difference is `await` should be used to retrieve values from methods.. | function | yes      | Android IOS | YES               |
| `Image()`      | WebView Image constructor. Unlike in the browsers accepts canvas as first argument. [MDN](https://developer.mozilla.org/en-US/docs/Web/API/HTMLImageElement/Image) | function | No       | Android IOS | YES               |
| `Path2D()`     | Path2D API constructor. Unlike in the browsers, this requires the canvas as first argument. See also https://developer.mozilla.org/en-US/docs/Web/API/Path2D/Path2D.. | function | No       | Android IOS | YES               |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/iddan/react-native-canvas/blob/master/license.txt) ，请自由地享受和参与开源。

