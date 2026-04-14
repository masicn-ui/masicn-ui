# masicn

> Copy-paste React Native UI components. Own the code. Ship faster.

masicn is a shadcn/ui-style component system built for React Native. Instead of installing a black-box UI library, you copy the source directly into your project — full control, zero lock-in.

**Built from scratch by [Manish Kumar](https://manishh.in) ([@lordofthemind](https://github.com/lordofthemind)) · Developed at [skipp.co.in](https://skipp.co.in)**

---

## The Name — मसि (Masi)

**Pronunciation:** _muh-see_ · **मसि** (Sanskrit/Hindi) · also written **मसी**

**Masi** (मसि / मसी) means **ink** in Sanskrit and several Indian languages. Historically, Indian masi was prepared from charcoal, gum, and natural pigments — the medium through which ideas became permanent, words became records, and art became visible.

> _"Just as ink can write anything — a poem, a law, a blueprint — masicn lets you build anything in React Native."_

The connection is intentional. A design system is the ink of UI development: invisible on its own, but the substance behind everything you ship. You bring the idea; masicn gives you the medium.

The **cn** suffix is a nod to shadcn/ui — the project that inspired this copy-paste philosophy.

---

## How It Works

```
npx masicn init       ← sets up the design system in your project
npx masicn add button ← copies Button.tsx into your project
```

That's it. You now own the code. Read it, change it, delete it — no restrictions.

---

## The Ecosystem

masicn is made up of several pieces that work together:

| Package | Repo | What it is |
|---------|------|------------|
| `masicn` (CLI) | [masicn-ui/cli](https://github.com/masicn-ui/cli) | The `npx masicn` command — init, add, update, remove |
| `@masicn/ui` | [masicn-ui/masicn](https://github.com/masicn-ui/masicn) | Core design system: tokens, theme, primitives, hooks |
| Registry | [masicn-ui/registry](https://github.com/masicn-ui/registry) | All component source files and metadata |
| Playground | private | Where all components are authored and tested |
| Gallery | private | Showcase app (coming to App Store / Play Store) |
| Docs | private | Documentation site (coming soon) |

---

## Getting Started

### Prerequisites

- Node.js >= 18
- An existing React Native project (>= 0.73)
- CocoaPods (for iOS)

### Step 1 — Initialize masicn

```bash
npx masicn init
```

The wizard will:
1. Ask you to pick a color palette
2. Copy the design system into your project (`src/masicn/`)
3. Patch `babel.config.js` and `react-native.config.js`
4. Install native dependencies (`react-native-reanimated`, `react-native-gesture-handler`)
5. Run `pod install` on iOS
6. Create `masicn.json` in your project root

### Step 2 — Add components

```bash
npx masicn add button
npx masicn add button card input    # multiple at once
npx masicn add                      # interactive picker
```

Components are copied as `.tsx` source files into your `outputDir` (default: `src/shared/components`). They import from your local design system copy — not from any npm package.

### Step 3 — Use them

```tsx
import { Button } from './shared/components/Button';

<Button variant="primary" onPress={handlePress}>
  Get Started
</Button>
```

---

## What You Get

### 55+ Components

| Category | Components |
|----------|-----------|
| Core | `button` `card` `avatar` `avatar-group` `badge` `chip` `image` `link` `tag` `pin` `detail-row` `dot` `ticker` `status-dot` `read-more` |
| Form | `text-input` `password-input` `textarea` `secure-input` `checkbox` `checkbox-group` `radio` `radio-group` `select` `slider` `range-slider` `switch` `segment` `toggle-group` |
| Feedback | `alert` `bottom-sheet` `left-sheet` `right-sheet` `top-sheet` `modal` `spinner` `loader` `shimmer` `skeleton` `snackbar` `toast` `progress` `progress-ring` `loading-overlay` |
| Interactive | `animated-card` `animated-number` `rating` `swipe-button` `drawer` `expandable` `dock` |
| Layout | `masonry-grid` `refreshable-list` `refreshable-scroll-view` `screen-layout` |
| Navigation | `accordion` `collapsible` `fab` `list-item` `search-bar` `tabs` |
| Overlay | `context-menu` `menu` `popover` `tooltip` |

### 17+ Blocks

Pre-composed screens and flows ready to drop in:

`action-sheet` `breadcrumb` `carousel` `confirm-dialog` `date-input` `empty-state` `form` `multi-select` `number-input` `otp-input` `pagination` `phone-input` `split-sheet` `step-indicator` `swipeable` `tag-input` `timeline`

### 15 Color Palettes

Pick one during init. Switch anytime in `masicn.json`.

| Palette | Vibe |
|---------|------|
| `masi` | Warm papaya + deep teal — the default |
| `ocean` | Deep blues + aqua |
| `sunset` | Warm oranges + purples |
| `forest` | Earthy greens + warm browns |
| `mono` | Monochrome slate |
| `rose` | Soft pinks + cranberry |
| `midnight` | Deep indigo + electric violet |
| `amber` | Golden honey + espresso |
| `nord` | Arctic blue-grays + frost |
| `coffee` | Espresso browns + caramel |
| `candy` | Hot pink + vivid sky blue — playful |
| `citrus` | Lime green + golden yellow — fresh |
| `grapeSoda` | Violet-purple + acid lime — loud |
| `jade` | Deep emerald + warm gold — premium |
| `neonTeal` | Electric teal + vivid violet — dark-native |

---

## The Design System (`@masicn/ui`)

All components are built on a layered design system. When you run `masicn init`, a local copy of this is placed in your project so you can read and modify it.

```
src/masicn/
├── tokens/       ← spacing, radius, typography, motion, elevation, ...
├── theme/        ← 15 palettes, createTheme(), dark/light mode
├── primitives/   ← Box, Stack, Row, Text, Pressable, Surface, ...
├── hooks/        ← useTheme(), useTokens(), useReducedMotion(), ...
├── animation/    ← spring presets (gentle, snappy, bouncy, ...)
└── utils/        ← rgba(), clamp(), color helpers
```

### Using tokens — always, no magic numbers

```tsx
const { theme } = useTheme();
const tokens = useTokens();

// Colors always from theme
<Box style={{ backgroundColor: theme.colors.surface.primary }} />

// Spacing always from tokens
<Stack style={{ padding: tokens.spacing.md, borderRadius: tokens.radius.lg }} />
```

### Primitives

```tsx
import { Box, Stack, Row, Text, Pressable, Surface } from '../masicn';
```

### Dark mode — automatic

The theme provides both `light` and `dark` variants. `MasicnProvider` handles switching.

```tsx
const { colorMode } = useTheme(); // 'light' | 'dark'
```

---

## Why Copy-Paste?

- **You own the code** — no waiting for a maintainer to accept your PR
- **No version hell** — components never break your app on upgrade
- **Easy to read** — the source is right there in your project
- **Easy to customize** — change props, styles, behavior without forking
- **No bundle bloat** — only what you add is in your bundle

The trade-off: you're responsible for applying updates when you want them. `masicn update` and `masicn diff` make this easy.

---

## CLI Commands

```bash
npx masicn init                     # set up masicn in your project
npx masicn add button               # add a component
npx masicn add button card input    # add multiple
npx masicn add --all                # add everything
npx masicn list                     # browse available components
npx masicn list --installed         # show installed components
npx masicn list --category form     # filter by category
npx masicn status                   # check installed vs registry
npx masicn update button            # update one component
npx masicn update                   # update all
npx masicn diff button              # see what changed
npx masicn remove button            # remove a component
npx masicn info button              # detailed component info + props
```

---

## `masicn.json`

Created by `masicn init` in your project root. Edit it anytime.

```json
{
  "version": "1",
  "outputDir": "src/shared/components",
  "blocksDir": "src/shared/blocks",
  "designSystemDir": "src/masicn",
  "palette": "masi",
  "localDesignSystem": true,
  "installedComponents": {
    "button": "0.0.1"
  }
}
```

---

## Links

- **npm (CLI):** [npmjs.com/package/masicn](https://www.npmjs.com/package/masicn)
- **npm (library):** [npmjs.com/package/@masicn/ui](https://www.npmjs.com/package/@masicn/ui)
- **Registry:** [github.com/masicn-ui/registry](https://github.com/masicn-ui/registry)
- **Design system:** [github.com/masicn-ui/masicn](https://github.com/masicn-ui/masicn)
- **Developer:** Manish Kumar — [manishh.in](https://manishh.in) · [@lordofthemind](https://github.com/lordofthemind)
- **Company:** [skipp.co.in](https://skipp.co.in)

---

## License

[MIT](./LICENSE) — free to use, modify, and distribute. Copyright © 2026 [Skipp](https://skipp.co.in).

Everything in the masicn ecosystem — the CLI, the design system library, and the component source files — is MIT licensed. When you copy a component into your project, you own that code completely. You can change it, ship it in a commercial product, or build on top of it without any restrictions. The only thing we ask is that the copyright notice is kept in place.

---

Made with care by [Manish Kumar](https://manishh.in) at [skipp.co.in](https://skipp.co.in)
