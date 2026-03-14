# Bolt.new UI Specification — AI Talent Marketplace Platform (Web App)

> **Generated for:** bolt.new full-stack code generation
> **Scope:** Web application only (`apps/web`) — recruiter, admin, and public/auth surfaces
> **Backend contract:** All pages wire to the existing GraphQL API at `apps/api`. No backend generation needed from bolt.
> **Design source:** Atome.ph design language (dark, bold, Spriteburst-accented consumer fintech) with Larsseit font family replacing all typography.
> **Reference:** `maingoalandreference/AI Talent Marketplace Platform (SOW).md`

---

## PART 1 — DESIGN SYSTEM

---

### 1.1 Brand Foundation

The visual identity is borrowed from **Atome's design language**: dark backgrounds, bold contrast, their signature yellow-green accent color called **Spriteburst**, clean layout blocks, and confident typography. The difference is the font — Larsseit replaces Atome's typeface entirely.

**Brand personality:**
- Confident, direct, premium
- Enterprise B2B but with consumer-grade polish
- Empowering, action-forward
- No decorative fluff — every element earns its space

**Visual DNA from Atome:**
- Full dark shell
- Spriteburst green as primary action and accent color
- Large bold headings
- Clean white on dark text hierarchy
- Rounded but not soft — firm corners with intent
- Strong contrast between surface layers
- Motion-forward: transitions that feel fast and purposeful

---

### 1.2 Color System

All colors are defined as CSS custom properties. Use these tokens everywhere — never hardcode hex values in components.

#### Background Layer Tokens

```css
--color-bg:           #000000;   /* deepest background — page shell */
--color-surface:      #0A0A0A;   /* elevated surface — panels, sidebar */
--color-surface-alt:  #1A1A1A;   /* card surface, table rows, input bg */
--color-surface-high: #222222;   /* hover state surface, active row */
--color-overlay:      rgba(0, 0, 0, 0.72);  /* modal/drawer scrim */
```

#### Text Tokens

```css
--color-text-primary:   #FFFFFF;    /* main content text */
--color-text-secondary: #A1A1AA;    /* subtext, metadata, helper labels */
--color-text-muted:     #52525B;    /* placeholder, disabled, timestamp */
--color-text-inverse:   #000000;    /* text on Spriteburst button */
```

#### Brand / Action Tokens

```css
--color-primary:          #EFFE5E;   /* Spriteburst — primary actions, highlights */
--color-primary-hover:    #BBB906;   /* Spriteburst hover state */
--color-primary-muted:    rgba(181, 227, 27, 0.12);  /* subtle primary tint */
--color-primary-border:   rgba(181, 227, 27, 0.30);  /* primary-tinted borders */
```

#### Semantic State Tokens

```css
--color-success:         #22C55E;
--color-success-muted:   rgba(34, 197, 94, 0.12);
--color-warning:         #F59E0B;
--color-warning-muted:   rgba(245, 158, 11, 0.12);
--color-destructive:     #EF4444;
--color-destructive-muted: rgba(239, 68, 68, 0.12);
--color-info:            #3B82F6;
--color-info-muted:      rgba(59, 130, 246, 0.12);
```

#### Border Tokens

```css
--color-border:        #27272A;   /* default border */
--color-border-subtle: #1F1F22;   /* very subtle divider */
--color-border-strong: #3F3F46;   /* focused/active borders */
```

#### Status Badge Colors (used for demand/interview/offer status chips)

| Status | Background | Text |
|--------|-----------|------|
| ACTIVE | `--color-success-muted` | `--color-success` |
| DRAFT | `--color-surface-high` | `--color-text-secondary` |
| PAUSED | `--color-warning-muted` | `--color-warning` |
| FILLED | `--color-info-muted` | `--color-info` |
| CANCELLED | `--color-destructive-muted` | `--color-destructive` |
| PENDING | `--color-warning-muted` | `--color-warning` |
| VERIFIED | `--color-success-muted` | `--color-success` |
| REJECTED | `--color-destructive-muted` | `--color-destructive` |
| SCHEDULED | `--color-info-muted` | `--color-info` |
| COMPLETED | `--color-success-muted` | `--color-success` |
| SENT | `--color-primary-muted` | `--color-primary` |
| ACCEPTED | `--color-success-muted` | `--color-success` |
| DECLINED | `--color-destructive-muted` | `--color-destructive` |

---

### 1.3 Typography System — Larsseit

All fonts use Larsseit, loaded from local files at `font/Larsseit-Sans-Serif-Font-Family/Larsseit/Larsseit/`.

#### Font Face Declarations

```css
@font-face {
  font-family: 'Larsseit';
  src: url('/fonts/Larsseit.otf') format('opentype');
  font-weight: 400;
  font-style: normal;
  font-display: swap;
}
@font-face {
  font-family: 'Larsseit';
  src: url('/fonts/Larsseit-Light.otf') format('opentype');
  font-weight: 300;
  font-style: normal;
  font-display: swap;
}
@font-face {
  font-family: 'Larsseit';
  src: url('/fonts/Larsseit-Medium.otf') format('opentype');
  font-weight: 500;
  font-style: normal;
  font-display: swap;
}
@font-face {
  font-family: 'Larsseit';
  src: url('/fonts/Larsseit-Bold.otf') format('opentype');
  font-weight: 700;
  font-style: normal;
  font-display: swap;
}
@font-face {
  font-family: 'Larsseit';
  src: url('/fonts/Larsseit-ExtraBold.otf') format('opentype');
  font-weight: 800;
  font-style: normal;
  font-display: swap;
}
```

#### Type Scale

```css
--font-family: 'Larsseit', system-ui, -apple-system, sans-serif;

/* Size / Line Height */
--text-xs:   12px / 1.4;
--text-sm:   14px / 1.5;
--text-base: 16px / 1.5;
--text-lg:   18px / 1.4;
--text-xl:   20px / 1.3;
--text-2xl:  24px / 1.25;
--text-3xl:  30px / 1.2;
--text-4xl:  36px / 1.15;
--text-5xl:  48px / 1.1;
--text-6xl:  64px / 1.05;
```

#### Typographic Role Assignments

| Role | Size | Weight | Color |
|------|------|--------|-------|
| Page title | `2xl–3xl` | `700` | `text-primary` |
| Section header | `xl` | `600` | `text-primary` |
| Subsection header | `lg` | `600` | `text-primary` |
| Body text | `base` | `400` | `text-primary` |
| Helper/label | `sm` | `400` | `text-secondary` |
| Caption/meta | `xs` | `400` | `text-muted` |
| Button text | `sm` | `600` | varies |
| Table header | `xs` | `600` uppercase | `text-muted` |
| Table cell | `sm` | `400` | `text-primary` |
| Badge/chip label | `xs` | `600` | varies |
| KPI value | `3xl–4xl` | `700` | `text-primary` |
| KPI label | `xs` | `500` | `text-secondary` |
| Hero title | `5xl–6xl` | `800` | `text-primary` |

**Atome-aligned rule:** Headings use `ExtraBold (800)`. Body uses regular/medium. Labels and UI chrome use `Medium (500)`. Never use `Thin` or `LightItalic` in UI chrome — only in editorial/marketing copy.

---

### 1.4 Spacing System

8px base grid. All spacing values are multiples of 4px.

```css
--space-1:  4px
--space-2:  8px
--space-3:  12px
--space-4:  16px
--space-5:  20px
--space-6:  24px
--space-8:  32px
--space-10: 40px
--space-12: 48px
--space-16: 64px
--space-20: 80px
--space-24: 96px
```

**Page margins:**
- Desktop: `--space-8` (32px) horizontal padding per side
- Content max-width: `1280px`
- Sidebar width: `240px` (fixed)
- Content area: `calc(100% - 240px)` minus margins

---

### 1.5 Border, Radius, Shadow

```css
/* Border radius */
--radius-sm:   6px;    /* chips, badges, small inputs */
--radius-md:   10px;   /* buttons, cards, inputs */
--radius-lg:   14px;   /* panels, modals */
--radius-xl:   20px;   /* large surface blocks */
--radius-full: 9999px; /* pill buttons, avatar */

/* Borders */
--border-default: 1px solid var(--color-border);
--border-strong:  1px solid var(--color-border-strong);
--border-primary: 1px solid var(--color-primary-border);

/* Shadows (minimal, Atome-aligned) */
--shadow-sm:  0 1px 3px rgba(0, 0, 0, 0.4);
--shadow-md:  0 4px 16px rgba(0, 0, 0, 0.5);
--shadow-lg:  0 12px 40px rgba(0, 0, 0, 0.7);
--shadow-glow: 0 0 24px rgba(181, 227, 27, 0.15);  /* Spriteburst glow for primary CTA */
```

---

### 1.6 Motion / Animation Tokens

Use Framer Motion for all web transitions. Respect `prefers-reduced-motion`.

```js
export const motion = {
  duration: {
    instant: 0.08,
    fast:    0.15,
    base:    0.22,
    slow:    0.35,
  },
  ease: {
    standard:  [0.2, 0.8, 0.2, 1],
    decelerate:[0, 0, 0.2, 1],
    accelerate:[0.4, 0, 1, 1],
    sharp:     [0.4, 0, 0.6, 1],
  }
}
```

#### Required Motion Patterns

| Pattern | Config |
|---------|--------|
| Page enter | `opacity: 0→1, y: 12→0, duration: base` |
| Panel/drawer slide | `x: 40→0, opacity: 0→1, duration: base` |
| Modal enter | `scale: 0.96→1, opacity: 0→1, duration: fast` |
| Table row expand | `height: auto, opacity: 0→1, duration: fast` |
| Filter reveal | `height: 0→auto, opacity: 0→1, duration: base` |
| Toast | `y: 20→0, opacity: 0→1, duration: fast` |
| Tab switch | `x: ±16→0, opacity: 0→1, duration: fast` |
| Skeleton pulse | CSS `animate-pulse` only |

**Reduced motion rule:** All transitions fall back to opacity-only (no translate/scale) when `prefers-reduced-motion: reduce` is detected.

---

### 1.7 Component Library

All components use Tailwind CSS + shadcn/ui base, styled with the tokens above. The component set below is mandatory for bolt.new to implement.

#### Button

```
Variants:  primary | secondary | ghost | destructive | outline
Sizes:     sm (h-8) | md (h-10) | lg (h-12)
Primary:   bg=Spriteburst, text=text-inverse, hover=primary-hover, glow shadow on hover
Secondary: bg=surface-high, text=text-primary, border=border-default
Ghost:     transparent, text=text-secondary, hover=surface-alt background
Destructive: bg=destructive-muted, text=destructive, hover=border-destructive
Radius:    radius-md
Font:      14px / Larsseit 600
Icon+text: gap-2, icon-size=16px
Loading:   spinner replaces icon, text remains
Disabled:  opacity-40, no hover effect
```

#### Input / Textarea

```
Background: surface-alt
Border: border-default
Border-focus: border-primary (Spriteburst)
Text: text-primary
Placeholder: text-muted
Radius: radius-md
Height: 40px (single), auto (textarea)
Label: above field, text-sm text-secondary Larsseit 500
Error state: border-destructive + error message below in text-xs text-destructive
Helper text: text-xs text-muted below field
```

#### Table

```
Container: surface background, border-default, radius-lg
Header row: text-xs uppercase tracking-wide text-muted, border-bottom
Data rows: text-sm text-primary, border-bottom border-subtle
Row hover: surface-high background, transition duration-fast
Sticky header: yes, for tables > 10 rows
Row selection: primary-muted left border accent (4px)
Empty state: centered, 200px min height, icon + text + action
Loading state: skeleton rows (3–5), animate-pulse
Pagination: bottom, text-sm, prev/next + page count
```

#### Badge / Status Chip

```
Padding: 2px 8px
Radius: radius-full
Font: text-xs Larsseit 600 uppercase
Colors: from Status Badge Color table in §1.2
No icons unless explicitly spec'd per page
Inline with table data only — not as decorative standalone chips
```

#### Sidebar Navigation

```
Width: 240px fixed
Background: surface (#0A0A0A)
Border-right: border-default
Logo area: 56px height, Spriteburst logo or wordmark
Nav item: h-10, px-4, radius-md, text-sm Larsseit 500 text-secondary
Nav item active: bg=primary-muted, text=text-primary, left-border 2px Spriteburst
Nav item hover: bg=surface-alt
Section dividers: text-xs uppercase text-muted px-4 mt-6 mb-2
Collapse:  not required for MVP
```

#### Top Bar

```
Height: 56px
Background: surface
Border-bottom: border-default
Contents: page breadcrumb left | search shortcut center | notifications + avatar right
Avatar: 32px circle, text initials fallback
Notification bell: unread dot in Spriteburst
```

#### Modal / Sheet

```
Backdrop: color-overlay, blur(4px)
Panel: surface background, radius-xl, shadow-lg
Header: title text-lg 600 + close button top-right
Footer: action buttons right-aligned
Enter animation: modal enter pattern from §1.6
Max width: 480px (standard), 720px (wide form), 960px (detail view)
```

#### KPI Row (Recruiter / Admin dashboards)

```
Layout: horizontal flex, equal-width cells, border-right dividers
No floating cards — use a single bordered container divided into cells
Cell: min 160px, padding 24px
Value: text-3xl Larsseit 700 text-primary
Label: text-xs Larsseit 500 text-secondary uppercase
Delta indicator: text-xs colored arrow + value (green=up, red=down)
Background: surface-alt
Radius: radius-lg (outer container only)
```

#### Empty State

```
Layout: centered column, padding 48px
Icon: 48px monochrome, text-muted
Title: text-base Larsseit 600
Body: text-sm text-secondary
CTA button: primary variant
All three elements required — no empty state without a next action
```

#### Skeleton Loader

```
Background: surface-high
Animate: pulse (opacity 0.4 → 0.8 → 0.4)
Shape: match the element it represents (text bars, table rows, etc.)
Duration: show after 200ms delay — never flash skeleton for fast loads
```

---

### 1.8 Layout Architecture

#### App Shell (Authenticated)

```
┌─────────────────────────────────────────────────────┐
│  [TOPBAR 56px — breadcrumb / search / user]          │
├──────────────┬──────────────────────────────────────┤
│              │                                       │
│  SIDEBAR     │   CONTENT AREA                        │
│  240px       │   padding: 32px                       │
│  fixed       │   max-width: 1280px                   │
│              │                                       │
│  [logo]      │   Page Header Row                     │
│  [nav items] │   Command Row                         │
│  [divider]   │   Primary Data Region                 │
│  [nav items] │   Detail Region (when active)         │
│              │                                       │
└──────────────┴──────────────────────────────────────┘
```

#### Page Structure (Standard)

Every authenticated page follows this exact structure:
1. **Page Header Row** — title (text-2xl 700) + status context + primary/secondary CTAs right-aligned
2. **Command Row** — search input + filter controls + segment tabs + secondary actions
3. **Primary Data Region** — table or list (the data source of truth)
4. **Detail Panel** — appears right or below when a row is selected
5. **State Regions** — loading / empty / error handled inline

---

### 1.9 Icon System

Use **lucide-react** exclusively. No other icon library. Do not use emoji as icons in UI chrome.

Install: `npm install lucide-react`

#### Icon Size Standard
```
16px — inline with text (button icons, table badges, inline actions)
20px — standalone action buttons, nav items
24px — page-level add/create triggers
48px — empty state illustrations (monochrome, text-muted color)
```

#### Icon↔Action Mapping (Required — do not substitute)

| Action / Concept | Icon name |
|-----------------|-----------|
| Create new | `Plus` |
| Edit / modify | `Pencil` |
| Delete / remove | `Trash2` |
| Search | `Search` |
| Filter | `SlidersHorizontal` |
| Sort | `ArrowUpDown` |
| Back / return | `ArrowLeft` |
| Expand row | `ChevronDown` |
| Collapse row | `ChevronUp` |
| More actions (kebab) | `MoreHorizontal` |
| External link | `ExternalLink` |
| Close / dismiss | `X` |
| Success / verified | `CheckCircle2` |
| Warning / alert | `AlertTriangle` |
| Error / critical | `XCircle` |
| Info | `Info` |
| Role / demand | `Briefcase` |
| Talent / person | `User` |
| Company | `Building2` |
| Interview | `CalendarDays` |
| Offer / contract | `FileText` |
| Analytics | `BarChart3` |
| Search / semantic | `Sparkles` |
| AI / assistant | `Bot` |
| Shortlist | `ListChecks` |
| Notification bell | `Bell` |
| Settings | `Settings` |
| Logout | `LogOut` |
| Download / export | `Download` |
| Upload | `Upload` |
| Copy | `Copy` |
| Refresh / regenerate | `RefreshCw` |
| Score gauge (match) | `Target` |
| Rate / currency | `DollarSign` |
| Location | `MapPin` |
| Time / duration | `Clock` |
| Availability | `CalendarCheck` |
| Verified badge | `BadgeCheck` |
| Platform admin | `ShieldCheck` |
| Concierge | `UserSearch` |

---

### 1.10 Chart Library

Use **Recharts** for all analytics charts. It is React-native, composable, and requires no additional configuration beyond Tailwind color overrides.

Install: `npm install recharts`

#### Chart Theme Config (pass to all charts)

```tsx
const CHART_COLORS = {
  primary:     '#EFFE5E',   // Spriteburst — main data series
  secondary:   '#FFFFFF',   // secondary series
  warning:     '#F59E0B',
  info:        '#3B82F6',
  destructive: '#EF4444',
  muted:       '#52525B',
  grid:        '#27272A',   // CartesianGrid stroke
  axis:        '#52525B',   // XAxis / YAxis tick fill
}
```

#### Recharts Standard Config (apply to every chart)

```tsx
// Wrapper: always use ResponsiveContainer
<ResponsiveContainer width="100%" height={280}>

// Grid
<CartesianGrid strokeDasharray="3 3" stroke={CHART_COLORS.grid} vertical={false} />

// Axes
<XAxis tick={{ fill: CHART_COLORS.axis, fontSize: 12, fontFamily: 'Larsseit' }} axisLine={false} tickLine={false} />
<YAxis tick={{ fill: CHART_COLORS.axis, fontSize: 12, fontFamily: 'Larsseit' }} axisLine={false} tickLine={false} />

// Tooltip (always custom)
<Tooltip
  contentStyle={{ background: '#1A1A1A', border: '1px solid #27272A', borderRadius: 10 }}
  labelStyle={{ color: '#FFFFFF', fontFamily: 'Larsseit', fontWeight: 600 }}
  itemStyle={{ color: '#A1A1AA', fontFamily: 'Larsseit' }}
/>

// Legend (when needed)
<Legend wrapperStyle={{ fontFamily: 'Larsseit', fontSize: 12, color: '#A1A1AA' }} />
```

#### Chart Type Assignments

| Chart | Type | Primary fill |
|-------|------|-------------|
| Hiring Velocity | `LineChart` | Spriteburst line |
| Pipeline Conversion | `BarChart` horizontal | Spriteburst fill |
| Top Skills in Demand | `BarChart` horizontal | Spriteburst fill |
| Role Aging | `BarChart` vertical | warning fill for 30+ buckets |
| Talent Growth | `AreaChart` | Spriteburst area, 0.15 opacity fill |
| Skill Distribution | `BarChart` horizontal | Spriteburst + info grouped |
| Supply-Demand Gap | `BarChart` grouped | primary + destructive |
| Time-to-Hire Distribution | `BarChart` histogram | Spriteburst fill |
| Pricing Trends | `LineChart` | Spriteburst primary, info secondary |

**Rules:**
- Never use pie/donut charts — use bar or funnel instead
- All chart containers have a `text-base Larsseit 600 text-primary` title above
- All charts: min height 240px, max height 360px for summary dashboards
- Empty chart state: show axes with "No data for this period" centered

---

### 1.11 Tailwind Config Snippet

Add these token extensions to `tailwind.config.ts`. This is required before any component generation.

```ts
// tailwind.config.ts (extend only — do not replace full config)
import type { Config } from 'tailwindcss'

const config: Config = {
  content: ['./app/**/*.{ts,tsx}', './components/**/*.{ts,tsx}'],
  theme: {
    extend: {
      fontFamily: {
        sans: ['Larsseit', 'system-ui', '-apple-system', 'sans-serif'],
      },
      colors: {
        bg:        '#000000',
        surface:   '#0A0A0A',
        'surface-alt':  '#1A1A1A',
        'surface-high': '#222222',
        primary:        '#EFFE5E',
        'primary-hover':'#BBB906',
        'primary-muted':'rgba(181,227,27,0.12)',
        border:         '#27272A',
        'border-strong':'#3F3F46',
        'text-primary': '#FFFFFF',
        'text-secondary':'#A1A1AA',
        'text-muted':   '#52525B',
        'text-inverse': '#000000',
      },
      borderRadius: {
        sm:   '6px',
        md:   '10px',
        lg:   '14px',
        xl:   '20px',
        full: '9999px',
      },
      boxShadow: {
        sm:   '0 1px 3px rgba(0,0,0,0.4)',
        md:   '0 4px 16px rgba(0,0,0,0.5)',
        lg:   '0 12px 40px rgba(0,0,0,0.7)',
        glow: '0 0 24px rgba(181,227,27,0.15)',
      },
    },
  },
}
export default config
```

---

### 1.12 globals.css Starter

This block belongs at the top of `apps/web/app/globals.css`. Merge with existing — do not replace.

```css
/* ─── Larsseit Font Faces ─── */
@font-face { font-family:'Larsseit'; src:url('/fonts/Larsseit-Light.otf') format('opentype'); font-weight:300; font-style:normal; font-display:swap; }
@font-face { font-family:'Larsseit'; src:url('/fonts/Larsseit.otf') format('opentype'); font-weight:400; font-style:normal; font-display:swap; }
@font-face { font-family:'Larsseit'; src:url('/fonts/Larsseit-Medium.otf') format('opentype'); font-weight:500; font-style:normal; font-display:swap; }
@font-face { font-family:'Larsseit'; src:url('/fonts/Larsseit-Bold.otf') format('opentype'); font-weight:700; font-style:normal; font-display:swap; }
@font-face { font-family:'Larsseit'; src:url('/fonts/Larsseit-ExtraBold.otf') format('opentype'); font-weight:800; font-style:normal; font-display:swap; }

/* ─── CSS Design Tokens ─── */
:root {
  --color-bg:            #000000;
  --color-surface:       #0A0A0A;
  --color-surface-alt:   #1A1A1A;
  --color-surface-high:  #222222;
  --color-overlay:       rgba(0,0,0,0.72);

  --color-primary:         #EFFE5E;
  --color-primary-hover:   #BBB906;
  --color-primary-muted:   rgba(181,227,27,0.12);
  --color-primary-border:  rgba(181,227,27,0.30);

  --color-text-primary:    #FFFFFF;
  --color-text-secondary:  #A1A1AA;
  --color-text-muted:      #52525B;
  --color-text-inverse:    #000000;

  --color-border:          #27272A;
  --color-border-subtle:   #1F1F22;
  --color-border-strong:   #3F3F46;

  --color-success:         #22C55E;
  --color-success-muted:   rgba(34,197,94,0.12);
  --color-warning:         #F59E0B;
  --color-warning-muted:   rgba(245,158,11,0.12);
  --color-destructive:     #EF4444;
  --color-destructive-muted:rgba(239,68,68,0.12);
  --color-info:            #3B82F6;
  --color-info-muted:      rgba(59,130,246,0.12);

  --radius-sm:   6px;
  --radius-md:   10px;
  --radius-lg:   14px;
  --radius-xl:   20px;
  --radius-full: 9999px;

  --shadow-sm:  0 1px 3px rgba(0,0,0,0.4);
  --shadow-md:  0 4px 16px rgba(0,0,0,0.5);
  --shadow-lg:  0 12px 40px rgba(0,0,0,0.7);
  --shadow-glow:0 0 24px rgba(181,227,27,0.15);
}

html, body { background: var(--color-bg); color: var(--color-text-primary); font-family: 'Larsseit', system-ui, sans-serif; }
*, *::before, *::after { box-sizing: border-box; }
```

**Font file deployment:** Copy all `.otf` files from `font/Larsseit-Sans-Serif-Font-Family/Larsseit/Larsseit/` into `apps/web/public/fonts/` before running bolt output.

---

### 1.13 Score Breakdown Component

The AI matching engine scores candidates on 7 factors. This component renders those scores anywhere a match explanation is needed (Shortlist tab, Candidate Profile Modal, Search results).

#### Factor Weights (from SOW — these are the exact weights)

| Factor | Weight | Field name |
|--------|--------|-----------|
| Skill match | 35% | `skillMatch` |
| Experience fit | 20% | `experienceFit` |
| Availability | 10% | `availability` |
| Pricing fit | 10% | `pricingFit` |
| Location match | 10% | `locationMatch` |
| Cultural values fit | 10% | `culturalFit` |
| Past placement feedback | 5% | `feedbackScore` |

#### Rendering Spec

```tsx
interface ScoreBreakdown {
  overall: number       // 0–100
  skillMatch: number    // 0–100
  experienceFit: number
  availability: number
  pricingFit: number
  locationMatch: number
  culturalFit: number
  feedbackScore: number
  explanation?: string  // AI-generated text explanation
}
```

**Full breakdown (Candidate Profile Modal header):**
```
Layout: 7 horizontal bars stacked vertically
Each bar:
  - Label: factor name + weight (text-xs text-muted)
  - Bar track: surface-high, radius-full, h-2
  - Bar fill: Spriteburst, animated width on mount (duration 0.6s decelerate)
  - Value: text-xs text-secondary right-aligned

Overall score: large arc gauge above bars
  - Arc: SVG, 180° sweep, Spriteburst stroke on surface-high track
  - Value: text-4xl ExtraBold Spriteburst, centered in arc
  - Label: "Match Score" text-xs text-muted below value

AI explanation (when present):
  - Below bars, text-sm text-secondary, italic
  - Prefixed with Bot icon
```

**Compact breakdown (Shortlist table row expand):**
```
Layout: horizontal flex, 7 mini bars with tooltips
Each: 56px wide, h-1.5 bar, factor label on hover tooltip
Overall: numeric badge left (Spriteburst bg, text-inverse, text-sm 700, radius-full px-2)
```

---

### 1.14 Notification Center

Triggered by the `Bell` icon in the TopBar. Renders as a slide-in panel from the right edge of the TopBar (not a full Sheet — partial overlay, 360px wide).

#### Panel Spec

```
Width: 360px
Position: absolute top-[56px] right-0
Background: surface (#0A0A0A)
Border: border-default, radius-lg (bottom corners only)
Shadow: shadow-lg
Max height: 480px, overflow-y scroll
Z-index: 50

Header (sticky within panel):
  Title: "Notifications" text-base 600
  Action: "Mark all read" — ghost text-sm right-aligned → markAllNotificationsRead mutation

Notification item:
  Height: auto (min 60px), padding 16px
  Unread: left border 2px Spriteburst + slightly lighter background
  Read: no left border, surface background
  Content: icon (20px, colored by type) + title (text-sm 600) + body (text-sm text-secondary) + timestamp (text-xs text-muted)
  Click: navigate to related entity, mark as read

Empty state:
  "All caught up. No new notifications." — centered, padding 48px
```

#### Notification Types

| Type | Icon | Color | Body pattern |
|------|------|-------|-------------|
| `MATCH_GENERATED` | `Sparkles` | primary | "AI found [N] candidates for [Role Title]" |
| `INTERVIEW_SCHEDULED` | `CalendarDays` | info | "Interview with [Name] set for [Date]" |
| `OFFER_ACCEPTED` | `CheckCircle2` | success | "[Name] accepted your offer for [Role]" |
| `OFFER_DECLINED` | `XCircle` | destructive | "[Name] declined your offer for [Role]" |
| `DEMAND_APPROVED` | `BadgeCheck` | success | "Your role '[Title]' has been approved" |
| `DEMAND_REJECTED` | `AlertTriangle` | warning | "Changes requested for '[Title]'" |
| `VERIFICATION_COMPLETE` | `ShieldCheck` | success | "[Name]'s profile has been verified" |
| `SYSTEM_ALERT` | `Info` | info | Platform system message |

---

### 1.15 Responsive Breakpoints

The app is desktop-first but auth pages and public pages must be fully responsive. Dashboard pages require readable tablet layout (1024px). Mobile web is not a priority — Expo handles mobile.

#### Breakpoint Definitions

```
sm:  640px   — auth form full-width stacking
md:  768px   — sidebar collapses to icon-only rail
lg:  1024px  — minimum for full dashboard experience
xl:  1280px  — content max-width cap
2xl: 1536px  — no special treatment
```

#### Responsive Rules per Surface

**Public / Auth pages (`/`, `/login`, `/register`, etc.):**
```
< 640px: single column, form full width, no brand panel
640px–1023px: single column centered panel, 480px max-width
≥ 1024px: two-column (brand panel left, form right)
```

**Dashboard (authenticated) pages:**
```
< 768px: sidebar hidden (hamburger menu trigger), content full width — not a design priority
768px–1023px: sidebar collapses to 56px icon-only rail, content expands
≥ 1024px: full 240px sidebar + content area

Table responsiveness:
- < 900px: hide non-essential columns (Budget Range, Posted Date)
- < 768px: collapse to card-style rows (Candidate name + score + single action)
```

**KPI Row:**
```
≥ 1024px: all cells in one row
768px–1023px: 2x2 grid
< 768px: single column stack
```

---

### 1.16 Toast Notification System

All user-feedback toasts use a fixed toast region. Use `sonner` library (shadcn/ui's preferred toast).

Install: `npm install sonner`

```
Position: bottom-right
Max visible: 3 (older ones auto-dismiss)
Duration: 4000ms (success), 6000ms (error — requires manual dismiss), 3000ms (info)
```

#### Toast Variants

```
Success: left border Spriteburst | icon CheckCircle2 primary | title text-primary | body text-secondary
Error:   left border destructive | icon XCircle destructive | title text-primary
Warning: left border warning     | icon AlertTriangle warning
Info:    left border info        | icon Info info
```

#### Usage Pattern (bolt should follow this pattern)

```tsx
import { toast } from 'sonner'

// Success
toast.success('Role published.', {
  description: 'AI is generating your shortlist — check back in a moment.'
})

// Error
toast.error('Role could not be saved.', {
  description: 'Check required fields and try again.'
})

// Loading → resolved (for mutations)
const id = toast.loading('Publishing role...')
// on success:
toast.success('Role published.', { id })
// on error:
toast.error('Could not publish.', { id })
```

---

### 1.17 Sidebar Navigation — Exact Items

The sidebar spec in §1.7 defines the visual style. This section defines the exact nav items, icons, routes, and section groupings for each role surface.

#### Recruiter Sidebar (`(dashboard)` layout)

```
┌──────────────────────────┐
│  [Logo wordmark]          │  h-14, Spriteburst color, px-5
├──────────────────────────┤
│  SECTION: "Workspace"     │  text-xs text-muted uppercase, px-4, mt-6 mb-2
│  ○ Dashboard              │  icon: LayoutDashboard → /dashboard
│  ○ Roles                  │  icon: Briefcase       → /dashboard/roles
│  ○ Shortlists             │  icon: ListChecks      → /dashboard/shortlists
│  ○ Search                 │  icon: Sparkles        → /dashboard/search
├──────────────────────────┤
│  SECTION: "Pipeline"      │
│  ○ Interviews             │  icon: CalendarDays    → /dashboard/interviews
│  ○ Offers                 │  icon: FileText        → /dashboard/offers
├──────────────────────────┤
│  SECTION: "Insights"      │
│  ○ Analytics              │  icon: BarChart3       → /dashboard/analytics
├──────────────────────────┤
│  [BOTTOM — pinned]        │
│  ○ Settings               │  icon: Settings        → /settings
│  ○ Sign Out               │  icon: LogOut          → signOut() call
└──────────────────────────┘
```

**Active state rule:** The nav item whose href matches `usePathname()` receives the active treatment (Spriteburst left border + primary-muted background). For nested routes (e.g. `/dashboard/roles/new`), the parent item `/dashboard/roles` is active.

#### Admin Sidebar (`(admin)` layout)

```
┌──────────────────────────┐
│  [Logo wordmark]          │  h-14, Spriteburst color, px-5
│  [ADMIN badge]            │  text-xs Spriteburst bg text-inverse px-2 rounded-sm ml-2
├──────────────────────────┤
│  SECTION: "Overview"      │
│  ○ Dashboard              │  icon: LayoutDashboard → /admin
├──────────────────────────┤
│  SECTION: "Governance"    │
│  ○ Users                  │  icon: User            → /admin/users
│  ○ Verification           │  icon: ShieldCheck     → /admin/verification
│  ○ Approvals              │  icon: BadgeCheck      → /admin/approvals
│  ○ Concierge              │  icon: UserSearch      → /admin/concierge
├──────────────────────────┤
│  SECTION: "Platform"      │
│  ○ Companies              │  icon: Building2       → /admin/companies
│  ○ Analytics              │  icon: BarChart3       → /admin/analytics
├──────────────────────────┤
│  [BOTTOM — pinned]        │
│  ○ Settings               │  icon: Settings        → /settings
│  ○ Sign Out               │  icon: LogOut          → signOut() call
└──────────────────────────┘
```

**Queue badge:** Verification and Approvals items display a count badge (number of pending items) to the right of the label when count > 0. Badge style: Spriteburst bg, text-inverse, text-xs, rounded-full, min-w-[20px], centered.

---

### 1.18 Additional Components

These components extend §1.7 and are required wherever their use is specified in Part 2.

#### File Upload

```
Use case: Verification document upload (admin/verification detail), resume upload (talent — mobile-only, not needed web)
Purpose: Single or multi-file drag-and-drop upload zone

Spec:
Container: dashed border (border-border-strong), border-dash 4px, radius-lg
Background: surface-alt
Center content: Upload icon (48px, text-muted) + title + helper text
Accepted types label: text-xs text-muted below ("PDF, JPG, PNG — max 10MB")
Drag-over state: border-primary + primary-muted background
Click: opens native file picker

Selected file display:
  Each file shown as a row below drop zone:
  - File icon (FileText, 16px) + filename (text-sm) + size (text-xs text-muted) + remove × button
  - Upload progress: Spriteburst progress bar on pending files
  - Uploaded: CheckCircle2 (success) + green filename text

Error state (file too large / wrong type): XCircle (destructive) + error text below filename row
```

#### Date Picker

```
Use case: Role start date, interview schedule date, offer start/end dates
Implementation: Use shadcn/ui Calendar component, styled for dark theme

Input trigger: standard Input spec (§1.7) + CalendarDays icon trailing
Calendar popover:
  Background: surface-alt
  Border: border-default, radius-lg
  Shadow: shadow-md
  Header: month/year navigation with ChevronLeft/ChevronRight
  Day cell: text-sm, h-9 w-9, hover=surface-high, radius-md
  Selected day: bg=primary (Spriteburst) text=text-inverse rounded-full
  Today: underline or subtle ring, NOT filled
  Out-of-month days: text-muted, opacity-40
  Disabled past dates (where required): opacity-30, no hover

Tailwind override (add to globals.css):
  .rdp-button_reset { color: var(--color-text-primary); }
  .rdp-day_selected { background: var(--color-primary); color: var(--color-text-inverse); }
  .rdp { background: var(--color-surface-alt); border: 1px solid var(--color-border); border-radius: var(--radius-lg); }
```

#### Dual Range Slider

```
Use case: Hourly rate filter in Search page, budget range in role creation
Implementation: Radix UI Slider (shadcn/ui base) — two thumbs

Track: surface-high, h-2, radius-full
Range fill: Spriteburst, between the two thumbs
Thumb: 16px circle, bg=surface border-2 border-primary, shadow-sm, focus-ring=primary
Value labels: text-xs text-muted above or below each thumb, update live
Min/max labels: text-xs text-muted at both ends of track
```

#### Pagination

```
Use case: All data tables — roles, users, interviews, offers, search results
Placement: Bottom of table container, 40px height, px-4

Layout: flex justify-between items-center

Left: "Showing 1–20 of 143 results" — text-sm text-muted
Center: page number buttons (for small datasets) OR prev/next only (for cursor-based)
Right: "20 per page" select (optional) — ghost dropdown

Page buttons:
  Current: bg=primary text=text-inverse w-8 h-8 rounded-md
  Other: ghost, text-secondary, hover=surface-alt
  Ellipsis: text-muted, non-interactive

Prev/Next buttons:
  ChevronLeft / ChevronRight icon + text
  Disabled when at boundary: opacity-40, cursor-not-allowed

Cursor-based (used by default): only Prev + page info + Next — no individual page buttons
```

#### Breadcrumb

```
Use case: TopBar — shows current route context
Placement: Left side of TopBar, after logo (on desktop)

Pattern: [Section] / [Page] / [Entity title if detail page]
Examples:
  Roles / Role Demands
  Roles / React Developer → /dashboard/roles → specific demand title
  Admin / Verification / Pending

Style:
  text-sm Larsseit 500
  Sections (not last): text-muted, hover=text-secondary, linked
  Last segment: text-primary, not linked
  Separator: "/" text-muted mx-2
  Max 3 segments — truncate entity title at 32 chars with ellipsis

Implementation: derive from usePathname() + demand/interview title from query cache
```

#### Command Palette

```
Use case: Global keyboard shortcut Cmd+K (Mac) / Ctrl+K (Win) — quick navigation + search
Trigger: keyboard shortcut, OR clicking the search hint in the TopBar center

Modal style:
  Width: 560px, centered on screen
  Background: surface-alt
  Border: border-strong
  Radius: radius-xl
  Shadow: shadow-lg
  Backdrop: overlay blur(4px)

Search input:
  Full width, text-base, no border (borderless, prominent)
  Placeholder: "Search roles, talent, shortcuts..."
  Icon: Search 20px text-muted left

Results list (below input):
  Groups with section headers (text-xs uppercase text-muted)
  Sections:
    "Quick Actions" — static: Create Role, Search Talent, Schedule Interview
    "Recent Roles" — last 5 viewed demands
    "Navigation" — all sidebar nav items

Result item: h-10 px-3 radius-md
  Icon (20px text-secondary) + label (text-sm text-primary) + shortcut hint right (text-xs text-muted)
  Hover/focus: bg=surface-high
  Selected: bg=primary-muted

Keyboard nav: ↑↓ to move, Enter to select, Esc to dismiss
Hook: useEffect on keydown for Cmd/Ctrl+K to open
State: managed with zustand or useState in a layout-level context
```

---

### 1.19 Accessibility

All bolt-generated components must follow these rules. Bolt should be instructed explicitly to include them.

#### Focus Ring

```css
/* Add to globals.css */
:focus-visible {
  outline: 2px solid var(--color-primary);
  outline-offset: 2px;
  border-radius: var(--radius-sm);
}
/* Remove default outline for non-keyboard focus */
:focus:not(:focus-visible) {
  outline: none;
}
```

All interactive elements (buttons, inputs, links, table rows, nav items) must show the Spriteburst focus ring on keyboard navigation. Mouse clicks must not show it.

#### ARIA Requirements

| Component | Required ARIA |
|-----------|-------------|
| Status badge | `role="status"` or `aria-label="Status: [value]"` |
| Score gauge | `role="meter"` `aria-valuenow` `aria-valuemin=0` `aria-valuemax=100` `aria-label="Match score"` |
| Table with sort | sortable column headers: `aria-sort="ascending"` or `"descending"` |
| Modal | `role="dialog"` `aria-modal="true"` `aria-labelledby` pointing to header |
| Sidebar nav | `<nav aria-label="Main navigation">` |
| TopBar | `<header role="banner">` |
| Page main | `<main>` with `id="main-content"` |
| Empty state | `aria-live="polite"` on the container |
| Loading skeleton | `aria-busy="true"` on the skeleton container, `aria-label="Loading"` |
| Toast region | `aria-live="polite"` (sonner handles this automatically) |
| File upload | `<input type="file" />` with visible label, `aria-describedby` pointing to file type helper |

#### Keyboard Shortcuts

| Shortcut | Action |
|----------|--------|
| `Cmd/Ctrl + K` | Open command palette |
| `Escape` | Close active modal, sheet, or command palette |
| `Enter` on table row | Navigate to detail / expand row |
| `Tab` | Standard focus traversal through all interactive elements |
| `Space` on checkbox | Toggle checkbox selection |
| `Arrow keys` | Navigate command palette results; navigate date picker calendar |

#### Skip Link

Add at the very top of `layout.tsx`, before sidebar and topbar:

```tsx
<a
  href="#main-content"
  className="sr-only focus:not-sr-only focus:absolute focus:z-50 focus:top-4 focus:left-4 focus:px-4 focus:py-2 focus:bg-primary focus:text-text-inverse focus:rounded-md focus:text-sm focus:font-medium"
>
  Skip to main content
</a>
```

---

### 1.20 Form Validation Patterns

All forms use **Zod** for schema validation and **react-hook-form** with `@hookform/resolvers/zod` for integration. Bolt should generate these schemas — do not use uncontrolled forms or custom validation logic.

Install: `npm install zod react-hook-form @hookform/resolvers`

#### Key Form Schemas (copy into form files)

```tsx
import { z } from 'zod'

// ─── Auth ───────────────────────────────────────────────
export const loginSchema = z.object({
  email:    z.string().email('Enter a valid email address.'),
  password: z.string().min(1, 'Password is required.'),
})

export const registerSchema = z.object({
  firstName: z.string().min(1, 'First name is required.'),
  lastName:  z.string().min(1, 'Last name is required.'),
  email:     z.string().email('Enter a valid email address.'),
  password:  z.string()
    .min(8, 'Password must be at least 8 characters.')
    .regex(/[A-Z]/, 'Include at least one uppercase letter.')
    .regex(/[0-9]/, 'Include at least one number.'),
  confirmPassword: z.string(),
}).refine(
  (data) => data.password === data.confirmPassword,
  { message: 'Passwords do not match.', path: ['confirmPassword'] }
)

export const forgotPasswordSchema = z.object({
  email: z.string().email('Enter a valid email address.'),
})

// ─── Demand (Create Role) ────────────────────────────────
export const createDemandSchema = z.object({
  title:            z.string().min(3, 'Role title must be at least 3 characters.').max(120),
  companyId:        z.string().min(1, 'Select a company.'),
  experienceLevel:  z.enum(['JUNIOR','MID','SENIOR','LEAD','EXECUTIVE'], { errorMap: () => ({ message: 'Select an experience level.' }) }),
  location:         z.string().optional(),
  remotePolicy:     z.enum(['ONSITE','HYBRID','REMOTE']),
  requiredSkillIds: z.array(z.string()).min(1, 'Add at least one required skill.'),
  requirements:     z.string().max(500).optional(),
  startDate:        z.string().optional(),
  contractDuration: z.string().optional(),
  budgetMin:        z.number().positive().optional(),
  budgetMax:        z.number().positive().optional(),
  currency:         z.string().default('USD'),
  rawNotes:         z.string().optional(),
}).refine(
  (data) => !data.budgetMin || !data.budgetMax || data.budgetMax >= data.budgetMin,
  { message: 'Budget max must be greater than budget min.', path: ['budgetMax'] }
)

// ─── Schedule Interview ──────────────────────────────────
export const scheduleInterviewSchema = z.object({
  candidateId: z.string().min(1, 'Select a candidate.'),
  demandId:    z.string().min(1, 'Select a role.'),
  scheduledAt: z.string().min(1, 'Pick a date and time.'),
  duration:    z.number().int().positive().default(60),
  meetingUrl:  z.string().url('Enter a valid URL.').optional().or(z.literal('')),
  notes:       z.string().max(500).optional(),
})

// ─── Offer ───────────────────────────────────────────────
export const createOfferSchema = z.object({
  candidateId: z.string().min(1, 'Select a candidate.'),
  demandId:    z.string().min(1, 'Select a role.'),
  hourlyRate:  z.number().positive('Enter a valid hourly rate.'),
  currency:    z.string().default('USD'),
  startDate:   z.string().min(1, 'Start date is required.'),
  endDate:     z.string().optional(),
  terms:       z.string().max(1000).optional(),
}).refine(
  (data) => !data.endDate || data.endDate > data.startDate,
  { message: 'End date must be after start date.', path: ['endDate'] }
)

// ─── Settings: Profile ───────────────────────────────────
export const updateProfileSchema = z.object({
  firstName: z.string().min(1, 'First name is required.'),
  lastName:  z.string().min(1, 'Last name is required.'),
  jobTitle:  z.string().max(120).optional(),
})

// ─── Settings: Change Password ───────────────────────────
export const changePasswordSchema = z.object({
  currentPassword: z.string().min(1, 'Current password is required.'),
  newPassword:     z.string()
    .min(8, 'New password must be at least 8 characters.')
    .regex(/[A-Z]/, 'Include at least one uppercase letter.')
    .regex(/[0-9]/, 'Include at least one number.'),
  confirmPassword: z.string(),
}).refine(
  (data) => data.newPassword === data.confirmPassword,
  { message: 'Passwords do not match.', path: ['confirmPassword'] }
)
```

#### react-hook-form Usage Pattern

```tsx
import { useForm } from 'react-hook-form'
import { zodResolver }  from '@hookform/resolvers/zod'
import { z } from 'zod'

type FormValues = z.infer<typeof createDemandSchema>

const form = useForm<FormValues>({
  resolver: zodResolver(createDemandSchema),
  defaultValues: { currency: 'USD', remotePolicy: 'HYBRID' },
})

// Field error display (below each input):
{form.formState.errors.title && (
  <p className="mt-1 text-xs text-destructive">{form.formState.errors.title.message}</p>
)}
```

---

### 1.21 Status Machine Flows

Every entity in the platform has a strict lifecycle. Bolt must render exactly the right action buttons for each status — never a button that would trigger an invalid transition.

#### Demand Status Flow

```
DRAFT ──[Publish Role]──► PENDING_APPROVAL ──[Admin Approves]──► ACTIVE ──[Pause]──► PAUSED ──[Resume]──► ACTIVE
                                                                    │                                        │
                                                         [Mark Filled]                                [Cancel]
                                                                    ▼                                        ▼
                                                                 FILLED                                CANCELLED
```

| Current Status | Button(s) shown on Role Detail | Mutation triggered | Next Status |
|----------------|-------------------------------|-------------------|-------------|
| `DRAFT` | "Publish Role" (primary) | `updateDemand(status: PENDING_APPROVAL)` | `PENDING_APPROVAL` |
| `PENDING_APPROVAL` | None — awaiting admin (show info banner: "Under review") | — | — |
| `ACTIVE` | "Pause" (ghost) · "Mark Filled" (success) · "Cancel" (destructive ghost) | `pauseDemand` / `fillDemand` / `cancelDemand` | `PAUSED` / `FILLED` / `CANCELLED` |
| `PAUSED` | "Resume" (ghost) · "Cancel" (destructive ghost) | `updateDemand(status: ACTIVE)` / `cancelDemand` | `ACTIVE` / `CANCELLED` |
| `FILLED` | None — archive badge, read-only | — | terminal |
| `CANCELLED` | None — archive badge, read-only | — | terminal |

**Status badge colors:**
- `DRAFT` → `bg-[#27272A] text-[#A1A1AA]`
- `PENDING_APPROVAL` → `bg-amber-950 text-amber-400` (`#F59E0B`)
- `ACTIVE` → `bg-green-950 text-green-400` (`#22C55E`)
- `PAUSED` → `bg-blue-950 text-blue-400` (`#3B82F6`)
- `FILLED` → `bg-[#1a1c00] text-[#EFFE5E]`
- `CANCELLED` → `bg-red-950 text-red-400` (`#EF4444`)

---

#### Shortlist Candidate Status Flow

```
AI_SUGGESTED ──[auto on generation]──► RECRUITER_REVIEWED ──[Request Interview]──► SHORTLISTED
                                                │
                                           [Reject]
                                                ▼
                                           REJECTED ──[Restore]──► RECRUITER_REVIEWED
```

| Current Status | Button(s) shown per row | Mutation | Next Status |
|----------------|------------------------|---------|-------------|
| `AI_SUGGESTED` | Row is highlighted as "new" — "Review" is passive (clicking the row triggers `reviewCandidate`) | `reviewCandidate` | `RECRUITER_REVIEWED` |
| `RECRUITER_REVIEWED` | "Request Interview" (primary inline) · "Reject" (ghost icon) | `scheduleInterview` / `rejectCandidate` | `SHORTLISTED` / `REJECTED` |
| `SHORTLISTED` | "Request Interview" (primary, re-requestable) · "Reject" (ghost) | `scheduleInterview` / `rejectCandidate` | unchanged / `REJECTED` |
| `REJECTED` | "Restore" (ghost, small) | `reviewCandidate` | `RECRUITER_REVIEWED` |

**Status badge colors:**
- `AI_SUGGESTED` → `bg-blue-950 text-blue-400` + Sparkles icon (new/AI)
- `RECRUITER_REVIEWED` → `bg-amber-950 text-amber-400`
- `SHORTLISTED` → `bg-[#1a1c00] text-[#EFFE5E]`
- `REJECTED` → `bg-[#27272A] text-[#52525B]` (muted — de-emphasize)

---

#### Interview Status Flow

```
SCHEDULED ──[Complete]──► COMPLETED ──[Submit Feedback]──► (feedback stored, status stays COMPLETED)
     │
     ├──[Cancel]──► CANCELLED
     └──[No-Show]──► NO_SHOW ──[Reschedule]──► SCHEDULED
```

| Current Status | Button(s) shown | Mutation | Next Status |
|----------------|----------------|---------|-------------|
| `SCHEDULED` | "Complete Interview" (primary) · "Reschedule" (ghost) · "Cancel" (destructive ghost) | `updateInterview(status: COMPLETED)` / `rescheduleInterview` / `cancelInterview` | `COMPLETED` / `SCHEDULED` (new time) / `CANCELLED` |
| `COMPLETED` | "Submit Feedback" (primary, if `feedback == null`) — else feedback shown read-only | `submitFeedback` | no status change |
| `CANCELLED` | None — read-only, terminal | — | terminal |
| `NO_SHOW` | "Reschedule" (ghost) | `rescheduleInterview` | `SCHEDULED` |

**Status badge colors:**
- `SCHEDULED` → `bg-blue-950 text-blue-400`
- `COMPLETED` → `bg-green-950 text-green-400`
- `CANCELLED` → `bg-[#27272A] text-[#52525B]`
- `NO_SHOW` → `bg-amber-950 text-amber-400`

---

#### Offer Status Flow

```
DRAFT ──[Send Offer]──► SENT ──[candidate accepts]──► ACCEPTED
                          │
                          ├──[candidate declines]──► DECLINED
                          └──[Withdraw]──► WITHDRAWN
```

| Current Status | Button(s) shown | Mutation | Next Status |
|----------------|----------------|---------|-------------|
| `DRAFT` | "Send Offer" (primary) · "Delete" (destructive ghost) | `sendOffer` | `SENT` |
| `SENT` | "Withdraw" (destructive ghost) — no other actions, awaiting candidate | `withdrawOffer` | `WITHDRAWN` |
| `ACCEPTED` | None — terminal success, show green Accepted banner | — | terminal |
| `DECLINED` | None — terminal, show muted Declined badge | — | terminal |
| `WITHDRAWN` | None — terminal, archive badge | — | terminal |

**Status badge colors:**
- `DRAFT` → `bg-[#27272A] text-[#A1A1AA]`
- `SENT` → `bg-blue-950 text-blue-400`
- `ACCEPTED` → `bg-green-950 text-green-400`
- `DECLINED` → `bg-red-950 text-red-400`
- `WITHDRAWN` → `bg-[#27272A] text-[#52525B]`

**Aging rule:** If `SENT` and `(now - sentAt) > 72 hours` → show `Clock` icon in `text-amber-400` next to badge. Tooltip: "No response in 3+ days."

---

### 1.22 KPI Row Component Spec

The `KPIRow` component appears on four pages: `/dashboard`, `/dashboard/analytics`, `/admin`, `/admin/analytics`. It is a **single horizontal container with internal dividers** — not floating cards, not a CSS grid of cards.

#### Visual Spec

```
Container:   bg-[#0A0A0A] border border-[#27272A] rounded-[4px] w-full
Layout:      flex flex-row, children each flex-1, separated by 1px dividers (bg-[#27272A])
Cell:        px-6 py-5 flex flex-col gap-1
```

Cell internals (top to bottom):
```
<label>   — text-[11px] uppercase tracking-widest text-[#A1A1AA] font-medium
<value>   — text-2xl font-bold; text-[#EFFE5E] for accent cells, text-white for secondary
<trend>   — (optional) flex items-center gap-1 text-xs
              ↑ green: TrendingUp icon + "+N vs last period"
              ↓ red:   TrendingDown icon + "-N vs last period"
```

#### TypeScript Props

```typescript
interface KPITrend {
  delta: number           // absolute or percent delta
  period: string          // e.g. "vs last 30 days"
  isPositive: boolean     // true = green up arrow, false = red down arrow
}

interface KPICell {
  label: string
  value: string | number
  format?: 'number' | 'percent' | 'currency' | 'days'
  trend?: KPITrend
  accent?: boolean        // true = Spriteburst value color
  alert?: boolean         // true = Spriteburst + pulse dot (for queue counts > 0)
}

interface KPIRowProps {
  cells: KPICell[]
  loading?: boolean
}
```

Skeleton state (`loading=true`): replace every value with `<div className="w-16 h-6 bg-[#222222] animate-pulse rounded" />`.

#### Page KPI Definitions

**`/dashboard` — Recruiter Dashboard (6 cells):**

| # | label | value field | accent | alert |
|---|-------|------------|--------|-------|
| 1 | Roles Posted | `stats.totalDemands` | ✓ | — |
| 2 | Shortlisted | `stats.totalShortlisted` | — | — |
| 3 | Interviews | `stats.totalInterviews` | — | — |
| 4 | Offers Accepted | `stats.offersAccepted` | — | — |
| 5 | Active Roles | `stats.activeRoles` | — | — |
| 6 | Avg. Days to Hire | `stats.avgDaysToHire` | — | — |

**`/admin` — Admin Dashboard (6 cells):**

| # | label | value field | accent | alert |
|---|-------|------------|--------|-------|
| 1 | Total Users | `stats.totalUsers` | ✓ | — |
| 2 | Active Talent | `stats.activeTalent` | — | — |
| 3 | Active Demands | `stats.activeDemands` | — | — |
| 4 | Placements MTD | `stats.placementsThisMonth` | — | — |
| 5 | Verification Queue | `stats.verificationQueueCount` | — | ✓ (if > 0) |
| 6 | Pending Approvals | `stats.pendingApprovals` | — | ✓ (if > 0) |

---

### 1.23 Dark UI Anti-Patterns

Bolt frequently outputs light-mode defaults for certain components. The table below maps every known failure point. **Add "Enforce dark theme — no white backgrounds or light borders anywhere" to every prompt, then specifically call out the affected components.**

| Component | Bolt default (wrong) | Correct spec |
|-----------|---------------------|-------------|
| Modal / Dialog | `bg-white` or `bg-card` | `bg-[#1A1A1A] border border-[#27272A] text-white` |
| Input, Textarea | white fill, light border | `bg-[#1A1A1A] border border-[#27272A] text-white placeholder:text-[#52525B] focus:border-[#EFFE5E]` |
| Select trigger + content | white/light dropdown | `bg-[#1A1A1A] border-[#27272A]` · content: `bg-[#0A0A0A]` · item hover: `bg-[#222222]` |
| Popover (date picker, command) | white bg | `bg-[#0A0A0A] border border-[#27272A] shadow-[0_8px_32px_rgba(0,0,0,0.6)]` |
| Tooltip (Radix default) | white bg, dark text | `bg-[#222222] text-white text-xs border border-[#27272A]` |
| Recharts `<Tooltip />` | white bg, serif font | `contentStyle={{ background: '#1A1A1A', border: '1px solid #27272A', color: '#fff', fontFamily: 'Larsseit' }}` |
| Table header row | `bg-muted` (light) | `bg-[#0A0A0A] text-[#A1A1AA] text-xs uppercase tracking-wider` |
| Loading skeleton | `bg-gray-200` shimmer | `bg-[#222222] animate-pulse` (no shimmer gradient — flat dark) |
| Alert / Banner (shadcn) | colored bg (info/warning) | `bg-[#1A1A1A] border-l-2 border-[#F59E0B] text-white` (border-accent only) |
| Sonner toast | default light theme | `<Toaster theme="dark" toastOptions={{ classNames: { toast: 'bg-[#1A1A1A] border border-[#27272A]' } }} />` |
| Focus ring (all interactive) | blue ring | `focus-visible:ring-1 focus-visible:ring-[#EFFE5E] focus-visible:outline-none` |
| Scrollbar (webkit) | browser default | `[&::-webkit-scrollbar]:w-1.5 [&::-webkit-scrollbar-track]:bg-transparent [&::-webkit-scrollbar-thumb]:bg-[#27272A]` |
| Calendar (react-day-picker) | white theme | override `.rdp` CSS vars: `--rdp-background-color: #1A1A1A; --rdp-accent-color: #EFFE5E; --rdp-color: #fff` |
| Command palette (cmdk) | white bg | `bg-[#0A0A0A]` root, `bg-[#222222]` selected item |
| Badge (shadcn default) | light gray | use status colors from §1.2 — never the default variant |
| Switch (shadcn) | blue thumb | `data-[state=checked]:bg-[#EFFE5E]` |
| Checkbox | blue check | `data-[state=checked]:bg-[#EFFE5E] data-[state=checked]:border-[#EFFE5E]` |

**Mandatory closing line for every bolt prompt:**
```
CRITICAL: This is a dark-only application — no white, no light surfaces, no default theme components.
Every shadcn/ui component must be overridden with the dark color tokens above.
```

---

### 1.24 Data Table Component — Reusable Spec

The `DataTable` component appears in 10+ pages. Define it once and reference it everywhere. This spec governs all list/table views in the platform.

#### Anatomy

```
┌─────────────────────────────────────────────────────────────────┐
│ COMMAND ROW — search + filter chips + sort + action button      │
│─────────────────────────────────────────────────────────────────│
│ HEADER ROW — col labels (sortable), sticky on scroll            │
│─────────────────────────────────────────────────────────────────│
│ DATA ROWS × N — clickable, hover highlight, checkbox optional   │
│─────────────────────────────────────────────────────────────────│
│ PAGINATION — items per page + page controls + count             │
└─────────────────────────────────────────────────────────────────┘
```

#### Container

```css
/* wrapper */
bg-[#000000]  w-full  rounded-[4px]  border border-[#27272A]  overflow-hidden
```

#### Command Row

```
height: 56px
bg-[#0A0A0A] border-b border-[#27272A] px-4 flex items-center gap-3
Left side:
  - Search input (h-9, w-64, bg-[#1A1A1A]) with Search icon 14px — placeholder: "Search..."
  - Active filter chips: each chip bg-[#222222] text-xs text-[#A1A1AA] px-2 py-0.5 rounded-[4px] + × icon (removes filter)
Right side (flex-end):
  - Sort dropdown (optional, if not inline with headers)
  - Primary action button (e.g. "Create Role", "Add Company") — Spriteburst
  - Secondary action button (optional ghost)
```

#### Header Row

```
height: 40px
bg-[#0A0A0A] border-b border-[#27272A]
Cells: text-[11px] font-semibold uppercase tracking-widest text-[#A1A1AA] px-4
Sticky: position sticky top-0 z-10
Sortable columns: show ChevronUp/ChevronDown icon 12px, active sort = text-white icon
Checkbox column (if bulk-select): 40px wide, left-most
Row-number column (if rank shown): 40px wide, left-most
```

#### Data Row

```
height: 52px (default), auto if content wraps
bg-[#000000] → hover bg-[#0A0A0A]
border-b border-[#27272A] (last row: no bottom border)
Cells: text-sm text-white px-4
transition: background 150ms ease

Selected row (checked): bg-[#1a1c00], border-l-2 border-[#EFFE5E]
Clickable rows: cursor-pointer

Row density option: compact (h-10), default (h-13), spacious (h-16)
Never use zebra striping — all rows same background, hover only
```

#### Column Type Patterns

| Column type | Render pattern |
|------------|----------------|
| Text (primary) | `text-sm text-white font-medium` |
| Text (secondary) | `text-sm text-[#A1A1AA]` |
| Status badge | `<StatusBadge status={row.status} />` from §1.2 |
| Score (0–100) | `<ScoreGauge value={row.score} />` — Spriteburst fill arc |
| Date | `text-sm text-[#A1A1AA]` — formatted as "14 Mar 2026" or relative "2 days ago" |
| Relative time | `text-xs text-[#52525B]` — "3 hours ago" (use `formatDistanceToNow` from `date-fns`) |
| Currency | `text-sm text-white` — `$120/hr` format |
| Skills chips | max 3 shown inline + `+N more` chip in `text-[#52525B]` if overflow |
| Avatar + name | `flex items-center gap-2` — 28px avatar circle + `text-sm font-medium text-white` |
| Actions | right-most column, `text-right`; inline buttons max 2, overflow in DropdownMenu |
| Boolean | `Check` icon `text-[#22C55E]` for true, `Minus` icon `text-[#52525B]` for false |
| Number | `text-sm font-mono text-white` (tabular nums) |

#### Action Column Patterns

```typescript
// Max 2 inline actions, rest in dropdown
// Primary inline: most common action for that row's status
// Ghost style: text-[#A1A1AA] hover:text-white text-xs h-7 px-2
// Dropdown trigger: MoreHorizontal icon button

// Example for roles table:
{status === 'ACTIVE'  && <Button size="sm" variant="ghost">Pause</Button>}
{status === 'DRAFT'   && <Button size="sm" variant="ghost">Publish</Button>}
<DropdownMenu> ... </DropdownMenu>
```

#### Pagination

```
height: 48px, border-t border-[#27272A], px-4
bg-[#0A0A0A]
Left: "Showing 1–25 of 143 results" — text-xs text-[#A1A1AA]
Right: [Previous] [1] [2] [3] ... [12] [Next] — text-xs, active page: bg-[#1A1A1A] text-white border border-[#27272A]
Items per page: select (options: 25 | 50 | 100), text-xs, far right
```

#### State: Loading

```
Show 5 skeleton rows. Each row:
  - checkbox cell: 20×20px rounded skeleton
  - text cell: h-4 w-[60–160px] bg-[#222222] animate-pulse rounded
  - badge cell: h-5 w-16 bg-[#222222] animate-pulse rounded-full
Stagger animation: each row delays 40ms more than previous
aria-busy="true" on table container
aria-label="Loading results"
```

#### State: Empty (no data at all)

```
Full-height centered (min 240px):
  Icon: matching page icon, 40px, text-[#27272A]
  Title: text-base font-semibold text-[#A1A1AA] — use §5.5 empty formula
  Body: text-sm text-[#52525B]
  CTA button: primary if there's a creation action, otherwise omitted
```

#### State: Empty (filtered — search/filter applied with no results)

```
Same structure but:
  Icon: SearchX 40px text-[#27272A]
  Title: "No results match your filters."
  Body: "Try adjusting your search or clearing filters."
  CTA: "Clear Filters" — ghost button
```

#### State: Error

```
Full-height centered:
  Icon: AlertCircle 40px text-[#EF4444]
  Title: "We couldn't load this data."
  Body: "Check your connection and try again."
  CTA: "Retry" — ghost button (re-executes refetch())
```

#### TypeScript Interface

```typescript
export interface DataTableColumn<T> {
  key: keyof T | string
  label: string
  sortable?: boolean
  width?: string            // e.g. 'w-48', 'w-24', 'flex-1'
  align?: 'left' | 'right' | 'center'
  render?: (row: T) => React.ReactNode
}

export interface DataTableProps<T> {
  columns: DataTableColumn<T>[]
  data: T[]
  loading?: boolean
  error?: boolean
  onRetry?: () => void
  onRowClick?: (row: T) => void
  selectable?: boolean
  selectedIds?: string[]
  onSelectionChange?: (ids: string[]) => void
  pagination?: {
    total: number
    page: number
    pageSize: number
    onPageChange: (page: number) => void
    onPageSizeChange: (size: number) => void
  }
  emptyState?: {
    icon?: LucideIcon
    title: string
    body?: string
    action?: React.ReactNode
  }
}
```

---

### 1.25 Apollo Client Provider — Next.js 14 App Router Setup

Next.js 14 App Router uses Server Components by default. Apollo Client requires a React Context, which only works in Client Components. Bolt must implement this exact pattern — any deviation will cause "hooks can only be called inside a Client Component" errors.

#### Required file: `lib/apollo-provider.tsx`

This file **must already exist** in `apps/web/lib/`. If bolt regenerates it, use this exact content:

```typescript
// apps/web/lib/apollo-provider.tsx
'use client'

import { ApolloClient, ApolloProvider, InMemoryCache, HttpLink } from '@apollo/client'
import { useMemo } from 'react'

function makeClient() {
  return new ApolloClient({
    link: new HttpLink({
      uri: process.env.NEXT_PUBLIC_GRAPHQL_URL ?? 'http://localhost:4000/graphql',
      // credentials: 'include'  // enable if using cookie-based auth
    }),
    cache: new InMemoryCache(),
    defaultOptions: {
      watchQuery: { fetchPolicy: 'cache-and-network' },
    },
  })
}

export function ApolloWrapper({ children }: { children: React.ReactNode }) {
  const client = useMemo(() => makeClient(), [])
  return <ApolloProvider client={client}>{children}</ApolloProvider>
}
```

#### Required: `app/layout.tsx` wrapper

The root layout wraps all children in `ApolloWrapper`. **Do not let bolt regenerate this file** — it's in `4.3 Existing Files That Must Not Be Overwritten`. The wrapper is already present:

```typescript
// apps/web/app/layout.tsx (existing — do not overwrite)
import { ApolloWrapper } from '@/lib/apollo-provider'
// ...
export default function RootLayout({ children }: { children: React.ReactNode }) {
  return (
    <html lang="en">
      <body>
        <ApolloWrapper>
          {children}
        </ApolloWrapper>
      </body>
    </html>
  )
}
```

#### Rules bolt must follow

| Rule | Why |
|------|-----|
| `'use client'` on every file that calls `useQuery` or `useMutation` | Apollo hooks are client-only |
| Never call `useQuery` in a Server Component | Will throw at runtime — context is null |
| Never import `ApolloClient` directly in page components | Always use hooks; Provider is in layout |
| `'use client'` goes on the page if the entire page is interactive, or on a wrapper component if only part of the page needs data | Keeps Server Components for static sections |
| When in doubt, put `'use client'` on the outermost component that uses Apollo | Safer than missing it |

#### Pattern for pages with mixed Server/Client needs

```typescript
// app/(dashboard)/dashboard/roles/page.tsx — pure Server Component
import { RolesClientView } from '@/components/roles/roles-client-view'

export default function RolesPage() {
  return <RolesClientView />  // all Apollo queries live in here
}

// components/roles/roles-client-view.tsx
'use client'
import { useQuery } from '@apollo/client'
// ...
```

---

### 1.26 shadcn/ui CSS Variable — Dark Theme Overrides

When shadcn is initialized, it writes CSS variables to `globals.css` in a `:root` block. By default these are light-mode values. The project uses a **dark-only** theme. Bolt must either:
1. Never use the default shadcn CSS variable names (e.g. `bg-background`, `text-foreground`) — use the raw Tailwind hex classes directly, **OR**
2. Override the shadcn CSS variables to match the dark token system

**Option 2 is correct** when using shadcn `cn()` utility extensively. Below are the exact overrides to add in `globals.css` inside `:root` (not inside `.dark`) since the app has no light mode:

```css
/* apps/web/app/globals.css — shadcn CSS variable overrides */
/* Force dark-only: put all values in :root, not in .dark */

:root {
  /* Backgrounds */
  --background:        10 10 10;       /* #000000 */
  --foreground:        255 255 255;    /* #FFFFFF */
  --card:              26 26 26;       /* #1A1A1A */
  --card-foreground:   255 255 255;
  --popover:           17 17 17;       /* #111111 */
  --popover-foreground: 255 255 255;

  /* Brand */
  --primary:           181 227 27;     /* #EFFE5E Spriteburst */
  --primary-foreground: 0 0 0;         /* black text on Spriteburst */

  /* Surfaces */
  --secondary:         34 34 34;       /* #222222 */
  --secondary-foreground: 255 255 255;
  --muted:             39 39 42;       /* #27272A */
  --muted-foreground:  161 161 170;    /* #A1A1AA */
  --accent:            34 34 34;
  --accent-foreground: 255 255 255;

  /* Semantic */
  --destructive:       239 68 68;      /* #EF4444 */
  --destructive-foreground: 255 255 255;
  --border:            39 39 42;       /* #27272A */
  --input:             26 26 26;       /* #1A1A1A */
  --ring:              181 227 27;     /* #EFFE5E — focus ring */

  /* Radius (matches §1.5) */
  --radius: 0.625rem;                  /* 10px = radius-md default */
}
```

**Usage note:** shadcn components consume these as `hsl(var(--primary))` — but our values are RGB triples, so the `hsl()` wrapper in shadcn tokens will produce incorrect colors. **Override the shadcn component class names directly** using the approach in §1.23 (explicit hex Tailwind classes) rather than relying on CSS variables for styling. Use the CSS variable override above only as a fallback for third-party components that read shadcn variables.

**Bolt instruction to include in prompts:**
```
Do NOT use shadcn default CSS variable class names (bg-background, bg-card, bg-popover,
bg-primary, text-foreground, etc.) in any component. Use explicit hex-based Tailwind
classes from §1.23 and §1.2 instead. Shadcn CSS variables are not reliable in this
dark-only configuration.
```

---

## PART 2 — PAGE SPECIFICATIONS

---

### 2.1 PUBLIC + AUTH PAGES

---

#### PAGE: Landing Page (`/`)

**Purpose:** Explain the platform to recruiters, convert to sign-up.
**Role:** Public (no auth required)
**Route exit:** `/login` or `/register`

**Layout Sections (top to bottom):**

**Section 1 — Navigation Bar**
```
Position: fixed top, full width
Background: transparent → surface on scroll (backdrop-blur)
Left: Larsseit wordmark/logo in Spriteburst
Right: "Sign In" (ghost button) + "Get Started" (primary button)
Height: 64px
Transition: background opacity 0→1 on scroll > 80px
```

**Section 2 — Hero**
```
Background: full-bleed dark (#000000)
Layout: two-column — left text, right visual
Headline: "Hire the Right Talent. Fast." — text-6xl ExtraBold, text-primary
Sub-headline: "AI-powered matching connects enterprise hiring teams with qualified talent — from shortlist to offer in hours, not weeks." — text-xl Regular, text-secondary, max-width 480px
Primary CTA: "Get Started" — primary large button, Spriteburst, leads to /register
Secondary CTA: "Sign In" — ghost button
Visual: abstract dark illustration or platform screenshot (fill with placeholder initially)
Padding: 120px top, 80px bottom
```

**Section 3 — Outcome Stats Row**
```
Three inline stats, dark dividers between:
- "4.2 hrs" / Average time to shortlist
- "93%" / Match accuracy score
- "2,300+" / Active talent profiles
Font: stat value text-4xl Bold Spriteburst, label text-sm text-secondary
Background: surface, full-width
Padding: 48px vertical
```

**Section 4 — How It Works**
```
Title: "From Demand to Hire in Three Steps" — text-3xl ExtraBold, centered
Three horizontal steps with numbered Spriteburst circles:
1. "Post a Role" — recruiter defines requirements, AI enhances description
2. "Review Your Shortlist" — AI ranks matched candidates with explained scores
3. "Move to Hire" — schedule interviews, send offers, track accepted placements
Each step: icon + title + one sentence description
Background: bg (#000000)
```

**Section 5 — Feature Modules**
```
Title: "Everything Your Hiring Team Needs" — text-3xl ExtraBold
Grid: 2x3 or 3x2 feature blocks, each with Spriteburst icon + title + body text
Modules to list:
- AI Talent Matching (vector search + scored shortlists)
- Smart Talent Search (semantic + filter)
- Role Description Assistant (AI-generated JDs)
- Interview & Offer Pipeline (end-to-end workflow)
- Admin Governance (verification, approvals, analytics)
- Recruiter Analytics (velocity, conversion, skills demand)
Block style: surface background, border-default, radius-lg, hover=surface-high
No decorative cards — functional info blocks with clear data density
```

**Section 6 — Role Pathways**
```
Two-panel layout:
Left: "For Recruiters" — what they do, screenshot/illustration, CTA "Start Hiring"
Right: "For Platform Admins" — what they manage, CTA "Admin Access"
Background: surface-alt gradient
```

**Section 7 — Footer**
```
Background: surface
Columns: Platform links | Resources | Legal
Bottom row: copyright + "Built with AI matching and pgvector"
Text: text-sm text-muted
```

**States:**
- No loading state (static page)
- CTA buttons route to `/register` and `/login`

---

#### PAGE: Login (`/login`)

**Purpose:** Authenticate returning users
**Route:** `/login`
**On success:** Redirect recruiter → `/dashboard`, admin → `/admin`

**Layout:**
```
Full-screen centered layout — dark background
Left half (desktop): platform brand panel — logo + tagline + feature blurb
Right half (desktop): login form panel (surface background, radius-xl, shadow-lg)
Mobile: form only, stacked
```

**Form Panel:**
```
Title: "Welcome Back" — text-2xl ExtraBold
Subtitle: "Sign in to continue to your workspace." — text-sm text-secondary

Fields:
- Email Address (type=email, autocomplete=email)
- Password (type=password, show/hide toggle)

Below fields: "Forgot Password?" right-aligned link → /forgot-password

Primary CTA: "Sign In" — primary full-width button

Divider: "or"
Secondary: "Create an account" link → /register
```

**States:**
- Loading: button shows spinner, disabled
- Error: red inline banner "Invalid email or password. Try again." below form
- Success: redirect, no flash

**Copy rules:**
- No "Login" — use "Sign In"
- Error must say what failed + what to do

---

#### PAGE: Register (`/register`)

**Purpose:** Create a recruiter account
**Route:** `/register`
**On success:** Redirect → `/dashboard`

**Form Panel:**
```
Title: "Create Your Account" — text-2xl ExtraBold
Subtitle: "Set up your recruiter workspace. It takes under a minute." — text-sm text-secondary

Fields:
- First Name
- Last Name
- Email Address
- Password (min 8 chars, strength indicator)
- Confirm Password

Primary CTA: "Create Account" — primary full-width button

Below: "Already have an account? Sign In" → /login
```

**Inline validation:**
- Email: format check on blur
- Password: strength meter (weak / fair / strong) as user types
- Confirm Password: match check on blur
- Required field errors appear below each field

**States:**
- Loading: spinner on button
- Error: field-level errors
- Success: redirect

---

#### PAGE: Forgot Password (`/forgot-password`)

**Layout:** Minimal centered panel, same shell as login

**Form:**
```
Title: "Reset Your Password"
Subtitle: "Enter your email address and we'll send you a reset link."
Field: Email Address
CTA: "Send Reset Link"
Back link: "Return to Sign In" → /login
```

**States:**
- Success state (no redirect): swap form for confirmation message
  - "Check your email. A reset link has been sent to [email]. It expires in 1 hour."
  - Link: "Didn't receive it? Resend" (mutation re-trigger)
- Error: "No account found for this email."

---

#### PAGE: Reset Password (`/reset-password`)

**Layout:** Minimal centered panel

**Form:**
```
Title: "Choose a New Password"
Subtitle: "Your new password must be at least 8 characters."
Fields:
- New Password (strength indicator)
- Confirm Password
CTA: "Reset Password"
```

**States:**
- Invalid token: error state "This link has expired or is invalid. Request a new one." + link to /forgot-password
- Success: confirmation message + "Sign In" link

---

### 2.2 RECRUITER DASHBOARD PAGES

---

#### PAGE: Recruiter Dashboard (`/dashboard`)

**Purpose:** Operational command center. Show hiring health at a glance and surface what needs action.
**Required queries:** `recruiterDashboard` (active demands, activity feed, KPIs)
**Role guard:** RECRUITER only

**KPI Row (top)**
```
Four cells in a single bordered container:
1. Active Roles — count of ACTIVE demands
2. Shortlisted Candidates — total candidates across active demands
3. Interviews This Week — scheduled interviews (current 7 days)
4. Avg. Time to Shortlist — median hours from demand created → shortlist generated
Each cell: value (text-3xl 700 Spriteburst), label (text-xs secondary uppercase)
Delta arrows where applicable (vs. last 30 days)
```

**Roles Requiring Attention (main section)**
```
Section header: "Roles Requiring Attention" — text-xl 600
List of demands that are: ACTIVE with no interviews yet, OR stale (>7 days no activity)
Each row: role title | company | days open | shortlist count | next action button
Next action CTA: "Review Shortlist" or "Schedule Interview" contextually
Max 5 rows, "View All Roles" link to /dashboard/roles
Empty state: "No roles need attention. All active demands are progressing."
```

**Recent Activity Feed (right column)**
```
Title: "Recent Activity"
Timeline list — each item: action description + timestamp + related entity link
Events: new match, interview scheduled, offer sent, demand created, candidate shortlisted
Max 10 items
Empty state: "No recent activity. Post a role to get started."
```

**Quick Action Bar (below KPI row)**
```
Horizontal row of buttons:
- "Create Role" → /dashboard/roles/new (primary)
- "Search Talent" → /dashboard/search (secondary)
- "Review Shortlists" → /dashboard/shortlists (secondary)
```

**Page enter animation:** Stagger KPI cells on load (delay 0, 0.06, 0.12, 0.18s)

---

#### PAGE: Roles List (`/dashboard/roles`)

**Purpose:** Manage all posted demands. Monitor status, take actions.
**Required queries:** `myDemands(filters, pagination)`
**Role guard:** RECRUITER

**Page Header Row:**
```
Title: "Role Demands"
Subtitle: "Monitor demand status and move roles through the pipeline."
Primary CTA: "New Role" → /dashboard/roles/new
```

**Command Row:**
```
Left: search input ("Search by title or skill...")
Center: status filter tabs — All | Active | Draft | Paused | Filled | Cancelled
Right: sort dropdown (Newest | Oldest | Most Candidates | Urgency)
```

**Demand Table:**
```
Columns:
- Role Title (clickable → /dashboard/roles/[id])
- Company
- Status Badge
- Required Skills (first 3 as small chips, +N overflow)
- Shortlisted (candidate count)
- Budget Range
- Posted Date
- Actions (View | Edit | Archive — row kebab menu)

Row: h-14, hover=surface-high
Click row → navigate to /dashboard/roles/[id]
```

**Pagination:** cursor-based, 20 rows per page

**States:**
- Loading: 5 skeleton rows
- Empty: "No demands yet. Create a role to generate your first shortlist." + "New Role" button
- Error: "We couldn't load your roles. Try again."

---

#### PAGE: Create Role (`/dashboard/roles/new`)

**Purpose:** Post a new talent demand with AI-assisted description.
**Required mutations:** `createDemand`, `generateRoleDescription` (AI engine via API)
**Role guard:** RECRUITER

**Layout:** Two-column form — left: form fields, right: AI preview panel

**Form Fields (left panel):**
```
Section 1 — Role Basics
- Role Title (text input, required)
- Company (dropdown from user's companies)
- Experience Level (select: Junior | Mid | Senior | Lead | Executive)
- Location (text input)
- Remote Policy (select: Onsite | Hybrid | Remote)

Section 2 — Skills & Requirements
- Required Skills (multi-select with search + tag creation)
  → Searches existing skills via `skills(search)` query
  → Each skill shown as Spriteburst-bordered chip with remove ×
- Project Requirements (textarea, 500 char limit)

Section 3 — Timeline & Budget
- Start Date (date picker)
- Contract Duration (text input: "3 months", "6 months", etc.)
- Budget Min / Budget Max (two number inputs, $ prefix)
- Currency (select, default USD)

Section 4 — Raw Description
- Your Notes (textarea, placeholder: "Describe what you need in your own words. AI will enhance this.")
```

**AI Panel (right panel):**
```
Title: "AI Role Assistant"
Subtitle: "Click 'Enhance with AI' to generate a polished role description from your notes."
State default: placeholder illustration + "Your AI-enhanced description will appear here."
Button: "Enhance with AI" → Spriteburst primary button
On trigger: loading state (shimmer in AI panel + "Analyzing your role requirements...")
On success: shows generated:
  - Formatted job title (may differ from raw)
  - Role summary paragraph
  - Responsibilities (bulleted)
  - Requirements (bulleted)
  - Nice-to-haves (bulleted)
  - Suggested skills (chips with "+ Add" action)
  - Salary band suggestion
  - Seniority recommendation

Accept/Reject controls:
- "Use This Description" → fills final description field
- "Try Again" → re-triggers AI
- "Edit Manually" → opens plain textarea with AI content pre-filled

Final description field (below AI panel):
- Editable textarea, used as `aiGeneratedDescription` field on submit
```

**Form Actions:**
```
"Save as Draft" — ghost button → createDemand(status: DRAFT)
"Publish Role" — primary button → createDemand(status: ACTIVE) + triggers AI shortlist generation
```

**States:**
- AI loading: shimmer animation in right panel
- Submit loading: spinner on publish button, disabled form
- Success: redirect to /dashboard/roles/[newId]
- Error: inline banner "Role could not be created. Check required fields."

---

#### PAGE: Role Detail (`/dashboard/roles/[id]`)

**Purpose:** Work a single demand through its full lifecycle.
**Required queries:** `demand(id)`, `shortlist(demandId)`, `interviews`, `offers`
**Required mutations:** varies by tab
**Role guard:** RECRUITER

**Layout:**
```
Header: role title + company + status badge + action buttons
Metadata Rail (right sidebar, fixed): budget | level | location | remote | skills | start date | duration | posted date
Tabs below header: Overview | Shortlist | Interviews | Offers
Tab content fills center column, metadata rail fixed right
```

**Tab 1 — Overview**
```
AI-generated description (formatted, read-only)
Original recruiter notes (collapsed by default)
Timeline: workflow events for this demand (demand created, shortlist generated, interviews, offers)
Action buttons: Edit Role | Pause | Mark Filled | Cancel
```

**Tab 2 — Shortlist**
```
Filter row: score range slider | availability | rate range | sort (Score | Availability | Rate)
Ranked table:
- Rank # | Candidate Name | Match Score (colored gauge) | Key Skills (first 3) | Availability | Hourly Rate | Status Badge
- Click row → expand inline OR open Candidate Profile Modal
Score gauge: Spriteburst fill, 0–100 arc
"Why this match" expand: AI explanation text below row
Row actions: "Request Interview" (primary inline) | "Reject" (ghost)
Bulk select: checkbox + "Request Interview for Selected"
"Regenerate Shortlist" button top-right → triggers AI re-match with loading state
```

**Candidate Profile Modal (shared component):**
```
Triggered from Shortlist or Search result rows
Wide modal (720px)
Tabs: Profile | Skills | Experience | Certifications
Profile tab: headline, summary, availability, rate, location, visa
Skills tab: proficiency bars per skill
Experience tab: timeline entries
Certifications tab: list with verify badges
Actions: "Request Interview" (primary) | "Reject Candidate" (destructive ghost)
Score breakdown visible in header: radar chart or horizontal bars for all 7 factors
```

**Tab 3 — Interviews**
```
Interview queue table:
Columns: Candidate | Scheduled Date/Time | Duration | Status | Actions
Status badges: SCHEDULED | COMPLETED | CANCELLED | NO_SHOW
Row expand: meeting URL + feedback form (if COMPLETED)
Actions: Reschedule | Cancel | View Detail → /dashboard/interviews/[demandId]/[interviewId]
"Schedule Interview" button → opens schedule modal
Schedule modal: candidate select (from shortlist SHORTLISTED status), date/time picker, duration, optional meeting URL
```

**Tab 4 — Offers**
```
Offer table:
Columns: Candidate | Hourly Rate | Start Date | Status | Sent Date | Actions
Actions: Send | Withdraw | View → /dashboard/offers/[demandId]/[offerId]
"Draft Offer" button → opens offer form modal
Offer form modal: 
  - Pre-filled candidate (from interview)
  - Hourly Rate (number), Start Date, End Date, Terms (textarea)
  - Save as Draft | Send Offer
```

---

#### PAGE: Shortlists Queue (`/dashboard/shortlists`)

**Purpose:** Review all shortlisted candidates across all demands in one queue.
**Required queries:** `allShortlists(filters)` — candidates across all my demands with RECRUITER_REVIEWED or AI_SUGGESTED status

**Command Row:**
```
Search: by candidate name or skill
Filter: by demand (dropdown) | by score range | by availability
Sort: Score (default) | Availability | Rate
```

**Ranked List:**
```
Each row: Demand label (chip) | Candidate | Score gauge | Top Skills | Availability | Rate | Status | Actions
Score gauge: Spriteburst-colored arc
"Score Breakdown" expand per row: horizontal bars for all 7 scoring factors
Actions: "Request Interview" | "Open Profile" | "Reject"
```

**States:**
- Empty: "No shortlisted candidates across your active roles. Publish a role to generate matches."
- Loading: skeleton rows

---

#### PAGE: Smart Talent Search (`/dashboard/search`)

**Purpose:** Direct semantic search of entire talent pool.
**Required queries:** `semanticSearch(query, filters)` via AI engine through API
**Role guard:** RECRUITER

**Layout:** Two-column — left: filter panel (collapsible), right: results

**Search Bar (full top):**
```
Large, prominent input — height 52px
Placeholder: "e.g. Senior ML engineer with fintech experience, available immediately"
"Run Search" button inline right — Spriteburst primary
Subtle label below: "Describe what you need in plain language. AI understands context and skills."
```

**Filter Panel (left, collapsible):**
```
Title: "Refine Results"
Sections:
- Skills (multi-select searchable, tags)
- Skill Match Mode (radio: Must have all | Match any)
- Experience Level (multi-checkbox)
- Industry (multi-checkbox)
- Availability (select: Immediate | 2 weeks | 1 month | 3 months)
- Hourly Rate (dual slider, $0–$300)
- Location / Remote (multi-select)
Clear All Filters link
```

**Results (right):**
```
Results count header: "42 candidates match your search"
Results table:
Columns: Candidate | Headline | Score | Top Skills | Availability | Rate | Actions
Row click → Candidate Profile Modal
Actions: "View Profile" | "Add to Shortlist"
Pagination: cursor-based

AI Recommendations section (above results if no query yet):
"Based on your recent roles, you may be interested in:"
3–5 candidate preview rows
```

**States:**
- No query yet: AI recommendations + empty search illustration
- Loading: skeleton rows
- No results: "No candidates match your search. Try adjusting skills or removing filters."
- Error: "Search failed. Try again or simplify your query."

---

#### PAGE: Interviews Queue (`/dashboard/interviews`)

**Purpose:** Manage all interviews across all demands in one place.
**Required queries:** `allInterviews(filters, pagination)`
**Role guard:** RECRUITER

**Command Row:**
```
Status filter tabs: All | Scheduled | Completed | Cancelled | No-Show
Date range filter
Search by candidate name
```

**Interview Table:**
```
Columns: Candidate | Role/Demand | Scheduled Date | Time | Duration | Status | Feedback | Actions
Actions: Reschedule | Cancel | Submit Feedback | View Detail
"Schedule New Interview" button top-right → opens schedule modal (demand + candidate + time)
```

**States:**
- Empty: "No interviews scheduled yet. Request one from Shortlist or Role Detail."
- Group by date option (calendar-adjacent view)

---

#### PAGE: Interview Detail (`/dashboard/interviews/[demandId]/[interviewId]`)

**Purpose:** Deep detail view for a single interview.
**Required queries:** `interview(id)` with candidate, demand, feedback
**Required mutations:** `submitFeedback`, `cancelInterview`, `rescheduleInterview`

**Layout:**
```
Left: interview info panel
  - Candidate section: avatar, name, headline, score
  - Interview section: date/time, duration, meeting URL
  - Demand section: role title, company
Right: action panel + feedback form
  - Status badge large
  - Action buttons: Complete Interview | Reschedule | Cancel
  - Feedback form (visible when status=COMPLETED):
    - Rating (1–5 stars, Spriteburst filled)
    - Feedback text (textarea)
    - Skills Demonstrated (multi-select tags)
    - "Submit Feedback" primary button → updateInterview mutation
```

**Timeline (bottom):**
```
Workflow events for this interview:
- Interview requested
- Interview scheduled
- (If applicable) Rescheduled
- Feedback submitted
- Offer drafted
```

---

#### PAGE: Offers Queue (`/dashboard/offers`)

**Purpose:** Track all offers across all demands.
**Required queries:** `allOffers(filters)`
**Role guard:** RECRUITER

**Command Row:**
```
Status tabs: All | Draft | Sent | Accepted | Declined | Withdrawn
Search by candidate
```

**Offer Table:**
```
Columns: Candidate | Role | Hourly Rate | Start Date | End Date | Status | Sent Date | Actions
Aging indicator: yellow/red flag icon if SENT > 72 hours with no response
Actions: Send | Withdraw | View Detail
```

**States:**
- Empty: "No offers yet. Draft an offer from an Interview detail page."

---

#### PAGE: Offer Detail (`/dashboard/offers/[demandId]/[offerId]`)

**Purpose:** Full offer view with terms, timeline, actions.
**Required queries:** `offer(id)` with candidate, demand, interview
**Required mutations:** `sendOffer`, `withdrawOffer`

**Layout:**
```
Header: Offer status badge + candidate name + role title
Two-column:
Left: Offer Terms
  - Hourly Rate, Currency
  - Start Date, End Date
  - Contract Duration (derived)
  - Terms (full text)
  - Candidate status (awaiting response / accepted / declined)
Right: Actions + Activity Timeline
  - "Send Offer" primary (if DRAFT)
  - "Withdraw Offer" destructive (if SENT)
  - Activity timeline: drafted, sent, opened (if tracked), responded
```

---

#### PAGE: Recruiter Analytics (`/dashboard/analytics`)

**Purpose:** Understand hiring performance, skill demand, pipeline health.
**Required queries:** `recruiterAnalytics` — aggregated from demands, shortlists, interviews, offers
**Role guard:** RECRUITER

**KPI Row (top):**
```
Cells: Roles Posted | Candidates Shortlisted | Interviews Conducted | Offers Accepted | Avg. Time to Hire | Avg. Cost per Hire
```

**Charts Section:**

**Chart 1 — Hiring Velocity (line chart)**
```
X axis: last 12 weeks
Y axis: demands created vs. shortlists generated vs. interviews vs. offers
Lines in: Spriteburst | white | warning | info colors
```

**Chart 2 — Pipeline Conversion (funnel or bar)**
```
Demand Posted → Shortlisted → Interview Requested → Interview Completed → Offer Sent → Offer Accepted
Show count + conversion % at each stage
```

**Chart 3 — Top Skills in Demand (horizontal bar)**
```
Top 10 required skills across all demands
Bar fill: Spriteburst
Sorted by frequency
```

**Chart 4 — Role Aging Distribution (bar)**
```
Buckets: 0–7 days | 8–14 | 15–30 | 31–60 | 60+
Shows how old open demands are getting
Warning color for 30+ days
```

**Data Table — Role Performance:**
```
Columns: Role Title | Status | Posted Date | Days Open | Shortlisted | Interviews | Offers | Stage
Sortable columns
```

**Filter Bar:** Date range selector (last 30/90/180 days / custom)

**Export:** "Export Report" → downloads CSV of all visible data

---

### 2.3 ADMIN PAGES

---

#### PAGE: Admin Dashboard (`/admin`)

**Purpose:** Platform operations overview. See what needs governance action.
**Required queries:** `adminDashboard` — platform-wide KPIs, queue snapshots
**Role guard:** ADMIN only

**KPI Row:**
```
Cells: Total Users | Active Talent | Active Demands | Placements This Month | Verification Queue | Pending Approvals
```

**Verification Queue Snapshot:**
```
Section header: "Verification Queue" + "Review All" link → /admin/verification
List of top 5 pending PENDING verification status talent profiles
Each row: name | submitted date | documents uploaded | "Review" CTA
Empty: "Verification queue is clear."
```

**Demand Approvals Snapshot:**
```
Section header: "Pending Approvals" + "Review All" → /admin/approvals
Top 5 demands awaiting approval
Each row: role title | company | submitted by | date | "Review" CTA
```

**System Alerts:**
```
Section: "Platform Alerts"
Flagged items: talent profiles with expired certifications, demands inactive > 30 days, offers unresponded > 5 days
Each alert: severity badge | message | action link
Empty: "No alerts. Platform operating normally."
```

---

#### PAGE: User Management (`/admin/users`)

**Purpose:** Manage all registered users.
**Required queries:** `users(filters, pagination)`
**Required mutations:** `updateUserRole`, `deactivateUser`, `activateUser`

**Command Row:**
```
Search by name or email
Role filter: All | TALENT | RECRUITER | ADMIN
Status filter: All | Active | Inactive
```

**User Table:**
```
Columns: Name | Email | Role (badge) | Status | Company (if recruiter) | Joined Date | Last Active | Actions
Actions: Edit Role | Deactivate / Activate | View Profile
Role edit: inline dropdown → confirm modal
Deactivate: confirm modal with reason text
Bulk actions: select multiple → bulk deactivate
```

**States:**
- Empty: "No users found."
- Loading: skeleton rows

---

#### PAGE: Talent Verification (`/admin/verification`)

**Purpose:** Review and decide on talent verification submissions.
**Required queries:** `talentVerificationQueue(status: PENDING)`
**Required mutations:** `approveTalentVerification`, `rejectTalentVerification`

**Layout:** Split-pane — left list, right document review panel

**Left: Verification Queue List**
```
Tabs: Pending | Approved | Rejected
Each row: name | headline | submitted date | document count
Click → loads detail in right panel
```

**Right: Verification Detail Panel**
```
Talent profile summary: name, photo, headline, skills, experience summary
Document section:
  - Identity documents (file viewer or download link)
  - Uploaded certifications with names
  - Verification status and notes history

Decision controls:
  - "Approve" — primary Spriteburst button → approveTalentVerification mutation
  - "Reject" — destructive button → opens modal with required reason field

Reason field (reject modal): textarea, required
Confirm rejected → rejectTalentVerification(reason)
```

**States:**
- Empty queue: "Verification queue is clear. No pending submissions."

---

#### PAGE: Company Management (`/admin/companies`)

**Purpose:** Manage portfolio companies and their recruiter assignments.
**Required queries:** `companies(filters)`
**Required mutations:** `createCompany`, `updateCompany`, `assignRecruiter`

**Command Row:**
```
Search by company name
Filter by industry or size
"Add Company" button → opens company form modal
```

**Company Table:**
```
Columns: Company Name | Industry | Size | Active Demands | Total Hires | Recruiters Assigned | Actions
Actions: Edit | Assign Recruiter | View Demands
```

**Assign Recruiter Modal:**
```
Company name header
Current recruiters list (removable)
Add recruiter: search RECRUITER-role users → assign
```

---

#### PAGE: Demand Approvals (`/admin/approvals`)

**Purpose:** Review demands before they go live (if admin approval is required).
**Required queries:** `demandsAwaitingApproval`
**Required mutations:** `approveDemand`, `rejectDemand`, `flagDemandHardToFill`

**Layout:** Split-pane (same as verification page pattern)

**Left: Approval Queue**
```
Each row: role title | company | recruiter | submitted date
Click → detail in right panel
```

**Right: Demand Detail Panel**
```
Full demand display: title, description, skills, level, location, budget
Recruiter info
Decision controls:
  - "Approve" → approveDemand
  - "Request Changes" → rejectDemand with required notes
  - "Flag as Hard-to-Fill" → flagDemandHardToFill (makes eligible for concierge)
```

---

#### PAGE: Concierge / Headhunter Assignment (`/admin/concierge`)

**Purpose:** Assign headhunters to hard-to-fill demands, track external candidate intake.
**Required queries:** `hardToFillDemands`, `conciergeAssignments`
**Required mutations:** `assignConcierge`, `submitExternalCandidate`

**Layout:**
```
Tabs: Hard-to-Fill Queue | Active Assignments | External Submissions
```

**Tab 1 — Hard-to-Fill Queue:**
```
Table: role title | company | days open | shortlist count | "Assign Concierge" action
Assign modal: select headhunter user (HEADHUNTER role) → assignConcierge mutation
```

**Tab 2 — Active Assignments:**
```
Table: demand | assigned headhunter | assignment date | candidates submitted | status
Status: SEARCHING | SUBMITTED | REVIEWING | CLOSED
```

**Tab 3 — External Submissions:**
```
Table: candidate name | demand | submitted by | date | status | actions
Status: SUBMITTED | SHORTLISTED | REJECTED
Manual intake form: "Submit External Candidate" button → form with name, contact, skills, notes, demand assignment
```

---

#### PAGE: Platform Analytics (`/admin/analytics`)

**Purpose:** Platform-wide metrics for operators.
**Required queries:** `adminAnalytics` — aggregated platform data
**Role guard:** ADMIN

**KPI Row:**
```
Cells: Total Active Talent | Total Demands | Placement Rate | Avg. Placement Fee | Platform Utilization | Supply-Demand Ratio
```

**Charts:**

**Chart 1 — Talent Growth (line)**
```
New talent registrations per week, last 12 weeks
Verified vs. unverified breakdown
```

**Chart 2 — Skill Distribution (horizontal bar)**
```
Top 20 skills in talent pool
Demand for each skill (secondary bar overlay)
Gap indicator where demand > supply
```

**Chart 3 — Supply-Demand Gap (grouped bar)**
```
Top 10 roles/skills — supply count vs. active demand count
Red highlight where gap is critical (supply < demand x 0.5)
```

**Chart 4 — Hiring Timeline Distribution (histogram)**
```
Distribution of time-to-hire across all completed placements
Mean + median lines
```

**Chart 5 — Revenue / Pricing Trends (line)**
```
Average accepted hourly rate per skill category over time
Revenue from placement fees over time (if tracked)
```

**Demand Monitoring Table:**
```
Columns: Company | Active Demands | Avg. Days Open | Fill Rate | Spend YTD
```

---

### 2.4 SYSTEM / SHELL PAGES

These pages are required by Next.js App Router. Bolt should generate them as minimal but on-brand dark-shell pages, not white-screen defaults.

---

#### PAGE: Not Found (`/not-found` → `app/not-found.tsx`)

```
Background: full dark shell (no sidebar — public layout)
Centered column:
  - "404" — text-6xl ExtraBold Spriteburst
  - "Page not found." — text-2xl 700 text-primary
  - "The page you're looking for doesn't exist or has been moved." — text-base text-secondary
  - "Go to Dashboard" — primary button → /dashboard
  - "Return Home" — ghost button → /
```

---

#### PAGE: Error (`app/error.tsx` — client component)

```
Background: full dark shell (no sidebar)
Centered column:
  - AlertTriangle icon 48px warning color
  - "Something went wrong." — text-2xl 700 text-primary
  - "An unexpected error occurred. Your data is safe." — text-base text-secondary
  - Error message in collapsed detail (show/hide, text-xs text-muted, monospace)
  - "Try Again" — primary button → calls reset()
  - "Go to Dashboard" — ghost button → /dashboard
```

---

#### PAGE: Loading (`app/loading.tsx` + per-route `loading.tsx`)

```
Full-page loading state — shows while server component data fetches
Background: color-bg
Centered: spinning ring (text-primary 40px) + "Loading..." text-sm text-secondary
Duration: always show — Next.js handles the timing via Suspense
```

Per-route variants (in each route folder):
- `(dashboard)/loading.tsx` — skeleton of the standard page layout (sidebar + topbar outlines)
- `(admin)/loading.tsx` — same pattern

---

#### PAGE: Account Settings (`/settings`)

**Purpose:** User can update their profile info, change password, and manage notifications.
**Route:** `/settings`
**Required queries:** `me` — current authenticated user
**Required mutations:** `updateProfile`, `changePassword`, `updateNotificationPreferences`
**Role guard:** Any authenticated role

**Layout:** Settings shell — no sidebar data tables, just a vertical settings page with left nav within content area.

**Settings Navigation (left column, sticky):**
```
Mini nav: 200px, text-sm, active=Spriteburst left border
- Profile
- Security
- Notifications
- (Admin only) Platform
```

**Section: Profile**
```
Fields:
- Avatar (upload circle, drag-drop or click — uploads to Cloudflare R2)
- First Name / Last Name (inline pair)
- Email (read-only with change-email action)
- Job Title (text input)
- Company (read-only if RECRUITER — managed by admin)
CTA: "Save Profile" → updateProfile mutation
Success toast: "Profile updated."
```

**Section: Security**
```
Fields:
- Current Password
- New Password (strength meter)
- Confirm New Password
CTA: "Change Password" → changePassword mutation
Success toast: "Password changed. You may need to sign in again."
```

**Section: Notifications**
```
Toggle list (one per notification type):
- AI shortlist generated
- Interview scheduled
- Offer accepted / declined
- Demand approved / rejected
Each: label + description + toggle (Spriteburst when on)
CTA: "Save Preferences" → updateNotificationPreferences mutation
```

---

### 2.5 SHARED MODALS (GENERATE ONCE — REUSED ACROSS PAGES)

These are not routes — they are reusable components. Generate them before any page group.

---

#### Confirm Action Modal

```
Purpose: Any destructive or irreversible action (deactivate user, cancel demand, reject candidate)
Width: 480px
Content:
  - Icon: AlertTriangle (warning) or Trash2 (destructive) — 24px
  - Title: text-base 600 text-primary (e.g. "Cancel this role?")
  - Body: text-sm text-secondary — explain consequence
  - Optional reason textarea (required for admin rejection flows)
Buttons (right-aligned):
  - Confirm — destructive variant
  - Cancel — ghost variant
```

#### Skill Selector Modal

```
Purpose: Add required skills to a demand or search filter
Width: 560px
Search input top: live filter of skills list
Left panel: searchable skill list with checkboxes
Right panel: "Selected Skills" — chips with × remove
CTA: "Apply Skills" → closes modal, returns selected array
Skill data source: `skills(search)` GraphQL query
Supports: create new skill (if no match in search results: "Add '[query]' as new skill")
```

#### Schedule Interview Modal

```
Purpose: Schedule an interview from shortlist, role detail, or interviews queue
Width: 560px
Fields:
  - Candidate (pre-filled from shortlist click, otherwise searchable)
  - Demand (pre-filled from context, otherwise dropdown)
  - Date (date picker, min = today)
  - Time (time picker, 30-min intervals)
  - Duration (select: 30 min | 1 hr | 1.5 hrs | 2 hrs)
  - Meeting URL (optional text input, placeholder "https://meet.google.com/...")
  - Internal Notes (optional textarea)
CTA: "Schedule Interview" → scheduleInterview mutation
Success: closes modal + toast "Interview scheduled."
```

#### Draft Offer Modal

```
Purpose: Draft a new offer from interview detail or offers queue
Width: 560px
Fields:
  - Candidate (pre-filled from interview, read-only if context)
  - Demand (pre-filled from context, read-only if context)
  - Hourly Rate (number, $ prefix, currency select)
  - Start Date (date picker)
  - End Date (date picker, must be after start date)
  - Contract Terms (textarea, 1000 char limit)
CTAs:
  - "Save as Draft" → createOffer(status: DRAFT)
  - "Send Offer Now" → createOffer + sendOffer in sequence
Success: closes modal + toast "Offer drafted." or "Offer sent."
```

---

## PART 3 — BOLT.NEW PROMPT CONTRACT

---

### 3.1 Mandatory Prompt Header (include with EVERY page prompt)

Copy-paste this block at the start of every bolt.new prompt:

```
Tech stack:
- Next.js 14 App Router
- TypeScript (strict, no `any`)
- Tailwind CSS with custom tokens (see tailwind.config.ts below)
- shadcn/ui base components
- Framer Motion for all transitions
- lucide-react for all icons (no substitutions)
- recharts for all charts
- sonner for all toasts
- Larsseit font (local, @font-face declared in globals.css, weights 300/400/500/700/800)

Design system tokens (Tailwind class names):
- bg-bg, bg-surface, bg-surface-alt, bg-surface-high
- text-text-primary, text-text-secondary, text-text-muted, text-text-inverse
- text-primary (Spriteburst #EFFE5E), bg-primary
- border-border, border-border-strong
- rounded-sm (6px), rounded-md (10px), rounded-lg (14px), rounded-xl (20px), rounded-full

Layout rules:
- NO card-heavy layouts — use tables, split-panes, and single bordered containers
- All interactive states: loading skeleton, empty with action, error with recovery
- Sidebar: 240px fixed, bg-surface, border-r border-border
- TopBar: 56px, bg-surface, border-b border-border
- Content: padding 32px, max-width 1280px

Rules:
- No Lorem Ipsum — use realistic recruiter/admin marketplace copy
- All CTAs: action-first (verb + object) from the CTA table in §5.4
- All empty states: factual statement + reason + one primary action
- Framer Motion page enter: opacity 0→1, y 12→0, duration 0.22s ease standard
- toast.success / toast.error from sonner for all mutation feedback
- Auth guard is handled externally — generate the page component only
- All `useQuery` / `useMutation` hooks: write with correct operation name, leave body as `// TODO: wire GraphQL`
```

---

### 3.1a TypeScript Interface Stubs

Include these interfaces in a shared types comment at the top of each generated file. Bolt should use them for all data references — no `any`, no inline type invention.

```tsx
// ─── Core Domain Types ───────────────────────────────────────────────

interface User {
  id: string
  email: string
  firstName: string
  lastName: string
  role: 'TALENT' | 'RECRUITER' | 'ADMIN'
  isActive: boolean
  createdAt: string
  company?: Company
}

interface Company {
  id: string
  name: string
  industry?: string
  size?: string
}

interface Skill {
  id: string
  name: string
  category?: string
}

interface Demand {
  id: string
  title: string
  status: 'DRAFT' | 'ACTIVE' | 'PAUSED' | 'FILLED' | 'CANCELLED'
  company: Company
  experienceLevel: 'JUNIOR' | 'MID' | 'SENIOR' | 'LEAD' | 'EXECUTIVE'
  location?: string
  remotePolicy: 'ONSITE' | 'HYBRID' | 'REMOTE'
  requiredSkills: Skill[]
  budgetMin?: number
  budgetMax?: number
  currency: string
  startDate?: string
  contractDuration?: string
  aiGeneratedDescription?: string
  createdAt: string
  updatedAt: string
  shortlistCount?: number
}

interface ShortlistedCandidate {
  id: string
  rank: number
  overallScore: number
  scoreBreakdown: ScoreBreakdown
  aiExplanation?: string
  status: 'AI_SUGGESTED' | 'RECRUITER_REVIEWED' | 'SHORTLISTED' | 'REJECTED'
  talent: TalentProfile
}

interface ScoreBreakdown {
  overall: number
  skillMatch: number      // weight 35%
  experienceFit: number   // weight 20%
  availability: number    // weight 10%
  pricingFit: number      // weight 10%
  locationMatch: number   // weight 10%
  culturalFit: number     // weight 10%
  feedbackScore: number   // weight 5%
  explanation?: string
}

interface TalentProfile {
  id: string
  firstName: string
  lastName: string
  headline?: string
  summary?: string
  availability: 'IMMEDIATE' | 'TWO_WEEKS' | 'ONE_MONTH' | 'THREE_MONTHS'
  hourlyRate?: number
  currency: string
  location?: string
  remotePreference: 'ONSITE' | 'HYBRID' | 'REMOTE' | 'ANY'
  verificationStatus: 'PENDING' | 'VERIFIED' | 'REJECTED'
  skills: TalentSkill[]
  experience: Experience[]
  certifications: Certification[]
}

interface TalentSkill {
  skill: Skill
  proficiencyLevel: 'BEGINNER' | 'INTERMEDIATE' | 'ADVANCED' | 'EXPERT'
  yearsOfExperience?: number
}

interface Experience {
  id: string
  title: string
  company: string
  startDate: string
  endDate?: string
  isCurrent: boolean
  description?: string
}

interface Certification {
  id: string
  name: string
  issuingOrganization?: string
  issueDate?: string
  expiryDate?: string
  credentialUrl?: string
}

interface Interview {
  id: string
  status: 'SCHEDULED' | 'COMPLETED' | 'CANCELLED' | 'NO_SHOW'
  scheduledAt: string
  duration: number
  meetingUrl?: string
  feedback?: InterviewFeedback
  candidate: TalentProfile
  demand: Demand
}

interface InterviewFeedback {
  rating: number
  notes: string
  skillsDemonstrated: Skill[]
}

interface Offer {
  id: string
  status: 'DRAFT' | 'SENT' | 'ACCEPTED' | 'DECLINED' | 'WITHDRAWN'
  hourlyRate: number
  currency: string
  startDate: string
  endDate?: string
  terms?: string
  sentAt?: string
  respondedAt?: string
  candidate: TalentProfile
  demand: Demand
}

interface Notification {
  id: string
  type: 'MATCH_GENERATED' | 'INTERVIEW_SCHEDULED' | 'OFFER_ACCEPTED' | 'OFFER_DECLINED' | 'DEMAND_APPROVED' | 'DEMAND_REJECTED' | 'VERIFICATION_COMPLETE' | 'SYSTEM_ALERT'
  title: string
  body: string
  isRead: boolean
  createdAt: string
  entityId?: string
  entityType?: string
}
```

---

### 3.2 Per-Page Prompt Additions

For each page, add after the header:

```
Page: [PAGE NAME]
Route: [/route/path]
Role surface: [PUBLIC / RECRUITER / ADMIN]

Purpose: [One sentence what this page does]

Required blocks:
[list from Part 2 spec for this page]

GraphQL operations needed:
- Query: [queryName] — fields: [field list]
- Mutation: [mutationName] — input: [input fields]

States to implement:
- Loading: [skeleton description]
- Empty: "[exact empty state copy]"
- Error: "[exact error state copy]"
- Success: "[exact success feedback copy]"

Specific constraints:
[any per-page rule from this spec]
```

---

### 3.3 Delivery Sequence for Bolt.new

Work in this order — each group is one bolt prompt session:

**Pre-work (before any page — generate once):**
0a. Tailwind config (`tailwind.config.ts` token extension)
0b. globals.css starter (font faces + CSS variables)
0c. Shared types file (`types/marketplace.ts` — from §3.1a interfaces)
0d. Motion constants (`lib/motion.ts` — from §1.6 tokens)
0e. Chart theme config (`lib/chart-theme.ts` — from §1.10)

**Shared components (generate once, before Group 2):**
- `components/ui/score-breakdown.tsx` — ScoreBreakdown component (§1.13)
- `components/ui/candidate-profile-modal.tsx` — full modal (§2.2, Role Detail Tab 2)
- `components/ui/kpi-row.tsx` — KPI container with cells
- `components/ui/status-badge.tsx` — Status chip
- `components/ui/empty-state.tsx` — Empty state with icon/title/body/CTA
- `components/ui/skeleton-rows.tsx` — Table skeleton loader
- `components/ui/notification-center.tsx` — Notification panel (§1.14)
- `components/modals/confirm-action-modal.tsx` — Confirm action (§2.5)
- `components/modals/skill-selector-modal.tsx` — Skill selector (§2.5)
- `components/modals/schedule-interview-modal.tsx` — Schedule interview (§2.5)
- `components/modals/draft-offer-modal.tsx` — Draft offer (§2.5)
- `components/layout/sidebar.tsx` — Sidebar nav (§1.7)
- `components/layout/topbar.tsx` — Top bar (§1.7)
- `components/ui/data-table.tsx` — Reusable data table (§1.24)
- `lib/apollo-provider.tsx` — ApolloWrapper client provider (§1.25) — **check if exists first**

**Group 1 — Auth + Public**
1. `/` (landing page)
2. `/login`
3. `/register`
4. `/forgot-password`
5. `/reset-password`
6. `app/not-found.tsx` + `app/error.tsx` + `app/loading.tsx`

**Group 2 — Recruiter Core**
7. `/dashboard` (dashboard home)
8. `/dashboard/roles` (roles list) ← use §3.4 as prompt template
9. `/dashboard/roles/new` (create role + AI panel) ← use §3.7 as exact prompt
10. `/dashboard/roles/[id]` (role detail, all 4 tabs)

**Group 3 — Recruiter Workflow**
11. `/dashboard/shortlists`
12. `/dashboard/search`
13. `/dashboard/interviews`
14. `/dashboard/interviews/[demandId]/[interviewId]`
15. `/dashboard/offers`
16. `/dashboard/offers/[demandId]/[offerId]`
17. `/dashboard/analytics` ← use §3.8 as prompt template

**Group 4 — Admin**
18. `/admin`
19. `/admin/users`
20. `/admin/verification` ← use §3.6 as exact prompt
21. `/admin/companies`
22. `/admin/approvals`
23. `/admin/concierge`
24. `/admin/analytics` ← use §3.8 as prompt template

**Group 5 — Settings**
25. `/settings` (profile, security, notifications tabs)

---

### 3.4 Complete Worked Prompt Example

This is a fully written bolt.new prompt for `/dashboard/roles`. Use it as the exact template for all other pages — structure, depth, and specificity are consistent with what bolt needs to produce production-quality output.

---

```
[SYSTEM HEADER — paste from §3.1 before this block]

---

Page: Roles List
Route: /dashboard/roles
Role surface: RECRUITER (auth guard handled externally)

Purpose: Displays all demands created by the authenticated recruiter. Recruiter monitors pipeline status, filters by stage, and navigates into individual role detail.

---

LAYOUT:
- App shell: Sidebar (240px, bg-surface, border-r border-border) + TopBar (56px, bg-surface, border-b border-border) + main content area
- Sidebar nav items: exact list from §1.17 Recruiter Sidebar — "Roles" item is active
- TopBar breadcrumb: "Roles / Role Demands"
- Content padding: 32px, max-width 1280px

---

PAGE HEADER ROW (top of content area):
- Left: title "Role Demands" (text-2xl font-bold text-text-primary) + subtitle "Monitor demand status and move roles through the pipeline." (text-sm text-text-secondary, mt-1)
- Right: "New Role" primary button (Briefcase icon, bg-primary text-text-inverse rounded-md h-10 px-4, hover:bg-primary-hover shadow-glow on hover) — navigates to /dashboard/roles/new

COMMAND ROW (below page header, mt-6):
- Left: search input (height 40px, bg-surface-alt border border-border rounded-md, Search icon left, placeholder="Search by title or skill...", text-sm) — client-side filter of loaded data, debounced 300ms
- Center: status filter tabs — "All | Active | Draft | Paused | Filled | Cancelled" (pill-style tabs, active=bg-primary-muted text-text-primary border-b-2 border-primary, inactive=text-text-secondary hover:text-text-primary)
- Right: sort dropdown — "Newest | Oldest | Most Candidates | Urgency" (ghost dropdown, ChevronDown icon, text-sm)

---

DEMAND TABLE:
Container: bg-surface border border-border rounded-lg mt-4 overflow-hidden

Table header row:
  background: bg-surface, border-b border-border
  Cell style: text-xs font-semibold uppercase tracking-wide text-text-muted px-4 py-3
  Columns (in order):
    1. "Role Title" — sorted by default, ArrowUpDown icon on hover
    2. "Company"
    3. "Status"
    4. "Required Skills"
    5. "Shortlisted"
    6. "Budget Range"
    7. "Posted Date"
    8. "" (actions column — no header)

Table data rows:
  Height: h-14 (56px)
  Cell style: text-sm text-text-primary px-4 py-3
  Border: border-b border-border-subtle
  Hover: bg-surface-high transition-colors duration-150
  Click anywhere on row: navigate to /dashboard/roles/[id]

  Column 1 — Role Title:
    Link style: font-medium text-text-primary hover:text-primary cursor-pointer

  Column 2 — Company:
    text-text-secondary

  Column 3 — Status:
    StatusBadge component — see §1.2 Status Badge table for colors
    ACTIVE: bg=success-muted text=success
    DRAFT: bg=surface-high text=text-secondary
    PAUSED: bg=warning-muted text=warning
    FILLED: bg=info-muted text=info
    CANCELLED: bg=destructive-muted text=destructive

  Column 4 — Required Skills:
    First 3 skills as chips (text-xs bg-primary-muted text-primary border border-primary-border rounded-full px-2 py-0.5)
    If more: "+N" chip (same style, bg-surface-high text-text-secondary)

  Column 5 — Shortlisted:
    Number centered, text-sm. If 0: text-muted. If >0: bold text-primary.

  Column 6 — Budget Range:
    "$X – $Y / hr" or "Not set" (text-muted) if no budget defined

  Column 7 — Posted Date:
    Relative format: "3 days ago" (use date-fns formatDistanceToNow)

  Column 8 — Actions:
    MoreHorizontal icon button (ghost, h-8 w-8)
    Dropdown menu on click:
      - "View" → navigate to /dashboard/roles/[id] (ExternalLink icon)
      - "Edit" → navigate to /dashboard/roles/[id]?edit=true (Pencil icon)
      - separator
      - "Pause" (visible if status=ACTIVE) → pauseDemand mutation, confirm first (AlertTriangle icon, warning text)
      - "Archive" (visible if status≠CANCELLED) → cancelDemand mutation, confirm first (Trash2 icon, destructive text)

---

PAGINATION:
Position: bottom of table container, px-4 py-3, border-t border-border
Left: "Showing 1–20 of [total] demands" — text-sm text-text-muted
Right: "Previous" | "Next" buttons — ghost, h-8 px-3 rounded-md, disabled at boundary
Default: 20 rows per page, cursor-based

---

STATES:

Loading state:
  Render 5 skeleton rows in the table body
  Each row: same height as data rows, cells contain animate-pulse rounded bg-surface-high bars
  Widths: col1=48%, col2=16%, col3=12%, col4=12%, col5=4%, col6=12%, col7=12%, col8=4%
  Show skeleton after 200ms delay (do not flash for fast loads)
  aria-busy="true" on table container

Empty state (zero demands, no filter applied):
  Centered in table body, min-height 320px
  Briefcase icon (48px, text-text-muted)
  Title: "No roles yet." (text-base font-semibold text-text-primary, mt-4)
  Body: "Create your first role demand to start generating AI-matched shortlists." (text-sm text-text-secondary, mt-2, max-w-xs)
  CTA: "Create Role" primary button (mt-6) → /dashboard/roles/new

Empty state (zero results after filter/search):
  Same structure but:
  Title: "No roles match your filters."
  Body: "Try clearing the search or selecting a different status."
  CTA: "Clear Filters" ghost button → resets search + sets tab to "All"

Error state:
  Centered, AlertTriangle icon (48px, text-warning)
  Title: "We couldn't load your roles."
  Body: "Check your connection and try again."
  CTA: "Retry" ghost button → re-triggers query

---

GRAPHQL HOOKS (write hooks with correct names, leave body as comment):
// TODO: wire GraphQL
const { data, loading, error, refetch } = useQuery(MY_DEMANDS_QUERY, {
  variables: { filters: activeFilters, first: 20, after: cursor }
})
// MY_DEMANDS_QUERY uses operation name: myDemands
// Return fields: id, title, status, company{name}, requiredSkills{id,name}, shortlistCount, budgetMin, budgetMax, currency, createdAt

const [pauseDemand] = useMutation(PAUSE_DEMAND_MUTATION, {
  onCompleted: () => toast.success('Role paused.'),
  onError: () => toast.error('Could not pause role. Try again.'),
  refetchQueries: ['myDemands'],
})
const [cancelDemand] = useMutation(CANCEL_DEMAND_MUTATION, {
  onCompleted: () => toast.success('Role archived.'),
  onError: () => toast.error('Could not archive role. Try again.'),
  refetchQueries: ['myDemands'],
})

---

ANIMATIONS:
- Page container: Framer Motion initial={opacity:0, y:12} animate={opacity:1, y:0} transition={duration:0.22, ease:[0.2,0.8,0.2,1]}
- Table rows: staggerChildren 0.03s on list container (only on initial mount, not on refetch)

---

TYPES: Use interfaces from §3.1a — specifically Demand, Company, Skill, User. No `any`.

---

OUTPUT EXPECTED:
- app/dashboard/roles/page.tsx (page component, server or client as appropriate)
- components/roles/demand-table.tsx (table component)
- components/roles/demand-row.tsx (single row, handles actions dropdown)
- components/roles/demand-filters.tsx (search + tab + sort bar)
```

---

### 3.5 Per-Page Prompt Checklist

Before sending any page prompt to bolt, verify:

- [ ] §3.1 mandatory header included in full
- [ ] TypeScript interfaces from §3.1a referenced
- [ ] All column names, widths, and data formats specified
- [ ] Every state (loading/empty/empty-filtered/error/success) explicitly written
- [ ] GraphQL operation names match §4.4 exactly
- [ ] Motion entry animation specified
- [ ] Toast feedback copy written for every mutation outcome
- [ ] Icon names (lucide-react) specified for every icon used
- [ ] `aria-busy`, `aria-label`, `role` attributes called out where needed

---

### 3.6 Complete Worked Prompt — `/admin/verification` (Split-Pane Pattern)

This fully-written bolt.new prompt demonstrates the **split-pane layout pattern** used by `/admin/verification` and `/admin/approvals`. Use it as the template for all split-pane admin pages.

---

**PROMPT:**

```
[PASTE §3.1 MANDATORY HEADER HERE — full block, unchanged]

---

Page: Talent Verification
Route: /admin/verification
Role surface: ADMIN only (if non-admin session: redirect to /login)

Purpose: Review pending talent verification submissions. Admins approve or reject identity documents and certifications uploaded by talent users.

---

LAYOUT — SPLIT-PANE (full height, no scroll on outer container):

Left panel (w-80 min-w-[320px], flex-shrink-0):
  bg-[#0A0A0A] border-r border-[#27272A] h-full overflow-y-auto
  Top: tab row — "Pending" | "Approved" | "Rejected"
    Active tab: border-b-2 border-[#EFFE5E] text-white
    Inactive tab: text-[#A1A1AA] hover:text-white
  Below tabs: list of verification entries (see Left List spec below)

Right panel (flex-1):
  bg-[#000000] h-full overflow-y-auto
  Content: verification detail panel OR empty prompt if no item selected (see Right Panel spec)

---

LEFT LIST — Verification Entry Row:

Each row in the list:
  - Padding: px-4 py-3
  - Selected state: bg-[#1A1A1A] border-l-2 border-[#EFFE5E]
  - Hover: bg-[#1A1A1A] cursor-pointer
  - Layout: flex items-start gap-3

  Left: Avatar — 36px circle, initials fallback (bg-[#27272A] text-white text-xs)
  Right: flex flex-col gap-0.5
    Name: text-sm font-medium text-white
    Headline: text-xs text-[#A1A1AA] truncate max-w-[180px]
    Row below: text-xs text-[#52525B] — "Submitted [relative time]" · "[N] documents"

  Empty state for each tab:
    Pending: icon=ShieldCheck (32px #A1A1AA) · "Verification queue is clear." · "All submitted profiles have been reviewed."
    Approved: "No approved verifications yet."
    Rejected: "No rejected verifications."

---

RIGHT PANEL — No Item Selected (default):

Center the following vertically and horizontally in the panel:
  Icon: ShieldCheck 48px text-[#27272A]
  Title: text-lg font-semibold text-[#A1A1AA] — "Select a submission to review"
  Body: text-sm text-[#52525B] — "Choose a pending verification from the left panel."

---

RIGHT PANEL — Item Selected (verification detail):

Page-enter animation: motion.div initial={{ opacity: 0, x: 12 }} animate={{ opacity: 1, x: 0 }} transition={{ duration: 0.22 }}

Top section — Talent Profile Summary:
  Padding: p-6 border-b border-[#27272A]
  Layout: flex items-start gap-4
  Left: Avatar 48px
  Right:
    Name: text-xl font-bold text-white
    Headline: text-sm text-[#A1A1AA]
    Row: availability chip + rate + location (text-xs text-[#52525B])
  Far right: Status badge using status colors from §1.2 / §1.21

Skills section:
  Padding: px-6 py-4 border-b border-[#27272A]
  Label: "Verified Skills" text-xs uppercase tracking-wider text-[#A1A1AA] mb-2
  Skill chips: flex flex-wrap gap-2, each chip bg-[#1A1A1A] border border-[#27272A] text-white text-xs px-2 py-0.5 rounded-[4px]

Experience summary:
  Padding: px-6 py-4 border-b border-[#27272A]
  Label: "Experience" text-xs uppercase tracking-wider text-[#A1A1AA] mb-2
  List: 2–3 most recent experience entries, each: title + company + dates (text-sm text-white + text-xs text-[#52525B])

Documents section:
  Padding: px-6 py-4 border-b border-[#27272A]
  Label: "Submitted Documents" text-xs uppercase tracking-wider text-[#A1A1AA] mb-3
  Each document row:
    Icon: FileText 16px text-[#A1A1AA]
    Filename: text-sm text-white flex-1
    Type badge: tiny chip (e.g. "Identity" | "Certificate")
    Action: "Download" — ghost button, ExternalLink icon
  If no documents: "No documents submitted." text-[#52525B]

Verification history:
  Padding: px-6 py-4 border-b border-[#27272A]
  Label: "Review History" text-xs uppercase
  If empty: "No previous review actions."
  Entry: [reviewer name] [action: Approved/Rejected] [timestamp] [reason if rejected]

Decision controls:
  Padding: px-6 py-6 sticky bottom-0 bg-[#000000] border-t border-[#27272A]
  Layout: flex items-center gap-3 justify-end
  "Reject" button: variant="outline" border-[#EF4444] text-[#EF4444] hover:bg-red-950 → opens reject modal
  "Approve Profile" button: bg-[#EFFE5E] text-black font-semibold hover:bg-[#c6f030] → calls approveTalentVerification mutation directly

---

REJECT MODAL:

Triggered by "Reject" button. Uses shared ConfirmActionModal pattern:
  Width: 480px
  Icon: AlertTriangle 24px text-[#EF4444]
  Title: "Reject this verification?"
  Body: text-sm text-[#A1A1AA] — "The talent will be notified and asked to resubmit with corrections."
  Required reason field:
    label: "Reason for rejection" text-xs text-[#A1A1AA]
    textarea: bg-[#1A1A1A] border border-[#27272A] min-h-[80px] text-white
    placeholder: "Describe what documents are missing or incorrect..."
    validation: required, min 10 characters
  Buttons (right-aligned):
    "Cancel" ghost
    "Confirm Rejection" bg-[#EF4444] text-white — calls rejectTalentVerification(id, reason)

---

GRAPHQL OPERATIONS:

// TODO: wire GraphQL — replace all mock data with these hooks
const { data, loading, error } = useQuery(TALENT_VERIFICATION_QUEUE, {
  variables: { status: activeTab.toUpperCase() },    // 'PENDING' | 'APPROVED' | 'REJECTED'
  fetchPolicy: 'cache-and-network',
})

// Selected item detail (fetch on selection)
const { data: detail, loading: detailLoading } = useQuery(TALENT_VERIFICATION_DETAIL, {
  variables: { talentId: selectedId },
  skip: !selectedId,
})

const [approveVerification, { loading: approving }] = useMutation(APPROVE_TALENT_VERIFICATION, {
  onCompleted: () => {
    toast.success('Profile approved. Talent is now verified.')
    refetch()
  },
  onError: () => toast.error('Approval failed. Please try again.'),
})

const [rejectVerification, { loading: rejecting }] = useMutation(REJECT_TALENT_VERIFICATION, {
  onCompleted: () => {
    toast.success('Verification rejected. Talent has been notified.')
    setRejectModalOpen(false)
    refetch()
  },
  onError: () => toast.error('Rejection failed. Please try again.'),
})

---

STATES:

Loading (left list):
  Skeleton rows: 5 rows, each [36px circle skeleton] + [two line text skeletons] — bg-[#222222] animate-pulse

Loading (right panel detail — on selection):
  3 skeleton sections: [summary bar], [skills row], [documents list]
  Each skeleton item: bg-[#222222] animate-pulse rounded

Error (left list):
  Icon: AlertCircle 32px text-[#EF4444]
  "We couldn't load the verification queue."
  "Check your connection and try again." → [Retry] button

Empty queue (Pending tab):
  Icon: ShieldCheck 48px text-[#27272A]
  "Verification queue is clear."
  "All submitted talent profiles have been reviewed."
  No CTA needed.

Approve in-progress ("Approve Profile" button):
  Show spinner inside button, disable both action buttons during mutation

---

COMPONENT FILE EXPECTATIONS:

Expected output files from bolt:
- app/(admin)/admin/verification/page.tsx
- components/admin/verification-queue-list.tsx   (left panel list + tabs)
- components/admin/verification-detail-panel.tsx  (right panel, full detail)
- components/admin/verification-document-row.tsx  (single document display row)
- components/modals/reject-verification-modal.tsx (reject modal, reuses ConfirmActionModal shell)

---

DARK MODE REQUIREMENT: This is a dark-only application — no white backgrounds anywhere. No default shadcn/ui theme colors. Every surface uses the dark token system. Modal background: bg-[#1A1A1A]. Input fields: bg-[#1A1A1A] border-[#27272A].
```

---

### 3.7 Complete Worked Prompt — `/dashboard/roles/new` (Two-Column Form + AI Panel)

This is the most complex page in the recruiter surface. It combines a multi-section form with a real-time AI assistant panel. Use this prompt as the exact template for any two-column form page.

---

**PROMPT:**

```
[PASTE §3.1 MANDATORY HEADER HERE — full block, unchanged]

---

Page: Create Role
Route: /dashboard/roles/new
Role surface: RECRUITER (redirect to /login if unauthenticated)

Purpose: Post a new talent demand. The recruiter fills in role details and requirements, then optionally uses the AI assistant to generate a polished description. The final demand is saved as DRAFT or published directly.

---

LAYOUT — TWO-COLUMN (form + AI panel):

Outer shell: DashboardLayout (sidebar + topbar, from §1.8)
Page container: max-w-7xl mx-auto px-6 py-8

page-enter animation: motion.div initial={{ opacity: 0, y: 10 }} animate={{ opacity: 1, y: 0 }} transition={{ duration: 0.22 }}

Two columns (flex-row gap-8):
  Left: flex-1  (form fields — scrollable)
  Right: w-[420px] flex-shrink-0 (AI panel — sticky top-[80px])

Page heading (above both columns, full width):
  Breadcrumb: Roles / Create New Role (text-xs text-[#A1A1AA], with / separator)
  Title: "Create New Role" — text-2xl font-bold text-white
  Subtitle: "Define what you need. AI will help you say it right." — text-sm text-[#A1A1AA]

---

LEFT — FORM FIELDS:

Form container: bg-[#0A0A0A] border border-[#27272A] rounded-[4px] p-6 space-y-8

Form sections are separated by <Separator className="bg-[#27272A]" /> between each section.

SECTION 1 — Role Basics:
  Section title: "Role Basics" text-xs font-semibold uppercase tracking-widest text-[#A1A1AA] mb-4
  
  Role Title (required):
    label: "Role Title" + red * asterisk
    input: type=text, placeholder="e.g. Senior React Engineer"
    error: "Role title is required."

  Experience Level (required):
    label: "Experience Level"
    Select component (shadcn) — dark override: bg-[#1A1A1A] border-[#27272A]
    Options: Junior | Mid | Senior | Lead | Executive
    Default: "Select level..."

  Location (optional):
    label: "Location" 
    input: type=text, placeholder="e.g. London, UK or Remote"
    helper text (below): "Leave blank if location is flexible."

  Remote Policy (required):
    label: "Remote Policy"
    Radio group (3 options, horizontal): Onsite | Hybrid | Remote
    Each option: flex items-center gap-2, radio dot in Spriteburst when checked
    Default: unselected

SECTION 2 — Skills & Requirements:
  Section title: "Skills & Requirements"

  Required Skills:
    label: "Required Skills"
    Input with search: type=text, placeholder="Search or add skills..."
    As user types: show dropdown list of matching skills from `skills(search)` query
    Each dropdown item: skill name — click adds as chip below
    Selected skills: flex flex-wrap gap-2 mt-2
    Skill chip: bg-[#1A1A1A] border border-[#EFFE5E] text-xs text-white px-2 py-1 rounded-[4px] + × button
    × button: text-[#A1A1AA] hover:text-white
    No match found: "Add '[query]' as new skill" option at bottom of dropdown → creates skill
    Validation: at least 1 skill required before publish (not before save-draft)

  Project Requirements:
    label: "Project Requirements" (optional)
    textarea: rows=3, bg-[#1A1A1A] border-[#27272A], placeholder="Any specific requirements, certifications, or context for this role..."
    char counter: "250/500" text-xs text-[#52525B] right-aligned below
    maxLength: 500

SECTION 3 — Timeline & Budget:
  Section title: "Timeline & Budget"

  Two-column sub-grid (grid grid-cols-2 gap-4):
    Start Date: label + DatePicker component — dark override (see §1.23)
    Contract Duration: label + input text, placeholder="e.g. 3 months"

  Two-column sub-grid:
    Budget Min ($): label + input type=number, prefix "$", currency select inline right (default USD)
    Budget Max ($): same pattern — must be ≥ Budget Min (cross-field validation)
    Validation error (inline below Budget Max): "Max budget must exceed minimum budget."

SECTION 4 — Your Notes:
  Section title: "Your Notes"
  Sub-label (body text, text-sm text-[#A1A1AA] mb-3):
    "Describe what you need in your own words. The AI assistant will transform this into a structured role description."
  Textarea: rows=6, bg-[#1A1A1A] border-[#27272A], placeholder="e.g. We need a React developer who knows the fintech space and can work independently. Must be comfortable with TypeScript and GraphQL..."
  Char counter: "0/2000" right-aligned below
  maxLength: 2000
  This field drives the "Enhance with AI" action in the right panel.

FINAL DESCRIPTION FIELD (below all sections, full width):
  label: "Final Role Description" 
  Small helper (text-xs text-[#52525B]): "This is what talent will see. Fill manually or accept the AI version."
  textarea: rows=8, bg-[#1A1A1A] border-[#27272A] — starts empty, populated by "Use This Description" in AI panel

---

FORM ACTION BAR (sticky bottom):
  Position: sticky bottom-0, bg-[#000000] border-t border-[#27272A] px-6 py-4
  Layout: flex items-center justify-between
  Left: "Back to Roles" — ghost button with ChevronLeft icon → /dashboard/roles (no confirmation needed if form untouched; show confirm dialog if dirty)
  Right (flex gap-3):
    "Save as Draft" — outline variant, calls createDemand({ ...fields, status: 'DRAFT' })
    "Publish Role" — primary Spriteburst, calls createDemand({ ...fields, status: 'ACTIVE' })
  Both buttons: show spinner + disabled during mutation, re-enable on error

---

RIGHT — AI PANEL:

Panel container: bg-[#0A0A0A] border border-[#27272A] rounded-[4px] p-5 sticky top-[80px] max-h-[calc(100vh-120px)] overflow-y-auto

Panel header:
  Icon: Sparkles 18px text-[#EFFE5E]
  Title: "AI Role Assistant" — text-base font-semibold text-white
  Subtitle: "Generate a polished description from your notes." — text-xs text-[#A1A1AA]

Divider: bg-[#27272A] my-4

STATE A — Idle (default, no generation triggered):
  Illustration placeholder: 160×120px area, bg-[#1A1A1A] border border-dashed border-[#27272A] rounded-[4px] flex items-center justify-center
    Inner: FileText 32px text-[#27272A]
  Body text (text-sm text-[#52525B] text-center mt-3):
    "Fill in your notes and click Enhance with AI."
  
  Button: "Enhance with AI" — full-width, primary Spriteburst, Sparkles icon left
  Disabled condition: "Your Notes" textarea is empty (show tooltip on hover: "Add some notes first")

STATE B — Loading (after button clicked):
  Hide illustration and button
  Show loading shimmer container (same dimensions as STATE C result):
    5 shimmer bars of varying width (bg-[#222222] animate-pulse h-3 rounded my-2)
  Status text: text-xs text-[#A1A1AA] text-center mt-3 — "Analyzing your role requirements..."
  
  // TODO: wire GraphQL
  const [generateDescription, { loading: aiLoading }] = useMutation(GENERATE_ROLE_DESCRIPTION, {
    variables: { input: { title, level, skills, notes: watchedNotes } },
    onCompleted: (data) => setAiResult(data.generateRoleDescription),
    onError: () => toast.error('AI generation failed. Try again or write your description manually.'),
  })

STATE C — Result shown:
  All content in a flex flex-col gap-4 space:

  Generated Role Title section:
    Label: text-[11px] uppercase tracking-wider text-[#A1A1AA] — "Suggested Title"
    Value: text-base font-semibold text-white — aiResult.suggestedTitle
    
  Role Summary section:
    Label: "Summary"
    Body: text-sm text-[#A1A1AA] leading-relaxed — aiResult.summary

  Responsibilities section:
    Label: "Responsibilities"
    Bulleted list (ul, li): text-sm text-[#A1A1AA], bullet color Spriteburst (text-[#EFFE5E] mr-2)
    
  Requirements section:
    Label: "Requirements"
    Bulleted list: same pattern
    
  Nice-to-Haves section:
    Label: "Nice to Have"
    Bulleted list: text-[#52525B] (lighter — lower priority)

  Suggested Skills section:
    Label: "AI Suggested Skills"
    Row of skill chips: bg-[#1A1A1A] border border-[#27272A] text-xs text-[#A1A1AA] px-2 py-0.5
    Each chip: "+ Add" micro-button inline — adds to required skills field on left
    
  Action buttons (below result, full width, flex gap-2):
    "Use This Description" — full-width primary Spriteburst — fills Final Description textarea with formatted text
    "Try Again" — full-width ghost — re-triggers generateRoleDescription mutation
    "Edit Manually" — text button (text-xs text-[#52525B] underline) — opens Final Description textarea and focuses it

STATE D — Error:
  Icon: AlertCircle 24px text-[#EF4444] centered
  Text: text-sm text-[#A1A1AA] text-center — "AI generation failed."
  Sub: text-xs text-[#52525B] — "Try again or write your description manually."
  Button: "Try Again" — ghost full-width

---

GRAPHQL OPERATIONS:

// TODO: wire GraphQL — createDemand mutation
const [createDemand, { loading: creating }] = useMutation(CREATE_DEMAND, {
  onCompleted: (data) => {
    const id = data.createDemand.id
    const status = data.createDemand.status
    if (status === 'ACTIVE') {
      toast.success('Role published. AI is generating your shortlist — check back in a moment.')
    } else {
      toast.success('Role saved as draft.')
    }
    router.push(`/dashboard/roles/${id}`)
  },
  onError: (err) => {
    toast.error('Role could not be created. Check required fields and try again.')
  },
})

// Skills search (debounced, min 2 chars)
const [skillSearch, setSkillSearch] = useState('')
const { data: skillsData } = useQuery(SEARCH_SKILLS, {
  variables: { search: skillSearch },
  skip: skillSearch.length < 2,
  debounce: 300,
})

---

STATES:

Loading — Submit:
  "Publish Role" button: show Loader2 icon animate-spin 16px, text "Publishing...", disabled
  "Save as Draft" button: disabled
  Form fields: disabled (pointer-events-none opacity-60)

Error — Validation:
  Each required field shows error below it (text-xs text-[#EF4444])
  summarize-errors banner is NOT used — field-level errors only
  Scroll to first error field on submit attempt

Success — Draft saved:
  toast.success("Role saved as draft.") — bottom-right sonner toast
  No redirect — stay on page to allow continued editing

Success — Published:
  toast.success("Role published. AI is generating your shortlist — check back in a moment.")
  router.push('/dashboard/roles/[new id]')

Dirty form — Back navigation:
  If form has been touched: show ConfirmActionModal
  Title: "Leave without saving?"
  Body: "Your role details will be lost."
  Confirm: "Leave" (destructive)
  Cancel: "Stay on Page"

---

COMPONENT FILE EXPECTATIONS:

Expected output files from bolt:
- app/(dashboard)/dashboard/roles/new/page.tsx         (main page, form + layout)
- components/roles/create-role-form.tsx                (left panel — all form sections)
- components/roles/ai-description-panel.tsx            (right panel — AI states A/B/C/D)
- components/roles/skill-input.tsx                     (skills search + chips component)
- schemas/create-demand-schema.ts                      (Zod schema for full form — see §1.20)

---

DARK MODE REQUIREMENT: This is a dark-only application. No white backgrounds anywhere. Every input, dropdown, textarea, select trigger, date picker, and modal must use dark token overrides. See §1.23 for exact CSS class overrides per component type.
```

---

### 3.8 Complete Worked Prompt — `/dashboard/analytics` (Charts + KPI + Table Pattern)

The analytics page is the most render-intensive page in the recruiter surface. It stacks 6 KPI cells, 4 Recharts charts, and a sortable data table. This worked prompt is the template for both `/dashboard/analytics` and `/admin/analytics`.

---

**PROMPT:**

```
[PASTE §3.1 MANDATORY HEADER HERE — full block, unchanged]

---

Page: Recruiter Analytics
Route: /dashboard/analytics
Role surface: RECRUITER (redirect to /login if unauthenticated)

Purpose: Show a recruiter their hiring performance — pipeline conversion, velocity trends, skills demand, and role aging. All data is aggregated from their demands, shortlists, interviews, and offers.

---

LAYOUT — ANALYTICS SHELL:

Outer shell: DashboardLayout (sidebar + topbar)
Page container: max-w-7xl mx-auto px-6 py-8
page-enter animation: motion.div initial={{ opacity: 0, y: 10 }} animate={{ opacity: 1, y: 0 }} transition={{ duration: 0.22 }}

Full-width sections stacked vertically (flex flex-col gap-8):
1. Page header
2. Filter bar
3. KPI row
4. Charts grid (2-column on desktop, 1-column on mobile)
5. Data table

---

PAGE HEADER:
  Title: "Analytics" — text-2xl font-bold text-white
  Subtitle: "Hiring performance across all your roles." — text-sm text-[#A1A1AA]
  Right side (flex-end): "Export Report" button — ghost variant, Download icon 16px
    → on click: download CSV of all visible data (leave as // TODO: implement export)

---

FILTER BAR:
  bg-[#0A0A0A] border border-[#27272A] rounded-[4px] px-4 py-3 flex items-center gap-3
  Label: text-xs text-[#A1A1AA] — "Showing data for:"
  Preset buttons (toggle group, one active at a time):
    "Last 30 days" | "Last 90 days" | "Last 180 days" | "All time"
    Active: bg-[#1A1A1A] border border-[#27272A] text-white
    Inactive: text-[#A1A1AA] hover:text-white
  Right: Date range picker — from/to date inputs (dark override §1.23)
  Note: date range picker and preset tabs are mutually exclusive — selecting one clears the other

---

KPI ROW:
  Uses KPIRow component from §1.22, 6 cells:
  1. "Roles Posted"        value: stats.totalDemands          accent: true
  2. "Shortlisted"         value: stats.totalShortlisted
  3. "Interviews"          value: stats.totalInterviews
  4. "Offers Accepted"     value: stats.offersAccepted
  5. "Avg. Days to Hire"   value: stats.avgDaysToHire + " days"
  6. "Fill Rate"           value: stats.fillRate + "%"   trend: delta vs previous period

---

CHARTS GRID:
  Layout: grid grid-cols-1 lg:grid-cols-2 gap-6
  Each chart: bg-[#0A0A0A] border border-[#27272A] rounded-[4px] p-5

  CHART CONTAINER PATTERN:
    Header (flex items-center justify-between mb-4):
      Title: text-sm font-semibold text-white
      Subtitle (optional): text-xs text-[#A1A1AA] ml-2
    Chart body: ResponsiveContainer width="100%" height={260}
    All charts: 'use client' required (recharts uses browser APIs)

  CHART 1 — Hiring Velocity (LineChart, spans full width: col-span-2):
    Title: "Hiring Velocity" + subtitle "Last 12 weeks"
    X axis: week labels ("W1", "W2" ... "W12") — text-[#52525B] text-xs
    Y axis: count — text-[#52525B] text-xs
    Grid: CartesianGrid strokeDasharray="3 3" stroke="#27272A"
    4 Lines:
      1. Demands created — stroke "#EFFE5E" (Spriteburst)
      2. Shortlists generated — stroke "#FFFFFF"
      3. Interviews — stroke "#F59E0B"
      4. Offers — stroke "#3B82F6"
    Legend: below chart, custom legend with colored squares + labels (text-xs text-[#A1A1AA])
    Tooltip: dark custom tooltip (background #1A1A1A, border #27272A, text white, font Larsseit)
    Empty state: show axes with "No data for this period" text centered in chart area (text-[#52525B])
    Data field: analyticsData.velocityWeeks (array of { week, demands, shortlists, interviews, offers })

  CHART 2 — Pipeline Conversion (BarChart, single series):
    Title: "Pipeline Conversion"
    X axis: stages — "Posted" | "Shortlisted" | "Interviewed" | "Offer Sent" | "Accepted"
    Y axis: count
    Bars: fill "#EFFE5E", radius [4,4,0,0]
    Data labels above each bar: count + conversion % from previous stage (text-xs text-[#A1A1AA])
    Tooltip: dark custom
    Data field: analyticsData.pipelineConversion (array of { stage, count, conversionFromPrev })

  CHART 3 — Top Skills in Demand (BarChart, horizontal):
    Title: "Top Skills in Demand" + subtitle "Across all your roles"
    Layout: horizontal bars (layout="vertical")
    Y axis: skill names — text-[#A1A1AA] text-xs, width={120}
    X axis: count — text-[#52525B] text-xs
    Bars: fill "#EFFE5E", radius [0,4,4,0]
    Top 10 skills, sorted descending
    Data field: analyticsData.topSkills (array of { skill, count })

  CHART 4 — Role Aging (BarChart, grouped by bucket):
    Title: "Role Aging Distribution" + subtitle "Days open"
    X axis buckets: "0–7d" | "8–14d" | "15–30d" | "31–60d" | "60+d"
    Y axis: number of roles
    Bar fill: #EFFE5E for ≤30d buckets, #F59E0B for 31–60d, #EF4444 for 60+d (warning hierarchy)
    Tooltip: dark custom + note "Roles open 30+ days risk talent drop-off"
    Data field: analyticsData.roleAging (array of { bucket, count })

---

DATA TABLE — Role Performance:
  Uses DataTable component from §1.24
  Title row (above table): "Role Performance" text-sm font-semibold text-white
  Columns:
    1. Role Title          — text-sm text-white font-medium, link to /dashboard/roles/[id]
    2. Status              — StatusBadge component
    3. Posted Date         — text-sm text-[#A1A1AA], formatted date
    4. Days Open           — text-sm text-white; if > 30: amber text; if > 60: red text
    5. Shortlisted         — number
    6. Interviews          — number
    7. Offers Sent         — number
    8. Stage               — text-xs text-[#A1A1AA] (e.g. "Interview stage")
  Sortable columns: Posted Date, Days Open, Shortlisted (default sort: Posted Date desc)
  Pagination: 10 per page, bottom pagination bar
  Empty state: "No roles yet. Post your first role to see performance data." + [Create Role] CTA

---

GRAPHQL OPERATIONS:

// TODO: wire GraphQL
'use client'
import { useQuery } from '@apollo/client'

const [dateFilter, setDateFilter] = useState<{ from: Date | null; to: Date | null }>({
  from: subDays(new Date(), 30),  // default: last 30 days
  to: new Date(),
})

const { data, loading, error, refetch } = useQuery(RECRUITER_ANALYTICS, {
  variables: {
    dateFrom: dateFilter.from?.toISOString(),
    dateTo: dateFilter.to?.toISOString(),
  },
  fetchPolicy: 'cache-and-network',
})

const analyticsData = data?.recruiterAnalytics

---

STATES:

Loading — KPI row:
  KPIRow loading={true} prop → shows 6 skeleton cells (bg-[#222222] animate-pulse)

Loading — each chart:
  Replace chart body with skeleton: bg-[#222222] animate-pulse w-full h-[260px] rounded-[4px]

Loading — table:
  DataTable loading={true} → 10 skeleton rows

Error:
  Show single error banner above KPI row:
  bg-[#1A1A1A] border-l-2 border-[#EF4444] px-4 py-3
  "We couldn't load your analytics. Check your connection and try again."
  [Retry] ghost button → refetch()

Empty (no data for period):
  KPI cells all show "—" (em-dash) not 0
  Charts show axes with "No data for this period" centered text in chart area
  Table shows empty state: "No roles found for this period."

Export CSV:
  // TODO: implement — call /api/analytics/export with current dateFilter params
  For now: toast.info('Export coming soon.')

---

COMPONENT FILE EXPECTATIONS:

Expected output files from bolt:
- app/(dashboard)/dashboard/analytics/page.tsx               (page shell)
- components/analytics/analytics-client-view.tsx             ('use client' wrapper)
- components/analytics/kpi-section.tsx                       (KPI row + filter bar)
- components/analytics/hiring-velocity-chart.tsx             (Chart 1)
- components/analytics/pipeline-conversion-chart.tsx         (Chart 2)
- components/analytics/top-skills-chart.tsx                  (Chart 3)
- components/analytics/role-aging-chart.tsx                  (Chart 4)
- components/analytics/role-performance-table.tsx            (DataTable instance)
- lib/chart-theme.ts                                         (chart color + tooltip config — shared)

All chart components must have 'use client' directive (recharts uses browser APIs).
Only analytics-client-view.tsx should call useQuery — pass data down as props to children.

---

DARK MODE REQUIREMENT: All chart components — dark grid, dark tooltip, Larsseit font on axes, no white plot backgrounds. See §1.10 and §1.23 for exact recharts overrides.
```

---

## PART 4 — INTEGRATION RULES (AFTER BOLT OUTPUT)

---

### 4.1 What to Keep from Bolt Output
- Layout structure and visual components
- Tailwind class patterns
- Component hierarchy and props interfaces
- Framer Motion animation code
- Font and color implementation

### 4.2 What to Replace After Bolt Output
- Any inline mock data → wire to existing GraphQL queries/mutations
- Any hardcoded user/auth state → use existing NextAuth.js session hooks
- Any invented API routes → use existing Apollo Client setup
- Any generated backend code → discard entirely

### 4.3 Existing Files That Must Not Be Overwritten
```
apps/web/app/layout.tsx
apps/web/app/globals.css (merge, not replace)
apps/web/middleware.ts
apps/web/next-auth.d.ts
apps/web/lib/*
```

### 4.4 GraphQL Operation Names (Real — Match Exactly)
Wire bolt components to these operation names, not invented ones:

**Queries:**
- `recruiterDashboard` — dashboard KPIs + activity
- `myDemands` — recruiter's demand list
- `demand(id)` — single demand detail
- `shortlist(demandId)` — candidates for a demand
- `allInterviews` — recruiter's interview queue
- `allOffers` — recruiter's offer queue
- `recruiterAnalytics` — recruiter metrics
- `adminDashboard` — admin KPIs
- `users` — admin user list
- `talentVerificationQueue` — pending verifications
- `companies` — company list
- `demandsAwaitingApproval` — approval queue
- `adminAnalytics` — platform metrics
- `semanticSearch` — talent search

**Mutations:**
- `createDemand` / `updateDemand` / `pauseDemand` / `cancelDemand` / `fillDemand`
- `generateShortlist` — triggers AI matching
- `reviewCandidate` / `rejectCandidate`
- `scheduleInterview` / `updateInterview` / `submitFeedback`
- `createOffer` / `sendOffer` / `withdrawOffer`
- `approveTalentVerification` / `rejectTalentVerification`
- `approveDemand` / `rejectDemand` / `flagDemandHardToFill`
- `assignConcierge` / `submitExternalCandidate`
- `updateUserRole` / `deactivateUser` / `activateUser`

### 4.5 Merge Blocker Checklist (Binary — Before Any Page Merges)

**Visual / Design**
- [ ] Route matches verified route matrix (§3.3)
- [ ] Larsseit loads correctly — check @font-face in globals.css and fonts in `public/fonts/`
- [ ] Spriteburst `#EFFE5E` used for primary actions and interactive accents
- [ ] No card-heavy layout — tables, split-panes, and bordered containers only
- [ ] All icons are from lucide-react (no external icon sets or emoji in chrome)
- [ ] KPI row uses single-container-with-dividers pattern (not floating cards)
- [ ] Status badges use exact colors from §1.2 Status Badge table

**Behavior / States**
- [ ] Framer Motion page enter transition implemented (opacity+y, 0.22s)
- [ ] Loading skeleton present for all async data regions
- [ ] Empty state has: factual statement + context + CTA action button
- [ ] Error state has: error message + recovery suggestion + retry/action
- [ ] All destructive actions go through Confirm Action Modal
- [ ] Toast feedback on every mutation (success and error) via sonner

**Charts (analytics pages only)**
- [ ] Using Recharts with ResponsiveContainer
- [ ] Chart theme applied (Spriteburst primary, dark grid, Larsseit axis font)
- [ ] No pie/donut charts
- [ ] Custom Tooltip with dark background applied
- [ ] Empty chart state shows axes with "No data for this period"

**Data / Integration**
- [ ] All mock/static data removed — replaced with useQuery/useMutation hooks
- [ ] GraphQL operation names match exactly from §4.4 list
- [ ] TypeScript interfaces match §3.1a stubs (no `any`, no invented inline types)
- [ ] Auth guard from existing middleware preserved (`apps/web/middleware.ts`)
- [ ] No hardcoded secrets, API endpoints, or database credentials

**Files**
- [ ] `apps/web/app/layout.tsx` not overwritten
- [ ] `apps/web/app/globals.css` merged (not replaced) — font faces and tokens preserved
- [ ] `apps/web/middleware.ts` not touched
- [ ] `apps/web/lib/*` not touched

If any item unchecked → page is design-only, not production-ready. Do not merge.

---

### 4.6 Post-Merge Manual Testing Protocol

After merging each bolt group into `apps/web`, run through this protocol before moving to the next group. It catches visual regressions and wiring gaps that automated checks miss.

#### Visual pass (browser, no interaction)

| Check | What to look at |
|-------|-----------------|
| Font rendering | Larsseit loads — open DevTools → Network → filter `otf` → confirm 5 font files loaded, no 404s |
| Background purity | No white or light surfaces anywhere — scan full page for any `bg-white` leaks |
| Spriteburst usage | Primary buttons, active nav item, score fill — all in `#EFFE5E` not blue |
| Status badges | All badges use exact colors from §1.2 — not default shadcn blue/green |
| KPI row | Single-container divider pattern — not floating cards |
| Icon set | All icons lucide-react — open DevTools → Sources, search for `heroicons` or `radix-icons` (should be 0) |
| Scrollbars | Thin dark webkit scrollbar visible on scrollable panels |
| Focus rings | Tab through all interactive elements — ring should be `#EFFE5E`, not blue |

#### Interaction pass

| Check | Steps |
|-------|-------|
| Page enter animation | Hard refresh — page should fade+slide in from bottom |
| Loading skeleton | Throttle network to Slow 3G — skeleton rows should appear, then data replaces them |
| Empty state | Temporarily return empty array from query — empty state icon+title+CTA should show |
| Error state | Kill API server or set network Offline — error panel with Retry button should show |
| Destructive modal | Click any destructive action — confirm modal must appear before mutation fires |
| Toast feedback | Complete any mutation — sonner toast should appear bottom-right with correct copy |
| Form validation | Submit a form with all required fields empty — field-level errors should show, no network request |
| Dirty form nav | Edit a form field, click Back — confirmation modal should appear |

#### Data wiring pass

| Check | How |
|-------|-----|
| No static mock data | DevTools → Network tab — verify GraphQL requests fire on page load |
| Correct query name | Request payload should match operation names from §4.4 |
| Auth guard | Open a `/dashboard/*` route in incognito — should redirect to `/login` |
| Admin guard | Sign in as RECRUITER role, navigate to `/admin` — should redirect (middleware enforced) |
| Refetch after mutation | After any create/update/delete, list should auto-refresh |

#### Responsive pass (resize browser)

| Breakpoint | What to check |
|-----------|---------------|
| 1440px | Full desktop layout — sidebar visible, full table columns |
| 1024px | Sidebar still visible, table scrolls horizontally if needed |
| 768px | Sidebar collapses to icon-only OR mobile sheet drawer |
| 375px | Single column, all content accessible, no horizontal overflow |

---

## PART 5 — COPY SYSTEM

---

### 5.1 Voice

**Tone:** Confident. Direct. Human. Outcome-oriented.
No hype. No buzzwords. Every sentence earns its place.

### 5.2 Banned Phrases

Never use in any UI copy generated by bolt or written manually:
- streamline, leverage, synergy, revolutionary, best-in-class, seamless, game-changer, cutting-edge, robust, holistic, ecosystem, paradigm, utilize (use "use")

### 5.3 Required Lexicon

| Use this | Not this |
|----------|----------|
| talent | candidate (unless quoting) |
| demand | job posting |
| shortlist | results |
| verify / verification | confirm / confirmation |
| approval | sign-off |
| platform admin | super admin |
| rate | salary (they're hourly) |

### 5.4 CTA Patterns

All CTAs: **verb + object**

| Page action | CTA text |
|-------------|---------|
| Create a demand | "Create Role" |
| Submit demand | "Publish Role" |
| Save incomplete | "Save as Draft" |
| Trigger AI matching | "Generate Shortlist" |
| Move to interview | "Request Interview" |
| Move to offer | "Draft Offer" |
| Send an offer | "Send Offer" |
| Verify talent | "Approve Profile" |
| Remove from shortlist | "Reject Candidate" |
| Search talent | "Run Search" |
| Approve demand | "Approve Demand" |
| Open admin queue | "Review Queue" |

### 5.5 Empty State Formula

```
[Factual statement about what's missing].
[One-sentence context why it's empty].
[Primary action CTA].
```

Examples:
- "No demands yet. Post your first role to generate AI-matched shortlists." → [Create Role]
- "No interviews scheduled. Request one from a candidate's shortlist profile." → [Go to Shortlists]
- "Verification queue is clear. All submitted profiles have been reviewed." → (no CTA needed)

### 5.6 Error State Formula

```
We couldn't load [resource].
[Suggested action or reason].
[Retry CTA if applicable].
```

Examples:
- "We couldn't load your roles. Check your connection and try again." → [Retry]
- "Search failed. Simplify your query or adjust filters." → [Reset Filters]

### 5.7 Success State Formula

```
[Entity] [past-tense action].
[Optional consequence / next step prompt].
```

Examples:
- "Role published. AI is generating your shortlist — check back in a moment."
- "Offer sent. The candidate has been notified by email."
- "Candidate approved. Their profile is now verified."

---

### 5.8 Page Title & Metadata Patterns

Bolt must generate a `<title>` for every route. Provide these via Next.js `generateMetadata` or static `metadata` export. Use the `NEXT_PUBLIC_APP_NAME` env var or the constant `"AI Talent Marketplace"` as the site name.

**Title format:** `[Page Name] · AI Talent Marketplace`

**Bolt instruction:** In every page file, include:
```typescript
import type { Metadata } from 'next'
export const metadata: Metadata = {
  title: '[Page Title] · AI Talent Marketplace',
  description: '[One sentence description]',
}
```
OR for dynamic pages (those with `[id]` params):
```typescript
export async function generateMetadata({ params }: { params: { id: string } }): Promise<Metadata> {
  // title falls back gracefully if data unavailable
  return {
    title: `[Dynamic value] · AI Talent Marketplace`,
  }
}
```

#### Title Table — All 25 Routes

| Route | `<title>` | `description` |
|-------|----------|---------------|
| `/` | `AI Talent Marketplace · AI-Powered Hiring` | `Connect enterprise hiring teams with qualified talent. AI-matched shortlists in hours.` |
| `/login` | `Sign In · AI Talent Marketplace` | `Sign in to your recruiter or admin workspace.` |
| `/register` | `Create Account · AI Talent Marketplace` | `Set up your recruiter workspace and start hiring with AI.` |
| `/forgot-password` | `Reset Password · AI Talent Marketplace` | `Request a password reset link for your account.` |
| `/reset-password` | `New Password · AI Talent Marketplace` | `Choose a new password for your account.` |
| `/dashboard` | `Dashboard · AI Talent Marketplace` | `Your hiring overview — active roles, shortlists, and pipeline health.` |
| `/dashboard/roles` | `Roles · AI Talent Marketplace` | `Manage your active, draft, and completed role demands.` |
| `/dashboard/roles/new` | `Create Role · AI Talent Marketplace` | `Post a new talent demand with AI-assisted description.` |
| `/dashboard/roles/[id]` | `[demand.title] · AI Talent Marketplace` | `[demand.title] — manage shortlists, interviews, and offers for this role.` |
| `/dashboard/shortlists` | `Shortlists · AI Talent Marketplace` | `Review AI-matched candidates across all your active roles.` |
| `/dashboard/search` | `Talent Search · AI Talent Marketplace` | `Search the full talent pool with AI semantic search and filters.` |
| `/dashboard/interviews` | `Interviews · AI Talent Marketplace` | `Manage all scheduled and completed interviews in one place.` |
| `/dashboard/interviews/[d]/[i]` | `Interview · AI Talent Marketplace` | `Interview detail — candidate, schedule, feedback, and offer actions.` |
| `/dashboard/offers` | `Offers · AI Talent Marketplace` | `Track all offers — drafted, sent, accepted, and declined.` |
| `/dashboard/offers/[d]/[o]` | `Offer · AI Talent Marketplace` | `Offer detail — terms, status, and timeline.` |
| `/dashboard/analytics` | `Analytics · AI Talent Marketplace` | `Hiring velocity, pipeline conversion, and skills demand analytics.` |
| `/admin` | `Admin Dashboard · AI Talent Marketplace` | `Platform operations overview — verification queue, approvals, and alerts.` |
| `/admin/users` | `User Management · AI Talent Marketplace` | `Manage all registered users, roles, and account status.` |
| `/admin/verification` | `Talent Verification · AI Talent Marketplace` | `Review and approve talent identity and certification submissions.` |
| `/admin/companies` | `Companies · AI Talent Marketplace` | `Manage portfolio companies and recruiter assignments.` |
| `/admin/approvals` | `Demand Approvals · AI Talent Marketplace` | `Review and approve talent demands before they go live.` |
| `/admin/concierge` | `Concierge · AI Talent Marketplace` | `Assign headhunters to hard-to-fill roles and track external candidates.` |
| `/admin/analytics` | `Platform Analytics · AI Talent Marketplace` | `Platform-wide metrics — talent growth, skill gaps, and hiring trends.` |
| `/settings` | `Account Settings · AI Talent Marketplace` | `Manage your profile, security, and notification preferences.` |
| `/not-found` | `Page Not Found · AI Talent Marketplace` | — |

**Rules:**
- Never use `<title>AI Talent Marketplace</title>` alone without a page qualifier — always include the page name first
- Dynamic routes must fall back gracefully: if data unavailable at render, use `Role Detail · AI Talent Marketplace`
- `description` is not visible to users but used for OG cards and Google — keep under 155 chars
- Do NOT generate `og:image` — no image CDN is configured yet

---

*This specification governs all bolt.new-generated web UI for the AI Talent Marketplace Platform. Every page, component, and copy element must comply before being merged into `apps/web`.*

---

## APPENDIX — QUICK REFERENCE

### A.1 Route → Query → Mutation Map

| Route | Primary Query | Primary Mutations |
|-------|-------------|------------------|
| `/dashboard` | `recruiterDashboard` | — |
| `/dashboard/roles` | `myDemands` | `pauseDemand`, `cancelDemand` |
| `/dashboard/roles/new` | `skills` | `createDemand`, `generateRoleDescription` |
| `/dashboard/roles/[id]` | `demand`, `shortlist` | `updateDemand`, `generateShortlist`, `reviewCandidate`, `scheduleInterview`, `createOffer` |
| `/dashboard/shortlists` | `allShortlists` | `reviewCandidate`, `rejectCandidate`, `scheduleInterview` |
| `/dashboard/search` | `semanticSearch` | `reviewCandidate` |
| `/dashboard/interviews` | `allInterviews` | `scheduleInterview`, `cancelInterview` |
| `/dashboard/interviews/[d]/[i]` | `interview` | `updateInterview`, `submitFeedback`, `rescheduleInterview`, `cancelInterview` |
| `/dashboard/offers` | `allOffers` | `sendOffer`, `withdrawOffer` |
| `/dashboard/offers/[d]/[o]` | `offer` | `sendOffer`, `withdrawOffer` |
| `/dashboard/analytics` | `recruiterAnalytics` | — |
| `/admin` | `adminDashboard` | — |
| `/admin/users` | `users` | `updateUserRole`, `deactivateUser`, `activateUser` |
| `/admin/verification` | `talentVerificationQueue` | `approveTalentVerification`, `rejectTalentVerification` |
| `/admin/companies` | `companies` | `createCompany`, `updateCompany`, `assignRecruiter` |
| `/admin/approvals` | `demandsAwaitingApproval` | `approveDemand`, `rejectDemand`, `flagDemandHardToFill` |
| `/admin/concierge` | `hardToFillDemands`, `conciergeAssignments` | `assignConcierge`, `submitExternalCandidate` |
| `/admin/analytics` | `adminAnalytics` | — |
| `/settings` | `me` | `updateProfile`, `changePassword`, `updateNotificationPreferences` |

---

### A.2 Page → Layout Pattern Map

| Layout pattern | Used by |
|---------------|---------|
| Full-bleed public | `/`, error, not found |
| Centered auth panel | `/login`, `/register`, `/forgot-password`, `/reset-password` |
| Dashboard shell (sidebar + topbar) | All `/dashboard/*` and `/admin/*` routes |
| Two-column form (fields + AI panel) | `/dashboard/roles/new` |
| Tabbed detail (header + metadata rail + tabs) | `/dashboard/roles/[id]` |
| Split-pane (queue list + detail panel) | `/admin/verification`, `/admin/approvals` |
| Split analytics (KPIs + charts + table) | `/dashboard/analytics`, `/admin/analytics` |
| Settings shell (left mini-nav + content) | `/settings` |

---

### A.3 Color Usage Cheat Sheet

```
Spriteburst (#EFFE5E):   primary buttons, active nav border, KPI values, score fill, chart primary series, Spriteburst icon accent, unread notification dot
White (#FFFFFF):         body text, table cells, headings, modal titles
#A1A1AA:                 secondary text, helper labels, table headers, chart axis
#52525B:                 placeholders, timestamps, disabled states
#000000:                 page shell background
#111111:                 sidebar, topbar, surface panels
#1A1A1A:                 card backgrounds, table row bg, input backgrounds
#222222:                 row hover, active selected row
#27272A:                 default borders, table dividers, chart grid
#22C55E:                 success states only
#F59E0B:                 warnings and aging indicators
#EF4444:                 destructive actions, error states
#3B82F6:                 info states, scheduled status
```

---

### A.4 File & Component Naming Conventions

All bolt-generated files must follow these conventions so merging into `apps/web` is clean and predictable.

#### File Naming

| File type | Convention | Example |
|-----------|-----------|---------|
| Page component | `page.tsx` (Next.js App Router) | `app/dashboard/roles/page.tsx` |
| Layout | `layout.tsx` | `app/(dashboard)/layout.tsx` |
| Loading state | `loading.tsx` | `app/dashboard/roles/loading.tsx` |
| Error boundary | `error.tsx` | `app/dashboard/error.tsx` |
| UI component | `kebab-case.tsx` | `components/ui/score-breakdown.tsx` |
| Feature component | `feature/component-name.tsx` | `components/roles/demand-table.tsx` |
| Modal | `modals/action-name-modal.tsx` | `components/modals/schedule-interview-modal.tsx` |
| Layout component | `layout/name.tsx` | `components/layout/sidebar.tsx` |
| Hook | `use-[name].ts` | `hooks/use-demand-filters.ts` |
| Util | `[name].ts` | `lib/format-date.ts` |
| Types | `marketplace.ts` | `types/marketplace.ts` |
| Zod schema | `[feature]-schema.ts` | `lib/schemas/demand-schema.ts` |
| Chart config | `chart-theme.ts` | `lib/chart-theme.ts` |
| Motion constants | `motion.ts` | `lib/motion.ts` |

#### Component Naming

| Convention | Rule |
|-----------|-------|
| PascalCase | All React components and TypeScript types/interfaces |
| Props interface | `ComponentNameProps` — e.g. `DemandTableProps` |
| Enum-like const | `UPPER_SNAKE_CASE` — e.g. `DEMAND_STATUS` |
| GraphQL documents | `OPERATION_NAME_QUERY` / `OPERATION_NAME_MUTATION` — e.g. `MY_DEMANDS_QUERY` |
| Hooks | camelCase with `use` prefix — e.g. `useDemandFilters` |
| Event handlers | `handle[Event]` — e.g. `handleRowClick`, `handleStatusFilter` |
| Boolean props | `is` or `has` prefix — e.g. `isLoading`, `hasError`, `isActive` |

#### Import Order (enforce in every generated file)

```tsx
// 1. React and Next.js
import { useState, useEffect } from 'react'
import Link from 'next/link'
import { useRouter } from 'next/navigation'

// 2. Third-party libraries
import { motion } from 'framer-motion'
import { useQuery, useMutation } from '@apollo/client'
import { toast } from 'sonner'
import { Briefcase, Plus } from 'lucide-react'

// 3. Internal UI components (shadcn)
import { Button } from '@/components/ui/button'
import { Badge } from '@/components/ui/badge'

// 4. Internal custom components
import { DemandTable } from '@/components/roles/demand-table'
import { EmptyState } from '@/components/ui/empty-state'

// 5. Types and schemas
import type { Demand } from '@/types/marketplace'

// 6. GraphQL documents
import { MY_DEMANDS_QUERY } from '@/graphql/queries'

// 7. Utils / constants
import { formatDistanceToNow } from 'date-fns'
import { MOTION_CONFIG } from '@/lib/motion'
```

#### Directory Structure (apps/web — bolt target)

```
apps/web/
├── app/
│   ├── (auth)/                    # public auth routes, no sidebar
│   │   ├── login/page.tsx
│   │   ├── register/page.tsx
│   │   ├── forgot-password/page.tsx
│   │   └── reset-password/page.tsx
│   ├── (dashboard)/               # recruiter routes, has sidebar + topbar
│   │   ├── layout.tsx
│   │   ├── dashboard/page.tsx
│   │   ├── dashboard/roles/
│   │   │   ├── page.tsx
│   │   │   ├── new/page.tsx
│   │   │   └── [id]/page.tsx
│   │   ├── dashboard/shortlists/page.tsx
│   │   ├── dashboard/search/page.tsx
│   │   ├── dashboard/interviews/
│   │   │   ├── page.tsx
│   │   │   └── [demandId]/[interviewId]/page.tsx
│   │   ├── dashboard/offers/
│   │   │   ├── page.tsx
│   │   │   └── [demandId]/[offerId]/page.tsx
│   │   └── dashboard/analytics/page.tsx
│   ├── (admin)/                   # admin routes, has admin sidebar + topbar
│   │   ├── layout.tsx
│   │   ├── admin/page.tsx
│   │   ├── admin/users/page.tsx
│   │   ├── admin/verification/page.tsx
│   │   ├── admin/companies/page.tsx
│   │   ├── admin/approvals/page.tsx
│   │   ├── admin/concierge/page.tsx
│   │   └── admin/analytics/page.tsx
│   ├── settings/page.tsx          # shared — any authenticated role
│   ├── page.tsx                   # landing page (public)
│   ├── not-found.tsx
│   ├── error.tsx
│   ├── loading.tsx
│   ├── layout.tsx                 # root layout — DO NOT OVERWRITE
│   └── globals.css                # MERGE ONLY — DO NOT REPLACE
├── components/
│   ├── layout/
│   │   ├── sidebar.tsx
│   │   ├── topbar.tsx
│   │   └── command-palette.tsx
│   ├── ui/
│   │   ├── status-badge.tsx
│   │   ├── kpi-row.tsx
│   │   ├── empty-state.tsx
│   │   ├── skeleton-rows.tsx
│   │   ├── score-breakdown.tsx
│   │   ├── notification-center.tsx
│   │   ├── file-upload.tsx
│   │   ├── date-picker.tsx
│   │   ├── range-slider.tsx
│   │   ├── pagination.tsx
│   │   └── breadcrumb.tsx
│   ├── modals/
│   │   ├── confirm-action-modal.tsx
│   │   ├── skill-selector-modal.tsx
│   │   ├── schedule-interview-modal.tsx
│   │   └── draft-offer-modal.tsx
│   ├── roles/
│   │   ├── demand-table.tsx
│   │   ├── demand-row.tsx
│   │   ├── demand-filters.tsx
│   │   └── candidate-profile-modal.tsx
│   ├── analytics/
│   │   ├── kpi-cell.tsx
│   │   └── chart-container.tsx    # wrapper with title + empty state
│   └── providers/
│       └── apollo-provider.tsx    # DO NOT GENERATE — already exists
├── graphql/
│   ├── queries.ts
│   └── mutations.ts
├── hooks/
│   └── use-command-palette.ts
├── lib/
│   ├── motion.ts
│   ├── chart-theme.ts
│   └── schemas/
│       ├── auth-schema.ts
│       ├── demand-schema.ts
│       ├── interview-schema.ts
│       └── offer-schema.ts
├── types/
│   └── marketplace.ts
└── public/
    └── fonts/                     # copy Larsseit .otf files here before running bolt
```

---

### A.5 Performance Budget

These are hard limits for the web app. Bolt-generated code should not introduce patterns that obviously violate them.

| Metric | Budget |
|--------|--------|
| Largest Contentful Paint (LCP) | < 2.5s on broadband |
| First Input Delay (FID) | < 100ms |
| Cumulative Layout Shift (CLS) | < 0.1 |
| JavaScript bundle (initial) | < 200kB gzipped |
| Font load | Non-blocking (`font-display: swap` — already in §1.12) |
| Skeleton shown after | 200ms delay (never on fast connections) |
| Image lazy loading | All `<img>` tags use `loading="lazy"` unless above-fold |
| Client components | Only where interactivity is required — prefer Server Components for data-display pages |

**Practical bolt rules (to include in prompts where relevant):**
- Use `'use client'` only at the lowest level component that needs it
- Pass data down from server components where possible
- Never put Apollo Client in a Server Component — always in Client Components or a provider
- `recharts` must be in a `'use client'` component (it uses browser APIs)

---

### A.6 Environment Variables — Web App (`apps/web`)

These are the env vars the Next.js web app reads at runtime. Bolt should reference them in `process.env` calls and **never hardcode values**.

#### Required `.env.local` for `apps/web`

```bash
# Auth (NextAuth.js)
NEXTAUTH_URL=http://localhost:3001
NEXTAUTH_SECRET=<generate with: openssl rand -base64 32>

# GraphQL API (Apollo Client)
NEXT_PUBLIC_GRAPHQL_URL=http://localhost:4000/graphql

# App
NEXT_PUBLIC_APP_URL=http://localhost:3001
NEXT_PUBLIC_APP_NAME="AI Talent Marketplace"
```

#### How bolt should reference them in code

```typescript
// Apollo Client setup (lib/apollo-client.ts) — already exists, do not regenerate
// Just reference NEXT_PUBLIC_GRAPHQL_URL as the endpoint

// NextAuth config (app/api/auth/[...nextauth]/route.ts) — already exists
// Uses NEXTAUTH_SECRET and NEXTAUTH_URL automatically

// For any client-side URL construction (e.g. image CDN, share links):
const appUrl = process.env.NEXT_PUBLIC_APP_URL ?? 'http://localhost:3001'
```

#### Variables NOT available to bolt-generated client code

- `DATABASE_URL` — only in `packages/db`, never web app
- `OPENROUTER_API_KEY` — only in `services/ai-engine`, never web app
- `JWT_SECRET` — only in `apps/api`, never web app
- Any `RESEND_*` or `R2_*` keys — backend only

#### Env var naming rules bolt must follow
- `NEXT_PUBLIC_` prefix: safe for browser bundle
- Without prefix: server-only (API routes, `generateMetadata`, `getServerSideProps`)
- Never use `process.env` in a Client Component for non-`NEXT_PUBLIC_` vars — it will be `undefined`

---

### A.7 GraphQL Minimum Field Selections

When wiring GraphQL queries in bolt-generated components, always request at minimum these fields per type. Requesting too few causes missing UI data; requesting too many wastes bandwidth. These are the **canonical field sets**.

#### `Demand` (role/demand object)

```graphql
fragment DemandCore on Demand {
  id
  title
  description
  status
  level
  location
  isRemote
  budgetMin
  budgetMax
  currency
  startDate
  duration
  createdAt
  updatedAt
  skills {
    id
    name
  }
  company {
    id
    name
    logoUrl
  }
  createdBy {
    id
    name
  }
}
```

#### `TalentProfile` (candidate/talent object)

```graphql
fragment TalentProfileCore on TalentProfile {
  id
  headline
  summary
  availability
  hourlyRate
  currency
  location
  isRemote
  verificationStatus
  user {
    id
    name
    email
    avatarUrl
  }
  skills {
    id
    name
    proficiencyLevel
    yearsOfExperience
  }
  matchScore         # only present in shortlist context
  scoreBreakdown {   # only present in shortlist context
    skillMatch
    experienceFit
    availability
    pricingFit
    locationMatch
    culturalFit
    feedbackScore
  }
}
```

#### `Shortlist` (single shortlist entry)

```graphql
fragment ShortlistEntry on Shortlist {
  id
  status
  aiExplanation
  createdAt
  talent {
    ...TalentProfileCore
  }
  demand {
    id
    title
  }
}
```

#### `Interview`

```graphql
fragment InterviewCore on Interview {
  id
  status
  scheduledAt
  duration
  meetingUrl
  notes
  feedback {
    rating
    text
    skillsDemonstrated
    submittedAt
  }
  talent {
    id
    user { id name avatarUrl }
    headline
  }
  demand {
    id
    title
    company { id name }
  }
  createdAt
  updatedAt
}
```

#### `Offer`

```graphql
fragment OfferCore on Offer {
  id
  status
  hourlyRate
  currency
  startDate
  endDate
  terms
  sentAt
  respondedAt
  talent {
    id
    user { id name avatarUrl }
    headline
  }
  demand {
    id
    title
    company { id name }
  }
  createdAt
  updatedAt
}
```

#### `User` (admin user management)

```graphql
fragment UserCore on User {
  id
  name
  email
  role
  status
  createdAt
  lastActiveAt
  company {
    id
    name
  }
  talentProfile {
    id
    verificationStatus
  }
}
```

#### `Company`

```graphql
fragment CompanyCore on Company {
  id
  name
  industry
  size
  logoUrl
  activeDemandCount
  totalHires
  recruiters {
    id
    name
    email
  }
}
```

#### Field selection rules for bolt prompts

1. **Always use named fragments** — do not inline all fields in every query; reference the fragments above.
2. **Never select `password`, `passwordHash`, or `refreshToken`** — these exist on User but must never be queried from the frontend.
3. **`matchScore` and `scoreBreakdown`** only exist in the shortlist context — do not request them on a bare `TalentProfile` query.
4. **Pagination pattern:** all list queries return `{ nodes: [...], pageInfo: { hasNextPage, endCursor } }` — always request both.
5. **Error handling:** wrap every `useQuery` result with the error check pattern from §1.20 — never render raw Apollo error objects.

---

### A.8 shadcn/ui Component Install Commands

Run these from `apps/web/` before starting bolt generation. Bolt assumes all shadcn components are already installed — if any are missing, the generated code will fail to compile.

#### One-shot install (all components needed for this project)

```bash
cd apps/web

npx shadcn@latest add \
  button \
  input \
  textarea \
  label \
  select \
  checkbox \
  radio-group \
  switch \
  slider \
  badge \
  avatar \
  separator \
  dialog \
  sheet \
  dropdown-menu \
  popover \
  tooltip \
  command \
  calendar \
  tabs \
  table \
  form \
  toast \
  skeleton \
  alert \
  progress \
  scroll-area \
  collapsible \
  accordion \
  card
```

This is a single command — copy-paste as-is. Each component installs its required Radix UI primitive.

#### Component → Radix primitive map (for debugging)

| shadcn component | Installs | Used by |
|-----------------|---------|---------|
| `button` | `@radix-ui/react-slot` | Every page |
| `input` | (native) | All forms |
| `textarea` | (native) | Create Role, Interview feedback, Offer terms |
| `label` | `@radix-ui/react-label` | All forms |
| `select` | `@radix-ui/react-select` | Level, Remote Policy, Currency, per-page select |
| `checkbox` | `@radix-ui/react-checkbox` | Bulk select in tables |
| `radio-group` | `@radix-ui/react-radio-group` | Skill match mode, remote policy |
| `switch` | `@radix-ui/react-switch` | Notification preferences in /settings |
| `slider` | `@radix-ui/react-slider` | Score range filter, rate range in search |
| `badge` | (none) | Status badges throughout |
| `avatar` | `@radix-ui/react-avatar` | Candidate profile, topbar user |
| `separator` | `@radix-ui/react-separator` | Form section dividers, KPI row dividers |
| `dialog` | `@radix-ui/react-dialog` | All modals (4 shared modals + reject modal) |
| `sheet` | `@radix-ui/react-dialog` | Mobile sidebar drawer |
| `dropdown-menu` | `@radix-ui/react-dropdown-menu` | Table row action overflow |
| `popover` | `@radix-ui/react-popover` | Skills dropdown, date picker trigger |
| `tooltip` | `@radix-ui/react-tooltip` | Aging indicator hover, disabled button hover |
| `command` | `cmdk` | Skills search in Skill Selector, Command Palette |
| `calendar` | `react-day-picker` | All date picker fields |
| `tabs` | `@radix-ui/react-tabs` | Role Detail (4 tabs), Concierge (3 tabs), Settings |
| `table` | (native HTML) | All data tables (DataTable component) |
| `form` | `react-hook-form` | All forms (wires labels + errors automatically) |
| `toast` | (native) | (Note: project uses sonner, not shadcn toast) |
| `skeleton` | (none) | Loading states |
| `alert` | (none) | System alert banners on Admin Dashboard |
| `progress` | `@radix-ui/react-progress` | Password strength bar in register |
| `scroll-area` | `@radix-ui/react-scroll-area` | Sidebar scroll, notification panel |
| `collapsible` | `@radix-ui/react-collapsible` | Original recruiter notes collapse in Role Overview |
| `accordion` | `@radix-ui/react-accordion` | Score factor expand in Shortlist |
| `card` | (none) | Not used in chrome — only in public landing page sections |

#### NPM packages to install separately (not in shadcn CLI)

```bash
# From apps/web/
npm install \
  framer-motion \
  recharts \
  sonner \
  date-fns \
  react-hook-form \
  @hookform/resolvers \
  zod \
  lucide-react \
  @apollo/client \
  graphql
```

Note: `@apollo/client` and `graphql` may already be installed — run `npm ls @apollo/client` to check before installing.

#### Verify all installed

```bash
# Quick check: look for shadcn-generated files
ls src/components/ui/ | sort
# Should show: accordion.tsx avatar.tsx badge.tsx button.tsx calendar.tsx checkbox.tsx ...
# Any missing file = run the shadcn add command for that component
```

---

### A.9 Common Bolt Failure Modes — Diagnosis & Fixes

Bolt produces excellent scaffolding but makes the same mistakes repeatedly. This table catalogs every known failure mode specific to this project's stack and how to fix each one post-generation.

#### TypeScript / Compilation Failures

| Symptom | Root cause | Fix |
|---------|-----------|-----|
| `Cannot find module '@/components/ui/...'` | Bolt generated a component reference before generating the component file | Generate/install the missing shadcn component (see A.8) or create the stub |
| `Type 'any' is not assignable` | Bolt used `any` despite instructions | Replace with the correct type from §3.1a interface stubs |
| `Hooks can only be called inside a Client Component` | `useQuery`/`useMutation` used in a Server Component | Add `'use client'` at top of the file, or extract query logic to a child client component |
| `Cannot read properties of undefined (reading 'nodes')` | Query data accessed before loading check | Wrap in `if (loading) return <SkeletonRows />` before data access |
| `Module not found: 'date-fns'` | date-fns not installed | `npm install date-fns` from `apps/web/` |
| `Module not found: 'sonner'` | sonner not installed | `npm install sonner` from `apps/web/` |
| Import says `recharts` but component is not 'use client' | recharts uses `window` — SSR crash | Add `'use client'` to every file that imports from recharts |

#### Visual / Design Failures

| Symptom | Root cause | Fix |
|---------|-----------|-----|
| White modal background | shadcn Dialog defaults to `bg-background` CSS var | Override: add `className="bg-[#1A1A1A] border border-[#27272A]"` to DialogContent |
| Blue focus ring on inputs | shadcn uses `ring-ring` CSS var (blue) | Add `focus-visible:ring-[#EFFE5E]` to input className |
| Light gray skeleton (`bg-gray-200`) | shadcn Skeleton light default | Replace with `bg-[#222222] animate-pulse` |
| Chart tooltip has white background | Recharts default tooltip | Add `contentStyle` prop — see §1.10 |
| Chart axis text too light/invisible | Recharts default axis color | Add `tick={{ fill: '#52525B', fontSize: 12 }}` to XAxis and YAxis |
| Font is not Larsseit (showing system sans-serif) | Font files missing from `public/fonts/` | Copy `.otf` files: `cp font/Larsseit*/*.otf apps/web/public/fonts/` |
| Font is not Larsseit — files present but not loading | @font-face missing from globals.css | Verify §1.12 font-face block is in globals.css (not replaced by bolt) |
| Sidebar active item has blue highlight | Bolt used default shadcn active state | Override: `data-[active=true]:border-l-2 data-[active=true]:border-[#EFFE5E] data-[active=true]:bg-[#1a1c00]` |
| Select dropdown has white background | Shadcn SelectContent default | Add `className="bg-[#0A0A0A] border-[#27272A]"` to SelectContent |
| Status badge wrong color (blue/green/gray generic) | Bolt invented its own badge colors | Replace with StatusBadge component using exact colors from §1.2 |
| KPI cells are floating cards | Bolt generated `<Card>` components | Replace grid of cards with single KPIRow container (§1.22) |

#### State / Behavior Failures

| Symptom | Root cause | Fix |
|---------|-----------|-----|
| No loading state — data appears instantly or page flashes | Bolt skipped skeleton | Add `if (loading) return <SkeletonRows count={5} />` before render |
| Destructive action fires immediately (no confirmation) | Bolt wired button directly to mutation | Wrap in ConfirmActionModal — show modal on click, fire mutation on Confirm |
| No toast on mutation complete | Bolt omitted sonner feedback | Add `onCompleted: () => toast.success('...')` and `onError: () => toast.error('...')` |
| Form submits despite validation errors | `onSubmit` wired to native submit, not react-hook-form | Use `handleSubmit` from `useForm()` as the form `onSubmit` handler |
| Page enter animation doesn't play | Bolt generated plain `<div>` | Replace with `<motion.div initial={{opacity:0,y:10}} animate={{opacity:1,y:0}} transition={{duration:0.22}}>` |
| Empty state missing or shows wrong copy | Bolt wrote "No data" / "No items" | Replace with §5.5 formula: factual + context + CTA |

#### GraphQL / Data Wiring Failures

| Symptom | Root cause | Fix |
|---------|-----------|-----|
| GraphQL operation not found | Bolt invented an operation name | Check §4.4 list — replace with exact operation name |
| `UNAUTHENTICATED` error on all queries | Apollo client not sending auth header | The existing Apollo Client setup in `lib/apollo-client.ts` handles this — verify bolt didn't overwrite it |
| `Cannot return null for non-nullable field` | Requesting a field that doesn't exist or is null | Cross-check against §A.7 fragment — don't request fields not in the schema |
| Pagination not working | Bolt used offset pagination instead of cursor | Use `pageInfo { hasNextPage, endCursor }` and `after: cursor` variables (§A.7) |
| `password` or `refreshToken` in query | Bolt included all User fields | Remove immediately — never query sensitive fields from frontend |

#### File Structure Failures

| Symptom | Root cause | Fix |
|---------|-----------|-----|
| `app/layout.tsx` overwritten (font-face gone) | Bolt regenerated root layout | Restore from git: `git checkout HEAD apps/web/app/layout.tsx` |
| `middleware.ts` overwritten (auth guard gone) | Bolt regenerated middleware | Restore from git: `git checkout HEAD apps/web/middleware.ts` |
| Component files in wrong directory | Bolt used its own convention | Move to match §A.4 naming conventions |
| `page.tsx` is missing `'use client'` but uses hooks | Bolt forgot the directive | Add `'use client'` as first line |
| `.env.local` values hardcoded in component | Bolt inlined placeholder URLs | Replace with `process.env.NEXT_PUBLIC_GRAPHQL_URL` (see §A.6) |
