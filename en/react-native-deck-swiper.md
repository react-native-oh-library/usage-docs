> Template version: v0.2.2

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

> [!TIP] [GitHub address](https://github.com/alexbrillant/react-native-deck-swiper)

## Installation and Usage

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

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

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
      swipeDirection: 'Slide the operation card. The sliding direction is displayed here.',
      cardIndex: 0,
      showSecondCardState:true,
      indexWhenmove:'Please move the card',
      positionWhenmove:'Please move the card',
      dragStartState:'Drag Start Trigger',
      dragEndState:'Triggered by the end of dragging'
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
  Swiping = (index, position) => {
    this.setState({
      ...this.props,
      indexWhenmove:index,
      positionWhenmove:position
    })
  };
  dragStart = () => {
    this.setState({
      ...this.props,
      dragStartState:'The drag has started！！！！'
    })
  } 
  dragEnd = () => {
    this.setState({
      ...this.props,
      dragEndState:'The drag is over！！！！'
    })
  } 

  useShowSecondCard = () =>{
    this.setState({
      ...this.props,
      showSecondCardState:true
    })
  }
  disuseShowSecondCard = () =>{
    this.setState({
      ...this.props,
      showSecondCardState:false
    })
  }
  //Display Stacking Cards
  useShowSecondCard = () =>{
      this.setState({
        ...this.props,
        showSecondCardState:true
      })
  }

  render() {
    return (
              <Text>The overall effect involves attributes and interfaces.</Text>
              <Text>onSwiped,Sliding direction：{this.state.swipeDirection}</Text>
              <Text>onTapCard,When lightly touched，Function called by the card: SwipeLeft is set to slide left.</Text>
              <Text>onSwipedAllCards,Function invoked when the card is swiped. After the card is swiped, the value is set to true. After the card is swiped, the status will not be reset when the'Back button' is used:{JSON.stringify(this.state.swipedAllCards)}</Text>
              <Text>onSwiping,Callback triggered when a card is moved: Swiping card at index {this.state.indexWhenmove}, position: {this.state.positionWhenmove}</Text>
              <Text>dragStart,Callback triggered when the card starts to drag:{this.state.dragStartState}</Text>
              <Text>dragEnd,Callback triggered when the card drag ends:{this.state.dragEndState}</Text>
              <View style={styles.container}>
                <Swiper
                  ref={swiper => {
                    this.swiper = swiper
                  }}
                  onSwiped={() => this.setState({ swipeDirection: this.state.swipeDirection = 'general' })}
                  onSwipedLeft={() => this.setState({ swipeDirection: this.state.swipeDirection = 'left' })}
                  onSwipedRight={() => this.setState({ swipeDirection: this.state.swipeDirection = 'right' })}
                  onSwipedTop={() => this.setState({ swipeDirection: this.state.swipeDirection = 'top' })}
                  onSwipedBottom={() => this.setState({ swipeDirection: this.state.swipeDirection = 'bottom' })}
                  onTapCard={this.swipeLeft}
                  cards={this.state.cards}
                  cardIndex={this.state.cardIndex}
                  cardVerticalMargin={200}
                  cardHorizontalMargin={80}
                  renderCard={this.renderCard}
                  onSwiping={this.Swiping}
                  onSwipedAll={this.onSwipedAllCards}
                  dragStart={this.dragStart}
                  dragEnd={this.dragEnd}
                  stackSize={3}
                  stackSeparation={20}
                  showSecondCard={this.state.showSecondCardState}
                  overlayLabels={{
                    bottom: {
                      title: 'Downward',
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
                      title: 'To the left',
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
                      title: 'To the right',
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
                      title: 'Upward',
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
                  animateOverlayLabelsOpacity
                  animateCardOpacity
                  swipeBackCard
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
                  <Button onPress={() => this.useShowSecondCard()} title='Display stacking cards (stacked by default. After reset, slide one card to take effect.)' />
                  <Button onPress={() => this.disuseShowSecondCard()} title='The stacked card is not displayed. (After you click this button, you need to slide one card to take effect.)' />
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

## Constraints

### Compatibility

This document is verified based on the following versions:

1. RNOH：0.72.27; SDK: HarmonyOS-Next-DB1 5.0.0.25; IDE: DevEco Studio 5.0.3.400SP7; ROM: 3.0.0.25;
2. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;

## Properties

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

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

## Event callback

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

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

## Static Methods

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP]  If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name            | Description                           | Type     | Required | Platform    | HarmonyOS Support |
| --------------- | ------------------------------------- | -------- | -------- | ----------- | ----------------- |
| swipeBack       | swipe back into deck last swiped card | callback | no       | iOS/Android | yes               |
| swipeLeft       | swipe left to the next card           | callback | no       | iOS/Android | yes               |
| swipeRight      | swipe right to the next card          | callback | no       | iOS/Android | yes               |
| swipeTop        | swipe top to the next card            | callback | no       | iOS/Android | yes               |
| swipeBottom     | swipe bottom to the next card         | callback | no       | iOS/Android | yes               |
| jumpToCardIndex | set the current card index            | callback | no       | iOS/Android | yes               |

## Known Issues

## Others

## License

This project is licensed under [The ISC License (ISC)](https://github.com/alexbrillant/react-native-deck-swiper/blob/master/LICENSE) .
