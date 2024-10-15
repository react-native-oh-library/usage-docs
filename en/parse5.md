<!-- {% raw %} -->
> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>parse5</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/TehShrike/deepmerge/blob/master/license.txt">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!tip] [Github address](https://github.com/inikulin/parse5)

## Installation and Usage

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

#### **npm**

```bash
npm install parse5@7.1.2
```

#### **yarn**

```bash
yarn add parse5@7.1.2
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

```js
import React, { useEffect, useState } from 'react';
import { View, Text, ScrollView, StyleSheet } from 'react-native';
import * as parse5 from 'parse5';

const App = () => {
  const [parsedContent, setParsedContent] = useState([]);

  useEffect(() => {
    const html = `
      <div>
        <h1>Hello, World!</h1>
        <p>This is a simple HTML parsing example.</p>
        <ul>
          <li>Item 1</li>
          <li>Item 2</li>
          <li>Item 3</li>
        </ul>
      </div>
    `;

    const document = parse5.parse(html);

    const extractContent = (nodes) => {
      let content = [];
      for (const node of nodes) {
        if (node.nodeName === 'h1') {
          content.push({ type: 'h1', text: node.childNodes[0].value });
        } else if (node.nodeName === 'p') {
          content.push({ type: 'p', text: node.childNodes[0].value });
        } else if (node.nodeName === 'ul') {
          const items = node.childNodes
            .filter((child) => child.nodeName === 'li')
            .map((li) => li.childNodes[0].value);
          content.push({ type: 'ul', items });
        } else if (node.childNodes && node.childNodes.length > 0) {
          content = content.concat(extractContent(node.childNodes));
        }
      }
      return content;
    };

    const content = extractContent(document.childNodes);
    setParsedContent(content);
  }, []);

  return (
    <ScrollView contentContainerStyle={styles.container}>
      {parsedContent.map((element, index) => {
        if (element.type === 'h1') {
          return <Text key={index} style={styles.h1}>{element.text}</Text>;
        } else if (element.type === 'p') {
          return <Text key={index} style={styles.p}>{element.text}</Text>;
        } else if (element.type === 'ul') {
          return (
            <View key={index} style={styles.ul}>
              {element.items.map((item, i) => (
                <Text key={i} style={styles.li}>{`• ${item}`}</Text>
              ))}
            </View>
          );
        }
        return null;
      })}
    </ScrollView>
  );
};

const styles = StyleSheet.create({
  container: {
    flexGrow: 1,
    justifyContent: 'center',
    alignItems: 'center',
    padding: 20,
    backgroundColor: '#f5fcff',
  },
  h1: {
    fontSize: 24,
    fontWeight: 'bold',
    marginBottom: 20,
  },
  p: {
    fontSize: 16,
    marginBottom: 10,
  },
  ul: {
    marginTop: 10,
    marginBottom: 20,
  },
  li: {
    fontSize: 16,
    marginLeft: 20,
  },
});

export default App;
```

## Constraints

### Compatibility

This document is verified based on the following versions：

1. RNOH：0.72.11; SDK：OpenHarmony(api11) 4.1.0.53; IDE：DevEco Studio 4.1.3.412; ROM：2.0.0.52;
2. RNOH：0.72.13; SDK：HarmonyOS NEXT Developer Preview1; IDE：DevEco Studio 4.1.3.500; ROM：2.0.0.58;
3. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;

## API

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

For details, see [parse5 Document address](https://parse5.js.org/index.html)

| Name                                           | Description                                                                   | Type     | Required | HarmonyOS Support |
| ---------------------------------------------- | ----------------------------------------------------------------------------- | -------- | -------- | ----------------- |
| parse(html, options?)                          | Parses an HTML string.                                                        | function | no       | yes               |
| parseFragment(fragmentContext, html, options?) | Parses an HTML fragment.                                                      | function | no       | yes               |
| serialize(node, options?)                      | Serializes an AST node to an HTML string.                                     | function | no       | yes               |
| serializeOuter(node, options?)                 | Serializes an AST element node to an HTML string, including the element node. | function | no       | yes               |

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/inikulin/parse5/blob/master/LICENSE).

<!-- {% endraw %} -->