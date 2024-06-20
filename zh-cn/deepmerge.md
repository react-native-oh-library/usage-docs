<!-- {% raw %} -->
> 模板版本：v0.1.3

<p align="center">
  <h1 align="center"> <code>deepmerge</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/TehShrike/deepmerge/blob/master/license.txt">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!tip] [Github 地址](https://github.com/TehShrike/deepmerge)

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install deepmerge@^4.3.1
```

#### **yarn**

```bash
yarn add deepmerge@^4.3.1
```

<!-- tabs:end -->

快速使用：

```js
import deepmerge from "deepmerge";

const x = {
  foo: { bar: 3 },
  array: [
    {
      does: "work",
      too: [1, 2, 3],
    },
  ],
};

const y = {
  foo: { baz: 4 },
  quux: 5,
  array: [
    {
      does: "work",
      too: [4, 5, 6],
    },
    {
      really: "yes",
    },
  ],
};

const output = {
  foo: {
    bar: 3,
    baz: 4,
  },
  array: [
    {
      does: "work",
      too: [1, 2, 3],
    },
    {
      does: "work",
      too: [4, 5, 6],
    },
    {
      really: "yes",
    },
  ],
  quux: 5,
};

deepmerge(x, y); // => output
```

## 约束与限制

### 兼容性

在下述版本验证通过：

1. RNOH：0.72.11; SDK：OpenHarmony(api11) 4.1.0.53; IDE：DevEco Studio 4.1.3.412; ROM：2.0.0.52;
2. RNOH：0.72.13; SDK：HarmonyOS NEXT Developer Preview1; IDE：DevEco Studio 4.1.3.500; ROM：2.0.0.58;

## API

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

详情见 [deepmerge源库地址](https://github.com/TehShrike/deepmerge)

| Name                                     | Description                                                                                          | Type     | Required | HarmonyOS Support |
| ---------------------------------------- | ---------------------------------------------------------------------------------------------------- | -------- | -------- | ----------------- |
| deepmerge(x, y, [options])               | Merge two objects x and y deeply, returning a new merged object with the elements from both x and y. | function | no       | yes               |
| deepmerge.all(arrayOfObjects, [options]) | Merges any number of objects into a single result object.                                            | function | no       | yes               |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/TehShrike/deepmerge/blob/master/license.txt) ，请自由地享受和参与开源。

<!-- {% endraw %} -->