# od-loading Component

`od-loading` is an Angular Component, which will display the open.DASH loading animation, in case a widget has not completed build, i.e. when data is still being retrieved or graphs are still being rendered.

## Usage

Add the following element above your content in your template.

```html
<od-loading ng-show="$ctrl.loading"></od-loading>
```

Use the [ng-show](https://docs.angularjs.org/api/ng/directive/ngShow) direktive to show/hide the animation.

Initialize the attribute in your controller with `true` and disable the animation by setting the attribute to `false` as soon as everything is loaded. 

```js
this.loading = true;

$timeout(() => { this.loading = false; }, 1000);
```

### Example using $scope

The same example using $scope:

Template:

```html
<od-loading ng-show="loading"></od-loading>
```

Javascript:

```js
$scope.loading = true;
```

## Behavior

An `od-loading` element behaves like a `div` with the following css:

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
