# design-system

Shared CSS design tokens and base styles for the agent-sh sites: agentsys, agent-sh.dev and agnix.

## Files

| File | What it holds |
|------|---------------|
| `tokens.css` | CSS custom properties on `:root`: background, border, text, accent and status colors, glow, typography, spacing, radius, shadows, glass, animation, z-index and layout. Breakpoints are listed in a comment for use in `@media` queries. |
| `base.css` | Reset, element defaults, a `prefers-reduced-motion` rule and utility classes: `.text-gradient`, `.glass`, `.glass-accent`, `.glow`, `.glow-strong`, `.border-gradient`, `.sr-only`. Import after `tokens.css`. |
| `tokens-docusaurus.css` | Maps the tokens to Docusaurus Infima `--ifm-*` variables, with a `html[data-theme='dark']` block. Import after `tokens.css`. |
| `check-sync.sh` | Checks that each consumer site imports the shared files. |

## Use

Plain sites import tokens and base styles:

```css
@import './design-system/tokens.css';
@import './design-system/base.css';
```

Docusaurus sites skip `base.css`, since Infima has its own reset, and import the bridge instead. Put site overrides after it:

```css
@import './design-system/tokens.css';
@import './design-system/tokens-docusaurus.css';
```

Fonts are not imported. Each site loads Inter and JetBrains Mono with `<link>` tags in its `<head>`. The tags to use are in the header comment of `tokens.css`.

## Check consumers

`check-sync.sh` expects this repo next to the consumer checkouts (`agentsys`, `agent-sh.dev`, `agnix`) in one parent directory:

```bash
./check-sync.sh
```

It exits 1 if a consumer file is missing or lacks the required `@import`.
