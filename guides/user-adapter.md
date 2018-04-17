# User Adapter

Custom user adapters are possible but not supported right now and will be added in the comming updates.

**Contents:**
<!-- TOC depthFrom:2 depthTo:3 -->

- [Prebuild User Adapters](#prebuild-user-adapters)
    - [Local User Adapter](#local-user-adapter)
    - [Parse User Adapter](#parse-user-adapter)
    - [Baasbox User Adapter](#baasbox-user-adapter)

<!-- /TOC -->

## Prebuild User Adapters

There are some adapters ready to use right now:

### Local User Adapter

Install via NPM: `npm i -S @opendash/user-adapter-local`

Make sure to install version `^4.0.0` for opendash version `2.0.0`.

```js
// app.js

import userAdapter from '@opendash/user-adapter-local';

// ...

instance.registerUserAdapter(userAdapter, {
  lsKey: 'some-unused-local-store-key', // default: 'opendash-user-adapter-local-data'
});
```

### Parse User Adapter

Install via NPM: `npm i -S @opendash/user-adapter-parse`

Make sure to install version `^4.0.0` for opendash version `2.0.0`.

```js
// app.js

import userAdapter from '@opendash/user-adapter-parse';

// ...

instance.registerUserAdapter(userAdapter, {
  url: 'https://parse.example.com/parse/',
  collection: 'openDASH2',
  applicationId: '1234567890',
  javaScriptKey: null, // default: undefined
});
```

### Baasbox User Adapter

Install via NPM: `npm i -S @opendash/user-adapter-baasbox`

Make sure to install version `^4.0.0` for opendash version `2.0.0`.

```js
// app.js

import userAdapter from '@opendash/user-adapter-baasbox';

// ...

instance.registerUserAdapter(userAdapter, {
  endpoint: 'https://baasbox.example.com',
  collection: 'openDASH',
  appCode: '123456789',
});
```