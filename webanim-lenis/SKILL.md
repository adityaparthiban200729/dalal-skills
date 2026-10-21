---
name: webanim-lenis
description: >-
  Add or fix Lenis smooth scrolling in the user's website project. Lenis
  (github.com/darkroomengineering/lenis, MIT, actively maintained) gives
  butter-smooth scroll on plain HTML or React sites via one CDN script.
  Use when the user says "smooth scroll", "buttery scroll", "add Lenis",
  "site feels jumpy when scrolling", or a reel mentions smooth
  scrolling.
---

# webanim-lenis

Adds Lenis smooth scrolling to the user's site. Source:
github.com/darkroomengineering/lenis (MIT, verified live 20 Oct 2026,
actively maintained).

## First check

Look for an existing Lenis setup (search the project for "lenis",
"Lenis(", "lenis@"). If it is already wired in (the user's 3d-hero
branch got smooth scrolling from Prompt 2), do NOT add a second
instance - two Lenis loops fight each other. Report that it exists.

## Add to a plain HTML site

1. Add the CDN script before the closing </body> (version pinned,
   verified 20 Oct 2026):

```html
<script src="https://unpkg.com/lenis@1.3.27/dist/lenis.min.js"></script>
```

2. Initialise it in a script after that:

```html
<script>
  const lenis = new Lenis({ lerp: 0.1 });
  function raf(time) { lenis.raf(time); requestAnimationFrame(raf); }
  requestAnimationFrame(raf);
</script>
```

3. Anchor links: use `lenis.scrollTo('#section')` on nav clicks, or add
   `anchors: true` to the options so normal # links scroll smoothly.
4. Back button and routing must keep working - test navigation after
   adding.
5. Respect reduced motion: skip init when
   `window.matchMedia('(prefers-reduced-motion: reduce)').matches`.

## Verify

Open the page, scroll, confirm motion is smooth and no console errors
mention lenis. Confirm the CDN script actually loads (network 200).
