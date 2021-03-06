---
id: version-0.63-vibration
title: Vibration
original_id: vibration
---

##### 本文档贡献者：[sunnylqm](https://github.com/search?q=sunnylqm%40qq.com+in%3Aemail&type=Users)(100.00%)

Vibrates the device.

## Example

<div class="toggler">
  <ul role="tablist" class="toggle-syntax">
    <li id="functional" class="button-functional" aria-selected="false" role="tab" tabindex="0" aria-controls="functionaltab" onclick="displayTabs('syntax', 'functional')">
      函数组件示例
    </li>
    <li id="classical" class="button-classical" aria-selected="false" role="tab" tabindex="0" aria-controls="classicaltab" onclick="displayTabs('syntax', 'classical')">
      Class组件示例
    </li>
  </ul>
</div>

<block class="functional syntax" />

```SnackPlayer name=Vibration&supportedPlatforms=ios,android
import React from "react";
import { Button, Platform, Text, Vibration, View, SafeAreaView, StyleSheet } from "react-native";

const Separator = () => {
  return <View style={Platform.OS === "android" ? styles.separator : null} />;
}

const App = () => {

  const ONE_SECOND_IN_MS = 1000;

  const PATTERN = [
    1 * ONE_SECOND_IN_MS,
    2 * ONE_SECOND_IN_MS,
    3 * ONE_SECOND_IN_MS
  ];

  const PATTERN_DESC =
    Platform.OS === "android"
      ? "wait 1s, vibrate 2s, wait 3s"
      : "wait 1s, vibrate, wait 2s, vibrate, wait 3s";

  return (
    <SafeAreaView style={styles.container}>
      <Text style={[styles.header, styles.paragraph]}>Vibration API</Text>
      <View>
        <Button title="Vibrate once" onPress={() => Vibration.vibrate()} />
      </View>
      <Separator />
      {Platform.OS == "android"
        ? [
            <View>
              <Button
                title="Vibrate for 10 seconds"
                onPress={() => Vibration.vibrate(10 * ONE_SECOND_IN_MS)}
              />
            </View>,
            <Separator />
          ]
        : null}
      <Text style={styles.paragraph}>Pattern: {PATTERN_DESC}</Text>
      <Button
        title="Vibrate with pattern"
        onPress={() => Vibration.vibrate(PATTERN)}
      />
      <Separator />
      <Button
        title="Vibrate with pattern until cancelled"
        onPress={() => Vibration.vibrate(PATTERN, true)}
      />
      <Separator />
      <Button
        title="Stop vibration pattern"
        onPress={() => Vibration.cancel()}
        color="#FF0000"
      />
    </SafeAreaView>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: "center",
    paddingTop: 44,
    padding: 8
  },
  header: {
    fontSize: 18,
    fontWeight: "bold",
    textAlign: "center"
  },
  paragraph: {
    margin: 24,
    textAlign: "center"
  },
  separator: {
    marginVertical: 8,
    borderBottomColor: "#737373",
    borderBottomWidth: StyleSheet.hairlineWidth
  }
});

export default App;
```

<block class="classical syntax" />

```SnackPlayer name=Vibration&supportedPlatforms=ios,android
import React, { Component } from "react";
import { Button, Platform, Text, Vibration, View, SafeAreaView, StyleSheet } from "react-native";

const Separator = () => {
  return <View style={Platform.OS === "android" ? styles.separator : null} />;
}

class App extends Component {
  render() {
    const ONE_SECOND_IN_MS = 1000;

    const PATTERN = [
      1 * ONE_SECOND_IN_MS,
      2 * ONE_SECOND_IN_MS,
      3 * ONE_SECOND_IN_MS
    ];

    const PATTERN_DESC =
      Platform.OS === "android"
        ? "wait 1s, vibrate 2s, wait 3s"
        : "wait 1s, vibrate, wait 2s, vibrate, wait 3s";

    return (
      <SafeAreaView style={styles.container}>
        <Text style={[styles.header, styles.paragraph]}>Vibration API</Text>
        <View>
          <Button title="Vibrate once" onPress={() => Vibration.vibrate()} />
        </View>
        <Separator />
        {Platform.OS == "android"
          ? [
              <View>
                <Button
                  title="Vibrate for 10 seconds"
                  onPress={() => Vibration.vibrate(10 * ONE_SECOND_IN_MS)}
                />
              </View>,
              <Separator />
            ]
          : null}
        <Text style={styles.paragraph}>Pattern: {PATTERN_DESC}</Text>
        <Button
          title="Vibrate with pattern"
          onPress={() => Vibration.vibrate(PATTERN)}
        />
        <Separator />
        <Button
          title="Vibrate with pattern until cancelled"
          onPress={() => Vibration.vibrate(PATTERN, true)}
        />
        <Separator />
        <Button
          title="Stop vibration pattern"
          onPress={() => Vibration.cancel()}
          color="#FF0000"
        />
      </SafeAreaView>
    );
  }
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: "center",
    paddingTop: 44,
    padding: 8
  },
  header: {
    fontSize: 18,
    fontWeight: "bold",
    textAlign: "center"
  },
  paragraph: {
    margin: 24,
    textAlign: "center"
  },
  separator: {
    marginVertical: 8,
    borderBottomColor: "#737373",
    borderBottomWidth: StyleSheet.hairlineWidth
  }
});

export default App;
```

<block class="endBlock syntax" />

> Android apps should request the `android.permission.VIBRATE` permission by adding `<uses-permission android:name="android.permission.VIBRATE"/>` to `AndroidManifest.xml`.

> The Vibration API is implemented as a `AudioServicesPlaySystemSound(kSystemSoundID_Vibrate)` call on iOS.

---

# Reference

## Methods

### `vibrate()`

```jsx
Vibration.vibrate(?pattern: number | Array<number>, ?repeat: boolean)
```

Triggers a vibration with a fixed duration.

**On Android,** the vibration duration defaults to 400 milliseconds, and an arbitrary vibration duration can be specified by passing a number as the value for the `pattern` argument. **On iOS,** the vibration duration is fixed at roughly 400 milliseconds.

The `vibrate()` method can take a `pattern` argument with an array of numbers that represent time in milliseconds. You may set `repeat` to true to run through the vibration pattern in a loop until `cancel()` is called.

**On Android,** the odd indices of the `pattern` array represent the vibration duration, while the even ones represent the separation time. **On iOS,** the numbers in the `pattern` array represent the separation time, as the vibration duration is fixed.

**Parameters:**

| Name    | Type             | Required | Description                                                | Platform     |
| ------- | ---------------- | -------- | ---------------------------------------------------------- | ------------ |
| pattern | number           | No       | Vibration duration in milliseconds. Defaults to 400 ms.    | Android      |
| pattern | Array of numbers | No       | Vibration pattern as an array of numbers in milliseconds.  | Android, iOS |
| repeat  | boolean          | No       | Repeat vibration pattern until cancel(), default to false. | Android, iOS |

---

### `cancel()`

```jsx
Vibration.cancel();
```

Call this to stop vibrating after having invoked `vibrate()` with repetition enabled.
