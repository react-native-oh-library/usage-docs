> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>galio-framework</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/galio-org/galio">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/galio-org/galio/blob/master/LICENSE.md">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>




> [!TIP] [Github 地址](https://github.com/galio-org/galio)

## 安装与使用

<!-- tabs:start -->

#### **npm**

```bash
npm install galio-framework@0.8.0
```

#### **yarn**

```bash
yarn add galio-framework@0.8.0
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import { Card, Block, theme } from 'galio-framework';
import React, { useState } from 'react';
import { Image, ScrollView, StyleSheet, Text, View } from 'react-native';

const CardDemo = () => {
    return (
        <Block style={styles.container}>
            <Card
                flex
                borderless={false}
                title="Christopher Moon"
                caption="139 minutes ago"
                location="Los Angeles, CA"
                avatar="https://avatars.githubusercontent.com/u/155599655?v=4"
                image="https://images.unsplash.com/photo-1497802176320-541c8e8de98d?&w=1600&h=900&fit=crop&crop=entropy&q=300"
                imageStyle={styles.cardImageRadius}
                locationColor={false}
                titleColor={'red'}
                captionColor={'pink'}
                footerStyle={styles.footerStyle}
                card={false}
            />
         </Block>
    )
};

const styles = StyleSheet.create({
    container: {
        flex: 1,
        backgroundColor: '#fff',
    },
    accordion: {
        borderWidth: 1,
        borderColor: '#ccc',
        borderRadius: 5,
        overflow: 'hidden',
        shadowRadius: 10
    },
    listStyle: {
        borderTopWidth: 10,
        borderTopColor: 'red',
    },
    headerStyle: {
        backgroundColor: '#5E72E4',
        padding: 10,
    },
    contentStyle: {
        paddingVertical: 10,
        paddingHorizontal: 20,
        fontWeight: 'bold'
    },
    inputArea: {
        width: '100%',
        height: '15%',
        borderWidth: 2,
        borderColor: '#000000',
        marginTop: 8,
        justifyContent: 'center',
        alignItems: 'center',
        backgroundColor: "white"
    },
    baseText: {
        width: '100%',
        height: '100%',
        fontWeight: 'bold',
        textAlign: 'center',
        fontSize: 16,
    },
    shadow: {
        shadowColor: "red",
        shadowOffset: {
            width: 10,
            height: 3,
        },
    },
    viewShadow: {
        elevation: 1.5,
        shadowColor: "#FF9C09",
        shadowOffset: { width: 0, height: 0 },
        shadowOpacity: 1,
        shadowRadius: 1.5,
    },
    cardImageRadius: {
        borderRadius: 30,
        opacity:0.5
    },
    imageBlockStyle: {
        borderColor: 'blue',
        borderWidth: 5,
        borderBlockColor: 'yellow'
    },
    footerStyle: {
        color: 'yellow',
        backgroundColor: '#FF7167',
        fontSize: 10,
        fontWeight: 'bold',
        borderRadius:10
    }
});

export default CardDemo;
```

## Link

本库依赖react-native-vector-icons，如已在鸿蒙工程中引入过该库，则无需再次引入。

如未引入请参照[react-native-vector-icons 文档](/zh-cn/react-native-vector-icons.md)进行引入

## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

1. RNOH: 0.72.27; SDK: HarmonyOS NEXT Developer Beta1 5.0.0.25(API Version 12 Canary4); IDE: DevEco Studio 5.0.3.400SP7; ROM: 3.0.0.29;
2. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;

## 属性

详情请见[galio](https://galio.io/docs/#/components)

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 Yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

### [Accordion](https://galio.io/docs/#/components/accordion?id=accordion)

|       Name       |                         Description                          |   Type    | Required |  Platform   | HarmonyOS Support |
| :--------------: | :----------------------------------------------------------: | :-------: | :------: | :---------: | :---------------: |
|      style       | Styling the Block which encapsulates the whole FlatList used for rendering the elements. |  object   |    no    | iOS/Android |        Yes        |
|    dataArray     | Array of objects with the following keys: title, content, icon: { name, family, size, color, style} |   array   |    no    | iOS/Android |        Yes        |
|      opened      | Index number representing which of the elements of your array should be opened when the component first renders. |  number   |    no    | iOS/Android |        Yes        |
|    listStyle     |                     FlatList style prop.                     |  object   |    no    | iOS/Android |        Yes        |
|       icon       |          Icon for the un-expanded piece of content           | component |    no    | iOS/Android |        Yes        |
|   expandedIcon   |           Icon used when the content is expanded.            | component |    no    | iOS/Android |        Yes        |
|   headerStyle    |         Object styling the header of the Accordion.          |  object   |    no    | iOS/Android |        Yes        |
|   contentStyle   |     Object styling the content section of the Accordion.     |  object   |    no    | iOS/Android |        Yes        |
| onAccordionClose | Function called when the user closes one of the Accordion's items. | function  |    no    | iOS/Android |        Yes        |
| onAccordionOpen  | Function called when the user expands one of the Accordion's items. | function  |    no    | iOS/Android |        Yes        |

###  [Block](https://github.com/galio-org/galio/blob/master/LICENSE.md)

|    Name     |                    Description                     |      Type       | Required |  Platform   | HarmonyOS Support |
| :---------: | :------------------------------------------------: | :-------------: | :------: | :---------: | :---------------: |
|   bottom    |    alignItems: 'flex-end' alignSelf: 'flex-end'    |     boolean     |    no    | iOS/Android |        Yes        |
|    card     | changes the View's border-radus, -width and -color |     boolean     |    no    | iOS/Android |        Yes        |
|   center    |      alignItems: 'center' alignSelf: 'center'      |     boolean     |    no    | iOS/Android |        Yes        |
|    flex     |           flex: 1 **or** `<yourNumber>`            | boolean, number |    no    | iOS/Android |        Yes        |
|    fluid    |                   width: 'auto'                    |     boolean     |    no    | iOS/Android |        Yes        |
|   height    |          changes the height of the Block           |     number      |    no    | iOS/Android |        Yes        |
|    left     |              alignItems: 'flex-start'              |     boolean     |    no    | iOS/Android |        Yes        |
|   middle    |     alignItems: 'center' alignSelf: 'center'.      |     boolean     |    no    | iOS/Android |        Yes        |
|    right    |              alignItems: 'flex-start'              |     boolean     |    no    | iOS/Android |        Yes        |
|     row     |                flexDirection: 'row'                |     boolean     |    no    | iOS/Android |        Yes        |
|    safe     |        Wraps the Block with a SafeAreaView         |     boolean     |    no    | iOS/Android |        Yes        |
|   shadow    |              adds shadow on the Block              |     boolean     |    no    | iOS/Android |        Yes        |
| shadowColor |             changes the shadow's color             |     string      |    no    | iOS/Android |        Yes        |
|    space    | your options are: 'between', 'around' or 'evenly'  |     string      |    no    | iOS/Android |        Yes        |
|     top     |  alignItems: 'flex-start' alignSelf: 'flex-start'  |     boolean     |    no    | iOS/Android |        Yes        |
|    width    |           changes the width of the Block           |     number      |    no    | iOS/Android |        Yes        |

### [Button](https://galio.io/docs/#/components/button?id=button)

|    Name     |                         Description                          |      Type       | Required |  Platform   | HarmonyOS Support |
| :---------: | :----------------------------------------------------------: | :-------------: | :------: | :---------: | :---------------: |
| capitalize  |      Transforms the first character in a capital letter      |     boolean     |    no    | iOS/Android |        Yes        |
|    color    | your options are: 'primary', 'theme', 'warning', 'success', 'transparent' or your own color |     string      |    no    | iOS/Android |        Yes        |
|  disabled   |                     Disables the button                      |     boolean     |    no    | iOS/Android |        Yes        |
|    icon     |        pick whatever icon you want from Expo's icons         | boolean, string |    no    | iOS/Android |        Yes        |
|  iconColor  |                    sets the icon's color                     | boolean, string |    no    | iOS/Android |        Yes        |
| iconFamily  | pick whatever icon family suits the icon you chose from Expo's icons |     number      |    no    | iOS/Android |        Yes        |
|  iconSize   |                     sets the icon's size                     |     boolean     |    no    | iOS/Android |        Yes        |
|   loading   |               Uses the for the loading effect                |     boolean     |    no    | iOS/Android |        Yes        |
| loadingSize |              your options are: 'small', 'large'              |     boolean     |    no    | iOS/Android |        Yes        |
|  lowercase  |                 makes all letters lowercase                  |     boolean     |    no    | iOS/Android |        Yes        |
|  onlyIcon   | adds specific styling for using only an icon in your button  |     boolean     |    no    | iOS/Android |        Yes        |
|   opacity   |                 changes the button's opacity                 |     boolean     |    no    | iOS/Android |        Yes        |
|   radius    |                 changes the button's radius                  |     string      |    no    |     No      |        No         |
| shadowColor | the default shadowColor is based on the button's color but you can also write a specific shadowColor |     string      |    no    | iOS/Android |        Yes        |
| shadowless  |                        removes shadow                        |     boolean     |    no    | iOS/Android |        Yes        |
|    size     |              your options are: 'large', 'small'              |     number      |    no    | iOS/Android |        Yes        |
|  uppercase  |                 makes all letters uppercase                  |     boolean     |    no    | iOS/Android |        Yes        |

### [Card](https://galio.io/docs/#/components/card?id=card)

|      Name       |                         Description                          |      Type       | Required |  Platform   | HarmonyOS Support |
| :-------------: | :----------------------------------------------------------: | :-------------: | :------: | :---------: | :---------------: |
|      card       |                 adding the necessary styles                  |     boolean     |    no    | iOS/Android |        Yes        |
|     shadow      |           adding the necessary styles for shadows            |     boolean     |    no    | iOS/Android |        Yes        |
|   borderless    |                   adding the card's border                   |     boolean     |    no    | iOS/Android |        Yes        |
|      image      |         write your relative path or URL to the image         |     string      |    no    | iOS/Android |        Yes        |
| imageBlockStyle |           styles for the Block wrapping the Image            |     string      |    no    | iOS/Android |        Yes        |
|   imageStyle    |                     styles for the Image                     |     object      |    no    | iOS/Android |        Yes        |
|     avatar      |    write your relative path or URL to the avatar's image     |     string      |    no    | iOS/Android |        Yes        |
|    location     | where is this coming from? write the location of the author  |     string      |    no    | iOS/Android |        Yes        |
|  locationColor  | the default locationColor is based on themes.COLORS.MUTED, but you can also write your own color | boolean, string |    no    | iOS/Android |        Yes        |
|      title      |                 write your main card's title                 |     string      |    no    | iOS/Android |        Yes        |
|   titleColor    |                  change your title's color                   |     string      |    no    | iOS/Android |        Yes        |
|     caption     |                 write your main card's title                 |     string      |    no    | iOS/Android |        Yes        |
|  captionColor   |                 change your caption's color                  |     string      |    no    | iOS/Android |        Yes        |
|   footerStyle   |   styles for the block wrapping the whole author's section   |     object      |    no    | iOS/Android |        Yes        |

### [Checkbox](https://galio.io/docs/#/components/checkbox?id=checkbox)

|     Name      |                         Description                          |                             Type                             | Required |  Platform   | HarmonyOS Support |
| :-----------: | :----------------------------------------------------------: | :----------------------------------------------------------: | :------: | :---------: | :---------------: |
| checkboxStyle | By sending an object you can style the checkbox's color, size and more |                             any                              |    no    | iOS/Android |        Yes        |
|   disabled    |  This disables the possibility of the checkbox being used.   |                           boolean                            |    no    | iOS/Android |        Yes        |
| flexDirection | Maybe you need the checkbox to be on top of an image? You can do that with this prop. | oneOf(['row', 'row-reverse', 'column', 'column-reverse']), string |    no    | iOS/Android |        Yes        |
|   iconColor   |              This prop changes the icon color.               |                            string                            |    no    | iOS/Android |        Yes        |
|   iconName    |                 This prop changes the icon.                  |                            string                            |    no    | iOS/Android |        Yes        |
|   iconSize    |           This prop changes the size of the icon.            |                            number                            |    no    | iOS/Android |        Yes        |
|  iconFamily   | In case you need an icon from a different package, this prop helps you change the icon package. |                            string                            |    no    | iOS/Android |        Yes        |
|     image     |      This allows you to place an image instead of text.      |                            string                            |    no    | iOS/Android |        Yes        |
|  imageStyle   |            Style the way your image looks here！             |                             any                              |    no    | iOS/Android |        Yes        |
| initialValue  | Should the initial state of your checkbox be false or true?  |                           boolean                            |    no    | iOS/Android |        Yes        |
|     label     |               The text next to your checkbox.                |                            string                            |    no    | iOS/Android |        Yes        |
|  labelStyle   |                  Style your checkbox's text                  |                             any                              |    no    | iOS/Android |        Yes        |
|   onChange    | This prop take an arrow function and everytime the user presses the checkbox the function is called. |                           function                           |    no    | iOS/Android |        Yes        |

### [Deck Swiper](https://galio.io/docs/#/components/deckswiper?id=deck-swiper)

|        Name         |                         Description                          |   Type   | Required |  Platform   | HarmonyOS Support |
| :-----------------: | :----------------------------------------------------------: | :------: | :------: | :---------: | :---------------: |
|        style        | Styling the Block which encapsulates the components used for swiping. |  object  |    no    | iOS/Android |        Yes        |
|     components      |      An array of components used for building the deck.      |  array   |    no    | iOS/Android |        Yes        |
|    onSwipeRight     |         Function called when the user swipes right.          | function |    no    | iOS/Android |        Yes        |
|     onSwipeLeft     |          Function called when the user swipes left.          | function |    no    | iOS/Android |        Yes        |
| focusedElementStyle |          Styling for the first element of the deck.          |  object  |    no    | iOS/Android |        Yes        |
|  nextElementStyle   | Styling for the elements underneath the first element of the deck. |  object  |    no    | iOS/Android |        Yes        |

### [Icon](https://galio.io/docs/#/components/icon?id=icon)

|  Name  |                  Description                  |  Type  | Required |  Platform   | HarmonyOS Support |
| :----: | :-------------------------------------------: | :----: | :------: | :---------: | :---------------: |
|  name  | Choose your Icon's name from Expo's icon list | string |    no    | iOS/Android |        Yes        |
| family | Choose your Icon's family from the same list  | string |   yes    | iOS/Android |        Yes        |
|  size  |          This sets your Icon's size           | number |    no    | iOS/Android |        Yes        |
| color  |          This sets your Icon's color          | string |    no    | iOS/Android |        Yes        |

### [Input](https://galio.io/docs/#/components/input?id=input)

|         Name         |                         Description                          |  Type   | Required |  Platform   | HarmonyOS Support |
| :------------------: | :----------------------------------------------------------: | :-----: | :------: | :---------: | :---------------: |
|         type         | this is basically the TextInput's keyboardType prop and it has the next options: 'default', 'number-pad', 'decimal-pad', 'numeric', 'email-address', 'phone-pad'. | string  |    no    | iOS/Android |        Yes        |
|       password       |  Tells the input that this is going to be a password input   | boolean |    no    | iOS/Android |        Yes        |
| placeholderTextColor |              Sets the placeholder's text color               | string  |    no    | iOS/Android |        Yes        |
|        label         |                 Sets the label of the input                  | string  |    no    | iOS/Android |        Yes        |
|       bgColor        |               Sets the Input's backgroundColor               | string  |    no    | iOS/Android |        Yes        |
|       rounded        |                Sets the corners to be rounded                | boolean |    no    | iOS/Android |        Yes        |
|      borderless      |              Sets the Input's borderWidth to 0               | boolean |    no    | iOS/Android |        Yes        |
|       viewPass       | Adds the functionality of pressing a button in order to see your password's letters | boolean |    no    | iOS/Android |        Yes        |
|         icon         |        Choose your Icon's name from Expo's icon list         | string  |    no    | iOS/Android |        Yes        |
|      iconColor       |                   Changes the Icon's color                   | string  |    no    | iOS/Android |        Yes        |
|        family        |         Choose your Icon's family from the same list         | string  |    no    | iOS/Android |        Yes        |
|        color         |                 Sets the Input's text color.                 | string  |    no    | iOS/Android |        Yes        |
|         help         | Sets a helper line for more information regarding your input. | string  |    no    | iOS/Android |        Yes        |
|         left         |           Sets the Icon to the left of the Input.            | boolean |    no    | iOS/Android |        Yes        |
|        right         |           Sets the Icon to the right of the Input.           | boolean |    no    | iOS/Android |        Yes        |
|       topHelp        |            Sets the helper line above the input.             | boolean |    no    | iOS/Android |        Yes        |
|      bottomHelp      |            Sets the helper line below the input.             | boolean |    no    | iOS/Android |        Yes        |

### [NavBar](https://galio.io/docs/#/components/navbar?id=navbar)

|     Name      |                         Description                          |     Type     | Required |  Platform   | HarmonyOS Support |
| :-----------: | :----------------------------------------------------------: | :----------: | :------: | :---------: | :---------------: |
|     back      |             Adds a back button for your navBar.              |   boolean    |    no    | iOS/Android |        Yes        |
|  transparent  |  Sets the backgroundColor and borderColor to 'transparent'   |   boolean    |    no    | iOS/Android |        Yes        |
|     title     |                     Title of the NavBar                      | node, string |    no    | iOS/Android |        Yes        |
|  titleStyle   |                Sets the styling for the title                |    object    |    no    | iOS/Android |        Yes        |
|     left      |                   Left side of the NavBar                    |     node     |    no    | iOS/Android |        Yes        |
|   leftStyle   | Sets the styling for the View wrapping the left side element. |    object    |    no    | iOS/Android |        Yes        |
| leftIconColor |           Sets the color of the left side's icon.            |    string    |    no    | iOS/Android |        Yes        |
|  onLeftPress  |           Function for the left side of the navbar           |   function   |    no    | iOS/Android |        Yes        |
|     right     |                   Right side of the NavBar                   |     node     |    no    | iOS/Android |        Yes        |
|  rightStyle   | Sets the styling for the View wrapping the left side element. |    object    |    no    | iOS/Android |        Yes        |

### [Radio](https://galio.io/docs/#/components/radio?id=radio)

|      Name       |                Description                |                             Type                             | Required |  Platform   | HarmonyOS Support |
| :-------------: | :---------------------------------------: | :----------------------------------------------------------: | :------: | :---------: | :---------------: |
|      color      |                  color.                   |                            string                            |    no    | iOS/Android |        Yes        |
| containerStyle  |              Container Style              |                             any                              |    no    | iOS/Android |        Yes        |
| radioOuterStyle |            Title of the NavBar            |                             any                              |    no    | iOS/Android |        Yes        |
| radioInnerStyle |      Sets the styling for the title       |                             any                              |    no    | iOS/Android |        Yes        |
|    disabled     |              Prohibited Use               |                           boolean                            |    no    | iOS/Android |        Yes        |
|  flexDirection  | Determines the direction of the main axis | oneOfType(['row', 'row-reverse', 'column', 'column-reverse']), string |    no    | iOS/Android |        Yes        |
|  initialValue   |               Initial Value               |                           boolean                            |    no    | iOS/Android |        Yes        |
|      label      |                   Label                   |                            string                            |    no    | iOS/Android |        Yes        |
|   labelStyle    |               Label Styles                |                             any                              |    no    | iOS/Android |        Yes        |
|    onChange     |       Change when radio is seleted        |                           function                           |    no    | iOS/Android |        Yes        |

### [Text](https://galio.io/docs/#/components/text?id=text)

|  Name  |                 Description                  |  Type   | Required |  Platform   | HarmonyOS Support |
| :----: | :------------------------------------------: | :-----: | :------: | :---------: | :---------------: |
|   h1   |      Sets the text's fontSize to 44px.       | boolean |    no    | iOS/Android |        Yes        |
|   h2   |      Sets the text's fontSize to 38px.       | boolean |    no    | iOS/Android |        Yes        |
|   h3   |      Sets the text's fontSize to 30px.       | boolean |    no    | iOS/Android |        Yes        |
|   h4   |      Sets the text's fontSize to 24px.       | boolean |    no    | iOS/Android |        Yes        |
|   h5   |      Sets the text's fontSize to 18px.       | boolean |    no    | iOS/Android |        Yes        |
|   p    |      Sets the text's fontSize to 16px.       | boolean |    no    | iOS/Android |        Yes        |
|  size  |        Sets the fontSize of the text.        | number  |    no    | iOS/Android |        Yes        |
| color  |         Sets the color of the text.          | string  |    no    | iOS/Android |        Yes        |
| muted  | Changes the text color to theme.COLORS.MUTED | boolean |    no    | iOS/Android |        Yes        |
|  bold  |        Sets the fontWeight to 'bold'.        | boolean |    no    | iOS/Android |        Yes        |
| italic |       Sets the fontStyle to 'italic'.        | boolean |    no    | iOS/Android |        Yes        |

### [Toast Notification](https://galio.io/docs/#/components/toastnotification?id=toast-notification)

|       Name        |                         Description                          |    Type     | Required |  Platform   | HarmonyOS Support |
| :---------------: | :----------------------------------------------------------: | :---------: | :------: | :---------: | :---------------: |
|       style       |             Styling the Block which encapsulate              |   object    |    no    | iOS/Android |        Yes        |
|     children      | The content of your toast notification. You can even just write a text or create your own component. | node/string |    no    | iOS/Android |        Yes        |
|      isShow       |         Toggle between the toast being shown or not.         |    bool     |    no    | iOS/Android |        Yes        |
| positionIndicator |              one of: 'top', 'center', 'bottom'               |   string    |    no    | iOS/Android |        Yes        |
|  positionOffset   |                  Whether to use positioning                  |   number    |    no    | iOS/Android |        Yes        |
|  fadeInDuration   |         The number of ms for the fade in animation.          |   number    |    no    | iOS/Android |        Yes        |
|  fadeOutDuration  |         The number of ms for the fade out animation.         |   number    |    no    | iOS/Android |        Yes        |
|       color       |   one of: 'primary', 'theme', 'info', 'warning', 'success'   |   string    |    no    | iOS/Android |        Yes        |
|       round       |         Maybe you want a rounded toast notification?         |   boolean   |    no    | iOS/Android |        Yes        |
|     textStyle     |     Style object for the children prop used as a string.     |   object    |    no    | iOS/Android |        Yes        |

### [Slider](https://galio.io/docs/#/components/slider?id=slider)

|       Name        |                         Description                          |   Type   | Required |  Platform   | HarmonyOS Support |
| :---------------: | :----------------------------------------------------------: | :------: | :------: | :---------: | :---------------: |
|    activeColor    |          This sets the active color of your slider.          |  string  |    no    | iOS/Android |        Yes        |
|       value       | The initial value at which the thumb of the slider is positioned |  number  |    no    | iOS/Android |        Yes        |
|     disabled      |       This prop makes the slider unusable to the user.       | boolean  |    no    | iOS/Android |        Yes        |
|   minimumValue    |            Sets the minimum value for the Slider.            |  number  |    no    | iOS/Android |        Yes        |
|   maximumValue    |            Sets the maximum value for the Slider.            |  number  |    no    | iOS/Android |        Yes        |
|    trackStyle     | By passing an object you can style the track of the Slider.  |   any    |    no    | iOS/Android |        Yes        |
|    thumbStyle     | By passing an object you can style the thumb of the Slider.  |   any    |    no    | iOS/Android |        Yes        |
|       step        |    This is a stepper. It sets fixed values for the thumb.    |  number  |    no    | iOS/Android |        Yes        |
| onSlidingComplete | By passing an arrow function you can decide what is going to happen when the Sliding is complete | function |    no    | iOS/Android |        Yes        |
|  onSlidingStart   | By passing an arrow function you can decide what is going to happen when the Sliding starts | function |    no    | iOS/Android |        Yes        |
|   onValueChange   | By passing an arrow function you can decide what is going to happen when the Sliding is moving. | function |    no    | iOS/Android |        Yes        |

### [Switch](https://galio.io/docs/#/components/switch?id=switch)

|        Name         |                 Description                  |                             Type                             | Required |  Platform   | HarmonyOS Support |
| :-----------------: | :------------------------------------------: | :----------------------------------------------------------: | :------: | :---------: | :---------------: |
|        color        |                 Switch Color                 | oneOfType(['primary', 'theme', 'error', 'warning', 'success', 'info']), string |    no    |     No      |        No         |
|      disabled       |        Whether the switch is disabled        |                           boolean                            |    no    | iOS/Android |        Yes        |
|    initialValue     |                Initial value                 |                           boolean                            |    no    | iOS/Android |        Yes        |
|     trackColor      |                 track Color                  |                            object                            |    no    | iOS/Android |        Yes        |
| ios_backgroundColor |             ios background color             |                            string                            |    no    | iOS/Android |        Yes        |
|      onChange       | Events that occur when the switch is changed |                           function                           |   yes    | iOS/Android |        Yes        |

### [GalioTheme](https://galio.io/docs/?ref=galio-repo#/GalioTheme?id=galiotheme-usage)

| Name  |                         Description                          |  Type  | Required |  Platform   | HarmonyOS Support |
| :---: | :----------------------------------------------------------: | :----: | :------: | :---------: | :---------------: |
| color | Theme color, [COLORS reference table](https://galio.io/docs/?ref=galio-repo#/GalioTheme?id=colors-reference-table) | Object |    no    | iOS/Android |        Yes        |
| size  | Set Font Size,  [SIZES reference table](https://galio.io/docs/?ref=galio-repo#/GalioTheme?id=sizes-reference-table) | Object |    no    | iOS/Android |        Yes        |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License(MIT)](https://github.com/galio-org/galio/blob/master/LICENSE.md)，请自由地享受和参与开源。

