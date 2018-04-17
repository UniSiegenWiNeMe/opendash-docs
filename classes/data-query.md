# OpenDashDataQuery Class

Instances of OpenDashDataQuery will be returned by the $data service. Use the query object to recive a custom list of items from the $data service.

<!-- TOC depthFrom:2 depthTo:3 -->

- [Usage](#usage)
- [Methods](#methods)
    - [OpenDashDataQuery.filter(func: Function)](#opendashdataqueryfilterfunc-function)
    - [OpenDashDataQuery.union(input: Array)](#opendashdataqueryunioninput-array)
    - [OpenDashDataQuery.intersection(input: Array)](#opendashdataqueryintersectioninput-array)
    - [OpenDashDataQuery.difference(input: Array)](#opendashdataquerydifferenceinput-array)
    - [OpenDashDataQuery.root()](#opendashdataqueryroot)
    - [OpenDashDataQuery.container()](#opendashdataquerycontainer)
    - [OpenDashDataQuery.items()](#opendashdataqueryitems)
    - [OpenDashDataQuery.run()](#opendashdataqueryrun)

<!-- /TOC -->

## Usage

Use the $data service to get an instance of OpenDashDataQuery.

Example:
```js
class controller {

  static get $inject() { return ['opendash/services/data']; }

  constructor($data) {
    let query = $data.query();
    query.container();
    query.root();
    let result = query.run();
  }
}
```

## Methods

### OpenDashDataQuery.filter(func: Function)

Modifies the result: The input Function will be called on each element in the result. When the Function returns true for an element, it will be returned.

Returns the OpenDashDataQuery instance.

### OpenDashDataQuery.union(input: Array)

Modifies the result: Elements from the result and the input Array will be returned.

Returns the OpenDashDataQuery instance.

### OpenDashDataQuery.intersection(input: Array)

Modifies the result: Only Elements which are both in the result and the input Array will be returned.

Returns the OpenDashDataQuery instance.

### OpenDashDataQuery.difference(input: Array)

Modifies the result: Only Elements from the result which not in the input Array will be returned.

Returns the OpenDashDataQuery instance.

### OpenDashDataQuery.root()

Modifies the result: Only Elements without parent will be returned.

Returns the OpenDashDataQuery instance.

### OpenDashDataQuery.container()

Modifies the result: Only instances of [OpenDashDataContainer](/classes/data-container.md) will be returned.

Returns the OpenDashDataQuery instance.

### OpenDashDataQuery.items()

Modifies the result: Only instances of [OpenDashDataItem](/classes/data-item.md) will be returned.

Returns the OpenDashDataQuery instance.

### OpenDashDataQuery.run()

Returns the result set, an Array containing all instances of [OpenDashDataItem](/classes/data-item.md) and [OpenDashDataContainer](/classes/data-container.md) matching the query.