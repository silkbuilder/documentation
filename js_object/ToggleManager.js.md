# ToggleManager
 The ToggleManager stores a list of element references and toggles the
`silk-hidden` CSS class on all of them with a single call to
[toggle](#ToggleManager+toggle).

Each entry in the toggle list can be one of the following:

| Entry            | What is toggled                                                                 | Needs `$object` |
|------------------|---------------------------------------------------------------------------------|:---------------:|
| `all`            | Every sibling of `$object` (and `$object` itself), except the element whose id equals `id`. | yes |
| `group`          | The closest ancestor of `$object` with the class `.silk-group`.                 | yes |
| `parent`         | The direct parent of `$object`.                                                 | yes |
| `grandpa`        | The parent of `$object`'s parent.                                               | yes |
| `#someId`        | The element(s) matched by the jQuery id selector.                               | no  |
| `.someClass`     | The element(s) matched by the jQuery class selector.                            | no  |
| `object.prop`    | `window.object.prop` (a global object's property that exposes `toggleClass`).   | no  |
| `name`           | `window.name` (a global object that exposes `toggleClass`, e.g. a Silk component). | no |

Prefixing any entry with `!` inverts it: that entry gets the opposite state
from the others. This makes it easy to swap two views, for example
`"#viewPanel,!#editPanel"`.

**Class semantics:** `status === true` **shows** the element (removes
`silk-hidden`) and `status === false` **hides** it (adds `silk-hidden`).
Entries prefixed with `!` behave the other way round.

**Inline styles:** when an element ends up visible, any inline
`display: none` on it (from jQuery's `.hide()` or a `style` attribute) is
cleared too, so removing `silk-hidden` really shows it. Other inline
`display` values are kept. This applies to both
[toggle](#ToggleManager+toggle) and [toggleElement](#ToggleManager+toggleElement).

Entries that cannot be resolved (an unknown global, a missing property)
are silently ignored.

**Kind**: global class  
**Requires**: <code>module:jQuery</code>, <code>module:ifUndefined</code>  


## Constructor
 <a name="_new"></a>

### new ToggleManager(toggleList, [id])
Creates a ToggleManager instance.


| Param | Type | Default | Description |
| --- | --- | --- | --- |
| toggleList | <code>string</code> |  | Comma-separated list of entries to toggle   (see the table above). Whitespace around entries is ignored. An empty   string makes [toggle](#ToggleManager+toggle) a no-op. |
| [id] | <code>string</code> | <code>&quot;\&quot;\&quot;&quot;</code> | Id of the element to keep out of the `all`   entry (usually the element that owns this manager). Only used by `all`.   - When `id` is empty, `all` only toggles siblings that **have** an id;     siblings without an id are left untouched.   - When `id` is set, `all` toggles every sibling except that id. Siblings     whose id matches a global object with a `toggle` method are toggled     through that object's `toggleClass`; all others are toggled directly. |

**Example** *(Toggle elements by id and class)*  
```js
// <div id="details">...</div>
// <p class="hint">...</p>
var tm = new ToggleManager("#details, .hint");

tm.toggle(false);  // adds "silk-hidden" → hides #details and every .hint
tm.toggle(true);   // removes "silk-hidden" → shows them again
```
**Example** *(Swap two panels with the &quot;!&quot; prefix)*  
```js
// <div id="viewPanel">...</div>
// <div id="editPanel" class="silk-hidden">...</div>
var panels = new ToggleManager("#viewPanel, !#editPanel");

panels.toggle(false);  // hides #viewPanel, shows #editPanel
panels.toggle(true);   // shows #viewPanel, hides #editPanel
```
**Example** *(Relative entries: group, parent and grandpa)*  
```js
// <div class="silk-group">
//   <div class="row">
//     <label><input id="nickname" type="text"></label>
//   </div>
// </div>
var $input = $("#nickname");

new ToggleManager("parent").toggle(false, $input);   // hides <label>
new ToggleManager("grandpa").toggle(false, $input);  // hides <div class="row">
new ToggleManager("group").toggle(false, $input);    // hides <div class="silk-group">

// Relative entries need $object; without it toggle() returns early.
new ToggleManager("parent").toggle(false);           // does nothing
```
**Example** *(Hide every sibling except one with &quot;all&quot;)*  
```js
// <div id="container">
//   <section id="mainPanel">...</section>
//   <section id="sidebar">...</section>
//   <section id="footerInfo">...</section>
// </div>
var $main = $("#mainPanel");
var focus = new ToggleManager("all", "mainPanel");

focus.toggle(false, $main);  // hides #sidebar and #footerInfo, keeps #mainPanel
focus.toggle(true, $main);   // shows them again
```
**Example** *(&quot;all&quot; combined with &quot;!&quot; to show the owner and hide the rest)*  
```js
// Hide all siblings, and explicitly make sure #mainPanel is visible.
var focus = new ToggleManager("all, !#mainPanel", "mainPanel");
focus.toggle(false, $("#mainPanel"));
```
**Example** *(Toggle global components by name)*  
```js
// Assuming global Silk components exist: window.customerGrid,
// window.toolbar.saveButton, each exposing toggleClass().
var tm = new ToggleManager("customerGrid, toolbar.saveButton");
tm.toggle(false);  // hides both components
```
**Example** *(Driving it from a checkbox)*  
```js
// Hide the shipping section while "Same as billing" is checked.
var shipping = new ToggleManager("#shippingAddress");
$("#sameAsBilling").on("change", function () {
    shipping.toggle(!this.checked); // checked → hidden, unchecked → shown
});
```
## Methods
 <a name="+toggle"></a>

### toggle(status, [$object]) ⇒ <code>void</code>
Shows or hides every entry in the toggle list.

Entries without a `!` prefix receive `status`; entries with a `!`
prefix receive `!status`.

Note: if an entry that needs `$object` (`all`, `group`, `parent`,
`grandpa`) is reached and `$object` is not provided, the method returns
immediately and any entries after it in the list are **not** processed.

**Kind**: instance method of [<code>ToggleManager</code>](#ToggleManager)  

| Param | Type | Description |
| --- | --- | --- |
| status | <code>boolean</code> | `true` shows (removes `silk-hidden`),   `false` hides (adds `silk-hidden`). Inverted for `!`-prefixed entries. |
| [$object] | <code>jQuery</code> | Reference element for the relative entries   `all`, `group`, `parent` and `grandpa`. Ignored by the other entry types. |

**Example**  
```js
var tm = new ToggleManager("#a, !#b");
tm.toggle(true);  // #a shown, #b hidden
```
**Example**  
```js
var tm = new ToggleManager("parent");
tm.toggle(true, $("#nickname"));  // shows the input's parent
```
<a name="ToggleManager+toggleElement"></a>

### toggleElement([status], $element) ⇒ <code>void</code>
Shows or hides a single jQuery element directly, without using the
toggle list given to the constructor.

`status` can take three forms:

| `status`     | Result                                                                 |
|--------------|------------------------------------------------------------------------|
| omitted      | Flips the current state: hidden becomes shown, shown becomes hidden.   |
| `true`       | Shows the element (removes `silk-hidden`).                             |
| `false`      | Hides the element (adds `silk-hidden`).                                |
| a function   | Called through `callFunction()`; a truthy result shows the element, a falsy result hides it. |

The `!` prefix and the relative entries (`all`, `group`, ...) do not
apply here; they belong to [toggle](#ToggleManager+toggle).

**Kind**: instance method of [<code>ToggleManager</code>](#ToggleManager)  
**Requires**: <code>module:callFunction</code>  

| Param | Type | Description |
| --- | --- | --- |
| [status] | <code>boolean</code> \| <code>function</code> | `true` shows, `false` hides, a   function decides at call time, and omitting it flips the current state. |
| $element | <code>jQuery</code> | The element to show or hide. Required. |

**Example** *(Show, hide and flip)*  
```js
var tm = new ToggleManager("");
var $help = $("#helpText");

tm.toggleElement(true, $help);       // shows #helpText
tm.toggleElement(false, $help);      // hides #helpText
tm.toggleElement(undefined, $help);  // flips: shows it again
```
**Example** *(Decide at call time with a function)*  
```js
// Show the discount row only when the cart total is over 100.
tm.toggleElement(function () {
    return cart.total > 100;
}, $("#discountRow"));
```

