# User Adapter

Custom user adapters are possible but not supported right now and will be added in the comming updates.

## Prebuild User Adapters

There are some adapters ready to use right now:

### Local User Adapter

Install via NPM: `npm i -S @opendash/user-adapter-local`

```js
// app.js

import userAdapter from '@opendash/user-adapter-local';

// ...

instance.registerUserAdapter(userAdapter);
```

### Baasbox User Adapter

Install via NPM: `npm i -S @opendash/user-adapter-baasbox`

```js
// app.js

import userAdapter from '@opendash/user-adapter-baasbox';

// ...

instance.env('USER-ADAPTER-BAASBOX-ENDPOINT', 'https://baasbox.example.com');
instance.env('USER-ADAPTER-BAASBOX-APP-CODE', '123456789');
instance.env('USER-ADAPTER-BAASBOX-COLLECTION', 'openDASH');

instance.registerUserAdapter(userAdapter);
```