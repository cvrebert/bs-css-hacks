bs-css-hacks
============
#### Index of CSS bugs/quirks/incompatibilities that [Bootstrap](https://github.com/twbs/bootstrap) works around, as of v3.2.0.<br>Goal: Ensure that each of these is mentioned in at least 1 [MDN](https://developer.mozilla.org/en-US/docs/Web)-like resource.<br>Because a common wiki is better than a bunch of scattered blog posts.
This list is based on scanning through the comments in Bootstrap's Less source code and the various warnings in Bootstrap's docs.

---
## To be documented

---
### iOS temporal `<input>` vertical text alignment when `display: block`
* The issue seems to be caused by setting `display: block;` on the temporal `<input>`
* https://github.com/twbs/bootstrap/issues/11266
* https://github.com/twbs/bootstrap/pull/13099
* Demo courtesy @mdo: http://jsbin.com/purer/1/
* Enhanced demo courtesy @mdo: http://jsbin.com/purer/2/

---
### IE8 `inline-block` + `float` line wrapping bug
```css
label {
  display: inline-block;
  max-width: 100%; // Force IE8 to wrap long content
}
```
* See https://github.com/twbs/bootstrap/issues/13141
* Progress on a reduced testcase: https://github.com/cvrebert/bootstrap/tree/ie8-label-wrap-bug
* Possibly related to http://stackoverflow.com/questions/22550988/native-ie8-why-do-these-inline-block-elements-not-wrap-words-if-their-pare ?

---
### IE8 and CSS `max-width` on images
* https://github.com/twbs/bootstrap/issues/9239
* https://github.com/h5bp/html5-boilerplate/issues/984#issuecomment-3985989

---
### IE9 `<input>` `display: table-cell` bug
```
// IE9 fubars the placeholder attribute in text inputs and the arrows on
// select elements in input groups. To fix it, we float the input.
```
* Details: https://github.com/twbs/bootstrap/issues/11561#issuecomment-28936855

---
### IE8-9 click events require non-`transparent` `background-color` bug
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
* IE8-9: `filter: alpha(opacity=0);` + non-`transparent` `background-color` works as a fix

---
### `:hover` and/or `:focus` stickiness on mobile browsers
* Bootstrap doesn't currently have any code specificially related to this, but there have been a few bug reports about this, so I figure it oughtta be mentioned in MDN.
* https://github.com/google/WebFundamentals/blob/master/src/site/documentation/user-input/touch-input/activestates/index.markdown#hover-and-focus-stickiness

---
## Resulting documentation improvements

The following incompatibilities have been successfully documented in [MDN](https://developer.mozilla.org/en-US/docs/Web):
* [`<fieldset>` `min-width` legacy weirdness](https://github.com/twbs/bootstrap/issues/12359)
  * https://developer.mozilla.org/en-US/docs/Web/HTML/Element/fieldset$compare?to=592121&from=584707
* [`resize` requires `overflow` other than `visible`](https://github.com/twbs/bootstrap/pull/13600)
  * [Is already documented in MDN.](https://developer.mozilla.org/en-US/docs/Web/CSS/resize) The Bootstrap source code comment was in error.
  * Also filed https://github.com/CSSLint/csslint/issues/517
* [iOS Safari `[disabled]` opacity](https://github.com/twbs/bootstrap/issues/11655)
  * https://developer.mozilla.org/en-US/docs/Web/HTML/Element/Input$compare?to=588017&from=572223
  * https://developer.mozilla.org/en-US/docs/Web/HTML/Element/textarea$compare?to=588343&from=587245
* [Android Browser `<select>` menu indicator triangle bug](http://getbootstrap.com/getting-started/#support-android-stock-browser)
  * https://developer.mozilla.org/en-US/docs/Web/HTML/Element/select$compare?to=590135&from=590133
* [Viewport `device-width` bug in IE10 on Windows 8 and Windows Phone 8](https://github.com/twbs/bootstrap/issues/10497)
  * https://developer.mozilla.org/en-US/docs/Web/CSS/@viewport$compare?to=592567&from=592565
* [Firefox `placeholder` text opacity](https://github.com/twbs/bootstrap/pull/11526)
  * https://developer.mozilla.org/en-US/docs/Web/CSS/::-moz-placeholder$compare?to=592109&from=522761
  * https://github.com/Fyrd/caniuse/pull/549
* [Firefox for Android gradients on form controls](https://github.com/twbs/bootstrap/issues/8702)
  * https://developer.mozilla.org/en-US/docs/Web/HTML/Element/button$compare?to=587233&from=584697
  * https://developer.mozilla.org/en-US/docs/Web/HTML/Element/select$compare?to=587235&from=536155
  * https://developer.mozilla.org/en-US/docs/Web/HTML/Element/textarea$compare?to=587243&from=578897
  * https://developer.mozilla.org/en-US/docs/Web/HTML/Element/Input$compare?to=588303&from=588017
* [Firefox for Android border on `input[type="file"]`](https://github.com/twbs/bootstrap/issues/8702)
  * https://developer.mozilla.org/en-US/docs/Web/HTML/Element/Input$compare?to=588351&from=588303

Hopefully these edits will survive in some form and not get wholesale reverted.

---
## Unable to reproduce, so still undocumented
### IE8 text input rendering bug when parent has opacity alpha filter
> Seems there is a bug in IE7-8 where `input[type="text"]` & `<textarea>` that are in a container which has `filter: alpha(opacity=N);` are not re-rendered when being typed in.
>
> Curiously enough, if you move your mouse out of the parent with the `filter`, the text will magically appear / update.

* See https://github.com/twbs/bootstrap/pull/3552
* http://jsbin.com/bazakefu/3/
* **Unable to reproduce in IE7 or IE8 on Sauce Labs**
* Perhaps related to http://snook.ca/archives/html_and_css/ie-position-fixed-opacity-filter ?
  * Couldn't repro this on Sauce either...
