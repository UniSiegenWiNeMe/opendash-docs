# fit-text Component

`fit-text` is an Angular Component, which allows you to scale font size to a maximum without creating overflow in parent containers.


# Usage

Use the `fit-text` Component in your template like this:

```html
<fit-text
  text="$ctrl.ft.text"
  group="$ctrl.ft.group"
  >
  </fit-text>
```

In your JS use the following code:

```js
this.ft = {
  text: "Your text",
  group: 1000, // sync group to sync multiple fit-text elements
};
```

`ftgroup` must be initialized at 1000.

# Examples of synchronization between multiple elements:

Multiple `fit-text` elements can be synced by using the same variable for `group`.

Example template:

```html
<fit-text
  fttext="$ctrl.ft1.text"
  ftgroup="$ctrl.ftgroup"
  >
  </fit-text>

<fit-text
  fttext="$ctrl.ft2.text"
  ftgroup="$ctrl.ftgroup"
  >
  </fit-text>
```

Javascript:

```js
this.ft1 = {
  text: "Text #1",
};


this.ft2 = {
  text: "Text #2",
};

this.ftgroup = "some random string";
```
