# react-native-wheel-picker
[![npm version](http://img.shields.io/npm/v/react-native-wheel-picker.svg?style=flat-square)](https://npmjs.org/package/react-native-wheel-picker "View this project on npm")
[![npm version](http://img.shields.io/npm/dm/react-native-wheel-picker.svg?style=flat-square)](https://npmjs.org/package/react-native-wheel-picker "View this project on npm")

## Introduction
Cross platform Picker component based on React-native.

Since picker is originally supported by ios while Android only supports a ugly Spinner component. If you want to have the same user behaviour, you can use this.

The android component is based on https://github.com/AigeStudio/WheelPicker which runs super fast and smoothly. It also supports curved effect which make it exactly the same looking and feel as the ios picker.
![](https://raw.githubusercontent.com/lesliesam/react-native-wheel-picker/master/demo.gif)
![](https://raw.githubusercontent.com/lesliesam/react-native-wheel-picker/master/demo_android.gif)

## How to use

Run command

For apps using RN 0.40 or higher, please run
```
npm i @gregfrench/react-native-wheel-picker --save
```
To link the project, please run
```
react-native link @gregfrench/react-native-wheel-picker
```

## Example code (using functional components)
```
import React, { useState } from 'react';
import { View, Text } from 'react-native';

import Picker from '@gregfrench/react-native-wheel-picker'
var PickerItem = Picker.Item;

const WheelPicker = () => {
  const [selectedItem, setSelectedItem ] = useState(2);
  const [itemList , setItemList ] = useState(['Item 1', 'Item 2', 'Item 3', 'Item 4', 'Item 5']);

  return (
    <View>
      <Text>
        <Picker style={{width: 150, height: 180}}
          selectedValue={selectedItem}
          itemStyle={{color:"black", fontSize:26}}
          onValueChange={(index) => setSelectedItem(index) }>
          {itemList.map((value, i) => (
            <PickerItem label={value} value={i} key={i}/>
          ))}
        </Picker>
      </Text>
    </View>
  );
};

export default WheelPicker;
```
## Example code (using classes)
```
import React, { Component } from 'react';
import { Text, View } from 'react-native';

import Picker from '@gregfrench/react-native-wheel-picker'
var PickerItem = Picker.Item;

export default class WheelPicker extends Component {

  constructor(props) {
    super(props);
    this.state = {
      selectedItem : 2,
      itemList: ['Item 1', 'Item 2', 'Item 3', 'Item 4', 'Item 5']
    };
  }

  onPickerSelect (index) {
    this.setState({
      selectedItem: index,
    });
  }

  onAddItem = () => {
    var name = 'New item';

    if (this.state.itemList.indexOf(name) == -1) {
      this.state.itemList.push(name);
    }

    this.setState({
      selectedItem: this.state.itemList.indexOf(name),
    });
  }

  render () {
    return (
      <View>
        <Picker style={{width: 150, height: 180}}
          selectedValue={this.state.selectedItem}
          itemStyle={{color:"black", fontSize:26}}
          onValueChange={(index) => this.onPickerSelect(index)}>
            {this.state.itemList.map((value, i) => (
                <PickerItem label={value} value={i} key={i}/>
            ))}
        </Picker>

        <Text style={{margin: 20}}>
          Selected item: {this.state.itemList[this.state.selectedItem]}
        </Text>

        <Text style={{margin: 20}} onPress={this.onAddItem}>
          Add item
        </Text>
      </View>
    );
  }
}
```
