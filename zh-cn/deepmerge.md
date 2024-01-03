> 模板版本：v0.0.1

<p align="center">
  <h1 align="center"> <code>deepmerge</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/TehShrike/deepmerge">
        <img src="https://img.shields.io/badge/platforms-android%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/TehShrike/deepmerge/blob/master/license.txt">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install deepmerge
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

```js
import deepmerge from 'deepmerge'

const x = {
	foo: { bar: 3 },
	array: [{
		does: 'work',
		too: [ 1, 2, 3 ]
	}]
}

const y = {
	foo: { baz: 4 },
	quux: 5,
	array: [{
		does: 'work',
		too: [ 4, 5, 6 ]
	}, {
		really: 'yes'
	}]
}

const output = {
	foo: {
		bar: 3,
		baz: 4
	},
	array: [{
		does: 'work',
		too: [ 1, 2, 3 ]
	}, {
		does: 'work',
		too: [ 4, 5, 6 ]
	}, {
		really: 'yes'
	}],
	quux: 5
}

deepmerge(x, y) // => output
```

## 约束与限制

## API

| 名称 | 说明 | 类型 | 是否必填 | 原库平台 | 鸿蒙支持 |
| ---- | ---- | ---- | -------- | -------- | -------- |
| deepmerge(x, y, [options]) | Merge two objects x and y deeply, returning a new merged object with the elements from both x and y. | function | No | All | Yes |
| deepmerge.all(arrayOfObjects, [options]) | Merges any number of objects into a single result object. | function | No | All | Yes |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/TehShrike/deepmerge/blob/master/license.txt) ，请自由地享受和参与开源。
