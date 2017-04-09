# od-loading Component

`od-loading` ist ein Angular Component, der benutzt wird um die standart Ladeanimation von open.DASH anzuzeigen.

## Benutzung

Im Tempalte oberhalb des zu überdeckenden Content sollte folgendes Element eingebunden werden:

```html
<od-loading ng-show="$ctrl.loading"></od-loading>
```

Damit die Ladeanimation an- und ausgeschaltet werden kann, wird die [ng-show](https://docs.angularjs.org/api/ng/directive/ngShow) Direktive benutzt, an die ein BOOLEAN übergeben wird oder einfacher, wie im Beispiel weiter unten: Es wird eine Variable mit einem BOOLEAN übergeben.

Im Controller wird diese Variable mit `true` initialiesiert und nach einer Sekunde wird die Ladeanimation beendet, indem die Variable auf `false` gesetzt wird.

```js
this.loading = true;

$timeout(() => { this.loading = false; }, 1000);
```

### Beispiel mit Scope

Das selbe Beispiel mit Scope, zur Nutzung in Modals.

Template:

```html
<od-loading ng-show="loading"></od-loading>
```

Javascript:

```js
$scope.loading = true;
```

## Verhalten

Im Prinzip verhält sich `od-loading` wie ein `div` Element mit folgenden Eigenschaften:

```css
od-loading {
  display: block;
  position: absolute;
  height: 100%;
  width: 100%;

  top: 0;
  bottom: 0;
  left: 0;
  right: 0;

  z-index: 9999;
}
```