---
name: webanim-vanta
description: >-
  Add a Vanta.js animated 3D background (waves, birds, fog, cells,
  globe) to the user's website project. Vanta
  (github.com/tengbao/vanta, MIT) runs on three.js and covers a hero
  section or full page. Note: Vanta is unmaintained since March 2024 -
  it works, but no fixes are coming. Use when the user says "animated
  background", "3D background", "Vanta", "shader background", "hero
  background effect".
---

# webanim-vanta

Adds a Vanta.js 3D background to the user's site. Source:
github.com/tengbao/vanta (MIT, verified live 20 Oct 2026).

## Warn first

- Unmaintained since March 2024: fine to use, nothing will be fixed.
- It adds real page weight (three.js + effect). On mobile this can
  hurt load time and battery. Offer to disable it on small screens.

## Add to a plain HTML site

1. Scripts before closing </body> - three.js r134 first (the version
   Vanta is built against), then the effect:

```html
<script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r134/three.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/vanta@0.5.24/dist/vanta.waves.min.js"></script>
```

2. Attach to the hero element:

```html
<script>
  VANTA.WAVES({ el: "#hero", mouseControls: true, touchControls: true,
    color: 0x111827, waveHeight: 18, waveSpeed: 0.8 });
</script>
```

Other effects swap the script and call: vanta.birds.min.js /
VANTA.BIRDS, vanta.fog.min.js / VANTA.FOG, vanta.cells.min.js /
VANTA.CELLS, vanta.globe.min.js / VANTA.GLOBE. Match the site's colour
scheme via the color option.

3. Keep text readable: the background sits behind content (position
   the canvas via the el's own stacking, z-index content above it).
4. Mobile option: skip init below 768px width, or pause with
   `vantaEffect.pause()` when the tab is hidden.

## Verify

Reload, confirm the effect renders, text stays readable, no console
errors about THREE, and the page still scrolls and navigates normally.
Check on a narrow viewport too.
