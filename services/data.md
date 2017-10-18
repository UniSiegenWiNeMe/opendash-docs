# Data Service (od.data.service)

The data service allows you to pull data from all registered data adapters at the same time.

<!-- TOC depthFrom:2 depthTo:3 -->

- [Usage](#usage)
- [Properties & Methods](#properties--methods)
  - [$data.list()](#datalist)
  - [$data.listByType(type: String)](#datalistbytypetype-string)
  - [$data.query()](#dataquery)
  - [$data.get(id: String)](#datagetid-string)

<!-- /TOC -->

## Usage

Use the Data Service by injecting `od.data.service` as an Angular Service. We suggest using `$data` as a name for the variable.

Example:
```js
class controller {

  static $inject = ['od.data.service'];

  constructor($data) {
    // ...
  }
}
```

## Properties & Methods

### $data.list()

Returns all open.DASH data items.

```js
let items = $data.list();
```

#### Response

Returns an Array containing all instances of [OpenDashDataItem](/classes/data-item.md) and [OpenDashDataContainer](/classes/data-container.md).

### $data.listByType(type: String)

Returns all open.DASH data items.

```js
let items = $data.listByType('Number');

items.forEach(i => {
  let item = i[0]; // OpenDashDataItem
  let index = i[1]; // Index

  item.value.values[index]; // A numeric value
});
```

#### Parameter

- **type**: One of the following Strings: Number, String, Boolean, Geo, Object

#### Response

Returns an two dimensional Arrays where the inner Array has two Elements. The first is a instance of [OpenDashDataItem](/classes/data-item.md), the second one is the index of the requested value type.

The same instance of [OpenDashDataItem](/classes/data-item.md) my be returned multiple times, if the value uses the requested value type multiple times.

### $data.query()

Returns a query.

```js
let items = $data.list();
```

#### Response

Returns an instances of [OpenDashDataQuery](/classes/data-query.md).

### $data.get(id: String)

Returns a single open.DASH data item.

```js
let item = $data.id('example.id');

if(!item) {
  // handle missing item
}
```

#### Response

Returns an instance of [OpenDashDataItem](/classes/data-item.md) if there is an item with the given id, if not `null` is returned.
