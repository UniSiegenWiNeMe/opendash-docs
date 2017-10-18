# OpenDashDataContext Class

Is available to data adapters.

<!-- TOC depthFrom:2 depthTo:3 -->

- [Methods](#methods)
  - [OpenDashDataContext.get()](#opendashdatacontextget)
  - [OpenDashDataContext.create(payload: Object)](#opendashdatacontextcreatepayload-object)
  - [OpenDashDataContext.createContainer(payload: Object)](#opendashdatacontextcreatecontainerpayload-object)

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
- **name**: Name of the item.
- **icon**: (Optional) Path to the icon of the item.
- **meta**: (Optional) Object of meta information about the item.
- **parent**: (Optional) ID of the parent item.
- **value**: (Optional) Value Object for the current value.
- **valueTypes**: Array representing the types of the value.

```js
{
  valueTypes: [
    {
      name: 'Display Name',
      type: 'Number', // One of the following Strings: Number, String, Boolean, Geo, Object
    },
  ],
}
```

### OpenDashDataContext.createContainer(payload: Object)

Create a new [OpenDashDataContainer](/classes/data-container.md) and save it in the data adapter.

#### Parameter

The parameter should be and object will the following properties:

- **id**: Unique identifier of the container.
- **name**: Name of the container.
- **icon**: (Optional) Path to the icon of the container.
- **meta**: (Optional) Object of meta information about the container.
- **parent**: (Optional) ID of the parent container.