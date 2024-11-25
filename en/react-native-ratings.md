> Template version: v0.2.2

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

> [!TIP] [GitHub address](https://github.com/Monte9/react-native-ratings)

## Installation and Usage

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

The following code shows the basic use scenario of the repository:

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

## Constraints

### Compatibility

This document is verified based on the following versions:

1. RNOH：0.72.20; SDK：HarmonyOS NEXT Developer Beta1; IDE：DevEco Studio 5.0.3.200; ROM：3.0.0.18;
2. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;

## Properties

### This component has the following properties:
> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.。

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
> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

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

## Known Issues

## Others

## License

This project is licensed under [MIT License](https://github.com/Monte9/react-native-ratings/blob/master/LICENSE) .