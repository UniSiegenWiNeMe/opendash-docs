# Adapter Service (od.adapter.service)

<!-- TOC depthFrom:2 depthTo:3 -->

- [Unterschied zu v1](#unterschied-zu-v1)
- [Nutzung](#nutzung)
  - [$adapter.list(options [, callback])](#adapterlistoptions--callback)
  - [$adapter.get(options [, callback])](#adaptergetoptions--callback)
  - [$adapter.values(options [, callback])](#adaptervaluesoptions--callback)
  - [$adapter.value(id [, callback])](#adaptervalueid--callback)
  - [$adapter.unsubscribe(subscription)](#adapterunsubscribesubscription)
  - [$adapter.set(id, value)](#adaptersetid-value)

<!-- /TOC -->

## Unterschied zu v1

Der Adapter Service in open.DASH v2 verhält sich etwas anders als die Adapter aus open.DASH v1.

Er greift auf alle verfügbaren Adapter zu und gibt über seine Methoden die Daten von allen Adaptern an den Nutzer weiter.

Die Methoden haben sich ein wenig geändert, anstatt viele Parameter zu benutzen, wird ein options Objekt als Parameter übergeben und optional ein zweiter Parameter mit einem Callback. Wird dieser Callback Parameter gesetzt, gibt die Methode statt einem Promise `null` zurück und wir zu einer Subscribe Methode, die neue Daten immer an den übergebenen Callback weitergibt.

## Nutzung

Der Adapter Service kann benutzt werden indem `od.adapter.service` über Angular injected wird. Es empfiehlt sich diesen dann mit dem Parameter Namen `$adapter` zu benutzen.

Beispiel:
```js
class controller {

  static $inject = ['od.adapter.service'];

  constructor($adapter) {
    // ...
  }
}
```

### $adapter.list(options [, callback])

Gibt ein Array von od-Objekten zurück.

#### Parameter
**options** - Objekt mit Optionen.

```js
{
  'key': value, // comment
}
```

**callback** _[optional]_ - Funktion, die ausgeführt wird, wenn neue Daten vorhanden sind. Für den Aufbau des data Objekts bitte weiter unten gucken.

```js
let subscription = $adapter.list(options, (err, data) => {
  if(err) {
    // Fehler behandeln.
    return;
  }
  // Daten verarbeiten.
});

// Die Subscription wird nicht mehr benötigt?
$adapter.unsubscribe(subscription);
```

#### Rückgabe

Falls kein Callback übergeben wird, wird ein Promise zurück gegeben, das ein Array mit od-Objekten resolved:

```js
// Beispiel:
let promise = $adapter.list({})

promise.then(devices => {
  console.log(devices);

  // =>
  devices = [
    {
      '@id': 'opendash.device.1234', // ID eines od-Objekts
      '@type': 'od.device', // Typ des od-Objekts
      // ...
    },
  ];
});

promise.then(null, err => {
  // Error behandeln.
});
```

### $adapter.get(options [, callback])

Gibt ein einzelnes od-Objekt zurück.

#### Parameter
**options** - String der die ID eines od-Objekts enthält.

```js
let promise = $adapter.get('opendash.objekt.id');

// ist das gleiche wie:
let promise = $adapter.get({
  'id': 'opendash.objekt.id', // comment
});
```

**options** - Objekt mit Optionen.

```js
let promise = $adapter.get({
  'id': 'opendash.objekt.id', // ID nach der gesucht wird.
});
```

**callback** _[optional]_ - Funktion, die ausgeführt wird, wenn neue Daten vorhanden sind. Für den Aufbau des data Objekts bitte weiter unten gucken.

```js
let subscription = $adapter.get('opendash.objekt.id', (err, data) => {
  if(err) {
    // Fehler behandeln.
    return;
  }
  // Daten verarbeiten.
});

// Die Subscription wird nicht mehr benötigt?
$adapter.unsubscribe(subscription);
```

#### Rückgabe

Falls kein Callback übergeben wird, wird ein Promise zurück gegeben, das ein Array mit od-Objekten resolved:

```js
let promise = $adapter.list({})

promise.then(device => {
  console.log(device);

  // =>
  device = {
    '@id': 'opendash.device.1234', // ID eines od-Objekts
    '@type': 'od.device', // Typ des od-Objekts
    // ...
  };
});

promise.then(null, err => {
  // Error behandeln.
});
```

### $adapter.values(options [, callback])

Gibt die od-Werte eines einzelnen od-Objekts zurück.

#### Parameter
**options** - String der die ID eines od-Objekts enthält.

```js
let promise = $adapter.values('opendash.objekt.id');

// ist das gleiche wie:
let promise = $adapter.values({
  'id': 'opendash.objekt.id', // comment
});
```

**options** - Objekt mit Optionen.

```js
let promise = $adapter.values({
  'id': 'opendash.objekt.id', // ID eines od-Objekts.
});
```

Werte aus der Vergangenheit abfragen:

`options.history` ist ein Objekt, es können entweder Daten zwischen zwei Zeitpunkten (mit `options.history.start` und `options.history.end`) und zwischen dem aktuellen Zeitpunkt und einem bestimmten Zeitpunkt (mit `options.history.since` oder `options.history.value` und `options.history.unit`) abgefragt werden.

**Aggregation über `options.history.aggregation`:**

`options.history.aggregation` muss einen der folgenden Werte haben:

* 0 = Eine Minute
* 1 = 15 Minuten
* 2 = Eine Stunde
* 3 = Ein Tag
* 4 = Eine Woche
* 5 = Ein Monat 

**Mit `options.history.start` und `options.history.end`:**

Beide werte müssen [Moment](http://momentjs.com/) Objekte oder von [Moment für den Konstruktor akzeptierte Werte](http://momentjs.com/docs/#/parsing/) sein. Es werden die Daten zwischen den beiten gegebenen Zeitpunkten angezeigt.

```js
let promise = $adapter.values({
  'id': 'opendash.objekt.id', // ID eines od-Objekts.
  'history': {
    'aggregation': 0,
    'start': moment(),
    'end': moment(),
  },
});
```

**Mit `options.history.since`:**

`options.history.since` muss ein [Moment](http://momentjs.com/) Objekt oder ein von [Moment für den Konstruktor akzeptierter Wert](http://momentjs.com/docs/#/parsing/) sein. Es werden die Daten zwischen dem aktuellen Zeitpunkt und dem in `options.history.since` angegebenen angezeigt.

```js
let promise = $adapter.values({
  'id': 'opendash.objekt.id', // ID eines od-Objekts.
  'history': {
    'aggregation': 0,
    'since': moment(),
  },
});
```

**Mit `options.history.value` und `options.history.unit`:**

`options.history.value` und `options.history.unit` werden in `moment().subtract(options.history.value, options.history.unit)` eingesetzt und in `options.history.since` gespeichert. Es werden die Daten zwischen dem aktuellen Zeitpunkt und dem in `options.history.since` angegebenen angezeigt.

```js
let promise = $adapter.values({
  'id': 'opendash.objekt.id', // ID eines od-Objekts.
  'history': {
    'aggregation': 0,
    'value': 100,
    'unit': 'hours',
  },
});
```

**callback** _[optional]_ - Funktion, die ausgeführt wird, wenn neue Daten vorhanden sind. Für den Aufbau des data Objekts bitte weiter unten gucken.

```js
let values = [];

let subscription = $adapter.values('opendash.objekt.id', (err, data) => {
  if(err) {
    // Fehler behandeln.
    return;
  }
  
  // Daten verarbeiten, zum Beispiel das values Array, das weiter oben definiert
  // wurde, mit den neuen Values mergen.
  data.forEach(e => values.push(e));
});

// Die Subscription wird nicht mehr benötigt?
$adapter.unsubscribe(subscription);
```

#### Rückgabe

Falls kein Callback übergeben wird, wird ein Promise zurück gegeben, das ein Array mit od-Werten resolved:

```js
let promise = $adapter.values('opendash.objekt.id')

promise.then(values => {
  console.log(values);
  // =>
  values = [
    {
      'date': new Date(), // JS Date Objekt.
      'unit': 'unit', // Einheit in die Values sind.
      'value': 'wert', // Objekt, Array, String, Number entsprechend der Einheit
    },
  ];
});

promise.then(null, err => {
  // Error behandeln.
});
```

### $adapter.value(id [, callback])

Kürzel für `$adapter.values()`

```js
let promise = $adapter.value('opendash.objekt.id');

// Ist das gleiche wie:

let promise = $adapter.values({
  id: 'opendash.objekt.id',
  limit: 1,
});
```

### $adapter.unsubscribe(subscription)

Wenn durch das übergeben eines Callbacks an eine unterstützende Funktion eine Subscription erzeugt wird, wird ein Promise zurück gegeben, das an `$adapter.unsubscribe()` übergeben werden kann, um die Subscription und somit jeden weiteren Aufruf des Callbacks zu beenden.

```js
let subscription = $adapter.get('opendash.objekt.id', (err, data) => {
  if(err) {
    // Fehler behandeln.
    return;
  }
  // Daten verarbeiten.
});

// Die Subscription wird nicht mehr benötigt?
$adapter.unsubscribe(subscription);
```

### $adapter.set(id, value)

Ist bisher zu Testzwecken implementiert.