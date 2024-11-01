> 模板版本：v0.2.2

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

> [!TIP] [Github 地址](https://github.com/gluestack/react-native-aria/tree/main)

## 安装与使用

React Native ARIA是可增量采用的。每个组件都作为单独的包发布，因此您可以在单个组件中使用它，并随着时间的推移逐渐添加更多组件。所有这些包都在npm上的@react-native-aria范围内发布。
> [!TIP] 该库已经不再维护，如果执行总包命令，项目运行缺失模块，就需要卸载旧包，在命令后增加--legacy-peer-deps，然后再次下载包文件

进入到工程目录并输入以下命令：

#### **yarn**

```bash
yarn add react-native-aria@0.2.3
```

<!-- tabs:end -->

#### **npm**

```bash
npm install react-native-aria@0.2.3
```

<!-- tabs:end -->

除了总包之外，我们还提供了一些单独包，如：@react-native-aria/button

#### **yarn**

```bash
yarn add @react-native-aria/button@0.2.7
```

<!-- tabs:end -->

#### **npm**

```bash
npm install @react-native-aria/button@0.2.7
```

<!-- tabs:end -->

下面的代码展示了useToggleButton的基本使用场景：

```js
import React from "react";
import { useToggleButton } from "@react-native-aria/button";
import { useToggleState } from "@react-stately/toggle";
import { Pressable, Text, View } from "react-native";
import { useRef } from "react";

export function ToggleButton(props: any) {
    const ref = useRef(null);
    let state = useToggleState(props);
    let { buttonProps, isPressed } = useToggleButton(props, state);

    return (
        <View style={{ flexDirection: 'row', alignItems: 'center' }}>
            <Text>ToggleButton：</Text>
            <Pressable ref={ref} {...buttonProps}
                style={{
                    backgroundColor: state.isSelected ? "rgb(9, 90, 186)" : "#e1e1e1", borderRadius: 15,
                    padding: 5, width: 100, height: 30, justifyContent: 'center', alignItems: 'center'
                }}
            >
                <Text style={{ color: state.isSelected ? "#f1f1f1" : "#000" }} >点击切换</Text>
            </Pressable>
        </View>
    );
}

export default ToggleButton

```

下面的代码展示了useCheckbox与useCheckboxGroup的基本使用场景：

```javascript
import React, { useContext, useRef } from 'react';
import { Pressable, View, Text } from 'react-native';
import { useCheckbox, useCheckboxGroupItem, useCheckboxGroup } from '@react-native-aria/checkbox';
import { useToggleState } from '@react-stately/toggle';
import { useCheckboxGroupState } from "@react-stately/checkbox";
import { useFocusRing } from '@react-native-aria/focus';

let CheckboxGroupContext = React.createContext<any>(null);

const CheckboxItems = [{ key: 'soccer', value: '足球' }, { key: 'baseball', value: '棒球' }, { key: 'basketball', value: '篮球' }]
const findName = (value: string) => {
    const item = CheckboxItems.find(i => { return i.key === value; })
    return item && item.value
}

export function CheckboxGroup(props: any) {
    let { children, label } = props;
    let state = useCheckboxGroupState(props);
    let { groupProps, labelProps } = useCheckboxGroup(props, state);

    return (
        <View {...groupProps} style={{ flexDirection: 'row', alignItems: 'center' }}>
            {label && <Text {...labelProps}>{label}</Text>}
            <CheckboxGroupContext.Provider value={state}>
                {children}
            </CheckboxGroupContext.Provider>
            <View><Text>已经选择：</Text>{props.value.map(i=>{
                return <Text>{findName(i)}</Text>
            })}</View> 
        </View>
    );
}


export function Checkbox(props: any) {
    let groupState = useContext(CheckboxGroupContext);
    let inputRef = useRef<HTMLInputElement>(null);

    let { isFocusVisible, focusProps } = useFocusRing();

    let { inputProps } = groupState ? useCheckboxGroupItem(
        {
            ...props,
            isRequired: props.isRequired,
            validationState: props.validationState,
        },
        groupState,
        inputRef
    ) : useCheckbox(props, useToggleState(props), inputRef);

    return (
        <View style={isFocusVisible ? { borderWidth: 2 } : {}}>
            <Pressable {...inputProps} {...focusProps} >
                <View style={{ flexDirection: 'row', alignItems: 'center', marginRight: 5 }}>
                    {props.children}
                </View>
            </Pressable>
        </View>
    );
}

export const CheckboxExample = () => {
    const [state, setCheckbox] = React.useState([]);

    return (
        <CheckboxGroup
            label="CheckboxGroup："
            value={state}
            onChange={(val: any) => {
                setCheckbox(val);
            }}
        >
            {CheckboxItems.map(i => {
                return <Checkbox key={i.key} value={i.key}>
                    <Text>{i.value}</Text>
                </Checkbox>;
            })}
        </CheckboxGroup>
    );
};
export default CheckboxExample

```

下面的代码展示了useRadio与useRadioGroup的基本使用场景：

```javascript
import React from "react";
import { useRadioGroupState } from "@react-stately/radio";
import { useRadio, useRadioGroup } from "@react-native-aria/radio";
import { Pressable, Text, View } from "react-native";
import { useFocusRing } from "@react-native-aria/focus";

let RadioContext = React.createContext<any>({});

const radioItems = [{ key: 'dogs', value: '狗子' }, { key: 'cats', value: '猫儿' }]
const findName = (value: string) => {
    const item = radioItems.find(i => { return i.key === value; })
    return item && item.value
}

export function RadioGroup(props: any) {
    let { children, label } = props;
    let state = useRadioGroupState(props);
    let { radioGroupProps, labelProps } = useRadioGroup(props, state);

    return (
        <View {...radioGroupProps} style={{ flexDirection: 'row', alignItems: 'center' }}>
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
            <Text>已经选择：{findName(state.selectedValue as string)}</Text>
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

    return (
        <Pressable {...inputProps}{...focusProps} style={{ marginRight: 5 }}>
            <View style={[{ flexDirection: 'row', alignItems: 'center' }, isFocusVisible ? { borderWidth: 1 } : {},]}>
                <Text>{props.children}</Text>
            </View>
        </Pressable>
    );
}

export const RadioExample = () => {
    return (
        <View>
            <RadioGroup label="RadioGroup：">
                {radioItems.map(i => {
                    return <Radio key={i.key} value={i.key}>{i.value}</Radio>
                })}
            </RadioGroup>
        </View>
    );
};
export default RadioExample

```

下面的代码展示了useSwitch的基本使用场景：

```javascript
import { useToggleState } from "@react-stately/toggle";
import React, { useRef } from "react";
import { StyleSheet, Text, View, Animated, Pressable } from "react-native";
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
            margin: 4,
            left: 0,
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

    const { isOn, icon, label, labelStyle = {} } = props;

    const toValue = isOn
        ? dimensions.current.width - dimensions.current.translateX
        : 0;

    Animated.timing(offsetX.current, {
        toValue,
        duration: props.animationSpeed,
        useNativeDriver: props.useNativeDriver,
    }).start();

    return (
        <View style={{ flexDirection: 'row', alignItems: 'center' }}>
            {label && <Text style={labelStyle}>{label}</Text>}
            <View style={[...createToggleSwitchStyle(), { marginBottom: 5 }]}>
                <Animated.View style={createInsideCircleStyle()}>{icon}</Animated.View>
            </View>
            <Text style={{ marginLeft: 5 }}>{isOn ? "开" : "关"}</Text>
        </View>
    );
}

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
                    label='Switch：'
                    size="large"
                    onToggle={state.toggle}
                />
            </View>
        </Pressable>
    );

}
export default ControlledSwitch

```

下面的代码展示了useOverlayPosition的基本使用场景：

```javascript
import React from "react";
import { useOverlayPosition, OverlayProvider, OverlayContainer } from "@react-native-aria/overlays";
import { useButton } from "@react-native-aria/button";
import { View, Text, Pressable, ScrollView, Modal } from "react-native";
import { useToggleState } from "@react-stately/toggle";

const positions = [
    "top",
    "left",
    "right",
    "bottom",
    "top left",
    "top right",
    "left top",
    "left bottom",
    "bottom right, bottom left",
    "right top",
    "right bottom",
];

export function TriggerWrapper() {
    const [placement, setPlacement] = React.useState<any>(-1);
    React.useEffect(() => {
        const id = setInterval(() => {
            setPlacement((prev) => (prev + 1) % positions.length);
        }, 2000);
        return () => clearInterval(id);
    }, []);

    return <Trigger placement={positions[placement]}></Trigger>;
}

const OverlayView = ({ targetRef, placement = 'top' }) => {
    let overlayRef = React.useRef();

    const { overlayProps } = useOverlayPosition({
        placement: placement as any,
        targetRef,
        overlayRef,
        offset: 10,
    });

    return (
        <ScrollView
            bounces={false}
            style={{
                position: "absolute",
                height: 400,
                backgroundColor: "lightgray",
                ...overlayProps.style,
            }}
            ref={(node) => overlayRef.current = node}
        >
            <View
                style={{
                    padding: 20,
                    height: 5000,
                }}
            >
                <Text>Hello world</Text>
            </View>
        </ScrollView>
    );
};

export function Trigger({ placement }: any) {
    let ref = React.useRef();
    const toggleState = useToggleState();

    let { buttonProps } = useButton({ onPress: toggleState.toggle }, ref);

    return (
        <View style={{ flexDirection: 'row', alignItems: "center" }} >
            <Text>useOverlayPosition：</Text>
            <Pressable
                {...buttonProps}
                ref={ref}
                role="button"
                aria-label="Click here to perform some actions"
            >
                <View
                    style={{
                        flexDirection: "row",
                        borderWidth: 1,
                        paddingHorizontal: 10,
                        paddingVertical: 10,
                    }}
                >
                    <Text>点我一下</Text>
                </View>
            </Pressable>
            <Modal visible={toggleState.isSelected} onRequestClose={toggleState.toggle}>
                <OverlayProvider>
                    <OverlayContainer>
                        <OverlayView targetRef={ref} placement={placement} />
                    </OverlayContainer>
                </OverlayProvider>
            </Modal>
        </View>
    );
}
export default TriggerWrapper

```

更多hooks请参考[react-native-aria官方文档](https://geekyants.github.io/react-native-aria/docs/)

## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

1. RNOH：0.72.13; SDK：HarmonyOS NEXT Developer Preview1; IDE：DevEco Studio 4.1.3.500; ROM：2.0.0.59;
2. RNOH：0.72.27; SDK：HarmonyOS-Next-DB1 5.0.0.29(SP1) ; IDE：DevEco Studio 5.0.3.400; ROM：3.0.0.25;
3. RNOH：0.72.29; SDK：HarmonyOS NEXT Developer Beta6; IDE：DevEco Studio 5.0.3.706; ROM：3.0.0.61;
4. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;

## Hooks

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name               | Description                                                                                                                                                                                                   | Type     | Required | Platform | HarmonyOS Support |
|--------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------|----------|----------|-------------------|
| useToggleButton    | Provides the behavior and accessibility implementation for a toggle button component. ToggleButtons allow users to toggle a selection on or off, for example switching between two states or modes.           | Function | no       | iOS,Android      | yes               |
| useCheckbox        | Provides the behavior and accessibility implementation for a checkbox component. Checkboxes allow users to select multiple items from a list of individual items, or to mark one individual item as selected. | Function | no       | iOS,Android      | yes               |
| useCheckboxGroup   | Provides the behavior and accessibility implementation for a checkbox group component. Checkbox groups allow users to select multiple items from a list of options.                                           | Function | no       | iOS,Android      | yes               |
| useRadioGroup      | Provides the behavior and accessibility implementation for a radio group component. Radio groups allow users to select a single item from a list of mutually exclusive options.                               | Function | no       | iOS,Android      | yes               |
| useSwitch          | Provides the behavior and accessibility implementation for a switch component. A switch is similar to a checkbox, but represents on/off values as opposed to selection.                                       | Function | no       | iOS,Android      | yes               |
| OverlayContainer   | Provides React Portal like functionality for React Native apps which can be useful for displaying absolutely positioned components like Menu, Tooltip, Popover.                                               | Function | no       | iOS,Android      | yes               |
| useOverlayPosition | Handles positioning overlays like popovers and menus relative to a trigger element, and updating the position when the window resizes.                                                                        | Function | no       | iOS,Android      | yes               |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/gluestack/react-native-aria/blob/main/LICENSE)，请自由地享受和参与开源。
