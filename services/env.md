# Env Service (od.env.service)

Mit dem Env Service kann man, ähnlich wie mit Umgebungsvariablen, die Instanz konfigurieren.

<!-- TOC depthFrom:2 depthTo:3 -->

- [Nutzung](#nutzung)
  - [$env(key: String)](#envkey-string)

<!-- /TOC -->

## Nutzung

1. Bei der Erstellung einer Instanz kann in das Objekt, welches an die bootstrap Methode übergeben wird, ein Schlüssel *env* eingefügt werden, der ein Objekt hält.

2. Der Env Service kann geladen werden indem `od.env.service` über Angular injected wird. Es empfiehlt sich diesen dann mit dem Parameter Namen `$env` zu benutzen. Wichtig hierbei ist, dass $env kein richtiger Service ist, sondern eher eine einzelne Funktion.

Beispiel:

```js
// Es wird eine Umgebungsvariable "BEISPIEL_ENV_VAR" eingefügt, mit dem Wert 1234.
bootstrap({
  // ...
  env: {
    'BEISPIEL_ENV_VAR': '1234',
  },
  // ...
});
```

```js
class controller {

  static $inject = ['od.env.service'];

  constructor($env) {
    $env('BEISPIEL_ENV_VAR'); // => '1234'
  }
}
```

### $env(key: String)

Fragt einen Schlüssel ab.

#### Parameter

**key** - Schlüssel vom Typ String der abgefragt werden soll.

#### Rückgabe

Gibt den Wert des Schlüssels zurück. Wirf einen Error, wenn der Schlüssel nicht vorhanden ist.