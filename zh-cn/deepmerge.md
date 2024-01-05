> 模板版本：v0.1.2

<p align="center">
  <h1 align="center"> <code>deepmerge</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/TehShrike/deepmerge/blob/master/license.txt">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

>[!tip] [Github 地址](https://github.com/TehShrike/deepmerge)


## 安装与使用

进入到工程目录并输入以下命令：

#### **yarn**

```bash
yarn add deepmerge
```
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

### 兼容性

 在下述版本验证通过：

 1. IDE：DevEco Studio 4.1.3.412;SDK：OpenHarmony(api11) 4.1.0.53;测试设备：Mate40 Pro(NOH-AN00);ROM：2.0.0.52(SP22C00E52R1P17log);RNOH：0.72.11

## API

详情见 [deepmerge源库地址](https://github.com/TehShrike/deepmerge)

| 名称 | 说明 | 类型 | 是否必填 | 原库平台 | 鸿蒙支持 |
| ---- | ---- | ---- | -------- | -------- | -------- |
| deepmerge(x, y, [options]) | Merge two objects x and y deeply, returning a new merged object with the elements from both x and y. | function | No | / | Yes |
| deepmerge.all(arrayOfObjects, [options]) | Merges any number of objects into a single result object. | function | No | / | Yes |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/TehShrike/deepmerge/blob/master/license.txt) ，请自由地享受和参与开源。
