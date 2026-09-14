# Frontend Mentor - Workit Landing Page Solution

This is a solution to the [Workit landing page challenge on Frontend Mentor](https://www.frontendmentor.io/challenges/workit-landing-page-2fYnyle5lu). Frontend Mentor challenges help you improve your coding skills by building realistic projects.

## Table of contents

- [Overview](#overview)
  - [The challenge](#the-challenge)
  - [Screenshot](#screenshot)
  - [Links](#links)
- [My process](#my-process)
  - [Built with](#built-with)
  - [What I learned](#what-i-learned)
  - [Continued development](#continued-development)
  - [Review fixes](#review-fixes)
  - [Useful resources](#useful-resources)
  - [AI Collaboration](#ai-collaboration)
- [Author](#author)

## Overview

### The challenge

Users should be able to:

- View the optimal layout for the landing page depending on their device's screen size
- See hover and focus states for all interactive elements on the page

### Screenshot

![Design preview for the Workit landing page](./preview.jpg)

### Links

- Solution URL: [Repository](https://github.com/jonghwascript/workit-landing.git)
- Live Site URL: [Live site](https://jonghwascript.github.io/workit-landing)

## My process

### Built with

- Semantic HTML5 markup
- SCSS modules with `@use`
- CSS custom properties and Sass variables
- Flexbox
- CSS Grid
- Mobile-first responsive workflow
- Local font files
- Gulp, Sass, and Prettier

### What I learned

This project helped me practice responsive layout details that are easy to overlook in a landing page: decorative curves, layered background images, fluid hero artwork, and accessible section structure.

I used `clip-path` to create the features section's curved edge without adding extra image assets:

```scss
.features-curve {
  clip-path: ellipse(70% 30% at 45% 51%);
}
```

In the original header layout, I learned that `background-clip: content-box` can exclude padding from the painted background area. The refactored hero now uses a separate decorative pseudo-element instead:

```scss
header {
  padding-bottom: 30px;
  background-clip: content-box;
}
```

For cases where only the bottom padding should be excluded from a section background, a pseudo-element is more flexible than changing the HTML structure:

```scss
.section {
  position: relative;
  padding: 40px 20px 80px;
  z-index: 1;
}

.section::before {
  content: '';
  position: absolute;
  inset: 0 0 100px;
  background-color: $solate-color-100;
  z-index: -1;
}
```

The hero image now stays in normal flow inside `.hero-art`. Its wrapper grows with the image, while an absolutely positioned pseudo-element paints the purple curve behind it. A fluid maximum width and `aspect-ratio` let the image scale without requiring image-height offsets in the next section:

```scss
.hero-center {
  width: calc(100% - 2.5rem);
  max-width: clamp(320px, 50vw, 767px);
  margin-inline: auto;
  height: auto;
  aspect-ratio: 320 / 184;
}
```

Another useful detail was using `em` to make an underline scale from the current text size:

```scss
.underline::after {
  width: 3.14em;
}
```

I also practiced placing multiple decorative background images on one element with comma-separated background layers:

```scss
header {
  background-image:
    url('../images/bg-pattern-1.svg'),
    url('../images/bg-pattern-2.svg');
  background-repeat: no-repeat, no-repeat;
}
```

For desktop decorative patterns, I learned that `clamp()` is a good way to combine fluid viewport-based movement with practical limits. A plain `vw` value can push a background image too far off screen on wider layouts, while a fixed pixel value can feel too static. `clamp()` keeps the position responsive without letting it drift past the intended range.

```scss
header {
  background-position:
    left clamp(-140px, -10vw, -80px) top 28%,
    right clamp(-72px, -5vw, -32px) top 40%;
}
```

Finally, I learned that percentages inside `transform: translate()` are based on the transformed element itself, not the viewport. When the movement should follow the viewport size, `vw`, `vh`, or `calc()` can create smoother responsive positioning.

```scss
.decorative-pattern {
  transform: translate(calc(-50% - 7vw), calc(-50% - 17vh));
}
```

### Continued development

I want to keep improving how I handle decorative assets across tablet and desktop breakpoints. In particular, I want to get more comfortable choosing between fixed pixel offsets, viewport units, percentages, and `calc()` so decorative images stay intentional instead of drifting too far as the screen grows.

I also want to continue refining accessibility details, including meaningful labels for interactive links, focus states, and hidden headings for sections that need semantic names.

- [x] Keep the hero image in normal flow, allow it to grow beyond 320px, remove fixed header heights and `main`'s negative margin, and replace image-dependent features padding with responsive section spacing. Separate the purple curve from content flow and remove the hero's clipping. Reviewed the bundled design preview and checked the hero at 375px, 768px, and 1440px in headless Edge.
- [ ] Compare exact image dimensions and spacing against full-resolution design references; the bundled preview is a composite rather than a breakpoint-specific specification.

### Review fixes

- Fixed button keyboard focus outlines by replacing the undefined CSS custom property `var(--Grey-500)` with the Sass variable `$green-color` (`#44ffa1`), retaining a 2px outline and 2px offset.
- Added `alt="Workit"` to the header logo and the page description: "Workit turns your product data into actionable insights."
- Prevented `.hero-btn` and `.btn-primary` from growing on hover by reserving a transparent 1px border in their base styles and changing only its color on hover.
- Included the existing Sass gray palette additions (`$grey-100` through `$grey-500`). These Sass variables do not define CSS custom properties.
- Regenerated the CSS and source map. Sass compilation and `git diff --check` passed; browser and screen reader verification remain outstanding.

### Useful resources

- [MDN - clip-path](https://developer.mozilla.org/en-US/docs/Web/CSS/clip-path) - Useful for understanding how CSS shapes can create curved section edges.
- [MDN - background-clip](https://developer.mozilla.org/en-US/docs/Web/CSS/background-clip) - Helped clarify how backgrounds are painted relative to borders, padding, and content.
- [MDN - aspect-ratio](https://developer.mozilla.org/en-US/docs/Web/CSS/aspect-ratio) - Useful for keeping responsive images stable while preserving their intended proportions.
- [MDN - transform](https://developer.mozilla.org/en-US/docs/Web/CSS/transform) - Helped clarify how percentage values behave inside transforms.

### AI Collaboration

I used ChatGPT as a learning partner while building and reviewing this project. The most helpful parts were discussing responsive CSS behavior, clarifying how layout units behave, improving semantic HTML structure, and reviewing small project metadata issues.

## Author

- Frontend Mentor - [@jonghwascript](https://www.frontendmentor.io/profile/jonghwascript)
