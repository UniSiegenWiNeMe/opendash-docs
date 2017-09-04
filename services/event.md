# Dashboard Service (od.dashboard.service)

The event services allows you to:
- Emit events
- Handle built in events
- Handle custom events

**Contents:**
<!-- TOC depthFrom:2 depthTo:3 -->

- [Usage](#usage)
  - [$event.on(event: String, callback: Function)](#eventonevent-string-callback-function)
  - [$event.on(events: Array, callback: Function)](#eventonevents-array-callback-function)
  - [$event.once(event: String, callback: Function)](#eventonceevent-string-callback-function)
  - [$event.on(events: Array, callback: Function)](#eventonevents-array-callback-function-1)
  - [$event.emit(event: String)](#eventemitevent-string)
  - [$event.emit(event: Array)](#eventemitevent-array)
- [Core Events](#core-events)

<!-- /TOC -->

## Usage

Use the Event Service by injecting `od.env.service` as an Angular Service. We suggest using `$env` as a name for the variable.

Example:
```js
class controller {

  static $inject = ['od.env.service'];

  constructor($env) {
    // ...
  }
}
```

### $event.on(event: String, callback: Function)

Adds an event listener for the given event, which will be called every time a the event is fired.

#### Example

```js
$event.on('od-dashboard-ready', () => {
  // do something every time
});
```

#### Response

No return.

### $event.on(events: Array, callback: Function)

```js
$event.on(events, callback);

// is the same as:

events.forEach(event => {
  $event.on(event, callback);
});
```

### $event.once(event: String, callback: Function)

Adds an event listener for the given event, which will be called when the event is fired the next time.

#### Example

```js
$event.once('od-dashboard-ready', () => {
  // do something once
});
```

#### Response

No return.

### $event.on(events: Array, callback: Function)

```js
$event.on(events, callback);

// is the same as:

events.forEach(event => {
  $event.on(event, callback);
});
```

### $event.emit(event: String)

Calls each registered event listener with the given name.

### $event.emit(event: Array)

```js
$event.emit(events);

// is the same as:

events.forEach(event => {
  $event.emit(event);
});
```

## Core Events

A list of events, which will be emitted by the core of open.DASH.

- **"od-dashboard-ready" Event:** Will be fired, when the dashboard service is ready.

- **"od-dashboard-changed" Event:** Will be fired, when the dashboard changes.

- **"od-dashboard-save" Event:** Will be fired, when the dashboard is saved to the user adapter.

- **"od-widgets-changed" Event:** Will be fired, when a widget changes

- **"od-widgets-added" Event:** Will be fired, when a widget was added to the dashboard.

- **"od-widgets-removed" Event:** Will be fired, when a widget was removed from the dashboard.