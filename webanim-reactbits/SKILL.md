---
name: webanim-reactbits
description: >-
  Use React Bits components (github.com/DavidHDev/react-bits, MIT +
  Commons Clause: free for personal and commercial use, cannot be
  resold as-is) in a React project: animated text, cards, buttons,
  backgrounds. Use when the user says "React Bits", "fancy button",
  "animated card", "text animation component". NOT for plain HTML
  sites - say so and offer a plain-HTML alternative instead.
---

# webanim-reactbits

Adds React Bits components to a React project. Source:
github.com/DavidHDev/react-bits (verified live 20 Oct 2026, ~50K
stars).

## Hard requirement

React Bits needs a React project (Vite/Next.js). The user's current
site is plain HTML - if that is still the target, stop and say React
Bits does not apply; offer GSAP/Lenis/Vanta equivalents instead. Only
proceed inside an actual React project.

## How to add a component

1. Pick the component on reactbits.dev or the repo.
2. Install route (repo README): either copy the component source from
   the repo into src/components, or use the jsrepo CLI:
   `npx jsrepo add github/DavidHDev/react-bits/...` for the specific
   component. Copying the source is simplest and has no registry
   dependency.
3. Some components need framer-motion or gsap as a peer dependency;
   install what the component's file imports.
4. Import and drop it in, wire the props to the site's colours/fonts.

## Licence note

MIT + Commons Clause: fine for his personal site and client work; he
cannot sell the components themselves as a component library. One line
to him when that could matter.
