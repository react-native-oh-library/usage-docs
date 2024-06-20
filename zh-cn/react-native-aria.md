> 模板版本：v0.1.3

<p align="center">
  <h1 align="center"> <code>react-native-aria</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/gluestack/react-native-aria/tree/main">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/gluestack/react-native-aria/blob/main/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!tip] [Github 地址](https://github.com/gluestack/react-native-aria/tree/v0.2.4)

## 安装与使用

React Native ARIA是可增量采用的。每个组件都作为单独的包发布，因此您可以在单个组件中使用它，并随着时间的推移逐渐添加更多组件。所有这些包都在npm上的@react-native-aria范围内发布。

进入到工程目录并输入以下命令：

#### **yarn**

```bash
yarn add @react-native-aria/button@0.2.2
```

<!-- tabs:end -->

#### **npm**

```bash
npm install @react-native-aria/button@0.2.2
```

<!-- tabs:end -->

除了单独的包之外，我们还提供了一个总包，其中包含所有React Native ARIA hooks

#### **yarn**

```bash
yarn add react-native-aria@0.2.2
```

<!-- tabs:end -->

#### **npm**

```bash
npm install react-native-aria@0.2.2
```

<!-- tabs:end -->

下面的代码展示了useToggleButton的基本使用场景：

<!-- {% raw %} -->
```js
import React from "react";
import { useToggleButton } from "@react-native-aria/button";
import { Pressable, Text, View } from "react-native";
import { useToggleState } from "@react-stately/toggle";
import { useRef } from "react";

export function ToggleButton(props) {
  const ref = useRef(null);
  let state = useToggleState(props);
  let { buttonProps, isPressed } = useToggleButton(props, state, ref); //useToggleButton 是一个用于创建可切换按钮的 Hook，接受三个参数

  return (
    <View>
      <Pressable
        ref={ref}
        {...buttonProps}
        style={{
          backgroundColor: state.isSelected ? "rgb(9, 90, 186)" : "#e1e1e1",
          padding: 5,
        }}
      >
        <Text
          style={{
            color: state.isSelected ? "#f1f1f1" : "#000",
          }}
        >
          A simple toggle button
        </Text>
      </Pressable>

      <View>
        <View>
          <Text>{state.isSelected ? "Selected" : "Not Selected"}</Text>
        </View>
      </View>
    </View>
  );
}

export default function AriaDemo() {
  return (
    <View style={{ width: "100%", marginTop: "100" }}>
      <ToggleButton>Toggle button</ToggleButton>
    </View>
  );
}
```
<!-- {% endraw %} -->

下面的代码展示了useCheckbox与useCheckboxGroup的基本使用场景：

```javascript
import React ,{ useContext, useRef }from 'react';
import {useCheckboxGroupState} from '@react-stately/checkbox';
import {useCheckbox, useCheckboxGroup,useCheckboxGroupItem} from '@react-native-aria/checkbox';
import {Platform, Pressable, Text, View} from 'react-native';
import {VisuallyHidden} from '@react-aria/visually-hidden';
import {useFocusRing} from '@react-native-aria/focus';
let CheckboxGroupContext = React.createContext<any>(null);

export function CheckboxGroup(props: any) {
  let {children, label} = props;
  let state = useCheckboxGroupState(props);
  let {checkboxgroupProps, labelProps} = useCheckboxGroup(props, state);

  return (
    <View {...checkboxgroupProps}>
      {label && <Text {...labelProps}>{label}</Text>}
      <CheckboxGroupContext.Provider value={state}>
        {children}
      </CheckboxGroupContext.Provider>
    </View>
  );
}
export function Checkbox(props: any) {

  let state = useContext(CheckboxGroupContext);
  const inputRef = React.useRef(null);
  let {isFocusVisible, focusProps} = useFocusRing();
  let { inputProps } = state
  ?
    useCheckboxGroupItem(
      {
        ...props,
        isRequired: props.isRequired,
        validationState: props.validationState,
      },
      state,
      inputRef
    )
  :
    useCheckbox(props, useToggleState(props), inputRef);
  return (
    <>
      <Pressable {...inputProps} {...focusProps}>
        <View style={{flexDirection: 'row', alignItems: 'center'}}>
          <View style={isFocusVisible ? {borderWidth: 1} : {}}></View>
          <Text>{props.children}</Text>
        </View>
        <Text>{inputProps.checked ? 'selected' : 'not selected'}</Text>
      </Pressable>
    </>
  );
}

export default function CheckboxDemo() {
  return (
    <View style={{width: '100%', marginTop: '20', marginLeft: '30'}}>
      <CheckboxGroup label="Favorite pet">
        <Checkbox value="dogs">Dogs</Checkbox>
        <Checkbox value="cats">Cats</Checkbox>
        <Checkbox value="rabbits">rabbits</Checkbox>
      </CheckboxGroup>
    </View>
  );
}

```

下面的代码展示了useRadio与useRadioGroup的基本使用场景：

```javascript
import React from "react";
import { useRadioGroupState } from "@react-stately/radio";
import { useRadio, useRadioGroup } from "@react-native-aria/radio";
import { Platform, Pressable, Text, View } from "react-native";
import { VisuallyHidden } from "@react-aria/visually-hidden";
import { useFocusRing } from "@react-native-aria/focus";

let RadioContext = React.createContext<any>({});

export function RadioGroup(props: any) {
  let { children, label } = props;
  let state = useRadioGroupState(props);
  let { radioGroupProps, labelProps } = useRadioGroup(props, state);

  return (
    <View {...radioGroupProps}>
      <Text {...labelProps}>{label}</Text>
      <RadioContext.Provider
        value={{
          isDisabled: props.isDisabled,
          isReadOnly: props.isReadOnly,
          state,
        }}
      >
        {children}
      </RadioContext.Provider>
    </View>
  );
}

export function Radio(props: any) {
  let { state, isReadOnly, isDisabled } = React.useContext(RadioContext);
  const inputRef = React.useRef(null);
  let { inputProps } = useRadio(
    { isReadOnly, isDisabled, ...props },
    state,
    inputRef
  );
  let { isFocusVisible, focusProps } = useFocusRing();

  let isSelected = state.selectedValue === props.value;

  return (
    <>
        <Pressable {...inputProps} {...focusProps}>
          <View style={{ flexDirection: "row", alignItems: "center" }}>
            <View style={isFocusVisible ? { borderWidth: 1 } : {}}>
              <Icon size={30} color={"#000"} name={"radiobox-marked"} />
            </View>
            <Text>{props.children}</Text>
          </View>
          <Text>{isSelected ? "selected" : "not selected"}</Text>
        </Pressable>
    </>
  );
}

export default function RadioDemo() {
  return (
    <View style={{width:'100%',marginTop:'20',marginLeft:'30'}}>
       <RadioGroup label="Favorite pet">
      <Radio value="dogs">Dogs</Radio>
      <Radio value="cats">Cats</Radio>
    </RadioGroup>
    </View>
     );
}
```

下面的代码展示了useSwitch的基本使用场景：

```javascript
import { useToggleState } from "@react-stately/toggle";
import React, { useRef } from "react";
import {
  StyleSheet,
  Text,
  View,
  Animated,
  Platform,
  Pressable,
} from "react-native";
import { useSwitch } from "@react-native-aria/switch";
import { useFocusRing } from "@react-native-aria/focus";
import { VisuallyHidden } from "@react-aria/visually-hidden";

const calculateDimensions = (size: any) => {
  switch (size) {
    case "small":
      return {
        width: 40,
        padding: 10,
        circleWidth: 15,
        circleHeight: 15,
        translateX: 22,
      };
    case "large":
      return {
        width: 70,
        padding: 20,
        circleWidth: 30,
        circleHeight: 30,
        translateX: 38,
      };
    default:
      return {
        width: 46,
        padding: 12,
        circleWidth: 18,
        circleHeight: 18,
        translateX: 26,
      };
  }
};
const defaultProps = {
  isOn: false,
  onColor: "#4cd137",
  offColor: "#ecf0f1",
  size: "medium",
  labelStyle: {},
  thumbOnStyle: {},
  thumbOffStyle: {},
  trackOnStyle: {},
  trackOffStyle: {},
  icon: null,
  disabled: false,
  animationSpeed: 300,
  useNativeDriver: true,
  circleColor: "white",
};
export function Switch(origProps: any) {
  const props = {
    ...defaultProps,
    ...origProps,
  };

  const offsetX = useRef(new Animated.Value(0));
  const dimensions = useRef(calculateDimensions(props.size));

  const createToggleSwitchStyle = () => [
    {
      justifyContent: "center",
      width: dimensions.current.width,
      borderRadius: 20,
      padding: dimensions.current.padding,
      backgroundColor: props.isOn ? props.onColor : props.offColor,
    },
    props.isOn ? props.trackOnStyle : props.trackOffStyle,
  ];

  const createInsideCircleStyle = () => [
    {
      alignItems: "center",
      justifyContent: "center",
      margin: Platform.OS === "web" ? 0 : 4,
      left: Platform.OS === "web" ? 4 : 0,
      position: "absolute",
      backgroundColor: props.circleColor,
      transform: [{ translateX: offsetX.current }],
      width: dimensions.current.circleWidth,
      height: dimensions.current.circleHeight,
      borderRadius: dimensions.current.circleWidth / 2,
      shadowColor: "#000",
      shadowOffset: {
        width: 0,
        height: 2,
      },
      shadowOpacity: 0.2,
      shadowRadius: 2.5,
      elevation: 1.5,
    },
    props.isOn ? props.thumbOnStyle : props.thumbOffStyle,
  ];

  const { isOn, icon } = props;

  const toValue = isOn
    ? dimensions.current.width - dimensions.current.translateX
    : 0;

  Animated.timing(offsetX.current, {
    toValue,
    duration: props.animationSpeed,
    useNativeDriver: props.useNativeDriver,
  }).start();

  return (
    <View style={styles.container}>
      <View style={[...createToggleSwitchStyle(), { marginBottom: 5 }]}>
        <Animated.View style={createInsideCircleStyle()}>{icon}</Animated.View>
      </View>
      <Text>{isOn ? "on" : "off"}</Text>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    alignItems: "center",
  },
  labelStyle: {
    marginHorizontal: 10,
  },
});

export function ControlledSwitch() {
  const state = useToggleState();
  const { isFocusVisible, focusProps } = useFocusRing();
  const inputRef = useRef(null);
  let { inputProps } = useSwitch(
    { "aria-label": "Example switch" },
    state,
    inputRef
  );
    return (
      <Pressable {...inputProps} {...focusProps} ref={inputRef}>
        <View style={isFocusVisible ? { borderWidth: 2 } : {}}>
          <Switch
            isOn={state.isSelected}
            onColor="green"
            offColor="red"
            label={"this is a switch"}
            labelStyle={{ color: "black", fontWeight: "900" }}
            size="large"
            onToggle={state.toggle}
          />
        </View>
      </Pressable>
    );
  }
export default function SwitchDemo () {
  return (
    <View style={{marginTop:'30'}}>
     <ControlledSwitch></ControlledSwitch>
    </View>
     );
}

```

下面的代码展示了useOverlayPosition的基本使用场景：

```javascript
import React from "react";
import {
  OverlayContainer,
  useOverlayPosition,
  OverlayProvider,
} from "@react-native-aria/overlays";
import {
  View,
  Text,
  Pressable,
  TouchableWithoutFeedback,
  StyleSheet,
} from "react-native";

// Button to close overlay on outside click
function CloseButton(props) {
  return (
    <TouchableWithoutFeedback onPress={props.onClose}>
      <View style={StyleSheet.absoluteFill}></View>
    </TouchableWithoutFeedback>
  );
}

const OverlayView = ({ triggerRef, placement }) => {
  let overlayRef = React.useRef();

  const { overlayProps } = useOverlayPosition({
    placement,
    targetRef: triggerRef,
    overlayRef,
    offset: 10,
  });

  return (
    <View
      style={{
        position: "absolute",
        ...overlayProps.style,
      }}
      ref={overlayRef}
    >
      <View
        style={{
          backgroundColor: "lightgray",
          padding: 20,
        }}
      >
        <Text>Hello World</Text>
      </View>
    </View>
  );
};

function Trigger({ placement }) {
  let triggerRef = React.useRef();
  const [visible, setVisible] = React.useState(false);
  const toggleVisible = () => {
    setVisible(!visible);
  };

  return (
    <View style={styles.wrapper}>
      <Pressable
        onPress={toggleVisible}
        ref={triggerRef}
        accessibilityRole="button"
        accessibilityLabel="Click here to open an overlay"
      >
        <View style={styles.trigger}>
          <Text>Trigger</Text>
        </View>
      </Pressable>
      {visible && (
        <OverlayContainer>
          <CloseButton onClose={toggleVisible} />
          <OverlayView triggerRef={triggerRef} placement={placement} />
        </OverlayContainer>
      )}
    </View>
  );
}

export default function OverlaysDemo() {
  return (
    <OverlayProvider>
      <Trigger />
      <View style={{ height: "100" }}></View>
    </OverlayProvider>
  );
}

const styles = StyleSheet.create({
  wrapper: {
    height: 500,
    alignItems: "center",
    justifyContent: "center",
  },
  trigger: {
    flexDirection: "row",
    borderWidth: 1,
    paddingHorizontal: 10,
    paddingVertical: 10,
  },
});
```

更多hooks请参考[react-native-aria官方文档](https://geekyants.github.io/react-native-aria/docs/)

## 约束与限制

## 兼容性

本文档内容基于以下版本验证通过：

1. RNOH：0.72.13; SDK：HarmonyOS NEXT Developer Preview1; IDE：DevEco Studio 4.1.3.500; ROM：2.0.0.59;

## 属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

以下属性已验证，详情见 [react-native-aria官方文档](https://geekyants.github.io/react-native-aria/docs/)

>

### Hooks

| Name               | Description                                                                                                                                                                                                   | Type     | Platform | HarmonyOS Support |
| ------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | -------- | ----------------- |
| useToggleButton    | Provides the behavior and accessibility implementation for a toggle button component. ToggleButtons allow users to toggle a selection on or off, for example switching between two states or modes.           | Function | All      | yes               |
| useCheckbox        | Provides the behavior and accessibility implementation for a checkbox component. Checkboxes allow users to select multiple items from a list of individual items, or to mark one individual item as selected. | Function | All      | yes               |
| useCheckboxGroup   | Provides the behavior and accessibility implementation for a checkbox group component. Checkbox groups allow users to select multiple items from a list of options.                                           | Function | All      | yes               |
| useRadioGroup      | Provides the behavior and accessibility implementation for a radio group component. Radio groups allow users to select a single item from a list of mutually exclusive options.                               | Function | All      | yes               |
| useSwitch          | Provides the behavior and accessibility implementation for a switch component. A switch is similar to a checkbox, but represents on/off values as opposed to selection.                                       | Function | All      | yes               |
| OverlayContainer   | Provides React Portal like functionality for React Native apps which can be useful for displaying absolutely positioned components like Menu, Tooltip, Popover.                                               | Function | All      | yes               |
| useOverlayPosition | Handles positioning overlays like popovers and menus relative to a trigger element, and updating the position when the window resizes.                                                                        | Function | All      | yes               |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/gluestack/react-native-aria/blob/main/LICENSE)，请自由地享受和参与开源。
