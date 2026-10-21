---
name: webanim-gsap
description: >-
  Add GSAP animations to the user's website project. GSAP
  (github.com/greensock/GSAP, now 100 percent free including all old
  Club plugins after the Webflow acquisition, commercial use allowed)
  animates anything: fade-ins, scroll-triggered reveals, timelines.
  Use when the user says "animate this", "add GSAP", "scroll
  animation", "make elements appear on scroll", "text reveal".
---

# webanim-gsap

Adds GSAP animations to the user's site. Source:
github.com/greensock/GSAP (verified live 20 Oct 2026: v3.15.0, every
plugin free incl. ScrollTrigger - webflow.com/blog/gsap-becomes-free).

## Add to a plain HTML site

1. CDN scripts before closing </body>:

```html
<script src="https://cdn.jsdelivr.net/npm/gsap@3.15.0/dist/gsap.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/gsap@3.15.0/dist/ScrollTrigger.min.js"></script>
<script>gsap.registerPlugin(ScrollTrigger);</script>
```

2. Simple reveal on load:

```html
<script>
  gsap.from(".hero h1", { y: 40, opacity: 0, duration: 1, ease: "power3.out" });
</script>
```

3. Scroll-triggered reveal:

```html
<script>
  gsap.utils.toArray(".reveal").forEach(el => {
    gsap.from(el, { y: 30, opacity: 0, duration: 0.8,
      scrollTrigger: { trigger: el, start: "top 85%" } });
  });
</script>
```

## Rules

- Animate transform and opacity only (cheap, smooth); not width/height.
- Keep animations under ~1s; subtle beats flashy for a portfolio.
- Respect prefers-reduced-motion: wrap animations in a matchMedia check.
- If Lenis is also present, tell ScrollTrigger to update on Lenis
  scroll: `lenis.on('scroll', ScrollTrigger.update)`.

## Verify

Reload, scroll the page, confirm each animation fires once at the right
moment and nothing flashes unstyled before the script loads.
