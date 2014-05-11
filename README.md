bs-css-hacks
============

// Core variables and mixins
@import "mixins.less";

// Core CSS
@import "scaffolding.less";
@import "grid.less";
@import "forms.less";

// Components
https://github.com/twbs/bootstrap/pull/3552
@import "dropdowns.less";
@import "button-groups.less";
@import "input-groups.less";
https://github.com/h5bp/html5-boilerplate/issues/984#issuecomment-3985989
@import "media.less";
@import "list-group.less";
@import "panels.less";

// Components w/ JavaScript
@import "modals.less";
@import "tooltip.less";
@import "popovers.less";
@import "carousel.less";

//--------------

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
