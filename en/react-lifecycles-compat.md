> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-lifecycles-compat</code> </h1>
</p>
<p align="center">
<a href="https://github.com/reactjs/react-lifecycles-compat/blob/master">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20web%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/reactjs/react-lifecycles-compat/blob/master/LICENSE.md">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>




> [!TIP] [GitHub address](https://github.com/reactjs/react-lifecycles-compat)

## Installation and Usage

Go to the project directory and execute the following instruction：

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

The following code shows the basic use scenario of the repository：

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
          New component
        </Text>
      </View>
    );
  }
}
class ExampleComponent extends React.Component {
  state = {
    Text1: "Not Executed ",
    count1: 0,
    Text2: "Not Executed ",
    visible: false,
  };
  static getDerivedStateFromProps = (nextProps, prevState) => {
    // Normally this method would only work for React 16.3 and newer,
    // But the polyfill will make it work for older versions also!
    return { Text1: "Executed ", count1: prevState.count1 + 1 };
  };

  getSnapshotBeforeUpdate(prevProps, prevState) {
    // Normally this method would only work for React 16.3 and newer,
    // But the polyfill will make it work for older versions also!
    return true;
  }
  componentDidUpdate(prevProps, prevState, snapshot) {
    if (snapshot) {
      if (this.state.Text2 !== "Executed ") {
        this.setState({
          Text2: "Executed ",
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
          GetderivedateFromprops Life cycle will call before react initialization and mounting and subsequent updates. Back a object to update the state, or return NULL to update any content without updating any content
        </Text>
        <Text style={{ backgroundColor: "#F5F5F5", margin: 5 }}>
          GetsnapshotBeForeupDate will be called directly before react update DOM, so that your component can capture some information before the DOM changes changes.
        </Text>
        <Button title="Click to create components!" onPress={this.handleClick} />
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
          life cycle getDerivedStateFromProps{this.state.Text1}+{this.state.count1}
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
          life cycle getSnapshotBeforeUpdate{this.state.Text2}
        </Text>
      </View>
    );
  }
}

// Polyfill your component so the new lifecycles will work with older versions of React:
polyfill(ExampleComponent);

export default ExampleComponent;
```

## Constraints

### Compatibility

This document is verified based on the following versions

1. RNOH：0.72.20; SDK：HarmonyOS NEXT Developer Preview2; IDE：DevEco Studio 5.0.3.200; ROM：205.0.0.18;
2. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;

| Name                     | Description                            | Required | Platform | HarmonyOS Support |
| ------------------------ | -------------------------------------- | -------- | -------- | ----------------- |
| getDerivedStateFromProps | Initialize the mount.                  | NO       | Android  | YES               |
| getSnapshotBeforeUpdate  | Call directly before updating the DOM. | NO       | Android  | YES               |

## Known Issues

## Others

The following matters should be consistent with the original library：

In order to make Polyfill work, your component cannot define the following life cycle: componentWillMount，componentWillReceiveProps，componentWillUpdate.

If your component contains GetsnapshotBeForeupDate, then it must also define componentDidUpdate. If it does not meet any of the above conditions, you will throw an error.

## License

This project is licensed under [The MIT License (MIT)](https://github.com/reactjs/react-lifecycles-compat/blob/master/LICENSE.md).
