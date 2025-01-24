> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>prop-types</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/facebook/prop-types/blob/v15.8.1/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github address](https://github.com/facebook/prop-types/tree/v15.8.1)

## Installation and Usage

<!-- tabs:start -->

#### **npm**

```bash
npm install prop-types
```

#### **yarn**

```bash
yarn add prop-types
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

```js
import React from 'react';
import { View, Text, StyleSheet } from 'react-native';
import PropTypes from 'prop-types';

const Greeting = ({ name, age }) => {
  return (
    <View style={styles.container}>
      <Text style={styles.text}>Hello, {name}!</Text>
      <Text style={styles.text}>You are {age} years old.</Text>
    </View>
  );
};


Greeting.propTypes = {
  name: PropTypes.string.isRequired, 
  age: PropTypes.number,             
};

Greeting.defaultProps = {
  age: 0,
};

const App = () => {
  return (
    <View style={styles.appContainer}>
      <Greeting name="John" age={30} />
      <Greeting name="Doe" />
    </View>
  );
};

const styles = StyleSheet.create({
  appContainer: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
    backgroundColor: '#f5fcff',
  },
  container: {
    marginBottom: 20,
  },
  text: {
    fontSize: 18,
  },
});

export default App;
```

### Compatibility

This document is verified based on the following versions:

1. RNOH: 0.72.11; SDK: OpenHarmony (api11) 4.1.0.53; IDE: DevEco Studio 4.1.3.412; ROM: 2.0.0.52;
2. RNOH: 0.72.13; SDK: HarmonyOS NEXT Developer Preview1; IDE: DevEco Studio 4.1.3.500; ROM: 2.0.0.58;
3. RNOH: 0.72.33; SDK: OpenHarmony 5.0.0.71 (API Version 12 Release); IDE: DevEco Studio 5.0.3.900; ROM: NEXT.0.0.71;

#### Properties

| Name        | Description                                                  | Type      | Required | HarmonyOS Support |
| ----------- | ------------------------------------------------------------ | --------- | -------- | ----------------- |
| any         | Any data type.                                               | Attribute | NO       | yes               |
| array       | The array type.                                              | Attribute | NO       | yes               |
| bool        | The Boolean type.                                            | Attribute | NO       | yes               |
| func        | The function type.                                           | Attribute | NO       | yes               |
| number      | The number type.                                             | Attribute | NO       | yes               |
| object      | The object type.                                             | Attribute | NO       | yes               |
| string      | The string type.                                             | Attribute | NO       | yes               |
| symbol      | The symbol type.                                             | Attribute | NO       | yes               |
| element     | The react element.                                           | Attribute | NO       | yes               |
| node        | Any content that can be rendered, such as a numeric string element, or an array. | Attribute | NO       | yes               |
| elementType | The react type.                                              | Attribute | NO       | yes               |
| instanceOf  | An instance of an object.                                    | function  | NO       | yes               |
| oneOf       | One of the given values.                                     | function  | NO       | yes               |
| oneOfType   | One of the specified types.                                  | function  | NO       | yes               |
| arrayOf     | An array of the specified type.                              | function  | NO       | yes               |
| objectOf    | An object with the attribute value of the specified type.    | function  | NO       | yes               |
| shape       | An object of the specified composition mode.                 | function  | NO       | yes               |
| exact       | A specified attribute that is contained.                     | function  | NO       | yes               |

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/facebook/prop-types/blob/v15.8.1/LICENSE).