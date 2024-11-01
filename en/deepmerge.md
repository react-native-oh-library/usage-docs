> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>deepmerge</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/TehShrike/deepmerge/blob/master/license.txt">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!tip] [Github address](https://github.com/TehShrike/deepmerge)

## Installation and Usage

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

#### **npm**

```bash
npm install deepmerge@4.3.1
```

#### **yarn**

```bash
yarn add deepmerge@4.3.1
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

```js
import React from 'react';
import { View, Text, StyleSheet, ScrollView } from 'react-native';
import deepmerge from 'deepmerge';

const App = () => {
  // Define two objects that need to be merged
  const object1 = {
    name: 'John',
    age: 30,
    address: {
      street: '123 Main St',
      city: 'Springfield',
    },
  };

  const object2 = {
    age: 31,
    address: {
      country: 'USA',
    },
    hobbies: ['Reading', 'Hiking'],
  };

  // Merge two objects using deepmerge
  const mergedObject = deepmerge(object1, object2);

  return (
    <ScrollView contentContainerStyle={styles.container}>
      <Text style={styles.title}>Object 1:</Text>
      <Text style={styles.text}>{JSON.stringify(object1, null, 2)}</Text>

      <Text style={styles.title}>Object 2:</Text>
      <Text style={styles.text}>{JSON.stringify(object2, null, 2)}</Text>

      <Text style={styles.title}>Merged Object:</Text>
      <Text style={styles.text}>{JSON.stringify(mergedObject, null, 2)}</Text>
    </ScrollView>
  );
};

const styles = StyleSheet.create({
  container: {
    flexGrow: 1,
    justifyContent: 'center',
    alignItems: 'center',
    backgroundColor: '#f5fcff',
    padding: 20,
  },
  title: {
    fontSize: 20,
    fontWeight: 'bold',
    marginVertical: 10,
  },
  text: {
    fontSize: 16,
    marginBottom: 20,
    textAlign: 'left',
    width: '100%',
  },
});

export default App;
```

## Constraints

### Compatibility

This document is verified based on the following versions:

1. RNOH：0.72.11; SDK：OpenHarmony(api11) 4.1.0.53; IDE：DevEco Studio 4.1.3.412; ROM：2.0.0.52;
2. RNOH：0.72.13; SDK：HarmonyOS NEXT Developer Preview1; IDE：DevEco Studio 4.1.3.500; ROM：2.0.0.58;
3. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;

## API

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

For details, see [deepmerge Source Code](https://github.com/TehShrike/deepmerge)

| Name                                     | Description                                                                                          | Type     | Required | HarmonyOS Support |
| ---------------------------------------- | ---------------------------------------------------------------------------------------------------- | -------- | -------- | ----------------- |
| deepmerge(x, y, [options])               | Merge two objects x and y deeply, returning a new merged object with the elements from both x and y. | function | no       | yes               |
| deepmerge.all(arrayOfObjects, [options]) | Merges any number of objects into a single result object.                                            | function | no       | yes               |

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/TehShrike/deepmerge/blob/master/license.txt).
