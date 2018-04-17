# Data adapters

An instance of open.DASH can have one or more data adapters.

In open.DASH they are used to normalize data provision by external web services to a format readable for open.DASH.

It especially must be able to receive all items, you have data for and respective time-based value data.

After getting the adapter to work, you will already be able to see your items in open.DASH and use predefined visualizations.

**Contents:**
<!-- TOC depthFrom:2 depthTo:3 -->

- [Creating a Data Adapter](#creating-a-data-adapter)
  - [Adapter Factory](#adapter-factory)
  - [Adapter Object](#adapter-object)
  - [Registering the Data Adapter](#registering-the-data-adapter)
- [Example](#example)

<!-- /TOC -->

## Creating a Data Adapter

### Adapter Factory

Each Data Adapter needs a Factory Method which will return the Adapter Object.

The Factory Method has one parameter by default: [$injector](https://docs.angularjs.org/api/auto/service/$injector).

You may change this behavior by setting a static attribute `$inject`, which needs to be an array. [Click here to learn more](https://docs.angularjs.org/api/auto/service/$injector#the-inject-property).

```js
const dataAdapterFactory = ($injector) => {
  let $user = $injector.get('od.user.adapter');

  return { ... }; // Adapter Object 
};

const anotherDataAdapterFactory = ($user, $http, $q) => {
  return { ... }; // Adapter Object 
};

anotherDataAdapterFactory.$inject = ['opendash/services/user', '$http', '$q'];
```

### Adapter Object

The Adapter Object needs the following methods:

#### init(ctx, resolve, reject)

The `init` method will be called when the Data Adapter has been loaded and has three parameters:

- **ctx**: An instance of [OpenDashDataContext](/classes/data-context.md);
- **resolve**: Call this function, if everything is loaded.
- **reject**: Call this function, if there is an error while initializing the Data Adapter.

When this method is called make sure to register all available [OpenDashDataItem](/classes/data-item.md) and their current values.

Do this by calling the `create` method of the [OpenDashDataContext](/classes/data-context.md#opendashdatacontextcreatepayload-object):

```js
  HTTPRequest().then(data => {
    data.forEach(item => {
      ctx.create(item);
    });
    resolve();
  });
```

#### history(ctx, resolve, reject, options)

The `history` method allows an [OpenDashDataItem](/classes/data-item.md) to pull historical values from the Data Adapter and has four parameters:

- **ctx**: An instance of [OpenDashDataContext](/classes/data-context.md);
- **resolve**: Call this function, to resolve an Array of historical values.
- **reject**: Call this function, if there is an error while loading the history.
- **options**: An Object holding information about the history request.

The options Object has the following information:

**id** the identifier of the [OpenDashDataItem](/classes/data-item.md). If you need more information about the item call `ctx.get(options.id)` to get the instance of [OpenDashDataItem](/classes/data-item.md) for the given item.

**aggregation** which is either a number in milliseconds or one of the following Strings: 'year', 'quarter', 'month', 'week', 'day', 'hour', 'minute', 'second' or 'millisecond'.

And either **start** and **end** or **since**:
- **start** and **end**: Are both [momentjs](http://momentjs.com/) Objects. Return all values between these dates.
- **since**: Is a [momentjs](http://momentjs.com/) Object. Return all values between this data and now.

The Array of value Objects should look like this:

```js
resolve([
  {
    date: 1483225200000, // Unix millisecond timestamp.
    value: ['Some value'], // Depending on item.valueTypes.
  },
]);
```

#### update(ctx, resolve, reject, payload)

The `update` method allows an [OpenDashDataItem](/classes/data-item.md) to save changed information in the Data Adapter and has four parameters:

- **ctx**: An instance of [OpenDashDataContext](/classes/data-context.md);
- **resolve**: Call this function, when the information is saved.
- **reject**: Call this function, if there is an error while saving the information.
- **payload**: An Object holding information about the change request.

The payload Object has the following information:

- **id** the identifier of the [OpenDashDataItem](/classes/data-item.md). If you need more information about the item call `ctx.get(options.id)` to get the instance of [OpenDashDataItem](/classes/data-item.md) for the given item.
- **key**: Key which has been changed.
- **value**: Value which has been changed.

### Registering the Data Adapter

Import your Data Adapter like this, where ever you want to create your instance of open.DASH:

```js
import dataAdapter from './data-adapter.js';
```

After creating your instance, register the Data Adapter like this:

```js
instance.registerDataAdapter(dataAdapter);
```

Once this is done, you are good to go.

## Example

```js
// app.js

import dataAdapter from './data-adapter.js';

instance.registerDataAdapter(dataAdapter);

// data-adapter.js
export default ($injector) => {

  const moment = $injector.get('moment');
  const _ = $injector.get('lodash');

  return {
    init(ctx, resolve, reject) {
      // Request a list of all items via HTTP/websocket
      HTTPRequest().then(data => {
        data.forEach(item => {
          // Create each item
          ctx.create(item);
        });
        // Call resolve() once you are done
        resolve();
      });
    },
    history(ctx, resolve, reject, options) {

      let itemID = options.id;

      if (options) {
        if (options.start && options.end) {
          let query = ...
        }

        if (options.since) {
          let query = ...
        }
      }

      // Get the value history for the given item via HTTP/websocket
      HTTPRequest(query).then(data => {
        let result = data.map(item => ({
          date: moment(item.timestamp).valueOf(), // unix millisecond timestamp 
          value: item.value, // map to the right 
        }));

        // Return the array of values by resolving it:
        resolve(result);
      });

    },
    update(ctx, resolve, reject, payload) {
      resolve(true);
    },
  };
}
```
