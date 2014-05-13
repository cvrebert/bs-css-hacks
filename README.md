bs-css-hacks
============
#### Index of CSS bugs/quirks/incompatibilities that Bootstrap works around.<br>Goal: Ensure that each of these is mentioned in at least 1 [MDN](https://developer.mozilla.org/en-US/docs/Web)-like resource.<br>Because a common wiki is better than a bunch of scattered blog posts.
This list is based on scanning through the comments in Bootstrap's Less source code and the various warnings in Bootstrap's docs.

---
## To be documented

---
```
// Special styles for iOS date input
//
// In Mobile Safari, date inputs require a pixel line-height that matches the
// given height of the input. Since this fucks up everything else, we have to
// appropriately reset it for Internet Explorer and the size variations.
```

---
```css
label {
  display: inline-block;
  max-width: 100%; // Force IE8 to wrap long content
}
```
* See https://github.com/twbs/bootstrap/issues/13141

---
```css
fieldset {
  // Chrome and Firefox set a `min-width: -webkit-min-content;` on fieldsets,
  // so we reset that to ensure it behaves more like a standard block element.
  // 
  min-width: 0;
}
```
* See https://github.com/twbs/bootstrap/issues/12359.

---
* `resize` requires `overflow: auto;` in Safari (version unknown)
* http://stackoverflow.com/questions/1837926/css3-resize-in-webkit-safari

---
* https://github.com/twbs/bootstrap/pull/3552

---
[Android `<select>` bug](http://getbootstrap.com/getting-started/#support-android-stock-browser)

---
[IE viewport width bug](http://getbootstrap.com/getting-started/#support-ie10-width)

---
* https://github.com/h5bp/html5-boilerplate/issues/984#issuecomment-3985989

---
```
// IE9 fubars the placeholder attribute in text inputs and the arrows on
// select elements in input groups. To fix it, we float the input.
```
* Details: https://github.com/twbs/bootstrap/issues/11561#issuecomment-28936855

---
```css
// IE10 in Windows (Phone) 8
//
// Support for responsive views via media queries is kind of borked in IE10, for
// Surface/desktop in split view and for Windows Phone 8. This particular fix
// must be accompanied by a snippet of JavaScript to sniff the user agent and
// apply some conditional CSS to *only* the Surface/desktop Windows 8. Look at
// our Getting Started page for more information on this bug.
//
// For more information, see the following:
//
// Issue: https://github.com/twbs/bootstrap/issues/10497
// Docs: http://getbootstrap.com/getting-started/#browsers
// Source: http://timkadlec.com/2012/10/ie10-snap-mode-and-responsive-design/

@-ms-viewport {
  width: device-width;
}
```
---
```css
// IE8-9 hack for event handling
//
// Internet Explorer 8-9 does not support clicks on elements without a set
// `background-color`. We cannot use `filter` since that's not viewed as a
// background color by the browser. Thus, a hack is needed.
//
// For IE8, we set solid black as it doesn't support `rgba()`. For IE9, we
// set alpha transparency for the best results possible.
background-color: #000 \9; // IE8
background-color: rgba(0,0,0,0); // IE9
```

---
## Resulting documentation improvements

The following incompatibilities have been successfully documented in [MDN](https://developer.mozilla.org/en-US/docs/Web):
* [Firefox placeholder text opacity](https://github.com/twbs/bootstrap/pull/11526)
  * https://developer.mozilla.org/en-US/docs/Web/CSS/::-moz-placeholder$compare?to=587215&from=522761
* [Firefox for Android gradients on form controls](https://github.com/twbs/bootstrap/issues/8702)
  * https://developer.mozilla.org/en-US/docs/Web/HTML/Element/button$compare?to=587233&from=584697
  * https://developer.mozilla.org/en-US/docs/Web/HTML/Element/select$compare?to=587235&from=536155
  * https://developer.mozilla.org/en-US/docs/Web/HTML/Element/textarea$compare?to=587243&from=578897
  * https://developer.mozilla.org/en-US/docs/Web/HTML/Element/Input$compare?to=588303&from=588017
* [Firefox for Android border on `input[type="file"]`](https://github.com/twbs/bootstrap/issues/8702)
  * https://developer.mozilla.org/en-US/docs/Web/HTML/Element/Input$compare?to=588351&from=588303
* [iOS Safari `[disabled]` opacity](https://github.com/twbs/bootstrap/issues/11655)
  * https://developer.mozilla.org/en-US/docs/Web/HTML/Element/Input$compare?to=588017&from=572223
  * https://developer.mozilla.org/en-US/docs/Web/HTML/Element/textarea$compare?to=588343&from=587245

Hopefully these edits will survive in some form and not get wholesale reverted.
