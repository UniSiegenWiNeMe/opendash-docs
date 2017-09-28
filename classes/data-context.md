# OpenDashDataContext Class

Is available to data adapters.

<!-- TOC depthFrom:2 depthTo:3 -->

- [Methods](#methods)
  - [OpenDashDataContext.get()](#opendashdatacontextget)
  - [OpenDashDataContext.create(payload: Object)](#opendashdatacontextcreatepayload-object)

<!-- /TOC -->

## Methods

### OpenDashDataContext.get()

Same as `$data.get()`. Returns an instance of [OpenDashDataItem](/classes/data-item.md).

To set a new value to an item, use this method.

```js
ctx.get('item.id').set('value', {
  date: 1483225200000, // Unix millisecond timestamp.
  value: 'Some value', // Depending on item type.
});
```

### OpenDashDataContext.create(payload: Object)

Create a new [OpenDashDataItem](/classes/data-item.md) and save it in the data adapter.

#### Parameter

The parameter should be and object will the following properties:

- **id**: Unique identifier of the item.
- **type**: Type of the item.
- **meta**: Object of meta information about the item, depending on type.
- **parent**: (Optional) ID of the parent item.
- **value**: (Optional) Value Object for the current value.

