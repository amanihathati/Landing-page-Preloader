# Landing Page Preloader Animation

This project is a cinematic preloader animation for a landing page. It is designed to feel premium, modern, and dramatic. Instead of a boring loading spinner, the page uses a full-screen image sequence that slides in, reveals itself, and then disappears to show the real website.

This script is great for portfolio sites, agencies, creative studios, and brand websites because it creates a strong first impression before the user even reaches the main content.

This README explains not just what the animation does, but how to build it and how to adapt it to your own site.

---

## What this animation is doing

When the page loads, the viewer does not immediately see the actual website. Instead, they experience a short intro sequence:

1. A black full-screen overlay appears.
2. A row of images rises upward from the lower part of the screen.
3. The images are revealed one after another.
4. The black loader is clipped away, almost like a curtain opening.
5. The page content slides in and fades into view.

The effect is meant to feel like the website is being created in front of the user's eyes. It adds narrative, movement, and emotion to an otherwise static landing page.

This is a common technique used in premium creative websites: the user sees the brand story before the content is fully revealed.

---

## Why this effect feels memorable

The reason this animation works is because it uses motion as a storytelling tool.

Instead of simply loading content, it tells the viewer:

- something important is about to appear
- the brand is cinematic and premium
- the page is designed with care
- the site has a visual identity beyond normal layouts

That is why the animation feels strong even though it is only a loader.

---

## Project structure

- `index.html` — the page skeleton and loader markup
- `styles.css` — visual styling and the initial hidden states
- `script.js` — GSAP timeline controlling the animation
- `assets/` — the images used in the loader and the site

---

## 1) Set up the HTML structure

The structure is very simple. The page includes a full-screen loader and then the visible website content underneath it.

```html
<div class="loader">
  <div class="loader-imgs">
    <div class="img">
      <img src="./assets/img1.jpg" alt="" />
    </div>
    <div class="img">
      <img src="./assets/img2.jpg" alt="" />
    </div>
    <div class="img">
      <img src="./assets/img3.jpg" alt="" />
    </div>
    <div class="img" id="loader-logo">
      <img src="./assets/logo.png" alt="" />
    </div>
    <div class="img">
      <img src="./assets/img4.jpg" alt="" />
    </div>
  </div>
</div>
```

The important part is that all these images are grouped inside a loader wrapper. That wrapper is what gets animated and then removed.

If you want to add this animation to your existing site, you can create a `div` like this at the top of your page and place it before the main content.

---

## 2) Start everything off-screen

In GSAP, the first step is to position all elements where they should start before the animation begins.

```javascript
document.addEventListener("DOMContentLoaded", function () {
  gsap.set(".img", { y: 500 });
  gsap.set(".loader-imgs", { x: 500 });
  gsap.set(".nav-item", { y: 25, opacity: 0 });
  gsap.set("h1, .item, footer", { y: 200 });
});
```

Here is what this does:

- `.img` starts 500px below its original position
- `.loader-imgs` starts shifted to the right
- nav items start lower and invisible
- hero text and footer items begin hidden below the screen

This creates the feeling that everything is coming from off-screen and moving into view.

This is the setup phase. Without this, the animation would feel abrupt or random.

---

## 3) Create the animation timeline

The animation is controlled with a GSAP timeline:

```javascript
const tl = gsap.timeline({ delay: 1 });
```

The `delay: 1` creates a short pause before the loader begins. That helps the user notice the intro and makes the animation feel more intentional. You can increase or decrease it depending on your taste.

A timeline is useful because it lets you control each part of the motion in sequence. This makes the intro feel choreographed rather than random.

---

## 4) Slide the images upward

```javascript
tl.to(".img", {
  y: 0,
  duration: 1.5,
  stagger: 0.05,
  ease: "power3.inOut",
});
```

This is the first and most noticeable motion.

### What each property does:

- `y: 0` means the images move back to their natural position
- `duration: 1.5` makes the movement smooth and not too fast
- `stagger: 0.05` means each image begins a little later than the previous one
- `ease: "power3.inOut"` makes the motion elegant and fluid

This creates a layered reveal, where the images appear like a wave instead of all at once.

If you want a more dramatic version, increase the duration or use a stronger easing like `expo.inOut`.

---

## 5) Move the loader strip into place

```javascript
.to(
  ".loader-imgs",
  {
    x: 0,
    duration: 3,
    ease: "power3.inOut",
  },
  "-=2.5"
)
```

The entire image group is moved horizontally to its final position using `x: 0`.

The `"-=2.5"` offset means that this animation starts before the previous animation fully ends. This overlap feels more natural and cinematic.

Why this matters:

- without overlap, the animation may feel too mechanical
- with overlap, the sequence feels like a choreographed reveal
- the whole intro has more depth and rhythm

This is a great trick to learn when making premium motion sequences.

---

## 6) Hide the images with clipping

```javascript
.to(
  ".img:not(#loader-logo)",
  {
    clipPath: "polygon(0% 0%, 100% 0%, 100% 0%, 0% 0%)",
    duration: 1,
    stagger: 0.1,
    ease: "power3.inOut",
  },
  "-=1"
)
```

This part is crucial. The images are not simply disappearing; they are being clipped away.

The `clipPath` shrinks the visible area of each image down to zero, creating a smooth collapsing effect.

This makes the loader feel like it is closing itself and revealing the real content behind it. It is a strong visual cue that the intro is ending.

This effect is often used in editorial and luxury websites because it feels refined and polished.

---

## 7) Collapse the black loader overlay

```javascript
.to(
  ".loader",
  {
    clipPath: "polygon(0% 0%, 100% 0%, 100% 0%, 0% 0%)",
    duration: 1,
    ease: "power3.inOut",
  },
  "-=0.5"
)
```

This is the moment the black preloader disappears.

The `.loader` is a full-screen black box fixed to the viewport, and its `clip-path` is animated until it disappears completely.

This is the exact moment when the page transitions from intro mode to real website mode.

If you want this effect for your own site, this is the central idea to copy: animate the overlay mask away so the content underneath is revealed.

---

## 8) Reveal the actual website content

```javascript
.to(
  ".nav-item, h1, footer, .item",
  {
    y: 0,
    opacity: 1,
    stagger: 0.1,
    duration: 1,
    ease: "power3.inOut",
  },
  "-=0.5"
);
```

This final step introduces the actual landing page.

The navigation, headline, and footer images move from hidden positions to their final state. They fade in and slide upward as the site becomes visible.

This is a perfect finishing move because the user is not suddenly thrown into the page. Instead, the content gracefully settles into place like a reveal finishing its final shot.

---

## Why the CSS matters

The loader styling is what gives this effect its final look.

```css
.loader {
  position: fixed;
  width: 100vw;
  height: 100vh;
  background: #000;
  clip-path: polygon(0% 0%, 100% 0%, 100% 100%, 0% 100%);
  pointer-events: none;
}
```

The full-screen black overlay creates a strong visual contrast against the light site background.

The `clip-path` is the secret because without it, there is no dramatic wipe or collapse. The clip path gives you control over how the overlay reveals and removes itself.

This creates the illusion of motion and hiding. It is not just a rectangular block; it is a moving mask.

---

## Styling the image row

```css
.loader-imgs {
  width: 150%;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  display: flex;
  gap: 50px;
  clip-path: polygon(0% 0%, 100% 0%, 100% 100%, 0% 100%);
}
```

This makes the image row wide and cinematic. A wide row of images feels more like a collage or a motion poster rather than a basic spinner.

The `display: flex` and `gap` create a neat horizontal arrangement, while the `position: absolute` makes the loader feel like a full-screen composition rather than a random animation.

---

## How to add this to your existing website

If you want to add this effect to another website, do this:

### Step 1: Add the loader markup
Place the loader before your main page content.

```html
<div class="loader">
  <div class="loader-imgs">
    <div class="img"><img src="your-image-1.jpg" alt="" /></div>
    <div class="img"><img src="your-image-2.jpg" alt="" /></div>
    <div class="img"><img src="your-image-3.jpg" alt="" /></div>
    <div class="img" id="loader-logo">
      <img src="your-logo.png" alt="" />
    </div>
  </div>
</div>
```

### Step 2: Add the loader CSS
Copy the `.loader` and `.loader-imgs` styles.

### Step 3: Hide your page content initially
Before the intro begins, hide the sections you want to reveal later.

```css
.hero, nav, footer {
  opacity: 0;
  transform: translateY(50px);
}
```

### Step 4: Add your GSAP timeline
Use the same idea:

```javascript
document.addEventListener("DOMContentLoaded", function () {
  gsap.set(".img", { y: 500 });
  gsap.set(".loader-imgs", { x: 500 });
  gsap.set(".hero, nav, footer", { y: 200, opacity: 0 });

  const tl = gsap.timeline({ delay: 1 });

  tl.to(".img", {
    y: 0,
    duration: 1.5,
    stagger: 0.05,
    ease: "power3.inOut",
  })
    .to(".loader-imgs", {
      x: 0,
      duration: 3,
      ease: "power3.inOut",
    }, "-=2.5")
    .to(".loader", {
      clipPath: "polygon(0% 0%, 100% 0%, 100% 0%, 0% 0%)",
      duration: 1,
      ease: "power3.inOut",
    }, "-=0.5")
    .to(".hero, nav, footer", {
      y: 0,
      opacity: 1,
      duration: 1,
      stagger: 0.1,
      ease: "power3.inOut",
    }, "-=0.5");
});
```

### Step 5: Replace the example content with your own
The structure is independent of the brand. You can use your own logo, hero text, and images. The animation logic stays the same.

---

## How to customize the animation

Here are the main things you can change:

- use fewer or more images
- increase the `stagger` for a slower reveal
- change the `duration` to make it more dramatic or softer
- replace the black loader with a custom brand color
- use your own logo in the center
- switch to `expo.inOut` for a stronger cinematic feel
- add text reveals after the loader fades out

For a luxury brand, slow it down and keep the spacing generous. For a modern startup, use faster motion and tighter timing.

---

## Common beginner mistakes

If your animation feels wrong, check these first:

### 1. You forgot to include GSAP
This project uses the CDN:

```html
<script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.5/gsap.min.js"></script>
```

### 2. The page content is not hidden before the animation
If your hero text is visible from the start, the intro loses its impact.

### 3. The `clipPath` is not animated properly
If the loader does not disappear smoothly, your clip path values need to be adjusted.

### 4. Timing values are too close together
If all animations happen at once, the reveal feels flat. Use stagger and timeline offsets to create rhythm.

### 5. The content is being animated but not first hidden
Without initial off-screen positions, the motion will look jumpy.

---

## Best use cases

This animation works best for:

- agency websites
- creative portfolios
- fashion brands
- startup landing pages
- photography or editorial layouts
- product launches

It is not ideal for content-heavy business sites that want a minimal or static first impression, but it is excellent when you want your website to feel premium and memorable.

---

## Final lesson

The real idea behind this effect is not the loader itself. The real idea is the reveal.

A good preloader is not just a loading screen. It is a transition between the user’s expectation and the brand’s identity. It tells the viewer that the website is an experience, not just content.

When you build a similar intro, think in terms of:

- layered motion
- intentional timing
- reveal rather than instant display
- strong visual contrast
- smooth transitions

That is what makes premium landing page motion feel professional.

---

## Summary

This animation is built from four main ingredients:

1. a full-screen black loader
2. a long horizontal image collage
3. staggered GSAP movement
4. clip-path reveal and collapse

Together, they create a cinematic intro that feels premium and modern.

If you want to use this effect in your own project, copy the structure, timing, and mask reveal logic and replace the images and text with your own brand content.

---

If you want, I can also rewrite this README into a version that is:

- more beginner-friendly
- more advanced for developers
- more like a tutorial article with copy-paste code blocks
- more focused on adding this effect to an existing website instead of a full page build

## Tips for improving it

- Add a custom brand logo in the center of the loader.
- Use different image sizes for a more editorial collage.
- Increase the duration for a slower luxury feel.
- Swap `power3.inOut` for `expo.inOut` for a more dramatic look.
- Add a subtle background noise or grain effect for a more premium result.
- Add text reveal after the loader disappears to make the brand message stronger.

---

## Final thought

This is more than a loading screen — it is a mini brand film. The real magic is in the timing, layered motion, and smooth reveal sequence. If you learn how to control timing and masks in GSAP, you can build intro animations that feel polished and memorable.

The best way to master this effect is to study the relationship between:

- timing
- easing
- stagger
- clipPath
- layering

Once you understand those, you can build your own cinematic landing page introductions.

---

## Code references

Main animation file:
- `script.js`

Main site structure:
- `index.html`

Styling for the intro and layout:
- `styles.css`
