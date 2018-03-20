# Amp Html Format Notes

## Sources:
* https://github.com/ampproject/amphtml/blob/master/spec/amp-html-format.md

## Notes

### HTML Tags

HTML tags can be used unchanged in AMP HTML. Certain tags have equivalent custom tags (such as `<img>` and `<amp-img>`) and other tags are outright prohibited:

<table>
  <tr>
    <th width="30%">Tag</th>
    <th>Status in AMP HTML</th>
  </tr>
  <tr>
    <td width="30%">script</td>
    <td>Prohibited unless the type is <code>application/ld+json</code>. (Other non-executable values may be added as needed.) Exception is the mandatory script tag to load the AMP runtime and the script tags to load extended components.</td>
  </tr>
  <tr>
    <td width="30%">noscript</td>
    <td>Allowed. Can be used anywhere in the document. If specified, the content inside the <code>&lt;noscript&gt;</code> element displays if JavaScript is disabled by the user.</td>
  </tr>
  <tr>
    <td width="30%">base</td>
    <td>Prohibited.</td>
  </tr>
  <tr>
    <td width="30%">img</td>
    <td>Replaced with <code>amp-img</code>.<br>
        Please note: <code>&lt;img&gt;</code> is a <a href="https://www.w3.org/TR/html5/syntax.html#void-elements">Void Element according to HTML5</a>, so it does not have an end tag. However, <code>&lt;amp-img&gt;</code> does have an end tag <code>&lt;/amp-img&gt;</code>.</td>
  </tr>
  <tr>
    <td width="30%">video</td>
    <td>Replaced with <code>amp-video</code>.</td>
  </tr>
  <tr>
    <td width="30%">audio</td>
    <td>Replaced with <code>amp-audio</code>.</td>
  </tr>
  <tr>
    <td width="30%">iframe</td>
    <td>Replaced with <code>amp-iframe</code>.</td>
  </tr>
    <tr>
    <td width="30%">frame</td>
    <td>Prohibited.</td>
  </tr>
  <tr>
    <td width="30%">frameset</td>
    <td>Prohibited.</td>
  </tr>
  <tr>
    <td width="30%">object</td>
    <td>Prohibited.</td>
  </tr>
  <tr>
    <td width="30%">param</td>
    <td>Prohibited.</td>
  </tr>
  <tr>
    <td width="30%">applet</td>
    <td>Prohibited.</td>
  </tr>
  <tr>
    <td width="30%">embed</td>
    <td>Prohibited.</td>
  </tr>
  <tr>
    <td width="30%">form</td>
    <td>Allowed. Require including <a href="https://www.ampproject.org/docs/reference/components/amp-form">amp-form</a> extension.</td>
  </tr>
  <tr>
    <td width="30%">input elements</td>
    <td>Mostly allowed with <a href="https://www.ampproject.org/docs/reference/components/amp-form#inputs-and-fields">exception of some input types</a>, namely, <code>&lt;input[type=image]&gt;</code>, <code>&lt;input[type=button]&gt;</code>, <code>&lt;input[type=password]&gt;</code>, <code>&lt;input[type=file]&gt;</code> are invalid. Related tags are also allowed: <code>&lt;fieldset&gt;</code>, <code>&lt;label&gt;</code></td>
  </tr>
  <tr>
    <td width="30%">button</td>
    <td>Allowed.</td>
  </tr>
  <tr>
    <td width="30%"><code><a name="cust"></a>style</code></td>
    <td><a href="#boilerplate">Required style tag for amp-boilerplate</a>. One additional style tag is allowed in head tag for the purpose of custom styling. This style tag must have the attribute <code>amp-custom</code>. <a href="#cust">🔗</a></td>
  </tr>
  <tr>
    <td width="30%">link</td>
    <td><code>rel</code> values registered on <a href="http://microformats.org/wiki/existing-rel-values">microformats.org</a> are allowed. If a <code>rel</code> value is missing from our whitelist, <a href="https://github.com/ampproject/amphtml/issues/new">please submit an issue</a>. <code>stylesheet</code> and other values like <code>preconnect</code>, <code>prerender</code> and <code>prefetch</code> that have side effects in the browser are disallowed. There is a special case for fetching stylesheets from whitelisted font providers.</td>
  </tr>
  <tr>
    <td width="30%">meta</td>
    <td>The <code>http-equiv</code> attribute may be used for specific allowable values; see the <a href="https://github.com/ampproject/amphtml/blob/master/validator/validator-main.protoascii">AMP validator specification</a> for details.</td>
  </tr>
  <tr>
    <td width="30%"><code><a name="ancr"></a>a</code></td>
    <td>The <code>href</code> attribute value must not begin with <code>javascript:</code>. If set, the <code>target</code> attribute value must be <code>_blank</code>. Otherwise allowed. <a href="#ancr">🔗</a></td>
  </tr>
  <tr>
    <td width="30%">svg</td>
    <td>Most SVG elements are allowed.</td>
  </tr>
</table>

### Comments
* Conditional HTML comments are not allowed

### HTML attributes

* Attribute names starting with `on` (such as `onclick` or `onmouseover`) are disallowed in AMP HTML.
* The attribute with the literal name `on` (no suffix) **is allowed**
* **The `style` attribute must not be used**
---
### Stylesheets
#### @-rules
* The following @-rules are allowed in stylesheets: `@font-face`, `@keyframes`, `@media`, `@supports`
* `@import` will not be allowed. Others may be added in the future.

#### Custom Styleshets
* Authors may add custom styles to a document using a single `<style amp-custom>` tag in the head of the document.
* Usage of the **!important** qualifier is not allowed
---
#### Properties

##### Banned Properties:
* `behavior`
* `-moz-binding`

##### Transitions
* AMP only allows transitions and animations of properties that can be GPU accelerated in common browsers.
* Whitelisted:
  - `opacity`
  - `transform` (also `-vendorPrefix-transform`)

##### Overflow
* `overflow` (and `overflow-y`, `overflow-x`) **may not** be styled as “auto” or “scroll”.

---
### Keyframes stylesheet

The following restrictions apply to the `<style amp-keyframes>` tag:
 1. May only be placed as the last child of the document's `<body>` element.
 2. May only contain `@keyframes`, `@media`, `@supports` rules and their combination.
 3. May not be larger than 500,000 bytes.

 ```html
 <style amp-keyframes>
 @keyframes anim1 {}

 @media (min-width: 600px) {
   @keyframes anim1 {}
 }
 </style>
 </body>
```
---

## Amp Components

### Types of Amp Components
* **Built In** (always available in an AMP document and have a dedicated custom element - <amp-img>)
* **Extended** (must be explicitly included into the document)
---
#### On
* The on attribute is used to install event handlers on elements. The events that are supported depend on the element.
* The value for the syntax is a simple domain specific language of the form:

```javascript
eventName:targetId[.methodName[(arg1=value, arg2=value)]]
```

Examples:
* `on="tap:fooId.showLightbox"`
* `on="submit-success:lightbox1;submit-error:lightbox2"`
---
#### Extended Components
* Extended components are components that do not necessarily ship with the AMP runtime. Instead they must be explicitly included into the document.Extended components are loaded by including a <script> tag
* The <script> tag must have an async attribute and must have a custom-element attribute referencing the name of the element

```javascript
<script async custom-element="amp-carousel" src="https://cdn.ampproject.org/v0/amp-carousel-0.1.js"></script>
```
