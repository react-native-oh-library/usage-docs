> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-root-siblings</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/magicismight/react-native-root-siblings">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/magicismight/react-native-root-siblings/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [! TIP] [Github 地址](https://github.com/magicismight/react-native-root-siblings)

## 安装与使用

<!-- tabs:start -->

#### **npm**

```bash
npm i react-native-root-siblings@5.0.1
```

#### **yarn**

```bash
yarn add react-native-root-siblings@5.0.1
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [! WARNING] 使用时 import 的库名不变。

The easiest way to create overlays( `Modal` , `Popover` , `Dialog` etc) for both `react` and `react-native` . 

Make your own `showModal` and use it in any component without any `isShow` state or even in a pure function call.

```jsx
import RootSiblingsManager from 'react-native-root-siblings';

export const showModal = (renderModal) => {
  let rootNode;
  const onClose = () => {
    rootNode?.destroy();
    rootNode = null;
  };
  rootNode = new RootSiblingsManager(renderModal(onClose));
  return onClose;
};

import WelcomeModal from './WelcomeModal';

export function showWelcomeModal() {
  showModal((onClose) => <WelcomeModal onClose={onClose} />);
}

// ...
function HomeScreen() {
  return <Button onClick={showWelcomeModal}>Welcome!</Button>
}

setTimeout(showWelcomeModal, 3000);
```

---

Insert `RootSiblingParent` between your providers and root app in your root render function.

```jsx
import { RootSiblingParent } from 'react-native-root-siblings';

return (
  <SomeProviders>
    <RootSiblingParent>  // <- use RootSiblingParent to wrap your root component
      <App />
    </RootSiblingParent>
  </SomeProviders>
);      
```

`RootSiblingParent` works as a mounting base and can be mounted multiple times. Only the last mounted one would be active.

In react native, a view has a higher hierarchy if it's more close to the root level.

```jsx
<RootSiblingParent>
  <RootView>  //  <- the highest view
    <NavigationView>
      <ScreenView>  //  <- the lowest view
       { /* what if you want to show a fullscreen modal here?
          * usually you have to use a Native Modal which is even higher than RootView
          * but it's buggy and has a lot of limitations
          */}
        <RootSiblingPortal>
        { /* View put in here would be transported to RootSiblingParent 
            * So it can have a same hierarchy as the RootView to cover any other views
            */}
          <View>
          </View>
        </RootSiblingPortal>
      </ScreenView>
    </NavigationView>
  </View>
</RootSiblingParent>
```

In react we have `createPortal` but still it's not so convenient as it can not be used outside of a component. 

`react-native-root-siblings` provides the most possible flexibility:

### Imperative API

1. Create sibling element

```jsx
let sibling = new RootSiblings(<View
    style={{top: 0,right: 0,bottom: 0,left: 0,backgroundColor: 'red'}}
/>);
```

This will create a View element cover all of your app elements, 
and returns a sibling instance.
You can create a sibling anywhere, no matter in a component, hook or even a pure function.

2. Update sibling element

```jsx
sibling.update(<View
    style={{top: 10,right: 10,bottom: 10,left: 10,backgroundColor: 'blue'}}
/>);
```

This will update the sibling instance to a View with blue backgroundColor and cover the screen by `10` offset distance.

3. Destroy sibling element

```js
sibling.destroy();
```

This will remove the sibling element.

### Component API

```jsx
import { RootSiblingPortal } from 'react-native-root-siblings';

class extends Component {
    render() {
        return (
            <RootSiblingPortal>
                <View style={[StyleSheet.absoluteFill, { backgroundColor: 'rgba(0, 0, 0, 0.25)' }]} />
            </RootSiblingPortal>
        )
    }
}

```

### EXAMPLE

```jsx
import React, {
    AppRegistry,
    View,
    Component,
    TouchableHighlight,
    StyleSheet,
    Text
} from 'react-native';
import Dimensions from 'Dimensions';

// Import library there,it will wrap everything registered by AppRegistry.registerComponent
// And add or remove other elements after the root component
import RootSiblings from 'react-native-root-siblings';

var id = 0;
var elements = [];
class SiblingsExample extends Component{
    addSibling = () => {
        let sibling = new RootSiblings(<View
            style={[styles.sibling, {top: id * 20}]}
        >
            <Text>I`m No.{id}</Text>
        </View>);
        id++;
        elements.push(sibling);
    };

    destroySibling = () => {
        let lastSibling = elements.pop();
        lastSibling && lastSibling.destroy();
    };

    updateSibling = () => {
        let lastId = elements.length - 1;
        lastId >= 0 && elements[lastId].update(<View
            style={[styles.sibling, {top: lastId * 20}]}
        >
            <Text>I`m No.{lastId} : {Math.random()}</Text>
        </View>);
    };

    render() {
        return <View style={styles.container}>
            <TouchableHighlight
                style={styles.button}
                onPress={this.addSibling}
            >
                <Text style={styles.buttonText}>Add element</Text>
            </TouchableHighlight>
            <TouchableHighlight
                style={styles.button}
                onPress={this.destroySibling}
            >
                <Text style={styles.buttonText}>Destroy element</Text>
            </TouchableHighlight>
            <TouchableHighlight
                style={styles.button}
                onPress={this.updateSibling}
            >
                <Text style={styles.buttonText}>Update element</Text>
            </TouchableHighlight>
        </View>;
    }
}

AppRegistry.registerComponent('SiblingsExample', () => SiblingsExample);

var styles = StyleSheet.create({
    container: {
        flex: 1,
        alignItems: 'center',
        justifyContent: 'center',
        backgroundColor: 'green',
    },
    button: {
        borderRadius: 4,
        padding: 10,
        marginLeft: 10,
        marginRight: 10,
        backgroundColor: '#ccc',
        borderColor: '#333',
        borderWidth: 1,
    },
    buttonText: {
        color: '#000'
    },
    sibling: {
        left: 0,
        height: 20,
        width: Dimensions.get('window').width / 2,
        backgroundColor: 'blue',
        opacity: 0.5
    }
});

```

## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

RNOH: 0.72.23; SDK: HarmonyOS NEXT Developer Beta1; IDE: DevEco Studio: 5.0.3.27; ROM: 3.0.0.19; 

RNOH: 0.72.33; SDK: Openharmony 5.0.0.71(API Version 12 Release); IDE: DevEco Studio: 5.0.3.900; ROM: Next.0.0.71;

## 静态方法

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| RootSiblings(element: ReactElement, options?: Options)  | 创建一个新的兄弟元素  | RootSiblings  | no | Android/IOS  | yes |
| RootSiblings.update(element: ReactNode, callback?: () => void)  | 更新兄弟元素内容  | void  | no | Android/IOS  | yes |
| RootSiblings.destroy(callback?: () => void)  | 销毁兄弟元素  | void  | no | Android/IOS  | yes |
| RootSiblingParent(props: {children: ReactNode; inactive?: boolean;})  | 包裹需要创建和管理的根级组件  | import("react/jsx-runtime").JSX.Element  | no | Android/IOS  | yes |
| RootSiblingPortal(props: { children: ReactNode;})  | 允许将子组件渲染到应用的根组件之外的任意位置  | null  | no | Android/IOS  | yes |
| setSiblingWrapper(wrapper: (sibling: ReactNode) => ReactNode)  | 设置全局组件的包装器  | void  | no | Android/IOS  | yes |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/magicismight/react-native-root-siblings/blob/master/LICENSE) ，请自由地享受和参与开源。
