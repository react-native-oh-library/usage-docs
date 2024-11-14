> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-modal</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/react-native-modal/react-native-modal">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/react-native-modal/react-native-modal/blob/master/LICENSE.md">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-modal)

## 安装与使用

Find the matching version information in the release address of a third-party library：[@react-native-oh-tpl/react-native-modal Releases](https://github.com/react-native-oh-library/react-native-modal/releases).For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

进入到工程目录并输入以下命令：


<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-modal
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-modal
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```ts
import React, { Component } from "react";
import { Button, StyleSheet, Text, View } from "react-native";
import Modal from "react-native-modal";

type Props = {
	onPress: () => any;
};
type State<P> = P & {
	visible: boolean;
};

const DefaultModalContent: React.FC<Props> = (props) => (
	<View style={styles.content}>
		<Text style={styles.contentTitle}>Hi 👋!</Text>
		<Button testID={"close-button"} onPress={props.onPress} title="Close" />
	</View>
);

abstract class ModalBaseScene<P extends object = {}> extends Component<any, State<P>> {
	abstract renderModal(): React.ReactElement<any>;
	// @ts-ignore
	constructor(props, state?: P) {
		super(props);
		// @ts-ignore
		this.state = {
			...state,
			visible: false
		};
	}

	open = () => this.setState({ visible: true } as any);
	close = () => this.setState({ visible: false } as any);
	isVisible = () => this.state.visible;
	public renderButton(): React.ReactElement<any> {
		return <Button testID={"modal-open-button"} onPress={this.open} title="Open" />;
	}
	render() {
		return (
			<View style={styles.view}>
				{this.renderButton()}
				{this.renderModal()}
			</View>
		);
	}
}

class DefaultModal extends ModalBaseScene {
	renderModal(): React.ReactElement<any> {
		return (
			<Modal testID={"modal"} isVisible={this.isVisible()}>
				<DefaultModalContent onPress={this.close} />
			</Modal>
		);
	}
}

const styles = StyleSheet.create({
	view: {
		flex: 1,
		alignItems: "center",
		justifyContent: "center"
	},
	content: {
		backgroundColor: "white",
		padding: 22,
		justifyContent: "center",
		alignItems: "center",
		borderRadius: 4,
		borderColor: "rgba(0, 0, 0, 0.1)"
	},
	contentTitle: {
		fontSize: 20,
		marginBottom: 12
	}
});

export default DefaultModal;
```

## 约束与限制

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-native-modal Releases](https://github.com/react-native-oh-library/react-native-modal/releases)

## 属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name | Description | Type | Default | Required | Platform | HarmonyOS Support |
| --- | --- | --- | --- | --- | --- | --- |
| animationIn | Modal show animation | `string` or `object` | "slideInUp" | no | all | yes |
| animationInTiming | Timing for the modal show animation (in ms) | `number` | 300 | no | all | yes |
| animationOut | Modal hide animation | `string` or `object` | "slideOutDown" | no | all | yes |
| animationOutTiming | Timing for the modal hide animation (in ms) | `number` | 300 | no | all | yes |
| avoidKeyboard | Move the modal up if the keyboard is open | `bool` | false | no | all | yes |
| coverScreen | Will use RN `Modal` component to cover the entire screen wherever the modal is mounted in the component hierarchy | `bool` | true | no | all | yes |
| hasBackdrop | Render the backdrop | `bool` | true | no | all | yes |
| backdropColor | The backdrop background color | `string` | "black" | no | all | yes |
| backdropOpacity | The backdrop opacity when the modal is visible | `number` | 0.70 | no | all | yes |
| backdropTransitionInTiming | The backdrop show timing (in ms) | `number` | 300 | no | all | yes |
| backdropTransitionOutTiming | The backdrop hide timing (in ms) | `number` | 300 | no | all | yes |
| customBackdrop | The custom backdrop element | `node` | null | no | all | yes |
| children | The modal content | `node` | **REQUIRED** | yes | all | yes |
| deviceHeight | Device height (useful on devices that can hide the navigation bar) | `bool` | null | no | all | yes |
| deviceWidth | Device width (useful on devices that can hide the navigation bar) | `bool` | null | no | all | yes |
| isVisible | Show the modal? | `bool` | **REQUIRED** | yes | all | yes |
| onBackButtonPress | Called when the Android back button is pressed | `func` | () => null | no | Android | yes |
| onBackdropPress | Called when the backdrop is pressed | `func` | () => null | no | all | yes |
| onModalWillHide | Called before the modal hide animation begins | `func` | () => null | no | all | yes |
| onModalHide | Called when the modal is completely hidden | `func` | () => null | no | all | yes |
| onModalWillShow | Called before the modal show animation begins | `func` | () => null | no | all | yes |
| onModalShow | Called when the modal is completely visible | `func` | () => null | no | all | yes |
| onSwipeStart | Called when the swipe action started | `func` | () => null | no | all | yes |
| onSwipeMove | Called on each swipe event | `func` | (percentageShown) => null | no | all | yes |
| onSwipeComplete | Called when the `swipeThreshold` has been reached | `func` | ({ swipingDirection }) => null | no | all | yes |
| onSwipeCancel | Called when the `swipeThreshold` has not been reached | `func` | () => null | no | all | yes |
| panResponderThreshold | The threshold for when the panResponder should pick up swipe events | `number` | 4 | no | all | yes |
| scrollOffset | When > 0, disables swipe-to-close, in order to implement scrollable content | `number` | 0 | no | all | yes |
| scrollOffsetMax | Used to implement overscroll feel when content is scrollable. See `/example` directory | `number` | 0 | no | all | yes |
| scrollTo | Used to implement scrollable modal. See `/example` directory for reference on how to use it | `func` | null | no | all | yes |
| scrollHorizontal | Set to true if your scrollView is horizontal (for a correct scroll handling) | `bool` | false | no | all | yes |
| swipeThreshold | Swiping threshold that when reached calls `onSwipeComplete` | `number` | 100 | no | all | yes |
| swipeDirection | Defines the direction where the modal can be swiped. Can be 'up', 'down', 'left, or 'right', or a combination of them like `['up','down']` | `string` or `array` | null | no | all | yes |
| useNativeDriver | Defines if animations should use native driver | `bool` | false | no | all | yes |
| useNativeDriverForBackdrop | Defines if animations for backdrop should use native driver (to avoid flashing on android) | `bool` | null | no | all | yes |
| hideModalContentWhileAnimating | Enhances the performance by hiding the modal content until the animations complete | `bool` | false | no | all | yes |
| propagateSwipe | Allows swipe events to propagate to children components (eg a ScrollView inside a modal) | `bool` or `func` | false | no | all | yes |
| style | Style applied to the modal | `any` | null | no | all | yes |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/react-native-modal/react-native-modal/blob/master/LICENSE.md) ，请自由地享受和参与开源。

