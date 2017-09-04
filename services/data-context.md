# OpenDashDataContext Class

Is available to data adapters.

<!-- TOC depthFrom:2 depthTo:3 -->

- [Usage](#usage)
  - [OpenDashDataContext.get()](#opendashdatacontextget)
  - [OpenDashDataContext.create(payload: Object)](#opendashdatacontextcreatepayload-object)

<!-- /TOC -->

## Usage

### OpenDashDataContext.get()

Same as `$data.get()`. Returns an instance of [OpenDashDataItem](/services/data-item.md).

To set a new value to an item, use this method.

```js
ctx.get('item.id').set('value', {
  date: 1483225200000, // Unix millisecond timestamp.
  value: 'Some value', // Depending on item type.
});
```

### OpenDashDataContext.create(payload: Object)

Create a new [OpenDashDataItem](/services/data-item.md) and save it in the data adapter.

#### Parameter

The parameter should be and object will the following properties:

- **id**: Unique identifier of the item.
- **type**: Type of the item.
- **meta**: Object of meta information about the item, depending on type.
- **parent**: (Optional) ID of the parent item.
- **children**: Array with instances of [OpenDashDataItem](/services/data-item.md) or `[]`; 
