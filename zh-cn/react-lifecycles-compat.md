> 模板版本：v0.1.3

<p align="center">
  <h1 align="center"> <code>react-lifecycles-compat</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/reactjs/react-lifecycles-compat">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/reactjs/react-lifecycles-compat)

## 安装与使用

进入到工程目录并输入以下命令：

> [!TIP] # 处替换为 tgz 包的路径

<!-- tabs:start -->

#### **npm**

```bash
npm install react-lifecycles-compat@3.0.4
```

#### **yarn**

```bash
yarn add react-lifecycles-compat@3.0.4
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

```js
import React from "react";
import { Text, View, Button } from "react-native";
import { polyfill } from "react-lifecycles-compat";
import { State } from "react-native-gesture-handler";
class ShowComponent extends React.Component {
  render() {
    return (
      <View>
        <Text
          style={{
            width: "95%",
            textAlign: "center",
            height: 60,
            lineHeight: 55,
            backgroundColor: "pink",
            fontSize: 40,
            borderRadius: 30,
          }}
        >
          新组件
        </Text>
      </View>
    );
  }
}
class ExampleComponent extends React.Component {
  state = {
    Text1: "未执行",
    count1: 0,
    Text2: "未执行",
    visible: false,
  };
  static getDerivedStateFromProps = (nextProps, prevState) => {
    // Normally this method would only work for React 16.3 and newer,
    // But the polyfill will make it work for older versions also!
    return { Text1: "已执行", count1: prevState.count1 + 1 };
  };

  getSnapshotBeforeUpdate(prevProps, prevState) {
    // Normally this method would only work for React 16.3 and newer,
    // But the polyfill will make it work for older versions also!
    return true;
  }
  componentDidUpdate(prevProps, prevState, snapshot) {
    if (snapshot) {
      if (this.state.Text2 !== "已执行") {
        this.setState({
          Text2: "已执行",
        });
      }
    }
  }
  // render() and other methods ...
  handleClick = () => {
    this.setState({ visible: true });
  };
  render() {
    const { visible, Text1, Text2, count1 } = this.state;
    return (
      <View>
        <View style={{ width: "100%", height: 60, margin: 10 }}>
          {visible ? <ShowComponent></ShowComponent> : <Text>{visible}</Text>}
        </View>
        <Text style={{ backgroundColor: "#F5F5F5", margin: 5 }}>
          getDerivedStateFromProps生命周期会在React初始化挂载和后续更新时调用render之前调用，返回一个对象来更新state，或者返回null就不更新任何内容
        </Text>
        <Text style={{ backgroundColor: "#F5F5F5", margin: 5 }}>
          getSnapshotBeforeUpdate生命周期会在React更新DOM之前时直接调用，使你的组件能够在DOM发生更改之前捕获一些信息
        </Text>
        <Button title="点击创建组件！" onPress={this.handleClick} />
        <Text
          style={{
            width: "100%",
            textAlign: "center",
            lineHeight: 40,
            height: 40,
            backgroundColor: "green",
            margin: 5,
            fontSize: 16,
          }}
        >
          生命周期getDerivedStateFromProps{this.state.Text1}+{this.state.count1}
        </Text>
        <Text
          style={{
            width: "100%",
            textAlign: "center",
            lineHeight: 40,
            height: 40,
            backgroundColor: "green",
            margin: 5,
            fontSize: 16,
          }}
        >
          生命周期getSnapshotBeforeUpdate{this.state.Text2}
        </Text>
      </View>
    );
  }
}

// Polyfill your component so the new lifecycles will work with older versions of React:
polyfill(ExampleComponent);

export default ExampleComponent;
```

### 兼容性

在以下版本验证通过

1. RNOH：0.72.13; SDK：HarmonyOS NEXT Developer Preview1; IDE：DevEco Studio 4.1.3.500; ROM：204.1.0.59;
2. RNOH：0.72.20; SDK：HarmonyOS NEXT Developer Beta1 B.0.18、HarmonyOS NEXT Developer Preview0 B.0.60、HarmonyOS NEXT Developer Preview2 B.0.73; IDE：DevEco Studio 5.0.3.200; ROM：2.0.0.13;

| Name                     | Description                            | Required | Platform | HarmonyOS Support |
| ------------------------ | -------------------------------------- | -------- | -------- | ----------------- |
| getDerivedStateFromProps | Initialize the mount.                  | NO       | Android  | YES               |
| getSnapshotBeforeUpdate  | Call directly before updating the DOM. | NO       | Android  | YES               |

## 遗留问题

## 其他

以下事项与原库保持一致需注意遵循：

为了使polyfill工作，您的组件不能定义以下生命周期：componentWillMount，componentWillReceiveProps，componentWillUpdate.

如果您的组件包含getSnapshotBeforeUpdate，那么也必须定义componentDidUpdate，如果不满足上述任何条件，将抛出错误.
