> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>NativeBase</code> </h1>
</p>
<p align="center">
   <a href="https://github.com/GeekyAnts/NativeBase">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/GeekyAnts/NativeBase/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/NativeBase)

## Installation and Usage

Find the matching version information in the release address of a third-party library: [@react-native-oh-tpl/native-base Releases](https://github.com/react-native-oh-library/NativeBase/releases).For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction：

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/native-base
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/native-base
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

```tsx
// NativeBaseProvider is a component that makes the theme available throughout your app. It uses React's Context API. Add NativeBaseProvider to the root of your app and update App.js as follows:s
import React from "react";
import { SafeAreaView, View } from "react-native";
import { NativeBaseProvider } from "native-base";

function App() {
  return (
    <NativeBaseProvider>
      <View style={{ backgroundColor: "white" }}>
        <SafeAreaView></SafeAreaView>
      </View>
    </NativeBaseProvider>
  );
}
export default App;
```

```tsx
import { StyleSheet, View } from "react-native";
import { Text } from "native-base";

export function TextTest() {
  return (
    <View style={styles.container}>
      <Text fontSize="xs">xs</Text>
      <Text fontSize="sm">sm</Text>
      <Text fontSize="md">md</Text>
      <Text fontSize="lg">lg</Text>
      <Text fontSize="xl">xl</Text>
      <Text fontSize="2xl">2xl</Text>
      <Text fontSize="3xl">3xl</Text>
      <Text fontSize="4xl">4xl</Text>
      <Text fontSize="5xl">5xl</Text>
      <Text fontSize="6xl">6xl</Text>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    justifyContent: "center",
    alignItems: "center",
    padding: 10,
    margin: 25,
    borderRadius: 5,
    borderWidth: 3,
  },
});
```

## Link

The HarmonyOS implementation of this library depends on the native code from @react-native-oh-tpl/react-native-reanimated、@react-native-oh-tpl/react-native-gesture-handler. If this library is included into your HarmonyOS application, there is no need to include it again; you can skip the steps in this section and use it directly.

If it is not included, follow the guide provided in [@react-native-oh-tpl/react-native-gesture-handler docs](/zh-cn/react-native-gesture-handler.md#link)、[@react-native-oh-tpl/react-native-reanimated docs](/zh-cn/react-native-reanimated.md#link)、[@react-native-oh-library/react-native-safe-area-context docs](/zh-cn/react-native-safe-area-context.md#link)、[@react-native-oh-tpl/react-native-svg docs](/zh-cn/react-native-svg.md#link)、[@react-native-oh-tpl/react-navigation-drawer docs](/zh-cn/react-navigation-drawer.md#link)、[@react-native-oh-tpl/react-native-tab-view docs](/zh-cn/react-native-tab-view.md#link)、[@react-native-oh-tpl/react-native-pager-view docs](/zh-cn/react-native-pager-view.md#link)、[@react-native-oh-tpl/react-native-swipe-list-view docs](/zh-cn/react-native-swipe-list-view.md) to add it to your project.

## Constraints

### Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/react-native-oh-tpl-native-base Releases](https://github.com/react-native-oh-library/NativeBase/releases)

## Components

For details about component usage, see. [NativeBase](https://docs.nativebase.io)

The following component attributes are currently supported:

> [!TIP] The Platform column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of HarmonyOS Support is yes, it means that the HarmonyOS platform supports this property; no means the opposite; partially means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

**AspectRatio**: AspectRatio controls the size of the undefined dimension of a node or child component. You can refer mozilla.org for more details.
| Name | Description | Type | Required | Platform | HarmonyOS Support |
| :------------------: | :----------------------------------------------------------: | :-------------------: | :------: | :------: | :---------------: |
| ratio | The aspect ratio of the container. Some examples are `16/9`, `16/10`, `9/16`, `4/3` | Object | No | All | Yes |

**Box**: This is a generic component for low level layout needs. It is similar to a div in HTML.
| Name | Description | Type | Required | Platform | HarmonyOS Support |
| :------------------: | :----------------------------------------------------------: | :-------------------: | :------: | :------: | :---------------: |
| children | Renders components as Box children. Accepts a JSX.Element or an array of JSX.Element.  | React.element | No | All | Yes |
| \_text | For providing props to Text inside Box | Any | No | All | Yes |
| bg | Abbreviation Setting Background | String | No | All | Yes |
| background | Various background-related settings can be accepted, such as color, image, gradient, etc. | String | No | All | Yes |
| bgColor | Explicitly used to set the background color | String | No | All | Yes |
| backgroundColor | Similar to bgColor, it is used to set the background color. | String | No | All | Yes |

**Center**: Center aligns its contents to the center within itself. It is a layout component.
[Center implements View](https://reactnative.dev/docs/view#props)

**Container**: The Container restricts a content's width according to current breakpoint, while keeping the size fluid.
[The container implements the functions of the box. Therefore, all attributes of the box can be transferred to the container.]

**Flex**: Flex provides helpful style shorthand and is a Box with display: flex.
| Name | Description | Type | Required | Platform | HarmonyOS Support |
| :------------------: | :----------------------------------------------------------: | :-------------------: | :------: | :------: | :---------------: |
| direction | Project positioning direction. Values can be column,column-reverse,row,row-reverse | String | No | All | Yes |
| wrap | Wrapping mode of child elements nowrap,wrap,wrap-reverse | String | No | All | Yes |
| align | Alignment mode of the child element on the cross axis. This parameter is optional baseline,normal,stretch | String | No | All | Yes |
| justify | Alignment mode of the child element on the main axis. This parameter is optional left,normal,right | String | No | All | Yes |
| basis | This parameter is optional-moz-fit-content,-moz-max-content,-moz-min-content,-webkit-auto,auto,content,fit-content,max-content,min-contents | String | No | All | Yes |
| grow | This parameter is optional Globals ,(number & {}) , (string & {}) | Number | No | All | Yes |
| shrink | This parameter is optional Globals , (number & {}) , (string & {}); | Number | No | All | Yes |

**HStack / Row**: HStack aligns items horizontally. Row is also an alias for HStack.
| Name | Description | Type | Required | Platform | HarmonyOS Support |
| :------------------: | :----------------------------------------------------------: | :-------------------: | :------: | :------: | :---------------: |
| direction | The direction of the Stack Items. This parameter is optional row,column,column-reverse,row-reverse | String | No | All | Yes |

**Stack**: Stack aligns items vertically or horizontally based on the direction prop.
| Name | Description | Type | Required | Platform | HarmonyOS Support |
| :------------------: | :----------------------------------------------------------: | :-------------------: | :------: | :------: | :---------------: |
| divider | The divider element to use between elements. | ReactElement | No | All | Yes |
| space | The space between each stack item. Accepts Responsive values. This parameter is optional sm,2xs,xs,md,xl,lg,2xl,gutter,SpaceType | ReactElement | No | All | Yes |
| reversed | Determines whether to reverse the direction of Stack Items. | Boolean | No | All | Yes |
| direction | The direction of the Stack Items,This parameter is optional row，column，column-reverse，row-reverse | String | No | All | Yes |
| isHovered | If true, the Stack will be in hovered state | Boolean | No | Web | No |
| isFocused | If true, the Stack will be focused | Boolean | No | No | No |
| isDisabled | If true, the Stack will be disabled. | Boolean | No | No | No |
| isInvalid | If true, the Stack will be invalid. | Boolean | No | No | No |
| isReadOnly | If true, prevents the value of the children from being edited. Used with FormControls. | Boolean | No | No | No |

**VStack / Column**: VStack aligns items vertically. Column is also an alias for VStack.
| Name | Description | Type | Required | Platform | HarmonyOS Support |
| :------------------: | :----------------------------------------------------------: | :-------------------: | :------: | :------: | :---------------: |
| direction |The direction of the VStack / Column This parameter is optional row,column,column-reverse,row-reverse | String | No | All | Yes |

**ZStack**: ZStack aligns items to the z-axis.
| Name | Description | Type | Required | Platform | HarmonyOS Support |
| :------------------: | :----------------------------------------------------------: | :-------------------: | :------: | :------: | :---------------: |
| reversed |Determines whether to reverse the direction of ZStack Items. | Boolean | No | All | Yes |

**Button**: The Button component triggers an event or an action. Examples can be submitting forms and deleting a data point.
| Name | Description | Type | Required | Platform | HarmonyOS Support |
| :------------------: | :----------------------------------------------------------: | :-------------------: | :------: | :------: | :---------------: |
| variant | The variant of the button style to use.This parameter is optional link，subtle，solid，ghost，outline，unstyled | String | No | All | Yes |
| colorScheme | The color of the radio when it's checked. This should be one of the color keys in the theme (e.g."green", "red"). | String | No | All | Yes |
| size | The size of the button.This parameter is optional s）、md、lg | String | No | All | Yes |
| isLoading | If true, the button will show a spinner. | Boolean | No | All | Yes |
| isHovered | If true, the button will be in hovered state. | Boolean | No | Web | No |
| isPressed | If true, the button will be in pressed state. | Boolean | No | All | Yes |
| isFocused | If true, the button will be focused. | Boolean | No | All | Yes |
| isFocusVisible | If true, the button focus ring will be visible. | Boolean | No | No | No |
| startIcon | The start icon element to use in the button. | React.element | No | All | Yes |
| endIcon | The end icon element to use in the button. | React.element | No | All | Yes |
| isLoadingText | Loading text | String | No | All | Yes |
| spinner | The spinner element to use when isLoading is set to true. | JSX.Element | No | All | Yes |
| isDisabled | If true, the button will be disabled. | Boolean | No | All | Yes |
| \_text | Props to style the child text | Object | No | All | Yes |
| \_stack |  Props to be passed to the HStack used inside of Button. HStack | Object | No | All | Yes |
| \_icon | Props to be passed to the Icon used inside of Button. | Object | No | All | Yes |
| spinnerPlacement | Prop to decide placement of spinner.This parameter is optional start，end | String | No | All | Yes |
| \_loading | Props to be passed to the button when isLoading is true. | Object | No | All | Yes |
| \_isDisabled | Props to be passed to the button when button is disabled. | Object | No | All | Yes |
| \_spinner | Props to be passed to the spinner when isLoading is true. | Object | No | All | Yes |
| \_hover | Props to be passed to the button when button is hovered. | Object | No | Web | No |
| \_pressed | Props to be passed to the button when button is pressed. | Object | No | All | Yes |
| \_focus | Props to be passed to the button when button is focused. | Object | No | All | Yes |
| rightIcon | The right icon element to use in the button. | React.element | No | All | Yes |
| leftIcon | The left icon element to use in the button. | React.element | No | All | Yes |
| direction | The direction of the Stack Items.This parameter is optional row,column | String | No | All | Yes |
| children | Renders components as Button children. Accepts a JSX.Element or an array of JSX.Element. | React.element | No | All | Yes |
| isAttached | If true, button will be atttached together. | Boolean | No | All | Yes |

**Pressable**: Pressable is a lower level primitive if you need more flexibility than a button and access to hover, pressed and focus events.
| Name | Description | Type | Required | Platform | HarmonyOS Support |
| :------------------: | :----------------------------------------------------------: | :-------------------: | :------: | :------: | :---------------: |
| onHoverIn | Called when a mouse enters the Pressable | () => void | No | Web | No |
| onHoverOut | Called when a mouse leaves the Pressable | () => void | No | Web | No |
| onFocus | Called when Pressable receives focus | () => void | No | No | No |
| onBlur | Called when Pressable loses focus | () => void | No | No | No |
| \_hover | Style props to be applied when hovered | Object | No | Web | No |
| \_pressed | Style props to be applied when pressed | Object | No | All | Yes |
| \_focus | Style props to be applied when focus | Object | No | All | Yes |
| \_disabled | Style props to be applied when disabled | Object | No | All | Yes |
| isDisabled | If true, the Pressable will be disabled. | Boolean | No | All | Yes |
| isHovered | If true, the Pressable will be hovered. | Boolean | No | Web | No |
| isPressed | If true, the Pressable will be pressed. | Boolean | No | All | Yes |
| isFocused | If true, the Pressable will be focused. | Boolean | No | No | No |
| isFocusVisible | If true, the focus ring will be visible . | Boolean | No | All | Yes |
| \_focusVisible | Style props to be applied when focus visible. These styles will be only applied when user is interacting the app using a keyboard. (Web only) | Object | No | Web | No |
| children | Renders components as Pressable children. Accepts a JSX.Element or an array of JSX.Element. | React.element | No | All | Yes |

**CheckBox**: The Checkbox component allows a user to select multiple values from various options in a form.
| Name | Description | Type | Required | Platform | HarmonyOS Support |
| :------------------: | :----------------------------------------------------------: | :-------------------: | :------: | :------: | :---------------: |
| id | assign id to checkbox | String | No | All | Yes |
| name | The name of the input field in a checkbox. | String | No | All | Yes |
| value | The value to be used in the checkbox input. This is the value that will be returned on form submission | String | No | All | Yes |
| defaultValue | The initial value of the checkbox group. | String | No | All | Yes |
| colorScheme | The color of the radio when it's checked. This should be one of the color keys in the theme (e.g."green", "red"). | String | No | All | Yes |
| size | The size (width and height) of the checkbox. | String | No | All | Yes |
| onChange | Function called when the state of the checkbox changes. | () => void | No | All | Yes |
| \_checkbox | Pass props will be passed to each checkbox. | Object | No | All | Yes |

**FormControl**: FormControl is used to form elements by providing context such as isInvalid, isDisabled, and isRequired.
| Name | Description | Type | Required | Platform | HarmonyOS Support |
| :------------------: | :----------------------------------------------------------: | :-------------------: | :------: | :------: | :---------------: |
| nativeID | If provided, this prop is passed to its children. | String | No | All | Yes |
| isInvalid | If true, the p will be invalid. | Boolean | No | All | Yes |
| isRequired | If true, the p will be required. | Boolean | No | All | Yes |
| isDisabled | If true, the p will be disabled. | Boolean | No | No | No |
| isReadOnly | If true, the p will be readOnly. | Boolean | No | All | Yes |
| \_disabled | Passed props will be applied on disabled state. | Object | No | All | Yes |
| htmlFor | Reflects the value of the 'for' content property. | String | No | Web | No |
| \_astrick | Props applied to astrick text | Object | No | Web | No |
| rightIcon | The right icon element to use in the FormControl.ErrorMessage. | React.element | No | All | Yes |
| leftIcon | The left icon element to use in the FormControl.ErrorMessage. | React.element | No | All | Yes |
| startIcon | The start icon element to use in the FormControl.ErrorMessage. | React.element | No | All | Yes |
| endIcon | The end icon element to use in the FormControl.ErrorMessage. | React.element | No | All | Yes |
| \_stack | Props to be passed to the HStack used inside of FormControl.ErrorMessage. FormControl.ErrorMessage 内部使用的 HStack 的参数 | Object | No | All | Yes |
| \_invalid | Passed props will be applied on invalid state. | Object | No | All | Yes |

**IconButton**: IconButton consists of the Button component. It is generally used to make an Icon pressable.
| Name | Description | Type | Required | Platform | HarmonyOS Support |
| :------------------: | :----------------------------------------------------------: | :-------------------: | :------: | :------: | :---------------: |
| colorScheme | The color of the radio when it's checked. This should be one of the color keys in the theme (e.g."green", "red"). | String | No | All | Yes |
| variant | The variant of the button style to use. | String | No | All | Yes |
| size | The size of the button. | String | No | All | Yes |
| isDisabled | If true, the button will be disabled. | Boolean | No | All | Yes |
| icon | The icon to be used. Refer to the Icon section of the docs for the available icon options. | React.element | No | All | Yes |
| \_icon | Props to be passed to the icon used inside of IconButton. IconButton 内部使用的图标的参数 | Object | No | All | Yes |
| \_hover |  Style props to be applied when hovered | Object | No | Web | No |
| \_pressed |  Style props to be applied when pressed | Object | No | All | Yes |
| \_focus |  Style props to be applied when focus | Object | No | All | Yes |

**Input**: The Input component allows a user to provide input in a text field.
| Name | Description | Type | Required | Platform | HarmonyOS Support |
| :------------------: | :----------------------------------------------------------: | :-------------------: | :------: | :------: | :---------------: |
| isInvalid | If true, the p will be invalid. | Boolean | No | All | Yes |
| variant |The variant of the Input style to use.This parameter is optional outline，filled，underlined，unstyled，rounded | String | No | All | Yes |
| isDisabled | If true, the button will be disabled. | Boolean | No | All | Yes |
| isHovered | If true, the Input will be hovered. | Boolean | No | Web | No |
| isFocused | If true, the Input will be focused. | Boolean | No | All | Yes |
| size | The size of the button.This parameter is optional sm、md、lg | String | No | All | Yes |
| isRequired | If true, the Input will be required. | Boolean | No | No | No |
| isReadOnly | If true, the Input will be readOnly. | Boolean | No | All | Yes |
| InputLeftElement | If given, adds the provided element to the left of the input. | React.element | No | All | Yes |
| leftElement | If given, adds the provided element to the left of the input. | React.element | No | All | Yes |
| InputRightElement | If given, adds the provided element to the right of the input. | React.element | No | All | Yes |
| rightElement | If given, adds the provided element to the right of the input. | React.element | No | All | Yes |
| type | Using the type password, user can mask the input. This parameter is optional text，password | String | No | All | Yes |
| isFullWidth | If true, the input element will span the full width of its parent | Boolean | No | No | No |
| wrapperRef | Ref to be passed to Icon's wrapper Box | Any | No | No | No |
| \_hover | Passed props will be applied on hovered state. | Object | No | Web | NO |
| \_focus | Passed props will be applied on focused state. | Object | No | All | Yes |
| \_disabled | Passed props will be applied on disabled state. | Object | No | All | Yes |
| \_readOnly | Passed props will be applied on readOnly state. | Object | No | All | Yes |
| \_invalid | assed props will be applied on invalid state. | Object | No | All | Yes |
| \_input | props are passed to InputBase component | Object | No | All | Yes |
| \_stack | Props to be passed to the Stack used inside. | Object | No | All | Yes |
| focusOutlineColor | This prop allows you to change outlineColor when input is in the focused state | String | No | All | Yes |
| invalidOutlineColor | This prop allows you to change outlineColor when input is in invalid state | String | No | All | Yes |
| ref | Obtain node data | Any | No | All | Yes |

**TextArea**: The Textarea component helps create multi-line text inputs.
| Name | Description | Type | Required | Platform | HarmonyOS Support |
| :------------------: | :----------------------------------------------------------: | :-------------------: | :------: | :------: | :---------------: |
| isInvalid | If true, the p will be invalid. | Boolean | No | All | Yes |
| variant | The variant of the Input style to use.This parameter is optional outline，filled，underlined，unstyled，rounded | String | No | All | Yes |
| isDisabled | If true, the button will be disabled. | Boolean | No | All | Yes |
| isHovered | If true, the Input will be hovered. | Boolean | No | Web | No |
| isFocused | If true, the Input will be focused. | Boolean | No | All | Yes |
| size |The size of the button.This parameter is optional sm、md、lg | String | No | All | Yes |
| isRequired | If true, the Input will be required. | Boolean | No | No | No |
| isReadOnly | If true, the Input will be readOnly. | Boolean | No | All | Yes |
| InputLeftElement | If given, adds the provided element to the left of the input. | React.element | No | All | Yes |
| leftElement | If given, adds the provided element to the left of the input. | React.element | No | All | Yes |
| InputRightElement | If given, adds the provided element to the right of the input. | React.element | No | All | Yes |
| rightElement | If given, adds the provided element to the right of the input. | React.element | No | All | Yes |
| type |  Using the type password, user can mask the input.This parameter is optional text，password | String | No | All | Yes |
| isFullWidth | If true, the input element will span the full width of its parent | Boolean | No | No | No |
| wrapperRef | Ref to be passed to Icon's wrapper Box | Any | No | All | Yes |
| \_hover | Passed props will be applied on hovered state. | Object | No | Web | NO |
| \_focus | Passed props will be applied on focused state. | Object | No | All | Yes |
| \_disabled | Passed props will be applied on disabled state. | Object | No | All | Yes |
| \_readOnly | Passed props will be applied on readOnly state. | Object | No | All | Yes |
| \_invalid | Passed props will be applied on invalid state. | Object | No | All | Yes |
| \_stack | Props to be passed to the Stack used inside. | Object | No | All | Yes |
| focusOutlineColor | This prop allows you to change outlineColor when input is in the focused state | Boolean | No | All | Yes |
| invalidOutlineColor | This prop allows you to change outlineColor when input is in invalid state | Boolean | No | All | Yes |
| placeholder | The string that will be rendered before text input has been entered | String | No | All | Yes |

**Link**: Links are accessible elements used primarily for navigation. This component is styled to resemble a hyperlink.
| Name | Description | Type | Required | Platform | HarmonyOS Support |
| :------------------: | :----------------------------------------------------------: | :-------------------: | :------: | :------: | :---------------: |
| href | URL that should be opened on Link press | String | No | All | Yes |
| size | Size of the link.This parameter is optional 2xl，xl，lg，md，sm，xsm | String | No | All | Yes |
| isUnderlined | Whether Link text should be underlined | Boolean | No | All | Yes |
| isHovered | Whether Link text should be hovered | Boolean | No | Web | No |
| onPress | Callback that will be invoked on Link press | () => void | No | All | Yes |
| isExternal | If true, link will be opened in new tab on web. It uses _target property to achieve this| String | No | Web | No |
| \_hover | Hover props. Accepts all styled system props. | Object | No | Web | No |
| wrapperRef | Ref to be attached to the Link wrapper | Any | No | All | Yes |

**Radio**: Radio limits the selection from a series of options to only one.
| Name | Description | Type | Required | Platform | HarmonyOS Support |
| :------------------: | :----------------------------------------------------------: | :-------------------: | :------: | :------: | :---------------: |
| value | The value to be used in the radio input. This is the value that will be returned on form submission | String | No | All | Yes |
| colorScheme | The color of the radio. This should be one of the color keys in the theme (e.g."green", "red"). | String | No | All | Yes |
| isDisabled | If true, the radio will be disabled | Boolean | No | All | Yes |
| isHovered | If true, the radio will be hovered | Boolean | No | Web | No |
| isPressed | If true, the radio will be pressed | Boolean | No | All | Yes |
| isFocused | If true, the radio will be focused | Boolean | No | All | Yes |
| isInvalid | If true, the radio is marked as invalid. Changes style of unchecked state. | Boolean | No | All | Yes |
| onChange | The callback fired when any children radio is checked or unchecked. | () => void | No | All | Yes |
| isFocusVisible | If true, the radio focus ring will be visible | Boolean | No | No | No |
| size | The size (width and height) of the radio. lg，md，sm | String | No | All | Yes |
| icon | If given, will use this icon instead of the default. | React.element | No | All | Yes |
| wrapperRef | Ref to be passed to Icon's wrapper Box | Any | No | All | Yes |
| \_stack | Props to be passed to the Stack used inside. | Object | No | All | Yes |
| \_disabled | Passed props wilICheckboxGroupProps will be applied on the disabled state. | Object | No | All | Yes |
| \_checked | Passed props will be applied on checked state. | Object | No | All | Yes |
| \_focus | Passed props will be applied on focus state. | Object | No | All | Yes |
| \_hover | Passed props will be applied on hover state. | Object | No | Web | No |
| \_invalid | Passed props will be applied on invalid state. | Object | No | All | Yes |
| \_pressed | Passed props will be applied on pressed state on native. | Object | No | All | Yes |
| \_icon | Icon related props can be passed in _icon. | Object | No | All | Yes |
| \_readOnly | Passed props will be applied on readonly state. | Object | No | All | Yes |
| \_interactionBox | You can style interaction box around the checkbox using this. | Object | No | All | Yes |
| ref | Obtain node data | Object | No | All | Yes |

**Select**: Select creates a dropdown list of items with the selected item in closed view.
| Name | Description | Type | Required | Platform | HarmonyOS Support |
| :------------------: | :----------------------------------------------------------: | :-------------------: | :------: | :------: | :---------------: |
| placeholder | The placeholder that describes the Select. | String | No | All | Yes |
| color | The Selected Item text color. | String | No | No | Yes |
| placeholderTextColor | The placeholder text color | String | No | iOS | No |
| \_item | Item props passed here will be passed to each Select.Item component. | Object | No | All | Yes |
| \_selectedItem | Item props passed here will be passed to the selected Select.Item component. | Object | No | All | Yes |
| selectedValue | Currently selected value. Useful for controlling the Select state | String | No | All | Yes |
| defaultValue | Default selected value. | String | No | All | Yes |
| onValueChange | Callback to be invoked when Select value is changed | () => void | No | All | Yes |
| isDisabled | Whether Select is disabled | Boolean | No | All | Yes |
| isHovered | Whether Select is hovered | Boolean | No | Web | No |
| isFocused | Whether Select is focused | Boolean | No | All | Yes |
| isFocusVisible | If true, the focus ring of select will be visible. | Boolean | No | No | No |
| dropdownIcon | If given, updates the dropdown Icon | React.element | No | All | Yes |
| dropdownOpenIcon | If given, updates the dropdown Icon when opened | React.element | No | All | Yes |
| dropdownCloseIcon | If given, updates the dropdown Icon when closed | React.element | No | All | Yes |
| variant |The variant of the button style to use.This parameter is optional outline，filled，underlined，unstyled，rounded | String | No | All | Yes |
| onOpen | Callback to be invoked when Select Dropdown or BottomSheet is opened. | () => void | No | All | Yes |
| onClose | Callback to be invoked when Select Dropdown or BottomSheet is closed. | () => void | No | All | Yes |
| \_actionSheet | props to be passed to underlying ActionSheet. Select uses ActionSheet underneath. | Object | No | All | Yes |
| \_actionSheetContent | props to be passed to underlying ActionSheet.Content. Select uses ActionSheet underneath. | Object | No | All | Yes |
| \_actionSheetBody | props to be passed to underlying Flatlist in ActionSheet.Content. Body 的参数 | Object | No | All | Yes |
| wrapperRef | Ref to be attached to the Select wrapper | Any | No | No | No |
| accessibilityLabel | Text read when the user interacts with the element | String | No | No | No |

**Select.Item**: Select.Item
| Name | Description | Type | Required | Platform | HarmonyOS Support |
| :------------------: | :----------------------------------------------------------: | :-------------------: | :------: | :------: | :---------------: |
| label | The label which will be displayed. | String | No | All | Yes |
| value | The value to be used for the item. This is the value that will be returned on form submission. | String | No | All | Yes |

**Switch**: 开关
| Name | Description | Type | Required | Platform | HarmonyOS Support |
| :------------------: | :----------------------------------------------------------: | :-------------------: | :------: | :------: | :---------------: |
| size | The size (width and height) of the switch.This parameter is optional lg，md，sm | String | No | All | Yes |
| isDisabled | If true, set the disabled to the invalid state. | Boolean | No | All | Yes |
| isHovered | If true, set the hovered state. | Boolean | No | Web | No |
| name | The input name of the Switch when used in a form. | String | No | All | Yes |
| onToggle | Function called when the state of the Switch changes. | () => void | No | All | Yes |
| isChecked | If true, set the Switch to the checked state. | Boolean | No | All | Yes |
| defaultIsChecked | If true, the checkbox will be initially checked. | Boolean | No | All | Yes |
| isInvalid | If true, set the switch to the invalid state. | Boolean | No | All | Yes |
| onTrackColor | The track color of the Switch when on. | Object | No | All | Yes |
| offTrackColor | The track color of the Switch when off. | Object | No | All | Yes |
| onThumbColor | The thumb color of the Switch when on. | Object | No | All | Yes |
| offThumbColor | The thumb color of the Switch when off. | Object | No | All | Yes |
| colorScheme | Color scheme to be used for the Switch | String | No | All | Yes |
| \_hover | Props when Switch is hovered. Accepts all the Switch props. | String | No | Web | No |

**Slider**: The Slider allows users to select options from a given range of values.
| Name | Description | Type | Required | Platform | HarmonyOS Support |
| :------------------: | :----------------------------------------------------------: | :-------------------: | :------: | :------: | :---------------: |
| value | The current value of the Slider | Number | No | All | Yes |
| defaultValue | The default value (uncontrolled). | Number | No | All | Yes |
| onChange | Handler that is called when the value changes. | () => void | No | All | Yes |
| colorScheme | Color scheme of the slider | String | No | All | Yes |
| orientation | The orientation of the Slider.This parameter is optional horizontal，vertical' | String | No | All | Yes |
| accessibilityLabel | Text description of slider. This will be announced by screen reader/ | String | No | No | No |
| isReversed | If true, the value will be incremented or decremented in reverse. | Boolean | No | All | Yes |
| isDisabled | Whether the Thumb is disabled | Boolean | No | All | Yes |
| onChangeEnd | Fired when the slider stops moving, due to being let go. | () => void | No | All | Yes |
| minValue | The slider's minimum value. | Number | No | All | Yes |
| maxValue | The slider's maximum value. | Number | No | All | Yes |
| step | The slider's step value. | Number | No | All | Yes |
| isReadOnly | Whether the whole Slider is readonly. | Boolean | No | All | Yes |
| \_disabled | Props applied if isDisabled is true. | Object | No | All | Yes |
| \_readOnly | Props applied if isReadOnly is true. | Object | No | All | Yes |
| sliderTrackHeight | Prop applied to change slider track height | Number | No | All | Yes |
| thumbSize | Prop applied to change size of slider thumb | Number | No | All | Yes |
| \_interactionBox | You can style interaction box around the checkbox using this. | Object | No | All | Yes |

**Badge**: Badges allow the highlighting of an item’s status. This provides quick recognition.
| Name | Description | Type | Required | Platform | HarmonyOS Support |
| :------------------: | :----------------------------------------------------------: | :-------------------: | :------: | :------: | :---------------: |
| variant | The style variant of the badge. | String | No | All | Yes |
| colorScheme | The color scheme to use for the badge. Must be a key in theme.colors.This parameter is optional success，danger，info，coolGray | String | No | All | Yes |
| rightIcon | The right icon element to use in the button. | React.element | No | All | Yes |
| leftIcon | The left icon element to use in the button. | React.element | No | All | Yes |
| startIcon | The start icon element to use in the button. | React.element | No | All | Yes |
| endIcon | The end icon element to use in the button. | React.element | No | All | Yes |
| \_text | Props to style the child text | Object | No | All | Yes |
| \_icon | Props to be passed to the Icon used inside of Button. | Object | No | All | Yes |

**Divider**: Divider can visually separate content in a given list or group.
| Name | Description | Type | Required | Platform | HarmonyOS Support |
| :------------------: | :----------------------------------------------------------: | :-------------------: | :------: | :------: | :---------------: |
| orientation | The orientation of the divider.,This parameter is optional vertical，horizontal | Number | No | All | Yes |
| thickness | The thickness of the divider. | String | No | All | Yes |

**Alert**: Alerts convey a state that can influence a system, feature, or page.
| Name | Description | Type | Required | Platform | HarmonyOS Support |
| :------------------: | :----------------------------------------------------------: | :-------------------: | :------: | :------: | :---------------: |
| status | The status of the alert.This parameter is optional info，warning，success，error | String | No | All | Yes |
| variant | The variant of the alert style to use. | String | No | All | Yes |
| colorScheme | The color scheme of the Alert. | String | No | All | Yes |

**Progress**: Progress helps show the progress status for a time-consuming task that consists of several steps.
| Name | Description | Type | Required | Platform | HarmonyOS Support |
| :------------------: | :----------------------------------------------------------: | :-------------------: | :------: | :------: | :---------------: |
| value | Value of Progress. | Number | No | All | Yes |
| size | Defines height of Progress | String | No | All | Yes |
| colorScheme | The color scheme of the progress. This should be one of the color keys in the theme (e.g."green", "red"). | String | No | All | Yes |
| \_filledTrack | Pseudo prop to give Prop to filled track | Object | No | All | Yes |
| min | Min progress value | Number | No | All | Yes |
| max | Max progress value | Number | No | All | Yes |

**Skeleton**: Skeleton showcases the loading state of a component.
| Name | Description | Type | Required | Platform | HarmonyOS Support |
| :------------------: | :----------------------------------------------------------: | :-------------------: | :------: | :------: | :---------------: |
| fadeDuration | The fadeIn duration in seconds | Number | No | All | Yes |
| isLoaded | If true, it will render its children | Boolean | No | All | Yes |
| speed | The animation speed in seconds | Number | No | All | Yes |
| startColor | The color at the animation start | String | No | All | Yes |
| endColor | The color at the animation end | String | No | All | Yes |
| size | Sizes for Skeleton | String | No | All | Yes |

**Skeleton.Text**: SkeletonText implements View
| Name | Description | Type | Required | Platform | HarmonyOS Support |
| :------------------: | :----------------------------------------------------------: | :-------------------: | :------: | :------: | :---------------: |
| fadeDuration | The fadeIn duration in seconds | Number | No | All | Yes |
| isLoaded | If true, it will render its children | Boolean | No | All | Yes |
| speed | The animation speed in seconds | Number | No | All | Yes |
| startColor | The color at the animation start | String | No | All | Yes |
| endColor | The color at the animation end | String | No | All | Yes |
| lines | Number of Lines in text | Number | No | All | Yes |
| \_line | Stying for each line | String | No | All | Yes |
| \_stack | Props to be passed to the Stack used inside. | String | No | No | No |

**Spinner**: Spinners gives visual cues to actions that are processing or awaiting a course change or results.
| Name | Description | Type | Required | Platform | HarmonyOS Support |
| :------------------: | :----------------------------------------------------------: | :-------------------: | :------: | :------: | :---------------: |
| color | The foreground color of the spinner (default is gray). | String | No | All | Yes |
| size | Size of the indicator. This parameter is optional lg，md，sm | String | No | All | Yes |

**Toast**: Toast displays alerts on top of an overlay.
| Name | Description | Type | Required | Platform | HarmonyOS Support |
| :------------------: | :----------------------------------------------------------: | :-------------------: | :------: | :------: | :---------------: |
| show | Message body | Object | No | All | Yes |
| close | Close individual | (id: any) => void; | No | All | Yes |
| closeAll | Close all | () => void | No | All | Yes |
| isActive | Anti shake design | (id: any) => boolean; | No | All | Yes |

**Toast.show**: 轻提示消息体
| Name | Description | Type | Required | Platform | HarmonyOS Support |
| :------------------: | :----------------------------------------------------------: | :-------------------: | :------: | :------: | :---------------: |
| title | The title to be rendered in the Toast | ReactNode | No | All | Yes |
| description | The description of the toast | ReactNode | No | All | Yes |
| duration | The delay before the toast hides (in milliseconds). If set to `null`, toast will never dismiss. | Number 或 null | No | All | Yes |
| id | The `id` of the toast. Mostly used when you need to prevent duplicate. By default, we generate a unique `id` for each toast | any | No | All | Yes |
| onCloseComplete | Callback function to run side effects after the toast has closed. | () => void | No | All | Yes |
| placement | The placement of the toast. Defaults to bottom.This parameter is optional top，top-right，top-left，bottom，bottom-left，bottom-right | String | No | All | Yes |
| render | Render a component toast component. Any component passed will receive 2 props: `id` and `onClose`. | (props: any) => ReactNode | No | All | Yes |
| \_title | For providing props to Title inside Toast | Object | No | All | Yes |
| \_description | For providing props to Description inside Toast | Object | No | All | Yes |
| accessibilityAnnouncement | The text to be announced by a screen reader when the Toast opens. | String | No | Android | No |
| accessibilityLiveRegion | Determines the [accessibility announcement tone](https://reactnative.dev/docs/accessibility#accessibilityliveregion-android). | String | No | Android | No |
| avoidKeyboard | If true and the keyboard is opened, the Toast will move up equivalent to the keyboard height. | Boolean | No | iOS | No |

**Text**: Text
| Name | Description | Type | Required | Platform | HarmonyOS Support |
| :------------------: | :----------------------------------------------------------: | :-------------------: | :------: | :------: | :---------------: |
| children | Renders components as Text children. Accepts a JSX.Element or an array of JSX.Element. | JSX.Element | No | All | Yes |
| fontSize | The size of font | String | No | All | Yes |
| letterSpacing | Letter spacing | String | No | All | Yes |
| lineHeight | Line height | String | No | All | Yes |
| fontWeight | Font weight | String | No | All | Yes |
| Fonts | Fonts | String | No | No | No |
| noOfLines | Used to truncate text at a specific number of lines | Number | No | All | Yes |
| bold | Used to make the text bold. | Number | No | All | Yes |
| isTruncated | If true, it will render an ellipsis when the text exceeds the width of the viewport or maxWidth set. | Boolean | No | All | Yes |
| italic | Used to make the text italic. | Boolean | No | All | Yes |
| underline | Used to underline the text. | Boolean | No | All | Yes |
| strikeThrough | A horizontal line through the center of the text. | Boolean | No | All | Yes |
| sub | Text will have smaller font size. | Boolean | No | All | Yes |
| highlight | Used to highlight the text with a yellow background. | Boolean | No | All | Yes |

**Heading**: Heading composes Text so one can use all the style props to render headlines.
| Name | Description | Type | Required | Platform | HarmonyOS Support |
| :------------------: | :----------------------------------------------------------: | :-------------------: | :------: | :------: | :---------------: |
| size | Sizes for Heading. This parameter is optional lg，md，sm | String | No | All | Yes |

**AlertDialog**: AlertDialog is used when a user needs to be interrupted with a mandatory confirmation or call-to-action. AlertDialog composes Modal so you can use all its props.
| Name | Description | Type | Required | Platform | HarmonyOS Support |
| :------------------: | :----------------------------------------------------------: | :-------------------: | :------: | :------: | :---------------: |
| isOpen | If true, the AlertDialog will open. Useful for controllable state behaviour | Boolean | No | All | Yes |
| onClose | Callback invoked when the AlertDialog is closed | () => void | No | All | Yes |
| defaultIsOpen | If true, the AlertDialog will be opened by default | Boolean | No | All | Yes |
| size | The size of the AlertDialog | Number | No | All | Yes |
| leastDestructiveRef | The ref of element that is least destructive child of the AlertDialog. | Object | No | No | No |
| initialFocusRef | The ref of element to receive focus when the AlertDialog opens. | Object | No | All | Yes |
| finalFocusRef | The ref of element to receive focus when the AlertDialog closes. | Object | No | All | Yes |
| avoidKeyboard | If true and the keyboard is opened, the AlertDialog will move up equivalent to the keyboard height. | Boolean | No | iOS | Yes |
| closeOnOverlayClick | If true, the AlertDialog will close when the overlay is clicked | Boolean | No | All | Yes |
| isKeyboardDismissable | If true, the AlertDialog will close when Escape key is pressed | Boolean | No | No | No |
| overlayVisible | If true, a backdrop element is visible | Boolean | No | All | Yes |
| backdropVisible | If true, a backdrop element is visible | Boolean | No | All | Yes |
| \_backdrop | Props applied on Overlay. | Any | No | All | Yes |
| \_backdropFade | Props applied on Overlay Animation. | Object | No | All | Yes |
| \_fade | Props applied on Child Fade Animation. | Object | No | All | Yes |
| \_slide | Props applied on Child Slide Animation. | Object | No | All | Yes |
| animationPreset | Sets the animation type | String | No | All | Yes |

**Menu**: Menu generates a dropdown menu along with the menu button design pattern.
| Name | Description | Type | Required | Platform | HarmonyOS Support |
| :------------------: | :----------------------------------------------------------: | :-------------------: | :------: | :------: | :---------------: |
| trigger | Function that returns a React Element. This element will be used as a Trigger for the menu. | () => void | Yes | All | Yes |
| onOpen | This function will be invoked when the menu is opened. | () => void | No | All | Yes |
| onClose | This function will be invoked when menu is closed.  It will also be called when the user attempts to close the menu via Escape key or backdrop press. | () => void | No | All | Yes |
| closeOnSelect | Whether menu should be closed when a menu item is pressed. | Boolean | No | All | Yes |
| defaultIsOpen | If true, the menu will be opened by default. | Boolean | No | All | Yes |
| isOpen | Whether the menu is opened. Useful for controlling the open state. | Boolean | No | All | Yes |
| crossOffset | The additional offset applied along the cross axis between the element and its trigger element. | Number | No | All | Yes |
| offset | The additional offset applied along the main axis between the element and its trigger element. | Number | No | All | Yes |
| shouldOverlapWithTrigger | Determines whether menu content should overlap with the trigger. | boolean | No | All | Yes |
| placement | menu placement.This parameter is optional top,bottom,left,right | String | No | All | Yes |
| \_overlay | Overlay related props can be passed in _overlay. | Object | No | All | Yes |
| \_presenceTransition | PresenceTransition related props can be passed in _presenceTransition. | Object | No | All | Yes |
| \_backdrop | Backdrop related props can be passed in _backdrop. | Object | No | All | Yes |
| shouldFlip | Whether the element should flip its orientation (e.g. top to bottom or left to right) when there is insufficient room for it to render completely. | Boolean | No | All | Yes |

**Menu.Item**: Menu.Item
| Name | Description | Type | Required | Platform | HarmonyOS Support |
| :------------------: | :----------------------------------------------------------: | :-------------------: | :------: | :------: | :---------------: |
| children | Children of Menu Item. | JSX.Element | No | All | Yes |
| isDisabled | Whether menu item is disabled. | Boolean | No | All | Yes |
| \_text | Props to be passed to Text. | Object | No | All | Yes |
| textValue | This value will be available for the typeahead menu feature. | String | No | All | Yes |

**Menu.Option**: Menu.Option
| Name | Description | Type | Required | Platform | HarmonyOS Support |
| :------------------: | :----------------------------------------------------------: | :-------------------: | :------: | :------: | :---------------: |
| value | Value of the Menu Item option. | String | No | All | Yes |
| \_stack | Stack related props can be passed in _stack. | Object | No | All | Yes |
| \_icon | Icon related props can be passed in _icon. | Object | No | All | Yes |
| \_text | Text related props can be passed in _text. | Object | No | All | Yes |

**Menu.MenuGroup**: Menu.MenuGroup
| Name | Description | Type | Required | Platform | HarmonyOS Support |
| :------------------: | :----------------------------------------------------------: | :-------------------: | :------: | :------: | :---------------: |
| title | The title of the menu group. | String | No | All | Yes |
| children | The children of the Menu group. | JSX.Element | No | All | Yes |
| \_title | Props to pass on to Text. | Object | No | All | Yes |

**Menu.MenuOptionGroup**: Menu.MenuOptionGroup
| Name | Description | Type | Required | Platform | HarmonyOS Support |
| :------------------: | :----------------------------------------------------------: | :-------------------: | :------: | :------: | :---------------: |
| type | Used to add selection type of menu group. | String | No | All | Yes |
| defaultValue | The initial value of the option group. | String | No | All | Yes |
| value | The value of the option group. | String | No | All | Yes |
| onChange | Function called when selection changes. | () => void | No | All | Yes |

**Modal**: A Modal is an overlay on the primary window or another dialog window. Content behind the modal dialog remains inert and users cannot interact with it.
| Name | Description | Type | Required | Platform | HarmonyOS Support |
| :------------------: | :----------------------------------------------------------: | :-------------------: | :------: | :------: | :---------------: |
| isOpen | If true, the modal will open. Useful for controllable state behavior. | Boolean | No | All | Yes |
| onClose | Callback invoked when the modal is closed. | () => void | No | All | Yes |
| defaultIsOpen | If true, the modal will be opened by default. | Boolean | No | All | Yes |
| size | The size of the modal. | String | No | All | Yes |
| initialFocusRef | The ref of element to receive focus when the modal opens. | Any | No | All | Yes |
| finalFocusRef | The ref of element to receive focus when the modal closes. | Any | No | All | Yes |
| avoidKeyboard | If true and the keyboard is opened, the modal will move up equivalent to the keyboard height. | Boolean | No | iOS | Yes |
| isKeyboardDismissable | If true, the modal will close when Escape key is pressed. | Boolean | No | All | Yes |
| overlayVisible | If true, a backdrop element is visible. | Boolean | No | All | Yes |
| backdropVisible | If true, a backdrop element is visible. | Boolean | No | All | Yes |
| animationPreset | Sets the animation type. | String | No | All | Yes |
| \_backdrop | Props applied on Overlay Animation. | Object | No | All | Yes |
| \_fade | Props applied on Child Fade Animation. | Object | No | All | Yes |
| \_slide | Props applied on Child Slide Animation. | Object | No | All | Yes |
| \_overlay | Props to be passed to the Overlay used inside of Modal. | Object | No | All | Yes |
| useRNModal | If true, renders react-native native modal | Boolean | No | All | Yes |
| \_backdropFade | Props applied on Overlay Animation. | Object | No | All | Yes |
| closeOnOverlayClick | If true, the modal will close when the overlay is clicked. | () => void | No | All | Yes |

**Popover**: Popover floats around a trigger. It is a non-modal dialog used to provide contextual information to the user. It should be paired with a pressable trigger element.
| Name | Description | Type | Required | Platform | HarmonyOS Support |
| :------------------: | :----------------------------------------------------------: | :-------------------: | :------: | :------: | :---------------: |
| isOpen | Whether the popover is opened. Useful for controlling the open state. | Boolean | No | All | Yes |
| onClose | This function will be invoked when popover is closed. It'll also be called when user attempts to close the popover via Escape key or backdrop press. | () => void | No | All | Yes |
| onOpen | This function will be invoked when popover is opened. | () => void | No | All | Yes |
| placement | Popover placement | String | No | All | Yes |
| defaultIsOpen | If true, the popover will be opened by default. | Boolean | No | All | Yes |
| initialFocusRef | The ref of element to receive focus when the popover opens. | Any | No | All | Yes |
| finalFocusRef | The ref of element to receive focus when the modal closes. | Any | No | All | Yes |
| isKeyboardDismissable | If true, the modal will close when Escape key is pressed. | Boolean | No | All | Yes |
| useRNModal | If true, renders react-native native modal | Boolean | No | All | Yes |
| trigger | Function that returns a React Element. This element will be used as a Trigger for the popover. | () => void | No | All | Yes |
| trapFocus | Whether popover should trap focus. | Boolean | No | No | No |
| crossOffset | The additional offset applied along the cross axis between the element and its trigger element. | Number | No | All | Yes |
| offset | The additional offset applied along the main axis between the element and its trigger element. | Number | No | All | Yes |
| shouldOverlapWithTrigger | Determines whether menu content should overlap with the trigger. | boolean | No | All | Yes |
| children | Popover children. | JSX.Element | No | All | Yes |
| shouldFlip | Whether the element should flip its orientation (e.g. top to bottom or left to right) when there is insufficient room for it to render completely. | Boolean | No | All | Yes |

**Avatar**: The Avatar component can display profile pictures, initials, or a fallback image to represent a user.
| Name | Description | Type | Required | Platform | HarmonyOS Support |
| :------------------: | :----------------------------------------------------------: | :-------------------: | :------: | :------: | :---------------: |
| source | The image source of the avatar. | Object | No | All | Yes |
| size | The size of the avatar. | String | No | All | Yes |
| \_image | For providing props to Image component inside the Avatar. | Object | No | All | Yes |
| wrapperRef | ref to be attached to the Avatar wrapper. | Any | No | All | Yes |

**Icon**: Icon
| Name | Description | Type | Required | Platform | HarmonyOS Support |
| :------------------: | :----------------------------------------------------------: | :-------------------: | :------: | :------: | :---------------: |
| as | Use <a href='https://github.com/expo/vector-icons'>@expo/vector-icons</a> | Any | No | All | Yes |
| size | The size of the icon. | String | No | All | Yes |
| color | The color of the icon. | String | No | All | Yes |
| name | name | String | No | All | Yes |
| viewBox | The viewBox of the icon. | String | No | All | Yes |
| path | icon path | JSX.Element[] | No | All | Yes |
| d | SVG path of the icon | String | No | All | Yes |

**Image**: The Image component allows one to display images.
| Name | Description | Type | Required | Platform | HarmonyOS Support |
| :------------------: | :----------------------------------------------------------: | :-------------------: | :------: | :------: | :---------------: |
| source | specify a source for image. | Object | No | All | Yes |
| alt | The alt text that describes the image. This will be added as accessibilityLabel in android/iOS and alt on web.   | String | No | All | Yes |
| \_alt | In the event of an error loading the src, specify a fallback source. | Object | No | All | Yes |
| size | The size of the Image. | String | No | All | Yes |
| src | specify a source for image. | String | No | All | Yes |
| fallbackSource | In the event of an error loading the src, specify a fallback source. | String | No | All | Yes |
| ignoreFallback | Opt out of the fallbackSource logic and show alternative text. | Boolean | No | All | Yes |
| fallbackElement | In the event of an error loading the src, specify a fallback JSX Element. | JSX.Element | No | All | Yes |

**ActionSheet**: 操作表
| Name | Description | Type | Required | Platform | HarmonyOS Support |
| :------------------: | :----------------------------------------------------------: | :-------------------: | :------: | :------: | :---------------: |
| isOpen | If true, the ActionSheet will open. Useful for controllable state behavior. | Boolean | No | All | Yes |
| onClose | Callback invoked when the modal is closed. | () => void | No | All | Yes |
| disableOverlay | If true, disables the overlay. | Boolean | No | All | Yes |
| hideDragIndicator | If true, hides the drag indicator. | Boolean | No | All | Yes |
| \_backdrop | Props applied on Overlay. | any | No | All | Yes |
| useRNModal | If true, renders react-native native modal | Boolean | No | All | Yes |

**Actionsheet.Content**: 操作表内容
| Name | Description | Type | Required | Platform | HarmonyOS Support |
| :------------------: | :----------------------------------------------------------: | :-------------------: | :------: | :------: | :---------------: |
| \_dragIndicatorWrapperOffSet | Props applied on area above actionsheet content. | Object | No | All | Yes |
| \_dragIndicatorWrapper | Props applied on area around drag indicator. | Object | No | All | Yes |
| \_dragIndicator | Props applied on drag indicator. | Object | No | All | Yes |

**PresenceTransition**: PresenceTransition provides a declarative API to add entry and exit transitions.
| Name | Description | Type | Required | Platform | HarmonyOS Support |
| :------------------: | :----------------------------------------------------------: | :-------------------: | :------: | :------: | :---------------: |
| onTransitionComplete | Callback invoked when the transition is completed. | () => void | No | All | Yes |
| initial | Styles before the transition starts. | Object | No | All | Yes |
| animate | Entry animation styles. | Object | No | All | Yes |
| exit | Exit animation styles. | Boolean | No | All | Yes |
| visible | Determines whether to start the animation. | Boolean | No | All | Yes |
| children | PresenceTransition children. | any | No | All | Yes |
| as | Accepts a Component to be rendered as Wrapper. Defaults to `View`. | any | No | All | Yes |

**Stagger**: Stagger component provides a declarative API to add staggered transitions.
| Name | Description | Type | Required | Platform | HarmonyOS Support |
| :------------------: | :----------------------------------------------------------: | :-------------------: | :------: | :------: | :---------------: |
| initial | Initial styles before the transition starts | Object | No | All | Yes |
| animate | The styles to which each child should animate to while entering. | Object | No | All | Yes |
| exit | The styles to which each child should animate to while exiting. | Object | No | All | Yes |
| visible | Determines whether to start the animation | Boolean | No | All | Yes |

**Slide**: Slide component provides a declarative API to add sliding transitions.
| Name | Description | Type | Required | Platform | HarmonyOS Support |
| :------------------: | :----------------------------------------------------------: | :-------------------: | :------: | :------: | :---------------: |
| in | Show or hidden | Boolean | No | All | Yes |
| duration | Slide duration  | Number | No | All | Yes |
| placement | Slide placement | String | No | All | Yes |

**FAB**: A floating action button (FAB) is a circular icon button that hovers over content to execute a primary action in the application.
| Name | Description | Type | Required | Platform | HarmonyOS Support |
| :------------------: | :----------------------------------------------------------: | :-------------------: | :------: | :------: | :---------------: |
| placement | Placement of the Fab. | String | No | All | Yes |
| label | Text to be displayed in Fab. | String | No | All | Yes |
| icon | Icon to be displayed in Fab. | React.Element | No | All | Yes |
| renderInPortal | Determines whether the Fab should be rendered in a Portal. | Boolean | No | All | Yes |

**Hidden**: Hidden is used to toggle the visibility value of child components responsively, based on the colorMode or based on the platform. It does not mount the child components in the restricted values of props.
| Name | Description | Type | Required | Platform | HarmonyOS Support |
| :------------------: | :----------------------------------------------------------: | :-------------------: | :------: | :------: | :---------------: |
| from | The from prop takes breakpoint from which the wrapped component is hidden. | String | No | All | Yes |
| till | The till prop takes breakpoint till which the wrapped component is hidden. | String | No | All | Yes |
| only | The only prop takes array of breakpoints on which the wrapped component is hidden. | String | No | All | Yes |
| colorMode | The colormode takes the mode on which the wrapped component must be hidden. | React.Element | No | No | No |
| platform | The platform takes the platform as string or array for the multiple on which the wrapped component must be hidden. | React.Element | No | All | Yes |
| children | Hidden children. | React.Element | No | All | Yes |
| isSSR | Is the component in the server-side rendering (SSR) environment | Boolean | No | No | No |

**KeyboardAvoidingView**: Provides a view that moves out of the way of virtual keyboard automatically. It solves the common problem of views needing to move out of the way of the virtual keyboard. It can automatically adjust either its height, position, or bottom padding based on the keyboard height.
| Name | Description | Type | Required | Platform | HarmonyOS Support |
| :------------------: | :----------------------------------------------------------: | :-------------------: | :------: | :------: | :---------------: |
| children | KeyboardAvoidingView children. | React.element | No | All | Yes |

**Scrollview**: Scrollview
| Name | Description | Type | Required | Platform | HarmonyOS Support |
| :------------------: | :----------------------------------------------------------: | :-------------------: | :------: | :------: | :---------------: |
| children | Scrollview children. | React.element | No | All | Yes |
| \_contentContainerStyle | Pass props to contentContainerStyle, and this also resolves NB tokens. | Object | No | All | Yes |

**View**: View
| Name | Description | Type | Required | Platform | HarmonyOS Support |
| :------------------: | :----------------------------------------------------------: | :-------------------: | :------: | :------: | :---------------: |
| children | View children. | React.element | No | All | Yes |

**FlatList**: FlatList
| Name | Description | Type | Required | Platform | HarmonyOS Support |
| :------------------: | :----------------------------------------------------------: | :-------------------: | :------: | :------: | :---------------: |
| \_contentContainerStyle | Pass props to contentContainerStyle, and this also resolves NB tokens. | Object | No | All | Yes |
| ref | Obtain node data | Object | No | All | Yes |

**Other and hooks**：包含 hooks 和外用组件
| Name | Description | Required | Platform | HarmonyOS Support |
| ---------------------- | ----------- | -------- | ----------------- | ----------------- |
| useDisclose | useDisclose handles common open, close, or toggle scenarios and can control feedback components such as Modal, AlertDialog, Drawer, etc. | NO | All | YES |
| useBreakpointValue | useBreakpointValue returns the value for the current breakpoint based on the provided responsive values object. It is also responsive to window resizing and returning the appropriate value according to the new window size. | NO | NO | NO |
| SectionList | 导出的是 RN 原生的 SectionList，可直接用 RN 的 SectionList | NO | All | YES |
| useClipboard | useClipboard controls and regulates the copying of content to the clipboard. | NO | All | YES |
| useMediaQuery | useMediaQuery is a custom hook that helps detect matches between a single media query or multiple media queries. React Native does not natively support media queries, so useMediaQuery is still limited. | NO | All | YES |
| useToken | useTheme is a custom hook to call theme object from the context. | NO | All | YES |
| useColorMode |useToken resolves design tokens from the theme. | NO | NO | NO |
| useTheme |useToken resolves design tokens from the theme. | NO | All | YES |
| useColorModeValue | useColorModeValue is a custom hook that can retrieve a value from parameters passed based on active color mode value. | NO | NO | NO |
| useContrastText | useContrastText is a custom hook that provides color contrast text color (either lightText or darkText) against the background color that is passed as a parameter. | NO | All | YES |
| useAccessibleColors | useContrastText is a custom hook that provides color contrast text color (either lightText or darkText) against the background color that is passed as a parameter. | NO | All | YES |
| Todo-List | 用本库的组件写的案例，如有业务需要可自行编写适合的组件 | NO | All | YES |
| AppBar | 用本库的组件写的案例，如有业务需要可自行编写适合的组件 | NO | All | YES |
| Card |用本库的组件写的案例，如有业务需要可自行编写适合的组件| NO | All | YES |
| Drawer Navigation | 快速地使用 [@react-native-oh-tpl/react-navigation-drawer](/zh-cn/react-navigation-drawer.md) | NO | All | YES |
| Tab View | 快速地使用 [@react-native-oh-tpl/react-native-tab-view 文档](/zh-cn/react-native-tab-view.md) in NB | NO | All | YES |
| Swipe List | 快速地使用 [@react-native-oh-tpl/react-native-swipe-list-view](/zh-cn/react-native-swipe-list-view.md) | NO | All | YES |
| Form with Validation | 用本库的组件写的案例，如有业务需要可自行编写适合的组件 | NO | All | YES |
| Login/Signup Forms | 用本库的组件写表单登录的案例，如有业务需要可自行编写适合的组件| NO | All | YES |
| SearchBar | 用本库的组件写的搜索案例，如有业务需要可自行编写适合的组件 | NO | All | YES |
| App drawer | 使用 FlatList 创建类似应用程序抽屉的布局非常常见，如有业务需要可自行编写适合的组件 | NO | All | YES |
| Footer |用本库的组件写的 Footer 案例，如有业务需要可自行编写适合的组件 | NO | All | YES |

## Known Issues

- [ ] FormControl 组件 isDisabled 属性无效: [issue#1](https://github.com/GeekyAnts/NativeBase/issues/5707)
- [ ] Select 组件 placeholderTextColor 属性无效: [issue#16](https://github.com/react-native-oh-library/NativeBase/issues/16)
- [X] Modal,AlertDialog,组件avoidKeyboard属性无效: [issue#17](https://github.com/react-native-oh-library/NativeBase/issues/17)

## Others

- 网站文档图标要用@expo/vector-icons（需要用到 expo 脚手架才可以），如果没有用到 expo 脚手架的可以用[react-native-vector-icons 文档](/zh-cn/react-native-vector-icons.md)平替
- Tooltip 当用户与元素交互时，工具提示会提供简短的信息性消息。工具提示的启动方法包括：通过鼠标悬停手势或键盘悬停手势。这个组件是在 web 端用的

## License

This project is licensed under [The MIT License (MIT)](https://github.com/GeekyAnts/NativeBase/blob/master/LICENSE).
