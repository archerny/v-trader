# V-Trader Design System

Owner: Visual Designer + Frontend Engineer
Created: 2026-03-29
Design review: All 7 dimensions reviewed via /plan-design-review

## Design Principles

**Style:** TradingView-native dark theme — directly referencing TradingView's actual color system and visual language, not a generic "inspired by" approach.

**Core Visual Identity from TradingView:**
- Background: Cool-blue undertone `#131722` → `#1e222d` → `#2a2e39` (blue channel > red channel in all backgrounds)
- Text: Warm gray `#d1d4dc` (not pure white, reduces glare during long trading sessions)
- Brand accent: `#2962ff` (TradingView's exact Dodger Blue)
- Up/profit: `#26a69a` (TradingView's exact teal-green)
- Down/loss: `#ef5350` (TradingView's exact coral-red)
- UI font: Trebuchet MS (TradingView's primary font)
- Minimal shadows, borders for separation instead of elevation
- No rounded fat cards — compact, data-dense surfaces

**Guiding Rule:** When in doubt about any visual decision, open TradingView's chart page in dark mode and match it. The goal is for V-Trader to feel like a native extension of TradingView's ecosystem.

---

## Color Palette

All background colors use TradingView's signature **cool-blue undertone** (blue channel > red channel).
Colors are sourced from TradingView's actual CSS variables and brand guidelines.

### Background (TradingView Dark Theme)
| Token | Value | TradingView Reference | Usage |
|-------|-------|----------------------|-------|
| `--bg-primary` | `#131722` | `--tv-color-platform-background` | Main background, deepest (the signature TradingView dark) |
| `--bg-secondary` | `#1e222d` | `--tv-color-pane-background` | Panel/card background, toolbar background |
| `--bg-tertiary` | `#2a2e39` | `--tv-color-pane-background-secondary` | Input fields, secondary panels, expanded toolbars |
| `--bg-hover` | `#363a45` | `--tv-color-toolbar-button-background-hover` | Row hover, button hover state |
| `--bg-active` | `#414650` | — | Active/pressed state background |

### Text (TradingView Dark Theme)
| Token | Value | Usage |
|-------|-------|-------|
| `--text-primary` | `#d1d4dc` | Primary text — TradingView's actual text color (warm gray, not pure white) |
| `--text-secondary` | `#787b86` | Secondary text, labels, axis labels — TradingView's muted text |
| `--text-muted` | `#4c525e` | Disabled, placeholder text |
| `--text-active` | `#ffffff` | Active/selected text, important highlights |

### Accent (TradingView Brand)
| Token | Value | Usage |
|-------|-------|-------|
| `--accent-blue` | `#2962ff` | TradingView brand blue — primary accent, links, buttons, selected state |
| `--accent-blue-hover` | `#1e53e5` | Accent hover state |
| `--accent-blue-active` | `#1848cc` | Accent pressed state |

### Semantic (Configurable: default International Standard)
| Token | Default (International) | Alternative (Chinese) | Usage |
|-------|------------------------|----------------------|-------|
| `--color-profit` | `#26a69a` | `#ef5350` | Profit / up — TradingView's exact green |
| `--color-loss` | `#ef5350` | `#26a69a` | Loss / down — TradingView's exact red |
| `--color-profit-bg` | `rgba(38,166,154,0.12)` | `rgba(239,83,80,0.12)` | Profit background fill |
| `--color-loss-bg` | `rgba(239,83,80,0.12)` | `rgba(38,166,154,0.12)` | Loss background fill |
| `--color-warning` | `#ff9800` | `#ff9800` | Warning, ATM highlight |
| `--color-info` | `#42a5f5` | `#42a5f5` | Info tooltip |

### Surface (TradingView Dark Theme)
| Token | Value | Usage |
|-------|-------|-------|
| `--border-color` | `#2a2e39` | Dividers, borders — same as bg-tertiary, TradingView style |
| `--border-subtle` | `#1e222d` | Subtle separators between panels |
| `--border-focus` | `#2962ff` | Focus ring — brand blue |

### Option Chain Specific
| Token | Value | Usage |
|-------|-------|-------|
| `--itm-call-bg` | `rgba(38,166,154,0.06)` | Call ITM row background (using TradingView green) |
| `--itm-put-bg` | `rgba(239,83,80,0.06)` | Put ITM row background (using TradingView red) |
| `--atm-border` | `#ff9800` | ATM row left border (3px) |
| `--row-hover-bg` | `rgba(255,255,255,0.04)` | Table row hover |
| `--row-selected-bg` | `rgba(41,98,255,0.12)` | Selected row background (brand blue tint) |
| `--selected-indicator` | `#26a69a` | Selected leg green bar |

---

## Typography

### Font Stack
| Token | Value | Usage |
|-------|-------|-------|
| `--font-sans` | `'Trebuchet MS', 'Roboto', 'Ubuntu', -apple-system, sans-serif` | UI text — TradingView uses Trebuchet MS as primary |
| `--font-mono` | `'JetBrains Mono', 'SF Mono', 'Menlo', monospace` | All financial numbers, code — monospace for aligned digits |

### Scale
| Token | Size / Line Height | Usage |
|-------|-------------------|-------|
| `--text-xs` | `11px / 16px` | Smallest labels |
| `--text-sm` | `12px / 18px` | Secondary data, table headers |
| `--text-base` | `13px / 20px` | Body text, table data |
| `--text-lg` | `15px / 22px` | Subtitles |
| `--text-xl` | `20px / 28px` | Large numbers, Greek main values |
| `--text-2xl` | `28px / 36px` | Core metrics (e.g., current price) |

### Weight
| Token | Value | Usage |
|-------|-------|-------|
| `--font-normal` | `400` | Body text |
| `--font-medium` | `500` | Table headers, labels |
| `--font-semibold` | `600` | Emphasized numbers |

---

## Spacing

Base unit: 4px

| Token | Value | Usage |
|-------|-------|-------|
| `--space-1` | `4px` | Minimum gap (icon ↔ text) |
| `--space-2` | `8px` | Compact element spacing |
| `--space-3` | `12px` | Table cell padding |
| `--space-4` | `16px` | Card padding, block spacing |
| `--space-5` | `20px` | Panel spacing |
| `--space-6` | `24px` | Section spacing |
| `--space-8` | `32px` | Large block spacing |

---

## Component Tokens

### Border Radius
| Token | Value | Usage |
|-------|-------|-------|
| `--radius-sm` | `4px` | Buttons, inputs, tags |
| `--radius-md` | `6px` | Cards, panels |
| `--radius-lg` | `8px` | Modals, large containers |
| `--radius-full` | `9999px` | Circular indicators |

### Shadow (Minimal — almost no shadows)
| Token | Value | Usage |
|-------|-------|-------|
| `--shadow-sm` | `none` | Cards use borders, not shadows |
| `--shadow-dropdown` | `0 4px 12px rgba(0,0,0,0.3)` | Dropdown menus only |
| `--shadow-modal` | `0 8px 32px rgba(0,0,0,0.5)` | Modals only |

### Layout
| Token | Value | Usage |
|-------|-------|-------|
| `--row-height` | `32px` | Default table row height |
| `--row-height-compact` | `28px` | Compact mode row height |
| `--header-height` | `36px` | Table header height |
| `--sidebar-width` | `56px` | Sidebar collapsed |
| `--sidebar-width-expanded` | `200px` | Sidebar expanded |
| `--tab-height` | `40px` | Tab bar height |
| `--tab-gap` | `0px` | Tabs touch, separated by bottom line |
| `--topbar-height` | `48px` | Top bar height |
| `--bottombar-height` | `32px` | Bottom bar height |

---

## Visual Anchors for Key Components

Each component directly references a specific TradingView element for visual consistency.

| Component | TradingView Reference | Specific Behavior |
|-----------|----------------------|-------------------|
| Price Chart | TradingView Lightweight Charts — exact same library, same look | Crosshair follows mouse, hover shows OHLCV. Time range: 1D/1W/1M/3M/1Y/All. Candlestick default with volume overlay at bottom 20% |
| Option Chain | TradingView watchlist density + Thinkorswim chain layout | Call left \| Strike center \| Put right. Cool-blue bg `#131722`, row hover `#363a45`. Hover row → [B][S] buttons appear |
| Greeks Dashboard | TradingView indicator value display style (compact, mono-font, color-coded) | Value changes with 300ms ease transition. Each Greek has tooltip explanation. Green=favorable, Red=unfavorable |
| P&L Chart | OptionStrat area-fill + TradingView chart styling | Profit area `rgba(38,166,154,0.12)` fill, loss area `rgba(239,83,80,0.12)` fill. TradingView crosshair interaction. Hover shows P&L at any price |
| IV Charts | TradingView overlay indicator style | IV and HV dual-line overlay, toggleable. Semi-transparent fill between lines. TradingView-style axis labels in `#787b86` |
| Metric Cards | TradingView watchlist summary style — compact, no decoration | Main number monospace `--text-xl`, change small `--text-sm`. No shadow, no border, subtle spacing. TradingView green/red with ▲/▼ arrows |
| Sidebar | TradingView left toolbar style — icon-only collapsed, minimal | 56px collapsed width, icons centered, active item highlighted with brand blue `#2962ff` left bar |
| Tab Bar | TradingView bottom tab/panel switcher style | Tabs tight together, active tab has brand blue `#2962ff` bottom border 2px. Text `#d1d4dc` active, `#787b86` inactive |

---

## Motion System

### Timing Tokens
| Token | Value | Usage |
|-------|-------|-------|
| `--duration-instant` | `100ms` | Color change, hover state |
| `--duration-fast` | `200ms` | Small element appear/disappear |
| `--duration-normal` | `300ms` | Panel switch, value transition |
| `--duration-slow` | `500ms` | Chart animation, large area transition |

### Easing
| Token | Value | Usage |
|-------|-------|-------|
| `--ease-default` | `cubic-bezier(0.4, 0, 0.2, 1)` | Standard |
| `--ease-in` | `cubic-bezier(0.4, 0, 1, 1)` | Exit |
| `--ease-out` | `cubic-bezier(0, 0, 0.2, 1)` | Enter |
| `--ease-spring` | `cubic-bezier(0.34, 1.56, 0.64, 1)` | Important feedback (button press) |

### Data Transitions
- **Price/number change:** 300ms ease smooth transition (not jump). Flash green (up) or red (down) for 800ms fade.
- **Greeks dashboard:** 300ms ease value transition. First load: count from 0 to target (500ms).
- **Charts:** First render left-to-right fade (500ms). Data update: smooth transition. Time range switch: 300ms zoom transition.

### Interaction Feedback
- **Option chain [B][S] buttons:** Hover row → buttons opacity 0→1 (150ms). Click → scale 0.95→1 spring (200ms). Success → green bar slide-in left (200ms).
- **Tab switch:** Bottom indicator slides to new tab (300ms). Content area: 200ms fade-in (no directional slide).
- **Strategy legs:** Add → new row slide-down + fade-in (300ms). Remove → fade-out + collapse (250ms). Reorder → smooth slide to new position (300ms).

### Anti-Motion Rules
- ✗ No page-level animations (full-page slide/zoom)
- ✗ No bounce/shake effects (financial tools need stability)
- ✗ No 3D transforms (not a marketing page)
- ✗ No row-level animation on table data update (only number flash)
- ✗ Respect `prefers-reduced-motion`: disable ALL animations

---

## Responsiveness & Accessibility

**Responsive strategy:** Desktop only (≥1280px). Below 1280px shows horizontal scrollbar. No tablet or mobile adaptation.

**Accessibility (minimum for personal tool):**
- Color contrast ≥ 4.5:1 (WCAG AA) — dark background naturally satisfies
- All interactive elements keyboard-focusable (Tab navigation)
- `prefers-reduced-motion` respected — all animations disabled
- Up/down not color-only — ▲/▼ arrows supplement green/red
- No ARIA labels (no screen reader support needed)
- No high-contrast theme
- No font scaling support
