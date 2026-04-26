# masicn

> Copy-paste React Native UI components. Own the code. Ship faster.

masicn is a shadcn/ui-style component system built for React Native. Instead of installing a black-box UI library, the CLI copies the source directly into your project — you own every line, full control, zero lock-in.

**Built from scratch by [Manish Kumar](https://manishh.in) ([@lordofthemind](https://github.com/lordofthemind)) · Developed at [skipp.co.in](https://skipp.co.in)**

[![npm CLI](https://img.shields.io/npm/v/masicn.svg?style=flat-square&label=masicn%20CLI)](https://www.npmjs.com/package/masicn)
[![npm design system](https://img.shields.io/npm/v/@masicn/ui.svg?style=flat-square&label=%40masicn%2Fui)](https://www.npmjs.com/package/@masicn/ui)
[![license](https://img.shields.io/badge/license-MIT-blue.svg?style=flat-square)](./LICENSE)

---

## TL;DR

- **Not an npm component library** — the CLI copies `.tsx` source files directly into your project. You own the code.
- **React Native CLI only** — bare RN projects (>= 0.73). Expo is not supported yet.
- **One command to start:** `npx masicn@latest init` → picks a palette, copies the design system, installs native deps, downloads fonts.
- **One command per component:** `npx masicn@latest add button` → `Button.tsx` lands in `src/shared/components/`.
- **54 components · 19 blocks · 15 color palettes** — all built on Reanimated, strict TypeScript, full accessibility.
- **Customize everything** — edit source directly, or use `createTheme()` to override any of 53 semantic color tokens.
- **No lock-in** — update on your schedule with `masicn update`, preview diffs with `masicn diff`.

---

## The Name — मसि (Masi)

**Pronunciation:** _muh-see_ · **मसि** (Sanskrit/Hindi) · also written **मसी**

**Masi** (मसि / मसी) means **ink** in Sanskrit and several Indian languages. Historically, Indian masi was prepared from charcoal, gum, and natural pigments — the medium through which ideas became permanent, words became records, and art became visible.

> _"Just as ink can write anything — a poem, a law, a blueprint — masicn lets you build anything in React Native."_

The **cn** suffix is a nod to shadcn/ui — the project that inspired this copy-paste philosophy.

---

## Screenshots

<!-- Replace with actual screenshots -->

| | | |
|---|---|---|
| ![Screen 1](./screenshots/1.png) | ![Screen 2](./screenshots/2.png) | ![Screen 3](./screenshots/3.png) |
| ![Screen 4](./screenshots/4.png) | ![Screen 5](./screenshots/5.png) | ![Screen 6](./screenshots/6.png) |

---

## How It Works

masicn is **not a library you install and import.** The CLI copies the design system and component source files directly into your project. Your project ends up with real, editable `.tsx` files — no hidden internals, no npm dependency to maintain.

```
npx masicn@latest init        ← sets up the design system in your project
npx masicn@latest add button  ← copies Button.tsx into your project
```

After `add button`, you'll find `src/shared/components/Button.tsx` in your codebase. Read it, change it, delete it — it's yours.

---

## Getting Started

### Prerequisites

- Node.js >= 18
- CocoaPods (for iOS)
- A **React Native CLI** project (>= 0.73):
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
2. Copy the entire design system (~91 files) into `src/masicn/`
3. Download Inter, Poppins, and Outfit fonts into `assets/fonts/` and link them
4. Patch `babel.config.js` and `react-native.config.js`
5. Install native dependencies (`react-native-reanimated`, `react-native-gesture-handler`, `react-native-safe-area-context`, `react-native-svg`, `react-native-screens`, `react-native-worklets`)
6. Run `pod install` on macOS
7. Create `masicn.json` in your project root

After init your project structure will look like this:

```
MyApp/
├── assets/
│   └── fonts/               ← Inter, Poppins, Outfit .ttf files
├── src/
│   └── masicn/              ← the design system, fully local
│       ├── tokens/
│       ├── theme/
│       ├── primitives/
│       ├── hooks/
│       ├── animation/
│       ├── utils/
│       └── system/
├── masicn.json
└── ...
```

| Flag | Description |
|------|-------------|
| `--interactive` | Full wizard — customise output dirs, design system path, auto-patch `App.tsx` |
| `--skip-install` | Skip `npm install` and `pod install` |

---

### Step 2 — Wrap your app with `MasicnProvider`

`masicn init` does this automatically. If you need to do it manually:

```tsx
import { MasicnProvider } from './src/masicn';
import { GestureHandlerRootView } from 'react-native-gesture-handler';

export default function App() {
  return (
    <GestureHandlerRootView style={{ flex: 1 }}>
      <MasicnProvider>
        {/* your app */}
      </MasicnProvider>
    </GestureHandlerRootView>
  );
}
```

`MasicnProvider` handles theming, dark/light mode, and the global overlay layer for sheets, modals, and toasts.

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `theme` | `'system' \| 'light' \| 'dark'` | `'system'` | Force a color mode or follow OS |
| `palettes` | `PaletteEntry[]` | built-in palettes | Provide custom palettes for runtime switching |

---

### Step 3 — Add components

```bash
npx masicn@latest add button               # single
npx masicn@latest add button card modal    # multiple at once
npx masicn@latest add                      # interactive searchable picker
npx masicn@latest add --all               # everything
npx masicn@latest add button --dry-run    # preview without writing
```

Files land in `outputDir` (default: `src/shared/components`). Registry dependencies are resolved and copied automatically.

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

### 54 Components

| Category | Components |
|----------|-----------|
| Display | `avatar` `avatar-group` `badge` `card` `dot` `expandable` `image` `link` `list-item` `tag` `ticker` |
| Feedback | `alert` `loader` `progress` `progress-ring` `shimmer` `skeleton` `snackbar` `spinner` `toast` |
| Actions | `button` `fab` `rating` `swipe-button` |
| Forms | `checkbox` `checkbox-group` `chip` `radio` `range-slider` `search-bar` `secure-input` `segment` `select` `slider` `switch` `text-input` `textarea` `toggle-group` |
| Navigation | `accordion` `collapsible` `detail-row` `dock` `pin` `tabs` |
| Overlays | `bottom-sheet` `context-menu` `drawer` `left-sheet` `menu` `modal` `popover` `right-sheet` `tooltip` `top-sheet` |

### 19 Blocks

Pre-composed screens and flows ready to drop in:

| Block | Block | Block |
|-------|-------|-------|
| `action-sheet` | `breadcrumb` | `carousel` |
| `chip-input` | `code-input` | `confirm` |
| `dual-sheet` | `empty-state` | `form` |
| `json-tree` | `masonry-grid` | `numeric` |
| `pagination` | `phone` | `refreshable-list` |
| `refreshable-scroll-view` | `stepper` | `swipeable` |
| `timeline` | | |

### 15 Color Palettes

Pick one during `init`. Generate a custom one with `masicn theme create`.

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
| `candy` | Hot pink + vivid sky blue |
| `citrus` | Lime green + golden yellow |
| `grapeSoda` | Violet-purple + acid lime |
| `jade` | Deep emerald + warm gold |
| `neonTeal` | Electric teal + vivid violet |

---

## The Design System

After `masicn init`, your project contains a full copy of the design system at `src/masicn/`. The layers, bottom-up:

```
src/masicn/
├── tokens/       ← spacing, radius, borders, typography, motion, elevation, sizes, ...
├── theme/        ← 15 palettes, createTheme(), dark/light mode
├── primitives/   ← Box, Stack, Row, Text, Pressable, Surface, ...
├── hooks/        ← useTheme(), useTokens(), useReducedMotion(), ...
├── animation/    ← motionEasing (standard, accelerate, decelerate, linear)
├── utils/        ← rgba(), clamp(), color helpers
└── system/       ← MasicnProvider, Masicn (portal), PortalHost
```

Every component you add imports from `'../../../masicn'` — never from any npm package. You can modify the design system itself without publishing anything.

---

### Tokens — no magic numbers

Always use tokens; never raw numbers:

```tsx
import { useTheme, useTokens } from '../masicn';

const { theme } = useTheme();
const { spacing, radius } = useTokens();

// colors always from theme
<Box style={{ backgroundColor: theme.colors.surfacePrimary }} />

// spacing and radius always from tokens
<Stack style={{ padding: spacing.md, borderRadius: radius.lg }} />
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

Low-level layout and display components all other components are built on:

```tsx
import { Box, Stack, Row, Wrap, Center, Spacer, Divider, Surface, Text, Pressable, Screen } from '../masicn';

// vertical list with gap
<Stack gap="lg">
  <Text variant="h2">Hello</Text>
  <Text variant="body">World</Text>
</Stack>

// horizontal row
<Row gap="sm" align="center">
  <Icon name="check" />
  <Text>Confirmed</Text>
</Row>
```

| Component | Description |
|-----------|-------------|
| `Box` | Base layout container |
| `Text` | Typography with variant + color token support |
| `Stack` | Vertical flex layout with gap |
| `Row` | Horizontal flex layout with gap |
| `Wrap` | Wrapping flex layout |
| `Center` | Centered content |
| `Spacer` | Flexible space filler |
| `Divider` | Visual separator |
| `Surface` | Themed surface with optional elevation |
| `Pressable` | Pressable with ripple and hit slop |
| `AspectRatio` | Aspect ratio container |
| `Circle` | Circular container |
| `Square` | Square container |
| `Screen` | Full-screen container |
| `SafeAreaScreen` | Safe area aware screen |
| `Icon` | SVG icon renderer |

---

### Theme API

#### `useTheme()`

Access the current theme and controls inside any component:

```tsx
import { useTheme } from '../masicn';

const {
  theme,          // fully resolved Theme object for the current mode + palette
  mode,           // 'light' | 'dark' | 'system'
  setMode,        // (mode: 'light' | 'dark' | 'system') => void
  toggleTheme,    // toggle between light and dark (ignores system pref)
  resetToSystem,  // resume following the OS light/dark preference
  palettes,       // PaletteEntry[] — all available palettes
  activePalette,  // name of the currently active palette
  setPalette,     // (name: string) => void — switch to a named palette
} = useTheme();

// use semantic color tokens — never raw hex
<Box style={{ backgroundColor: theme.colors.background }} />
<Text style={{ color: theme.colors.textPrimary }} />
```

#### `createTheme(overrides?)`

Creates a `{ light, dark }` theme pair. Accepts deep partial overrides — only the keys you provide are changed, everything else stays from the base palette. In dev mode, warns if you override some color tokens but not all (partial overrides can cause unexpected colors).

```tsx
import { createTheme } from '../masicn';

const myTheme = createTheme({
  light: {
    colors: {
      primary: '#6200ee',
      onPrimary: '#ffffff',
      background: '#f5f5f5',
    },
  },
  dark: {
    colors: {
      primary: '#bb86fc',
      onPrimary: '#000000',
      background: '#121212',
    },
  },
});
// myTheme.light and myTheme.dark are fully resolved Theme objects
```

Pass the pair to `MasicnProvider` via a `PaletteEntry`:

```tsx
import { MasicnProvider } from './masicn';

const brandPalette = { name: 'brand', label: 'Brand', pair: myTheme };

<MasicnProvider palettes={[brandPalette]}>
  <App />
</MasicnProvider>
```

Or use `masicn theme create` to generate a full 53-token palette interactively from two brand colors.

#### Color tokens

All 53 semantic color tokens available on `theme.colors.*`:

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
| Navigation | `card` `tabBarActive` `tabBarInactive` `tabBarBackground` `notification` |
| Misc | `shadow` `skeleton` |

---

### Dark Mode — automatic

`MasicnProvider` reads the OS color scheme by default. Toggle programmatically:

```tsx
const { mode, toggleTheme, setMode, resetToSystem } = useTheme();

// toggle light ↔ dark
<Button onPress={toggleTheme}>Toggle</Button>

// force a mode
setMode('dark');

// go back to following the OS
resetToSystem();
```

---

### Animation System

All built-in components use Reanimated for UI-thread animations. Spring presets and duration values come from `src/masicn/tokens/motion.ts`:

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

### Hooks

```tsx
import {
  useTheme,           // current theme, mode, toggleTheme, setPalette
  useTokens,          // raw design tokens (spacing, radius, typography, motion, ...)
  useReducedMotion,   // boolean — true when OS prefers reduced motion
  useResponsive,      // responsive breakpoints (Breakpoint, ResponsiveInfo)
  useAccessibilityProps, // accessibility prop helpers
  useFocusTrap,       // keyboard focus management for modals/dialogs
  useGradients,       // gradient helpers derived from the active theme
} from '../masicn';
```

---

## CLI Reference

All commands support `--help` for inline docs.

### `init` — first-time setup

```bash
npx masicn@latest init
npx masicn@latest init --interactive    # full wizard
npx masicn@latest init --skip-install  # skip npm install + pod install
```

### `doctor` — health checks

Run 8 automated checks against your project setup:

```bash
npx masicn@latest doctor
```

Checks: `masicn.json` valid · `MasicnProvider` in App · Reanimated babel plugin (last) · `GestureHandlerRootView` in App · gesture-handler import in index · peer deps installed · font assets present · design system files present.

Exits with code 1 if any check fails, with a `fix:` hint for each failure.

### `add` — install components

```bash
npx masicn@latest add button                 # single
npx masicn@latest add button card modal      # multiple
npx masicn@latest add                        # interactive picker
npx masicn@latest add --all                 # everything
npx masicn@latest add button --dry-run      # preview without writing
npx masicn@latest add button --force        # overwrite existing files
```

Registry dependencies are resolved and installed automatically.

### `update` — pull newer versions

```bash
npx masicn@latest update button      # one component
npx masicn@latest update             # all installed components
npx masicn@latest update -d          # refresh design system files from GitHub
npx masicn@latest update -d --force  # refresh without confirmation
```

### `remove` — uninstall a component

```bash
npx masicn@latest remove button
npx masicn@latest remove button --yes    # skip confirmation
```

### `list` — browse the registry

```bash
npx masicn@latest list
npx masicn@latest list --installed
npx masicn@latest list --category form
```

### `status` — check for updates

```bash
npx masicn@latest status
npx masicn@latest status --check-modified    # flag locally edited files
```

```
  button        v0.0.2   ✔ up to date
  card          v0.0.1   ↑ v0.0.2 available
  bottom-sheet  v0.0.2   ✔ up to date  (modified locally)
```

### `diff` — compare to registry

```bash
npx masicn@latest diff button
```

Line-by-line diff between your local file and the registry version.

### `info` — component details

```bash
npx masicn@latest info button
npx masicn@latest info bottom-sheet
```

Shows props table, peer deps, registry deps, install status, and usage examples.

### `search` — find components

```bash
npx masicn@latest search button
npx masicn@latest search "swipe gesture"
npx masicn@latest search sheet --top 5
```

Ranked by tag match (3pts), name (2pts), description (1pt).

### `graph` — dependency tree

```bash
npx masicn@latest graph               # full ecosystem
npx masicn@latest graph avatar-group  # single component
npx masicn@latest graph --cycles      # detect circular dependencies
```

### `usage` — scan your project

```bash
npx masicn@latest usage
npx masicn@latest usage --unused      # only show components with zero usages
npx masicn@latest usage --src app/src
```

### `upgrade` — one-step refresh

```bash
npx masicn@latest upgrade             # design system + all components
npx masicn@latest upgrade --channel dev
```

### `migrate` — apply breaking changes

```bash
npx masicn@latest migrate                     # report all migrations
npx masicn@latest migrate button              # one component
npx masicn@latest migrate --apply             # auto-fix transforms
npx masicn@latest migrate --apply --dry-run   # preview transforms
```

### `theme create` — generate a palette

```bash
npx masicn@latest theme create brand
npx masicn@latest theme create brand --preview
```

Interactively enter two brand colors (hex). Derives all 53 semantic tokens using `chroma-js`. Writes to `src/masicn/theme/palettes/<name>.ts`.

```tsx
import { brandPalette } from './masicn/theme/palettes/brand';
<MasicnProvider palettes={[{ name: 'brand', label: 'Brand', pair: brandPalette }]}>
```

### `interactive` — TUI browser

```bash
npx masicn@latest interactive
npx masicn@latest i    # alias
```

Browse all components in a grouped multiselect TUI, resolve deps, confirm, install.

### `mcp` — AI tool integration

```bash
npx masicn@latest mcp
```

Starts a [Model Context Protocol](https://modelcontextprotocol.io) server on `stdin/stdout`. Add to Claude Desktop (`~/Library/Application Support/Claude/claude_desktop_config.json`):

```json
{
  "mcpServers": {
    "masicn": { "command": "npx", "args": ["masicn@latest", "mcp"] }
  }
}
```

Tools: `list_components` · `get_component_details` · `search_components` · `install_component`

---

## `masicn.json`

Created by `masicn init`. Edit it manually if needed.

```json
{
  "version": "1",
  "registry": "https://raw.githubusercontent.com/masicn-ui/registry/master/registry.json",
  "outputDir": "src/shared/components",
  "importAlias": "@/shared/components",
  "blocksDir": "src/shared/blocks",
  "blocksAlias": "@/shared/blocks",
  "designSystemDir": "src/masicn",
  "masicnAlias": "@/masicn",
  "palette": "masi",
  "localDesignSystem": true,
  "fontSetup": "masicn",
  "installedComponents": {
    "button": "0.0.2"
  }
}
```

---

## Why Copy-Paste?

The short version: you control what ships.

- **You own the code** — no waiting for a maintainer to accept your PR
- **No version hell** — components never silently break on an upgrade
- **Easy to read** — the source is right there in your editor
- **Easy to customize** — change props, styles, behavior without forking a library
- **No bundle bloat** — only what you add is in your bundle

The trade-off: you're responsible for applying updates when you want them. `masicn update` and `masicn diff` make this easy without forcing anything on you.

---

## Comparison

> Facts current as of 2026.

| | masicn | Gluestack UI v3 | Tamagui | React Native Paper | NativeBase v3 |
|---|---|---|---|---|---|
| **Install model** | Copy-paste (CLI) | Copy-paste (CLI) | npm + compiler | npm + optional Babel plugin | npm — ⚠️ maintenance mode |
| **Styling** | RN token objects | NativeWind / Tailwind | Compiler-extracted tokens | Material Design v3 theme | Theme object + utility props |
| **Bundle impact** | Only what you add | Only what you add | ~25 KB gzipped core | ~200–300 KB (tree-shakeable) | Entire library |
| **Expo support** | ❌ RN CLI only (planned) | ✅ Full | ✅ Full | ✅ Full | ✅ (team recommends migrating) |
| **Dark mode** | Automatic + `setMode()` | ✅ Built-in | ✅ Built-in | ✅ `MD3DarkTheme` | ✅ Supported |
| **Animation** | Reanimated — UI thread | Flexible | Flexible | ✅ Built-in | Limited |
| **`reduceMotion`** | ✅ `useReducedMotion()` — every component | Depends on impl | ✅ Respects OS | ✅ Automatic | ❌ Not built-in |
| **Accessibility** | `accessibilityRole` + `accessibilityLabel` + `accessibilityHint` — enforced | Good | Strong | Excellent (WCAG, 48dp) | Standard RN props only |
| **TypeScript** | Strict — no `any`, no `@ts-ignore` | TypeScript-first v3 | Full type safety | Good | Partial |
| **Custom themes** | `createTheme()` — 53 semantic tokens | NativeWind CSS vars | `createTamagui()` | `MD3LightTheme` override | Theme object |
| **Components** | 54 + 19 blocks | 50+ | 50+ | 30+ | ~40 (not growing) |
| **Web support** | ❌ RN only | ✅ NativeWind | ✅ First-class | ❌ RN only | ❌ RN only |

**Pick masicn if** you want native-feeling components with zero styling-engine dependency, a local design system you can read and edit, and Reanimated animations baked in. Best for teams building a bespoke brand.

**Pick Gluestack UI v3 if** you're coming from NativeBase, want Tailwind utility classes, or need Expo SDK 53+ support right now.

**Pick Tamagui if** you're building cross-platform (React Native + web) and want a compiler-based approach with a tiny core.

**Pick React Native Paper if** your product must follow Google's Material Design 3 spec exactly.

---

## How Components Are Built

Every masicn component follows strict conventions:

**Tokens everywhere — no magic numbers:**
```tsx
{ padding: spacing.md, borderRadius: radius.lg }   // ✓
{ padding: 16, borderRadius: 8 }                   // ✗
```

**Colors always semantic — never raw hex:**
```tsx
backgroundColor: theme.colors.surfacePrimary   // ✓
backgroundColor: '#ffffff'                     // ✗
```

**Animations on the UI thread:**
```tsx
const opacity = useSharedValue(0);
const style = useAnimatedStyle(() => ({ opacity: opacity.value }));
// Always Reanimated — never Animated API
```

**Accessibility enforced:**
```tsx
<Pressable
  accessibilityRole="button"
  accessibilityLabel={label}
  accessibilityHint={hint}
  accessibilityState={{ disabled }}
/>
```

**Reduced motion respected:**
```tsx
const reducedMotion = useReducedMotion();
// instant duration when reduceMotion is on, animated otherwise
```

---

## Links

- **npm (CLI):** [npmjs.com/package/masicn](https://www.npmjs.com/package/masicn)
- **npm (design system):** [npmjs.com/package/@masicn/ui](https://www.npmjs.com/package/@masicn/ui)
- **Registry:** [github.com/masicn-ui/registry](https://github.com/masicn-ui/registry)
- **Developer:** Manish Kumar — [manishh.in](https://manishh.in) · [@lordofthemind](https://github.com/lordofthemind)
- **Company:** [skipp.co.in](https://skipp.co.in)

---

## License

[MIT](./LICENSE) — free to use, modify, and distribute. Copyright © 2026 [Skipp](https://skipp.co.in).

Everything in the masicn ecosystem — the CLI and all component source files — is MIT licensed. When you copy a component into your project, you own that code completely. Change it, ship it in a commercial product, or build on top of it without any restrictions.

---

Made with care by [Manish Kumar](https://manishh.in) at [skipp.co.in](https://skipp.co.in)
