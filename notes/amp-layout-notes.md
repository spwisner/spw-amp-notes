# Amp Layout Notes

## Sources:
* https://github.com/ampproject/amphtml/blob/master/spec/amp-html-layout.md

## Notes

### Layout Attributes

#### `width` and `height`
* Depending on the value of the layout attribute, AMP component elements must have a width and height attribute that contains an integer pixel value.

#### `layout`
* AMP provides a set of layouts that specify how an AMP component behaves in the document layout.

You can specify a layout for a component by adding the `layout` attribute with one of the values specified in the table below:

<table>
  <thead>
    <tr>
      <th width="30%">Value</th>
      <th>Behavior  and  Requirements</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Not present</td>
      <td>If no value is specified, the layout for the component is inferred as follows:
        <ul>
          <li>If <code>height</code> is present and <code>width</code> is absent or is set to <code>auto</code>, a <code>fixed-height</code> layout is assumed.</li>
          <li>If <code>width</code> and <code>height</code> are present along with a <code>sizes</code> or <code>heights</code> attribute, a <code>responsive</code> layout is assumed.</li>
          <li>If <code>width</code> and <code>height</code> are present, a  <code>fixed</code> layout is assumed.</li>
          <li> if <code>width</code> and <code>height</code> are absent, a <code>container</code> layout is assumed.</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td><code>container</code></td>
      <td>The element lets its children define its size, much like a normal HTML <code>div</code>. The component is assumed to not have specific layout itself but only act as a container; its children are rendered immediately.</td>
    </tr>
    <tr>
      <td><code>fill</code></td>
      <td>The element takes the space available to it&mdash;both width and height. In other words, the layout and size of a <code>fill</code> element matches its parent. For an element to fill its parent container, specify the "fill" layout, and ensure the parent container specifies `position:relative` or `position:absolute`. </td>
    </tr>
    <tr>
      <td><code>fixed</code></td>
      <td>The element has a fixed width and height with no responsiveness supported. The <code>width</code> and <code>height</code> attributes must be present. The only exceptions are the <code>amp-pixel</code> and <code>amp-audio</code> components. </td>
    </tr>
    <tr>
      <td><code>fixed-height</code></td>
      <td>The element takes the space available to it but keeps the height unchanged. This layout works well for elements such as <code>amp-carousel</code> that involves content positioned horizontally. The <code>height</code> attribute must be present. The <code>width</code> attribute must not be present or must be equal to <code>auto</code>. </td>
    </tr>
    <tr>
      <td><code>flex-item</code></td>
      <td>The element and other elements in its parent with layout type <code>flex-item</code> take the parent container's remaining space when the parent is a flexible container (i.e., <code>display: flex</code>). The <code>width</code> and <code>height</code> attributes are not required.</td>
    </tr>
    <tr>
      <td><code>intrinsic</code></td>
      <td>The element takes the space available to it and resizes its height automatically to the aspect ratio given by the <code>width</code> and <code>height</code> attributes. This layout works very well for most AMP elements, including <code>amp-img</code>, <code>amp-video</code>, etc.  The available space depends on the parent element and can also be customized using <code>max-width</code> CSS. The <code>width</code> and <code>height</code> attributes must be present.  This layout differs from <code>responsive</code> by having an intrinsic height and width. This is most apparent inside a floated element where a <code>responsive</code> layout will render 0x0 and <code>intrinsic</code> layout will inflate to the smaller of its natural size or any CSS constraint. </td>
    </tr>
    <tr>
      <td><code>nodisplay</code></td>
      <td>The element isn't displayed, and takes up zero space on the screen as if its display style was <code>none</code>. This layout can be applied to every AMP element.  It’s assumed that the element can display itself on user action (e.g., <code>amp-lightbox</code>). The <code>width</code> and <code>height</code> attributes are not required.</td>
    </tr>
    <tr>
      <td><code>responsive</code></td>
      <td>The element takes the space available to it and resizes its height automatically to the aspect ratio given by the <code>width</code> and <code>height</code> attributes. This layout works very well for most AMP elements, including <code>amp-img</code>, <code>amp-video</code>, etc.  The available space depends on the parent element and can also be customized using <code>max-width</code> CSS. The <code>width</code> and <code>height</code> attributes must be present.<p><strong>Note</strong>: Elements with <code>"layout=responsive"</code> have no intrinsic size. The size of the element is determined from its container element. To ensure your AMP element displays, you must specify a width and height for the  containing element. Do not specify <code>"display:table"</code> on the containing element as this overrides the display of the AMP element, rendering the AMP element invisible.</p></td>
    </tr>
  </tbody>
</table>

#### `sizes`

* The `sizes` attribute describes how the width of the element is calculated depending on the media conditions.
* **Is extended to all elements, not just images**.

```html
<amp-img src="https://acme.org/image1.png"
    width="400" height="300"
    layout="responsive"
    sizes="(min-width: 320px) 320px, 100vw">
</amp-img>
```

#### `heights`

Differs from `sizes` for two reasons:
1. It applies to the height, not the width of the element.
2. Percent values are allowed, e.g. 86%. If a percent value is used, it indicates the percentage of the element's width.

```html
<amp-img src="https://acme.org/image1.png"
    width="320" height="256"
    heights="(min-width:500px) 200px, 80%">
</amp-img>
```

#### `media`
All AMP elements support the `media` attribute. The value of media is a media query.
* If the query does not match, the element is not rendered at all and its resources and potentially its child resources will not be fetched.
* If the browser window changes size or orientation, the media queries are re-evaluated

```html
<amp-img
    media="(min-width: 650px)"
    src="wide.jpg"
    width=466
    height=355 layout="responsive" ></amp-img>
<amp-img
    media="(max-width: 649px)"
    src="narrow.jpg"
    width=527
    height=193 layout="responsive" ></amp-img>
```
* In the example above, depending on the screen width, *one of the two images* will be fetched and rendered

#### `placeholder`
* The placeholder attribute indicates that the element marked with this attribute acts as a placeholder for the parent AMP element
* By default, the placeholder is immediately shown for the AMP element

```html
<amp-anim src="animated.gif" width=466 height=355 layout="responsive" >
  <amp-img placeholder src="preview.png" layout="fill"></amp-img>
</amp-anim>
```

#### `fallback`
* A fallback is a convention that allows the element to communicate to the reader that the browser does not support the element.
* If specified, a fallback element must be a direct child of the AMP element

```html
<amp-anim src="animated.gif" width=466 height=355 layout="responsive" >
  <div fallback>Cannot play animated images on this device.</div>
</amp-anim>
```

#### `noloading`
* The `noloading` attribute indicates whether the "loading indicator" should be turned off for this element.
* Opt out of this behavior by adding this attribute.

### Summary of Layout Requirements & Behaviors

<table>
  <thead>
    <tr>
      <th width="21%">Layout</th>
      <th width="20%">Width/<br>Height Required?</th>
      <th width="20%">Defines Size?</th>
      <th width="20%">Additional Elements</th>
      <th width="19%">CSS "display"</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code>container</code></td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td><code>block</code></td>
    </tr>
    <tr>
      <td><code>fill</code></td>
      <td>No</td>
      <td>Yes, parent's size.</td>
      <td>No</td>
      <td><code>block</code></td>
    </tr>
    <tr>
      <td><code>fixed</code></td>
      <td>Yes</td>
      <td>Yes, specified by <code>width</code> and <code>height</code>.</td>
      <td>No</td>
      <td><code>inline-block</code></td>
    </tr>
    <tr>
      <td><code>fixed-height</code></td>
      <td><code>height</code> only; <code>width</code> can be <code>auto</code></td>
      <td>Yes, specified by the parent container and <code>height</code>.</td>
      <td>No</td>
      <td><code>block</code></td>
    </tr>
    <tr>
      <td><code>flex-item</code></td>
      <td>No</td>
      <td>No</td>
      <td>Yes, based on parent container.</td>
      <td><code>block</code></td>
    </tr>
    <tr>
      <td><code>nodisplay</code></td>
      <td>No</td>
      <td>No</td>
      <td>No</td>
      <td><code>none</code></td>
    </tr>
    <tr>
      <td><code>responsive</code></td>
      <td>Yes</td>
      <td>Yes, based on parent container and aspect ratio of <code>width:height</code>.</td>
      <td>Yes, <code>i-amphtml-sizer</code>.</td>
      <td><code>block</code></td>
    </tr>
  </tbody>
</table>
