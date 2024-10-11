<!-- {% raw %} -->
> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-canvas</code> </h1>
</p>
<p align="center">
        <a href="https://github.com/iddan/react-native-canvas">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20windows%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/iddan/react-native-canvas/blob/master/license.txt">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>



> [!TIP] [Github address](https://github.com/iddan/react-native-canvas)

## Installation and Usage

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-canvas@0.1.39
```

#### **yarn**

```bash
yarn add react-native-canvas@0.1.39
```

[!TIP] If the dependency is not fully installed, please perform:
```bash
npm install --save-dev @type/react-native-canvas@0.1.39
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```tsx
import React, { useRef, useEffect } from "react";
import { View, StyleSheet, Text, ScrollView } from "react-native";
import Canvas, {
  Image as CanvasImage,
  CanvasRenderingContext2D,
  Path2D
} from "react-native-canvas";

const CanvasDemo = () => {
  const canvasRef = useRef<Canvas>(null);

  useEffect(() => {
    const canvas = canvasRef.current;
    if (canvas) {
      canvas.width = 300;
      canvas.height = 500;
      const context = canvas.getContext("2d") as CanvasRenderingContext2D;

      // draw Background
      context.fillStyle = "gray";
      context.fillRect(0, 0, 1000, 1000);

      //draw rectangle
      context.fillStyle = "blue";
      context.fillRect(10, 10, 100, 100);

      //draw an ellipse
      const ellipse = new Path2D(canvas);
      ellipse.ellipse(200, 60, 50, 30, 0, 0, 2 * Math.PI);
      context.fillStyle = "green";
      context.fill(ellipse);

      //draw lines
      context.beginPath();
      context.moveTo(10, 150);
      context.lineTo(150, 150);
      context.strokeStyle = "red";
      context.stroke();

      // draw Text
      context.font = "bold 24px Arial";
      context.fillStyle = "orange";
      context.fillText("Hello World", 20, 200);

      //draw a picture
      const image = new CanvasImage(canvas);
      image.src =
        "https://upload.wikimedia.org/wikipedia/commons/6/63/Biho_Takashi._Bat_Before_the_Moon%2C_ca._1910.jpg";
      image.addEventListener("load", () => {
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
    alignItems: "center",
    justifyContent: "center",
    paddingVertical: 50,
  },
  title: {
    fontSize: 24,
    fontWeight: "bold",
    marginBottom: 20,
  },
  canvas: {
    width: 300,
    height: 500,
    backgroundColor: "blue",
  },
});

export default CanvasDemo;
```

## Link

The HarmonyOS implementation of this library relies on the native code of @react-native-oh-tpl/react-native-webview，If the library has already been introduced in the HarmonyOS project, there is no need to introduce it again. You can skip the steps in this chapter and use it directly.

If not introduced, please refer to the Link section of the document[@react-native-oh-tpl/react-native-webview ](react-native-webview.md)for introduction.

## Constraints

### Compatibility

This document is verified based on the following versions:

1. RNOH：0.72.20; SDK：HarmonyOS NEXT Developer Preview2; IDE：DevEco Studio 5.0.3.200; ROM：205.0.0.18;

## Properties

| Name           | Description                                                                                                                                                                                   | Type     | Required | Platform    | HarmonyOS Support |
| -------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | -------- | ----------- | ----------------- |
| `heigth`       | Reflects the height of the canvas in pixels.                                                                                                                                                  | number   | yes      | Android IOS | YES               |
| `width`        | Reflects the width of the canvas in pixels.                                                                                                                                                   | number   | yes      | Android IOS | YES               |
| `getContext()` | Standard CanvasRenderingContext2D. [MDN](https://developer.mozilla.org/en/docs/Web/API/CanvasRenderingContext2D). Only difference is `await` should be used to retrieve values from methods.. | function | yes      | Android IOS | YES               |
| `Image()`      | WebView Image constructor. Unlike in the browsers accepts canvas as first argument. [MDN](https://developer.mozilla.org/en-US/docs/Web/API/HTMLImageElement/Image)                            | function | No       | Android IOS | YES               |
| `Path2D()`     | Path2D API constructor. Unlike in the browsers, this requires the canvas as first argument. See also https://developer.mozilla.org/en-US/docs/Web/API/Path2D/Path2D..                         | function | No       | Android IOS | YES               |

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/iddan/react-native-canvas/blob/master/license.txt).
<!-- {% endraw %} -->