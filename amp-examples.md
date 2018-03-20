# Amp Snippets

## Sources:
* https://github.com/ampproject/amphtml/blob/master/spec/amp-html-layout.md

### Images

A simple responsive image, where width and height are used to determine the aspect ratio:
```html
<amp-img src="/img/amp.jpg"
    width="1080"
    height="610"
    layout="responsive"
    alt="an image"></amp-img>
```
---
A responsive image using the `sizes` attribute:
```html
<amp-img src="https://acme.org/image1.png"
    width="400" height="300"
    layout="responsive"
    sizes="(min-width: 320px) 320px, 100vw">
</amp-img>
```
---
Using the `heights` attribute:
```html
<amp-img src="https://acme.org/image1.png"
    width="320" height="256"
    heights="(min-width:500px) 200px, 80%">
</amp-img>
```
---
Using `media` attribute
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
* Depending on the screen width, one of the two images will be fetched and rendered
* The media attribute is available on all AMP elements
---
Using `placeholder` attribute
```html
<amp-anim src="animated.gif" width=466 height=355 layout="responsive" >
  <amp-img placeholder src="preview.png" layout="fill"></amp-img>
</amp-anim>
```
---
Using `fallback`
```html
<amp-anim src="animated.gif" width=466 height=355 layout="responsive" >
  <div fallback>Cannot play animated images on this device.</div>
</amp-anim>
```

----------
### Keyframes

#### Stylesheet
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
### Custom Fonts
* Must serve over https

```html
<link rel="stylesheet" href="https://fonts.googleapis.com/css?family=Tangerine">
```
---
