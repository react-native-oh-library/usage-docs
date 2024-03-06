模板版本：v0.1.3

<p align="center">
  <h1 align="center"> <code>react-native-swipe-list-view</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/jemise111/react-native-swipe-list-view">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>



> [!TIP] [Github 地址](https://github.com/rnc-archive/react-native-drawer-layout-polyfill)

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install --save react-native-swipe-list-view
```

#### **yarn**

```bash
yarn add react-native-swipe-list-view
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

```tsx
import React, { useState } from 'react';
import {
    Animated,
    Image,
    StyleSheet,
    Text,
    TouchableOpacity,
    TouchableHighlight,
    View,
} from 'react-native';

import { SwipeListView } from 'react-native-swipe-list-view';

const rowSwipeAnimatedValues = {};
Array(20)
    .fill('')
    .forEach((_, i) => {
        rowSwipeAnimatedValues[`${i}`] = new Animated.Value(0);
    });

export default function SwipeValueBasedUi() {
    const [listData, setListData] = useState(
        Array(20)
            .fill('')
            .map((_, i) => ({ key: `${i}`, text: `item #${i}` }))
    );

    const closeRow = (rowMap, rowKey) => {
        if (rowMap[rowKey]) {
            rowMap[rowKey].closeRow();
        }
    };

    const deleteRow = (rowMap, rowKey) => {
        closeRow(rowMap, rowKey);
        const newData = [...listData];
        const prevIndex = listData.findIndex(item => item.key === rowKey);
        newData.splice(prevIndex, 1);
        setListData(newData);
    };

    const onRowDidOpen = rowKey => {
        console.log('This row opened', rowKey);
    };

    const onSwipeValueChange = swipeData => {
        const { key, value } = swipeData;
        rowSwipeAnimatedValues[key].setValue(Math.abs(value));
    };

    const renderItem = data => (
        <TouchableHighlight
            onPress={() => console.log('You touched me')}
            style={styles.rowFront}
            underlayColor={'#AAA'}
        >
            <View>
                <Text>I am {data.item.text} in a SwipeListView</Text>
            </View>
        </TouchableHighlight>
    );

    const renderHiddenItem = (data, rowMap) => (
        <View style={styles.rowBack}>
            <Text>Left</Text>
            <TouchableOpacity
                style={[styles.backRightBtn, styles.backRightBtnLeft]}
                onPress={() => closeRow(rowMap, data.item.key)}
            >
                <Text style={styles.backTextWhite}>Close</Text>
            </TouchableOpacity>
            <TouchableOpacity
                style={[styles.backRightBtn, styles.backRightBtnRight]}
                onPress={() => deleteRow(rowMap, data.item.key)}
            >
                <Animated.View
                    style={[
                        styles.trash,
                        {
                            transform: [
                                {
                                    scale: rowSwipeAnimatedValues[
                                        data.item.key
                                    ].interpolate({
                                        inputRange: [45, 90],
                                        outputRange: [0, 1],
                                        extrapolate: 'clamp',
                                    }),
                                },
                            ],
                        },
                    ]}
                >
                    <Image
                        source={require('../images/trash.png')}
                        style={styles.trash}
                    />
                </Animated.View>
            </TouchableOpacity>
        </View>
    );

    return (
        <View style={styles.container}>
            <SwipeListView
                data={listData}
                renderItem={renderItem}
                renderHiddenItem={renderHiddenItem}
                leftOpenValue={75}
                rightOpenValue={-150}
                previewRowKey={'0'}
                previewOpenValue={-40}
                previewOpenDelay={3000}
                onRowDidOpen={onRowDidOpen}
                onSwipeValueChange={onSwipeValueChange}
            />
        </View>
    );
}

const styles = StyleSheet.create({
    container: {
        backgroundColor: 'white',
        flex: 1,
    },
    backTextWhite: {
        color: '#FFF',
    },
    rowFront: {
        alignItems: 'center',
        backgroundColor: '#CCC',
        borderBottomColor: 'black',
        borderBottomWidth: 1,
        justifyContent: 'center',
        height: 50,
    },
    rowBack: {
        alignItems: 'center',
        backgroundColor: '#DDD',
        flex: 1,
        flexDirection: 'row',
        justifyContent: 'space-between',
        paddingLeft: 15,
    },
    backRightBtn: {
        alignItems: 'center',
        bottom: 0,
        justifyContent: 'center',
        position: 'absolute',
        top: 0,
        width: 75,
    },
    backRightBtnLeft: {
        backgroundColor: 'blue',
        right: 75,
    },
    backRightBtnRight: {
        backgroundColor: 'red',
        right: 0,
    },
    trash: {
        height: 25,
        width: 25,
    },
});
```

```jsx
import React, { useState, useRef } from 'react';
import {
    Animated,
    Dimensions,
    StyleSheet,
    Text,
    TouchableHighlight,
    View,
} from 'react-native';

import { SwipeListView } from 'react-native-swipe-list-view';

const rowTranslateAnimatedValues = {};
Array(20)
    .fill('')
    .forEach((_, i) => {
        rowTranslateAnimatedValues[`${i}`] = new Animated.Value(1);
    });

export default function SwipeToDelete() {
    const [listData, setListData] = useState(
        Array(20)
            .fill('')
            .map((_, i) => ({ key: `${i}`, text: `item #${i}` }))
    );

    const animationIsRunning = useRef(false);

    const onSwipeValueChange = swipeData => {
        const { key, value } = swipeData;
        if (
            value < -Dimensions.get('window').width &&
            !animationIsRunning.current
        ) {
            animationIsRunning.current = true;
            Animated.timing(rowTranslateAnimatedValues[key], {
                toValue: 0,
                duration: 200,
                useNativeDriver: false,
            }).start(() => {
                const newData = [...listData];
                const prevIndex = listData.findIndex(item => item.key === key);
                newData.splice(prevIndex, 1);
                setListData(newData);
                animationIsRunning.current = false;
            });
        }
    };

    const renderItem = data => (
        <Animated.View
            style={[
                styles.rowFrontContainer,
                {
                    height: rowTranslateAnimatedValues[
                        data.item.key
                    ].interpolate({
                        inputRange: [0, 1],
                        outputRange: [0, 50],
                    }),
                },
            ]}
        >
            <TouchableHighlight
                onPress={() => console.log('You touched me')}
                style={styles.rowFront}
                underlayColor={'#AAA'}
            >
                <View>
                    <Text>I am {data.item.text} in a SwipeListView</Text>
                </View>
            </TouchableHighlight>
        </Animated.View>
    );

    const renderHiddenItem = () => (
        <View style={styles.rowBack}>
            <View style={[styles.backRightBtn, styles.backRightBtnRight]}>
                <Text style={styles.backTextWhite}>Delete</Text>
            </View>
        </View>
    );

    return (
        <View style={styles.container}>
            <SwipeListView
                disableRightSwipe
                data={listData}
                renderItem={renderItem}
                renderHiddenItem={renderHiddenItem}
                rightOpenValue={-Dimensions.get('window').width}
                onSwipeValueChange={onSwipeValueChange}
                useNativeDriver={false}
            />
        </View>
    );
}

const styles = StyleSheet.create({
    container: {
        backgroundColor: 'white',
        flex: 1,
    },
    backTextWhite: {
        color: '#FFF',
    },
    rowFront: {
        alignItems: 'center',
        backgroundColor: '#CCC',
        borderBottomColor: 'black',
        borderBottomWidth: 1,
        justifyContent: 'center',
        height: 50,
    },
    rowBack: {
        alignItems: 'center',
        backgroundColor: 'red',
        flex: 1,
        flexDirection: 'row',
        justifyContent: 'space-between',
        paddingLeft: 15,
    },
    backRightBtn: {
        alignItems: 'center',
        bottom: 0,
        justifyContent: 'center',
        position: 'absolute',
        top: 0,
        width: 75,
    },
    backRightBtnRight: {
        backgroundColor: 'red',
        right: 0,
    },
});
```

```jsx
import React from 'react';
import { StyleSheet, Text, View } from 'react-native';
import { SwipeRow } from 'react-native-swipe-list-view';

export default function StandaloneRow() {
    return (
        <View style={styles.container}>
            <View style={styles.standalone}>
                <SwipeRow leftOpenValue={75} rightOpenValue={-75}>
                    <View style={styles.standaloneRowBack}>
                        <Text style={styles.backTextWhite}>Left</Text>
                        <Text style={styles.backTextWhite}>Right</Text>
                    </View>
                    <View style={styles.standaloneRowFront}>
                        <Text>I am standalone SwipeRow #1</Text>
                    </View>
                </SwipeRow>
                <View style={styles.spacer} />
                <SwipeRow leftOpenValue={75} rightOpenValue={-75}>
                    <View style={styles.standaloneRowBack}>
                        <Text style={styles.backTextWhite}>Left</Text>
                        <Text style={styles.backTextWhite}>Right</Text>
                    </View>
                    <View style={styles.standaloneRowFront}>
                        <Text>I am standalone SwipeRow #2</Text>
                    </View>
                </SwipeRow>
            </View>
        </View>
    );
}

const styles = StyleSheet.create({
    container: {
        backgroundColor: 'white',
        flex: 1,
    },
    standalone: {
        marginTop: 30,
        marginBottom: 30,
    },
    standaloneRowFront: {
        alignItems: 'center',
        backgroundColor: '#CCC',
        justifyContent: 'center',
        height: 50,
    },
    standaloneRowBack: {
        alignItems: 'center',
        backgroundColor: '#8BC645',
        flex: 1,
        flexDirection: 'row',
        justifyContent: 'space-between',
        padding: 15,
    },
    backTextWhite: {
        color: '#FFF',
    },
    spacer: {
        height: 50,
    },
});
```

```jsx
import React, { useState } from 'react';
import {
    StyleSheet,
    Text,
    TouchableOpacity,
    TouchableHighlight,
    View,
} from 'react-native';

import { SwipeListView } from 'react-native-swipe-list-view';

export default function SectionList() {
    const [listData, setListData] = useState(
        Array(5)
            .fill('')
            .map((_, i) => ({
                title: `title${i + 1}`,
                data: [
                    ...Array(5)
                        .fill('')
                        .map((_, j) => ({
                            key: `${i}.${j}`,
                            text: `item #${j}`,
                        })),
                ],
            }))
    );

    const closeRow = (rowMap, rowKey) => {
        if (rowMap[rowKey]) {
            rowMap[rowKey].closeRow();
        }
    };

    const deleteRow = (rowMap, rowKey) => {
        closeRow(rowMap, rowKey);
        const [section] = rowKey.split('.');
        const newData = [...listData];
        const prevIndex = listData[section].data.findIndex(
            item => item.key === rowKey
        );
        newData[section].data.splice(prevIndex, 1);
        setListData(newData);
    };

    const onRowDidOpen = rowKey => {
        console.log('This row opened', rowKey);
    };

    const renderItem = data => (
        <TouchableHighlight
            onPress={() => console.log('You touched me')}
            style={styles.rowFront}
            underlayColor={'#AAA'}
        >
            <View>
                <Text>I am {data.item.text} in a SwipeListView</Text>
            </View>
        </TouchableHighlight>
    );

    const renderHiddenItem = (data, rowMap) => (
        <View style={styles.rowBack}>
            <Text>Left</Text>
            <TouchableOpacity
                style={[styles.backRightBtn, styles.backRightBtnLeft]}
                onPress={() => closeRow(rowMap, data.item.key)}
            >
                <Text style={styles.backTextWhite}>Close</Text>
            </TouchableOpacity>
            <TouchableOpacity
                style={[styles.backRightBtn, styles.backRightBtnRight]}
                onPress={() => deleteRow(rowMap, data.item.key)}
            >
                <Text style={styles.backTextWhite}>Delete</Text>
            </TouchableOpacity>
        </View>
    );

    const renderSectionHeader = ({ section }) => <Text>{section.title}</Text>;

    return (
        <View style={styles.container}>
            <SwipeListView
                useSectionList
                sections={listData}
                renderItem={renderItem}
                renderHiddenItem={renderHiddenItem}
                renderSectionHeader={renderSectionHeader}
                leftOpenValue={75}
                rightOpenValue={-150}
                previewRowKey={'0'}
                previewOpenValue={-40}
                previewOpenDelay={3000}
                onRowDidOpen={onRowDidOpen}
            />
        </View>
    );
}

const styles = StyleSheet.create({
    container: {
        backgroundColor: 'white',
        flex: 1,
    },
    backTextWhite: {
        color: '#FFF',
    },
    rowFront: {
        alignItems: 'center',
        backgroundColor: '#CCC',
        borderBottomColor: 'black',
        borderBottomWidth: 1,
        justifyContent: 'center',
        height: 50,
    },
    rowBack: {
        alignItems: 'center',
        backgroundColor: '#DDD',
        flex: 1,
        flexDirection: 'row',
        justifyContent: 'space-between',
        paddingLeft: 15,
    },
    backRightBtn: {
        alignItems: 'center',
        bottom: 0,
        justifyContent: 'center',
        position: 'absolute',
        top: 0,
        width: 75,
    },
    backRightBtnLeft: {
        backgroundColor: 'blue',
        right: 75,
    },
    backRightBtnRight: {
        backgroundColor: 'red',
        right: 0,
    },
});
```

```jsx
import React, { useState } from 'react';
import {
    StyleSheet,
    Text,
    TouchableOpacity,
    TouchableHighlight,
    View,
} from 'react-native';

import { SwipeListView, SwipeRow } from 'react-native-swipe-list-view';

export default function PerRowConfig() {
    const [listData, setListData] = useState(
        Array(20)
            .fill('')
            .map((_, i) => ({ key: `${i}`, text: `item #${i}` }))
    );

    const closeRow = (rowMap, rowKey) => {
        if (rowMap[rowKey]) {
            rowMap[rowKey].closeRow();
        }
    };

    const deleteRow = (rowMap, rowKey) => {
        closeRow(rowMap, rowKey);
        const newData = [...listData];
        const prevIndex = listData.findIndex(item => item.key === rowKey);
        newData.splice(prevIndex, 1);
        setListData(newData);
    };

    const renderItem = (data, rowMap) => (
        <SwipeRow
            disableLeftSwipe={parseInt(data.item.key) % 2 === 0}
            leftOpenValue={20 + Math.random() * 150}
            rightOpenValue={-150}
        >
            <View style={styles.rowBack}>
                <Text>Left</Text>
                <TouchableOpacity
                    style={[styles.backRightBtn, styles.backRightBtnLeft]}
                    onPress={() => closeRow(rowMap, data.item.key)}
                >
                    <Text style={styles.backTextWhite}>Close</Text>
                </TouchableOpacity>
                <TouchableOpacity
                    style={[styles.backRightBtn, styles.backRightBtnRight]}
                    onPress={() => deleteRow(rowMap, data.item.key)}
                >
                    <Text style={styles.backTextWhite}>Delete</Text>
                </TouchableOpacity>
            </View>
            <TouchableHighlight
                onPress={() => console.log('You touched me')}
                style={styles.rowFront}
                underlayColor={'#AAA'}
            >
                <View>
                    <Text>I am {data.item.text} in a SwipeListView</Text>
                </View>
            </TouchableHighlight>
        </SwipeRow>
    );

    return (
        <View style={styles.container}>
            <SwipeListView data={listData} renderItem={renderItem} />
        </View>
    );
}

const styles = StyleSheet.create({
    container: {
        backgroundColor: 'white',
        flex: 1,
    },
    backTextWhite: {
        color: '#FFF',
    },
    rowFront: {
        alignItems: 'center',
        backgroundColor: '#CCC',
        borderBottomColor: 'black',
        borderBottomWidth: 1,
        justifyContent: 'center',
        height: 50,
    },
    rowBack: {
        alignItems: 'center',
        backgroundColor: '#DDD',
        flex: 1,
        flexDirection: 'row',
        justifyContent: 'space-between',
        paddingLeft: 15,
    },
    backRightBtn: {
        alignItems: 'center',
        bottom: 0,
        justifyContent: 'center',
        position: 'absolute',
        top: 0,
        width: 75,
    },
    backRightBtnLeft: {
        backgroundColor: 'blue',
        right: 75,
    },
    backRightBtnRight: {
        backgroundColor: 'red',
        right: 0,
    },
});
```

```jsx
import React, { useState, useRef } from 'react';
import {
    StyleSheet,
    Text,
    TouchableOpacity,
    TouchableHighlight,
    View,
} from 'react-native';

import { SwipeListView } from 'react-native-swipe-list-view';

export default function Basic() {
    const [listData] = useState(
        Array(20)
            .fill('')
            .map((_, i) => ({ key: `${i}`, text: `item #${i}` }))
    );
    const openRowRef = useRef(null);

    const onRowDidOpen = (rowKey, rowMap) => {
        openRowRef.current = rowMap[rowKey];
    };

    const closeOpenRow = () => {
        if (openRowRef.current && openRowRef.current.closeRow) {
            openRowRef.current.closeRow();
        }
    };

    const renderItem = data => (
        <TouchableHighlight
            onPress={() => console.log('You touched me')}
            style={styles.rowFront}
            underlayColor={'#AAA'}
        >
            <View>
                <Text>I am {data.item.text} in a SwipeListView</Text>
            </View>
        </TouchableHighlight>
    );

    const renderHiddenItem = () => (
        <View style={styles.rowBack}>
            <Text>Left</Text>
            <View style={[styles.backRightBtn, styles.backRightBtnLeft]}>
                <Text style={styles.backTextWhite}>Left</Text>
            </View>
            <View style={[styles.backRightBtn, styles.backRightBtnRight]}>
                <Text style={styles.backTextWhite}>Right</Text>
            </View>
        </View>
    );

    return (
        <View style={styles.container}>
            <SwipeListView
                data={listData}
                renderItem={renderItem}
                renderHiddenItem={renderHiddenItem}
                leftOpenValue={75}
                rightOpenValue={-150}
                previewRowKey={'0'}
                previewOpenValue={-40}
                previewOpenDelay={3000}
                onRowDidOpen={onRowDidOpen}
            />
            <TouchableOpacity onPress={closeOpenRow} style={styles.closeButton}>
                <Text>Close Open Row</Text>
            </TouchableOpacity>
        </View>
    );
}

const styles = StyleSheet.create({
    container: {
        backgroundColor: 'white',
        flex: 1,
    },
    backTextWhite: {
        color: '#FFF',
    },
    rowFront: {
        alignItems: 'center',
        backgroundColor: '#CCC',
        borderBottomColor: 'black',
        borderBottomWidth: 1,
        justifyContent: 'center',
        height: 50,
    },
    rowBack: {
        alignItems: 'center',
        backgroundColor: '#DDD',
        flex: 1,
        flexDirection: 'row',
        justifyContent: 'space-between',
        paddingLeft: 15,
    },
    backRightBtn: {
        alignItems: 'center',
        bottom: 0,
        justifyContent: 'center',
        position: 'absolute',
        top: 0,
        width: 75,
    },
    backRightBtnLeft: {
        backgroundColor: 'blue',
        right: 75,
    },
    backRightBtnRight: {
        backgroundColor: 'red',
        right: 0,
    },
    closeButton: {
        backgroundColor: 'white',
        bottom: 30,
        borderWidth: 1,
        borderRadius: 4,
        borderColor: 'black',
        padding: 15,
        position: 'absolute',
        right: 30,
    },
});
```

```jsx
import React, { useState } from 'react';
import {
    StyleSheet,
    Text,
    TouchableOpacity,
    TouchableHighlight,
    View,
} from 'react-native';

import { SwipeListView } from 'react-native-swipe-list-view';

export default function Basic() {
    const [listData, setListData] = useState(
        Array(20)
            .fill('')
            .map((_, i) => ({ key: `${i}`, text: `item #${i}` }))
    );

    const closeRow = (rowMap, rowKey) => {
        if (rowMap[rowKey]) {
            rowMap[rowKey].closeRow();
        }
    };

    const deleteRow = (rowMap, rowKey) => {
        closeRow(rowMap, rowKey);
        const newData = [...listData];
        const prevIndex = listData.findIndex(item => item.key === rowKey);
        newData.splice(prevIndex, 1);
        setListData(newData);
    };

    const onRowDidOpen = rowKey => {
        console.log('This row opened', rowKey);
    };

    const renderItem = data => (
        <TouchableHighlight
            onPress={() => console.log('You touched me')}
            style={styles.rowFront}
            underlayColor={'#AAA'}
        >
            <View>
                <Text>I am {data.item.text} in a SwipeListView</Text>
            </View>
        </TouchableHighlight>
    );

    const renderHiddenItem = (data, rowMap) => (
        <View style={styles.rowBack}>
            <Text>Left</Text>
            <TouchableOpacity
                style={[styles.backRightBtn, styles.backRightBtnLeft]}
                onPress={() => closeRow(rowMap, data.item.key)}
            >
                <Text style={styles.backTextWhite}>Close</Text>
            </TouchableOpacity>
            <TouchableOpacity
                style={[styles.backRightBtn, styles.backRightBtnRight]}
                onPress={() => deleteRow(rowMap, data.item.key)}
            >
                <Text style={styles.backTextWhite}>Delete</Text>
            </TouchableOpacity>
        </View>
    );

    return (
        <View style={styles.container}>
            <SwipeListView
                data={listData}
                renderItem={renderItem}
                renderHiddenItem={renderHiddenItem}
                leftOpenValue={75}
                rightOpenValue={-150}
                previewRowKey={'0'}
                previewOpenValue={-40}
                previewOpenDelay={3000}
                onRowDidOpen={onRowDidOpen}
            />
        </View>
    );
}

const styles = StyleSheet.create({
    container: {
        backgroundColor: 'white',
        flex: 1,
    },
    backTextWhite: {
        color: '#FFF',
    },
    rowFront: {
        alignItems: 'center',
        backgroundColor: '#CCC',
        borderBottomColor: 'black',
        borderBottomWidth: 1,
        justifyContent: 'center',
        height: 50,
    },
    rowBack: {
        alignItems: 'center',
        backgroundColor: '#DDD',
        flex: 1,
        flexDirection: 'row',
        justifyContent: 'space-between',
        paddingLeft: 15,
    },
    backRightBtn: {
        alignItems: 'center',
        bottom: 0,
        justifyContent: 'center',
        position: 'absolute',
        top: 0,
        width: 75,
    },
    backRightBtnLeft: {
        backgroundColor: 'blue',
        right: 75,
    },
    backRightBtnRight: {
        backgroundColor: 'red',
        right: 0,
    },
});
```

```jsx
import React, { useState } from 'react';
import {
    StyleSheet,
    Text,
    Image,
    Animated,
    TouchableOpacity,
    TouchableHighlight,
    View,
} from 'react-native';

import SwipeListView from '../SwipeListView';

export default function Actions() {
    const [listData, setListData] = useState(
        Array(20)
            .fill('')
            .map((_, i) => ({
                key: `${i}`,
                text: `item #${i}`,
                initialLeftActionState: i % 2 !== 0,
            }))
    );

    const closeRow = (rowMap, rowKey) => {
        if (rowMap[rowKey]) {
            rowMap[rowKey].closeRow();
        }
    };

    const deleteRow = (rowMap, rowKey) => {
        closeRow(rowMap, rowKey);
        const newData = [...listData];
        const prevIndex = listData.findIndex(item => item.key === rowKey);
        newData.splice(prevIndex, 1);
        setListData(newData);
    };

    const onRowDidOpen = rowKey => {
        console.log('This row opened', rowKey);
    };

    const onLeftActionStatusChange = rowKey => {
        console.log('onLeftActionStatusChange', rowKey);
    };

    const onRightActionStatusChange = rowKey => {
        console.log('onRightActionStatusChange', rowKey);
    };

    const onRightAction = rowKey => {
        console.log('onRightAction', rowKey);
    };

    const onLeftAction = rowKey => {
        console.log('onLeftAction', rowKey);
    };

    const VisibleItem = props => {
        console.log(props.leftActionState);

        const {
            rowHeightAnimatedValue,
            rightActionState,
            leftActionState,
            data,
            removeRow,
        } = props;

        if (rightActionState) {
            Animated.timing(rowHeightAnimatedValue, {
                toValue: 0,
                duration: 200,
            }).start(() => {
                removeRow();
            });
        }

        return (
            <Animated.View
                style={[
                    styles.rowFront,
                    { height: rowHeightAnimatedValue },
                    leftActionState && { backgroundColor: 'lightgreen' },
                ]}
            >
                <TouchableHighlight
                    onPress={() => console.log('You touched me')}
                    style={[
                        styles.rowFront,
                        leftActionState && {
                            backgroundColor: 'lightgreen',
                        },
                    ]}
                    underlayColor={'#AAA'}
                >
                    <View>
                        <Text>I am {data.item.text} in a SwipeListView</Text>
                    </View>
                </TouchableHighlight>
            </Animated.View>
        );
    };

    const renderItem = (data, rowMap) => {
        const rowHeightAnimatedValue = new Animated.Value(50);
        return (
            <VisibleItem
                rowHeightAnimatedValue={rowHeightAnimatedValue}
                data={data}
                removeRow={() => deleteRow(rowMap, data.item.key)}
            />
        );
    };

    const HiddenItemWithActions = props => {
        const {
            leftActionActivated,
            rightActionActivated,
            swipeAnimatedValue,
            rowActionAnimatedValue,
            rowHeightAnimatedValue,
            onClose,
            onDelete,
        } = props;

        if (rightActionActivated) {
            Animated.spring(rowActionAnimatedValue, {
                toValue: 500,
            }).start();
        } else {
            Animated.spring(rowActionAnimatedValue, {
                toValue: 75,
            }).start();
        }

        return (
            <Animated.View
                style={[
                    styles.rowBack,
                    { height: rowHeightAnimatedValue },
                    leftActionActivated && { backgroundColor: 'lightgreen' },
                ]}
            >
                <Text>Left</Text>
                {!leftActionActivated && (
                    <TouchableOpacity
                        style={[styles.backRightBtn, styles.backRightBtnLeft]}
                        onPress={onClose}
                    >
                        <Text style={styles.backTextWhite}>Close</Text>
                    </TouchableOpacity>
                )}
                {!leftActionActivated && (
                    <Animated.View
                        style={[
                            styles.backRightBtn,
                            styles.backRightBtnRight,
                            { flex: 1, width: rowActionAnimatedValue },
                        ]}
                    >
                        <TouchableOpacity
                            style={[
                                styles.backRightBtn,
                                styles.backRightBtnRight,
                            ]}
                            onPress={onDelete}
                        >
                            <Animated.View
                                style={[
                                    styles.trash,
                                    {
                                        transform: [
                                            {
                                                scale: swipeAnimatedValue.interpolate(
                                                    {
                                                        inputRange: [-90, -45],
                                                        outputRange: [1, 0],
                                                        extrapolate: 'clamp',
                                                    }
                                                ),
                                            },
                                        ],
                                    },
                                ]}
                            >
                                <Image
                                    source={require('../images/trash.png')}
                                    style={styles.trash}
                                />
                            </Animated.View>
                        </TouchableOpacity>
                    </Animated.View>
                )}
            </Animated.View>
        );
    };

    const renderHiddenItem = (data, rowMap) => {
        const rowActionAnimatedValue = new Animated.Value(75);
        const rowHeightAnimatedValue = new Animated.Value(50);
        return (
            <HiddenItemWithActions
                data={data}
                rowMap={rowMap}
                rowActionAnimatedValue={rowActionAnimatedValue}
                rowHeightAnimatedValue={rowHeightAnimatedValue}
                onClose={() => closeRow(rowMap, data.item.key)}
                onDelete={() => deleteRow(rowMap, data.item.key)}
            />
        );
    };

    return (
        <View style={styles.container}>
            <SwipeListView
                data={listData}
                renderItem={renderItem}
                renderHiddenItem={renderHiddenItem}
                onRowDidOpen={onRowDidOpen}
                leftOpenValue={75}
                rightOpenValue={-150}
                leftActivationValue={100}
                rightActivationValue={-200}
                leftActionValue={0}
                rightActionValue={-500}
                onLeftAction={onLeftAction}
                onRightAction={onRightAction}
                onLeftActionStatusChange={onLeftActionStatusChange}
                onRightActionStatusChange={onRightActionStatusChange}
            />
        </View>
    );
}

const styles = StyleSheet.create({
    container: {
        backgroundColor: 'white',
        flex: 1,
    },
    backTextWhite: {
        color: '#FFF',
    },
    rowFront: {
        alignItems: 'center',
        backgroundColor: '#CCC',
        borderBottomColor: 'black',
        borderBottomWidth: 1,
        justifyContent: 'center',
        height: 50,
        width: '100%',
    },
    rowBack: {
        alignItems: 'center',
        backgroundColor: '#DDD',
        flex: 1,
        flexDirection: 'row',
        justifyContent: 'space-between',
        paddingLeft: 15,
    },
    backRightBtn: {
        alignItems: 'flex-end',
        bottom: 0,
        justifyContent: 'center',
        position: 'absolute',
        top: 0,
        width: 75,
        paddingRight: 17,
    },
    backRightBtnLeft: {
        backgroundColor: 'blue',
        right: 75,
    },
    backRightBtnRight: {
        backgroundColor: 'red',
        right: 0,
    },
    trash: {
        height: 25,
        width: 25,
        marginRight: 7,
    },
});
```



## 兼容性

在以下版本验证通过

1. RNOH：0.72.13; SDK：HarmonyOS NEXT Developer Preview1; IDE：DevEco Studio 4.1.3.500; ROM：204.1.0.59;

## 属性

详情见[react-native-swipe-list-view](https://reactnative.dev/docs/drawerlayoutandroid)

# `SwipeListView`

| Name                                 | Description                                                  | Type     | Required | Platform      | HarmonyOS Support | note                                                         |
| ------------------------------------ | ------------------------------------------------------------ | -------- | -------- | ------------- | ----------------- | ------------------------------------------------------------ |
| data                                 | List of objects to be passed into the `renderItem` and `renderHiddenItem` functions. Each item must include a unique `key` property or `keyExtractor` must be implemented to ensure full functionality. | array    | YES      | Android IOS   | YES               |                                                              |
| useSectionList                       | Render list using React Native's `SectionList`               | bool     | YES      | Android IOS   | YES               |                                                              |
| renderItem                           | How to render a row in a FlatList. Should return a valid React Element. | func     | YES      | Android IOS   | YES               | { rowData: any, rowMap: { string: SwipeRowRef } } : ReactElement |
| renderHiddenItem                     | How to render a hidden row in a FlatList (renders behind the row). Should return a valid React Element. This is required unless `renderItem` returns a `<SwipeRow>` (see [Per Row Behavior](https://github.com/jemise111/react-native-swipe-list-view/blob/master/docs/per-row-behavior.md)). | func     | YES      | Android IOS   | YES               | { rowData: any, rowMap: { string: SwipeRowRef } } : ReactElement |
| leftOpenValue                        | TranslateX value for opening the row to the left (positive number) | number   | NO       | Android IOS   | YES               | 0                                                            |
| `rightOpenValue`                     | TranslateX value for opening the row to the right (negative number) | `number` | NO       | Android IOS   | YES               | 0                                                            |
| `leftActivationValue`                | TranslateX value for firing onLeftActionStatusChange (positive number) | `number` | NO       | Android       | NO                | The original library only does the function of Android       |
| `rightActivationValue`               | TranslateX value for firing onRightActionStatusChange (negative number) | `number` | NO       | Android IOS   | YES               |                                                              |
| `rightActionValue`                   | TranslateX value for right action to which the row will be shifted after gesture release | `number` | NO       | Android IOS   | YES               |                                                              |
| `initialLeftActionState`             | Initial value for left action state (default is false)       | `bool`   | NO       | Android IOS   | YES               |                                                              |
| `initialRightActionState`            | Initial value for right action state (default is false)      | `bool`   | NO       | Android IOS   | YES               |                                                              |
| `closeOnRowPress`                    | Should open rows be closed when a row is pressed             | `bool`   | NO       | `Android IOS` | YES               |                                                              |
| `closeOnRowOpen`                     | Should open rows be closed when another row is opened        | `bool`   | NO       | Android IOS   | YES               |                                                              |
| `closeOnRowBeginSwipe`               | Should open rows be closed when a row begins to swipe open   | `bool`   | NO       | `Android IOS` | YES               | false                                                        |
| `closeOnScroll`                      | Should open rows be closed when the listView begins scrolling | `bool`   | NO       | Android IOS   | YES               | true                                                         |
| `disableLeftSwipe`                   | Disable ability to swipe the row left                        | `bool`   | NO       | Android IOS   | YES               | false                                                        |
| `disableRightSwipe`                  | Disable ability to swipe the row right                       | `bool`   | NO       | Android IOS   | YES               | false                                                        |
| `stopLeftSwipe`                      | TranslateX value for stop the row to the left (positive number). This number is the stop value corresponding to the `leftOpenValue` (while the row is swiping in the right direction) | `number` | NO       | Android IOS   | YES               |                                                              |
| `stopRightSwipe`                     | TranslateX value for stop the row to the right (negative number). This number is the stop value corresponding to the `rightOpenValue` (while the row is swiping in the left direction) | `number` | NO       | Android IOS   | YES               |                                                              |
| `directionalDistanceChangeThreshold` | Change the sensitivity of the row                            | `number` | NO       | Android IOS   | YES               | `2`                                                          |
| `swipeToOpenPercent`                 | What % of the left/right openValue does the user need to swipe past to trigger the row opening. | `number` | NO       | Android IOS   | YES               | 50                                                           |
| `swipeToClosePercent`                | What % of the left/right openValue does the user need to swipe past to trigger the row closing. | `number` | NO       | Android IOS   | YES               | 50                                                           |
| `swipeToOpenVelocityContribution`    | Describes how much the ending velocity of the gesture affects whether the swipe will result in the item being closed or open. A velocity factor of 0 (the default) means that the velocity will have no bearing on whether the swipe settles on a closed or open position and it'll just take into consideration the swipeToOpenPercent. Ideal values for this prop tend to be between 5 and 15. | `number` | NO       | Android IOS   | YES               | 0                                                            |

# `SwipeRow `

|                 Name                 |                         Description                          |   Type   | Required | HarmonyOS Support |   Platform    | note                                                         |
| :----------------------------------: | :----------------------------------------------------------: | :------: | :------: | :---------------: | :-----------: | ------------------------------------------------------------ |
|          `closeOnRowPress`           |          Should the row be closed when it is tapped          |  `bool`  |   YES    |        YES        |  Android IOS  |                                                              |
| `directionalDistanceChangeThreshold` |              Change the sensitivity of the row               | `number` |   YES    |        YES        |  Android IOS  | 2                                                            |
|              `friction`              | Friction for the open / close animation. Controls "bounciness"/overshoot. https://facebook.github.io/react-native/docs/animated#spring | `number` |   YES    |        YES        |  Android IOS  | 7                                                            |
|              `tension`               | Tension for the open / close animation. Controls speed. https://facebook.github.io/react-native/docs/animated#spring | `number` |   YES    |        YES        | `Android IOS` | 40                                                           |
|         `restSpeedThreshold`         | RestSpeedThreshold for the open / close animation. Controls speed. https://facebook.github.io/react-native/docs/animated#spring | `number` |   YES    |        YES        | `Android IOS` | 0.001                                                        |
|     `restDisplacementThreshold`      | RestDisplacementThreshold for the open / close animation. Controls speed. https://facebook.github.io/react-native/docs/animated#spring | `number` |   YES    |        YES        |  Android IOS  | 0.001                                                        |
|           `leftOpenValue`            | TranslateX value for opening the row to the left (positive number) | `number` |   YES    |        YES        | `Android IOS` | 0                                                            |
|           `rightOpenValue`           | TranslateX value for opening the row to the right (negative number) | `number` |   YES    |        YES        | `Android IOS` | 0                                                            |
|        `leftActivationValue`         | TranslateX value for firing onLeftActionStatusChange (positive number) | `number` |   YES    |        YES        |  Android IOS  |                                                              |
|        `rightActivationValue`        | TranslateX value for firing onRightActionStatusChange (negative number) | `number` |   YES    |        YES        |  Android IOS  |                                                              |
|       `initialLeftActionState`       |    Initial value for left action state (default is false)    |  `bool`  |   YES    |        YES        |  Android IOS  |                                                              |
|      `initialRightActionState`       |   Initial value for right action state (default is false)    |  `bool`  |   YES    |        YES        |  Android IOS  |                                                              |
|          `leftActionValue`           | TranslateX value for left action to which the row will be shifted after gesture release | `number` |   YES    |        YES        |  Android IOS  |                                                              |
|          `rightActionValue`          | TranslateX value for right action to which the row will be shifted after gesture release | `number` |   YES    |        YES        |  Android IOS  |                                                              |
|           `stopLeftSwipe`            | TranslateX value for stop the row to the left (positive number). This number is the stop value corresponding to the `leftOpenValue` (while the row is swiping in the right direction) | `number` |   YES    |        YES        |  Android IOS  |                                                              |
|           `stopRightSwipe`           | TranslateX value for stop the row to the right (negative number). This number is the stop value corresponding to the `rightOpenValue` (while the row is swiping in the left direction) | `number` |   YES    |        YES        |  Android IOS  |                                                              |
|             `onRowPress`             |                 Called when row is pressed.                  |  `func`  |   YES    |        YES        |  Android IOS  | `{ } : void`                                                 |
|             `onRowOpen`              | Called when row is animating open. Used by the SwipeListView to keep references to open rows. |  `func`  |   YES    |        YES        |  Android IOS  | { toValue: number } : void                                   |
|            `onRowDidOpen`            |              Called when row has animated open               |  `func`  |   YES    |        YES        |  Android IOS  | { toValue: number } : void                                   |
|             `onRowClose`             |             Called when row is animating closed              |  `func`  |   YES    |        YES        |  Android IOS  | { } : void                                                   |
|           `onRowDidClose`            |         Called when a swipe row has animated closed          |  `func`  |   YES    |        YES        |  Android IOS  | { } : void                                                   |
|      `onLeftActionStatusChange`      | Called once when swipe value crosses the leftActivationValue |  `func`  |   YES    |        YES        |  Android IOS  | `{ data: { isActivated: boolean, value: number, key: string } } : void` |
|     `onRightActionStatusChange`      | Called once when swipe value crosses the rightActivationValue |  `func`  |   YES    |        YES        |  Android IOS  | `{ data: { isActivated: boolean, value: number, key: string } } : void` |
|            `onLeftAction`            |        Called when row shifted to leftActivationValue        |  `func`  |   YES    |        YES        |  Android IOS  | { } : void                                                   |
|           `onRightAction`            |       Called when row shifted to rightActivationValue        |  `func`  |   YES    |        YES        |  Android IOS  | { } : void                                                   |
|         `swipeToOpenPercent`         | What % of the left/right openValue does the user need to swipe past to trigger the row opening. | `number` |   YES    |        YES        |  Android IOS  | `50`                                                         |
|        `swipeToClosePercent`         | What % of the left/right openValue does the user need to swipe past to trigger the row closing. | `number` |   YES    |        YES        |  Android IOS  | 50                                                           |
|          `setScrollEnabled`          | Used by the SwipeListView to close rows on scroll events. You shouldn't need to use this prop explicitly. |  `func`  |   YES    |        YES        |  Android IOS  |                                                              |
|          `disableLeftSwipe`          |            Disable ability to swipe the row left             |  `bool`  |   YES    |        YES        |  Android IOS  | false                                                        |
|         `disableRightSwipe`          |            Disable ability to swipe the row right            |  `bool`  |   YES    |        YES        |  Android IOS  | false                                                        |
|      `recalculateHiddenLayout`       |    Enable hidden row onLayout calculations to run always     |  `bool`  |   YES    |        YES        | `Android IOS` | false                                                        |
|               `style`                |      Styles for the parent wrapper View of the SwipeRow      | `object` |   YES    |        YES        |  Android IOS  |                                                              |
|              `preview`               | Should the row do a slide out preview to show that it is swipeable |  `bool`  |   YES    |        YES        |  Android IOS  | false                                                        |
|          `previewDuration`           |         Duration of the slide out preview animation          | `number` |   YES    |        YES        |  Android IOS  | 300                                                          |
|           `previewRepeat`            |                 Should the animation repeat                  |  `bool`  |   YES    |        YES        |  Android IOS  | false                                                        |
|         `previewRepeatDelay`         |      Delay between each preview repeat in milliseconds       | `number` |   YES    |        YES        |  Android IOS  | 1000                                                         |
|          `previewOpenValue`          |     TranslateX value for the slide out preview animation     | `number` |   YES    |        YES        |  Android IOS  | 0.5 * props.rightOpenValue                                   |
|         `onSwipeValueChange`         | Callback invoked any time the translateX value of the row changes |  `func`  |   YES    |        YES        |  Android IOS  | { swipeData: { key: string, value: number, direction: 'left' |
|         `swipeGestureBegan`          |            Called when the row is animating swipe            |  `func`  |   YES    |        YES        |  Android IOS  | `{ } : void`                                                 |
|         `swipeGestureEnded`          |        Called when user has ended their swipe gesture        |  `func`  |   YES    |        YES        |  Android IOS  | { rowKey: string; data: { translateX: number; direction: 'left' |
|  `swipeToOpenVelocityContribution`   | Describes how much the ending velocity of the gesture affects whether the swipe will result in the item being closed or open. A velocity factor of 0 (the default) means that the velocity will have no bearing on whether the swipe settles on a closed or open position and it'll just take into consideration the swipeToOpenPercent. Ideal values for this prop tend to be between 5 and 15. | `number` |   YES    |        YES        | `Android IOS` | 0                                                            |
|          `shouldItemUpdate`          |    Callback to determine whether component should update     |  `func`  |   YES    |        YES        |  Android IOS  | { currentItem: any, newItem: any }                           |
|     `forceCloseToLeftThreshold`      | TranslateX amount(not value!) threshold that triggers force-closing the row to the Left End (positive number) | `number` |   YES    |        YES        |  Android IOS  |                                                              |
|     `forceCloseToRightThreshold`     | TranslateX amount(not value!) threshold that triggers force-closing the row to the Right End (positive number) | `number` |   YES    |        YES        |  Android IOS  |                                                              |
|         `onForceCloseToLeft`         |  Callback invoked when row is force closing to the Left End  |  `func`  |   YES    |        YES        |  Android IOS  |                                                              |
|        `onForceCloseToRight`         | Callback invoked when row is force closing to the Right End  |  `func`  |   YES    |        YES        |  Android IOS  |                                                              |
|       `onForceCloseToLeftEnd`        | Callback invoked when row has finished force closing to the Left End |  `func`  |   YES    |        YES        |  Android IOS  |                                                              |
|       `onForceCloseToRightEnd`       | Callback invoked when row has finished force closing to the Right End |  `func`  |   YES    |        YES        |  Android IOS  |                                                              |
|          `useNativeDriver`           |          useNativeDriver: `true` for all animations          |  `bool`  |   YES    |        YES        |  Android IOS  | true                                                         |
|              `swipeKey`              | Optional key to identify a standalone row, used in the `onSwipeValueChange` callback | `string` |   YES    |        YES        |  Android IOS  |                                                              |
|            `onPreviewEnd`            |    Callback that runs after row swipe preview is finished    |  `func`  |   YES    |        YES        |  Android IOS  | { } : void                                                   |



## 遗留问题

## 其他
