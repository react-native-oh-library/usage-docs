<!-- {% raw %} -->

> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-deck-swiper</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/alexbrillant/react-native-deck-swiper">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/alexbrillant/react-native-deck-swiper/blob/master/LICENSE">
         <img src="https://img.shields.io/badge/license-ISC-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/alexbrillant/react-native-deck-swiper)

## 安装与使用

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-deck-swiper@2.0.17
```

#### **yarn**

```bash
yarn add react-native-deck-swiper@2.0.17
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React, { Component, useState } from 'react'
import Swiper from 'react-native-deck-swiper'
import { Button, StyleSheet, Text, View, ScrollView } from 'react-native'

function* range(start, end) {
  for (let i = start; i <= end; i++) {
    yield i
  }
}

export default class DeckSwiperExample extends Component {

  constructor(props) {
    super(props)
    this.state = {
      cards: [...range(1, 10)],
      swipedAllCards: false,
      swipeDirection: '操作卡片滑动，此处显示滑动方向',
      cardIndex: 0,
      //是否显示下一张卡片
      showSecondCardState:true,
      //卡片移动时候的索引
      indexWhenmove:'请移动卡片',
      positionWhenmove:'请移动卡片',
      dragStartState:'拖动开始触发',
      dragEndState:'拖动结束触发'
    }
  }

  renderCard = (card, index) => {
    return (
      <View style={styles.card}>
        <Text style={styles.text}>{card} - {index}</Text>
      </View>
    )
  };

  onSwiped = (type) => {
    console.log(`on swiped ${type}`)
  }

  onSwipedAllCards = () => {
    this.setState({
      swipedAllCards: this.state.swipedAllCards = true
    })
  };

  //轻触时，卡片滑动的方向
  swipeLeft = () => {
    this.swiper.swipeLeft()
  };
  swipeRight = () => {
    this.swiper.swipeRight()
  };
  swipeTop = () => {
    this.swiper.swipeTop()
  };
  swipeBottom = () => {
    this.swiper.swipeBottom()
  };
  //卡片拖动时，调用的函数
  Swiping = (index, position) => {
    this.setState({
      ...this.props,
      indexWhenmove:index,
      positionWhenmove:position
    })
  };
  //拖动开始时候要调用的函数
  dragStart = () => {
    this.setState({
      ...this.props,
      dragStartState:'拖动已经开始了！！！！'
    })
  } 
  //拖动结束时候要调用的函数
  dragEnd = () => {
    this.setState({
      ...this.props,
      dragEndState:'拖动已经结束了！！！！'
    })
  } 

  //显示堆叠卡片
  useShowSecondCard = () =>{
    this.setState({
      ...this.props,
      showSecondCardState:true
    })
  }
  //不显示堆叠卡片
  disuseShowSecondCard = () =>{
    this.setState({
      ...this.props,
      showSecondCardState:false
    })
  }
  //显示堆叠卡片
  useShowSecondCard = () =>{
      this.setState({
        ...this.props,
        showSecondCardState:true
      })
  }

  render() {
    return (
              <Text>该整体效果涉及属性和接口</Text>
              <Text>onSwiped,滑动方向：{this.state.swipeDirection}</Text>
              <Text>onTapCard,轻触时，卡片调用的函数:这里设置的是swipeLeft向左滑动</Text>
              <Text>onSwipedAllCards,刷卡时候调用的函数,刷卡完毕置位true.刷卡完毕的情况下使用'回退按键',该状态不会重置:{JSON.stringify(this.state.swipedAllCards)}</Text>
              <Text>onSwiping,卡片移动时触发的回调: Swiping card at index {this.state.indexWhenmove}, position: {this.state.positionWhenmove}</Text>
              <Text>dragStart,卡片开始拖动时候触发的回调:{this.state.dragStartState}</Text>
              <Text>dragEnd,卡片拖动结束时候触发的回调:{this.state.dragEndState}</Text>
              <View style={styles.container}>
                <Swiper
                  ref={swiper => {
                    this.swiper = swiper
                  }}
                  //滑动方向
                  onSwiped={() => this.setState({ swipeDirection: this.state.swipeDirection = 'general' })}
                  onSwipedLeft={() => this.setState({ swipeDirection: this.state.swipeDirection = 'left' })}
                  onSwipedRight={() => this.setState({ swipeDirection: this.state.swipeDirection = 'right' })}
                  onSwipedTop={() => this.setState({ swipeDirection: this.state.swipeDirection = 'top' })}
                  onSwipedBottom={() => this.setState({ swipeDirection: this.state.swipeDirection = 'bottom' })}
                  //轻触卡时要调用的函数，这里是向左滑动
                  onTapCard={this.swipeLeft}
                  //需要渲染的卡片组，必填
                  cards={this.state.cards}
                  //首张卡片，这里为设置为0
                  cardIndex={this.state.cardIndex}
                  //卡片的垂直边距，默认为60
                  cardVerticalMargin={200}
                  //卡片的水平边距，默认为20
                  cardHorizontalMargin={80}
                  //卡片渲染的参数，必填
                  renderCard={this.renderCard}
                  //卡片移动时触发的回调
                  onSwiping={this.Swiping}
                  //当卡片滑完后触发的回调
                  onSwipedAll={this.onSwipedAllCards}
                  //拖动开始触发的函数
                  dragStart={this.dragStart}
                  //拖动结束触发的函数
                  dragEnd={this.dragEnd}
                  //显示堆叠卡片,只有当showSecondCard为true的时候,才会生效
                  stackSize={3}
                  //卡之间的垂直间隔f,具体表现为卡片的堆叠样式,例如此处为-100，成多米诺形式
                  stackSeparation={20}
                  //是否显示第二张卡
                  showSecondCard={this.state.showSecondCardState}
                  //滑动覆盖标签，滑动时候卡片上的覆盖样式
                  overlayLabels={{
                    bottom: {
                      title: '向下',
                      style: {
                        label: {
                          backgroundColor: 'black',
                          borderColor: 'black',
                          color: 'white',
                          borderWidth: 1
                        },
                        wrapper: {
                          flexDirection: 'column',
                          alignItems: 'center',
                          justifyContent: 'center'
                        }
                      }
                    },
                    left: {
                      title: '向左',
                      style: {
                        label: {
                          backgroundColor: 'black',
                          borderColor: 'black',
                          color: 'white',
                          borderWidth: 1
                        },
                        wrapper: {
                          flexDirection: 'column',
                          alignItems: 'flex-end',
                          justifyContent: 'flex-start',
                          marginTop: 30,
                          marginLeft: -30
                        }
                      }
                    },
                    right: {
                      title: '向右',
                      style: {
                        label: {
                          backgroundColor: 'black',
                          borderColor: 'black',
                          color: 'white',
                          borderWidth: 1
                        },
                        wrapper: {
                          flexDirection: 'column',
                          alignItems: 'flex-start',
                          justifyContent: 'flex-start',
                          marginTop: 30,
                          marginLeft: 30
                        }
                      }
                    },
                    top: {
                      title: '向上',
                      style: {
                        label: {
                          backgroundColor: 'black',
                          borderColor: 'black',
                          color: 'white',
                          borderWidth: 1
                        },
                        wrapper: {
                          flexDirection: 'column',
                          alignItems: 'center',
                          justifyContent: 'center'
                        }
                      }
                    }
                  }}
                  //动画卡覆盖标签不透明度，默认为false
                  animateOverlayLabelsOpacity
                  animateCardOpacity
                  //回退卡片动画
                  swipeBackCard
                  //背景图
                  containerStyle={
                    {
                        height: 700,
                        zIndex: 0,
                        position: 'absolute',
                        top: 0,
                        left: 0,
                    }}
                >
                  <Button onPress={() => this.swiper.swipeBack()} title='Swipe Back' />
                  <Button onPress={() => this.useShowSecondCard()} title='显示堆叠卡片(默认为堆叠；重置后，需要滑动一张卡片生效)' />
                  <Button onPress={() => this.disuseShowSecondCard()} title='不显示堆叠卡片(点击后，需要滑动一张卡片生效)' />
                </Swiper>
              </View>
    )
  }
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#F5FCFF',
    width: '100%',
    height: '700',
    display: 'flex', 
    position: 'relative'
  },
  card: {
    flex: 1,
    borderRadius: 4,
    borderWidth: 2,
    borderColor: '#E8E8E8',
    justifyContent: 'center',
    backgroundColor: 'white',
  },
  text: {
    textAlign: 'center',
    fontSize: 50,
    backgroundColor: 'transparent'
  },
  done: {
    textAlign: 'center',
    fontSize: 30,
    color: 'white',
    backgroundColor: 'transparent'
  }
})

export default App;
```

## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

1. RNOH: 0.72.27; SDK: HarmonyOS-Next-DB1 5.0.0.25; IDE: DevEco Studio 5.0.3.400SP7; ROM: 3.0.0.25;

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

### Card props

| Name            | Description                                                  | Type                      | Required | Platform    | HarmonyOS Support |
| --------------- | ------------------------------------------------------------ | ------------------------- | -------- | ----------- | ----------------- |
| cards           | array of data for the cards to be rendered                   | array                     | yes      | iOS/Android | yes               |
| renderCard      | function to render the card based on the data                | func(cardData, cardIndex) | yes      | iOS/Android | yes               |
| keyExtractor    | function to get the card's react key                         | func(cardData)            | no       | iOS/Android | yes               |
| cardIndex       | cardIndex to start with                                      | number                    | no       | iOS/Android | yes               |
| infinite        | keep swiping indefinitely                                    | bool                      | no       | iOS/Android | yes               |
| horizontalSwipe | enable/disable horizontal swiping                            | bool                      | no       | iOS/Android | yes               |
| verticalSwipe   | enable/disable vertical swiping                              | bool                      | no       | iOS/Android | yes               |
| showSecondCard  | enable/disable second card while swiping                     | bool                      | no       | iOS/Android | yes               |
| stackSize       | number of underlaying cards to show (showSecondCard must be enabled) | number                    | no       | iOS/Android | yes               |

### Swipe animation props

| Name                   | Description                     | Type   | Required | Platform    | HarmonyOS Support |
| ---------------------- | ------------------------------- | ------ | -------- | ----------- | ----------------- |
| verticalThreshold      | vertical swipe threshold        | number | no       | iOS/Android | yes               |
| horizontalThreshold    | horizontal swipe threshold      | number | no       | iOS/Android | yes               |
| swipeAnimationDuration | duration of the swipe animation | number | no       | iOS/Android | yes               |
| disableBottomSwipe     | disable bottom swipe            | bool   | no       | iOS/Android | yes               |
| disableLeftSwipe       | disable left swipe              | bool   | no       | iOS/Android | yes               |
| disableRightSwipe      | disable right swipe             | bool   | no       | iOS/Android | yes               |
| disableTopSwipe        | disable top swipe               | bool   | no       | iOS/Android | yes               |

### Stack props

| Name                   | Description                                            | Type   | Required | Platform    | HarmonyOS Support |
| ---------------------- | ------------------------------------------------------ | ------ | -------- | ----------- | ----------------- |
| stackSeparation        | vertical separation between underlaying cards          | number | no       | iOS/Android | yes               |
| stackScale             | percentage to reduce the size of each underlaying card | number | no       | iOS/Android | yes               |
| stackAnimationFriction | spring animation friction (bounciness)                 | number | no       | iOS/Android | yes               |
| stackAnimationTension  | spring animation tension (speed)                       | number | no       | iOS/Android | yes               |

### Rotation animation props

| Name                | Description                                            | Type  | Required | Platform    | HarmonyOS Support |
| ------------------- | ------------------------------------------------------ | ----- | -------- | ----------- | ----------------- |
| inputRotationRange  | x values range for the rotation output                 | array | no       | iOS/Android | yes               |
| outputRotationRange | rotation values for the x values in inputRotationRange | array | no       | iOS/Android | yes               |

### Opacity animation props

| Name                              | Description                                                  | Type   | Required | Platform    | HarmonyOS Support |
| --------------------------------- | ------------------------------------------------------------ | ------ | -------- | ----------- | ----------------- |
| animateCardOpacity                | animate card opacity                                         | bool   | no       | iOS/Android | yes               |
| inputCardOpacityRangeX            | pan x card opacity input range                               | array  | no       | iOS/Android | yes               |
| outputCardOpacityRangeX           | opacity values for the values in inputCardOpacityRangeX      | array  | no       | iOS/Android | yes               |
| inputCardOpacityRangeY            | pan y card opacity input range                               | array  | no       | iOS/Android | yes               |
| outputCardOpacityRangeY           | opacity values for the values in inputCardOpacityRangeY      | array  | no       | iOS/Android | yes               |
| animateOverlayLabelsOpacity       | animate card overlay labels opacity                          | bool   | no       | iOS/Android | yes               |
| inputOverlayLabelsOpacityRangeX   | pan x overlay labels opacity input range                     | array  | no       | iOS/Android | yes               |
| outputOverlayLabelsOpacityRangeX  | opacity values for the values in inputOverlayLabelsOpacityRangeX | array  | no       | iOS/Android | yes               |
| inputOverlayLabelsOpacityRangeY   | pan x overlay labels opacity input range                     | array  | no       | iOS/Android | yes               |
| outputOverlayLabelsOpacityRangeY  | opacity values for the values in inputOverlayLabelsOpacityRangeY | array  | no       | iOS/Android | yes               |
| overlayOpacityVerticalThreshold   | vertical threshold for overlay label                         | number | no       | iOS/Android | yes               |
| overlayOpacityHorizontalThreshold | horizontal threshold for overlay label                       | number | no       | iOS/Android | yes               |

### Swipe overlay labels

| Name                     | Description                  | Type   | Required | Platform    | HarmonyOS Support |
| ------------------------ | ---------------------------- | ------ | -------- | ----------- | ----------------- |
| overlayLabels            | swipe labels title and style | object | no       | iOS/Android | yes               |
| overlayLabelStyle        | swipe labels style           | object | no       | iOS/Android | yes               |
| overlayLabelWrapperStyle | overlay label wrapper style  | object | no       | iOS/Android | yes               |

### Swipe back to previous card props

| Name                              | Description                               | Type | Required | Platform    | HarmonyOS Support |
| --------------------------------- | ----------------------------------------- | ---- | -------- | ----------- | ----------------- |
| goBackToPreviousCardOnSwipeLeft   | previous card is rendered on left swipe   | bool | no       | iOS/Android | yes               |
| goBackToPreviousCardOnSwipeRight  | previous card is rendered on right swipe  | bool | no       | iOS/Android | yes               |
| goBackToPreviousCardOnSwipeTop    | previous card is rendered on top swipe    | bool | no       | iOS/Android | yes               |
| goBackToPreviousCardOnSwipeBottom | previous card is rendered on bottom swipe | bool | no       | iOS/Android | yes               |

### Style props

| Name                 | Description                                               | Type   | Required | Platform    | HarmonyOS Support |
| -------------------- | --------------------------------------------------------- | ------ | -------- | ----------- | ----------------- |
| backgroundColor      | background color for the view containing the cards        | string | no       | iOS/Android | yes               |
| marginTop            | marginTop for the swiper container                        | number | no       | iOS/Android | yes               |
| marginBottom         | marginBottom for the swiper container                     | number | no       | iOS/Android | yes               |
| cardVerticalMargin   | card vertical margin                                      | number | no       | iOS/Android | yes               |
| cardHorizontalMargin | card horizontal margin                                    | number | no       | iOS/Android | yes               |
| childrenOnTop        | render children on top or not                             | bool   | no       | iOS/Android | yes               |
| cardStyle            | override swipable card style                              | node   | no       | iOS/Android | yes               |
| containerStyle       | overrides for the containing style                        | node   | no       | iOS/Android | yes               |
| pointerEvents        | pointerEvents prop for the containing                     | string | no       | iOS/Android | yes               |
| useViewOverflow      | use ViewOverflow instead of View for the Swiper component | bool   | no       | iOS/Android | yes               |

### Swipe back Props

| Name                         | Description                                                 | Type   | Required | Platform    | HarmonyOS Support |
| ---------------------------- | ----------------------------------------------------------- | ------ | -------- | ----------- | ----------------- |
| previousCardDefaultPositionX | Animation start position oX when card swipes back into deck | number | no       | iOS/Android | yes               |
| previousCardDefaultPositionY | Animation start position oY when card swipes back into deck | number | no       | iOS/Android | yes               |
| stackAnimationFriction       | spring animation friction (bounciness)                      | number | no       | iOS/Android | yes               |
| stackAnimationTension        | spring animation tension (speed)                            | number | no       | iOS/Android | yes               |
| swipeBackCard                | renders swipe back card, in order to animate it             | bool   | no       | iOS/Android | yes               |

## 事件回调

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name              | Description                                                  | Type | Required | Platform    | HarmonyOS Support |
| ----------------- | ------------------------------------------------------------ | ---- | -------- | ----------- | ----------------- |
| onSwipedAll       | function to be called when all cards have been swiped        | func | no       | iOS/Android | yes               |
| onSwiped          | function to be called when a card is swiped. it receives the swiped card index | func | no       | iOS/Android | yes               |
| onSwipedAborted   | function to be called when a card is released before reaching the threshold | func | no       | iOS/Android | yes               |
| onSwipedLeft      | function to be called when a card is swiped left. it receives the swiped card index | func | no       | iOS/Android | yes               |
| onSwipedRight     | function to be called when a card is swiped right. it receives the swiped card index | func | no       | iOS/Android | yes               |
| onSwipedTop       | function to be called when a card is swiped top. it receives the swiped card index | func | no       | iOS/Android | yes               |
| onSwipedBottom    | function to be called when a card is swiped bottom. it receives the swiped card index | func | no       | iOS/Android | yes               |
| onSwiping         | function to be called when a card is being moved. it receives X and Y positions | func | no       | iOS/Android | yes               |
| dragStart         | function to be called when drag start                        | func | no       | iOS/Android | yes               |
| dragEnd           | function to be called when drag end                          | func | no       | iOS/Android | yes               |
| onTapCard         | function to be called when tapping a card. it receives the tapped card index | func | no       | iOS/Android | yes               |
| onTapCardDeadZone | maximum amount of movement before a tap is no longer recognized as a tap | func | no       | iOS/Android | yes               |

## 静态方法

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name            | Description                           | Type     | Required | Platform    | HarmonyOS Support |
| --------------- | ------------------------------------- | -------- | -------- | ----------- | ----------------- |
| swipeBack       | swipe back into deck last swiped card | callback | no       | iOS/Android | yes               |
| swipeLeft       | swipe left to the next card           | callback | no       | iOS/Android | yes               |
| swipeRight      | swipe right to the next card          | callback | no       | iOS/Android | yes               |
| swipeTop        | swipe top to the next card            | callback | no       | iOS/Android | yes               |
| swipeBottom     | swipe bottom to the next card         | callback | no       | iOS/Android | yes               |
| jumpToCardIndex | set the current card index            | callback | no       | iOS/Android | yes               |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The ISC License (ISC)](https://github.com/alexbrillant/react-native-deck-swiper/blob/master/LICENSE) ，请自由地享受和参与开源。

<!-- {% endraw %} -->