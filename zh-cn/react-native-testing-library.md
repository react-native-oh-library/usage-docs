
> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-testing-library</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/callstack/react-native-testing-library">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20web%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/callstack/react-native-testing-library/blob/main/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/callstack/react-native-testing-library)


## 安装与使用

本库需要和测试运行器一起使用，本文档以Jest测试框架作为示例演示。

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install -D jest@29.7.0
npm install -D @testing-library/react-native@12.5.1
```

#### **yarn**

```bash
yarn add -D jest@29.7.0
yarn add -D @testing-library/react-native@12.5.1
```

<!-- tabs:end -->

配置Jest匹配器，目前有两种配置方法：

方法一：在jest-setup.ts中引入：

```js
import '@testing-library/react-native/extend-expect';
```

方法二：在jest.config.js中配置：

```json
{
  "preset": "react-native",
  "setupFilesAfterEnv": ["@testing-library/react-native/extend-expect"]
}
```

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import * as React from 'react';
import { Pressable, ScrollView, Text, TextInput, View } from 'react-native';
import { render, screen, userEvent } from '@testing-library/react-native';

type QuestionsBoardProps = {
  questions: string[];
  onSubmit: (obj: {}) => void;
};

jest.useFakeTimers();

function QuestionsBoard({ questions, onSubmit }: QuestionsBoardProps) {
  const [data, setData] = React.useState({});

  return (
    <ScrollView>
      {questions.map((q, index) => {
        return (
          <View key={q}>
            <Text>{q}</Text>
            <TextInput
              accessibilityLabel="answer input"
              accessibilityHint="input"
              onChangeText={(text) => {
                setData((state) => ({
                  ...state,
                  [index + 1]: { q, a: text },
                }));
              }}
            />
          </View>
        );
      })}
      <Pressable accessibilityRole={'button'} onPress={() => onSubmit(data)}>
        <Text>Submit</Text>
      </Pressable>
    </ScrollView>
  );
}

test('form submits two answers', async () => {
  const questions = ['q1', 'q2'];
  const onSubmit = jest.fn();

  const user = userEvent.setup();
  render(<QuestionsBoard questions={questions} onSubmit={onSubmit} />);

  const answerInputs = screen.getAllByLabelText('answer input');
  await user.type(answerInputs[0], 'a1');
  await user.type(answerInputs[1], 'a2');
  await user.press(screen.getByRole('button', { name: 'Submit' }));

  expect(onSubmit).toHaveBeenCalledWith({
    '1': { q: 'q1', a: 'a1' },
    '2': { q: 'q2', a: 'a2' },
  });
});
```
## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

1. RNOH: 0.72.27; SDK: HarmonyOS-Next-DB1 5.0.0.29(SP1); IDE: DevEco Studio 5.0.3.403; ROM: 3.0.0.25;
2. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;

## API

详细请查看 [react-native-testing-library 的文档介绍](https://callstack.github.io/react-native-testing-library/docs/api)

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| render  | render your UI components for testing purposes | function | yes | All | yes |
| screen | access rendered UI | object | no | All | yes |
| userEvent | simulate common user interactions like [`press`](https://callstack.github.io/react-native-testing-library/docs/api/events/user-event#press) or [`type`](https://callstack.github.io/react-native-testing-library/docs/user-event#type) in a realistic way | object | no | All | yes |
| fireEvent | simulate any component event in a simplified way | function | no | All | yes |
| renderHook | render hooks for testing purposes | function | no | All | yes |
| waitFor | Waits for a period of time for the `expectation` | function | no | All | yes |
| configure | configure | function | no | All | yes |
| resetToDefaults | reset to Defaults | function | no | All | yes |
| isHiddenFromAccessibility | Checks if given element is hidden from assistive technology, e.g. screen readers. | function | no | All | yes |
| within | performs [queries](https://callstack.github.io/react-native-testing-library/docs/api/queries) scoped to given element | function | no | All | yes |
| act | action | function | no | All | yes |
| cleanup | Unmounts React trees that were mounted with `render` and clears `screen` variable that holds latest `render` output. | function | no | All | yes |

 ### screen

> [!TIP] "\*"号表示省略了变体或者谓词部；查询接口由两部分组成：变体和谓词，它们之间由单词by分隔，例如: getBy\*是查询变体，\*ByRole是谓词；变体和谓词之间可以任意组合。


| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| getBy* | Exactly one matching element | function | no | All | yes |
| getAllBy* | At least one matching element | function | no | All | yes |
| queryBy* | Zero or one matching element | function | no | All | yes |
| queryAllBy* | No assertion | function | no | All | yes |
| findBy* | Exactly one matching element | function | no | All | yes |
| findAllBy* | At least one matching element | function | no | All | yes |
| *ByRole | Returns a `ReactTestInstance` with matching `role` or `accessibilityRole` prop. | function | no | All | yes |
| *ByLabelText | Returns a `ReactTestInstance` with matching label | function | no | All | yes |
| *ByPlaceholderText | Returns a `ReactTestInstance` for a `TextInput` with a matching placeholder – may be a string or regular expression | function | no | All | yes |
| *ByDisplayValue | Returns a `ReactTestInstance` for a `TextInput` with a matching display value – may be a string or regular expression | function | no | All | yes |
| *ByText | Returns a `ReactTestInstance` with matching text – may be a string or regular expression | function | no | All | yes |
| *ByHintText | Returns a `ReactTestInstance` with matching `accessibilityHint` prop | function | no | All | yes |
| *ByTestId | Returns a `ReactTestInstance` with matching `testID` prop. `testID` – may be a string or a regular expression | function | no | All | yes |
| rerender | Re-render the in-memory tree with a new root element | function | no | All | yes |
| unmount | Unmount the in-memory tree, triggering the appropriate lifecycle events | function | no | All | yes |
| debug | Pretty prints deeply rendered component passed to `render` | function | no | All | yes |
| toJSON | Get the rendered component JSON representation, e.g. for snapshot testing | function | no | All | yes |
| root | Returns the rendered root [host element](https://callstack.github.io/react-native-testing-library/docs/advanced/testing-env#host-and-composite-components) | object | no | All | yes |


### userEvent

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| setup | Creates a User Event object instance, which can be used to trigger events. | function | no | All | yes |
| press | This helper simulates a press on any pressable element | function | no | All | yes |
| longPress | Simulates a long press user interaction. | function | no | All | yes |
| type | This helper simulates the user focusing on a `TextInput` element | function | no | All | yes |
| clear | This helper simulates the user clearing the content of a `TextInput` element | function | no | All | yes |
| scrollTo | This helper simulates the user scrolling a host `ScrollView` element | function | no | All | yes |

### Jest matchers

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| toBeOnTheScreen | This allows you to assert whether an element is attached to the element tree or not. If you hold a reference to an element and it gets unmounted during the test it will no longer pass this assertion. | function | no | All | yes |
| toHaveTextContent | This allows you to assert whether the given element has the given text content or not. It accepts either `string` or `RegExp` matchers, as well as [text match options](https://callstack.github.io/react-native-testing-library/docs/api/queries#text-match-options) of `exact` and `normalizer` | function | no | All | yes |
| toContainElement | This allows you to assert whether the given container element does contain another host element. | function | no | All | yes |
| toBeEmptyElement | This allows you to assert whether the given element does not have any host child elements or text content | function | no | All | yes |
| toHaveDisplayValue | This allows you to assert whether the given `TextInput` element has a specified display value. It accepts either `string` or `RegExp` matchers, as well as [text match options](https://callstack.github.io/react-native-testing-library/docs/api/queries#text-match-options) of `exact` and `normalizer` | function | no | All | yes |
| toHaveAccessibilityValue | This allows you to assert whether the given element has a specified accessible value | function | no | All | yes |
| toBeEnabled | These allow you to assert whether the given element is enabled or disabled from the user's perspective. It relies on the accessibility disabled state as set by `aria-disabled` or `accessibilityState.disabled` props. It will consider a given element disabled when it or any of its ancestors is disabled. | function | no | All | yes |
| toBeSelected | This allows you to assert whether the given element is selected from the user's perspective. It relies on the accessibility selected state as set by `aria-selected` or accessibilityState.selected props | function | no | All | yes |
| toBeChecked | These allow you to assert whether the given element is checked or partially checked from the user's perspective. It relies on the accessibility checked state as set by `aria-checked` or `accessibilityState.checked` props | function | no | All | yes |
| toBeExpanded | These allows you to assert whether the given element is expanded or collapsed from the user's perspective. It relies on the accessibility disabled state as set by `aria-expanded` or `accessibilityState.expanded` props | function | no | All | yes |
| toBeBusy | This allows you to assert whether the given element is busy from the user's perspective. It relies on the accessibility selected state as set by `aria-busy` or `accessibilityState.busy` props. | function | no | All | yes |
| toHaveStyle | This allows you to assert whether the given element has given styles | function | no | All | yes |
| toHaveAccessibleName | This allows you to assert whether the given element has a specified accessible name. It accepts either `string` or `RegExp` matchers, as well as [text match options](https://callstack.github.io/react-native-testing-library/docs/api/queries#text-match-options) of `exact` and normalizer | function | no | All | yes |
| toHaveProp | This allows you to assert whether the given element has a given prop. When the `value` parameter is `undefined` it will only check for existence of the prop, and when `value` is defined it will check if the actual value matches passed value. | function | no | All | yes |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/callstack/react-native-testing-library/blob/main/LICENSE) ，请自由地享受和参与开源。