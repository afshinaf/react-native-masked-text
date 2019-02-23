# react-native-masked-text

![downloads](https://img.shields.io/npm/dt/react-native-masked-text.svg)
[![Help Contribute to Open Source](https://www.codetriage.com/benhurott/react-native-masked-text/badges/users.svg)](https://www.codetriage.com/benhurott/react-native-masked-text)

![logo](docs/res/logo.png)

This is a simple masked text (normal text and input text) component for React-Native.

## Supported Versions

React-native: 0.32.0 or higher

## Install

`npm install react-native-masked-text --save`

## Usage (TextInputMask)

For all the masks you will use in this way:

```jsx
import { TextInputMask } from 'react-native-masked-text'


//...

<TextInputMask
    type={'type-of-the-mask'}
    options={{
        // the options for your mask if needed
    }}
    value={this.state.text}
    onChangeText={text => {
      this.setState({
        text: text,
      })
    }}
    style={textInputStype}
/>
```


### Cel Phone

Mask:

* default: `(99) 9999-9999` or `(99) 99999-9999`
* international: `+999 999 999 999`

Sample code ([source](https://github.com/benhurott/react-native-masked-text-samples/blob/master/ReactNativeMaskedTextSamples/Samples/CelPhone.js)):

```jsx

```


### CPF

Mask: `999.999.999-99`

Sample code ([source](https://github.com/benhurott/react-native-masked-text-samples/blob/master/ReactNativeMaskedTextSamples/Samples/Cpf.js)):

```jsx
import React from 'react'
import { View, Text } from 'react-native'
import { TextInputMask } from 'react-native-masked-text'

import { textInputStype, container } from './styles'

export default class MyScreen extends React.Component {
  constructor(props) {
    super(props)

    this.state = {
      cpf: ''
    }
  }

  render() {
    return (
      <View style={container}>
        <Text>CPF</Text>
        <TextInputMask
          type={'cpf'}
          value={this.state.cpf}
          onChangeText={text => {
            this.setState({
              cpf: text
            })
          }}
          style={textInputStype}
        />
      </View>
    )
  }
}
```

### CNPJ

Mask: `99.999.999/9999-99`

Sample code ([source](https://github.com/benhurott/react-native-masked-text-samples/blob/master/ReactNativeMaskedTextSamples/Samples/Cnpj.js)):

```jsx
import React from 'react'
import { View, Text } from 'react-native'
import { TextInputMask } from 'react-native-masked-text'

import { textInputStype, container } from './styles'

export default class MyScreen extends React.Component {
  constructor(props) {
    super(props)

    this.state = {
      cnpj: ''
    }
  }

  render() {
    return (
      <View style={container}>
        <Text>CNPJ</Text>
        <TextInputMask
          type={'cnpj'}
          value={this.state.cnpj}
          onChangeText={text => {
            this.setState({
              cnpj: text
            })
          }}
          style={textInputStype}
        />
      </View>
    )
  }
}
```

### Credit Card

Mask:

* visa or master: `9999 9999 9999 9999` or `9999 **** **** 9999` (obfuscated)
* amex: `9999 999999 99999` or `9999 ****** 99999` (obfuscated)
* diners: `9999 999999 9999` or `9999 ****** 9999` (obfuscated)

Sample code ([source](https://github.com/benhurott/react-native-masked-text-samples/blob/master/ReactNativeMaskedTextSamples/Samples/CreditCard.js))

```jsx
import React from 'react'
import { View, Text } from 'react-native'
import { TextInputMask } from 'react-native-masked-text'

import { textInputStype, container } from './styles'

export default class MyScreen extends React.Component {
  constructor(props) {
    super(props)

    this.state = {
      creditCard: ''
    }
  }

  render() {
    return (
      <View style={container}>
        <Text>Credit Card</Text>
        <TextInputMask
          type={'credit-card'}
          options={{
            obfuscated: false,
            issuer: 'amex'
          }}
          value={this.state.creditCard}
          onChangeText={text => {
            this.setState({
              creditCard: text
            })
          }}
          style={textInputStype}
        />
      </View>
    )
  }
}
```

#### Options

| name | type | required | default | description |
| ---- | ---- | -------- | ------- | ----------- |
| obfuscated | boolean | no | `false` | if the mask should be obfuscated or not |
| issuer | string | no | `visa-or-mastercard` | the type of the card mask. The options are: `visa-or-mastercard`, `amex` or `diners` |











## Usage (TextMask)

```jsx
import React, { Component } from 'react'

// import the component
import { TextMask } from 'react-native-masked-text'

export default class MyComponent extends Component {
    constructor(props) {
        super(props)
        this.state = {
            text: '4567123409871234'
        }
    }

    render() {
        // the type is required but options is required only for some specific types.
        // the sample below will output 4567 **** **** 1234
        return (
            <TextMask
                value={this.state.text}
                type={'credit-card'}
                options={{
                    obfuscated: true
                }}
            />
        )
    }
}
```

### Props

The same of _TextInputMask_, but for React-Native _Text_ component instead _TextInput_.
<br />
_Warning_: if the value not match the mask, it will not appear.

### Methods

`getElement()`: return the instance of _Text_ component.

## Extra (MaskService)

If you want, we expose the `MaskService`. You can use it:

**Methods**

-   static toMask(type, value, settings): mask a value.
    -   `type` (String, required): the type of the mask (`cpf`, `datetime`, etc...)
    -   `value` (String, required): the value to be masked
    -   `settings` (Object, optional): if the mask type accepts options, pass it in the settings parameter
-   static toRawValue(type, maskedValue, settings): get the raw value of a masked value.
    -   `type` (String, required): the type of the mask (`cpf`, `datetime`, etc...)
    -   `maskedValue` (String, required): the masked value to be converted in raw value
    -   `settings` (Object, optional): if the mask type accepts options, pass it in the settings parameter
-   static isValid(type, value, settings): validate if the mask and the value match.
    -   `type` (String, required): the type of the mask (`cpf`, `datetime`, etc...)
    -   `value` (String, required): the value to be masked
    -   `settings` (Object, optional): if the mask type accepts options, pass it in the settings parameter
-   static getMask(type, value, settings): get the mask used to mask the value

Ex:

```jsx
import { MaskService } from 'react-native-masked-text'

var money = MaskService.toMask('money', '123', {
    unit: 'US$',
    separator: '.',
    delimiter: ','
})

// money -> US$ 1.23
```

## Throubleshooting

-   If the `es2015` error throw by babel, try run `react-native start --reset-cache`

## Changelog

View changelog [HERE](CHANGELOG.md)

## Thanks to

-   <div>Icons made by <a href="http://www.freepik.com" title="Freepik">Freepik</a> from <a href="https://www.flaticon.com/" title="Flaticon">www.flaticon.com</a> is licensed by <a href="http://creativecommons.org/licenses/by/3.0/" title="Creative Commons BY 3.0" target="_blank">CC 3.0 BY</a></div>

-   Thanks to [vanilla-masker](https://github.com/BankFacil/vanilla-masker) =).
-   Thanks to [moment](http://momentjs.com/) =).
