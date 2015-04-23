# react-native-qrcode-reader
A simple QR Code Reader Screen implemented with [react-native-camera](https://github.com/lwansbrough/react-native-camera).

## Getting started
1. Install [react-native-camera](https://github.com/lwansbrough/react-native-camera/blob/master/README.md#getting-started).
2. Copy QRCodeScreen.js to your project.

## Usage

```javascript
'use strict';

var React = require('react-native');
var {
  AppRegistry,
  StyleSheet,
  Text,
  View,
  TouchableOpacity,
  NavigatorIOS,
} = React;

var QRCodeScreen = require('./QRCodeScreen');

var cameraApp = React.createClass({
  render: function() {
    return (
      <NavigatorIOS
        style={styles.container}
        initialRoute={{
          title: 'Index',
          backButtonTitle: 'Back',
          component: Index,
        }}
      />
    );
  }
});

var Index = React.createClass({

  render: function() {
    return (
      <View style={styles.contentContainer}>
        <TouchableOpacity onPress={this._onPressQRCode}>
          <Text>Read QRCode</Text>
        </TouchableOpacity>
      </View>
    );
  },

  _onPressQRCode: function() {
    this.props.navigator.push({
      component: QRCodeScreen,
      title: 'QRCode',
      passProps: {
        onSucess: this._onSucess,
        onCancel: this._onCancel,
      },
    });
  },

  _onSucess: function(result) {
    console.log(result);
  },

  _onCancel: function() {
    console.log('Canceled!');
  }

});

var styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#F5FCFF',
  },
  contentContainer: {
    flex: 1,
    alignItems: 'center',
    justifyContent: 'center',
  }
});

AppRegistry.registerComponent('cameraApp', () => cameraApp);
```

## Properties

#### `cancelButtonVisible`

Values: true, false (default)

Use the `cancelButtonVisible` property to display or hidden cancel button on bottom of view.

#### `cancelButtonTitle`

Value: `Cancel` (default)

Use the `cancelButtonTitle` property to change text of button cancel.

#### `onSucess`

Will call the specified method when a barcode is detected in the camera's view.
Event contains a string with the barcode.

#### `onCancel`
Will call the specified method when cancel button was pressed.
