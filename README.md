bs-css-hacks
============
#### Index of CSS bugs/quirks/incompatibilities that [Bootstrap](https://github.com/twbs/bootstrap) works around, as of v3.2.0.<br>Goal: Ensure that each of these is mentioned in at least 1 [MDN](https://developer.mozilla.org/en-US/docs/Web)-like resource.<br>Because a common wiki is better than a bunch of scattered blog posts.
This list is based on scanning through the comments in Bootstrap's Less source code and the various warnings in Bootstrap's docs.

---
## To be documented

---
### iOS date input
```
// In Mobile Safari, date inputs require a pixel line-height that matches the
// given height of the input.
```
* https://github.com/twbs/bootstrap/issues/11266
  * @mdo: "the comment seems to imply unitless values are busted"
* https://github.com/twbs/bootstrap/pull/13099

---
### IE8 line wrapping bug
```css
label {
  display: inline-block;
  max-width: 100%; // Force IE8 to wrap long content
}
```
* See https://github.com/twbs/bootstrap/issues/13141
* No idea as to the cause; hasLayout maybe???
  * http://www.sitepoint.com/web-foundations/internet-explorer-haslayout-property/

---
### IE8 text input rendering bug when parent has opacity alpha filter
> Seems there is a bug in IE7-8 where `input[type="text"]` & `<textarea>` that are in a container which has `filter: alpha(opacity=N);` are not re-rendered when being typed in.
>
> Curiously enough, if you move your mouse out of the parent with the `filter`, the text will magically appear / update.

* See https://github.com/twbs/bootstrap/pull/3552
* http://jsbin.com/pisagahi/1

---
### IE8 and CSS max-width on images
* https://github.com/h5bp/html5-boilerplate/issues/984#issuecomment-3985989

---
### IE9 `display: table-cell` bug
```
// IE9 fubars the placeholder attribute in text inputs and the arrows on
// select elements in input groups. To fix it, we float the input.
```
* Details: https://github.com/twbs/bootstrap/issues/11561#issuecomment-28936855

---
### Viewport width bug in IE10 in Windows 8 and Windows Phone 8

```css
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
* http://getbootstrap.com/getting-started/#support-ie10-width
* Supposedly [fixed in Windows Phone 8 Update 3 (a.k.a. GDR3)](http://blogs.windows.com/windows_phone/b/wpdev/archive/2013/10/14/introducing-windows-phone-preview-for-developers.aspx)
  * Although apparently there's some dispute as to whether the Lumia Black version of GDR3 actually fixed this, particularly for Lumia 920 phones
    * https://github.com/twbs/bootstrap/issues/8719#issuecomment-35170732
    * https://github.com/twbs/bootstrap/issues/12285#issuecomment-32753285
    * https://github.com/twbs/bootstrap/issues/13238#issue-30487014

---
### IE9 click events require background-color bug
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
* https://github.com/twbs/bootstrap/pull/11186
* https://github.com/twbs/bootstrap/commit/6a93a6b88a4b874fba5a1d1edd817cbd91ccfacc
* Explicit `background-color: transparent;` does not help
* `filter: alpha(opacity=0);` alone does not help
* `opacity: 0;` alone does not help
  * is not supported in IE8
  * is supported in IE9, but setting only an `opacity` doesn't avoid the bug
* IE9: `opacity` + non-`transparent` `background-color` works as a fix
* `rgba(0,0,0,0)`
  * is not supported in IE8
  * works as a fix in IE9
* IE8-9: `filter: alpha(opacity=0);` + non-`transparent` `background-color` probably
* Need to test `background: transparent`

---
## Resulting documentation improvements

The following incompatibilities have been successfully documented in [MDN](https://developer.mozilla.org/en-US/docs/Web):
* [`<fieldset>` `min-width` legacy weirdness](https://github.com/twbs/bootstrap/issues/12359)
  * https://developer.mozilla.org/en-US/docs/Web/HTML/Element/fieldset$compare?to=589697&from=584707
* [iOS Safari `[disabled]` opacity](https://github.com/twbs/bootstrap/issues/11655)
  * https://developer.mozilla.org/en-US/docs/Web/HTML/Element/Input$compare?to=588017&from=572223
  * https://developer.mozilla.org/en-US/docs/Web/HTML/Element/textarea$compare?to=588343&from=587245
* [Android Browser `<select>` menu indicator triangle bug](http://getbootstrap.com/getting-started/#support-android-stock-browser)
  * https://developer.mozilla.org/en-US/docs/Web/HTML/Element/select$compare?to=590135&from=590133
* [Firefox `placeholder` text opacity](https://github.com/twbs/bootstrap/pull/11526)
  * https://developer.mozilla.org/en-US/docs/Web/CSS/::-moz-placeholder$compare?to=587215&from=522761
* [Firefox for Android gradients on form controls](https://github.com/twbs/bootstrap/issues/8702)
  * https://developer.mozilla.org/en-US/docs/Web/HTML/Element/button$compare?to=587233&from=584697
  * https://developer.mozilla.org/en-US/docs/Web/HTML/Element/select$compare?to=587235&from=536155
  * https://developer.mozilla.org/en-US/docs/Web/HTML/Element/textarea$compare?to=587243&from=578897
  * https://developer.mozilla.org/en-US/docs/Web/HTML/Element/Input$compare?to=588303&from=588017
* [Firefox for Android border on `input[type="file"]`](https://github.com/twbs/bootstrap/issues/8702)
  * https://developer.mozilla.org/en-US/docs/Web/HTML/Element/Input$compare?to=588351&from=588303
* [`resize` requires `overflow` other than `visible`](https://github.com/twbs/bootstrap/pull/13600)
  * [Is already documented in MDN.](https://developer.mozilla.org/en-US/docs/Web/CSS/resize) The Bootstrap source code comment was in error.

Hopefully these edits will survive in some form and not get wholesale reverted.
