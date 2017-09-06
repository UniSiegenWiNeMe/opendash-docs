# Data adapters

An instance of open.DASH can have one or more data adapters.

Data adapters are Angular Services, for more information about Angular Services, check out the official documentation.

In open.DASH they are used to normalize data provision by external web services to a format readable for open.DASH.

It especially must be able to receive all items, you have data for and respective time-based value data.

After getting the adapter to work, you will already be able to see your items in open.DASH and use predefined visualizations.

## Example

```js
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
          // ...
        }

        if (options.since) {
          // ...
        }
      }

      // Get the value history for the given item via HTTP/websocket
      HTTPRequest().then(data => {
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
