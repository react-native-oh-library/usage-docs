> Template version: v0.2.1

<p align="center">
  <h1 align="center"> <code>immer</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/immerjs/immer/blob/main/LICENSE">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/immerjs/immer/blob/main/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [Github address](https://github.com/immerjs/immer)

## Installation and Usage

Go to the project directory and execute the following instruction:


<!-- tabs:start -->

#### **npm**

```bash
npm i immer@10.0.4
```

#### **yarn**

```bash
yarn add immer@10.0.4
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

```js
import React, {useState, useEffect, Component} from 'react';
import {
  View,
  Text,
  Button,
  StyleSheet,
  ScrollView,
  Switch,
  TextInput,
} from 'react-native';
import {
  createDraft,
  finishDraft,
  current,
  produce,
  original,
  isDraft,
  enablePatches,
  produceWithPatches,
  enableMapSet,
  freeze,
  nothing,
  setAutoFreeze,
  isDraftable,
  immerable,
  Immutable,
  castImmutable,
  castDraft,
  applyPatches,
  setUseStrictShallowCopy,
} from 'immer';

// 初始状态
const initialState = {
  count: 0,
  text: 'Hello from Immer!',
};
enablePatches();

// 启用enablePatches插件
enableMapSet();
// 启用enableMapSet插件
setUseStrictShallowCopy(true);

const MyComponent = () => {
  const [myMap, setMyMap] = useState(new Map([['key1', 'value1']]));
  const [overStates, setOverStates] = useState(false);
  const toggleSwitch = value => {
    setOverStates(value);
  };
  let [states, setStates] = useState(false);
  const [originals, setOriginals] = useState({users: [{name: 'zhansan'}]});
  let [res, setRes] = useState('');
  let [currentText, setCurrent] = useState('');
  const [count, setCount] = useState({age: 0});
  let [baseState, setBaseState] = useState([
    {
      title: 'Title1',
      done: true,
    },
  ]);
  const [text, setText] = useState('Hello');
  let [result, setResult] = useState({});
  let [patches, setPatches] = useState({});
  let [inversePatches, setInversePatches] = useState({});
  const [data, setData] = useState({name: 'John', age: 30});
  const [produceStatus, setProduceStatus] = useState(false);
  const [castDraftState, setCastDraftState] = useState({
    count: 0,
  });
  const [state, setState] = useState(initialState);
  const [freezeRest, setFreezeRest] = useState({a: 1, b: {c: 2}});
  const [stateRes, setStateRes] = useState({count: 0, text: 'hello-world'});
  const [texts, setTexts] = useState('Please enter your content');
  const [stateNothing, setStateNothing] = useState({
    name: 'John',
    age: 30,
    isStudent: false,
  });
  const obj = {a: 1, b: 2};
  const arr = [1, 2, 3];
  const str = 'Hello, immer!';
  const num = 42;
  const frozenObj = freeze({c: 3}, true);
  const [objStatus, setObjStatus] = useState(false);
  const [arrStatus, setArrStatus] = useState(false);
  const [strStatus, setStrStatus] = useState(false);
  const [numStatus, setNumStatus] = useState(false);
  const [draftsStatus, setDratfStatus] = useState(false);
  let originalRes = {
    name: 'Initial data 1',
    age: 18,
  };
  let fork = originalRes;
  // 用户在向导中所作的所有更改
  let changes = [];
  // 与向导中所做的所有更改相反
  let inverseChanges = [];
  let [obj1, setObj1] = useState({});
  let [obj2, setObj2] = useState({});
  const incrementCount = () => {
    if (count.age < 3) {
      setCount(
        produce(count, draft => {
          draft.age += 1;
        }),
      );
    } else {
      setCount(
        produce(count, draft => {
          draft.age = 0;
        }),
      );
    }
  };
  const decrement = () => {
    if (count.age > 0) {
      setCount(
        produce(count, draft => {
          draft.age -= 1;
        }),
      );
    } else {
      setCount(
        produce(count, draft => {
          draft.age = 3;
        }),
      );
    }
  };
  const onAdd = () => {
    if (baseState.length < 3) {
      return setBaseState(
        produce(baseState, draftState => {
          draftState.push({title: 'Add', done: states});
          setStates((states = isDraft(draftState)));
        }),
      );
    }
  };
  const onDelete = (e: number) => {
    return setBaseState(
      produce(draft => {
        draft.splice(e, 1);
      }),
    );
  };
  const onChange = (item: object, e: number) => {
    const res = produce(baseState, draftState => {
      draftState[e].done = !draftState[e].done;
      draftState[e].title = 'Updated Data';
      setStates((states = isDraft(draftState)));
    });
    setBaseState(res);
  };
  // 使用createDraft来创建一个草稿副本
  const increment = () => {
    const draft = createDraft(state);
    if (state.count < 5) {
      draft.count += 1; // 修改草稿副本
    } else {
      draft.count = 0;
    }
    const nextState = finishDraft(draft); // 获取修改后的不可变状态
    setState(nextState); // 更新React状态
  };
  const updateMap = () => {
    setMyMap(
      produce(myMap, draftMap => {
        draftMap.set('key1', 'updatedValue1'); // 更新键值对
        draftMap.set('key2', 'value2'); // 添加新的键值对
        draftMap.delete('key3'); // 尝试删除一个不存在的键值对（不会有影响）
      }),
    );
  };
  const renderMapEntries = () => {
    return Array.from(myMap.entries()).map(([key, value]) => (
      <Text key={key}>
        {key}: {value}
      </Text>
    ));
  };
  const changeText = () => {
    const draft = createDraft(state);
    draft.text = 'Text updated!'; // 修改草稿副本
    const nextState = current(draft); // 获取当前修改后的状态（与finishDraft效果相同）
    setState(nextState); // 更新React状态
  };
  const clickOriginal = () => {
    const a = setOriginals(
      produce(originals, draft => {
        draft.users[0].name = '4444';
        setCurrent(current(draft).users[0].name);
        console.log('Original state:', original(draft)?.users[0].name); // 输出原始状态
        setRes(original(draft).users[0].name);
      }),
    );
  };
  const handleClick = () => {
    const [result, patches, inversePatches] = produceWithPatches(
      text,
      draft => (draft = 'Hello-World'),
    );
    setResult(result);
    setPatches(patches);
    setInversePatches(inversePatches);
    console.log('result:', result);
    console.log('Patches:', patches);
    console.log('Inverse Patches:', inversePatches);

    setText(result);
  };
  // -----------------------------------------------
  class MyImmerableObject extends React.Component {
    // 声明immerable属性，告诉immer处理哪些属性
    static [immerable] = true;
    // 定义您的对象的属性
    constructor(name, age) {
      super(name, age);
      this.name = name;
      this.age = age;
    }
    /* // 不使用immerable
    // 声明immerable属性，告诉immer处理哪些属性
    static [immerable] = true;
    // 定义您的对象的属性
    constructor(name, age) {
      super(name, age);
      this.name = name;
      this.age = age;
    } */
  }
  const [myState, setMyState] = useState(new MyImmerableObject('Alice', 10));
  const updateValue = () => {
    // 使用immerable
    const res = produce(myState, draft => {
      draft.age = 26;
    });
    /*  // 不使用immerable
    const res = {...myState, age: 26}; */
    setMyState(res);
  };
  // 在组件挂载时设置 immer 的自动冻结行为
  useEffect(() => {
    // 启用/停用自动冻结
    setAutoFreeze(overStates);
  }, [overStates]); // 空依赖数组确保此 effect 只运行一次
  const incrementCountLeft = () => {
    const res = freeze(Object.assign({}, freezeRest), true);
    res.a = 110;
    res.b.c = 220;
    console.log('invoke freeze-deep:', overStates, res);
    setFreezeRest(res);
  };
  const tryToModifyFrozenStateLeft = () => {
    const res = freeze(Object.assign({}, freezeRest), false);
    res.a = 111;
    res.b.c = 222;
    console.log('invoke freeze-deep:', overStates, res);
    setFreezeRest(res);
  };
  const ClickOffFreeze = () => {
    const res1 = Object.assign({}, freezeRest);
    res1.a = 10;
    res1.b.c = 20;
    console.log('not invoke freeze:', res);
    setFreezeRest(res1);
  };
  const ClickOnFreeze = () => {
    const res = freeze(Object.assign({}, freezeRest));
    res.a = 11;
    res.b.c = 22;
    console.log('invoke freeze:', res);
    setFreezeRest(res);
  };
  const inputText = e => {
    let nextState = produce(stateRes, draft => {});
    setTexts(e);
    nextState.text = e;
    setStateRes(nextState);
  };
  const clickNothing = e => {
    const nextStateNothing = produce(stateNothing, draft => e);
    setStateNothing(nextStateNothing);
  };
  const isDraftObj = () => {
    setObjStatus(isDraftable(obj));
  };
  const isDraftArr = () => {
    setArrStatus(isDraftable(arr));
  };
  const isDraftStr = () => {
    setStrStatus(isDraftable(str));
  };
  const isDraftNum = () => {
    setNumStatus(isDraftable(num));
  };
  const isDrafts = () => {
    setDratfStatus(isDraftable(frozenObj));
  };
  // --------------------------------------------
  const [draftRes, setDraftRes] = useState({
    name: 'John',
    age: 30,
    hobbies: ['reading', 'coding'],
  });

  const [setUseStrictShallowCopyRes, setSetUseStrictShallowCopyRes] = useState({
    name: 'John',
    age: 30,
    address: {
      city: 'New York',
      country: 'USA',
    },
  });
  const [setUseStrictShallowCopyInit, setSetUseStrictShallowCopyInit] =
    useState();
  const updateData = () => {
    let newData = {};
    if (!produceStatus) {
      newData = produce(data, draft => {
        if (draft.age < 40) {
          draft.age += 1;
        } else {
          draft.age = 0;
        }
      });
    } else {
      newData = castImmutable(data, draft => {
        draft.age += 1;
      });
    }

    setData(newData);
  };
  const Clickfn = () => {
    setProduceStatus(!produceStatus);
  };
  const AddFn = () => {
    setCastDraftState(
      produce(castDraftState, draftState => {
        if (castDraftState.count < 10) {
          draftState.count += 1;
        } else {
          draftState.count = 0;
        }
      }),
    );
  };
  const doubleCount = () => {
    setCastDraftState(
      produce(castDraftState, draftState => {
        if (castDraftState.count < 100) {
          draftState.count *= 2;
        } else {
          draftState.count = 0;
        }
      }),
    );
  };
  const resetCount = () => {
    const newState = castDraft({count: 0});
    setCastDraftState(newState);
  };
  const ClickChange = () => {
    fork = produce(
      fork,
      draft => {
        draft.age = 10;
        draft.name = 'lisi';
      },
      // 产生的第三个参数是一个回调，patches 将从这里产生
      (patches, inversePatches) => {
        changes.push(...patches);
        inverseChanges.push(...inversePatches);
      },
    );
  };
  const fn1 = () => {
    // 当向导完成（成功）后，我们可以将 fork 中的更改重播到新的状态！
    let originalRes2 = applyPatches(originalRes, changes);
    setObj1(originalRes2);
    console.log('originalRes2:', originalRes2);
  };
  const fn2 = () => {
    // state 现在包含来自两个代码路径的更改！
    // 最后，即使在完成向导之后，用户也可能会改变主意并撤消他的更改......
    let originalRes3 = applyPatches(originalRes, inverseChanges);
    setObj2(originalRes3);
  };
  const handleAddHobby = () => {
    //不使用Draft<T>
    const newDraftRes = {...draftRes};
    newDraftRes.hobbies[1] = 'swimming';
    setDraftRes(newDraftRes);
    // 使用Draft<T>
    /*  const nextDraftRes = produce(draftRes, draft => {
      draft.hobbies[1] = 'swimming';
    });
    setDraftRes(nextDraftRes); */
  };
  interface Person {
    name: string;
    age: number;
  }
  // 使用Immutable<T>
  const immutableObj1: Immutable<Person> = {
    name: 'Alice',
    age: 20,
  };
  // 不使用Immutable<T>
  // const immutableObj1 = {
  //   name: 'Alice',
  //   age: 20,
  // };
  const [immutableData, setImmutableData] = useState();
  const changeObj1 = () => {
    const res = immutableObj1;
    res.name = 'lisi';
    console.log('immutableObj1:', immutableObj1);
    setImmutableData(res);
  };
  const useSetUseStrictShallowCopy = () => {
    const res = produce(setUseStrictShallowCopyRes, draft => {
      draft.age = 55;
      draft.address.city = 'China';
    });
    console.log('res:', JSON.stringify(res));
    console.log(
      'setSetUseStrictShallowCopyRes:',
      JSON.stringify(setUseStrictShallowCopyRes),
    );
    setSetUseStrictShallowCopyInit(res);
  };

  // ----------------分割 end-------------
  return (
    <ScrollView style={{height: '100%'}}>
      <View style={styles.container}>
        <Text style={styles.text}>Immer</Text>
        {/* verify ---produce---api */}
        <View style={styles.container}>
          <Text style={styles.text}>verify -produce- Expectation immutable data can be changed</Text>
          <View
            style={{
              flexDirection: 'row',
              margin: 5,
              justifyContent: 'space-between',
              width: '60%',
            }}>
            <Button title="Count +" onPress={incrementCount} />
            <Text style={{fontSize: 20}}>Count: {count.age}</Text>
            <Button title="Count -" onPress={decrement} />
          </View>
          <Button title="Add" onPress={onAdd} />
          <View
            style={{
              width: '100%',
            }}>
            {baseState.map((item, index) => (
              <View
                style={{
                  borderWidth: 1,
                  margin: 3,
                  display: 'flex',
                  justifyContent: 'space-between',
                  flexDirection: 'row',
                }}
                key={index}>
                <View style={{width: '70%'}}>
                  <Text>Title:{item.title}</Text>
                  <Text>State:{item.done ? 'true' : 'false'}</Text>
                  <Text>isDraft state:{`${states}`}</Text>
                </View>
                <View
                  style={{
                    flexDirection: 'row',
                    flex: 1,
                    height: '100%',
                    justifyContent: 'space-evenly',
                    alignItems: 'center',
                  }}>
                  <Button
                    title="Update"
                    onPress={() => {
                      onChange(item, index);
                    }}
                  />
                  <Button
                    title="Delete"
                    onPress={() => {
                      onDelete(index);
                    }}
                  />
                </View>
              </View>
            ))}
          </View>
        </View>
        {/* --------verify ----createDraft--&--finishDraft---------------- */}
        <View style={styles.container}>
          <Text style={styles.text}>verify createDraft--&--finishDraft</Text>
          <Text>Count: {state.count}</Text>
          <Text>Text: {state.text}</Text>
          <Button title="Increment" onPress={increment} />
          <Button title="Change Text" onPress={changeText} />
        </View>
        {/* -----------------verify --original-------current--------------- */}
        <View style={styles.container}>
          <Text style={styles.text}>
            verify original--current--Expected value verify original: obtains the original state after the modification
          </Text>
          <Text>Initial data：{JSON.stringify(originals)}</Text>
          <Text>original:{res}</Text>
          <Text>res:{originals.users[0].name}</Text>
          <Text>current: {currentText}</Text>
          <Button title="original" onPress={clickOriginal} />
        </View>
        {/* ------enablePatches-----produceWithPatches------------------ */}
        <View style={styles.container}>
          <Text style={styles.text}>verify enablePatches--produceWithPatches</Text>
          <Text>{text}</Text>
          <Text>result:{JSON.stringify(result)}</Text>
          <Text>patches:{JSON.stringify(patches)}</Text>
          <Text>inversePatches:{JSON.stringify(inversePatches)}</Text>
          <Button title="Add World" onPress={handleClick} />
        </View>
        {/* ----------verify --enableMapSet------------------------------- */}
        <View style={styles.container}>
          <Text style={styles.text}>verify enableMapSet</Text>
          <Text>Current Map:</Text>
          {renderMapEntries()}
          <Button title="Update Map" onPress={updateMap} />
        </View>
        {/* -----------------verify --freeze----------------------- */}
        <View style={styles.container}>
          <Text style={styles.text}>verify freeze</Text>
          <Text>
            freeze(obj,deep?)obj：Object to be frozen deep (optional): A boolean value, defaults to false. If true, the object is deep frozen, including all of its nested objects. If false or not provided, only the top-level properties of the object are frozen
          </Text>
          <View style={{flexDirection: 'row', justifyContent: 'space-evenly'}}>
            <View style={{alignItems: 'center'}}>
              <Text>init:{JSON.stringify(freezeRest)}</Text>
              <Button
                title="not invoke freeze ,changing the data : init a=10 c=20"
                onPress={ClickOffFreeze}
              />
              <Button
                title="invoke freeze ,changing the data : init a=11 c=22"
                onPress={ClickOnFreeze}
              />
              <Button
                title="when the state of deep is false ,changing the data : init a=110 c=220"
                onPress={tryToModifyFrozenStateLeft}
              />
              <Button
                title="when the state of deep is true ,changing the data : init a=110 c=220"
                onPress={incrementCountLeft}
              />
            </View>
          </View>
        </View>
        {/* --------------verify --setAutoFreeze------------------- */}
        <View style={styles.container}>
          <Text style={styles.text}>---verify setAutoFreeze----</Text>
          <Text>
            setAutoFreeze is freeze, state：{JSON.stringify(overStates)}
          </Text>
          <Switch onValueChange={toggleSwitch} value={overStates} />
          <TextInput
            style={{height: 40, borderColor: 'gray', borderWidth: 1}}
            onChangeText={inputText}
            value={texts}
          />
          <Text>What you entered: {stateRes.text}</Text>
          <Text>Current Count: {JSON.stringify(stateRes)}</Text>
        </View>
        {/* --------------verify ---nothing------------------------ */}
        <View style={styles.container}>
          <Text style={styles.text}>verify nothing</Text>
          <Text>
            Defined data:
            {JSON.stringify(stateNothing)}
          </Text>
          <Text>Name: {typeof stateNothing}</Text>
          <View style={{flexDirection: 'row'}}>
            <View style={{marginRight: 10}}>
              <Button
                title="mark nothing"
                onPress={() => {
                  clickNothing(nothing);
                }}
              />
            </View>
            <View>
              <Button
                title="mark undefined"
                onPress={() => {
                  clickNothing(undefined);
                }}
              />
            </View>
          </View>
        </View>
        {/* -----------verify ----isDraftable---------------------- */}
        <View style={styles.container}>
          <Text style={styles.text}>verify isDraftable</Text>
          {/* <Button title="Check Draftability" onPress={checkDraftability} />
          <Text>{result ? '可变对象' : '不可变对象'}</Text> */}
          <View style={{flexDirection: 'row', alignItems: 'center'}}>
            <Text>state--isDraftable({JSON.stringify(obj)})</Text>
            <Button title="isDraftObj" onPress={isDraftObj} />
            <Text>state:{JSON.stringify(objStatus)}</Text>
          </View>
          <View style={{flexDirection: 'row', alignItems: 'center'}}>
            <Text>state--isDraftable({JSON.stringify(arr)})</Text>
            <Button title="isDraftArr" onPress={isDraftArr} />
            <Text>state--{JSON.stringify(arrStatus)}</Text>
          </View>
          <View style={{flexDirection: 'row', alignItems: 'center'}}>
            <Text>state--isDraftable({JSON.stringify(str)})</Text>
            <Button title="isDraftStr" onPress={isDraftStr} />
            <Text>state--{JSON.stringify(strStatus)}</Text>
          </View>
          <View style={{flexDirection: 'row', alignItems: 'center'}}>
            <Text>state--isDraftable({JSON.stringify(num)})</Text>
            <Button title="isDraftNum" onPress={isDraftNum} />
            <Text>state--{JSON.stringify(numStatus)}</Text>
          </View>
          <View style={{flexDirection: 'row', alignItems: 'center'}}>
            <Text>state--isDraftable({JSON.stringify(frozenObj)})</Text>
            <Button title="isDrafts" onPress={isDrafts} />
            <Text>state--{JSON.stringify(draftsStatus)}</Text>
          </View>
        </View>
        {/* -----------verify ---immerable-------------------- */}
        <View style={styles.container}>
          <Text style={styles.text}>
            verify ---immerable,Symbols that can be added to constructors or prototypes
          </Text>
          <Text>NUM:{JSON.stringify(myState)}</Text>
          <Button title="Update Value" onPress={updateValue} />
        </View>
        {/* -----------------verify --castImmutable----------------------- */}
        <View style={styles.container}>
          <Text style={styles.text}>verify castImmutable</Text>
          <Text>castImmutable,If the expected castImmune is true, the data is immutable</Text>
          <Text>castImmutable:{produceStatus ? 'true' : 'false'}</Text>
          <Button title="castImmutable status" onPress={Clickfn} />
          <Text>Age: {data.age}</Text>
          <Button title="Update Age" onPress={updateData} />
        </View>
        {/* -------------------verify --castDraft--- */}
        <View style={styles.container}>
          <Text style={styles.text}>verify castDraft</Text>
          <Text>
            castDraft, Expect any immutable type to be converted to its mutable counterpart. It's just a conversion and doesn't actually do anything
          </Text>
          <Text>Count: {castDraftState.count}</Text>
          <Button title="AddFn" onPress={AddFn} />
          <Button title="doubleCount" onPress={doubleCount} />
          <Button title="resetCount" onPress={resetCount} />
        </View>
        {/* ---------------verify --applyPatches-------------- */}
        <View style={styles.container}>
          <Text style={styles.text}>verify applyPatches</Text>
          <Text>Initial data:{JSON.stringify(originalRes)}</Text>
          <Button title="改变初始值age=10" onPress={ClickChange} />
          <Button title="fn1" onPress={fn1} />
          <Text>Updated data:{JSON.stringify(obj1)}</Text>
          <Button title="fn2" onPress={fn2} />
          <Text>Recovered data:{JSON.stringify(obj2)}</Text>
        </View>
        <View style={styles.container}>
          <Text style={styles.text}>
            verify the TypeScript type exposed by Draft to convert an immutable type to a soft type
          </Text>
          <Text>{JSON.stringify(draftRes)}</Text>
          <Button title="add--use Draft<T>" onPress={handleAddHobby} />
        </View>
        {/* verify Immutable<T> */}
        {/*   <View style={styles.container}>
          <Text style={styles.text}>
            verify Immutable暴露的 TypeScript 类型以将可变类型转换为不可变类型
          </Text>
          <Text>初始数据：{JSON.stringify(immutableObj1)}</Text>
          <Text>更改后数据:{JSON.stringify(immutableData)}</Text>
          <Button title="change" onPress={changeObj1} />
        </View> */}
        {/* verify setUseStrictShallowCopy */}
        <View style={styles.container}>
          <Text style={styles.text}>
            verify setUseStrictShallowCopy
            It can be used to enable strict shallow copy, and if enabled, immer will ensure that the original object is not accidentally modified
          </Text>
          <Text>Initial data:{JSON.stringify(setUseStrictShallowCopyRes)}</Text>
          <Text>Updated data:{JSON.stringify(setUseStrictShallowCopyInit)}</Text>
          <Button title="use" onPress={useSetUseStrictShallowCopy} />
        </View>
      </View>
    </ScrollView>
  );
};

const styles = StyleSheet.create({
  container: {
    width: '100%',
    justifyContent: 'center',
    alignItems: 'center',
    padding: 10,
    marginBottom: 5,
    borderWidth: 1,
  },
  text: {
    width: '100%',
    fontSize: 18,
    marginBottom: 0,
    textAlign: 'center',
    fontWeight: '700',
    margin: 5,
  },
  border: {
    borderWidth: 1,
  },
});

export default MyComponent;


```

## Compatibility

This document is verified based on the following versions:

1. RNOH：0.72.20; SDK：HarmonyOS NEXT Developer Preview2; IDE：DevEco Studio 5.0.3.200; ROM：205.0.0.18;

## API

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

> | Name                      | Description                                                                                                                                               | Required | Type | Platform    | HarmonyOS Support |
> | ------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | ----------- | ----------------- | ----------------- |
> | (default)              | Immer Core API, usually named produce: import {produce} from "immer"                                                                                     | NO       | Function | Android IOS | YES               |
> | applyPatches            | Given a basic state or draft, as well as a set of patches, apply patches                                                                                             | NO       | Function | Android IOS | YES               |
> | castDraft               | Convert any immutable type to its mutable counterpart. This is just a conversion, and in fact, nothing has been done.                                                                              | NO       | Function | Android IOS | YES               |
> | castImmutable           | Convert any mutable type to its immutable counterpart. This is just a conversion, and in fact, nothing has been done.                                                                              | NO       | Function | Android IOS | YES               |
> | createDraft             | Given a basic state, create a variable draft, and any modifications will be recorded                                                                                            | NO       | Function | Android IOS | YES               |
> | current                 | Given a draft object (not necessarily the root node of the object), take a snapshot of the current state of the draft                                                                                    | NO       | Function | Android IOS | YES               |
> | Draft<T>                | Exposed TypeScript types to convert immutable types to mutable types                                                                                                        | NO       | Function | Android IOS | YES               |
> | enableMapSet()          | Enable support for Map and Set collections.                                                                                                                        | NO       | Function | Android IOS | YES               |
> | enablePatches()         | Enable support for JSON patches                                                                                                                                | NO       | Function | Android IOS | YES               |
> | finishDraft             | Given a draft created using createDraft, freeze the draft and generate and return the next immutable state, which captures all changes                                                         | NO       | Function | Android IOS | YES               |
> | freeze(obj, deep?)     | Freeze draftable objects. Return the original object. By default, it freezes lightly, but if the second parameter is true, it will recursively freeze.                                                                   | NO       | Function | Android IOS | YES               |
> | Immer                   | Constructor that can be used to create a second "immer" instance (exposing all APIs listed in this instance), which does not share its settings with the global instance                                                            | NO       | Function | Android IOS | YES               |
> | immerable               | Constructor that can be used to create a second "immer" instance (exposing all APIs listed in this instance), which does not share its settings with the global instance                                                                              | NO       | Function | Android IOS | YES               |
> | Immutable<T>            | Exposed TypeScript types to convert mutable types to immutable classes                                                                                                        | NO       | Function | Android IOS | YES               |
> | isDraft                 | If the given object is a draft object, return true                                                                                                                    | NO       | Function | Android IOS | YES               |
> | isDraftable             | If Immer is able to turn this object into a draft, return true. This applies to: arrays, objects without prototypes, objects with prototypes based on Object, objects with 'immerable' symbols on their constructors or prototypes | NO       | Function | Android IOS | YES               |
> | nothing                 | The value that can be returned from the recipe to indicate that it should be generated undefined                                                                                                          | NO       | Function | Android IOS | YES               |
> | original                | Given a draft object (not necessarily the root node of the object), return the original object with the same path in the original state tree (if it exists)                                                                | NO       | Function | Android IOS | YES               |
> | Patch                   | Exposed TypeScript type, describing (reverse) the shape of patches object                                                                                                    | NO       | Function | Android IOS | YES               |
> | produce                 | The core API of Immer is also exposed as a default export                                                                                                                 | NO       | Function | Android IOS | YES               |
> | produceWithPatches      | Same as product , but it not only returns the generated object, but also a tuple composed of [result, patch, invertPatches]                                                      | NO       | Function | Android IOS | YES               |
> | setAutoFreeze           | Enable/disable recursive automatic freezing. Default enabled                                                                                                                         | NO       | Function | Android IOS | YES               |
> | setUseStrictShallowCopy | Can be used to enable strict shallow copying, if enabled, the importer will replicate as many non enumerable attributes as possible                                                                                         | NO       | Function | Android IOS | YES               |

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/immerjs/immer/blob/main/LICENSE), Please enjoy and participate freely in open source.