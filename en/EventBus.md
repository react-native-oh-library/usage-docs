<!-- {% raw %} -->
Template version: v0.2.0

<p align="center">
  <h1 align="center"> <code>EventBus</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/krasimir/EventBus/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/krasimir/EventBus)

## Installation and Usage

Go to the project directory and execute the following instruction：

<!-- tabs:start -->

#### **npm**

```bash
npm i eventbusjs@0.2.0
```

#### **yarn**

```bash
yarn add eventbusjs@0.2.0
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository：

```tsx
import { useState, createContext } from "react";
import {
  View,
  Button,
  StyleSheet,
  ScrollView,
  Text,
  TextInput,
} from "react-native";
import EventBus from "eventbusjs";
import EventBus3 from "eventbusjs";
const TAG = "EventBus";
const MyContext = createContext("null");

const styles = StyleSheet.create({
  main: {
    height: "100%",
  },
  mainItem: {
    marginTop: 20,
  },
  container: {
    paddingTop: 10,
    paddingBottom: 10,
    paddingLeft: 20,
    paddingRight: 20,
  },
  box: {
    marginTop: 10,
    marginBottom: 10,
    marginLeft: 20,
    marginRight: 20,
    height: 100,
    borderWidth: 1,
    borderColor: "#000",
    overflow: "scroll",
  },
  title: {
    fontSize: 14,
    fontWeight: "bold",
  },
  inputWrap: {
    disPlay: "flex",
  },
  inputText: {
    width: "100%",
    height: 40,
    borderWidth: 1,
    borderColor: "gray",
    marginBottom: 10,
  },
});

function eventTest() {
  console.warn(`${TAG}-----,The eventTest event of type test_event is successfully dispatched`);
}

var TestParamsClass1 = function (this: any) {
  this.className = "TestParamsClass1";
  this.doSomeThing = function (
    event: Event,
    param1: number | string,
    param2: number | string,
  ) {
    console.warn(
      `${TAG}, className=${this.className},event=${JSON.stringify(event)},params=${param1}--${param2}`,
    );
  };
};
var TestParamsClass2 = function (this: any) {
  this.className = "TestParamsClass2";
  this.ready = function (param1: number | string, param2: number | string) {
    EventBus3.dispatch("custom_event", this, param1, param2);
  };
};
var p1 = new (TestParamsClass1 as any)();
var p2 = new (TestParamsClass2 as any)();

function EventBusDemo() {
  const [msg, setMsg] = useState("");
  const [msgParams, setMsgParams] = useState("");
  const [firstVal, setFirstVal] = useState("");
  const [secondVal, setSecondVal] = useState("");
  const [onOff, setOnOff] = useState(true);
  function handleAdd() {
    const has = EventBus.hasEventListener("test_event", eventTest, 0);
    if (has) {
      setMsg("There are already test_evnt types of eventTest events in eventBus");
      console.log(`${TAG}, There are already test_evnt types of eventTest events in eventBus`);
    } else {
      EventBus.addEventListener("test_event", eventTest, 0);
      setMsg("The eventTest event of type test_event is successfully added");
      console.log(`${TAG}, The eventTest event of type test_event is successfully added`);
    }
  }

  function handleHas() {
    let has = EventBus.hasEventListener("test_event", eventTest, 0);
    setMsg(
      has
        ? "An eventTest of type test_event exists"
        : "There is no eventTest event of type test_event",
    );
    console.log(
      `${TAG}, ${has ? "An eventTest of type test_event exists" : "There is no eventTest event of type test_event"}`,
    );
  }

  function handleRemove() {
    let has = EventBus.hasEventListener("test_event", eventTest, 0);
    if (has) {
      EventBus.removeEventListener("test_event", eventTest, 0);
      setMsg("The EventTest event of test_event type has been deleted");
      console.log(`${TAG}, The EventTest event of test_event type has been deleted`);
    } else {
      setMsg("No eventTest event of Test_event type");
      console.log(`${TAG}, No eventTest event of Test_event type`);
    }
  }

  function handleDispatch() {
    let has = EventBus.hasEventListener("test_event", eventTest, 0);
    if (has) {
      EventBus.dispatch("test_event");
      setMsg("The eventTest event of type test_event is successfully executed");
      console.log(`${TAG}, The eventTest event of type test_event is successfully executed`);
    } else {
      setMsg("test_event type of eventTest event has been deleted or no event found");
      console.log(`${TAG}, test_event type of eventTest event has been deleted or no event found`);
    }
  }

  function handleGet() {
    setMsg(`${JSON.stringify(EventBus.getEvents())}`);
    console.log(`${TAG}, ${JSON.stringify(EventBus.getEvents())}`);
  }

  function handleAddForParams() {
    let has = EventBus3.hasEventListener("custom_event", p1.doSomeThing, p1);
    if (has) {
      setMsgParams("P1.dosomething events in EventBus exist in P1.dosomething");
      console.log(
        `${TAG}, P1.dosomething events in EventBus exist in P1.dosomething`,
      );
    } else {
      if (firstVal.length <= 1 || secondVal.length <= 1) {
        console.error("Parameter length does not meet expectations");
      } else {
        EventBus3.addEventListener("custom_event", p1.doSomeThing, p1);
        setMsgParams("Successfully add the P1.dosomething event of Custom_Event type");
        console.log(`${TAG}, 'Successfully add the P1.dosomething event of Custom_Event type'`);
        setOnOff(true);
      }
    }
  }
  function handleDispatchForParams() {
    if (onOff) {
      let has = EventBus3.hasEventListener("custom_event", p1.doSomeThing, p1);
      if (has) {
        p2.ready(firstVal, secondVal);
        setMsgParams(`Dispatching the event succeeded，param1=${firstVal},param2=${secondVal}`);
        console.log(
          `${TAG}, Dispatching the event succeeded，param1=${firstVal},param2=${secondVal}`,
        );
        setOnOff(false);
      } else {
        setMsgParams(
          "The P1.Dosomething event of Custom_event type has been deleted or found not found",
        );
        console.log(
          `${TAG}, The P1.Dosomething event of Custom_event type has been deleted or found not found`,
        );
      }
    } else {
      setMsgParams("Please remove the old P1.Dosomething event first");
      console.log(`${TAG}, Please remove the old P1.Dosomething event first`);
    }
  }
  function handleRemoveForParams() {
    setOnOff(true);
    let has = EventBus3.hasEventListener("custom_event", p1.doSomeThing, p1);
    if (has) {
      EventBus3.removeEventListener("custom_event", p1.doSomeThing, p1);
      setMsgParams("Successfully delete the P1.dosomething event of Custom_Event type");
      console.log(`${TAG}, Successfully delete the P1.dosomething event of Custom_Event type`);
    } else {
      setMsgParams("The P1.dosomething event that did not find the Custom_Event type");
      console.log(`${TAG}, The P1.dosomething event that did not find the Custom_Event type`);
    }
  }
  return (
    <MyContext.Provider value={{ myGlobalVar: "" }}>
      <ScrollView style={styles.main}>
        <View style={styles.mainItem}>
          <Text style={styles.title}>Basic use & Keeping the scope</Text>
          <View style={styles.container}>
            <Button title="Add eventTest event" onPress={handleAdd}></Button>
          </View>
          <View style={styles.container}>
            <Button
              title="Distribute Eventtest event"
              onPress={handleDispatch}
            ></Button>
          </View>
          <View style={styles.container}>
            <Button title="Remove the EventTest event" onPress={handleRemove}></Button>
          </View>
          <View style={styles.container}>
            <Button
              title="Determine whether there is an eventTest event"
              onPress={handleHas}
            ></Button>
          </View>
          <View style={styles.container}>
            <Button
              title="Get all events (commonly used for debugging related)"
              onPress={handleGet}
            ></Button>
          </View>
          <View style={styles.box}>
            <Text style={{ color: "blue" }}>{msg}</Text>
          </View>
        </View>

        <View style={styles.mainItem}>
          <Text style={styles.title}>Passing additional parameters</Text>
          <View style={styles.container}>
            <View style={styles.inputWrap} flexDirection={"row"}>
              <TextInput
                onChangeText={(text) => setFirstVal(text)}
                style={styles.inputText}
                placeholder="Please enter a parameter with a length greater than 1"
                maxLength={12}
              />
              <TextInput
                onChangeText={(text) => setSecondVal(text)}
                style={styles.inputText}
                placeholder="Please enter a parameter with a length greater than 1"
                maxLength={12}
              />
            </View>
            <Button title="Add Dosomething event" onPress={handleAddForParams}>
              'add'
            </Button>
          </View>
          <View style={styles.container}>
            <Button
              title="Distribute Dosomething event"
              onPress={handleDispatchForParams}
            ></Button>
          </View>
          <View style={styles.container}>
            <Button
              title="Remove Dosomething incident"
              onPress={handleRemoveForParams}
            ></Button>
          </View>
          <View style={styles.box}>
            <Text style={{ color: "blue" }}>{msgParams}</Text>
          </View>
        </View>
      </ScrollView>
    </MyContext.Provider>
  );
}
export default EventBusDemo;
```

## Compatibility

This document is verified based on the following versions

1. RNOH：0.72.20; SDK：HarmonyOS NEXT Developer Preview2; IDE：DevEco Studio 5.0.3.200; ROM：205.0.0.18;

## API

See for details [EventBus](https://github.com/krasimir/EventBus/blob/master/README.md)

| Name                | Description | Required | HarmonyOS Support |
| ------------------- | ----------- | -------- | ----------------- |
| addEventListener    | -           | -        | YES               |
| removeEventListener | -           | -        | YES               |
| hasEventListener    | -           | -        | YES               |
| dispatch            | -           | -        | YES               |
| getEvents           | -           | -        | YES               |

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://www.mit-license.org/).

<!-- {% endraw %} -->