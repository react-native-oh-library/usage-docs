> 模板版本：v0.2.2

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
npm install @rneui/themed@4.0.0-rc.8
npm install @rneui/base@4.0.0-rc.7
```

#### **yarn**

```bash
yarn add @rneui/themed@4.0.0-rc.8
yarn add @rneui/base@4.0.0-rc.7
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

```tsx
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

## Link

本库 HarmonyOS 侧实现依赖 @react-native-oh-tpl/react-native-safe-area-context 的原生端代码，如已在 HarmonyOS 工程中引入过该库，则无需再次引入，可跳过本章节步骤，直接使用。

如未引入请参照[@react-native-oh-tpl/react-native-safe-area-context 文档的 Link 章节](https://gitee.com/react-native-oh-library/usage-docs/blob/master/zh-cn/react-native-safe-area-context.md#link)进行引入。

### 在 ArkTs 侧引入和注册字体文件

步骤一：
    复制字体文件到  `entry\src\main\resources\rawfile\fonts` 目录下(如使用了外部字体文件，需要将*.ttf文件复制过来)

步骤二：
    打开 `entry/src/main/ets/pages/Index.ets`，添加以下代码

```ts
  //特别注意：FontAwesome 系列中字体的 familyName 需要通过代码逻辑自行理解
  build() {
    Column() {
      if (this.rnohCoreContext && this.shouldShow) {
        if (this.rnohCoreContext?.isDebugModeEnabled) {
          RNOHErrorDialog({ ctx: this.rnohCoreContext })
        }
        RNApp({
          rnInstanceConfig: {
            fontResourceByFontFamily:{
              "FontAwesome": $rawfile("fonts/FontAwesome.ttf"),
              "FontAwesome5_Brands": $rawfile("fonts/FontAwesome5_Brands.ttf"),
              "FontAwesome5_Regular": $rawfile("fonts/FontAwesome5_Regular.ttf"),
              "FontAwesome5_Solid": $rawfile("fonts/FontAwesome5_Solid.ttf"),
              "Pacifico-Regular": $rawfile("fonts/Pacifico-Regular.ttf"),
              "StintUltraCondensed-Regular": $rawfile("fonts/StintUltraCondensed-Regular.ttf") }
          },
        })
      }
    }
    .height('100%')
    .width('100%')
  }
```


## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

1. RNOH：0.72.26; SDK：HarmonyOS NEXT Developer Beta1; IDE：DevEco Studio 5.0.3.300; ROM：3.0.0.22;
2. RNOH：0.72.29; SDK：HarmonyOS NEXT Developer Beta6; IDE：DevEco Studio 5.0.3.700; ROM：3.0.0.60;
3. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;
## 组件

详细请查看 [react-native-elements的文档介绍](https://reactnativeelements.com)

以下为目前已支持的组件属性：

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

**AirbnbRating**：爱彼迎风格的评级组件

|         Name         |                         Description                          |         Type          | Required | Platform | HarmonyOS Support |
| :------------------: | :----------------------------------------------------------: | :-------------------: | :------: | :------: | :---------------: |
|        count         |        Total number of ratings to displayDefault is 5        |        number         |    No    |   All    |        Yes        |
|    defaultRating     |           Initial value for the ratingDefault is 3           |        number         |    No    |   All    |        Yes        |
|      isDisabled      | Whether the rating can be modiefied by the userDefault is false |        boolean        |    No    |   All    |        Yes        |
|    onFinishRating    | Callback method when the user finishes rating. Gives you the final rating value as a whole number | (number: any) => void |    No    |   All    |        Yes        |
| ratingContainerStyle |          Style for rating containerDefault is none           |      View Style       |    No    |   All    |        Yes        |
|     reviewColor      |          Color value for review.Default is #f1c40f           |        string         |    No    |   All    |        Yes        |
|      reviewSize      |             Size value for review.Default is 40              |        number         |    No    |   All    |        Yes        |
|       reviews        | Labels to show when each value is tappede.g. If the first star is tapped, then value in index 0 will be used as the labelDefault is ['Terrible', 'Bad', 'Okay', 'Good', 'Great'] |       string[]        |    No    |   All    |        Yes        |
|    selectedColor     |       Color value for filled stars.Default is #004666        |        string         |    No    |   All    |        Yes        |
|      showRating      | Determines if to show the reviews above the ratingDefault is true |        boolean        |    No    |   All    |        Yes        |
|         size         |              Size of rating imageDefault is 40               |        number         |    No    |   All    |        Yes        |
|  starContainerStyle  |           Style for star containerDefault is none            |      View Style       |    No    |   All    |        Yes        |
|      starImage       |              Pass in a custom base image source              |        string         |    No    |    No    |        No         |

**Avatar**：一个头像、Icon、字母渲染组件

|         Name          |                         Description                          |                        Type                         | Required | Platform | HarmonyOS Support |
| :-------------------: | :----------------------------------------------------------: | :-------------------------------------------------: | :------: | :------: | :---------------: |
|       Component       | Component for enclosing element (eg: TouchableHighlight, View, etc). |                   React Component                   |    No    |   All    |        Yes        |
|    ImageComponent     |              Custom ImageComponent for Avatar.               |               ComponentClass<{}, any>               |    No    |   All    |        Yes        |
|      avatarStyle      |                   Style for avatar image.                    |                     ImageStyle                      |    No    |   All    |        Yes        |
|    containerStyle     |                 Styling for outer container.                 |                     View Style                      |    No    |   All    |        Yes        |
|         icon          | Displays an icon as the main content of the Avatar. **Cannot be used alongside title**. When used with the `source` prop it will be used as the placeholder. |                     AvatarIcon                      |    No    |   All    |        Yes        |
|       iconStyle       |              Extra styling for icon component.               |                     Text Style                      |    No    |   All    |        Yes        |
|      imageProps       | Optional properties to pass to the avatar e.g "resizeMode".  |                 ImageProps(Object)                  |    No    |   All    |        Yes        |
|      onLongPress      |       Callback function when long pressing component.        |                      Function                       |    No    |   All    |        Yes        |
|        onPress        |          Callback function when pressing component.          |                      Function                       |    No    |   All    |        Yes        |
|       onPressIn       |       Called when a touch is engaged before `onPress`.       |            GestureResponderEventHandler             |    No    |   All    |        Yes        |
|      onPressOut       |      Called when a touch is released before `onPress`.       |            GestureResponderEventHandler             |    No    |   All    |        Yes        |
| overlayContainerStyle |          Style for the view outside image or icon.           |                     Text Style                      |    No    |   All    |        Yes        |
|        rounded        |                  Makes the avatar circular.                  |                       boolean                       |    No    |   All    |        Yes        |
|         size          |                     Size of the avatar.                      |     `number`,`small`,`medium`,`large`,`xlarge`      |    No    |   All    |        Yes        |
|        source         |           Image source to be displayed on avatar.            |                 ImageSourcePropType                 |    No    |   All    |        Yes        |
|      titleStyle       |                     Style for the title.                     |                     Text Style                      |    No    |   All    |        Yes        |

**Avatar.Accessory**：Avatar组件的子组件，接收所有 [Icon](https://reactnativeelements.com/docs/components/icon#props), [Image](https://reactnativeelements.com/docs/components/image#props), [Text](https://reactnative.dev/docs/text#props) 的 props

|      Name      |                    Description                    |             Type             | Required | Platform | HarmonyOS Support |
| :------------: | :-----------------------------------------------: | :--------------------------: | :------: | :------: | :---------------: |
|  onLongPress   |    Called when a long-tap gesture is detected.    | GestureResponderEventHandler |    No    |   All    |        Yes        |
|    onPress     |   Called when a single tap gesture is detected.   | GestureResponderEventHandler |    No    |   All    |        Yes        |
|   onPressIn    | Called when a touch is engaged before `onPress`.  | GestureResponderEventHandler |    No    |   All    |        Yes        |
|   onPressOut   | Called when a touch is released before `onPress`. | GestureResponderEventHandler |    No    |   All    |        Yes        |

**Badge**：徽章组件，通常用于向用户传达数值或指示物品的状态

|      Name      |                        Description                        |                  Type                  | Required | Platform | HarmonyOS Support |
| :------------: | :-------------------------------------------------------: | :------------------------------------: | :------: | :------: | :---------------: |
|   Component    |  Custom component to replace the badge outer component.   |            React Component             |    No    |   All    |        Yes        |
|   badgeStyle   | Additional styling for badge (background) view component. |               View Style               |    No    |   All    |        Yes        |
| containerStyle |                 Style for the container.                  |               View Style               |    No    |   All    |        Yes        |
|  onLongPress   |        Called when a long-tap gesture is detected.        |      GestureResponderEventHandler      |    No    |   All    |        Yes        |
|    onPress     |       Called when a single tap gesture is detected.       |                Function                |    No    |   All    |        Yes        |
|   onPressIn    |     Called when a touch is engaged before `onPress`.      |      GestureResponderEventHandler      |    No    |   All    |        Yes        |
|   onPressOut   |     Called when a touch is released before `onPress`.     |      GestureResponderEventHandler      |    No    |   All    |        Yes        |
|     status     |            Determines color of the indicator.             | `primary`,`success`,`warning` ,`error` |    No    |   All    |        Yes        |
|   textProps    |              Extra props for text component.              |               TextProps                |    No    |   All    |        Yes        |
|   textStyle    |             Extra styling for icon component.             |               Text Style               |    No    |   All    |        Yes        |
|     value      |  Text value to be displayed by badge, defaults to empty.  |               ReactNode                |    No    |   All    |        Yes        |

**BottomSheet**：从屏幕底部显示内容的组件，依赖react-native-safe-area-context三方库

|      Name       |                         Description                          |      Type       | Required | Platform | HarmonyOS Support |
| :-------------: | :----------------------------------------------------------: | :-------------: | :------: | :------: | :---------------: |
|  backdropStyle  |               Style of the backdrop container.               |   View Style    |    No    |   All    |        Yes        |
| containerStyle  | Style of the bottom sheet's container. Use this to change the color of the underlay. |   View Style    |    No    |   All    |        Yes        |
|    isVisible    |                Is the modal component shown.                 |     boolean     |    No    |   All    |        Yes        |
|   modalProps    |           Additional props handed to the `Modal`.            |   ModalProps    |    No    |   All    |        Yes        |
| onBackdropPress |                 Handler for backdrop press.                  |    Function     |    No    |   All    |        Yes        |
| scrollViewProps |              Used to add props to Scroll view.               | ScrollViewProps |    No    |   All    |        Yes        |

**Button**：按钮组件，接收所有 [TouchableOpacityProps](https://reactnative.dev/docs/touchableopacity#props) 的 props

|        Name         |                         Description                          |                             Type                             | Required | Platform | HarmonyOS Support |
| :-----------------: | :----------------------------------------------------------: | :----------------------------------------------------------: | :------: | :------: | :---------------: |
| TouchableComponent  |               Component for user interaction.                |                       typeof Component                       |    No    |   All    |        Yes        |
|    ViewComponent    |                   Component for container.                   |                       React Component                        |    No    |   All    |        Yes        |
|     buttonStyle     |         Add additional styling for button component.         |                          View Style                          |    No    |   All    |        Yes        |
|        color        |                       Color of Button                        | `string`,`primary`,`secondary`,`success` | No | All | Yes |
|   containerStyle    |               Styling for Component container.               |                          View Style                          |    No    |   All    |        Yes        |
|      disabled       |                  Disables user interaction.                  |                           boolean                            |    No    |   All    |        Yes        |
| disabledTitleStyle  |              Style of the title when disabled.               |                      disabledTitleStyle                      |    No    |   All    |        Yes        |
|        icon         | Displays a centered icon (when no title) or to the left (with text). (can be used along with iconRight as well). Can be an object or a custom component. |                           IconNode                           |    No    |   All    |        Yes        |
| iconContainerStyle  |            Styling for Icon Component container.             |                          View Style                          |    No    |   All    |        Yes        |
|    iconPosition     | Displays Icon to the position mentioned. Needs to be used along with `icon` prop. | `left`,`right`,`top`,`bottom` | No | All | Yes           |
|      iconRight      | Displays Icon to the right of title. Needs to be used along with `icon` prop. |                           boolean                            |    No    |   All    |        Yes        |
| linearGradientProps | Displays a linear gradient. See [usage](https://reactnativeelements.com/docs/components/button#linear-gradient). |                            object                            |    No    |   All    |        Yes        |
|       loading       |              Prop to display a loading spinner.              |                           boolean                            |    No    |   All    |        Yes        |
|    loadingProps     |    Add additional props for ActivityIndicator component.     |                    ActivityIndicatorProps                    |    No    |   All    |        Yes        |
|    loadingStyle     |                          View Style                          |                          View Style                          |    No    |   All    |        Yes        |
|       radius        |                       Radius of button                       | `number`,`sm`,`md`,`lg` | No | All | Yes              |
|       raised        | Add raised button styling (optional). Has no effect if `type="clear"`. |                           boolean                            |    No    |   All    |        Yes        |
|        size         |                         Button size                          |            `sm`,`md`,`lg` |    No    |   All    |        Yes        |
|        title        |                      Add button title.                       | `string`,`ReactElement<{}, string`,`JSXElementConstructor<any>>` | No |   All    |        Yes        |
|     titleProps      |           Add additional props for Text component.           |                          TextProps                           |    No    |   All    |        Yes        |
|     titleStyle      |         Add additional styling for title component.          |                          Text Style                          |    No    |   All    |        Yes        |
|        type         |                       Type of button.                        | `solid`,`clear`,`outline` |    No    |   All    |        Yes        |
|      uppercase      |                    Uppercase button title                    |                           boolean                            |    No    |   All    |        Yes        |

**ButtonGroup**：按钮组组件

|           Name            |                         Description                          |                       Type                        | Required | Platform | HarmonyOS Support |
| :-----------------------: | :----------------------------------------------------------: | :-----------------------------------------------: | :------: | :------: | :---------------: |
|         Component         |   Choose other button component such as TouchableOpacity.    |                  React Component                  |    No    |   All    |        Yes        |
|       activeOpacity       |       Add active opacity to the button in buttonGroup.       |                      number                       |    No    |   No  |        No        |
|          button           |                  Button for the component.                   |                      object                       |    No    |   No  |        No        |
|   buttonContainerStyle    |            Specify styling for button containers.            |                    View Style                     |    No    |   All    |        Yes        |
|        buttonStyle        |                 Specify styling for button.                  |                    View Style                     |    No    |   All    |        Yes        |
|          buttons          | Array of buttons for component (required), if returning a component, must be an object with { element: componentName }. | `(string`,`ButtonComponent`,`ButtonObject)[]` | No |   All    |        Yes        |
|      containerStyle       |          Specify styling for main button container.          |                    View Style                     |    No    |   All    |        Yes        |
|         disabled          | Controls if buttons are disabled. Setting `true` makes all of them disabled, while using an array only makes those indices disabled. |    `boolean`,`number[]` |No               |   All    |        Yes        |
|   disabledSelectedStyle   |       Styling for each selected button when disabled.        |                    View Style                     |    No    |   All    |        Yes        |
| disabledSelectedTextStyle | Styling for the text of each selected button when disabled.  |                    Text Style                     |    No    |   All    |        Yes        |
|       disabledStyle       |            Styling for each button when disabled.            |                    View Style                     |    No    |   All    |        Yes        |
|     disabledTextStyle     |      Styling for the text of each button when disabled.      |                    Text Style                     |    No    |   All    |        Yes        |
|     innerBorderStyle      | Update the styling of the interior border of the list of buttons. |        { color?: string; width?: number; }        |    No    |   All    |        Yes        |
|      onHideUnderlay       |             Function called on hiding underlay.              |                     Function                      |    No    |   No  |        No        |
|        onLongPress        |         Called when a long-tap gesture is detected.          |           GestureResponderEventHandler            |    No    |   No  |        No        |
|          onPress          |             Method to update Button Group Index.             |             (...args: any[]) => void              |    No    |   All    |        Yes        |
|         onPressIn         |       Called when a touch is engaged before `onPress`.       |           GestureResponderEventHandler            |    No    |   All    |        Yes        |
|        onPressOut         |      Called when a touch is released before `onPress`.       |           GestureResponderEventHandler            |    No    |   All    |        Yes        |
|      onShowUnderlay       |             Function called on showing underlay.             |                     Function                      |    No    |   All    |        Yes        |
|      selectMultiple       |         Allows the user to select multiple buttons.          |                      boolean                      |    No    |   All    |        Yes        |
|    selectedButtonStyle    |             Specify styling for selected button.             |                    View Style                     |    No    |   All    |        Yes        |
|       selectedIndex       |         Current selected index of array of buttons.          |                      number                       |    No    |   All    |        Yes        |
|      selectedIndexes      |     Current selected indexes from the array of buttons.      |                     number[]                      |    No    |   All    |        Yes        |
|     selectedTextStyle     |   Specify specific styling for text in the selected state.   |                    Text Style                     |    No    |   All    |        Yes        |
|       setOpacityTo        |                 Function to set the opacity.                 |              (value: number) => void              |    No    |   No  |        No        |
|         textStyle         |              Specify specific styling for text.              |                    Text Style                     |    No    |   All    |        Yes        |
|       underlayColor       |        Specify underlayColor for TouchableHighlight.         |                        ng                         |    No    |   No  |        No        |
|         vertical          |             Display the ButtonGroup vertically.              |                      boolean                      |    No    |   All    |        Yes        |

**Card**：卡片组件

|      Name      |      Description       |    Type    | Required | Platform | HarmonyOS Support |
| :------------: | :--------------------: | :--------: | :------: | :------: | :---------------: |
| containerStyle | Outer container style. | View Style |    No    |   All    |        Yes        |
|  wrapperStyle  | Inner container style. | View Style |    No    |   All    |        Yes        |

**Card.Divider**：卡片分割线组件，接收所有 [Divider](https://reactnativeelements.com/docs/components/divider#props) 组件的 Props

**Card.FeaturedSubtitle**：卡片功能字幕组件，接收所有 [Text](https://reactnativeelements.com/docs/components/text#props) 组件的 Props

**Card.FeaturedTitle**：卡片功能标题组件，接收所有 [Text](https://reactnativeelements.com/docs/components/text#props) 组件的 Props

**Card.Image**：卡片图片组件，接收所有 [Image](https://reactnativeelements.com/docs/components/image#props) 组件的 Props

|      Name      |                    Description                    |             Type             | Required | Platform | HarmonyOS Support |
| :------------: | :-----------------------------------------------: | :--------------------------: | :------: | :------: | :---------------: |
|  onLongPress   |    Called when a long-tap gesture is detected.    | GestureResponderEventHandler |    No    |   All    |        Yes        |
|    onPress     |   Called when a single tap gesture is detected.   | GestureResponderEventHandler |    No    |   All    |        Yes        |
|   onPressIn    | Called when a touch is engaged before `onPress`.  | GestureResponderEventHandler |    No    |   All    |        Yes        |
|   onPressOut   | Called when a touch is released before `onPress`. | GestureResponderEventHandler |    No    |   All    |        Yes        |

**Card.Title**：卡片标题组件，接收所有 [Text](https://reactnativeelements.com/docs/components/text#props) 组件的 Props

**CheckBox**：选择框组件，接收所有[View](https://reactnative.dev/docs/view#props) 的 props.

|        Name        |                   Description                   |                             Type                             | Required | Platform | HarmonyOS Support |
| :----------------: | :---------------------------------------------: | :----------------------------------------------------------: | :------: | :------: | :---------------: |
|     Component      | Specify React Native component for main button. |                       React Component                        |    No    |   All    |        Yes        |
|       center       |           Aligns checkbox to center.            |                           boolean                            |    No    |   All    |        Yes        |
|    checkedTitle    |        Specify a custom checked message.        |                            string                            |    No    |   All    |        Yes        |
|   containerStyle   |            Style of main container.             |                          View Style                          |    No    |   All    |        Yes        |
|      disabled      |           Disables user interaction.            |                           boolean                            |    No    |   All    |        Yes        |
|   disabledStyle    | Style of the checkbox container when disabled.  |                          View Style                          |    No    |   All    |        Yes        |
| disabledTitleStyle |        Style of the title when disabled.        |                          Text Style                          |    No    |   All    |        Yes        |
|     fontFamily     |         Specify different font family.          |                            string                            |    No    |   All    |        Yes        |
|     iconRight      |          Moves icon to right of text.           |                           boolean                            |    No    |   All    |        Yes        |
|       right        |            Aligns checkbox to right.            |                           boolean                            |    No    |   All    |        Yes        |
|     textStyle      |                 Style of text.                  |                          Text Style                          |    No    |   All    |        Yes        |
|       title        |               Title of checkbox.                | `string` ，`ReactElement<{}, string` ，`JSXElementConstructor<any>>` |    No    |   All    |        Yes        |
|     titleProps     | Additional props for the title Text component.  |                          TextProps                           |    No    |   All    |        Yes        |
|    wrapperStyle    |       Style for the wrapper of checkbox.        |                          View Style                          |    No    |   All    |        Yes        |

**Chip**：显示触摸区组件，接收所有 [Button](https://reactnativeelements.com/docs/components/button#props) 的props

| Name |      Description       |        Type        | Required | Platform | HarmonyOS Support |
| :--: | :--------------------: | :----------------: | :------: | :------: | :---------------: |
| type | Outer container style. | `solid`，`outline` |    No    |   All    |        Yes        |

**Dialog**：对话框组件，接收所有 [Overlay](https://reactnativeelements.com/docs/components/overlay#props) 的props

|      Name      |                        Description                        |             Type             | Required | Platform | HarmonyOS Support |
| :------------: | :-------------------------------------------------------: | :--------------------------: | :------: | :------: | :---------------: |
|    children    |                 Add Enclosed components.                  |          ReactNode           |    No    |   All    |        Yes        |
|  onLongPress   |        Called when a long-tap gesture is detected.        | GestureResponderEventHandler |    No    |    No    |        No         |
|   onPressIn    |     Called when a touch is engaged before `onPress`.      | GestureResponderEventHandler |    No    |    No    |        No         |
|   onPressOut   |     Called when a touch is released before `onPress`.     | GestureResponderEventHandler |    No    |    No    |        No         |
|  overlayStyle  | Add additional styling to the internal Overlay component. |          View Style          |    No    |   All    |        Yes        |

**Dialog.Actions**：定义对话框操作组件

|   Name   |                     Description                     |   Type    | Required | Platform | HarmonyOS Support |
| :------: | :-------------------------------------------------: | :-------: | :------: | :------: | :---------------: |
| children | Add Enclosed components as an action to the dialog. | ReactNode |    No    |   All    |        Yes        |

**Dialog.Button**：定义对话框按钮组件，接收所有 [Button](https://reactnativeelements.com/docs/components/button#props) 的props

**Dialog.Actions**：对话框加载组件

|   Name   |                     Description                     |   Type    | Required | Platform | HarmonyOS Support |
| :------: | :-------------------------------------------------: | :-------: | :------: | :------: | :---------------: |
| children | Add Enclosed components as an action to the dialog. | ReactNode |    No    |   All    |        Yes        |

**Dialog.Loading**：定义对话框操作组件

|     Name     |                     Description                      |          Type          | Required | Platform | HarmonyOS Support |
| :----------: | :--------------------------------------------------: | :--------------------: | :------: | :------: | :---------------: |
| loadingProps | Add additional props for ActivityIndicator component | ActivityIndicatorProps |    No    |   All    |        Yes        |
| loadingStyle |    Add additional styling for loading component.     |       View Style       |    No    |   All    |        Yes        |

**Dialog.Title**：定义对话框标题组件

|    Name    |                 Description                 |    Type    | Required | Platform | HarmonyOS Support |
| :--------: | :-----------------------------------------: | :--------: | :------: | :------: | :---------------: |
|   title    |              Add Dialog title.              |   string   |    No    |   All    |        Yes        |
| titleProps |  Add additional props for Text component.   | TextProps  |    No    |   All    |        Yes        |
| titleStyle | Add additional styling for title component. | Text Style |    No    |   All    |        Yes        |

**Divider**：分割线组件，接收所有 [View](https://reactnative.dev/docs/view#props) 的props.

|      Name      |                      Description                      |            Type             | Required | Platform | HarmonyOS Support |
| :------------: | :---------------------------------------------------: | :-------------------------: | :------: | :------: | :---------------: |
|     color      |              The color of the component.              |           string            |    No    |   All    |        Yes        |
|     inset      |             Applies inset to the divider.             |           boolean           |    No    |   All    |        Yes        |
|   insetType    | Applies inset to a specific direction to the divider. |  `middle`，`left`，`right`  |    No    |   All    |        Yes        |
|  orientation   |           Apply orientation to the divider.           |  `vertical` ，`horizontal`  |    No    |   All    |        Yes        |
|     style      |             Applies style to the divider.             |         View Style          |    No    |   All    |        Yes        |
|   subHeader    |          Adds subHeader text to the divider.          |           string            |    No    |   All    |        Yes        |
| subHeaderStyle |    Adds style to the subHeader text of the divider    |         Text Style          |    No    |   All    |        Yes        |
|     width      |                        number                         | Apply width to the divider. |    No    |   All    |        Yes        |

**FAB**：浮动操作按钮组件，接收所有 [Button](https://reactnativeelements.com/docs/components/button#props) 的props.

|   Name    |                         Description                          |       Type        | Required | Platform | HarmonyOS Support |
| :-------: | :----------------------------------------------------------: | :---------------: | :------: | :------: | :---------------: |
|   color   |                 Change the color of the FAB.                 |      string       |    No    |   All    |        Yes        |
| placement | FAB placement at bottom, (optional) use [`style`](https://reactnativeelements.com/docs/components/fab#style) in case of custom placement. | `left`， `right`  |    No    |   All    |        Yes        |
|   size    |                     Change Size of FAB.                      | `small` ，`large` |    No    |   All    |        Yes        |
|   style   |                        Style for FAB                         |    View Style     |    No    |   All    |        Yes        |
| upperCase |         Transform Extended Label text to uppercase.          |      boolean      |    No    |   All    |        Yes        |
|  visible  |              Decide the visibility of the FAB.               |      boolean      |    No    |   All    |        Yes        |

**Header**：浮动操作按钮组件，接收所有 [View](https://reactnative.dev/docs/view#props) 的props

|                       Name                        |                         Description                          |                 Type                 | Required | Platform | HarmonyOS Support |
| :-----------------------------------------------: | :----------------------------------------------------------: | :----------------------------------: | :------: | :------: | :---------------: |
|                   ViewComponent                   |                   Component for container.                   |           React Component            |    No    |   All    |        Yes        |
|                  backgroundColor                  |        Sets backgroundColor of the parent component.         |                string                |    No    |   All    |        Yes        |
|                  backgroundImage                  |          Sets backgroundImage for parent component.          |         ImageSourcePropType          |    No    |   All    |        Yes        |
|               backgroundImageStyle                |      Styling for backgroundImage in the main container.      |              ImageStyle              |    No    |   All    |        Yes        |
|                     barStyle                      |            Sets the color of the status bar text.            |            StatusBarStyle            |    No    |    No    |        No         |
|                  centerComponent                  |              Define your center component here.              |          HeaderSubComponent          |    No    |   All    |        Yes        |
|               centerContainerStyle                |      Styling for container around the centerComponent.       |              View Style              |    No    |   All    |        Yes        |
| Styling for container around the centerComponent. |            Add children component to the header.             | `(Element`，`Element[]) & ReactNode` |    No    |   All    |        Yes        |
|                  containerStyle                   |              Styling around the main container.              |              View Style              |    No    |   All    |        Yes        |
|                     elevated                      |                     Elevation for header                     |               boolean                |    No    |    No    |        No         |
|                   leftComponent                   |               Define your left component here.               |          HeaderSubComponent          |    No    |   All    |        Yes        |
|                leftContainerStyle                 |       Styling for container around the leftComponent.        |              View Style              |    No    |   All    |        Yes        |
|                linearGradientProps                | Displays a linear gradient. See [usage](https://reactnativeelements.com/docs/components/header#lineargradient-usage). |                Object                |    No    |    No    |        No         |
|                     placement                     |                     Alignment for title.                     |      `center`，`left`，`right`       |    No    |   All    |        Yes        |
|                  rightComponent                   |              Define your right component here.               |          HeaderSubComponent          |    No    |   All    |        Yes        |
|                rightContainerStyle                |       Styling for container around the rightComponent.       |              View Style              |    No    |   All    |        Yes        |
|                  statusBarProps                   |               Accepts all props for StatusBar.               |            StatusBarProps            |    No    |   All    |        Yes        |

**Icon**：字体图标组件，接收所有 [Text](https://reactnative.dev/docs/text#props) 的props.

|      Name      |                         Description                          |             Type             | Required | Platform | HarmonyOS Support |
| :------------: | :----------------------------------------------------------: | :--------------------------: | :------: | :------: | :---------------: |
|   Component    |                Update React Native Component.                |       React Component        |    No    |   All    |        Yes        |
|     brand      |          Uses the brands font (FontAwesome5 only).           |           boolean            |    No    |   All    |        Yes        |
| containerStyle |            Add styling to container holding icon.            |          View Style          |    No    |   All    |        Yes        |
|    disabled    | Disables onPress events. Only works when `onPress` has a handler. |           boolean            |    No    |   All    |        Yes        |
| disabledStyle  | Style for the button when disabled. Only works when `onPress` has a handler. |          View Style          |    No    |   All    |        Yes        |
|   iconProps    |     Provide all props from react-native Icon component.      |          IconProps           |    No    |   All    |        Yes        |
|  onLongPress   |         Called when a long-tap gesture is detected.          | GestureResponderEventHandler |    No    |   All    |        Yes        |
|    onPress     |        Called when a single tap gesture is detected.         | GestureResponderEventHandler |    No    |   All    |        Yes        |
|   onPressIn    |       Called when a touch is engaged before `onPress`.       | GestureResponderEventHandler |    No    |   All    |        Yes        |
|   onPressOut   |      Called when a touch is released before `onPress`.       | GestureResponderEventHandler |    No    |   All    |        Yes        |
|     raised     |                  Adds box shadow to button.                  |           boolean            |    No    |   All    |        Yes        |
|    reverse     |                    Reverses color scheme.                    |           boolean            |    No    |   All    |        Yes        |
|  reverseColor  |                 Specify reverse icon color.                  |            string            |    No    |   All    |        Yes        |
|     solid      |                     Uses the solid font.                     |           boolean            |    No    |   All    |        Yes        |
|     testID     |                       Test ID of icon.                       |            string            |    No    |   All    |        Yes        |
|      type      | Type of icon set. [Supported sets here](https://reactnativeelements.com/docs/components/icon#available-icon-sets). |            string            |    No    |   All    |        Yes        |

**Image**：图片组件，接收所有 [React Native Image](https://reactnative.dev/docs/image#props) 的props.

|          Name          |                      Description                      |                           Type                            | Required | Platform | HarmonyOS Support |
| :--------------------: | :---------------------------------------------------: | :-------------------------------------------------------: | :------: | :------: | :---------------: |
|       Component        |         Define the component passed to image.         |                      React Component                      |    No    |   All    |        Yes        |
|     ImageComponent     | Specify a different component as the Image component. |                     typeof Component                      |    No    |   All    |        Yes        |
|   PlaceholderContent   |       Content to load when Image is rendering.        | `ReactElement<any, string`，`JSXElementConstructor<any>>` |    No    |   All    |        Yes        |
| childrenContainerStyle |    Additional styling for the children container.     |                        View Style                         |    No    |   All    |        Yes        |
|     containerStyle     |         Additional styling for the container.         |                        View Style                         |    No    |   All    |        Yes        |
|      onLongPress       |      Called when a long-tap gesture is detected.      |               GestureResponderEventHandler                |    No    |   All    |        Yes        |
|        onPress         |     Called when a single tap gesture is detected.     |               GestureResponderEventHandler                |    No    |   All    |        Yes        |
|       onPressIn        |   Called when a touch is engaged before `onPress`.    |               GestureResponderEventHandler                |    No    |   All    |        Yes        |
|       onPressOut       |   Called when a touch is released before `onPress`.   |               GestureResponderEventHandler                |    No    |   All    |        Yes        |
|    placeholderStyle    |   Additional styling for the placeholder container.   |                        View Style                         |    No    |   All    |        Yes        |
|       transition       |        Perform fade transition on image load.         |                          boolean                          |    No    |   All    |        Yes        |
|   transitionDuration   |        Perform fade transition on image load.         |                          number                           |    No    |   All    |        Yes        |

**Input**：表单组件，接收所有 [React Native TextInput](https://reactnative.dev/docs/textinput#props), [View](https://reactnative.dev/docs/view#props) 的props.

|          Name           |                         Description                          |      Type       | Required | Platform | HarmonyOS Support |
| :---------------------: | :----------------------------------------------------------: | :-------------: | :------: | :------: | :---------------: |
|     InputComponent      | component that will be rendered in place of the React Native TextInput | React Component |    No    |   All    |        Yes        |
|     containerStyle      |                      Style for containe                      |   View Style    |    No    |   All    |        Yes        |
|        disabled         |                 disables the input component                 |     boolean     |    No    |   All    |        Yes        |
|   disabledInputStyle    | disabled styles that will be passed to the style props of the React Native TextInput |   Text Style    |    No    |   All    |        Yes        |
|      errorMessage       |     Error message to be displayed under the input field      |     string      |    No    |   All    |        Yes        |
|       errorProps        | props to be passed to the React Native Text component used to display the error message |     object      |    No    |   All    |        Yes        |
|       errorStyle        |                 add styling to error message                 |   Text Style    |    No    |   All    |        Yes        |
|   inputContainerStyle   |            styling for Input Component Container             |   View Style    |    No    |   All    |        Yes        |
|       inputStyle        |                  Style for Input Component                   |   Text Style    |    No    |   All    |        Yes        |
|          label          |               add a label on top of the input                |    ReactNode    |    No    |   All    |        Yes        |
|       labelProps        | props to be passed to the React Native Text component used to display the label or React Component used instead of simple string in label prop |     object      |    No    |   All    |        Yes        |
|       labelStyle        | styling for the label; You can only use this if label is a string |   Text Style    |    No    |   All    |        Yes        |
|        leftIcon         |                 displays an icon on the left                 |    IconNode     |    No    |   All    |        Yes        |
| leftIconContainerStyle  |          styling for left Icon Component container           |   View Style    |    No    |   All    |        Yes        |
|   renderErrorMessage    | If the error message container should be rendered (take up vertical space). If false, when showing errorMessage, the layout will shift to add it at that time. |     boolean     |    No    |    No    |        No         |
|        rightIcon        |                displays an icon on the right                 |    IconNode     |    No    |   All    |        Yes        |
| rightIconContainerStyle |          styling for right Icon Component container          |   View Style    |    No    |   All    |        Yes        |
|          shake          |                         Shake method                         |    Function     |    No    |   All    |        Yes        |

**LinearProgress**：加载条组件，接收所有 [View](https://reactnative.dev/docs/view#props) 的props.

|    Name    |                         Description                          |                 Type                 | Required | Platform | HarmonyOS Support |
| :--------: | :----------------------------------------------------------: | :----------------------------------: | :------: | :------: | :---------------: |
| animation  |                      Animation duration                      | `boolean` , `{ duration?: number; }` |    No    |   All    |        Yes        |
|   color    |                  Color for linear progress.                  |                string                |    No    |   All    |        Yes        |
|   style    |    Add additional styling for linear progress component.     |              View Style              |    No    |   All    |        Yes        |
| trackColor |               Track color for linear progress.               |                string                |    No    |   All    |        Yes        |
|   value    | The value of the progress indicator for the determinate variant. Value between 0 and 1. |                number                |    No    |   All    |        Yes        |
|  variant   |                       Type of button.                        |    `determinate`，`indeterminate`    |    No    |   All    |        Yes        |

**ListItem**：列表渲染组件，接收所有 [View](https://reactnative.dev/docs/view#props) 的props.

|                          Name                           |                         Description                          |      Type       | Required | Platform | HarmonyOS Support |
| :-----------------------------------------------------: | :----------------------------------------------------------: | :-------------: | :------: | :------: | :---------------: |
|                        Component                        |             Replace element with custom element.             | React Component |    No    |   All    |        Yes        |
|                      ViewComponent                      |                Container for linear gradient.                | React Component |    No    |   All    |        Yes        |
|                      bottomDivider                      |         Add divider at the bottom of the list item.          |     boolean     |    No    |   All    |        Yes        |
|                        children                         |                    Add enclosed children.                    |       any       |    No    |   All    |        Yes        |
|                     containerStyle                      |              Additional main container styling.              |   View Style    |    No    |   All    |        Yes        |
|                      disabledStyle                      |   Specific styling to be used when list item is disabled.    |   View Style    |    No    |   All    |        Yes        |
| Specific styling to be used when list item is disabled. |             Props for linear gradient component.             |       any       |    No    |   All    |        Yes        |
|                           pad                           | Adds spacing between the leftComponent, the title component & right component. |     number      |    No    |   All    |        Yes        |
|                       topDivider                        |           Add divider at the top of the list item.           |     boolean     |    No    |   All    |        Yes        |

**ListItem.Accordion**：列表渲染折叠组件，接收所有 [ListItem](https://reactnativeelements.com/docs/components/listitem#props) 的props.

|    Name    |                         Description                          |              Type              | Required | Platform | HarmonyOS Support |
| :--------: | :----------------------------------------------------------: | :----------------------------: | :------: | :------: | :---------------: |
| animation  |              Decide whether to show animation.               | Animated.TimingAnimationConfig |    No    |   All    |        Yes        |
|  content   |                 Similar to ListItem's child.                 |           ReactNode            |    No    |   All    |        Yes        |
| expandIcon | Icon when Accordion is expanded, if not provided `icon` will be rotated 180deg. |            IconNode            |    No    |   All    |        Yes        |
|    icon    |                    Add enclosed children.                    |            IconNode            |    No    |   All    |        Yes        |
| isExpanded |               Decide if Accordion is Expanded.               |            boolean             |    No    |   All    |        Yes        |
| leftRotate |                    Rotate Icon left side                     |            boolean             |    No    |   All    |        Yes        |
|   noIcon   |                  Don't show accordion icon.                  |            boolean             |    No    |   All    |        Yes        |
| noRotation |           Don't rotate when Accordion is expanded.           |            boolean             |    No    |   All    |        Yes        |

**ListItem.ButtonGroup**：列表渲染按钮组组件，接收所有 [ButtonGroup](https://reactnativeelements.com/docs/components/buttongroup#props) 的props.

|      Name      |                    Description                    |             Type             | Required | Platform | HarmonyOS Support |
| :------------: | :-----------------------------------------------: | :--------------------------: | :------: | :------: | :---------------: |
|  onLongPress   |    Called when a long-tap gesture is detected.    | GestureResponderEventHandler |    No    |   All    |        Yes        |
|   onPressIn    | Called when a touch is engaged before `onPress`.  | GestureResponderEventHandler |    No    |   All    |        Yes        |
|   onPressOut   | Called when a touch is released before `onPress`. | GestureResponderEventHandler |    No    |   All    |        Yes        |

**ListItem.CheckBox**：列表渲染选择框组件，接收所有 [CheckBox](https://reactnativeelements.com/docs/components/checkbox#props) 的props.

**ListItem.Chevron**：列表渲染字体图标组件，接收所有 [Icon](https://reactnativeelements.com/docs/components/icon#props) 的props.

|      Name      |                    Description                    |             Type             | Required | Platform | HarmonyOS Support |
| :------------: | :-----------------------------------------------: | :--------------------------: | :------: | :------: | :---------------: |
|  onLongPress   |   Called when a single tap gesture is detected.   | GestureResponderEventHandler |    No    |   All    |        Yes        |
|    onPress     |   Called when a single tap gesture is detected.   | GestureResponderEventHandler |    No    |   All    |        Yes        |
|   onPressIn    | Called when a touch is engaged before `onPress`.  | GestureResponderEventHandler |    No    |   All    |        Yes        |
|   onPressOut   | Called when a touch is released before `onPress`. | GestureResponderEventHandler |    No    |   All    |        Yes        |

**ListItem.Content**：列表渲染内容组件，接收所有 [Text](https://reactnativeelements.com/docs/components/text#props) 的props.

| Name  |          Description          |  Type   | Required | Platform | HarmonyOS Support |
| :---: | :---------------------------: | :-----: | :------: | :------: | :---------------: |
| right | Start content from the right. | boolean |    No    |   All    |        Yes        |

**ListItem.Input**：列表渲染表单组件，接收所有 [Input](https://reactnativeelements.com/docs/components/input#props) 的props.

**ListItem.Subtitle**：列表渲染字幕组件，接收所有 [Text](https://reactnative.dev/docs/text#props) 的props.

| Name  |          Description          |  Type   | Required | Platform | HarmonyOS Support |
| :---: | :---------------------------: | :-----: | :------: | :------: | :---------------: |
| right | Start content from the right. | boolean |    No    |   All    |        Yes        |

**ListItem.Swipeable**：列表渲染滑动框组件，接收所有 [ListItem](https://reactnativeelements.com/docs/components/listitem#props) 的props.

|     Name      |                 Description                 |                  Type                   | Required | Platform | HarmonyOS Support |
| :-----------: | :-----------------------------------------: | :-------------------------------------: | :------: | :------: | :---------------: |
|   animation   |      Decide whether to show animation.      |     Animated.TimingAnimationConfig      |    No    |   All    |        Yes        |
|  leftContent  |                Left Content.                | ReactNode or resetCallback => ReactNode |    No    |   All    |        Yes        |
|   leftStyle   |          Style of left container.           |               View Style                |    No    |   All    |        Yes        |
|   leftWidth   |       Width of swipe left container.        |                 number                  |    No    |   All    |        Yes        |
| onSwipeBegin  |    Handler for swipe in either direction    | `(direction: left`,`right) => unknown`  |    No    |   All    |        Yes        |
|  onSwipeEnd   |           Handler for swipe end.            |              () => unknown              |    No    |   All    |        Yes        |
| rightContent  |               Right Content.                | ReactNode or resetCallback => ReactNode |    No    |   All    |        Yes        |
|  rightStyle   |          Style of right container.          |               View Style                |    No    |   All    |        Yes        |
|  rightWidth   |       Width of swipe right container.       |                 number                  |    No    |   All    |        Yes        |

**ListItem.Title**：列表渲染标题组件，接收所有 [View](https://reactnative.dev/docs/view#props) 的props

| Name  |   Description    |  Type   | Required | Platform | HarmonyOS Support |
| :---: | :--------------: | :-----: | :------: | :------: | :---------------: |
| right | Add right title. | boolean |    No    |    No    |        No         |

**Overlay**：弹窗组件，接收所有 [Text](https://reactnativeelements.com/docs/components/text#props) 的props

|      Name       |                         Description                          |             Type             | Required | Platform | HarmonyOS Support |
| :-------------: | :----------------------------------------------------------: | :--------------------------: | :------: | :------: | :---------------: |
| ModalComponent  | Override React Native `Modal` component (usable for web-platform). |       typeof Component       |    No    |   All    |        Yes        |
|  backdropStyle  |               Style of the backdrop container.               |          iew Style           |    No    |   All    |        Yes        |
|   fullScreen    | If set to true, the modal will take up the entire screen width and height. |           boolean            |    No    |   All    |        Yes        |
|    isVisible    |               If true, the overlay is visible.               |           boolean            |    No    |   All    |        Yes        |
| onBackdropPress | Handler for backdrop press (only works when `fullscreen` is false). |           Function           |    No    |   All    |        Yes        |
|   onLongPress   |         Called when a long-tap gesture is detected.          | GestureResponderEventHandler |    No    |   All    |        Yes        |
|    onPressIn    |       Called when a touch is engaged before `onPress`.       | GestureResponderEventHandler |    No    |   All    |        Yes        |
|   onPressOut    |      Called when a touch is released before `onPress`.       | GestureResponderEventHandler |    No    |   All    |        Yes        |
|  overlayStyle   |                 Style of the actual overlay.                 |          View Style          |    No    |   All    |        Yes        |

**PricingCard**：价格卡组件

|      Name      |                Description                 |                Type                | Required | Platform | HarmonyOS Support |
| :------------: | :----------------------------------------: | :--------------------------------: | :------: | :------: | :---------------: |
|     button     |            Button information.             | `ButtonProps`，`ButtonInformation` |    No    |   All    |        Yes        |
|     color      |      Color scheme for button & title.      |               string               |    No    |   All    |        Yes        |
| containerStyle |          Outer component styling.          |             View Style             |    No    |   All    |        Yes        |
|      info      |            Pricing information.            |              string[]              |    No    |   All    |        Yes        |
|   infoStyle    |     Specify pricing information style.     |             Text Style             |    No    |   All    |        Yes        |
| onButtonPress  | Function to be run when button is pressed. |              Function              |    No    |   All    |        Yes        |
|     price      |    Price mentioned in the pricing card.    |         `string`，`number`         |    No    |   All    |        Yes        |
|  pricingStyle  |                 Text Style                 |    Specify pricing text style.     |    No    |   All    |        Yes        |
|     title      |       Add title in the pricing card.       |               string               |    No    |   All    |        Yes        |
|   titleStyle   |         Specify title text style.          |             Text Style             |    No    |   All    |        Yes        |
|  wrapperStyle  |      Inner wrapper component styling.      |             View Style             |    No    |   All    |        Yes        |

**Ratings**：评分组件

|         Name          |                         Description                          |         Type          | Required | Platform | HarmonyOS Support |
| :-------------------: | :----------------------------------------------------------: | :-------------------: | :------: | :------: | :---------------: |
|       fractions       | The number of decimal places for the rating value; must be between 0 and 20 |        anyany         |    No    |    No    |        No         |
|       imageSize       |          The size of each rating imageDefault is 50          |        number         |    No    |    No    |        No         |
|       jumpValue       |    he number to jump per swipeDefault is 0 (not to jump)     |        number         |    No    |    No    |        No         |
|       minValue        |      The minimum value the user can selectDefault is 0       |        number         |    No    |    No    |        No         |
|    onFinishRating     | Callback method when the user finishes rating. Gives you the final rating value as a whole number |       Function        |    No    |    No    |        No         |
|     onStartRating     |         Callback method when the user starts rating.         |       Function        |    No    |    No    |        No         |
|     onSwipeRating     |          Callback method when the user is swiping.           | (number: any) => void |    No    |    No    |        No         |
| ratingBackgroundColor | Pass in a custom background-fill-color for the rating icon; use this along with type='custom' prop aboveDefault is 'white' |        string         |    No    |    No    |        No         |
|      ratingColor      | Pass in a custom fill-color for the rating icon; use this along with type='custom' prop aboveDefault is '#f1c40f' |        string         |    No    |    No    |        No         |
|      ratingCount      |        Number of rating images to displayDefault is 5        |        number         |    No    |    No    |        No         |
|      ratingImage      | Pass in a custom image source; use this along with type='custom' prop above |       ReactNode       |    No    |    No    |        No         |
|    ratingTextColor    |                Color used for the text labels                |        string         |    No    |    No    |        No         |
|       readonly        | Whether the rating can be modiefied by the userDefault is false |        boolean        |    No    |    No    |        No         |
|      showRating       | Displays the Built-in Rating UI to show the rating value in real-timeDefault is false |        boolean        |    No    |    No    |        No         |
|   showReadOnlyText    |        Whether the text is read onlyDefault is false         |        boolean        |    No    |    No    |        No         |
|     startingValue     |     The initial rating to renderDefault is ratingCount/2     |        number         |    No    |    No    |        No         |
|         style         | Exposes style prop to add additonal styling to the container view |      View Style       |    No    |    No    |        No         |
|       tintColor       |                Color used for the background                 |        string         |    No    |    No    |        No         |
|         type          |     Graphic used for represent a ratingDefault is 'star'     |        string         |    No    |    No    |        No         |

**SearchBar**：搜索框组件，接收所有 [Input](https://reactnativeelements.com/docs/components/input#props) 的 props

|          Name           |              Description               |            Type             | Required | Platform | HarmonyOS Support |
| :---------------------: | :------------------------------------: | :-------------------------: | :------: | :------: | :---------------: |
|    cancelButtonProps    |    Properties of the Cancel button     |         Text Style          |    No    |    No    |        No         |
|    cancelButtonTitle    |       Title of the Cancel button       |           string            |    No    |    No    |        No         |
|       cancelIcon        |       Icon of the Cancel button        |          IconNode           |    No    |    No    |        No         |
|        clearIcon        |               Clear Icon               |          IconNode           |    No    |   All    |        Yes        |
|     containerStyle      |          Style for container           |         View Style          |    No    |   All    |        Yes        |
|   inputContainerStyle   |       Style for input container        |         View Style          |    No    |   All    |        Yes        |
|       inputStyle        |              Input Style               |         Text Style          |    No    |   All    |        Yes        |
| leftIconContainerStyle  |       Left Icon Container Style        |         View Style          |    No    |   All    |        Yes        |
|       lightTheme        |              light Theme               |           boolean           |    No    |    No    |        No         |
|      loadingProps       |         ActivityIndicatorProps         |   ActivityIndicatorProps    |    No    |   All    |        Yes        |
|        onCancel         | Callback Function on cancel icon press |        `(() => any)`        |    No    |    No    |        No         |
|         onClear         | Callback Function on clear icon press  |          Function           |    No    |   All    |        Yes        |
|        platform         |           Platform judgment            | `default`，`android`，`ios` |    No    |    No    |        No         |
| rightIconContainerStyle |       Right Icon Container Style       |   rightIconContainerStyle   |    No    |   All    |        Yes        |
|          round          |         Whether it is rounded          |           boolean           |    No    |   All    |        Yes        |
|       searchIcon        |            Icon for search             |          IconNode           |    No    |   All    |        Yes        |
|       showCancel        |              Show cancel               |           boolean           |    No    |    No    |        No         |
|       showLoading       |              Show loading              |           boolean           |    No    |   All    |        Yes        |

**Slider**：滑动条组件

|         Name          |                         Description                          |                       Type                       | Required | Platform | HarmonyOS Support |
| :-------------------: | :----------------------------------------------------------: | :----------------------------------------------: | :------: | :------: | :---------------: |
|    allowTouchTrack    | If true, thumb will respond and jump to any touch along the track. |                     boolean                      |    No    |   All    |        Yes        |
|  animateTransitions   | Set to true if you want to use the default 'spring' animation. |                     boolean                      |    No    |   All    |        Yes        |
|    animationConfig    | Used to configure the animation parameters. These are the same parameters in the [Animated library](https://reactnative.dev/docs/animations.html). | `TimingAnimationConfig`，`SpringAnimationConfig` |    No    |   All    |        Yes        |
|     animationType     | Set to 'spring' or 'timing' to use one of those two types of animations with the default [animation properties](https://reactnative.dev/docs/animations.html). |                `spring`，`timing`                |    No    |   All    |        Yes        |
|    containerStyle     |         Apply style to the container of the slider.          |                      Style                       |    No    |   All    |        Yes        |
|    debugTouchArea     | Set this to true to visually see the thumb touch rect in green. |                     boolean                      |    No    |   All    |        Yes        |
|       disabled        |      If true the user won't be able to move the slider.      |                     boolean                      |    No    |   All    |        Yes        |
| maximumTrackTintColor |   The color used for the track to the right of the button.   |                      string                      |    No    |   All    |        Yes        |
|     maximumValue      |             Initial maximum value of the slider.             |                      number                      |    No    |   All    |        Yes        |
| minimumTrackTintColor |   The color used for the track to the left of the button.    |                      string                      |    No    |   All    |        Yes        |
|     minimumValue      |             Initial minimum value of the slider.             |                      number                      |    No    |   All    |        Yes        |
|   onSlidingComplete   | Callback called when the user finishes changing the value (e.g. when the slider is released). |             (value: number) => void              |    No    |   All    |        Yes        |
|    onSlidingStart     | Callback called when the user starts changing the value (e.g. when the slider is pressed). |             (value: number) => void              |    No    |   All    |        Yes        |
|     onValueChange     | Callback continuously called while the user is dragging the slider. |             (value: number) => void              |    No    |   All    |        Yes        |
|      orientation      |              Set the orientation of the slider.              |             `vertical`,`horizontal`              |    No    |   All    |        Yes        |
|         step          | Step value of the slider. The value should be between 0 and maximumValue - minimumValue). |                      number                      |    No    |   All    |        Yes        |
|         style         |          The style applied to the slider container.          |                    View Style                    |    No    |   All    |        Yes        |
|      thumbProps       | The props applied to the thumb. Uses `Component` prop which can accept `Animated` components. |                       any                        |    No    |   All    |        Yes        |
|      thumbStyle       |               The style applied to the thumb.                |                    View Style                    |    No    |   All    |        Yes        |
|    thumbTintColor     |                The color used for the thumb.                 |                      string                      |    No    |   All    |        Yes        |
|    thumbTouchSize     | The size of the touch area that allows moving the thumb. The touch area has the same center as the visible thumb. This allows to have a visually small thumb while still allowing the user to move it easily. |                     Sizable                      |    No    |   All    |        Yes        |
|      trackStyle       |               The style applied to the track.                |                    View Style                    |    No    |   All    |        Yes        |
|         value         |                 Initial value of the slider.                 |                      number                      |    No    |   All    |        Yes        |

**Skeleton**：骨架屏组件，接收所有 [View](https://reactnative.dev/docs/view#props) 的props

|          Name           |            Description             |           Type            | Required | Platform | HarmonyOS Support |
| :---------------------: | :--------------------------------: | :-----------------------: | :------: | :------: | :---------------: |
| LinearGradientComponent |  Custom Linear Gradient Component  |      React Component      |    No    |   All    |        Yes        |
|        animation        |         Type of animation          | `none`|`wave`|`pulse` | No | No |    No    |
|         circle          |       show circular variant        |          boolean          |    No    |   All    |        Yes        |
|         height          |      Height of Skeleton View       |    `string`，`number`     |    No    |   All    |        Yes        |
|      skeletonStyle      | Custom style for skeleton gradient |        View Style         |    No    |   All    |        Yes        |
|          width          |       Width of Skeleton View       |     `string`,`number`     |    No    |   All    |        Yes        |

**SocialIcon**：社交字体图标组件

|          Name          |                         Description                          |             Type             | Required | Platform | HarmonyOS Support |
| :--------------------: | :----------------------------------------------------------: | :--------------------------: | :------: | :------: | :---------------: |
|       Component        |                       Type of button.                        |       React Component        |    No    |   All    |        Yes        |
| activityIndicatorStyle |            Style to render when in loading state.            |          View Style          |    No    |   All    |        Yes        |
|         button         |              Creates button with a social icon.              |           boolean            |    No    |   All    |        Yes        |
|        disabled        |                Disables the button, if true.                 |           boolean            |    No    |   All    |        Yes        |
|       fontFamily       |                Specify different font family.                |            string            |    No    |    No    |        No         |
|       fontStyle        |                    Specify text styling.                     |          Text Style          |    No    |   All    |        Yes        |
|       fontWeight       | Specify font weight of title if set as a button with a title. |            string            |    No    |    No    |        No         |
|       iconColor        |                Specify the color of the icon.                |            string            |    No    |   All    |        Yes        |
|        iconSize        |                Specify the size of the icon.                 |            number            |    No    |   All    |        Yes        |
|       iconStyle        |              Extra styling for icon component.               |          View Style          |    No    |    No    |        No         |
|        iconType        | Type of icon set. [Supported sets here](https://reactnativeelements.com/docs/components/icon#available-icon-sets). |            string            |    No    |   All    |        Yes        |
|         light          | Reverses icon color scheme, setting background to white and icon to primary color. |           boolean            |    No    |    No    |        No         |
|        loading         |                   Shows loading indicator.                   |           boolean            |    No    |   All    |        Yes        |
|      onLongPress       |         Called when a long-tap gesture is detected.          | GestureResponderEventHandler |    No    |   All    |        Yes        |
|        onPress         |        Called when a single tap gesture is detected.         | GestureResponderEventHandler |    No    |   All    |        Yes        |
|       onPressIn        |       Called when a touch is engaged before `onPress`.       | GestureResponderEventHandler |    No    |   All    |        Yes        |
|       onPressOut       |      Called when a touch is released before `onPress`.       | GestureResponderEventHandler |    No    |   All    |        Yes        |
|         raised         |      Raised adds a drop shadow, set to false to remove.      |           boolean            |    No    |    No    |        No         |
|         small          |         Decides the size of the activity indicator.          |            string            |    No    |    No    |        No         |
|         style          |                 Adds styling to the button.                  |          View Style          |    No    |   All    |        Yes        |
|         title          |                 Title if made into a button.                 |            string            |    No    |   All    |        Yes        |
|          type          |                      Social media type.                      |       SocialMediaType        |    No    |   All    |        Yes        |
|     underlayColor      |                     Add Underlay color.                      |            string            |    No    |    No    |        No         |

**SpeedDial**：浮动快速操作按钮组件，接收所有 [Button](https://reactnativeelements.com/docs/components/button#props), [FAB](https://reactnativeelements.com/docs/components/fab#props)  的props

|          Name          |                       Description                        |       Type       | Required | Platform | HarmonyOS Support |
| :--------------------: | :------------------------------------------------------: | :--------------: | :------: | :------: | :---------------: |
| backdropPressableProps |               Props for Backdrop Pressable               |  PressableProps  |    No    |    No    |        No         |
|        children        |              SpeedDial Action as children.               | SpeedDial.Action |    No    |   All    |        Yes        |
|         isOpen         |                 Opens the action stack.                  |     boolean      |    No    |   All    |        Yes        |
|     labelPressable     |          onPress on Label Press for all Actions          |     boolean      |    No    |   All    |        Yes        |
|        onClose         | Callback fired when the component requests to be closed. |     Function     |    No    |   All    |        Yes        |
|         onOpen         |  Callback fired when the component requests to be open.  |     Function     |    No    |   All    |        Yes        |
|        openIcon        |       Icon shown on FAB when action stack is open.       |     IconNode     |    No    |   All    |        Yes        |
|      overlayColor      |           Add overlay color to the speed dial.           |      string      |    No    |   All    |        Yes        |
|   transitionDuration   |    The duration for the transition, in milliseconds.     |      number      |    No    |   All    |        Yes        |

**SpeedDial.Action**：浮动快速操作子按钮组件，接收所有 [FAB](https://reactnativeelements.com/docs/components/fab#props) 的props

|      Name      |      Description       |  Type   | Required | Platform | HarmonyOS Support |
| :------------: | :--------------------: | :-----: | :------: | :------: | :---------------: |
| labelPressable | onPress on Label Press | boolean |    No    |   All    |        Yes        |

**Switch**：滑动开关组件，接收所有 [View](https://reactnative.dev/docs/view#props) 的props

| Name  |            Description             |  Type  | Required | Platform | HarmonyOS Support |
| :---: | :--------------------------------: | :----: | :------: | :------: | :---------------: |
| color | The color of the Switch component. | string |    No    |   All    |        Yes        |

**Tab**：导航栏组件，接收所有 [View](https://reactnative.dev/docs/view#props) 的props

|       Name       |               Description                |                     Type                      | Required | Platform | HarmonyOS Support |
| :--------------: | :--------------------------------------: | :-------------------------------------------: | :------: | :------: | :---------------: |
|   buttonStyle    |         Additional button style          | `ViewStyle or (active: boolean) => ViewStyle` |    No    |   All    |        Yes        |
|  containerStyle  | Additional Styling for button container. | `ViewStyle or (active: boolean) => ViewStyle` |    No    |    No    |        No         |
|      dense       |              Dense Tab Item              |                    boolean                    |    No    |    No    |        No         |
| disableIndicator |       Disable the indicator below.       |                    boolean                    |    No    |   All    |        Yes        |
|   iconPosition   |              Icon Position               |       `left`，`right`，`top`，`bottom`        |    No    |   All    |        Yes        |
|  indicatorStyle  |  Additional styling for tab indicator.   |                  View Style                   |    No    |   All    |        Yes        |
|     onChange     |        On Index Change Callback.         |            (value: number) => void            |    No    |   All    |        Yes        |
|    scrollable    |           Makes Tab Scrolling            |                    boolean                    |    No    |    No    |        No         |
|    titleStyle    |      Additional button title style       | `ViewStyle or (active: boolean) => ViewStyle` |    No    |    No    |        No         |
|      value       |       Child position index value.        |                    number                     |    No    |   All    |        Yes        |
|     variant      |      Define the background Variant.      |             `primary`，`default`              |    No    |   All    |        Yes        |

**Tab.Item**：导航栏子组件，接收所有 [Button](https://reactnativeelements.com/docs/components/button#props) 的props

|        Name        |                   Description                    |                     Type                      | Required | Platform | HarmonyOS Support |
| :----------------: | :----------------------------------------------: | :-------------------------------------------: | :------: | :------: | :---------------: |
|       active       |      Allows to define if TabItem is active.      |                    boolean                    |    No    |    No    |        No         |
|    buttonStyle     |             Additional button style              | `ViewStyle or (active: boolean) => ViewStyle` |    No    |   All    |        Yes        |
|   containerStyle   |     Additional Styling for button container.     | `ViewStyle or (active: boolean) => ViewStyle` |    No    |   All    |        Yes        |
|       dense        |                  Dense Tab Item                  |                    boolean                    |    No    |    No    |        No         |
| iconContainerStyle | Additional Styling for Icon Component container. | `ViewStyle or (active: boolean) => ViewStyle` |    No    |   All    |        Yes        |
|     titleStyle     |          Additional button title style           | `ViewStyle or (active: boolean) => ViewStyle` |    No    |   All    |        Yes        |
|      variant       |          Define the background Variant.          |             `primary`，`default`              |    No    |    No    |        No         |

**TabView**：滑动开关内容组件

|         Name          |                         Description                          |          Type          | Required | Platform | HarmonyOS Support |
| :-------------------: | :----------------------------------------------------------: | :--------------------: | :------: | :------: | :---------------: |
|    animationConfig    |             Define the animation configurations.             |    AnimationConfig     |    No    |   All    |        Yes        |
|     animationType     | Choose the animation type among `spring` and `timing`. This is visible when there is tab change. |   `spring`，`timing`   |    No    |   All    |        Yes        |
|    containerStyle     |               Styling for Component container.               |       View Style       |    No    |   All    |        Yes        |
|     disableSwipe      |                    Swipe disabled or not                     |        Boolean         |    No    |   All    |        Yes        |
|   disableTransition   |                     Disables transition                      |        Boolean         |    No    |   All    |        Yes        |
|     minSwipeRatio     |      Minimum distance to swipe before the view changes.      |         number         |    No    |   All    |        Yes        |
|     minSwipeSpeed     |       Minimum speed to swipe before the view changes.        |         number         |    No    |   All    |        Yes        |
|       onChange        |                  On Index Change Callback.                   | (value: number) => any |    No    |   All    |        Yes        |
|     onSwipeStart      |            Handler when the user swipes the view.            |  (direction) => void   |    No    |   All    |        Yes        |
| tabItemContainerStyle |        Styling for TabView.Item Component container.         |       View Style       |    No    |   All    |        Yes        |
|         value         |                 Child position index value.                  |         number         |    No    |   All    |        Yes        |

**TabView.Item**：滑动开关内容子组件，接受所有 [View](https://reactnative.dev/docs/view#props) 的 props

**Text**：文本内容组件组件

|  Name   |           Description            |    Type    | Required | Platform | HarmonyOS Support |
| :-----: | :------------------------------: | :--------: | :------: | :------: | :---------------: |
|   h1    |     Text with Font size 40.      |  boolean   |    No    |   All    |        Yes        |
| h1Style |     Styling when h1 is set.      | Text Style |    No    |   All    |        Yes        |
|   h2    |     Text with Font size 34.      |  boolean   |    No    |   All    |        Yes        |
| h2Style |     Styling when h2 is set.      | Text Style |    No    |   All    |        Yes        |
|   h3    |     Text with Font size 28.      |  boolean   |    No    |   All    |        Yes        |
| h3Style |     Styling when h3 is set.      | Text Style |    No    |   All    |        Yes        |
|   h4    |     Text with Font size 22.      |  boolean   |    No    |   All    |        Yes        |
| h4Style |     Styling when h4 is set.      | Text Style |    No    |   All    |        Yes        |
|  style  | Add additional styling for Text. | Text Style |    No    |   All    |        Yes        |

**Tile**：卡片图块组件

|         Name          |                         Description                          |              Type              | Required | Platform | HarmonyOS Support |
| :-------------------: | :----------------------------------------------------------: | :----------------------------: | :------: | :------: | :---------------: |
|    ImageComponent     |               Custom ImageComponent for Tile.                |        typeof Component        |    No    |   All    |        Yes        |
|     activeOpacity     |          Number passed to control opacity on press.          |             number             |    No    |    No    |        No         |
|        caption        |         Text inside the tilt when tile is featured.          |           ReactNode            |    No    |   All    |        Yes        |
|     captionStyle      | Styling for the caption (optional); You only use this if `caption` is a string. |           Text Style           |    No    |   All    |        Yes        |
|    containerStyle     |            Styling for the outer tile container.             |           View Style           |    No    |   All    |        Yes        |
| contentContainerStyle |     Styling for bottom container when not featured tile.     |           View Style           |    No    |   All    |        Yes        |
|       featured        |                Changes the look of the tile.                 |            boolean             |    No    |   All    |        Yes        |
|        height         |                     Height for the tile.                     |             number             |    No    |   All    |        Yes        |
|         icon          |                    Icon Component Props.                     |           IconObject           |    No    |   All    |        Yes        |
|  iconContainerStyle   |            Styling for the outer icon container.             |           View Style           |    No    |   All    |        Yes        |
|  imageContainerStyle  |                    Styling for the image.                    |           View Style           |    No    |   All    |        Yes        |
|      imageProps       | Optional properties to pass to the image if provided e.g "resizeMode". |       ImageProps(Object)       |    No    |   All    |        Yes        |
|       imageSrc        |                    Source for the image.                     | `string`,`ImageSourcePropType` |    No    |   All    |        Yes        |
| overlayContainerStyle | Styling for the overlay container when using featured tile.  |           View Style           |    No    |    No    |        No         |
|         title         |                    Text inside the tile.                     |             string             |    No    |   All    |        Yes        |
|  titleNumberOfLines   |                  Number of lines for Title.                  |             number             |    No    |   All    |        Yes        |
|      titleStyle       |                    Styling for the title.                    |           Text Style           |    No    |   All    |        Yes        |
|         width         |                     Width for the tile.                      |             number             |    No    |   All    |        Yes        |

**Tooltip**：文本提示组件

|           Name           |                         Description                          |                           Type                           | Required | Platform | HarmonyOS Support |
| :----------------------: | :----------------------------------------------------------: | :------------------------------------------------------: | :------: | :------: | :---------------: |
|      ModalComponent      | Override React Native `Modal` component (usable for web-platform). |                     typeof Component                     |    No    |   All    |        Yes        |
|      animationType       |                        Animation Type                        |                      `none`,`fade`                       |    No    |   All    |        Yes        |
|     backgroundColor      |       Sets backgroundColor of the tooltip and pointer.       |                        ColorValue                        |    No    |   All    |        Yes        |
| closeOnlyOnBackdropPress | Flag to determine whether to disable auto hiding of tooltip when touching/scrolling anywhere inside the active tooltip popover container. When `true`, Tooltip closes only when overlay backdrop is pressed (or) highlighted tooltip button is pressed. |                         boolean                          |    No    |    No    |        No         |
|      containerStyle      |           Passes style object to tooltip container           |                        View Style                        |    No    |   All    |        Yes        |
|          height          | Tooltip container height. Necessary in order to render the container in the correct place. Pass height according to the size of the content rendered inside the container. |                          number                          |    No    |   All    |        Yes        |
|      highlightColor      |   Color to highlight the item the tooltip is surrounding.    |                        ColorValue                        |    No    |   All    |        Yes        |
|         onClose          |      Function which gets called on closing the tooltip.      |                         Function                         |    No    |   All    |        Yes        |
|          onOpen          |      Function which gets called on opening the tooltip.      |                         Function                         |    No    |   All    |        Yes        |
|       overlayColor       |        Color of overlay shadow when tooltip is open.         |                        ColorValue                        |    No    |   All    |        Yes        |
|       pointerColor       | Color of tooltip pointer, it defaults to the [`backgroundColor`](https://reactnativeelements.com/docs/components/tooltip#backgroundcolor) if none is passed. |                        ColorValue                        |    No    |   All    |        Yes        |
|       pointerStyle       |             Style to be applied on the pointer.              |                        View Style                        |    No    |   All    |        Yes        |
|         popover          |      Component to be rendered as the display container.      | `ReactElement<{}, string`，`JSXElementConstructor<any>>` |    No    |   All    |        Yes        |
|   skipAndroidStatusBar   | Force skip StatusBar height when calculating element position. Pass `true` if Tooltip used inside react-native Modal component. |                         boolean                          |    No    |   All    |        Yes        |
|       toggleAction       | Define type of action that should trigger tooltip. Available options *onPress*, *onLongPress* |                          string                          |    No    |   All    |        Yes        |
|      toggleOnPress       |   Flag to determine to toggle or not the tooltip on press.   |                         boolean                          |    No    |   All    |        Yes        |
|         visible          |                     To show the tooltip.                     |                         boolean                          |    No    |   All    |        Yes        |
|          width           | Tooltip container width. Necessary in order to render the container in the correct place. |                          number                          |    No    |   All    |        Yes        |
|       withOverlay        | Flag to determine whether or not display overlay shadow when tooltip is open. |                         boolean                          |    No    |   All    |        Yes        |
|       withPointer        |   Flag to determine whether or not to display the pointer.   |                         boolean                          |    No    |   All    |        Yes        |

## 遗留问题
## 其他
-  Rating组件的readonly、onFinishRating等属性无法生效，与Android/iOS一致：[issue#1](https://github.com/react-native-elements/react-native-elements/issues/3736)、[issue#2](https://github.com/react-native-elements/react-native-elements/issues/3718)。
-  AirbnbRatings组件的startImage属性无法生效，与Android/iOS一致：[issue#3](https://github.com/react-native-elements/react-native-elements/issues/3718)。
-  ButtonGroups组件的activeOpacity、button等属性无法生效，与Android/iOS一致：[issue#4](https://github.com/react-native-elements/react-native-elements/issues/3938)。
-  Dialog组件的onLongPress、onpressIn等属性无法生效，与Android/iOS一致：[issue#5](https://github.com/react-native-elements/react-native-elements/issues/3931)。
-  Header组件的barStyle、elevated等属性无法生效，与Android、iOS一致：[issue#6](https://github.com/react-native-elements/react-native-elements/issues/3935)。
-  Input组件的renderErrorMessage属性无法生效，与Android、iOS一致：[issue#7](https://github.com/react-native-elements/react-native-elements/issues/3933)。
-  ListItem.Swipeable组件的minSlideWidth属性无法生效，与Android、iOS一致：[issue#8](https://github.com/react-native-elements/react-native-elements/issues/3825)。
-  ListItem.Title组件的right属性无法生效，与Android、iOS一致：[issue#9](https://github.com/react-native-elements/react-native-elements/issues/3934)。
-  SearchBar组件的cancelButtonProps、showCancel等属性无法生效，与Android、iOS一致：[issue#10](https://github.com/react-native-elements/react-native-elements/issues/3939)。
-  SocialIcon组件的fontFamily、fontWeight等属性无法生效，与Android、iOS一致：[issue#11](https://github.com/react-native-elements/react-native-elements/issues/3940)。
-  SpeedDial组件的backdropPressableProps属性无法生效，与Android、iOS一致：[issue#12](https://github.com/react-native-elements/react-native-elements/issues/3937)。
-  Tab组件的containerStyle、dense等属性无法生效，与Android、iOS一致：[issue#13](https://github.com/react-native-elements/react-native-elements/issues/3941)。
-  Tab.Item组件的active、dense等属性无法生效，与Android、iOS一致：[issue#14](https://github.com/react-native-elements/react-native-elements/issues/3936)。
-  Tile组件的activeOpacity等属性无法生效，与Android、iOS一致：[issue#15](https://github.com/react-native-elements/react-native-elements/issues/3932)。
-  Tooltip组件的closeOnlyOnBackdropPress属性无法生效，与Android、iOS一致：[issue#16](https://github.com/react-native-elements/react-native-elements/issues/3811)。

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/react-native-elements/react-native-elements/blob/next/LICENSE)，请自由地享受和参与开源。