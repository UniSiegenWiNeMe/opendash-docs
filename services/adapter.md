# Adapter Service (od.adapter.service)

This service should not be used anymore.

<!-- TOC depthFrom:2 depthTo:3 -->

- [Breaking Changes](#breaking-changes)
  - [$adapter.list(options [, callback])](#adapterlistoptions--callback)
  - [$adapter.get(options [, callback])](#adaptergetoptions--callback)
  - [$adapter.values(options [, callback])](#adaptervaluesoptions--callback)
  - [$adapter.set(id, value)](#adaptersetid-value)

<!-- /TOC -->

## Breaking Changes

The adapter services got removed in favor of the new data service, which will simplify things a lot.

Below you will find information on how to update to the new data service.

### $adapter.list(options [, callback])

Now is a synchronous operation, which will return the array directly instead of a promise.

```js
$data.list();
```

### $adapter.get(options [, callback])

Now synchronously returns an instance of OpenDashDataItem.

```js
let item = $data.get('opendash.object.id');
```

### $adapter.values(options [, callback])

You now make calls on an instance of OpenDashDataItem instead of specifying the id. 

There are two ways to get values for an object. You get the current value synchronously as a property of the instance itself or call the history() method to get historical values.

```js
// before:
let promise = $adapter.values({
  'id': 'opendash.object.id',
});

// after:
$data.get('opendash.object.id').value;
```

```js
let history = {
  'aggregation': 0, // works diffrent now
  'start': moment(),
  'end': moment(),
};

// before:
let promise = $adapter.values({
  'id': 'opendash.object.id', // od-object ID.
  'history': history,
});

// after:
$data.get('opendash.object.id').history(history);
```

### $adapter.set(id, value)

Internal function. Now it's `$data.get('opendash.object.id').set(key, value);`.