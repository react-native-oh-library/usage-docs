> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-ezswiper</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/easyui/react-native-ezswiper">       
         <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/easyui/react-native-ezswiper/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!Tip] [GitHub address](https://github.com/easyui/react-native-ezswiper)

## Installation and Usage

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-ezswiper@1.3.0 --save
```

#### **yarn**

```bash
yarn add react-native-ezswiper@1.3.0 --save
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

```js
/**
 * Sample React Native App
 * https://github.com/facebook/react-native
 * @flow
 */

import React, { Component } from 'react';
import {
  StyleSheet,
  Text,
  Button,
  View,
  Dimensions,
  ScrollView,
  SafeAreaView,
  Image
} from 'react-native';

const { width } = Dimensions.get('window');
import EZSwiper from 'react-native-ezswiper';

export default class ezswiperApp extends Component<{}> {
  constructor(props) {
    super(props)
    this.state = {
      currentPage: 0,
    };
  }

  renderTitle(title) {
    return <Text style={{ backgroundColor: 'green' }}>{title}</Text>
  }

  renderRow(obj, index) {
    return (
      <View style={[styles.cell, { backgroundColor: index % 2 === 0 ? 'red' : 'yellow' }]}>
        <Text>{obj}</Text>
      </View>
    )
  }

  renderImageRow(obj, index) {
    return (
      <View style={[styles.cell, { backgroundColor: 'gray', overflow: 'hidden' }]}>
        <Image
          style={{ position: 'absolute', top: 0, right: 0, bottom: 0, left: 0, width: undefined, height: undefined }}
          resizeMode={'contain'}
          source={obj} />
        <Text style={{ backgroundColor: 'transparent', color: 'white' }}>{'Victoria\'s Secre ' + index}</Text>

      </View>
    )
  }


  onPressRow(obj, index) {
    console.log('onPressRow=>obj:' + obj + ' ,index:' + index);
    alert('onPressRow=>obj:' + obj + ' ,index:' + index);
  }

  onWillChange(obj, index) {
    console.log('onWillChange=>obj:' + obj + ' ,index:' + index);
  }

  onDidChange(obj, index, setDidChangeObj, setIndex) {
    setDidChangeObj(obj);
    setIndex(index)
  }

  render() {

    return (
      <SafeAreaView>
        <ScrollView>
          <View style={styles.tips}>
            <Text>card:ratio 0.6</Text>
          </View>
          <EZSwiper style={[styles.swiper, { width: width, height: 150 }]}
            dataSource={['0', '1', '2', '3']}
            width={width}
            height={150}
            autoplayDirection={false}
            renderRow={this.renderRow}
            onPress={this.onPressRow}
            onWillChange={this.onWillChange}
            ratio={0.6}
            index={2}
            horizontal={true}
            loop={true}
            autoplayTimeout={2}
          />
          <View style={styles.tips}>
            <Text>left</Text>
          </View>
          <EZSwiper style={[styles.swiper, { width: width, height: 150 }]}
            dataSource={['0', '1', '2', '3']}
            width={width}
            height={150}
            renderRow={this.renderRow}
            onPress={this.onPressRow}
            onWillChange={this.onWillChange}
            index={2}
            horizontal={true}
            loop={true}
            autoplayTimeout={2}
            cardParams={{ cardSide: width * 0.6, cardSmallSide: 150 * 0.6, cardSpace: width * (1 - 0.6) / 2 * 0.4 }}
            offset={-width * 0.2 + 20}
          />
          <View style={styles.tips}>
            <Text>right</Text>
          </View>
          <EZSwiper style={[styles.swiper, { width: width, height: 150 }]}
            dataSource={['0', '1', '2', '3']}
            width={width}
            height={150}
            renderRow={this.renderRow}
            onPress={this.onPressRow}
            onWillChange={this.onWillChange}
            ratio={0.6}
            index={2}
            horizontal={true}
            loop={true}
            autoplayTimeout={2}
            offset={60}
          />
          <View style={styles.tips}>
            <Text>normal</Text>
          </View>
          <EZSwiper style={[styles.swiper, { width: width, height: 150 }]}
            dataSource={['0', '1', '2', '3']}
            width={width}
            height={150}
            renderRow={this.renderRow}
            onPress={this.onPressRow} />
          <View style={styles.tips}>
            <Text>card ratio:0.867 loop:false index:2</Text>
          </View>
          <EZSwiper style={[styles.swiper, { width: width - 100, height: 150, marginHorizontal: 50 }]}
            dataSource={['0', '1', '2', '3', '4']}
            width={width - 100}
            height={150}
            renderRow={this.renderRow}
            onPress={this.onPressRow}
            ratio={0.867}
            loop={false}
            index={2}
          />

          <EZSwiper style={[styles.swiper, { width: width, height: 150 }]}
            dataSource={['0', '1', '2', '3']}
            width={width}
            height={150}
            renderRow={this.renderRow}
            onPress={this.onPressRow}
            cardParams={{ cardSide: width * 0.867, cardSmallSide: 150 * 0.867, cardSpace: width * (1 - 0.867) / 2 * 0.2 }}
          />
          <View style={styles.tips}>
            <Text>card ratio:0.867 horizontal:false</Text>
          </View>
          <EZSwiper style={[styles.swiper, { width: width, height: 200 }]}
            dataSource={['0', '1', '2', '3']}
            width={width}
            height={200}
            renderRow={this.renderRow}
            onPress={this.onPressRow}
            ratio={0.867}
            horizontal={false}
          />
          <DidChangeDom renderRow={this.renderRow} />
          <WillChangeDom renderRow={this.renderRow} />
          <ScrollToDom renderRow={this.renderRow} />
        </ScrollView>
      </SafeAreaView>

    );
  }
}


const DidChangeDom = (props) => {
  const [didChangeObj, setDidChangeObj] = React.useState(0);
  const [index, setIndex] = React.useState(0);

  return (
    <View>
      <View style={styles.tips}>
        <Text>obj:{didChangeObj}   index:{index}</Text>
      </View>
      <EZSwiper style={[styles.swiper, { width: width, height: 150 }]}
        dataSource={['0', '1', '2', '3']}
        width={width}
        height={150}
        renderRow={props.renderRow}
        onDidChange={(obj, index) => {
          setDidChangeObj(obj)
          setIndex(index)
        }} />
    </View>)
}

const WillChangeDom = (props) => {
  const [didChangeObj, setDidChangeObj] = React.useState(0);
  const [index, setIndex] = React.useState(0);

  return (
    <View>
      <View style={styles.tips}>
        <Text>obj:{didChangeObj}   index:{index}</Text>
      </View>
      <EZSwiper style={[styles.swiper, { width: width, height: 150 }]}
        dataSource={['0', '1', '2', '3']}
        width={width}
        height={150}
        renderRow={props.renderRow}
        onWillChange={(obj, index) => {
          setDidChangeObj(obj)
          setIndex(index)
        }} />
    </View>)
}

function ScrollToDom(props) {
  this.refDom = null;
  const refDomFn = (view) => {
    this.refDom = view
  }
  const scrollTo = (index) => {
    if (this.refDom) {
      this.refDom.scrollTo(index + 1, true)
    }
  }
  return (
    <View>
      <View style={{ display: 'flex' }}>
        <Button onPress={() => scrollTo(0)} style={styles.button} title="Press 0" />
        <Button onPress={() => scrollTo(1)} style={styles.button} title="Press 1" />
        <Button onPress={() => scrollTo(2)} style={styles.button} title="Press 2" />
        <Button onPress={() => scrollTo(3)} style={styles.button} title="Press 3" />
        <Button onPress={() => scrollTo(4)} style={styles.button} title="Press 4" />
      </View>
      <EZSwiper style={[styles.swiper, { width: width, height: 150 }]}
        dataSource={['0', '1', '2', '3', '4']}
        width={width}
        ref={refDomFn}
        height={150}
        renderRow={props.renderRow}
      />
    </View>)
}


const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: 'white',
  },
  swiper: {
    backgroundColor: 'white'
  },
  button: {
    width: 50,
    height: 30,
  },
  cell: {
    backgroundColor: 'red',
    flex: 1,
    alignItems: 'center',
    justifyContent: 'center',
  },
  pageControl: {
    position: 'absolute',
    bottom: 4,
    right: 10,
  },
  tips:{
    backgroundColor:'green'
  }
});
```



## Constraints

## Compatibility

This document is verified based on the following versions:

 1.RNOH: 0.72.29; SDK：OpenHarmony-5.0.0.65; IDE：DevEco Studio 5.0.3.706; ROM：NEXT.0.0.65;
 2.RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;

## Properties

> [!Tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!Tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                  | Description                                                                                            | Type     | default | Required | Platform | HarmonyOS Support |
| --------------------- | ------------------------------------------------------------------------------------------------------ | -------- | -------- | -------- | ----------------- | ----------------- |
| `width`       | swiper width                 | number |  | Yes       | All      | yes               |
| `height`         | swiper height                             | number |  | Yes       | All      | yes               |
| `index`        | initial index bar.                                   | number | 0 | No       | All      | yes               |
| `offset`      | initial left and right or up and down offsets view.                                                               | number | 0 | No       | All      | yes               |
| `horizontal` | swiper derection is horizontal                   | boolean | true | No       | All      | yes               |
| `loop`        | swiper is loop | boolean  | true | No       | All      | yes               |
| `autoplayTimeout`               | auto play mode (in second)                       | number | 5 | No       | All      | yes               |
| `autoplayDirection`            | cycle direction control                                            | boolean  | true | No       | All      | yes               |
| `ratio`      | scaling ratio                                                         | number | 1 | No       | All      | yes               |
| `cardParams`          | swiper card advanced object                                                      | object | {} | No       | All      | yes               |
| `renderRow`               | render card view                                    | function |   | Yes    | All      | yes               |
| `onPress`         | card is clicked action                                   | function |    | No       | All      | yes               |
| `onWillChange`       | next card will show                              | function |    | No       | All      | yes               |
| `onDidChange`       | next card showed                               | function  |   | No       | All      | yes               |

cardParams is object：{cardSide,cardSmallSide,cardSpace}
<img src="../img/cardParams.png" />

## Static Methods

> [!Tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!Tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                  | Description                                                                                            | Type     | Required | Platform | HarmonyOS Support |
| --------------------- | ------------------------------------------------------------------------------------------------------ | -------- | -------- | -------- | ----------------- |
| `scrollTo(index, animated = true)`       | scroll to position                | function | No       | All      | yes               |

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/easyui/react-native-ezswiper).
