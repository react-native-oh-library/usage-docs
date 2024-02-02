> 模板版本：v0.1.3

<p align="center">
  <h1 align="center"> <code>htmlparser2</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/fb55/htmlparser2">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20windows%20|%20web|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/callstack/react-native-slider/blob/main/LICENSE.md">
        <img src="https://img.shields.io/npm/l/@react-native-community/slider.svg" alt="License" />
    </a>
</p>


> [!tip] [Github 地址](https://github.com/fb55/htmlparser2)

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->
#### **npm**

```bash
npm install htmlparser2@9.1.0
```

**yarn**

```bash
yarn add htmlparser2@9.1.0
```

<!-- tabs:end -->

快速使用：

```js
import * as htmlparser2 from "htmlparser2";

const parser = new htmlparser2.Parser({
    onopentag(name, attributes) {
        /*
         * This fires when a new tag is opened.
         *
         * If you don't need an aggregated `attributes` object,
         * have a look at the `onopentagname` and `onattribute` events.
         */
        if (name === "script" && attributes.type === "text/javascript") {
            console.log("JS! Hooray!");
        }
    },
    ontext(text) {
        /*
         * Fires whenever a section of text was processed.
         *
         * Note that this can fire at any point within text and you might
         * have to stitch together multiple pieces.
         */
        console.log("-->", text);
    },
    onclosetag(tagname) {
        /*
         * Fires when a tag is closed.
         *
         * You can rely on this event only firing when you have received an
         * equivalent opening tag before. Closing tags without corresponding
         * opening tags will be ignored.
         */
        if (tagname === "script") {
            console.log("That's it?!");
        }
    },
});
parser.write(
    "Xyz <script type='text/javascript'>const foo = '<<bar>>';</script>",
);
parser.end();
```

## 兼容性

在下述版本验证通过：

1. RNOH：0.72.11; SDK：OpenHarmony(api11) 4.1.0.53; IDE：DevEco Studio 4.1.3.412; ROM：2.0.0.52;
2. RNOH：0.72.13; SDK：HarmonyOS NEXT Developer Preview1; IDE：DevEco Studio 4.1.3.500; ROM：2.0.0.58;

## 生态系统

> | Name                                                         | Description                                             |
> | ------------------------------------------------------------ | ------------------------------------------------------- |
> | [htmlparser2](https://github.com/fb55/htmlparser2)           | Fast & forgiving HTML/XML parser                        |
> | [domhandler](https://github.com/fb55/domhandler)             | Handler for htmlparser2 that turns documents into a DOM |
> | [domutils](https://github.com/fb55/domutils)                 | Utilities for working with domhandler's DOM             |
> | [css-select](https://github.com/fb55/css-select)             | CSS selector engine, compatible with domhandler's DOM   |
> | [cheerio](https://github.com/cheeriojs/cheerio)              | The jQuery API for domhandler's DOM                     |
> | [dom-serializer](https://github.com/cheeriojs/dom-serializer) | Serializer for domhandler's DOM                         |

## 遗留问题

解析器错误地将（小于）识别为起始标签: [issue#1](https://github.com/fb55/htmlparser2/issues/1620)

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/fb55/htmlparser2/blob/master/LICENSE) ，请自由地享受和参与开源。
