bs-css-hacks
============
#### Index of CSS bugs/quirks/incompatibilities that [Bootstrap](https://github.com/twbs/bootstrap) works around, as of v3.2.0.<br>Goal: Ensure that each of these is mentioned in at least 1 [MDN](https://developer.mozilla.org/en-US/docs/Web)-like resource.<br>Because a common wiki is better than a bunch of scattered blog posts.
This list is based on scanning through the comments in Bootstrap's Less source code and the various warnings in Bootstrap's docs.

---
## To be documented

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
* [iOS temporal `<input>` with `display: block` has its text vertically misaligned](https://github.com/twbs/bootstrap/issues/11266)
  * https://developer.mozilla.org/en-US/docs/Web/HTML/Element/Input$compare?to=596375&from=596363
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
* [IE8-9 `click` events on `transparent` overlaid elements bug](https://github.com/twbs/bootstrap/pull/11186)
  * https://developer.mozilla.org/en-US/docs/Web/Reference/Events/click$compare?to=615503&from=402259
  * https://developer.mozilla.org/en-US/docs/Web/CSS/background-color$compare?to=615509&from=494737

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
