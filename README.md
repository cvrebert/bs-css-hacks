bs-css-hacks
============
```
// Core variables and mixins
// Mixins
// --------------------------------------------------

// Utilities
@import "mixins/opacity.less";
@import "mixins/image.less";
@import "mixins/resize.less";
@import "mixins/responsive-visibility.less";
@import "mixins/size.less";
@import "mixins/tab-focus.less";
@import "mixins/text-emphasis.less";
@import "mixins/text-overflow.less";
@import "mixins/vendor-prefixes.less";

// Components
@import "mixins/buttons.less";
@import "mixins/panels.less";
@import "mixins/pagination.less";
@import "mixins/list-group.less";
@import "mixins/nav-divider.less";
@import "mixins/forms.less";
@import "mixins/progress-bar.less";
@import "mixins/table-row.less";

// Skins
@import "mixins/gradients.less";

// Layout
@import "mixins/clearfix.less";
@import "mixins/center-block.less";
@import "mixins/nav-vertical-align.less";
@import "mixins/grid-framework.less";
@import "mixins/grid.less";

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

// Components w/ JavaScript
@import "modals.less";
@import "tooltip.less";
@import "popovers.less";

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

//--------------
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
