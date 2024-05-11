> 模板版本：v0.2.0

<p align="center">
  <h1 align="center"> <code>react-native-ratings</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/Monte9/react-native-ratings">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/Monte9/react-native-ratings/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/Monte9/react-native-ratings)

## 安装与使用

<!-- tabs:start -->

#### **npm**

```bash
npm install --save react-native-ratings@8.1.0
```

#### **yarn**

```bash
yarn add react-native-ratings@8.1.0
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

```tsx
import React, { useState } from 'react';
import { View, Text, StyleSheet } from 'react-native';
import { Rating, AirbnbRating } from 'react-native-ratings';

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
    padding: 20,
    backgroundColor: '#f2f2f2',
  },
  title: {
    fontSize: 18,
    fontWeight: 'bold',
    marginTop: 20,
    marginBottom: 10,
  }
});

export function RatingsDemo () {
  const [rating, setRating] = useState(3);

  const ratingCompleted = (rating: number) => {
    console.log("Rating is: " + rating);
    setRating(rating);
  };

  return (
    <View style={styles.container}>
      <Text style={styles.title}>Standard Rating</Text>
      <Rating
        type="star"
        ratingCount={5}
        imageSize={30}
        showRating
        onFinishRating={ratingCompleted}
      />

      <Text style={styles.title}>Custom Icon Rating</Text>
      <Rating
        type="custom"
        ratingImage={require('../assets/expo.png')}
        ratingColor="#3498db"
        ratingBackgroundColor="#c8c7c8"
        ratingCount={6}
        imageSize={40}
        onFinishRating={ratingCompleted}
        style={{ paddingVertical: 10 }}
      />

      <Text style={styles.title}>Airbnb Rating</Text>
      <AirbnbRating
        count={5}
        reviews={["Terrible", "Bad", "Okay", "Good", "Great"]}
        defaultRating={3}
        size={20}
        onFinishRating={ratingCompleted}
      />

      <Text style={styles.title}>Read-only Rating</Text>
      <Rating
        readonly
        startingValue={rating}
        ratingCount={5}
        imageSize={30}
      />

      <Text style={styles.title}>Fractional Rating</Text>
      <Rating
        fractions={2}
        startingValue={2.5}
        ratingCount={5}
        imageSize={30}
        onFinishRating={ratingCompleted}
      />
    </View>
  );
};

```

## 约束与限制

#### 兼容性

在下述版本验证通过：

RNOH：0.72.20; SDK：HarmonyOS NEXT Developer Beta1; IDE：DevEco Studio 5.0.3.200; ROM：3.0.0.18;

## 属性

### 此组件有以下属性:
> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

|           Name            |                    Description                    |                           Type                           | Required |  Platform   | HarmonyOS Support |
| :-----------------------: | :-----------------------------------------------: | :------------------------------------------------------: | :------: | :---------: | :---------------: |
|     **type**     |       Choose one of the built-in types: star, rocket, bell, heart or use type custom to render a custom image (optional)        |                         String                           |    No    | iOS/Android |        Yes        |
|     **ratingImage**             |                   Pass in a custom image source; use this along with type='custom' prop above (optional)                   |                         String                           |    YES   | iOS/Android |        Yes        |
|      **ratingColor**       |                 Pass in a custom fill-color for the rating icon; use this along with type='custom' prop above (optional)              |                         String                           |    No    | iOS/Android |        Yes        |
|  **ratingBackgroundColor**   |       Pass in a custom background-fill-color for the rating icon; use this along with type='custom' prop above (optional)      |                         String                           |    No    | iOS/Android |        Yes        |
|     **tintColor**     |       Color used to change the background of the rating icon (optional)        |                         String                           |    No    | iOS/Android |        Yes        |
|     **ratingCount**     |       The number of rating images to display (optional)        |                         number                           |    No    | iOS/Android |        Yes        |
|     **ratingTextColor**     |       	Color used for the text labels         |                         String                           |    No    | iOS/Android |        Yes        |
|     **imageSize**     |       The size of each rating image (optional)         |                         number                           |    No    | iOS/Android |        Yes        |
|     **showRating**     |       Displays the Built-in Rating UI to show the rating value in real-time (optional)         |                         boolean                           |    No    | iOS/Android |        Yes        |
|     **readonly**     |       Whether the rating can be modiefied by the user         |                         boolean                           |    No    | iOS/Android |        Yes        |
|     **startingValue**     |       The initial rating to render        |                         number                           |    No    | iOS/Android |        Yes        |
|     **fractions**     |       The number of decimal places for the rating value; must be between 0 and 20         |                         number                           |    No    | iOS/Android |        Yes        |
|     **minValue**     |       The minimum value the user can select         |                         number                           |    No    | iOS/Android |        Yes        |
|     **style**     |       Exposes style prop to add additonal styling to the container view (optional)         |                         style                           |    No    | iOS/Android |        Yes        |
|     **jumpValue**     |       The value to jump when rating value changes (if jumpValue === 0.5, rating value increases/decreases like 0, 0.5, 1.0, 1.5 ...). Default is 0 (not to jump)        |                         number                           |    No    | iOS/Android |        Yes        |
|     **onStartRating**     |       Callback method when the user starts rating. Gives you the start rating value as a whole number         |                         function                           |    No    | iOS/Android |        Yes        |
|     **onSwipeRating**     |       Callback method when the user is swiping. Gives you the current rating value as a whole number         |                         function                           |    No    | iOS/Android |        Yes        |
|     **onFinishRating**     |       Callback method when the user finishes rating. Gives you the final rating value as a whole number (required)         |                         function                           |    No    | iOS/Android |        Yes        |

## **API（AirbnbRating）**
> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

|           Name            |                    Description                    |                           Type                           | Required |  Platform   | HarmonyOS Support |
| :-----------------------: | :-----------------------------------------------: | :------------------------------------------------------: | :------: | :---------: | :---------------: |
|     **defaultRating**   |           Initial value for the rating           |                         number                           |    No    | iOS/Android |        Yes        |
|     **reviews**  |   Labels to show when each value is tapped e.g. If the first star is tapped, then value in index 0 will be used as the label  |                         string                           |    No    | iOS/Android |        Yes        |
|     **count**  |   Total number of ratings to display  |                         number                           |    No    | iOS/Android |        Yes        |
|     **selectedColor**  |   Pass in a custom fill-color for the rating icon  |                         string                           |    No    | iOS/Android |        Yes        |
|     **unSelectedColor**  |   Pass in a custom not fill-color for the rating icon  |                         string                           |    No    | iOS/Android |        Yes        |
|     **reviewColor**  |   Pass in a custom text color for the review text  |                         string                           |    No    | iOS/Android |        Yes        |
|     **size**  |   The size of each rating image (optional)  |                         number                           |    No    | iOS/Android |        Yes        |
|     **reviewSize**  |   Pass in a custom font size for the review text  |                         number                           |    No    | iOS/Android |        Yes        |
|     **showRating**  |   Determines if to show the reviews above the rating  |                         boolean                           |    No    | iOS/Android |        Yes        |
|     **isDisabled**  |   Whether the rating can be modiefied by the user  |                         boolean                           |    No    | iOS/Android |        Yes        |
|     **onFinishRating**  |   Callback method when the user finishes rating. Gives you the final rating value as a whole number  |                         function                           |    No    | iOS/Android |        Yes        |
|     **starContainerStyle**  |   Custom styles applied to the star container  |                         object                            |    No    | iOS/Android |        Yes        |
|     **ratingContainerStyle**  |   Custom styles applied to the rating container  |                         object                            |    No    | iOS/Android |        Yes        |
|     **starImage**  |   Pass in a custom base image source (optional)  |                         string                           |    No    | iOS/Android |        Yes        |
|     **starStyle**  |   Custom styles applied to the star (optional)  |                         object                           |    No    | iOS/Android |        Yes        |

## 遗留问题

## 其他

## 开源协议

本项目基于 [MIT License](https://github.com/Monte9/react-native-ratings/blob/master/LICENSE) ，请自由地享受和参与开源。