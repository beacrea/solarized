# Solarized Web Tokens

This folder contains a web‑oriented Design Tokens resource for the Solarized color scheme, expressed using the Design Tokens Community Group (DTCG) Format Module 2025.10 ([1][4]).

The goal of this resource is to:

- Preserve the canonical 16‑color Solarized palette (8 base monotones, 8 accents) ([1][2]).  
- Provide a general, implementation‑agnostic set of light/dark roles for web UIs.  
- Adhere to the DTCG 2025.10 format so tools can parse, validate, and resolve the tokens consistently ([4]).

## Files

- `solarized.web.2025.10.tokens.json`  
  A single token file that exposes the Solarized palette and generic web roles in the DTCG 2025.10 format ([4]).

The `id` field in this file is aligned with its expected location in this repository, and the root uses the official 2025.10 format schema URL for schema‑aware tooling ([4]).

## DTCG 2025.10 adherence

This token file is structured to follow the Design Tokens Format Module 2025.10 ([4]).

- Uses the 2025.10 format schema via the `$schema` URL, enabling JSON Schema–based validation in editors and build pipelines ([4]).  
- Uses `$type` and `$value` on token objects to distinguish groups from tokens, in line with the DTCG object model ([4]).  
- Color values are expressed as DTCG `color` values with:
  - `colorSpace: "srgb"`  
  - `components`: an RGB triple  
  - `hex`: the canonical Solarized hex string (optional convenience) ([1]).  
- Semantic tokens reference palette tokens using curly‑brace references (for example, `{color.palette.base3}`), which conforms to the reference format defined in the spec ([4]).

This design keeps palette tokens strictly primitive and role tokens as aliases, so alternate semantic mappings or additional theme layers can be added without changing the core Solarized values ([4]).

## Palette overview

Solarized defines 16 colors: 8 monotone “base” tones and 8 accents ([1][2]).

### Base tones

| Swatch | Token  | Hex       | RGB            | Description                |
|--------|--------|-----------|----------------|----------------------------|
| <span style="display:inline-block;width:1.2em;height:1.2em;background:#002b36;border:1px solid #000;"></span> | base03 | `#002b36` | `0, 43, 54`    | Darkest base tone          |
| <span style="display:inline-block;width:1.2em;height:1.2em;background:#073642;border:1px solid #000;"></span> | base02 | `#073642` | `7, 54, 66`    | Very dark base             |
| <span style="display:inline-block;width:1.2em;height:1.2em;background:#586e75;border:1px solid #000;"></span> | base01 | `#586e75` | `88, 110, 117` | Dark UI text / subtle fg   |
| <span style="display:inline-block;width:1.2em;height:1.2em;background:#657b83;border:1px solid #000;"></span> | base00 | `#657b83` | `101, 123, 131`| Primary dark text tone     |
| <span style="display:inline-block;width:1.2em;height:1.2em;background:#839496;border:1px solid #000;"></span> | base0  | `#839496` | `131, 148, 150`| Primary light text tone    |
| <span style="display:inline-block;width:1.2em;height:1.2em;background:#93a1a1;border:1px solid #000;"></span> | base1  | `#93a1a1` | `147, 161, 161`| Light UI text / subtle fg  |
| <span style="display:inline-block;width:1.2em;height:1.2em;background:#eee8d5;border:1px solid #000;"></span> | base2  | `#eee8d5` | `238, 232, 213`| Light surface background   |
| <span style="display:inline-block;width:1.2em;height:1.2em;background:#fdf6e3;border:1px solid #000;"></span> | base3  | `#fdf6e3` | `253, 246, 227`| Lightest base tone         |

### Accent tones

| Swatch | Token   | Hex       | RGB            | Description     |
|--------|---------|-----------|----------------|-----------------|
| <span style="display:inline-block;width:1.2em;height:1.2em;background:#b58900;border:1px solid #000;"></span> | yellow  | `#b58900` | `181, 137, 0`  | Accent: yellow  |
| <span style="display:inline-block;width:1.2em;height:1.2em;background:#cb4b16;border:1px solid #000;"></span> | orange  | `#cb4b16` | `203, 75, 22`  | Accent: orange  |
| <span style="display:inline-block;width:1.2em;height:1.2em;background:#dc322f;border:1px solid #000;"></span> | red     | `#dc322f` | `220, 50, 47`  | Accent: red     |
| <span style="display:inline-block;width:1.2em;height:1.2em;background:#d33682;border:1px solid #000;"></span> | magenta | `#d33682` | `211, 54, 130` | Accent: magenta |
| <span style="display:inline-block;width:1.2em;height:1.2em;background:#6c71c4;border:1px solid #000;"></span> | violet  | `#6c71c4` | `108, 113, 196`| Accent: violet  |
| <span style="display:inline-block;width:1.2em;height:1.2em;background:#268bd2;border:1px solid #000;"></span> | blue    | `#268bd2` | `38, 139, 210` | Accent: blue    |
| <span style="display:inline-block;width:1.2em;height:1.2em;background:#2aa198;border:1px solid #000;"></span> | cyan    | `#2aa198` | `42, 161, 152` | Accent: cyan    |
| <span style="display:inline-block;width:1.2em;height:1.2em;background:#859900;border:1px solid #000;"></span> | green   | `#859900` | `133, 153, 0`  | Accent: green   |

These values match the canonical Solarized definition by Ethan Schoonover ([1][3]).

### Swatch representation

While this repository does not include rendered images, the hex values above can be previewed directly in:

- Browser dev tools (for example, entering the hex value in a color picker).  
- Design tools that support JSON‑based token imports adhering to the DTCG format ([4]).

Many Solarized cheat sheets and theme previews on the web show the same colors; those can be used to visually verify this mapping ([2]).

## Roles and theming

The web token file defines generic roles in addition to the core palette.

- `color.palette.*`  
  The raw Solarized colors, intended to remain unchanged ([1]).

- `color.role.background.*`  
  Generic background roles with `light` and `dark` values (for example, page backgrounds and secondary surfaces).

- `color.role.foreground.*`  
  Generic text/icon roles with `light` and `dark` values (default, muted, inverse).

- `color.role.border.*`  
  Neutral border roles (subtle and strong).

- `color.role.accent.*`  
  Generic accent roles mapped to the chromatic Solarized colors (primary, success, warning, danger, info).

These roles are intentionally neutral and not tied to any specific component library; they are meant to be a reusable foundation for web‑oriented Solarized implementations.

## Using these tokens

A few suggested usage patterns:

- **Design tools**  
  Import the token file using a DTCG‑compatible plugin or pipeline to get the Solarized palette and roles as named colors ([4]).

- **Theming systems**  
  Bind `light` and `dark` role values into a theme or resolver layer, instead of hard‑coding Solarized hex values in CSS or code ([4]).

- **Extensions / integrations**  
  Additional token files (for typography, spacing, or platform‑specific roles) can reference this palette and role set using DTCG references, keeping color definitions centralized in this web resource ([4]).

## References

[1]: https://ethanschoonover.com/solarized/ "Solarized – Ethan Schoonover"  
[2]: https://en.wikipedia.org/wiki/Solarized "Solarized on Wikipedia"  
[3]: https://github.com/solarized "Solarized GitHub organization"  
[4]: https://www.designtokens.org/TR/2025.10/format/ "Design Tokens Format Module 2025.10"  
