# fit-text Component

`fit-text` is an Angular Component, which allows you to scale it's font size to a maximum without creating overflow.


## Usage

Use the `fit-text` Component in your template like this:

```html
<fit-text
  fttext="$ctrl.ft.text"
  ftwidth="$ctrl.ft.width"
  ftheight="$ctrl.ft.height"
  ftgroup="$ctrl.ft.group"
  >
  </fit-text>
```

In your JS use the following code:

```js
this.ft = {
  text: "Your text",
  width: "100%", // width of the elements
  height: "50%", // height of the elements
  group: 1000, // sync group to sync multiple fit-text elements
};
```

`ftgroup` must be initialized at 1000.

### Examples of synchronization between multiple elements:

Multiple `fit-text` elements can be synced by using the same variable for `ftgroup`.

Example template:

```html
<fit-text
  fttext="$ctrl.ft1.text"
  ftwidth="$ctrl.ft1.width"
  ftheight="$ctrl.ft1.height"
  ftgroup="$ctrl.ftgroup"
  >
  </fit-text>

<fit-text
  fttext="$ctrl.ft2.text"
  ftwidth="$ctrl.ft2.width"
  ftheight="$ctrl.ft2.height"
  ftgroup="$ctrl.ftgroup"
  >
  </fit-text>
```

Javascript:

```js
this.ft1 = {
  text: "Text #1",
  width: "100%",
  height: "50%",
};


this.ft2 = {
  text: "Text #2",
  width: "100%",
  height: "50%",
};

this.ftgroup = 1000;
```