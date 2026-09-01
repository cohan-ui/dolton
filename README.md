# Doltone House Harbourside — build

Static build of the Figma concept (1440 master, responsive to 390). No framework, no build step.

```
index.html      markup
styles.css      all styles — tokens at top match the Figma values exactly
main.js         spaces engine, event-type re-theming, GSAP motion, gallery, FAQ, form
vendor/         GSAP 3.13 + ScrollTrigger + SplitText (vendored, no CDN dependency)
assets/img/     all imagery extracted from the .fig, optimised (86MB → 3.5MB)
```

## Explore the Spaces — as implemented
- Whole card is the hit target; click swaps the detail panel with a 250ms crossfade (skipped under `prefers-reduced-motion`). Selected card gets the gold treatment + `aria-pressed`, panel is `aria-live="polite"`, cards carry `aria-controls`.
- Horizon is the default loaded state; ✕ resets to it.
- Deep links work: `#space-lume` opens with Lume loaded (fresh load and `hashchange`). Swaps use `history.replaceState` so the page never re-scrolls.
- "Enquire about {space}" carries the selection into the form's Space of Interest ("— carried from your selection" appears only after a real selection).
- Event-type toggle (nav + form, kept in sync) re-themes the lens section and each space's use-case line — it never resets the space selection.
- Mobile (≤768): panel hidden, cards become inline expand/collapse accordions, one open at a time, Close ✕, 44px targets, gentle scroll adjustment only when the expanded state opens off-screen.
- **One deliberate deviation from the interaction spec:** the Figma layout stacks panel-above-grid, so the sticky two-column arrangement isn't applied in this pass. Instead, a card click nudges the panel into view only if it's fully off-screen (standard `scrollIntoView`, interruptible, no scroll-jacking). If you want the pinned-panel two-column variant, the grid collapses to one column beside a `position: sticky` panel — say the word.

## Motion (Kononenko-style, all native scroll — no hijacking)
- Hero: image settle 1.12→1, gold rule draw, SplitText char rise on the H1, staggered lede/CTAs. Slow Ken Burns stands in for the background video; PAUSE VIDEO stops it.
- Headlines: SplitText line-mask rises; eyebrows/paragraphs fade-up; stats/lists/cards stagger in groups.
- Images: clip-path rise + inner scale settle on reveal, scrubbed parallax on the large media, staggered stacking in the architecture column.
- Native `loading="lazy"` + fade-in on load; everything degrades to visible-immediately without GSAP or with reduced motion.

## Open items
- Floorplan downloads, venue tour, form steps 2–3, and the MENU overlay are stubs.
- Capacity figures beyond Horizon show TBC per the design; Cove's use-case line was blank in the file — placeholder copy added.
- Fonts load from Google Fonts (Playfair Display, IBM Plex Sans Condensed, Archivo Narrow).
