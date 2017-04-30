# Dashboard Service (od.dashboard.service)

Der Event Service ist dazu da mit Events in open.DASH zu arbeiten. Es können Events emittiert werden und auf Events reagiert werden.

<!-- TOC depthFrom:2 depthTo:3 -->

- [Nutzung](#nutzung)
  - [$event.on(event: String, callback: Function)](#eventonevent-string-callback-function)
  - [$event.on(events: Array, callback: Function)](#eventonevents-array-callback-function)
  - [$event.emit(event: String)](#eventemitevent-string)
  - [$event.emit(event: Array)](#eventemitevent-array)
- [Core Events](#core-events)
  - ["od-dashboard-ready" Event](#od-dashboard-ready-event)
  - ["od-dashboard-changed" Event](#od-dashboard-changed-event)
  - ["od-dashboard-save" Event](#od-dashboard-save-event)
  - ["od-widgets-changed" Event](#od-widgets-changed-event)
  - ["od-widgets-added" Event](#od-widgets-added-event)
  - ["od-widgets-removed" Event](#od-widgets-removed-event)

<!-- /TOC -->

## Nutzung

Der Event Service kann benutzt werden indem `od.event.service` über Angular injected wird. Es empfiehlt sich diesen dann mit dem Parameter Namen `$event` zu benutzen.

Beispiel:

```js
class controller {

  static $inject = ['od.event.service'];

  constructor($event) {
    // ...
  }
}
```

### $event.on(event: String, callback: Function)

Fügt einen Event Listener für das übergebene Event hinzu.

#### Beispiel

```js
$event('od-dashboard-ready', () => {
  // do something
});
```

#### Rückgabe

Gibt `null` zurück.

### $event.on(events: Array, callback: Function)

Wenn an die `.on()` Methode ein Array von Events/Strings übergeben wird, statt einem String, dann wird die `.on()` Methode für jedes Event/jeden String auseführt. 

### $event.emit(event: String)

Signalisiert dass ein Event ausgelöst wurde.

### $event.emit(event: Array)

Wenn an die `.emit()` Methode ein Array von Events/Strings übergeben wird, statt einem String, dann wird die `.emit()` Methode für jedes Event/jeden String auseführt. 

## Core Events

Events die von dem Core von open.DASH emittiert werden.

### "od-dashboard-ready" Event

Wird ausgelöst, wenn der Dashboard Service geladen hat.

### "od-dashboard-changed" Event

Wird ausgelöst, wenn das Dashboard sich verändert hat.

### "od-dashboard-save" Event

Wird ausgelöst, wenn das Dashboard gespeichert wird.

### "od-widgets-changed" Event

Wird ausgelöst, wenn sich eins der Widgets verändert hat.

### "od-widgets-added" Event

Wird ausgelöst, wenn ein Widget zum Dashboard hinzugeügt wurde.

### "od-widgets-removed" Event

Wird ausgelöst, wenn ein Widget aus dem Dashboard gelöscht wurde.