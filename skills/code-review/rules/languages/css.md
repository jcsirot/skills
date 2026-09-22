# CSS Review Guide

Apply this guide to CSS, Sass/Less, CSS modules, utility classes, and styles
embedded in templates or components. Consider the browser support matrix and
the project's design-system conventions before recommending a change.

## Code quality, accessibility, and performance

- Check cascade layers, specificity, inheritance, source order, naming,
  scoping, and whether selectors make future overrides predictable.
- Check layout behavior across viewport sizes, writing directions, zoom,
  dynamic content, user font settings, and supported browsers.
- Check focus indicators, contrast, target size, state styles, forced colors,
  reduced motion, and alternatives to color-only communication.
- Check stacking contexts, overflow, positioning, z-index, containment,
  compositing, and interaction with portals or fixed/sticky elements.
- Check token reuse, theme/dark-mode behavior, duplication, dead rules,
  generated CSS size, selector cost, and render-triggering animations.
- Check that component styles do not leak globally or rely on fragile DOM
  structure, and that states are represented consistently with the UI logic.

## Security

- Treat interpolated or user-controlled CSS as a trust boundary. Check
  `url()`, custom properties, selectors, and style attributes for injection,
  exfiltration, unsafe resource loading, or unexpected browser requests.
- Check external fonts, images, imports, and other resources for trusted
  origins, CSP compatibility, privacy impact, and accidental credential
  leakage through URLs.
- Check CSS changes that weaken click targets, hide security warnings,
  obscure focus, or create deceptive overlays for unintended security impact.
- Do not classify ordinary CSS obfuscation or a missing convention as a
  vulnerability without an actual data, execution, or user-safety path.
