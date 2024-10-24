> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>htmlparser2</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/fb55/htmlparser2">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20windows%20|%20web|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/fb55/htmlparser2/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/fb55/htmlparser2)

## Installation and Usage

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

#### **npm**

```bash
npm install htmlparser2@9.1.0
// 以下为配合htmlparser2使用的相关库，可视业务情况进行安装
npm install circular-json@0.5.9
```

#### **yarn**

```bash
yarn add htmlparser2@9.1.0
// 以下为配合htmlparser2使用的相关库，可视业务情况进行安装
yarn add circular-json@0.5.9
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React, { useEffect, useState } from 'react';
import * as htmlparser2 from 'htmlparser2';
import { View, Text } from 'react-native';

// Use htmlparser2 to parse HTML text
function HtmlParser() {
    const [parsedContent, setParsedContent] = useState('');

    useEffect(() => {
        const parser = new htmlparser2.Parser({
            onopentag(name, attributes) {
                if (name === 'script' && attributes.type === 'text/javascript') {
                    console.log('JS! Hooray!');
                    setParsedContent(parsedContent => parsedContent + 'JS! Hooray!')
                }
            },
            ontext(text) {
                console.log('-->', text);
                setParsedContent(parsedContent => parsedContent + text);
            },
            onclosetag(tagname) {
                if (tagname === 'script') {
                    console.log("That's it?!");
                    setParsedContent(parsedContent => parsedContent + "That's it?!");

                }
            },
        });

        parser.write("Xyz <script type='text/javascript'>const foo = '111<<bar>>';</script>");
        parser.end();
    }, []);

    return (
        <View>
            <Text style={{ color: 'white' }}>{parsedContent}</Text>
        </View>
    );
}

export default HtmlParser; 
```

上述案例使用htmlparser2来解析HTML文本
下面的案例使用parseDocument，将html解析为DOM树

```js

import { parseDocument } from "htmlparser2";
import CircularJSON from "circular-json";
import { View, Text } from 'react-native';

// html to DOM
function HtmlParser() {
    const dom = parseDocument(
        '<div data-foo="In the end, it doesn\'t really matter."></div><div data-foo="Indeed-that\'s a delicate matter.">',
    );
    return (
        <View>
            <Text style={{ color: 'white' }}>{CircularJSON.stringify(dom)}</Text>
        </View>
    );
}
export default HtmlParser; 
```

## Constraints

### Compatibility

This document is verified based on the following versions:

1. RNOH：0.72.11; SDK：OpenHarmony(api11) 4.1.0.53; IDE：DevEco Studio 4.1.3.412; ROM：2.0.0.52;
2. RNOH：0.72.13; SDK：HarmonyOS NEXT Developer Preview1; IDE：DevEco Studio 4.1.3.500; ROM：2.0.0.58;
3. RNOH：0.72.27; SDK：HarmonyOS-Next-DB1 5.0.0.29(SP1); IDE：DevEco Studio 5.0.3.400; ROM：3.0.0.25;
4. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;

## Static Methods

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                 | Description       | Type     | Required | Platform    | HarmonyOS Support |
|----------------------|-------------------|----------|----------|-------------|-------------------|
| parseDocument        | 解析DOM树            | function | no       | ios,android | yes               |
| createDocumentStream | 创建一个可读流           | function | no       | ios,android | yes               |
| parseFeed            | 解析RSS 或 Atom feed | function | no       | ios,android | yes               |

## Known Issues

- [ ] 解析器错误地将（小于）识别为起始标签问题: [issue#1](https://github.com/fb55/htmlparser2/issues/1620)

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/fb55/htmlparser2/blob/master/LICENSE).
