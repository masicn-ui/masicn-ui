# masicn

> Copy-paste React Native UI components. Own the code. Ship faster.

masicn is a shadcn/ui-style component system built for React Native. Instead of installing a black-box UI library, the CLI copies the source directly into your project — you own every line, full control, zero lock-in.

**Built from scratch by [Manish Kumar](https://manishh.in) ([@lordofthemind](https://github.com/lordofthemind)) · Developed at [skipp.co.in](https://skipp.co.in)**

[![npm CLI](https://img.shields.io/npm/v/masicn.svg?style=flat-square&label=masicn)](https://www.npmjs.com/package/masicn)
[![license](https://img.shields.io/badge/license-MIT-blue.svg?style=flat-square)](./LICENSE)

---

## The Name — मसि (Masi)

**Pronunciation:** _muh-see_ · **मसि** (Sanskrit/Hindi) · also written **मसी**

**Masi** (मसि / मसी) means **ink** in Sanskrit and several Indian languages. Historically, Indian masi was prepared from charcoal, gum, and natural pigments — the medium through which ideas became permanent, words became records, and art became visible.

> _"Just as ink can write anything — a poem, a law, a blueprint — masicn lets you build anything in React Native."_

The connection is intentional. A design system is the ink of UI development: invisible on its own, but the substance behind everything you ship. You bring the idea; masicn gives you the medium.

The **cn** suffix is a nod to shadcn/ui — the project that inspired this copy-paste philosophy.

---

## Screenshots

<!-- Replace the placeholders below with actual screenshots from the app -->

| | | |
|---|---|---|
| ![Screen 1](./screenshots/1.png) | ![Screen 2](./screenshots/2.png) | ![Screen 3](./screenshots/3.png) |
| ![Screen 4](./screenshots/4.png) | ![Screen 5](./screenshots/5.png) | ![Screen 6](./screenshots/6.png) |

---

## How It Works

masicn is **not a library you install and import.** Instead, the CLI copies the design system and component source files directly into your project. Your project ends up with real, editable `.tsx` files — no hidden internals, no npm dependency to maintain.

```
npx masicn@latest init        ← sets up the design system in your project
npx masicn@latest add button  ← copies Button.tsx into your project
```

After `add button`, you'll find `src/shared/components/Button/Button.tsx` in your codebase. Read it, change it, delete it — it's yours.

---

## Getting Started

### Prerequisites

- Node.js >= 18
- CocoaPods (for iOS)
- A **React Native CLI** project (>= 0.73) scaffolded with:
  ```bash
  npx @react-native-community/cli@latest init MyApp
  ```

> **Expo is not supported yet.** masicn patches native config files (`babel.config.js`, `react-native.config.js`) in a way specific to bare React Native CLI projects. Expo support is planned.

---

### Step 1 — Initialize masicn

```bash
npx masicn@latest init
```

The wizard will:
1. Ask you to pick one of 15 color palettes
2. Copy the entire design system into `src/masicn/` inside your project
3. Patch `babel.config.js` and `react-native.config.js`
4. Install native dependencies (`react-native-reanimated`, `react-native-gesture-handler`, `react-native-safe-area-context`, `react-native-svg`, `react-native-screens`)
5. Run `pod install` on iOS
6. Create `masicn.json` in your project root

After init your project structure will look like this:

```
MyApp/
├── src/
│   └── masicn/              ← the design system, now fully local
│       ├── tokens/
│       ├── theme/
│       ├── primitives/
│       ├── hooks/
│       ├── animation/
│       └── utils/
├── masicn.json
└── ...
```

| Flag | Description |
|------|-------------|
| `--interactive` | Full wizard — customize output dirs, design system mode, auto-patch `App.tsx` |
| `--skip-install` | Skip `npm install` and `pod install` |

---

### Step 2 — Wrap your app with `MasicnProvider`

```tsx
import { MasicnProvider } from './masicn';

export default function App() {
  return (
    <MasicnProvider>
      {/* your app */}
    </MasicnProvider>
  );
}
```

`MasicnProvider` handles theming, dark/light mode, and the global overlay layer for sheets, modals, and toasts.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `theme` | `'system' \| 'light' \| 'dark'` | `'system'` | Force a color mode or follow OS |
| `palettes` | `PaletteEntry[]` | built-in palettes | Override/extend the palette list |

---

### Step 3 — Add components

```bash
npx masicn@latest add button               # single
npx masicn@latest add button card modal    # multiple at once
npx masicn@latest add                      # interactive searchable picker
npx masicn@latest add --all               # everything
```

Files land in your `outputDir` (default: `src/shared/components`). Registry dependencies are resolved and copied automatically.

---

### Step 4 — Use them

```tsx
import { Button } from './shared/components/Button';

<Button variant="primary" onPress={handlePress}>
  Get Started
</Button>
```

---

## What You Get

### 54+ Components

| Category | Components |
|----------|-----------|
| Display | `avatar` `avatar-group` `badge` `card` `dot` `expandable` `image` `link` `list-item` `read-more` `tag` `ticker` |
| Feedback | `alert` `loader` `progress` `progress-ring` `shimmer` `skeleton` `snackbar` `spinner` `toast` |
| Actions | `button` `fab` `rating` `swipe-button` |
| Forms | `checkbox` `checkbox-group` `chip` `radio` `radio-group` `range-slider` `search-bar` `secure-input` `segment` `select` `slider` `switch` `text-input` `textarea` `toggle-group` |
| Navigation | `accordion` `collapsible` `detail-row` `dock` `pin` `tabs` |
| Overlays | `bottom-sheet` `context-menu` `drawer` `left-sheet` `menu` `modal` `popover` `right-sheet` `tooltip` `top-sheet` |

### 17+ Blocks

Pre-composed screens and flows ready to drop in:

| Block | Block | Block |
|-------|-------|-------|
| `action-sheet` | `breadcrumb` | `carousel` |
| `chip-input` | `code-input` | `confirm-dialog` |
| `date-input` | `dual-sheet` | `empty-state` |
| `form` | `json-tree` | `numeric-input` |
| `pagination` | `phone-input` | `stepper` |
| `swipeable` | `timeline` | |

### 3 Layout Components

`masonry-grid` · `refreshable-list` · `refreshable-scroll-view`

### 15 Color Palettes

Pick one during `init`. Switch anytime by editing `masicn.json`.

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

## The Design System

After `masicn init`, your project contains a full copy of the design system at `src/masicn/`. The layers, bottom-up:

```
src/masicn/
├── tokens/       ← spacing, radius, borders, typography, motion, elevation, ...
├── theme/        ← 15 palettes, createTheme(), dark/light mode
├── primitives/   ← Box, Stack, Row, Text, Pressable, Surface, ...
├── hooks/        ← useTheme(), useTokens(), useReducedMotion(), ...
├── animation/    ← spring presets (gentle, snappy, bouncy, ...)
└── utils/        ← rgba(), clamp(), color helpers
```

Every component you add imports from `'../../../masicn'` (relative path inside your project) — never from any npm package. This is intentional: you can modify the design system itself without publishing anything.

---

### Tokens — no magic numbers

Always use tokens; never raw numbers:

```tsx
import { useTheme, useTokens } from '../masicn';

const { theme } = useTheme();
const tokens = useTokens();

// colors always from theme
<Box style={{ backgroundColor: theme.colors.surfacePrimary }} />

// spacing always from tokens
<Stack style={{ padding: tokens.spacing.md, borderRadius: tokens.radius.lg }} />
```

**Spacing scale** (4pt grid):

| Token | Value |
|-------|-------|
| `none` | 0 |
| `xxs` | 2 |
| `xs` | 4 |
| `sm` | 8 |
| `md` | 12 |
| `lg` | 16 |
| `xl` | 24 |
| `xxl` | 32 |
| `xxxl` | 48 |

---

### Primitives

Primitives are low-level layout and display components that all other components are built on. They are already in `src/masicn/primitives/` after init.

```tsx
import { Box, Stack, Row, Wrap, Center, Spacer, Divider, Surface, Text, Icon, Pressable, Screen } from '../masicn';

// vertical list with spacing
<Stack gap="lg">
  <Text variant="heading">Hello</Text>
  <Text variant="body">World</Text>
</Stack>

// horizontal row
<Row gap="sm" align="center">
  <Icon name="check" />
  <Text>Confirmed</Text>
</Row>
```

---

### Dark mode — automatic

`MasicnProvider` reads the OS color scheme by default. Toggle programmatically:

```tsx
const { colorMode, toggleTheme } = useTheme();
// colorMode: 'light' | 'dark'
```

---

### Custom Themes with `createTheme`

You can override any color in the default light or dark theme using `createTheme`. All color keys are optional — you only provide what you want to change, and the rest inherits from the base palette.

```tsx
import { createTheme, MasicnProvider } from './masicn';

// override brand and background colors for both modes
const myTheme = createTheme({
  light: {
    colors: {
      primary: '#6200ee',
      onPrimary: '#ffffff',
      background: '#f5f5f5',
      surfacePrimary: '#ffffff',
    },
  },
  dark: {
    colors: {
      primary: '#bb86fc',
      onPrimary: '#000000',
      background: '#121212',
      surfacePrimary: '#1e1e1e',
    },
  },
});

// pass the custom pair to MasicnProvider
export default function App() {
  return (
    <MasicnProvider palettes={[{ name: 'brand', ...myTheme }]}>
      {/* your app */}
    </MasicnProvider>
  );
}
```

**Full list of overridable color tokens:**

| Group | Tokens |
|-------|--------|
| Background | `background` |
| Surfaces | `surfacePrimary` `surfaceSecondary` `surfaceTertiary` `surfaceOverlay` |
| Brand | `primary` `onPrimary` `secondary` `onSecondary` `tertiary` `onTertiary` `primaryContainer` |
| Text | `textPrimary` `textSecondary` `textTertiary` `textDisabled` `textInverse` `textLink` |
| Icons | `iconPrimary` `iconSecondary` `iconDisabled` |
| Borders | `borderPrimary` `borderSecondary` `borderFocused` `separator` |
| Inputs | `inputBackground` `inputBorder` `inputPlaceholder` |
| Status | `error` `onError` `success` `onSuccess` `warning` `onWarning` `info` `onInfo` `accent` `onAccent` |
| Interactive | `overlay` `highlight` `ripple` `disabled` |
| Navigation | `card` `tabBarActive` `tabBarInactive` `tabBarBackground` |
| Misc | `shadow` `skeleton` |

---

### Animation System

All built-in components use Reanimated. Spring presets and duration values are in `src/masicn/tokens/motion.ts`:

```tsx
import { motion, motionEasing } from '../masicn';
import { withSpring, withTiming } from 'react-native-reanimated';

// spring — runs on UI thread
withSpring(1, motion.spring.snappy)

// timing with easing
withTiming(1, { duration: motion.duration.normal, easing: motionEasing.standard })
```

**Spring presets:**

| Preset | Feel |
|--------|------|
| `gentle` | Smooth, overdamped settle |
| `snappy` | Fast and crisp |
| `bouncy` | Intentionally springy |
| `responsive` | Layout transitions |
| `sheet` | Bottom / side sheets |
| `snap` | Carousel snap |
| `dialog` | Modal scale-in |
| `check` | Checkbox pop |
| `indicator` | Radio dot |

**Duration presets:** `instant` (0ms) · `micro` (100ms) · `fast` (120ms) · `normal` (200ms) · `slow` (300ms) · `slower` (500ms) · `dramatic` (700ms)

---

## CLI Reference

### `init`

Set up masicn in your React Native project. Run this once.

```bash
npx masicn@latest init
```

### `add [components...]`

```bash
npx masicn@latest add button               # single
npx masicn@latest add button card modal    # multiple
npx masicn@latest add                      # interactive picker
npx masicn@latest add --all               # everything
```

| Flag | Description |
|------|-------------|
| `-f, --force` | Overwrite existing files without prompting |
| `--all` | Add every available component and block |

### `list`

```bash
npx masicn@latest list                       # all
npx masicn@latest list --installed           # only installed
npx masicn@latest list --category form       # filter by category
```

Categories: `core` · `form` · `feedback` · `interactive` · `layout` · `navigation` · `overlay` · `blocks`

### `info <component>`

Full details — props table, peer dependencies, registry dependencies, install status.

```bash
npx masicn@latest info button
npx masicn@latest info bottom-sheet
```

### `status`

See installed components and whether updates are available.

```bash
npx masicn@latest status
```

```
  button        v0.0.1   ✔ up to date
  card          v0.0.1   ✔ up to date  (modified locally)
  bottom-sheet  v0.0.1   ✔ up to date
```

### `update [component]`

```bash
npx masicn@latest update button    # one component
npx masicn@latest update           # all installed
```

### `diff <component>`

Line-by-line diff between your local file and the current registry version.

```bash
npx masicn@latest diff button
```

### `remove <component>`

```bash
npx masicn@latest remove button
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

## Why Copy-Paste?

The short version: you control what ships.

- **You own the code** — no waiting for a maintainer to accept your PR
- **No version hell** — components never silently break your app on an upgrade
- **Easy to read** — the source is right there in your editor
- **Easy to customize** — change props, styles, behavior without forking a library
- **No bundle bloat** — only what you add is in your bundle

The trade-off: you're responsible for applying updates when you want them. `masicn update` and `masicn diff` make this easy without forcing anything on you.

---

## Comparison with Other Design Systems

> Facts current as of 2026. Sources: official docs, GitHub repos, npm registry.

### Libraries at a glance

**NativeBase v3** — effectively in maintenance mode. The team that built it now maintains Gluestack UI as the successor and no longer recommends NativeBase for new projects.

**Gluestack UI v3** — the active successor to NativeBase from the same team (GeekyAnts). Switched to a copy-paste architecture in v2/v3, similar in spirit to masicn and shadcn/ui. Uses NativeWind (Tailwind CSS utility classes) as its styling engine.

**Tamagui** — an actively maintained cross-platform library (React Native + web). Uses a compiler to extract styles at build time. Token-based configuration via `tamagui.config.ts`. Core bundle is ~25 KB gzipped.

**React Native Paper** — implements Google's Material Design v3 (Material You). Actively maintained by Callstack. Strong accessibility story, respects OS `reduceMotion`. Primarily an npm package with an optional Babel plugin for tree-shaking.

---

### Feature comparison

| | masicn | Gluestack UI v3 | Tamagui | React Native Paper | NativeBase v3 |
|---|---|---|---|---|---|
| **Install model** | Copy-paste (CLI copies `.tsx` files) | Copy-paste (CLI-based, similar model) | npm package + compiler | npm package + optional Babel plugin | npm package — ⚠️ maintenance mode |
| **Styling approach** | Native token objects (`spacing.md`, `radius.lg`) | NativeWind / Tailwind utility classes | Compiler-extracted tokens via `tamagui.config.ts` | Material Design v3 theme object | Theme object + utility props |
| **Bundle impact** | Only what you add | Only what you add (copy-paste) | ~25 KB gzipped core | ~200–300 KB; tree-shakeable via Babel plugin | Entire library (one reason it was replaced) |
| **Vendor lock-in** | None — source lives in your repo | None — source lives in your repo | Low — but compiler is a build-time dependency | Moderate — tied to Material Design paradigm | Moderate — library updates can break app |
| **Expo support** | ❌ RN CLI only (Expo planned) | ✅ Full (Expo SDK 50+, optimized for SDK 53) | ✅ Full, documented setup guides | ✅ Full | ✅ (but team recommends migrating to Gluestack) |
| **Dark mode** | Automatic — follows OS, toggle programmatically | ✅ Built-in via theme tokens | ✅ Built-in, theme nesting supported | ✅ `MD3DarkTheme` + `useColorScheme` | ✅ Supported |
| **Animation** | Reanimated only — UI thread, semantic spring presets | Flexible — default plugin, Reanimated, or Moti | Flexible — RN Animated, Reanimated, CSS, Motion | ✅ Built-in, respects OS `reduceMotion` | Limited — some stagger helpers |
| **`reduceMotion` guard** | ✅ `useReducedMotion()` — enforced in every component | Depends on implementation | Respects OS preference | ✅ Respected automatically | ❌ Not built-in |
| **Accessibility** | Enforced by convention — every component has `accessibilityRole`, `accessibilityLabel`, `accessibilityHint` | Good — built with a11y in mind | Strong — ARIA-compliant, FocusScope | Excellent — WCAG compliant, 48dp touch targets, RTL | Standard RN props only |
| **TypeScript** | Strict — no `any`, no `@ts-ignore` | Excellent — TypeScript-first in v3 | Excellent — full type safety | Good — full types; `withTheme` limited to MD3 only | Partial — legacy definitions |
| **Custom themes** | `createTheme()` — override any of 65+ semantic color tokens | NativeWind CSS variables / token overrides | `createTamagui()` — token overrides | `MD3LightTheme` / `MD3DarkTheme` override | Theme object override |
| **Design philosophy** | RN-native tokens, no CSS, no external styling engine | Utility-first (Tailwind/NativeWind) | Cross-platform compiler, shared web+native tokens | Material Design spec compliance | Component-level theme props |
| **Component count** | 54 components + 17 blocks | 50+ | 50+ | 30+ | ~40 (not growing) |
| **Primitives** | Box, Stack, Row, Text, Pressable, Surface, Icon, Screen, ... | Box, HStack, VStack, ... | View, Text, Stack, XStack, YStack, ... | Surface (limited) | Box, HStack, VStack, ... |
| **Cross-platform (web)** | ❌ React Native only | ✅ Web via NativeWind | ✅ First-class web support | ❌ React Native only | ❌ React Native only |

---

### How to choose

**Pick masicn if** you want native-feeling components with zero dependency on any styling engine, a local design system you can actually read and edit, and Reanimated animations baked in from day one. Best for teams building a bespoke brand — not a generic Material or utility-class look.

**Pick Gluestack UI v3 if** you're coming from NativeBase, want Tailwind/NativeWind utility classes, or need Expo SDK 53+ support right now. The copy-paste model is similar to masicn's, but styling is CSS-first rather than RN-native.

**Pick Tamagui if** you're building a cross-platform app (React Native + web) and want a compiler-based approach with a tiny core bundle. More setup complexity upfront.

**Pick React Native Paper if** your product must follow Google's Material Design 3 spec exactly. Best accessibility out of all four, best choice if you're on Android-first.

**Avoid NativeBase** for new projects — the team recommends migrating to Gluestack UI.

---

## How Components Are Built

Every masicn component follows strict conventions so the source is consistent and readable no matter which component you open:

**Tokens everywhere:**
```tsx
// always tokens, never raw numbers
{ padding: spacing.md, borderRadius: radius.lg }
```

**Colors always semantic:**
```tsx
// always from theme, never raw hex
backgroundColor: theme.colors.surfacePrimary
borderColor: theme.colors.borderPrimary
```

**Animation on the UI thread:**
```tsx
// Reanimated for all transitions — never Animated API
const opacity = useSharedValue(0);
const style = useAnimatedStyle(() => ({ opacity: opacity.value }));
```

**Accessibility built in:**
```tsx
<Pressable
  accessibilityRole="button"
  accessibilityLabel={label}
  accessibilityHint={hint}
  accessibilityState={{ disabled }}
/>
```

---

## Links

- **npm (CLI):** [npmjs.com/package/masicn](https://www.npmjs.com/package/masicn)
- **Registry:** [github.com/masicn-ui/registry](https://github.com/masicn-ui/registry)
- **Developer:** Manish Kumar — [manishh.in](https://manishh.in) · [@lordofthemind](https://github.com/lordofthemind)
- **Company:** [skipp.co.in](https://skipp.co.in)

---

## License

[MIT](./LICENSE) — free to use, modify, and distribute. Copyright © 2026 [Skipp](https://skipp.co.in).

Everything in the masicn ecosystem — the CLI and all component source files — is MIT licensed. When you copy a component into your project, you own that code completely. You can change it, ship it in a commercial product, or build on top of it without any restrictions.

---

Made with care by [Manish Kumar](https://manishh.in) at [skipp.co.in](https://skipp.co.in)
