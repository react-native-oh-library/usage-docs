> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-gifted-chat</code> </h1>
</p>
<p align="center">
   <a href="https://github.com/FaridSafi/react-native-gifted-chat">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
   <a href="https://github.com/FaridSafi/react-native-gifted-chat/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-blue.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/FaridSafi/react-native-gifted-chat)

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->


#### **npm**

```bash
npm install react-native-gifted-chat@2.4.0
```

#### **yarn**

```bash
yarn add react-native-gifted-chat@2.4.0
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

```tsx
import React, { useState } from 'react'
import { View } from 'react-native'

import { GiftedChat, IMessage } from 'react-native-gifted-chat'

export function App() {
  const [messages, setMessages] = useState([
    {
      _id: 1,
      text: 'My message111',
      createdAt: new Date(Date.UTC(2016, 5, 11, 17, 20, 0)),
      user: {
        _id: 2,
        name: 'React Native',
        avatar: 'https://facebook.github.io/react/img/logo_og.png',
      },
      quickReplies: {
        type: 'radio', // or 'checkbox',
        keepIt: true,
        values: [
          {
            title: '😋 Yes',
            value: 'yes',
          },
          {
            title: '📷 Yes, let me show you with a picture!',
            value: 'yes_picture',
          },
          {
            title: '😞 Nope. What?',
            value: 'no',
          },
        ],
      },
    },
  ])

  const onSend = (newMsg: IMessage[]) => setMessages([...messages, ...newMsg])

  return (
    <View style={{ flex: 1}}>
      <GiftedChat
        messages={messages}
        onSend={onSend}
        user={{_id: 1, name: 'Developer'}}
        messagesContainerStyle={{ flex: 1 }}
        isKeyboardInternallyHandled={false}
      />
    </View>
  )
}
```
## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

RNOH: 0.72.27; SDK: HarmonyOS-Next-DB1 5.0.0.29(SP1); IDE: DevEco Studio 5.0.3.403; ROM: 3.0.0.25;

## 属性

>[!TIP] "Platform"列表示该属性在原三方库上支持的平台。

>[!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

|              Name               |                         Description                          |      Type       | Required |  Platform   | HarmonyOS Support |
| :-----------------------------: | :----------------------------------------------------------: | :-------------: | :------: | :---------: | :---------------: |
|     **messageContainerRef**     |                    *Ref to the flatlist*                     | *FlatList ref*  |    No    | iOS/Android |        Yes        |
|        **textInputRef**         |                    Text field error text                     | *TextInput ref* |    No    | iOS/Android |        Yes        |
|          **messages**           |                     Messages to display                      |     *Array*     |    No    | iOS/Android |        Yes        |
|          **isTyping**           | Typing Indicator state; If you use`renderFooter` it will override this |     Boolean     |    No    | iOS/Android |        Yes        |
|            **text**             |                          Input text                          |     String      |    No    | iOS/Android |        Yes        |
|         **placeholder**         | Placeholder when `text` is empty; default is `'Type a message...'` |     String      |    No    | iOS/Android |        Yes        |
|     **messageIdGenerator**      |     Generate an id for new messages. Defaults to UUID v4     |   *Function*    |    No    | iOS/Android |        Yes        |
|            **user**             |                  User sending the messages                   |    *Object*     |    No    | iOS/Android |        Yes        |
|           **onSend**            |               Callback when sending a message                |   *Function*    |    No    | iOS/Android |        Yes        |
|       **alwaysShowSend**        |        Always show send button in input text composer        |     Boolean     |    No    | iOS/Android |        Yes        |
|           **locale**            | Locale to localize the dates. You need first to import the locale you need (ie. `require('dayjs/locale/de')` or `import 'dayjs/locale/fr'`) |    *String*     |    No    | iOS/Android |        Yes        |
|         **timeFormat**          | *(String)* - Format to use for rendering times; default is `'LT'` (see [Day.js Format](https://day.js.org/docs/en/display/format)) |    *String*     |    No    | iOS/Android |        Yes        |
|         **dateFormat**          | Format to use for rendering dates; default is `'ll'` (see [Day.js Format](https://day.js.org/docs/en/display/format)) |    *String*     |    No    | iOS/Android |        Yes        |
|         **loadEarlier**         | Enables the "load earlier messages" button, required for `infiniteScroll` |     Boolean     |    No    | iOS/Android |        Yes        |
| **isKeyboardInternallyHandled** | Determine whether to handle keyboard awareness inside the plugin. If you have your own keyboard handling outside the plugin set this to false; default is `true` |     Boolean     |    No    | iOS/Android |        Yes        |
|        **onLoadEarlier**        |            Callback when loading earlier messages            |   *Function*    |    No    | iOS/Android |        Yes        |
|      **isLoadingEarlier**       | Display an `ActivityIndicator` when loading earlier messages |     Boolean     |    No    | iOS/Android |        Yes        |
|        **renderLoading**        |           Render a loading view when initializing            |   *Function*    |    No    | iOS/Android |        Yes        |
|      **renderLoadEarlier**      |            Custom "Load earlier messages" button             |   *Function*    |    No    | iOS/Android |        Yes        |
|        **renderAvatar**         | Custom message avatar; set to `null` to not render any avatar for the message |   *Function*    |    No    | iOS/Android |        Yes        |
|       **showUserAvatar**        | Whether to render an avatar for the current user; default is `false`, only show avatars for other users |     Boolean     |    No    | iOS/Android |        Yes        |
|  **showAvatarForEveryMessage**  | avatars will only be displayed when a consecutive message is from the same user on the same day; |     Boolean     |    No    | iOS/Android |        Yes        |
|        **onPressAvatar**        |           Callback when a message avatar is tapped           |   *Function*    |    No    | iOS/Android |        Yes        |
|      **onLongPressAvatar**      |        Callback when a message avatar is long-pressed        |   *Function*    |    No    | iOS/Android |        Yes        |
|      **renderAvatarOnTop**      | Render the message avatar at the top of consecutive messages |     Boolean     |    No    | iOS/Android |        Yes        |
|        **renderBubble**         |                    Custom message bubble                     |   *Function*    |    No    | iOS/Android |        Yes        |
|         **renderTicks**         |       Custom ticks indicator to display message status       |    Function     |    No    | iOS/Android |        Yes        |
|     **renderSystemMessage**     |                    Custom system message                     |    Function     |    No    | iOS/Android |        Yes        |
|           **onPress**           |          Callback when a message bubble is pressed           |    Function     |    No    | iOS/Android |        Yes        |
|         **onLongPress**         | Callback when a message bubble is long-pressed; default is to show an ActionSheet with "Copy Text" (see [example using `showActionSheetWithOptions()`](https://github.com/FaridSafi/react-native-gifted-chat/blob/master@{2017-09-25}/src/Bubble.js#L96-L119)) |    Function     |    No    | iOS/Android |        Yes        |
|          **inverted**           |             Reverses display order of `messages`             |     Boolean     |    No    | iOS/Android |        Yes        |
|   **renderUsernameOnMessage**   | ndicate whether to show the user's username inside the message bubble |     Boolean     |    No    | iOS/Android |        Yes        |
|       **renderUsername**        |                  Custom Username container                   |   *Function*    |    No    | iOS/Android |        Yes        |
|        **renderMessage**        |                   Custom message container                   |   *Function*    |    No    | iOS/Android |        Yes        |
|      **renderMessageText**      |                     Custom message text                      |   *Function*    |    No    | iOS/Android |        Yes        |
|     **renderMessageImage**      |                     Custom message image                     |   *Function*    |    No    | iOS/Android |        Yes        |
|     **renderMessageVideo**      |                     Custom message video                     |   *Function*    |    No    | iOS/Android |        Yes        |
|         **imageProps**          | Extra props to be passed to the [``](https://facebook.github.io/react-native/docs/image.html) component created by the default `renderMessageImage` |    *Object*     |    No    | iOS/Android |        Yes        |
|         **videoProps**          | Extra props to be passed to the video component created by the required `renderMessageVideo` |    *Object*     |    No    | iOS/Android |        Yes        |
|        **lightboxProps**        | Extra props to be passed to the `MessageImage`'s [Lightbox](https://github.com/oblador/react-native-lightbox) |    *Object*     |    No    | iOS/Android |        Yes        |
|     **isCustomViewBottom**      | Determine whether renderCustomView is displayed before or after the text, image and video views |     Boolean     |    No    | iOS/Android |        Yes        |
|      **renderCustomView**       |                Custom view inside the bubble                 |   *Function*    |    No    | iOS/Android |        Yes        |
|          **renderDay**          |                  Custom day above a message                  |   *Function*    |    No    | iOS/Android |        Yes        |
|         **renderTime**          |                 Custom time inside a message                 |   *Function*    |    No    | iOS/Android |        Yes        |
|        **renderFooter**         | Custom footer component on the ListView, e.g. `'User is typing...'`; see [App.tsx](https://github.com/FaridSafi/react-native-gifted-chat/blob/master/example/App.tsx) for an example. Overrides default typing indicator that triggers when `isTyping` is true |   *Function*    |    No    | iOS/Android |        Yes        |
|       **renderChatEmpty**       | Custom component to render in the ListView when messages are empty |   *Function*    |    No    | iOS/Android |        Yes        |
|      **renderChatFooter**       | Custom component to render below the MessageContainer (separate from the ListView) |   *Function*    |    No    | iOS/Android |        Yes        |
|     **renderInputToolbar**      |              Custom message composer container               |   *Function*    |    No    | iOS/Android |        Yes        |
|       **renderComposer**        |              Custom text input message composer              |   *Function*    |    No    | iOS/Android |        Yes        |
|        **renderActions**        |   Custom action button on the left of the message composer   |   *Function*    |    No    | iOS/Android |        Yes        |
|         **renderSend**          | Custom send button; you can pass children to the original `Send` component quite easily, for example, to use a custom icon ([example](https://github.com/FaridSafi/react-native-gifted-chat/pull/487)) |   *Function*    |    No    | iOS/Android |        Yes        |
|       **renderAccessory**       |   Custom second line of actions below the message composer   |   *Function*    |    No    | iOS/Android |        Yes        |
|     **onPressActionButton**     | Callback when the Action button is pressed (if set, the default `actionSheet` will not be used) |   *Function*    |    No    | iOS/Android |        Yes        |
|        **bottomOffset**         | Distance of the chat from the bottom of the screen (e.g. useful if you display a tab bar) |     Number      |    No    | iOS/Android |        No         |
|    **minInputToolbarHeight**    |     Minimum height of the input toolbar; default is `44`     |     Number      |    No    | iOS/Android |        No         |
|        **listViewProps**        | Extra props to be passed to the messages [``](https://facebook.github.io/react-native/docs/listview.html); some props can't be overridden, see the code in `MessageContainer.render()` for details |    *Object*     |    No    | iOS/Android |        Yes        |
|       **textInputProps**        | Extra props to be passed to the [``](https://facebook.github.io/react-native/docs/textinput.html) |    *Object*     |    No    | iOS/Android |        Yes        |
|       **textInputStyle**        | Custom style to be passed to the [``](https://facebook.github.io/react-native/docs/textinput.html) |    *Object*     |    No    | iOS/Android |        Yes        |
|          **multiline**          | Indicates whether to allow the [``](https://facebook.github.io/react-native/docs/textinput.html) to be multiple lines or not; |     Boolean     |    No    | iOS/Android |        Yes        |
|  **keyboardShouldPersistTaps**  | Determines whether the keyboard should stay visible after a tap; see [``](https://facebook.github.io/react-native/docs/scrollview.html) docs |     String      |    No    | iOS/Android |        Yes        |
|     **onInputTextChanged**      |             Callback when the input text changes             |   *Function*    |    No    | iOS/Android |        Yes        |
|       **maxInputLength**        |            Max message composer TextInput length             |    *Number*     |    No    | iOS/Android |        Yes        |
|        **parsePatterns**        | Custom parse patterns for [react-native-parsed-text](https://github.com/taskrabbit/react-native-parsed-text) used to linking message content (like URLs and phone numbers), e.g.: |   *Function*    |    No    | iOS/Android |        Yes        |
|          **extraData**          | Extra props for re-rendering FlatList on demand. This will be useful for rendering footer etc. |    *Object*     |    No    | iOS/Android |        Yes        |
|      **minComposerHeight**      |              Custom min-height of the composer               |    *Object*     |    No    | iOS/Android |        Yes        |
|      **maxComposerHeight**      |              Custom max height of the composer               |    *Object*     |    No    | iOS/Android |        No         |
|       **scrollToBottom**        |  Enables the scroll to bottom Component (Default is false)   |     Boolean     |    No    | iOS/Android |        Yes        |
|   **scrollToBottomComponent**   |         Custom Scroll To Bottom Component container          |   *Function*    |    No    | iOS/Android |        Yes        |
|    **scrollToBottomOffset**     | Custom Height Offset upon which to begin showing Scroll To Bottom Component (Default is 200) |    *Number*     |    No    | iOS/Android |        Yes        |
|     **scrollToBottomStyle**     |         Custom style for Bottom Component container          |    *Object*     |    No    | iOS/Android |        Yes        |
|          **alignTop**           | Controls whether or not the message bubbles appear at the top of the chat (Default is false - bubbles align to bottom) |    *Boolean*    |    No    | iOS/Android |        Yes        |
|        **onQuickReply**         |   Callback when sending a quick reply (to backend server)    |   *Function*    |    No    | iOS/Android |        Yes        |
|     **renderQuickReplies**      |                 Custom all quick reply view                  |   *Function*    |    No    | iOS/Android |        Yes        |
|       **quickReplyStyle**       |                Custom quick reply view style                 |    *Object*     |    No    | iOS/Android |        Yes        |
|    **renderQuickReplySend**     |                 Custom quick reply send view                 |   *Function*    |    No    | iOS/Android |        Yes        |
|     **shouldUpdateMessage**     | Lets the message component know when to update outside of normal cases. |   *Function*    |    No    | iOS/Android |        Yes        |
|       **infiniteScroll**        | infinite scroll up when reach the top of messages container, automatically call onLoadEarlier function if exist (not yet supported for the web). You need to add `loadEarlier` prop too. |    *Boolean*    |    No    | iOS/Android |        Yes        |

## 遗留问题
 - [ ] iOS 和 HarmonyOS侧效果有差异 RN输入框键盘弹出遮挡了输入框 新建一个项目加一个在屏幕底下的输入框,键盘弹出会默认把输入框顶上来
 - [ ] 输入框最大高 maxComposerHeight 设置无效果 监听输入框高度改变 onContentSizeChange未触发
 - [ ] 输入工具栏最小高 minInputToolbarHeight 设置无效果 监听输入框高度改变 onContentSizeChange未触发
 - [ ] 聊天与屏幕底部的距离 bottomOffset 设置无法查看效果,IOS设置后效果为键盘弹出后聊天栏与输入栏之间的距离,RN键盘弹出未把输入框顶上来

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/FaridSafi/react-native-gifted-chat/blob/master/LICENSE) ，请自由地享受和参与开源。