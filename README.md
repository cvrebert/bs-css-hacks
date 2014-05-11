bs-css-hacks
============
#### Index of CSS bugs/quirks/incompatibilities that Bootstrap works around.<br>Goal: Ensure each of these is mentioned in at least 1 [MDN](https://developer.mozilla.org/en-US/docs/Web)-like resource.

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
input[disabled] & {
  opacity: 1; // iOS fix for unreadable disabled content
}
```
* https://github.com/twbs/bootstrap/issues/11655

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
The Fennec default gradient (& file border) can be negated by:
```css
button,
textarea,
input[type="text"],
select[multiple]
{
  background-image: none;
}

input[type="file"] {
  border: none;
}
```

---
## Results

* https://developer.mozilla.org/en-US/docs/Web/CSS/::-moz-placeholder$compare?to=587215&from=522761
