# Vanilla Scroll Sky
<img width="808" height="418" alt="AISelect_20260506_215346_Chrome" src="https://github.com/user-attachments/assets/db855679-5cb4-4c50-a2a4-6ff86283e92f" />


A pure CSS scrollytelling utility for sticky image reveals and moving captions.

Vanilla Scroll Sky uses normal HTML, CSS classes, CSS Custom Properties, CSS Cascade Layers, `@scope`, container queries, `position: sticky`, and CSS scroll-driven animations.

No JavaScript. No Web Components. No framework.

## Status

Vanilla Scroll Sky targets modern browsers.

The sticky layout remains readable without scroll-driven animations. If `animation-timeline: view()` is not supported, images and captions are shown without transform animations.

## Features

- Pure CSS
- No JavaScript
- No framework
- Sticky image stage
- Scroll-driven image reveal
- Optional moving caption
- Per-instance configuration with CSS Custom Properties
- Scoped component styles with `@scope`
- Cascade organization with `@layer`
- Container query hook with a named container
- Reduced-motion handling
- Fallback for missing scroll-driven animations

## Installation

Copy `src/vanilla-scroll-sky.css` into your project and include it:

```html
<link rel="stylesheet" href="/assets/css/vanilla-scroll-sky.css">
```

If your site already uses Cascade Layers, import it into your components layer:

```css
@layer base, components, utilities;

@import url("/assets/css/vanilla-scroll-sky.css") layer(components);
```

## Basic markup

```html
<section class="vss vss--image-left">
  <div class="vss__image">
    <img src="image.jpg" alt="Description of the image">
  </div>

  <div class="vss__caption">
    <h2>Caption heading</h2>
    <p>This text scrolls over the sticky image.</p>
  </div>
</section>
```

If there is no caption, omit the caption element:

```html
<section class="vss vss--image-right">
  <div class="vss__image">
    <img src="image.jpg" alt="Description of the image">
  </div>
</section>
```

## Image reveal classes

Use one of these classes on the `.vss` element:

```txt
vss--image-left
vss--image-right
vss--image-top
vss--image-bottom
vss--image-none
```

Example:

```html
<section class="vss vss--image-left">
```

## Caption motion classes

Use one of these classes on the `.vss` element:

```txt
vss--caption-left-center
vss--caption-right-center
vss--caption-left-right
vss--caption-right-left
```

Recommended readable options:

```txt
vss--caption-left-center
vss--caption-right-center
```

Stronger pass-through options:

```txt
vss--caption-left-right
vss--caption-right-left
```

Use pass-through motion mainly for short captions, labels, or visual emphasis.

## Per-instance configuration

Set CSS Custom Properties on the `.vss` element:

```html
<section
  class="vss vss--image-bottom vss--caption-left-center"
  style="
    --vss-image-stick-top: 4.5rem;
    --vss-image-height: 62svh;
    --vss-scene-duration: 220svh;
    --vss-caption-delay: 36svh;
    --vss-caption-motion-distance: 80vw;
  "
>
```

## Custom properties

### Timing and layout

```txt
--vss-scene-duration
--vss-caption-delay
--vss-scene-exit-space
--vss-image-stick-top
--vss-image-height
```

### Image reveal

```txt
--vss-image-start-offset
--vss-image-start-scale
--vss-image-fit
--vss-image-position
```

### Caption

```txt
--vss-caption-motion-distance
--vss-caption-max-width
--vss-caption-padding
```

## Defaults

```css
.vss {
  --vss-scene-duration: 220svh;
  --vss-caption-delay: 40svh;
  --vss-caption-motion-distance: 80vw;
  --vss-image-stick-top: 0;
  --vss-image-height: 66svh;
  --vss-image-start-offset: 4rem;
  --vss-image-start-scale: .96;
  --vss-scene-exit-space: 55svh;
  --vss-caption-max-width: 52rem;
  --vss-caption-padding: clamp(1.5rem, 4vw, 3rem);
  --vss-image-fit: cover;
  --vss-image-position: center;
}
```

## Strong image reveal

To make an image appear strongly from the left:

```html
<section
  class="vss vss--image-left"
  style="--vss-image-start-offset: 100vw;"
>
```

## Subtle caption motion

```html
<section
  class="vss vss--caption-right-center"
  style="--vss-caption-motion-distance: 6rem;"
>
```

## Image fitting

```html
<section
  class="vss vss--image-right"
  style="--vss-image-fit: contain;"
>
```

For wide images where the important content is on the left:

```html
<section
  class="vss vss--image-left"
  style="--vss-image-position: left top;"
>
```

## CSS functions

Custom properties can use normal CSS values and functions:

```html
<section
  class="vss vss--image-bottom vss--caption-left-center"
  style="
    --vss-image-height: clamp(28rem, 65svh, 44rem);
    --vss-scene-duration: calc(190svh + 20rem);
    --vss-caption-delay: clamp(18rem, 35svh, 32rem);
    --vss-caption-motion-distance: clamp(8rem, 40vw, 34rem);
  "
>
```

## Accessibility

Use meaningful alternative text when the image is part of the story:

```html
<img src="image.jpg" alt="A precise description of the image">
```

If the image is decorative, use an empty alt attribute:

```html
<img src="texture.jpg" alt="">
```

The caption is regular page HTML. Use semantic headings, paragraphs, links, and lists.

## Reduced motion

Vanilla Scroll Sky respects the user's reduced-motion preference.

When `prefers-reduced-motion: reduce` is active:

- image transform animation is disabled
- caption transform animation is disabled
- the sticky layout still works
- the content remains readable

## Browser behavior

The sticky layout uses `position: sticky`.

The reveal and caption motion use CSS scroll-driven animations:

```css
animation-timeline: view();
```

If scroll-driven animations are not supported, Vanilla Scroll Sky falls back to a non-animated state.

## Scope and style isolation

Vanilla Scroll Sky uses:

```css
@layer vanilla-scroll-sky {
  @scope (.vss) {
    ...
  }
}
```

This keeps the utility organized and prevents its selectors from leaking into unrelated markup.

This is not the same as Shadow DOM. Caption content remains normal page HTML and may inherit typography or content styles from your site.

## Recommended file structure

```txt
vanilla-scroll-sky/
├─ README.md
├─ LICENSE
├─ package.json
├─ src/
│  └─ vanilla-scroll-sky.css
└─ demo/
   └─ index.htm
```

## License

MIT
