模板版本：v0.1.3

<p align="center">
  <h1 align="center"> <code>immer</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/reactjs/react-lifecycles-compat">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>



> [!TIP] [Github 地址](https://github.com/immerjs/immer)

## 安装与使用

进入到工程目录并输入以下命令：

>[!TIP] # 处替换为 tgz 包的路径

<!-- tabs:start -->

#### **npm**

```bash
npm immer@10.0.3
```

#### **yarn**

```bash
yarn add immer@10.0.3
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

```js
import React, {useState, useEffect} from 'react';
import {View, Text, Button, StyleSheet, ScrollView} from 'react-native';
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
class ShowComponent extends React.Component {
  state = {
    mapData: new Map(),
    setData: new Set(),
  };

  updateData = () => {
    this.setState(
      produce(draft => {
        draft.mapData.set('key', 'value');
        draft.setData.add('new item');
      }),
    );
  };

  render() {
    return (
      <View>
        <Button title="Update Data" onPress={this.updateData} />
        <Text>Map Data: {Array.from(this.state.mapData)}</Text>
        <Text>Set Data: {Array.from(this.state.setData)}</Text>
      </View>
    );
  }
}
const MyComponent = () => {
  let [states, setStates] = useState(false);
  const [originals, setOriginals] = useState({users: [{name: 'zhansan'}]});
  let [res, setRes] = useState('');
  let [currentText, setCurrent] = useState('');
  // ----------------------------------------------------
  const [count, setCount] = useState({age: 0});
  let [baseState, setBaseState] = useState([
    {
      title: '标题1',
      done: true,
    },
  ]);
  const [text, setText] = useState('Hello');
  let [result, setResult] = useState({});
  let [patches, setPatches] = useState({});
  let [inversePatches, setInversePatches] = useState({});
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
          draftState.push({title: '新增', done: false});
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
      draftState[e].title = '更改后数据';
      setStates((states = isDraft(draftState)));
    });
    setBaseState(res);
  };
  // ----------------------------------------------------
  const [state, setState] = useState(initialState);
  // 使用createDraft来创建一个草稿副本
  const increment = () => {
    const draft = createDraft(state);
    draft.count += 1; // 修改草稿副本
    // setCurrent(current(draft.count))
    const nextState = finishDraft(draft); // 获取修改后的不可变状态
    setState(nextState); // 更新React状态
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
      draft => (draft += ' World'),
    );
    setResult(result);
    setPatches(patches);
    setInversePatches(inversePatches);
    console.log('result:', result);
    console.log('Patches:', patches);
    console.log('Inverse Patches:', inversePatches);

    setText(result);
  };
  // ---------------------------------------------------------
  const [stateLeft, setStateLeft] = useState([
    {count: 0},
    {age: 17, name: 'zhansan'},
  ]);
  const [stateRight, setStateRight] = useState([
    {count: 0},
    {age: 17, name: 'zhansan'},
  ]);
  const [stateRes, setStateRes] = useState({count: 0});
  const [stateNothing, setStateNothing] = useState({
    name: 'John',
    age: 30,
    isStudent: false,
  });
  const [isDraftableList, setIsDraftableList] = useState({
    one: false,
    two: false,
    three: false,
  });
  class MyComponent extends React.Component {
    constructor(props) {
      super(props);

      // 设置immerable标志
      this[immerable] = true;

      this.state = {
        data: {
          count: 0,
          text: 'Hello Immer!',
          immerable: true,
        },
      };
    }

    incrementCount = () => {
      this.setState(
        produce(draft => {
          draft.data.count += 1;
          draft.data.text = 'hahhaha';
        }),
      );
    };

    render() {
      return (
        <View>
          <Text>Count: {this.state.data.count}</Text>
          <Text>text: {this.state.data.text}</Text>
          <Button title="Increment" onPress={this.incrementCount} />
        </View>
      );
    }
  }
  const [counter, setCounter] = useState<Immutable<number>>(0);
  // 在组件挂载时设置 immer 的自动冻结行为
  useEffect(() => {
    // 启用自动冻结
    setAutoFreeze(true);

    // 清理函数（可选），在这里我们不需要做任何清理工作
    return () => {
      // 如果需要，可以在这里禁用自动冻结
      setAutoFreeze(false);
    };
  }, []); // 空依赖数组确保此 effect 只运行一次
  // 使用 immer 的 freeze 函数来冻结状态对象
  freeze(stateLeft, true);
  freeze(stateRight, false);
  // 尝试修改冻结的对象将会失败，并且不会触发组件的重新渲染
  const tryToModifyFrozenStateLeft = () => {
    try {
      setStateRight(
        produce(pradft => {
          pradft[0].age = 20;
          pradft[0].name = 'Lisi';
        }),
      );
    } catch (error) {
      console.error('Error modifying frozen state:', error);
    }
  };
  const tryToModifyFrozenStateRight = () => {
    try {
      setStateRight(
        produce(pradft => {
          pradft[1].age = 20;
          pradft[1].name = 'Lisi';
        }),
      );
    } catch (error) {
      console.error('Error modifying frozen state:', error);
    }
  };
  const incrementCountLeft = () => {
    // 使用 setState 来安全地更新状态
    // setState(prevState => ({state[0].count: prevState[0].count + 1}));
    setStateLeft(
      produce(stateLeft, prevState => {
        prevState[0].count += 1;
      }),
    );
  };
  const incrementCountRight = () => {
    // 使用 setState 来安全地更新状态
    setStateRight(
      produce(stateRight, prevState => {
        prevState[0].count += 1;
      }),
    );
  };
  const ClickincrementCount = () => {
    // 使用 immer 的 produce 函数来安全地更新状态
    const nextState = produce(stateRes, draft => {
      draft.count += 1;
    });
    // 由于启用了自动冻结，nextState 现在是一个不可变对象
    try {
      // 尝试修改 nextState 将会失败，因为它已经被冻结了
      nextState.count = 100; // 这会抛出错误，因为 nextState 是不可变的
    } catch (error) {
      console.error('Error modifying frozen state:', error);
    }

    setStateRes(nextState);
  };
  const removeProperty = () => {
    const nextStateNothing = produce(stateNothing, draft => {
      draft.name = 'wangwu';
      // 使用 nothing 来删除 age 属性
      delete draft.age; // 传统的删除方法
      // 或者使用 immer 的 nothing 来达到相同的效果
      // draft.isStudent = nothing; // 这将删除 isStudent 属性
    });
    setStateNothing(nextStateNothing);
    console.log('stateNothing:', stateNothing);
    console.log('nextStateNothing:', typeof nextStateNothing.isStudent);
  };
  /*  useEffect(() => {
    console.log('Current state:', stateLeft);
  }, [stateLeft]); */
  const clickNothing = () => {
    const nextStateNothing = produce(stateNothing, draft => {
      draft.name = 'wangwu';
      // 使用 nothing 来删除 age 属性
      // 或者使用 immer 的 nothing 来达到相同的效果
      draft.isStudent = nothing; // 这将删除 isStudent 属性
    });
    setStateNothing(nextStateNothing);
    console.log('stateNothing:', stateNothing);
    console.log('nextStateNothing:', typeof nextStateNothing.isStudent);
  };
  const checkDraftability = () => {
    const arr = {
      one: isDraftable(stateRes),
      two: isDraftable('Hello, World!'),
      three: isDraftable(42),
    };
    setIsDraftableList(arr);
    console.log('Is state draftable?', isDraftable(stateRes)); // 应该输出 true
    console.log('Is string draftable?', isDraftable('Hello, World!')); // 应该输出 false
    console.log('Is number draftable?', isDraftable(42)); // 应该输出 false
    // ... 可以检查其他类型的值
  };
  const incrementCounter = () => {
    setCounter(produce(counter, draftCounter => (draftCounter += 10)));
  };
  // ------------------------------分割线--------------------------------------------------------------------
  const [data, setData] = useState({name: 'John', age: 30});
  const [produceStatus, setProduceStatus] = useState(false);
  const [castDraftState, setCastDraftState] = useState({
    count: 0,
  });
  const updateData = () => {
    let newData = {};
    if (!produceStatus) {
      newData = produce(data, draft => {
        draft.age += 1;
      });
    } else {
      newData = castImmutable(data, draft => {
        draft.age += 1;
      });
    }

    setData(newData);
    console.log('newData:', newData);
  };
  const Clickfn = () => {
    setProduceStatus(!produceStatus);
  };
  const AddFn = () => {
    // 使用immer的produce函数来创建一个新的状态副本
    const newState = produce(castDraftState, draftState => {
      // 在新状态副本中增加count的值
      draftState.count += 1;
    });

    // 使用castDraft函数确保新状态与原始状态不共享内存
    const nextState = castDraft(newState);
    // 更新状态
    setCastDraftState(nextState);
  };
  // ---------------分割--start-----------
  let originalRes = {
    name: '初始数据1',
    age: 18,
  };
  let fork = originalRes;
  // 用户在向导中所作的所有更改
  let changes = [];
  // 与向导中所做的所有更改相反
  let inverseChanges = [];
  let [obj1, setObj1] = useState({});
  let [obj2, setObj2] = useState({});
  const ClickChange = () => {
    fork = produce(
      fork,
      draft => {
        draft.age = 20;
      },
      // 产生的第三个参数是一个回调，patches 将从这里产生
      (patches, inversePatches) => {
        changes.push(...patches);
        inverseChanges.push(...inversePatches);
      },
    );
    // 同时，我们的原始状态被替换，例如
    // 从服务器收到了一些更改
    originalRes = produce(originalRes, draft => {
      draft.name = '更改后数据';
    });
  };
  const fn1 = () => {
    // 当向导完成（成功）后，我们可以将 fork 中的更改重播到新的状态！
    let originalRes2 = applyPatches(originalRes, changes);
    setObj1(originalRes2);
  };
  const fn2 = () => {
    // state 现在包含来自两个代码路径的更改！
    // 最后，即使在完成向导之后，用户也可能会改变主意并撤消他的更改......
    let originalRes3 = applyPatches(originalRes, inverseChanges);
    setObj2(originalRes3);
  };

  // ----------------分割 end-------------
  return (
    <ScrollView style={{height: '100%'}}>
      <View style={styles.container}>
        <Text style={styles.text}>Immer</Text>
        {/* 验证---produce---api */}
        <View style={styles.container}>
          <Text style={styles.text}>验证-produce-期望值不可变数据可以更改</Text>
          <View
            style={{
              flexDirection: 'row',
              margin: 5,
              justifyContent: 'space-between',
              width: '60%',
            }}>
            <Button title="计数加+" onPress={incrementCount} />
            <Text style={{fontSize: 20}}>Count: {count.age}</Text>
            <Button title="计数减-" onPress={decrement} />
          </View>
          <Button title="添加" onPress={onAdd} />
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
                  <Text>标题：{item.title}</Text>
                  <Text>状态:{item.done ? 'true' : 'false'}</Text>
                  <Text>isDraft状态:{`${states}`}</Text>
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
                    title="更改"
                    onPress={() => {
                      onChange(item, index);
                    }}
                  />
                  <Button
                    title="删除"
                    onPress={() => {
                      onDelete(index);
                    }}
                  />
                </View>
              </View>
            ))}
          </View>
        </View>
        {/* --------验证----createDraft--&--finishDraft---------------- */}
        <View style={styles.container}>
          <Text style={styles.text}>验证createDraft--&--finishDraft</Text>
          <Text>Count: {state.count}</Text>
          <Text>Text: {state.text}</Text>
          <Button title="Increment" onPress={increment} />
          <Button title="Change Text" onPress={changeText} />
        </View>
        {/* -----------------验证--original-------current--------------- */}
        <View style={styles.container}>
          <Text style={styles.text}>
            验证original--current--期望值验证original:获取修改后的原始状态
          </Text>
          <Text>初始数据：{JSON.stringify(originals)}</Text>
          <Text>original:{res}</Text>
          <Text>res:{originals.users[0].name}</Text>
          <Text>current: {currentText}</Text>
          <Button title="original" onPress={clickOriginal} />
        </View>
        {/* ------enablePatches-----produceWithPatches------------------ */}
        <View style={styles.container}>
          <Text style={styles.text}>验证enablePatches--produceWithPatches</Text>
          <Text>{text}</Text>
          <Text>result:{JSON.stringify(result)}</Text>
          <Text>patches:{JSON.stringify(patches)}</Text>
          <Text>inversePatches:{JSON.stringify(inversePatches)}</Text>
          <Button title="Add World" onPress={handleClick} />
        </View>
        {/* ----------验证--enableMapSet------------------------------- */}
        <View style={styles.container}>
          <Text style={styles.text}>验证enableMapSet</Text>
          <ShowComponent>123</ShowComponent>
        </View>
        {/* ------------------------------------- */}
        {/* -----------------验证--freeze----------------------- */}
        <View style={styles.container}>
          <Text style={styles.text}>验证freeze</Text>
          <View style={{flexDirection: 'row', justifyContent: 'space-evenly'}}>
            <View style={{alignItems: 'center'}}>
              <View style={{flexDirection: 'row'}}>
                <Text>freez开</Text>
              </View>
              <Text>Count: {stateLeft[0].count}</Text>
              <Text>age: {stateLeft[1].age}</Text>
              <Text>name: {stateLeft[1].name}</Text>
              <Button title="Increment" onPress={incrementCountLeft} />
              <Button
                title="Try to change"
                onPress={tryToModifyFrozenStateLeft}
              />
            </View>
            <View>
              <View style={{}}>
                <View style={{flexDirection: 'row'}}>
                  <Text>freez关</Text>
                </View>
                <Text>Count: {stateRight[0].count}</Text>
                <Text>age: {stateRight[1].age}</Text>
                <Text>name: {stateRight[1].name}</Text>
                <Button title="IncrementLeft" onPress={incrementCountRight} />
                <Button
                  title="changeLeft"
                  onPress={tryToModifyFrozenStateRight}
                />
              </View>
            </View>
          </View>
        </View>
        {/* --------------验证--setAutoFreeze------------------- */}
        <View style={styles.container}>
          <Text style={styles.text}>---验证setAutoFreeze----</Text>
          <Text>setAutoFreeze为自动冻结,默认为true</Text>
          <Text>Current Count: {stateRes.count}</Text>
          <Button title="Increment Count" onPress={ClickincrementCount} />
        </View>
        {/* --------------验证---nothing------------------------ */}
        <View style={styles.container}>
          <Text style={styles.text}>验证nothing</Text>
          <Text>Name: {stateNothing.name}</Text>
          {stateNothing.age !== undefined ? (
            <Text>Age: {stateNothing.age}</Text>
          ) : null}
          {typeof stateNothing.isStudent == 'boolean' ? (
            <Text>Is Student: {stateNothing.isStudent ? 'Yes' : 'No'}</Text>
          ) : null}
          <View style={{flexDirection: 'row'}}>
            <View style={{marginRight: 10}}>
              <Text>期望age属性删除</Text>
              <Button title="delete删除" onPress={removeProperty} />
            </View>
            <View>
              <Text>期望is student属性删除</Text>
              <Button title="nothing删除" onPress={clickNothing} />
            </View>
          </View>
        </View>
        {/* -----------验证----isDraftable---------------------- */}
        <View style={styles.container}>
          <Text style={styles.text}>验证isDraftable</Text>
          <Text>
            state:{isDraftableList.one ? 'true' : 'false'}----期望值为true
          </Text>
          <Text>
            Hello, World:{isDraftableList.two ? 'true' : 'false'}----期望值false
          </Text>
          <Text>
            42:{isDraftableList.three ? 'true' : 'false'}----期望值false
          </Text>
          <Button title="Check Draftability" onPress={checkDraftability} />
        </View>
        {/* -----------验证---immerable-------------------- */}
        <View style={styles.container}>
          <Text style={styles.text}>验证---immerable,期望可以改变值</Text>
          <MyComponent />
        </View>
        {/* ----------------验证---Immutable<T>----------- */}
        <View style={styles.container}>
          <Text style={styles.text}>验证--Immutable--</Text>
          <Text>Counter: {counter}</Text>
          <Button title="Increment" onPress={incrementCounter} />
        </View>
        {/* -----------------验证--castImmutable----------------------- */}
        <View style={styles.container}>
          <Text style={styles.text}>验证castImmutable</Text>
          <Text>castImmutable,期望值castImmutable为true时数据不可变</Text>
          <Text>castImmutable:{produceStatus ? 'true' : 'false'}</Text>
          <Button title="castImmutable status" onPress={Clickfn} />
          <Text>Age: {data.age}</Text>
          <Button title="Update Age" onPress={updateData} />
        </View>
        {/* -------------------验证--castDraft--- */}
        <View style={styles.container}>
          <Text style={styles.text}>验证castDraft</Text>
          <Text>
            castDraft,期望值使用castDraft函数确保新状态与原始状态不共享内存
          </Text>
          <Text>Count: {castDraftState.count}</Text>
          <Button title="Increment" onPress={AddFn} />
        </View>
        {/* ---------------验证--applyPatches-------------- */}
        <View style={styles.container}>
          <Text style={styles.text}>验证applyPatches</Text>
          <Text>初始数据：{JSON.stringify(originalRes)}</Text>
          <Button title="改变初始值" onPress={ClickChange} />
          <Button title="fn1" onPress={fn1} />
          <Text>改变后数据：{JSON.stringify(obj1)}</Text>
          <Button title="fn2" onPress={fn2} />
          <Text>恢复的数据--{JSON.stringify(obj2)}</Text>
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

## 兼容性

在以下版本验证通过

1. RNOH：0.72.13; SDK：HarmonyOS NEXT Developer Preview1; IDE：DevEco Studio 4.1.3.500; ROM：204.1.0.59;

## API

> | Name                      | Description                                                  | Required | Platform    | HarmonyOS Support |
> | ------------------------- | ------------------------------------------------------------ | -------- | ----------- | ----------------- |
> | `(default)`               | Immer 核心 API，通常命名为 `produce`: `import {produce} from "immer"` | NO       | Android IOS | YES               |
> | `applyPatches`            | 给定一个基本 state 或 draft，以及一组 patches ，应用 patches | NO       | Android IOS | YES               |
> | `castDraft`               | 将任何不可变类型转换为其可变对应物。这只是一个转换，实际上并没有做任何事情。 | NO       | Android IOS | YES               |
> | `castImmutable`           | 将任何可变类型转换为其不可变对应物。这只是一个转换，实际上并没有做任何事情。 | NO       | Android IOS | YES               |
> | `createDraft`             | 给定一个基本 state，创建一个可变 draft，任何修改都将被记录下来 | NO       | Android IOS | YES               |
> | `current`                 | 给定一个 draft 对象（不必是对象的根结点），对 draft 的当前状态进行快照 | NO       | Android IOS | YES               |
> | `Draft<T>`                | 暴露的 TypeScript 类型以将不可变类型转换为可变类型           | NO       | Android IOS | YES               |
> | `enableMapSet()`          | 启用对 `Map` 和 `Set` 集合的支持。                           | NO       | Android IOS | YES               |
> | `enablePatches()`         | 启用对 JSON patches 的支持                                   | NO       | Android IOS | YES               |
> | `finishDraft`             | 给定使用 `createDraft` 创建的 draft，冻结 draft 并生成并返回下一个不可变状态，该状态捕获所有更改 | NO       | Android IOS | YES               |
> | `freeze(obj, deep?)`      | 冻结可 draft 对象。返回原始对象。默认情况下浅冻结，但如果第二个参数为真，它将递归冻结。 | NO       | Android IOS | YES               |
> | `Immer`                   | 可用于创建第二个“immer”实例（暴露此实例中列出的所有 API）的构造函数，它不与全局实例共享其设置 | NO       | Android IOS | YES               |
> | `immerable`               | 可以添加到构造函数或原型的符号，表示 Immer 应该将类视为可以安全 draft 的东西 | NO       | Android IOS | YES               |
> | `Immutable<T>`            | 暴露的 TypeScript 类型以将可变类型转换为不可变类型           | NO       | Android IOS | YES               |
> | `isDraft`                 | 如果给定对象是 draft 对象，则返回 true                       | NO       | Android IOS | YES               |
> | `isDraftable`             | 如果 Immer 能够将此对象变成 draft，则返回 true。这适用于：数组、没有原型的对象、以 `Object` 为原型的对象、在其构造函数或原型上具有 `immerable` 符号的对象 | NO       | Android IOS | YES               |
> | `nothing`                 | 可以从 recipe 返回的值，以指示应生成 `undefined`             | NO       | Android IOS | YES               |
> | `original`                | 给定一个 draft 对象（不必是对象的根结点），返回原始状态树中相同路径的原始对象（如果存在） | NO       | Android IOS | YES               |
> | `Patch`                   | 暴露的 TypeScript 类型，描述（反向）patches 对象的形状       | NO       | Android IOS | YES               |
> | `produce`                 | Immer 的核心 API，也暴露为 `default` 导出                    | NO       | Android IOS | YES               |
> | `produceWithPatches`      | 与 `produce` 相同，但它不仅返回生成的对象，还返回一个由 `[result, patch, inversePatches]` 组成的元组 | NO       | Android IOS | YES               |
> | `setAutoFreeze`           | 启用/禁用递归的自动冻结。默认启用                            | NO       | Android IOS | YES               |
> | `setUseStrictShallowCopy` | 可用于启用严格浅拷贝，如果启用，immer将尽可能多地复制不可枚举属性 | NO       | Android IOS | YES               |

## 遗留问题

## 其他
