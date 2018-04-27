# Mangle props in Uglifyjs2 vs Uglifyjs3

To reproduce, first minify preact with v2 and v3:

```bash
cd uglifyjs3 && npm run build
cd uglifyjs2 && npm run build
```

and then compare both `dist/preact.js` files. Notice how the exports have been mangled with uglifyjs3, but remain stable with uglifyjs2.

Expected (with uglifyjs v2):

```js
!(function() {
  "use strict";
  function VNode() {}
  function h(nodeName, attributes) {}
  //...snip
  var preact = {
    h: h,
    createElement: h,
    cloneElement: cloneElement,
    Component: Component,
    render: render,
    rerender: rerender,
    options: options
  };
  if ("undefined" != typeof module) module.exports = preact;
  else self.preact = preact;
})();
```

Acutal (with uglifyjs v3):

```js
!(function() {
  "use strict";
  function u() {}
  var T = {};
  var s = [];
  var v = [];
  function n(i, f) {}
  //...snip
  var i = {
    I: n,
    createElement: n,
    N: function(i, f) {
      return n(
        i.nodeName,
        _(_({}, i.attributes), f),
        2 < arguments.length ? [].slice.call(arguments, 2) : i.children
      );
    },
    O: g,
    p: function(i, f, n) {
      return L(n, i, {}, !1, f, !1);
    },
    U: r,
    options: T
  };
  if ("undefined" != typeof module) module.q = i;
  else self.A = i;
})();
```
