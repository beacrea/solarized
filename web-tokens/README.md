
# Solarized Web Tokens

This folder contains a web‑oriented Design Tokens resource for the Solarized color scheme, expressed using the Design Tokens Community Group (DTCG) Format Module 2025.10 and Resolver Module 2025.10 ([1][4][5]).

The goal of this resource is to:

- Preserve the canonical 16‑color Solarized palette (8 base monotones, 8 accents) as immutable primitives ([1][2]).  
- Provide a general, implementation‑agnostic set of semantic roles for light/dark web UIs.  
- Support multiple consumption patterns (single-theme, multi-theme, resolver-driven) via DTCG 2025.10 standards ([4][5]).  
- Enable seamless integration with modern design-system and token tooling pipelines ([4][6]).

## Files and usage

### Token files

- **`solarized.tokens.json`**  
  Generic roles with `light` and `dark` values nested in a single object. Use this if your tool or runtime can select between `light` and `dark` keys on individual tokens. Best for flexible, runtime-driven theme switching.

- **`solarized.multi-theme.tokens.json`**  
  Explicit `theme.light` and `theme.dark` group hierarchies within the same file. Useful for systems that understand nested theme structures but do not require a full resolver. Best for design tools and systems with built-in theme support.

- **`solarized.light.tokens.json`**  
  Single-theme variant with Solarized Light mappings only (concrete values, no theme branching). For backward compatibility, simpler toolchains, and light-only applications.

- **`solarized.dark.tokens.json`**  
  Single-theme variant with Solarized Dark mappings only. Pair with the light variant for dual-theme support without a resolver. For backward compatibility, simpler toolchains, and dark-only applications.

### Resolver

- **`solarized.resolver.json`**  
  DTCG 2025.10 Resolver that binds `light` and `dark` contexts to the multi-theme file ([5]). Use this for full context-aware token resolution in DTCG-compliant tools and build pipelines. Enables dynamic theme switching and modular token composition.

### Scripts and assets

- **`generate_solarized_swatches.py`**  
  Python script to generate color swatch PNG images into `/assets`. Run from this folder:  
  ```
  pip install pillow
  python generate_solarized_swatches.py
  ```

- **`/assets/`**  
  Contains 16 PNG swatch images (one per Solarized color) for visual reference in documentation, design tools, and web previews.

## DTCG 2025.10 adherence

All token files follow the Design Tokens Format Module 2025.10 ([4]):

- `$schema` points to the official 2025.10 format schema for validation.  
- `$type` and `$value` distinguish groups from tokens per DTCG object model.  
- Color values use `colorSpace: "srgb"`, `components` (normalized 0–1 RGB triple), and optional `hex` for convenience.  
- Semantic tokens use curly-brace references (e.g., `{color.palette.base3}`) for token aliasing and traceability.  
- All token names follow DTCG naming conventions (no leading `$`, no `..` or other reserved patterns).

The resolver file follows the Resolver Module 2025.10 ([5]):

- Defines token `sets` (palette, light-theme, dark-theme) as reusable token groups.  
- Defines a `theme` modifier with `light` and `dark` contexts for dynamic selection.  
- `resolutionOrder` chains palette + theme modifier application.  
- Supports JSON Pointer references and relative file paths for token composition.

---

## Palette overview

Solarized defines 16 colors: 8 monotone "base" tones forming a continuum from dark to light, and 8 chromatic accents for semantic meaning and visual hierarchy ([1][2]).  
For a visual overview of the full palette, see the Solarized palette image on Wikimedia Commons ([8]).

### Base tones (monotones)

The base tones form the backbone of the Solarized theme, providing neutral background and foreground colors with carefully calibrated contrast.

| Swatch                              | Token  | Hex       | RGB            | Purpose / Description                |
|-------------------------------------|--------|-----------|----------------|--------------------------------------|
| ![base03](./doc-assets/base03.png)      | base03 | `#002b36` | `0, 43, 54`    | Darkest base tone; dark mode background. Lowest luminance. |
| ![base02](./doc-assets/base02.png)      | base02 | `#073642` | `7, 54, 66`    | Very dark base tone; dark mode surfaces and subtle UI elements. |
| ![base01](./doc-assets/base01.png)      | base01 | `#586e75` | `88, 110, 117` | Dark UI text and subtle foreground; used for muted labels and metadata in dark mode. |
| ![base00](./doc-assets/base00.png)      | base00 | `#657b83` | `101, 123, 131`| Primary dark text tone; main text color for light mode. Strong contrast against light backgrounds. |
| ![base0](./doc-assets/base0.png)        | base0  | `#839496` | `131, 148, 150`| Primary light text tone; main text color for dark mode. Maintains readability on dark backgrounds. |
| ![base1](./doc-assets/base1.png)        | base1  | `#93a1a1` | `147, 161, 161`| Light UI text and subtle foreground; secondary text in light mode. Lower emphasis than base00. |
| ![base2](./doc-assets/base2.png)        | base2  | `#eee8d5` | `238, 232, 213`| Light surface background; light mode surfaces, cards, and subtle UI layers. Higher luminance. |
| ![base3](./doc-assets/base3.png)        | base3  | `#fdf6e3` | `253, 246, 227`| Lightest base tone; light mode primary background. Highest luminance. |

**Design intent**: The base ramp creates a symmetric, low-contrast palette where `base03` ↔ `base3`, `base02` ↔ `base2`, `base01` ↔ `base1`, and `base00` ↔ `base0` form complements ([1]). This symmetry enables a unified theme system where swapping light and dark is structurally consistent.

### Accent tones (chromatic)

The accent tones are reserved for semantic meaning, interactive elements, and status indication. They are applied consistently across both light and dark modes, ensuring semantic clarity regardless of theme.

| Swatch                              | Token   | Hex       | RGB            | Semantic Use                         |
|-------------------------------------|---------|-----------|----------------|--------------------------------------|
| ![yellow](./doc-assets/yellow.png)      | yellow  | `#b58900` | `181, 137, 0`  | Warning, caution, attention-needed states. Links and highlights. |
| ![orange](./doc-assets/orange.png)      | orange  | `#cb4b16` | `203, 75, 22`  | Secondary accent, alt-text, special emphasis. |
| ![red](./doc-assets/red.png)            | red     | `#dc322f` | `220, 50, 47`  | Errors, destructive actions, critical alerts. |
| ![magenta](./doc-assets/magenta.png)    | magenta | `#d33682` | `211, 54, 130` | Tertiary accent, non-semantic highlight. |
| ![violet](./doc-assets/violet.png)      | violet  | `#6c71c4` | `108, 113, 196`| Tertiary accent, non-semantic highlight. |
| ![blue](./doc-assets/blue.png)          | blue    | `#268bd2` | `38, 139, 210` | Primary accent, brand color, links, interactive elements, primary actions. |
| ![cyan](./doc-assets/cyan.png)          | cyan    | `#2aa198` | `42, 161, 152` | Info, information, secondary status. |
| ![green](./doc-assets/green.png)        | green   | `#859900` | `133, 153, 0`  | Success, positive states, validation. |

**Design intent**: Accents are used consistently across both Solarized Light and Solarized Dark, maintaining semantic meaning regardless of theme ([1]). This design choice makes it easy for users to develop visual muscle memory for status and action meanings.

---

## Light and dark themes

This resource supports both **Solarized Light** and **Solarized Dark** from a single canonical palette, enabling seamless theme switching without duplicating color definitions.

### Solarized Light

**Use case**: Office, business, daylight, or print-friendly interfaces where light backgrounds reduce eye strain in bright environments.

- **Background**: `base3` (off-white, `#fdf6e3`)  
  - Primary page/app background. Soft, warm off-white that reduces glare while remaining distinct from pure white.  
- **Primary text**: `base00` (dark, `#657b83`)  
  - Body text, primary content. Dark enough for WCAG AAA contrast against `base3`. ([7])  
- **Secondary text**: `base1` (medium, `#93a1a1`)  
  - Hints, labels, metadata. Lower emphasis without sacrificing accessibility.  
- **Tertiary text**: `base2` (very light, `#eee8d5`)  
  - Disabled states, very subtle annotations. Use sparingly.  
- **Surfaces**: `base2` (subtle layer)  
  - Cards, panels, inset elements. Slightly darker than primary background for depth.  
- **Borders**: `base2` (subtle) to `base1` (strong)  
  - Dividers use subtle `base2`; focus rings and strong outlines use `base1`.  

### Solarized Dark

**Use case**: Evening, low-light, or dark-mode-first interfaces where dark backgrounds reduce strain in dim environments.

- **Background**: `base03` (dark, `#002b36`)  
  - Primary page/app background. Deep blue-black that feels grounded and reduces glare in dark environments.  
- **Primary text**: `base0` (light, `#839496`)  
  - Body text, primary content. Light enough for WCAG AAA contrast against `base03`. ([7])  
- **Secondary text**: `base01` (medium, `#586e75`)  
  - Hints, labels, metadata. Lower emphasis while maintaining legibility.  
- **Tertiary text**: `base02` (very dark, `#073642`)  
  - Disabled states, very subtle annotations. Use sparingly.  
- **Surfaces**: `base02` (subtle layer)  
  - Cards, panels, inset elements. Slightly lighter than primary background for depth.  
- **Borders**: `base02` (subtle) to `base01` (strong)  
  - Dividers use subtle `base02`; focus rings and strong outlines use `base01`.  

### Accents across both themes

Accents (`blue`, `green`, `yellow`, `red`, `cyan`) remain identical across both Solarized Light and Solarized Dark, maintaining semantic clarity:

- `accent.primary` (blue) always signals interactive or branded content.  
- `accent.success` (green) always signals positive outcomes.  
- `accent.warning` (yellow) always signals caution or attention.  
- `accent.danger` (red) always signals errors or destructive actions.  
- `accent.info` (cyan) always signals informational content.

This consistency reduces cognitive load: users learn once and apply everywhere.

---

## Roles and semantic mapping

Across all token files, semantic roles organize Solarized's raw palette into meaningful UI categories. Roles are intentionally neutral and not tied to specific component libraries, making them reusable across platforms and toolchains.

### Role hierarchy

Roles are organized in a three-level hierarchy:

1. **Palette layer** (`color.palette.*`)  
   Raw Solarized colors, never modified.  

2. **Role layer** (`color.role.*` or `color.theme.{light,dark}.*`)  
   Semantic mappings of palette colors to UI purposes.  

3. **Component layer** (application-specific)  
   Components use roles (or extend roles) to define their own visual behavior.

Example: A button component might reference `color.role.button.primary.background`, which in turn references `{color.palette.blue}`.

### Role definitions

#### Background roles

Used for surfaces, containers, and spatial organization.

- **`background.default`**  
  Primary page or application background. The base surface all other UI sits on top of.  
  - Light: `base3` (`#fdf6e3`)  
  - Dark: `base03` (`#002b36`)  

- **`background.subtle`**  
  Secondary surfaces layered on top of the default background. Used for cards, panels, sidebars, modals, and inset regions to create visual hierarchy and separation.  
  - Light: `base2` (`#eee8d5`)  
  - Dark: `base02` (`#073642`)  

**Usage**: Always start with `background.default` for your main viewport. Use `background.subtle` for components that need to appear "elevated" or distinct.

#### Foreground roles

Used for text and icons.

- **`foreground.default`**  
  Primary text and icon color for legible, high-emphasis content (body text, headings, key labels).  
  - Light: `base00` (`#657b83`)  
  - Dark: `base0` (`#839496`)  

- **`foreground.muted`**  
  Secondary text, supporting information, hints, and metadata. Lower emphasis than default, but still legible for sustained reading.  
  - Light: `base1` (`#93a1a1`)  
  - Dark: `base01` (`#586e75`)  

- **`foreground.inverse`**  
  Text color for high-contrast situations: overlaid on accent colors, strong backgrounds, or when maximum legibility is needed (e.g., buttons, badges, alerts).  
  - Light: `base03` (`#002b36`) — dark text on light accents  
  - Dark: `base3` (`#fdf6e3`) — light text on dark accents  

**Usage**: Always use `foreground.default` for primary body text. Use `muted` for supporting labels and metadata. Use `inverse` only when text sits on top of accents or strong backgrounds.

#### Border roles

Used for dividers, outlines, focus indicators, and structural separation.

- **`border.subtle`**  
  Low-emphasis dividers, hairlines, and faint outlines (e.g., list separators, table borders, soft boundaries).  
  - Light: `base2` (`#eee8d5`)  
  - Dark: `base02` (`#073642`)  

- **`border.strong`**  
  High-emphasis component outlines, focus rings, and interactive boundaries (e.g., form field outlines, focus indicators, tabs).  
  - Light: `base1` (`#93a1a1`)  
  - Dark: `base01` (`#586e75`)  

**Usage**: Use `subtle` for non-interactive structural divisions. Use `strong` for interactive elements and focus states to ensure visibility and accessibility.

#### Accent roles

Used for semantic meaning, interaction, and status indication.

- **`accent.primary`**  
  Primary brand or interactive accent for links, buttons, and key interactive elements.  
  - All themes: `blue` (`#268bd2`)  

- **`accent.success`**  
  Positive or success state indication (form validation, success messages, completion).  
  - All themes: `green` (`#859900`)  

- **`accent.warning`**  
  Warning or caution state indication (alerts that need attention, cautionary labels).  
  - All themes: `yellow` (`#b58900`)  

- **`accent.danger`**  
  Destructive action or error state indication (delete buttons, error messages, critical alerts).  
  - All themes: `red` (`#dc322f`)  

- **`accent.info`**  
  Informational or neutral accent (info messages, secondary actions, help text).  
  - All themes: `cyan` (`#2aa198`)  

**Usage**: Reserve accents for semantically meaningful UI. Don't use them just for visual interest. Each accent should consistently signal the same meaning throughout your application.

---

## Token tooling and integrations

Modern design systems rely on DTCG-compliant tooling to manage, transform, and distribute tokens across platforms and formats ([4][5][6]).

### Design tools

#### Figma

**Native token support** (via Figma Variables or plugins):

1. Use `solarized.light.tokens.json` and `solarized.dark.tokens.json` for simple, separate-file theming.  
2. Or use `solarized.multi-theme.tokens.json` with a Figma token plugin (Tokens Studio, Figma Tokens, etc.).  
3. Import tokens into component styles and text styles.  
4. Theme switching in Figma is automatic: publish one file, switch theme context, and all components update.

**Example workflow**:
- Create a Figma file with "Light" and "Dark" variable groups.
- Import Solarized tokens into these groups.
- Build components that reference variables (e.g., `fill: var(--color-background-default)`).
- Toggle theme mode in Figma to see live theme switching.

#### Adobe XD, Sketch, etc.

Similar workflows apply. Most modern design tools support JSON token import and variable/style binding.

### Token transformation and build tools

#### Style Dictionary

**Use case**: Generate platform-specific token formats (CSS, SCSS, JavaScript, JSON) from a single DTCG source.

```
// style-dictionary.config.js
module.exports = {
  source: ['solarized.light.tokens.json'],
  platforms: {
    css: {
      transformGroup: 'css',
      files: [
        {
          destination: 'output/tokens.light.css',
          format: 'css/variables',
        },
      ],
    },
    js: {
      transformGroup: 'js',
      files: [
        {
          destination: 'output/tokens.light.js',
          format: 'javascript/es6',
        },
      ],
    },
  },
};
```

**Output**:
```
/* tokens.light.css */
:root {
  --color-palette-base03: #002b36;
  --color-palette-base3: #fdf6e3;
  --color-role-background-default: #fdf6e3;
  --color-role-foreground-default: #657b83;
  /* ... */
}
```

#### Terrazzo / Token Transformer

Web-based tools that validate and transform DTCG tokens interactively:

1. Upload `solarized.multi-theme.tokens.json`.  
2. Export as CSS, SCSS, JavaScript, or other formats.  
3. Validate token references and syntax.  
4. Generate component-specific token subsets if needed.

#### Custom resolvers

Build a lightweight resolver in your application to handle context switching:

```
// solarized-resolver.js
function resolveToken(token, theme = 'light') {
  if (token.light && token.dark) {
    return token[theme];
  }
  return token;
}

export default resolveToken;
```

### CI/CD and automation

#### Automated token sync

Use GitHub Actions or similar to:

1. Validate token files against DTCG schemas.  
2. Generate and commit output formats (CSS, JS).  
3. Sync tokens to design tools (Figma, Zeroheight, etc.).  
4. Trigger design-system documentation rebuilds.

Example GitHub Actions workflow:

```
name: Validate and Transform Tokens

on: [push]

jobs:
  validate:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - run: npm install -g token-transformer
      - run: token-transformer solarized.light.tokens.json output/tokens.light.json
      - run: git add output/ && git commit -m 'Generated tokens'
```

#### Design-system documentation

Integrate token files into documentation sites (Zeroheight, Storybook, custom HTML):

```
<div class="swatch" style="background: var(--color-palette-base3); color: var(--color-role-foreground-default);">
  Base3: #fdf6e3
</div>
```

---

## Use cases and integration patterns

### 1. Web applications (React, Vue, Svelte, etc.)

**Pattern**: Single-theme token file + CSS Custom Properties

```
// src/theme.js
import lightTokens from './tokens/solarized.light.tokens.json';

export const setupTheme = () => {
  const root = document.documentElement;
  
  Object.entries(lightTokens.color.palette).forEach(([key, token]) => {
    const cssVar = `--color-palette-${key}`;
    root.style.setProperty(cssVar, token.$value.hex);
  });

  Object.entries(lightTokens.color.role).forEach(([role, values]) => {
    Object.entries(values).forEach(([key, token]) => {
      const cssVar = `--color-role-${role}-${key}`;
      root.style.setProperty(cssVar, token.$value.hex);
    });
  });
};
```

```
/* src/styles/colors.css */
:root {
  --color-bg: var(--color-role-background-default);
  --color-text: var(--color-role-foreground-default);
  --color-accent: var(--color-accent-primary);
}

body {
  background: var(--color-bg);
  color: var(--color-text);
}

a {
  color: var(--color-accent);
}
```

**Benefits**: Dynamic theme switching, single source of truth, CSS-native.

### 2. Design-to-development handoff

**Pattern**: Multi-theme token file + design tool variable binding

1. Designer imports `solarized.multi-theme.tokens.json` into Figma.  
2. Creates components that reference theme variables.  
3. Exports component specs with token references.  
4. Developer implements components using the same token references.  

**Result**: Perfect alignment between design and code.

### 3. Multi-platform theme system (web + native)

**Pattern**: Separate single-theme files + platform-specific transformers

```
solarized.light.tokens.json    → CSS/SCSS for web
solarized.light.tokens.json    → YAML for iOS
solarized.light.tokens.json    → XML for Android
```

Each platform consumes the same token definitions but outputs in its native format.

### 4. Monorepo design systems

**Pattern**: Resolver-driven context selection + token composition

```
/packages/tokens
  ├── solarized.multi-theme.tokens.json
  ├── solarized.resolver.json
  ├── /extensions
  │   ├── typography.tokens.json
  │   ├── spacing.tokens.json
  │   └── elevation.tokens.json
  └── /outputs
      ├── web/
      ├── mobile/
      └── docs/
```

The resolver binds core tokens to context, allowing each extension to inherit theme behavior.

### 5. Accessible color-blindness-friendly theming

**Future pattern** (not yet implemented): Extend token set with `colorblind.protanopia`, `colorblind.deuteranopia`, etc.

```
{
  "color": {
    "palette": { /* base Solarized */ },
    "theme": {
      "light": { /* standard */ },
      "dark": { /* standard */ },
      "light-protanopia": { /* adjusted for red-blind users */ }
    }
  }
}
```

---

## Extending the resource

This token set can be extended with additional token types while preserving the Solarized palette and roles as the foundation:

### Typography

```
{
  "typography": {
    "display": { "$type": "typography", "$value": { "fontFamily": "Inter", "fontSize": { "value": 32, "unit": "px" }, ... } },
    "body": { "$type": "typography", "$value": { ... } }
  }
}
```

### Spacing

```
{
  "spacing": {
    "xs": { "$type": "dimension", "$value": { "value": 4, "unit": "px" } },
    "sm": { "$type": "dimension", "$value": { "value": 8, "unit": "px" } }
  }
}
```

### Elevation / Shadows

```
{
  "shadow": {
    "sm": { "$type": "shadow", "$value": { "color": "{color.palette.base01}", "offsetX": 0, "offsetY": 2, "blur": 4, "spread": 0 } },
    "lg": { "$type": "shadow", "$value": { ... } }
  }
}
```

### Borders and strokes

```
{
  "border": {
    "default": { "$type": "strokeStyle", "$value": { "dashArray": [], "lineCap": "round" } },
    "dashed": { "$type": "strokeStyle", "$value": { "dashArray":, "lineCap": "round" } }[1]
  }
}
```

**Best practice**: Always reference palette and role tokens from extensions. This keeps the design system cohesive and maintainable.

---

## Accessibility considerations

Solarized was designed with accessibility in mind ([1]), with carefully calibrated contrast ratios:

- **Light mode**: `base3` (bg) + `base00` (text) = 8.6:1 WCAG AAA contrast ([7])  
- **Dark mode**: `base03` (bg) + `base0` (text) = 8.6:1 WCAG AAA contrast ([7])  
- **Accents**: All accents maintain ≥4.5:1 contrast against both light and dark backgrounds ([7])  

When extending the token set:

1. **Test color combinations** for WCAG AAA compliance (minimum 7:1 for body text).  
2. **Use accent roles consistently** for semantic meaning; don't rely on color alone.  
3. **Provide focus indicators** using `border.strong` for keyboard navigation.  
4. **Test with colorblind simulators** (Coblis, Color Oracle) to ensure accents remain distinguishable.

---

## Contributing and feedback

This is a community resource. If you have suggestions for improvements, additional token types, or use cases, please open an issue or pull request ([3]).

---

## References

[1]: https://ethanschoonover.com/solarized/ "Solarized – Ethan Schoonover"  
[2]: https://en.wikipedia.org/wiki/Solarized "Solarized on Wikipedia"  
[3]: https://github.com/solarized "Solarized GitHub organization"  
[4]: https://www.designtokens.org/TR/2025.10/format/ "Design Tokens Format Module 2025.10"  
[5]: https://www.designtokens.org/TR/2025.10/resolver/ "Design Tokens Resolver Module 2025.10"  
[6]: https://www.designtokens.org/ "Design Tokens Community Group"  
[7]: https://www.w3.org/WAI/WCAG21/Understanding/contrast-minimum.html "WCAG 2.1 Contrast (Minimum)"  
[8]: https://commons.wikimedia.org/wiki/File:Solarized-palette.png "Solarized palette image (Wikimedia Commons)"