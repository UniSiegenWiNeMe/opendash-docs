# OpenDashDataItem Class

Instances of OpenDashDataItem will be returned by the $data service.

<!-- TOC depthFrom:2 depthTo:3 -->

- [Usage](#usage)
- [Properties](#properties)
  - [OpenDashDataItem.value](#opendashdataitemvalue)
  - [OpenDashDataItem.valueTypes](#opendashdataitemvaluetypes)
- [Methods](#methods)
  - [OpenDashDataItem.isParent(input: OpenDashDataContainer)](#opendashdataitemisparentinput-opendashdatacontainer)
  - [OpenDashDataItem.history(options: Object)](#opendashdataitemhistoryoptions-object)
  - [OpenDashDataItem.watch(callback: Function)](#opendashdataitemwatchcallback-function)
  - [OpenDashDataItem.liveValues(callback: Function)](#opendashdataitemlivevaluescallback-function)
  - [OpenDashDataItem.set(key: String, value: Any, save: Boolean, saveForUser: Boolean)](#opendashdataitemsetkey-string-value-any-save-boolean-saveforuser-boolean)

<!-- /TOC -->

## Usage

Use the $data service to get an instance of OpenDashDataItem. In the following example `item` will be an OpenDashDataItem.

Example:
```js
class controller {

  static $inject = ['od.data.service'];

  constructor($data) {
    let item = $data.get('object.id');
  }
}
```


## Properties

- **id**: Unique identifier of the item.
- **name**: Name of the item.
- **icon**: Path to the icon of the item.
- **meta**: Object of meta information about the item.
- **parent**: ID of the parent item or `null`.
- **value**: Value Object for the current value or `null` if there is no current value available.
- **valueTypes**: Array representing the types of the value.

### OpenDashDataItem.value

Returns the current value of the item.

```js
item.value;
```

#### Response

Returns an Object with two keys: date and value. Where date is a unix millisecond timestamp and value is depending on the type of the item.

```js
{
  date: 1483225200000, // unix millisecond timestamp
  value: [10], // depending on item.valueTypes
}
```

### OpenDashDataItem.valueTypes

Returns the current value of the item.

Returns an Array of Objects which have two properties:

- **name**: Name of the value, which will be displayed in the dashboard.
- **type**: Type of the value, which must be one of the following Strings: Number, String, Boolean, Geo, Object

```js
item.valueTypes;

// =>

[
  {
    name: 'Display Name',
    type: 'Number', // One of the following Strings: Number, String, Boolean, Geo, Object
  },
];
```

## Methods

### OpenDashDataItem.isParent(input: OpenDashDataContainer)

Returns `true` or `false` wether the input container is a direct or indirect parent of the item.

### OpenDashDataItem.history(options: Object)

Returns historical values of the item.

#### Parameter

**options**: Object with options to request data between two dates by using `options.start` and `options.end` or between now and a given date by using `options.since` or `options.value` and `options.unit`.

**Aggregation: `options.aggregation`:**

`options.aggregation` must have one of the following values:

- String: a 'year' (shortcut: 'y', 'years')
- String: a 'quarter' (shortcut: 'Q', 'quarters')
- String: a 'month' (shortcut: 'M', 'months')
- String: a 'week' (shortcut: 'w', 'weeks')
- String: a 'day' (shortcut: 'd', 'days')
- String: a 'hour' (shortcut: 'h', 'hours')
- String: a 'minute' (shortcut: 'm', 'minutes')
- String: a 'second' (shortcut: 's', 'seconds')
- String: a 'millisecond' (shortcut: 'ms', 'milliseconds')
- Number: Aggregation in milliseconds.

**Using `options.start` and `options.end`:**

Both values must be [momentjs](http://momentjs.com/) objects or values which will be accepted by the [momentjs constructor](http://momentjs.com/docs/#/parsing/).

```js
let promise = item.history({
  'aggregation': 0,
  'start': moment(),
  'end': moment(),
});
```

**With `options.since`:**

`options.since` must be [momentjs](http://momentjs.com/) objects or values which will be accepted by the [momentjs constructor](http://momentjs.com/docs/#/parsing/).

```js
let promise = item.history({
  'aggregation': 0,
  'since': moment(),
});
```

**With `options.value` und `options.unit`:**

`options.value` and `options.unit` will be used in `moment().subtract(options.value, options.unit)` and will be saved in `options.since`.

```js
let promise = item.history({
  'aggregation': 0,
  'value': 100,
  'unit': 'hours',
});
```

#### Response

A Promise will be returned, which resolves to an array of values.

```js
let promise = item.history({
  // ...
})

promise.then(values => {
  console.log(values);
  // =>
  values = [
    {
      'date': 1483225200000, // unix millisecond timestamp.
      'value': [10], // depending on item.valueTypes
    },
  ];
});

promise.then(null, err => {
  // Error handling.
});
```

### OpenDashDataItem.watch(callback: Function)

Use the watch method to register a callback which will be called whenever a value changes.

#### Parameter

**callback**: Function which will be called, whenever the item changes.

The callback will be called with three parameters: key, newValue and oldValue.

#### Example

```js
item.watch((key, newValue, oldValue) => {
  if(key === 'value') {
    console.log(`Value changed from ${oldValue} to ${newValue}`);
  }
});
```

#### Response

No response.

### OpenDashDataItem.liveValues(callback: Function)

Use the liveValues method to register a callback which will be called when the value changes. If there is a value when the method is called, the callback will be called immediately.

#### Parameter

**callback**: Function which will be called, when a value changes.

The callback will be called with a single parameter: `value`.

#### Example

```js
item.liveValues((value) => {
  console.log(`Value of ${item.id} currently is ${value}`);
});
```

#### Response

No response.

### OpenDashDataItem.set(key: String, value: Any, save: Boolean, saveForUser: Boolean)

Set a new value for a given property.

#### Parameter

- **key**: Key which identifies the property which will be changed.
- **value**: The new value.
- **save**: Wether the value will be send to the data adapter or not. Set save to `true` to send the value to the adapter.
- **saveForUser** Wether the value will be saved in the user adaper or not.

If `save` is set to `true`, the value will not be changed in the item itself, but will be send to the adapter. If it's set to `false` it will be saved to the item without notifying the adapter.

If `saveForUser` is set to `true`, the value will be changed in the item and it will be send to the user adapter. The user adapter will remember the overwritten value and load it the next the user opens open.DASH.

Adapters can use this method to set new values to the item like this:

```js
item.set('value', {
  date: 1483225200000, // Unix millisecond timestamp
  value: ['Some value'], // Depending on item.valueType.
});
```
#### Response

A Promise will be returned, which will resolve without a value, if the set operation was successfull or reject with an error message.
