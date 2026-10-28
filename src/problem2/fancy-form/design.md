# CarWhisperer — Cinematic Glass Design System

> Style-only reference extracted from the supplied screenshot. No layout rules. Colors and material parameters are approximations, intended for visual tuning against the reference.

## 1. Aesthetic direction

**Cinematic automotive glassmorphism:** dark, smoky, blue-gray translucent surfaces that merge into a cool atmospheric environment. The material is closer to tinted architectural glass than bright white frosted glass. Emphasize softness, premium restraint, subtle edge lighting, and high legibility.

**Keywords:** smoked glass, slate-blue tint, soft frost, diffused light, brushed silver, quiet luxury, atmospheric depth, restrained glow.

**Avoid:** milky-white glass, heavy neon, saturated gradients, thick borders, sharp black shadows, excessively blurred text, glossy plastic, or large colored glows.

## 2. Color tokens

| Token | Approximate value | Use |
|---|---|---|
| `--atmosphere-deep` | `#172D38` | Deep background shadows |
| `--atmosphere-mid` | `#284450` | Ambient blue base |
| `--atmosphere-light` | `#607A87` | Diffuse illuminated zones |
| `--glass-tint` | `#263E4B` | Glass pigmentation |
| `--glass-strong` | `rgba(20, 38, 49, .48)` | Darker floating glass |
| `--glass-default` | `rgba(34, 57, 70, .38)` | Standard glass |
| `--glass-light` | `rgba(106, 135, 149, .20)` | Illuminated glass |
| `--glass-stroke` | `rgba(235, 246, 252, .10)` | Hairline border |
| `--glass-edge-light` | `rgba(255, 255, 255, .19)` | Top-edge highlight |
| `--text-primary` | `#F1F5F7` | Main labels and values |
| `--text-secondary` | `#B8C8D0` | Supporting labels |
| `--text-muted` | `#8FA4AE` | Low-priority labels |
| `--silver` | `#DCE7EC` | Highlights, icon accents |

The glass color is not a flat fill: it is the combination of translucent tint, blurred backdrop, top-to-bottom tonal variation, and soft edge highlights.

## 3. Glass material recipe

1. **Tint:** dark desaturated blue-gray at approximately 25–50% opacity.
2. **Backdrop blur:** approximately 14–26px on primary surfaces; 8–14px for small controls. This is a suggested implementation range, not a measurable screenshot value.
3. **Saturation:** slight backdrop saturation boost (`115–130%`) to preserve the cinematic blue atmosphere.
4. **Gradient:** subtly brighter and more translucent near the top, darker near the bottom.
5. **Outline:** 1px white stroke at only 6–12% opacity; selectively brighten top edge.
6. **Inner light:** very faint inset white highlight along the upper edge.
7. **Depth shadow:** broad, low-opacity navy/black shadow, never a hard black drop shadow.
8. **Contrast:** white text remains opaque and crisp; only the surface behind it is blurred.

### CSS implementation

```css
:root {
  --atmosphere-deep: #172d38;
  --atmosphere-mid: #284450;
  --atmosphere-light: #607a87;
  --glass-tint: #263e4b;
  --text-primary: #f1f5f7;
  --text-secondary: #b8c8d0;
  --text-muted: #8fa4ae;
  --glass-border: rgba(235, 246, 252, 0.10);
  --glass-highlight: rgba(255, 255, 255, 0.19);
}

.glass {
  background: linear-gradient(
    165deg,
    rgba(105, 133, 148, 0.20) 0%,
    rgba(39, 64, 78, 0.38) 48%,
    rgba(18, 36, 47, 0.49) 100%
  );
  border: 1px solid var(--glass-border);
  -webkit-backdrop-filter: blur(20px) saturate(120%);
  backdrop-filter: blur(20px) saturate(120%);
  box-shadow:
    inset 0 1px 0 rgba(255, 255, 255, 0.11),
    0 12px 32px rgba(9, 22, 30, 0.15);
}

.glass--dark {
  background: linear-gradient(160deg,
    rgba(34, 56, 69, 0.58),
    rgba(15, 31, 41, 0.66));
  -webkit-backdrop-filter: blur(14px) saturate(115%);
  backdrop-filter: blur(14px) saturate(115%);
}

.glass--light {
  background: linear-gradient(160deg,
    rgba(166, 191, 201, 0.24),
    rgba(66, 97, 112, 0.27));
  border-color: rgba(255, 255, 255, 0.13);
}

.glass--control {
  background: rgba(18, 37, 48, 0.43);
  border: 1px solid rgba(255, 255, 255, 0.07);
  -webkit-backdrop-filter: blur(12px);
  backdrop-filter: blur(12px);
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.07);
}
```

## 4. Lighting and atmosphere

- Use a cool blue-gray environment with broad, diffused lighting, not a plain solid-color background.
- Soft diagonal light shafts and subtle bright patches create the photographic, showroom-like quality.
- Light should appear to **pass behind** the glass, revealing translucency without washing out content.
- A gentle vignette darkens the edges; brighter atmospheric areas remain near the visual subject.
- Optional noise/grain should be extremely subtle, just enough to prevent gradients from feeling synthetic.
- Avoid hard glow around the glass perimeter. Most brightness comes from the scene behind the panel and the thin upper-edge reflection.

Suggested ambient gradient:

```css
.atmosphere {
  background:
    radial-gradient(ellipse at 77% 18%, rgba(158, 190, 201, .22), transparent 42%),
    radial-gradient(ellipse at 36% 62%, rgba(109, 148, 164, .22), transparent 48%),
    linear-gradient(145deg, #172d38 0%, #365462 57%, #243d49 100%);
}
```

## 5. Borders, highlights and shadow

- **Border:** 1px, low-opacity cool white; avoid strong all-around outlines.
- **Top edge:** subtly brighter than other edges to simulate reflected overhead lighting.
- **Inner highlight:** `inset 0 1px 0 rgba(255,255,255,.08)` to `.14`.
- **Outer shadow:** broad 12–36px blur, low-opacity dark blue-black.
- **Layer separation:** primarily via tint, opacity, blur, and light direction rather than deep elevation.
- **Corners:** softly rounded, visually smooth. The radius is a material treatment rather than a layout requirement.

## 6. Typography

- Use a clean, modern geometric or neo-grotesque sans-serif: **Inter**, **Manrope**, or **SF Pro Display** as practical approximations.
- Large display text: light or regular weight (`300–400`), slightly tight tracking (`-0.02em` to `-0.04em`).
- Primary labels: regular/medium (`400–500`), crisp white.
- Supporting descriptions: regular (`400`), cool gray-blue.
- Tiny metadata: restrained contrast; do not rely on ultra-low opacity for important information.
- Numerals: lightweight, clean, generously spaced from their unit labels.
- Prefer sentence case and short labels over uppercase technical styling.

```css
.glass-title { color: #f1f5f7; font-weight: 300; letter-spacing: -.035em; }
.glass-label { color: #f1f5f7; font-weight: 400; letter-spacing: -.015em; }
.glass-caption { color: #b8c8d0; font-weight: 400; }
.glass-muted { color: #8fa4ae; }
```

## 7. Icons and fine details

- Thin, precise outline icons, approximately 1.4–1.7px stroke.
- Use pale white/silver at approximately 80–95% opacity for active icons, softer gray-blue for secondary icons.
- Icon containers can use darker glass than their parent surfaces for subtle separation.
- Decorative lines, progress arcs, and chart marks are thin and silver-white, not neon.
- Charts use translucent fills, restrained strokes, and soft highlights. Avoid thick grid lines or saturated chart palettes.
- Small selected indicators can use a short white underline, narrow highlight, or brighter glass surface.

## 8. Interaction and motion

| State | Treatment |
|---|---|
| Default | Dark blue translucent glass, muted thin border |
| Hover | Slightly brighter tint, marginally stronger edge reflection |
| Active/selected | Lighter glass, brighter white icon/text, subtle inset glow |
| Pressed | Slightly darker tint and reduced highlight |
| Disabled | Reduced text/icon contrast without losing legibility |
| Focus-visible | Distinct pale-blue/white outline for keyboard accessibility |

- Transitions: `180–280ms`, ease-out; avoid springy or playful motion.
- Opacity, border-color, and background-color changes should be small and refined.
- Optional hover lift should be minimal, around 1–2px.
- Respect `prefers-reduced-motion`.

```css
.glass-interactive {
  transition: background-color 220ms ease, border-color 220ms ease,
              box-shadow 220ms ease, transform 220ms ease;
}
.glass-interactive:hover {
  border-color: rgba(255,255,255,.17);
  box-shadow: inset 0 1px 0 rgba(255,255,255,.16),
              0 14px 32px rgba(9,22,30,.18);
}
.glass-interactive:focus-visible {
  outline: 2px solid rgba(221,239,248,.8);
  outline-offset: 3px;
}
@media (prefers-reduced-motion: reduce) {
  .glass-interactive { transition: none; }
}
```

## 9. Implementation considerations

- Glass requires detailed background content or tonal variation behind it to be perceptible. Against a flat solid background, blur alone may appear ineffective.
- Use `backdrop-filter` on the **surface**, not on the text or icons.
- Backdrop blur and transparency are expensive on some devices: limit overlapping glass layers and offer a solid-color fallback.
- Verify text contrast over both bright and dark portions of the environment.
- Use separate light/dark glass variants rather than one opacity everywhere.
- Tune opacity and blur **in context**, since screenshot appearance depends on the scene behind the surface.

## 10. Design prompt for implementation

> Build a premium cinematic automotive interface inspired by CarWhisperer's smoky blue glass aesthetic. Use dark slate-blue semi-transparent panels with 12–24px backdrop blur, soft blue-gray gradients, ultra-thin translucent white borders, delicate top-edge reflections, and broad subtle shadows. Typography should be lightweight, geometric, and crisp white with cool gray-blue supporting labels. Icons should be minimal, thin-stroke, and silver-white. The environment should feel like a softly lit automotive studio, with diffused cool light and atmospheric depth. Favor quiet, sophisticated glass materials over bright milky glass, neon gradients, or heavy shadows. Apply the styling independently of any specific page layout.
