

> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>reassure</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/callstack/reassure">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20Windows%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/callstack/reassure/blob/main/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/callstack/reassure)

## 安装与使用

<!-- tabs:start -->

#### **npm**

```bash
npm install reassure@1.0.0
```

#### **yarn**

```bash
yarn add reassure@1.0.0
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

文件名称结尾必须包含`.perf-test.`，比如：MeasureFunction.perf-test.tsx

```js
import {measureFunction} from 'reassure';
import {test} from '@jest/globals';

function fib(n: number): number {
  if (n <= 1) {
    return n;
  }

  return fib(n - 1) + fib(n - 2);
}

test('MeasureFunction runs 10', async () => {
  await measureFunction(() => fib(20), {runs: 10});
});

test('MeasureFunction runs 20', async () => {
  await measureFunction(() => fib(30), {runs: 20});
});

test('MeasureFunction warmupRuns 10', async () => {
  await measureFunction(() => fib(30), {warmupRuns: 10});
});

test('MeasureFunction warmupRuns 20', async () => {
  await measureFunction(() => fib(30), {warmupRuns: 20});
});

test('MeasureFunction writeFile false', async () => {
  await measureFunction(() => fib(30), {writeFile: false});
});

test('MeasureFunction writeFile true', async () => {
  await measureFunction(() => fib(30), {writeFile: true});
});

```

## 基础配置

### 配置 jest.config.js

```js
/** @type {import('ts-jest').JestConfigWithTsJest} */
module.exports = {
  preset: 'react-native',
  setupFilesAfterEnv: ['./jest-setup.js'],
};
```

### 配置 jest-setup.js

```js
/* eslint-disable no-undef */
import {configure} from 'reassure';

configure({testingLibrary: 'react-native'});

```

### 安装 jest

如已安装 jest，可忽略

```shell
npm install --save-dev jest@29.2.1
```

###  安装 babel-jest

如已安装 babel-jest，可忽略

```shell
npm instal --save-dev babel-jest@29.2.1
```

### 安装 @testing-library/react-native

```shell
npm install --save-dev @testing-library/react-native@12.5.2
```

## 生成性能报告

```shell
npx reassure
```

性能报告默认在当前工程根目录的`.reassure`文件夹中

## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

1. RNOH：0.72.27; SDK：HarmonyOS NEXT Developer Beta1 5.0.0.25 (API Version 12 Canary4); IDE：DevEco Studio 5.0.3.400SP7; ROM：3.0.0.25;
2. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;

## API

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name            | Description                                                  | Type                                                         | Required | Platform | HarmonyOS Support |
| --------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | -------- | -------- | ----------------- |
| measureRenders  | rendering the passed screen inside a `React.Profiler` component, measuring its performance and writing results to the output file | async function measureRenders(<br/>  ui: React.ReactElement,<br/>  options?: MeasureRendersOptions,<br/>): Promise<MeasureResults> { | no       | all      | yes               |
| measureFunction | Allows you to wrap any synchronous function, measure its performance and write results to the output file | async function measureFunction(<br/>  fn: () => void,<br/>  options?: MeasureFunctionOptions,<br/>): Promise<MeasureResults> { | no       | all      | yes               |
| resetToDefaults | Reset current config to the original `defaultConfig` object  | Function                                                     | no       | all      | yes               |

**MeasureRendersOptions**

| Name       | Description                                                  | Type                                                | Required | Platform | HarmonyOS Support |
| ---------- | ------------------------------------------------------------ | --------------------------------------------------- | -------- | -------- | ----------------- |
| runs       | number of runs per series for the particular test            | number                                              | no       | all      | yes               |
| warmupRuns | number of additional warmup runs that will be done and discarded before the actual runs | number                                              | no       | all      | yes               |
| wrapper    | React component, such as a Provider, which the ui will be wrapped with | React.ComponentType<{children: React.ReactElement}> | no       | all      | yes               |
| scenario   | a custom async function, which defines user interaction within the ui by utilized RNTL functions | (screen: any) => Promise<any>                       | no       | all      | yes               |
| writeFile  | should write output to file                                  | boolean                                             | no       | all      | yes               |

**MeasureFunctionOptions**

| Name       | Description                                                  | Type    | Required | Platform | HarmonyOS Support |
| ---------- | ------------------------------------------------------------ | ------- | -------- | -------- | ----------------- |
| runs       | number of runs per series for the particular test            | number  | no       | all      | yes               |
| warmupRuns | number of additional warmup runs that will be done and discarded before the actual runs | number  | no       | all      | yes               |
| writeFile  | should write output to file                                  | boolean | no       | all      | yes               |

**configure**

| Name           | Description                                                  | Type           | Required | Platform | HarmonyOS Support |
| -------------- | ------------------------------------------------------------ | -------------- | -------- | -------- | ----------------- |
| runs           | number of runs per series for the particular test            | number         | no       | all      | yes               |
| warmupRuns     | number of additional warmup runs that will be done and discarded before the actual runs | number         | no       | all      | yes               |
| outputFile     | should write output to file                                  | boolean        | no       | all      | yes               |
| verbose | make Reassure log more, e.g. for debugging purposes | boolean | no | all | yes   |
| testingLibrary | where to look for `render` and `cleanup` functions           | TestingLibrary | no       | all      | yes               |

**dangerReassure**

| Name          | Description                | Type   | Required | Platform | HarmonyOS Support |
| ------------- | -------------------------- | ------ | -------- | -------- | ----------------- |
| inputFilePath | Enter the path to the file | number | no       | all      | yes               |
| debug         | Enable the debug mode.     | number | no       | all      | yes               |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/callstack/reassure/blob/main/LICENSE) ，请自由地享受和参与开源。
