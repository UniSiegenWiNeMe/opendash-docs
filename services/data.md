# Data Service (od.data.service)

The data service allows you to pull data from all registered data adapters at the same time.

<!-- TOC depthFrom:2 depthTo:3 -->

- [Usage](#usage)
  - [$data.list() (sync)](#datalist-sync)
  - [$data.get(id: String) (sync)](#datagetid-string-sync)

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

### $data.list() (sync)

Returns all open.DASH data items.

```js
let items = $data.list();
```

#### Response

Returns an Array containing all instances of [OpenDashDataItem](services/data-item.md).

### $data.get(id: String) (sync)

Returns a single open.DASH data item.

```js
let item = $data.id('example.id');

if(!item) {
  // handle missing item
}
```

#### Response

Returns an instance of [OpenDashDataItem](services/data-item.md) if there is an item with the given id, if not `null` is returned.