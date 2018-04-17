# OpenDashDataContainer Class

Instances of OpenDashDataContainer will be returned by the $data service.

<!-- TOC depthFrom:2 depthTo:3 -->

- [Usage](#usage)
- [Properties](#properties)

<!-- /TOC -->

## Usage

Use the $data service to get an instance of OpenDashDataContainer. In the following example `container` might be an OpenDashDataContainer. The `containers` Array will be an Array of OpenDashDataContainers.

Example:
```js
class controller {

  static get $inject() { return ['opendash/services/data']; }

  constructor($data) {
    let container = $data.get('container.id');
    let containers = $data.query().container().run();
  }
}
```

## Properties

- **id**: Unique ID of the container.
- **name**: Name of the container.
- **icon**: Path to an image, representing the container.
- **parent**: Instance of `OpenDashDataItem`, `OpenDashDataContainer` or `null`.
- **children**: Direct children of the container. Array with instances of `OpenDashDataItem` or `OpenDashDataContainer`, might be empty.
- **items**: All direct and indirect children of the container. Array with instances of `OpenDashDataItem` or `OpenDashDataContainer`, might be empty.
- **meta**: Object of meta information about the container, depending on type.