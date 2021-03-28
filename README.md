## Table of Content

- [Table of Content](#table-of-content)
- [Description](#description)
- [Browser Support](#browser-support)
- [Usage](#usage)
- [Options](#options)
    - [hashTracking](#hashtracking)
    - [closeOnConfirm](#closeonconfirm)
    - [closeOnCancel](#closeoncancel)
    - [closeOnEscape](#closeonescape)
    - [closeOnOutsideClick](#closeonoutsideclick)
    - [modifier](#modifier)
    - [appendTo](#appendto)
- [Globals](#globals)
    - [NAMESPACE](#namespace)
    - [DEFAULTS](#defaults)
- [Methods](#methods)
- [Events](#events)
- [CSS](#css)
    - [Classes](#classes)
    - [States](#states)
    - [Modifier](#modifier-1)
- [Credits](#credits)
- [License](#license)

## Description
Smoothup is a modal that works. Write your modal output in HTML. The DOM will stay there. Smoothup would turn it into a modal.

Smoothup was based on [Remodal](https://github.com/VodkaBears/Remodal/) which is no longer actively maintained. But thanks for their works! That plugin was awesome.

## Browser Support

- Modern browsers which are up to date.

## Usage

Download the latest version from [GitHub](https://github.com/usefulteam/smoothup/releases/latest)

Include the CSS files from the dist folder in the head section:
```html
<link rel="stylesheet" href="dist/smoothup.min.css">
<link rel="stylesheet" href="dist/smoothup-default-theme.min.css">
```

Include the JS file from the dist folder before the `</body>`:
```html
<script src="dist/smoothup.min.js"></script>
```

You can define the background container for the modal(for effects like a blur). It can be any simple content wrapper:
```html
<div class="smoothup-bg">
...Page content...
</div>
```

And now create the modal dialog:
```html
<div class="smoothup" data-smoothup-id="modal">
  <button data-smoothup-action="close" class="smoothup-close"></button>
  <h1>Smoothup</h1>
  <p>
    Responsive, lightweight, fast, synchronized with CSS animations, fully customizable modal window plugin with declarative configuration and hash tracking.
  </p>
  <br>
  <button data-smoothup-action="cancel" class="smoothup-cancel">Cancel</button>
  <button data-smoothup-action="confirm" class="smoothup-confirm">OK</button>
</div>
```

Don't use the `id` attribute, if you want to avoid the anchor jump, use `data-smoothup-id`.

So, now you can call it with the hash:
```html
<a href="#modal">Call the modal with data-smoothup-id="modal"</a>
```
Or:
```html
<a data-smoothup-target="modal">Call the modal with data-smoothup-id="modal"</a>

## Initialization with JavaScript

Do not set the 'smoothup' class, if you prefer a JS initialization.
```html
<div data-smoothup-id="modal">
  <button data-smoothup-action="close" class="smoothup-close"></button>
  <h1>Smoothup</h1>
  <p>
    Responsive, lightweight, fast, synchronized with CSS animations, fully customizable modal window plugin with declarative configuration and hash tracking.
  </p>
</div>
<script>
    var options = {...};

    $('[data-smoothup-id=modal]').smoothup(options);
</script>
```

## Options

You can pass additional options with the `data-smoothup-options` attribute.
```html
<div class="smoothup" data-smoothup-id="modal"
  data-smoothup-options="hashTracking: false, closeOnOutsideClick: false">

  <button data-smoothup-action="close" class="smoothup-close"></button>
  <h1>Smoothup</h1>
  <p>
    Responsive, lightweight, fast, synchronized with CSS animations, fully customizable modal window plugin with declarative configuration and hash tracking.
  </p>
  <br>
  <button data-smoothup-action="cancel" class="smoothup-cancel">Cancel</button>
  <button data-smoothup-action="confirm" class="smoothup-confirm">OK</button>
</div>
```

#### hashTracking
`Default: true`

To open the modal without the hash, use the `data-smoothup-target` attribute.
```html
<a data-smoothup-target="modal" href="#">Call the modal with data-smoothup-id="modal"</a>
```

#### closeOnConfirm
`Default: true`

If true, closes the modal window after clicking the confirm button.

#### closeOnCancel
`Default: true`

If true, closes the modal window after clicking the cancel button.

#### closeOnEscape
`Default: true`

If true, closes the modal window after pressing the ESC key.

#### closeOnOutsideClick
`Default: true`

If true, closes the modal window by clicking anywhere on the page.

#### modifier
`Default: ''`

Modifier CSS classes for the modal that is added to the overlay, modal, background and wrapper (see [CSS](#css)).

#### appendTo
`Default: document.body`

## Globals

```html
<script>
window.SMOOTHUP_GLOBALS = {
  NAMESPACE: 'modal',
  DEFAULTS: {
    hashTracking: false
  }
};
</script>
<script src="../dist/smoothup.js"></script>
```

#### NAMESPACE

Base HTML class for your modals. CSS theme should be updated to reflect this.

#### DEFAULTS

Extends the default settings.

## Methods

Get the instance of the modal and call a method:
```js
var inst = $('[data-smoothup-id=modal]').smoothup();

/**
 * Opens the modal window
 */
inst.open();

/**
 * Closes the modal window
 */
inst.close();

/**
 * Returns a current state of the modal
 * @returns {'closed'|'closing'|'opened'|'opening'}
 */
inst.getState();

/**
 * Destroys the modal window
 */
inst.destroy();
```

## Events

```js
$(document).on('opening', '.smoothup', function () {
  console.log('Modal is opening');
});

$(document).on('opened', '.smoothup', function () {
  console.log('Modal is opened');
});

$(document).on('closing', '.smoothup', function (e) {

  // Reason: 'confirmation', 'cancellation'
  console.log('Modal is closing' + (e.reason ? ', reason: ' + e.reason : ''));
});

$(document).on('closed', '.smoothup', function (e) {

  // Reason: 'confirmation', 'cancellation'
  console.log('Modal is closed' + (e.reason ? ', reason: ' + e.reason : ''));
});

$(document).on('confirmation', '.smoothup', function () {
  console.log('Confirmation button is clicked');
});

$(document).on('cancellation', '.smoothup', function () {
  console.log('Cancel button is clicked');
});
```

## CSS

#### Classes

`.smoothup` – the default class of modal dialogs.

`.smoothup-wrapper` – the additional wrapper for the `.smoothup`, it is not the overlay and used for the alignment.

`.smoothup-overlay` – the overlay of modal dialogs, it is under the wrapper.

`.smoothup-bg` – the background of modal dialogs, it is under the overlay and usually it is the wrapper of your content. You should add it on your own.

The `smoothup` prefix can be changed in the global settings. See [the `NAMESPACE` option](#namespace).

#### States

States are added to the `.smoothup`, `.smoothup-overlay`, `.smoothup-bg`, `.smoothup-wrapper` classes.

List:
```
.smoothup-is-opening
.smoothup-is-opened
.smoothup-is-closing
.smoothup-is-closed
```

#### Modifier

A modifier that is specified in the [options](#options) is added to the `.smoothup`, `.smoothup-overlay`, `.smoothup-bg`, `.smoothup-wrapper` classes.

## Credits

- [Remodal](https://github.com/VodkaBears/Remodal/) by [Ilya Caulfield](https://github.com/VodkaBears/).
  Smoothup was based on [Remodal](https://github.com/VodkaBears/Remodal/). Thanks a lot!

## License
- [Remodal License](https://github.com/vodkabears/Smoothup/blob/master/LICENSE)
- [Smoothup License](https://oss.ninja/mit?organization=Useful%20Team)

