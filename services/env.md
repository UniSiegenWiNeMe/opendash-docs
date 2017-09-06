# Env Service (od.env.service)

The env service allows you to use and register global environment variables, to configurate your instance.

**Contents:**
<!-- TOC depthFrom:2 depthTo:3 -->

- [Usage](#usage)
  - [$env(name: String)](#envname-string)
  - [$env(name: String, value: Any)](#envname-string-value-any)
  - [$env(name: String, null, defaultValue: Any)](#envname-string-null-defaultvalue-any)
- [Example](#example)

<!-- /TOC -->

## Usage

> Note: The $env service is not a real service, as it's a single function, instead of a class.

- When creating a new instance of open.DASH, the instance has access to the env service using the `env` method of the instance.

Example:

```js
const instance = new openDASH();

// Set the OD-EVENTS-LOG environment variable
instance.env('OD-EVENTS-LOG', true);
```

- Use the Env Service by injecting `od.env.service` as an Angular Service. We suggest using `$env` as a name for the variable.

Example:

```js
class controller {

  static $inject = ['od.env.service'];

  constructor($env) {
    // Get the OD-EVENTS-LOG environment variable
    let logging = $env('OD-EVENTS-LOG');
  }
}
```

### $env(name: String)

Get the environment variable with given name.

#### Parameter

**name** - String which identifies the environment variable.

#### Response

Returns the value of the environment variable, if the environment variable is not set, an error will be thrown.

### $env(name: String, value: Any)

Sets a new value for the environment variable with given name.

#### Parameter

**name** - String which identifies the environment variable.
**value** - Anything you want to store in the environment variable.

#### Response

No response.

### $env(name: String, null, defaultValue: Any)

Get the environment variable with given name, if there is no response the value of defaultValue will be taken.

#### Parameter

**name** - String which identifies the environment variable.
**null** - Simply null
**defaultValue** - The value which is used as a fallback.

#### Response

Returns the value of the environment variable, if the environment variable is not set, the default value will be returned.

## Example

```js
$env('example', 'value'); // Value will be set
$env('example'); // Returns 'value'
$env('example', null, 42); // Returns 'value'
$env('another-example', null, 42); // Returns 42
$env('another-example'); // Throws an error
```