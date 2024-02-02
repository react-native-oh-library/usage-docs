> 模板版本：v0.1.3

<p align="center">
  <h1 align="center"> <code>js-beautify</code> </h1>
</p>
<p align="center">
        <a href="https://github.com/beautifier/js-beautify/blob/main/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>


> [!tip] [Github 地址](https://github.com/beautifier/js-beautify)

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install js-beautify@^1.14.9
```

#### **yarn**

```bash
yarn add js-beautify@^1.14.9
```

<!-- tabs:end -->

快速使用：

```typescript
import React from 'react';
import { View, Text } from 'react-native';
import { js_beautify, html_beautify, css_beautify } from 'js-beautify';

const options = { "indent_size": 2, "space_in_empty_paren": true }
const dataObj = {completed: false,id: 1,title: "delectus aut autem",userId: 1,}
const dataJson = JSON.stringify(dataObj)
js_beautify(dataJson, options)
/* OUTPUT
{
  "completed": false,
  "id": 1,
  "title": "delectus aut autem",
  "userId": 1,
}
*/

const data ='<html><head></head><body><p>Hello</p><p>World!</p><p>More content!</p></body></html>';
const options = {
  "indent_size": 4, 
  "indent_char": ' ',
  "max_preserve_newlines": 2, 
  "preserve_newlines": true 
}
html_beautify(data,options);

const data = 'header{background-color: #333;color: #fff;padding: 10px 0;text-align: center;}';
const option = {
  "indent_size": 4,
  "indent_char": ' '
}
css_beautify(data,options)

```

## 约束与限制

#### 兼容性

在下述版本验证通过：

1. RNOH：0.72.11; SDK：OpenHarmony(api11) 4.1.0.53; IDE：DevEco Studio 4.1.3.412; ROM：2.0.0.52;
2. RNOH：0.72.13; SDK：HarmonyOS NEXT Developer Preview1; IDE：DevEco Studio 4.1.3.500; ROM：2.0.0.58;
 
## API列表

#### js_beautify

 **方法**

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该方法；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name        | Description  | Type     | Required | HarmonyOS Support |
| ----------- | ------------ | -------- | -------- | ----------------- |
| js_beautify | 格式化js代码 | function | no       | partially         |

**可选参数(options)**

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                       | Description                                                  | Type    | Required | HarmonyOS Support | note                  |
| -------------------------- | ------------------------------------------------------------ | ------- | -------- | ----------------- | --------------------- |
| indent_size                | 一个缩进级别的空格数,默认值4。                               | number  | no       | yes               |                       |
| indent_char                | 用于缩进的字符，默认值‘ ’（一个空格）。                      | string  | no       | yes               |                       |
| indent_with_tabs           | 使用制表符(tab)进行缩进，默认值false。                       | boolean | no       | yes               |                       |
| eol                        | 结束行的字符,默认值“\n”。                                    | string  | no       | yes               |                       |
| end_with_newline           | 以新行结束输出，默认值false。                                | boolean | no       | yes               |                       |
| indent_level               | 每行前的初始缩进级别,默认值0。                               | number  | no       | yes               |                       |
| preserve_newlines          | 保留数组/对象项间的新行，默认 true。                         | boolean | no       | yes               |                       |
| max_preserve_newlines      | 保留连续新行的最大数量，默认值10。                           | number  | no       | yes               |                       |
| space_in_paren             | 在括号内加上空格，默认值false。                              | boolean | no       | yes               |                       |
| space_in_empty_paren       | 在空的括号加上空格，默认值false。                            | boolean | no       | yes               | 与Android一致均无效果 |
| jslint_happy               | 对jslint严格模式进行优化,默认值false。                       | boolean | no       | yes               |                       |
| space_after_anon_function  | 在函数关键字（如function或=>）后面加空格，默认值false。      | boolean | no       | yes               |                       |
| space-after-named-function | 在命名函数的括号前添加一个空格，默认值false。                | boolean | no       | yes               |                       |
| brace_style                | 设置括号样式，默认值"collapse"。                             | array   | no       | yes               |                       |
| unindent-chained-methods   | 不缩进链式调用的方法,默认值false。                           | boolean | no       | yes               |                       |
| break-chained-methods      | 在链式调用的方法之间插入换行符，默认值false。                | boolean | no       | yes               |                       |
| keep_array_indentation     | 保持数组元素原来的缩进格式，默认值false。                    | boolean | no       | yes               |                       |
| wrap_line_length           | 每行的最大字符数，默认值0。                                  | number  | no       | yes               | 与Android一致均无效果 |
| e4x                        | 忽略XML元素，默认值false。                                   | boolean | no       | yes               |                       |
| comma_first                | 将逗号置于行首，默认值false。                                | boolean | no       | yes               |                       |
| operator_position          | 在打破行时，运算符放在新行的哪一侧，默认值"before-newline"。 | array   | no       | yes               |                       |
| indent-empty-lines         | 保留空行上的缩进,默认值false                                 | boolean | no       | yes               |                       |
| templating                 | 模板语言列表，默认值["auto"]                                 | array   | no       | yes               |                       |

#### css_beautify

**方法**

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该方法；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name         | Description   | Type     | Required | HarmonyOS Support |
| ------------ | ------------- | -------- | -------- | ----------------- |
| css_beautify | 格式化css代码 | function | no       | yes               |

**可选参数(options)**

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                       | Description                             | Type    | Required | HarmonyOS Support |
| -------------------------- | --------------------------------------- | ------- | -------- | ----------------- |
| indent_size                | 一个缩进级别的空格数,默认值4。          | number  | no       | yes               |
| indent_char                | 用于缩进的字符，默认值‘ ’（一个空格）。 | string  | no       | yes               |
| indent_with_tabs           | 使用制表符(tab)进行缩进，默认值false。  | boolean | no       | yes               |
| eol                        | 结束行的字符,默认值“\n”。               | string  | no       | yes               |
| end_with_newline           | 以新行结束输出，默认值false。           | boolean | no       | yes               |
| brace_style                | 设置括号样式，默认值"collapse"。        | array   | no       | yes               |
| selector-separator-newline | 在多个选择器之间添加换行符，默认值false | boolean | no       | yes               |
| newline-between-rules      | 在CSS规则之间添加换行符，默认值true     | boolean | no       | yes               |

#### html_beautify

**方法**

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该方法；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name          | Description    | Type     | Required | HarmonyOS Support |
| ------------- | -------------- | -------- | -------- | ----------------- |
| html_beautify | 格式化html代码 | function | no       | yes               |

**可选参数(options)**

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                        | Description                                           | Type    | Required | HarmonyOS Support |                       |
| --------------------------- | ----------------------------------------------------- | ------- | -------- | ----------------- | --------------------- |
| indent_size                 | 一个缩进级别的空格数,默认值4。                        | number  | no       | yes               |                       |
| indent_char                 | 用于缩进的字符，默认值‘ ’（一个空格）。               | string  | no       | yes               |                       |
| indent_with_tabs            | 使用制表符(tab)进行缩进，默认值false。                | boolean | no       | yes               |                       |
| eol                         | 结束行的字符,默认值“\n”。                             | string  | no       | yes               |                       |
| end_with_newline            | 以新行结束输出，默认值false。                         | boolean | no       | yes               |                       |
| indent-inner-html           | 缩进<head>和<body>部分。                              | boolean | no       | yes               |                       |
| preserve_newlines           | 保留数组/对象项间的新行，默认 true。                  | boolean | no       | yes               |                       |
| max_preserve_newlines       | 保留连续新行的最大数量，默认值10。                    | number  | no       | yes               |                       |
| brace_style                 | 设置括号样式，默认值"collapse"。                      | array   | no       | yes               |                       |
| indent_scripts              | 设置script 标签内的内容应的缩进格式，默认值“normal”。 | array   | no       | yes               |                       |
| wrap-line-length            | 每行的最大字符数,默认值250。                          | number  | no       | yes               | 与Android一致均无效果 |
| wrap_attributes             | 将属性换到新行,默认值"auto"。                         | array   | no       | yes               |                       |
| wrap_attributes_min_attrs   | 标签的属性的个数达到该值，每个属性都会换行，默认值2。 | number  | no       | yes               |                       |
| wrap-attributes-indent-size | 设置属性换行缩进大小，默认值4。                       | number  | no       | yes               |                       |
| Inline                      | 指定某个元素为内联元素，内联元素不会换行。            | array   | no       | yes               | 与Android一致均无效果 |
| inline_custom_elements      | 设置自定义组件为内联元素，默认值true。                | boolean | no       | yes               | 与Android一致均无效果 |
| unformatted                 | 不被重新格式化的标签,默认值内联元素。                 | array   | no       | yes               | 与Android一致均无效果 |
| content_unformatted         | 指定某些标签的内容不被重新格式化,默认值”pre”          | array   | no       | yes               |                       |
| extra_liners                | 设置某些标签前面有换行,默认值[ head,body,/html]       | array   | no       | yes               |                       |

## 遗留问题

## 其他

## 开源协议

本项目基于 [MIT License](https://github.com/beautifier/js-beautify/blob/main/LICENSE) ，请自由地享受和参与开源。

