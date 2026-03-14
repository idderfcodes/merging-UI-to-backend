# MOBILE-UI-SPEC.md — AI Talent Marketplace · Expo React Native
# Build Contract for Cursor / AI-assisted code generation

> **Status:** Master spec — TALENT role mobile app only  
> **Tech stack:** Expo SDK 50 · React Native · Expo Router · Apollo Client · TypeScript strict  
> **Scope:** All 10 talent-facing screens + design system + build prompts + integration rules  
> **Backend:** Apollo GraphQL API at port 4000 (same schema as web)  
> **Companion spec:** `notes/BOLT-UI-SPEC.md` (recruiter + admin web)  
> **Last updated:** March 2026

---

## CRITICAL BRAND CORRECTION

The current codebase uses **wrong brand colors**. The mobile app was scaffolded with a sky-blue
palette (`#020617` / `#38bdf8`) that does NOT match the platform brand.

**Replace all existing color values with the correct brand palette as documented in §1.1.**

The providers (`auth-provider.tsx`, `apollo-provider.tsx`, `talent-profile-provider.tsx`,
`talent-workflow-provider.tsx`) are correct — rebuild UI layer only.

---

## TABLE OF CONTENTS

- PART 1 — Design System (§1.1–§1.13)
- PART 2 — Screen Specifications (§2.1–§2.10)
- PART 3 — Build Prompts (§3.1–§3.5)
- PART 4 — Integration Rules (§4.1–§4.6)
- PART 5 — Copy System (§5.1–§5.4)
- APPENDIX A.1–A.5

---

## PART 1 — DESIGN SYSTEM

### §1.1 Brand Colors

All colors must be defined in `constants/colors.ts`. **Never hardcode hex strings directly
in screen files.** Import from `constants/colors`.

```typescript
// apps/mobile/constants/colors.ts
export const Colors = {
  // Backgrounds — layered dark system (same as web)
  bg: {
    base:    '#000000',  // page background
    surface: '#0A0A0A',  // card / sheet background
    raised:  '#1A1A1A',  // elevated card
    overlay: '#222222',  // modal / popover overlay
  },

  // Text
  text: {
    primary:   '#FFFFFF',
    secondary: '#A1A1AA',
    tertiary:  '#52525B',
    disabled:  '#3F3F46',
    inverse:   '#000000',
  },

  // Accent — Spriteburst
  accent: {
    primary:   '#EFFE5E',
    pressed:   '#BBB906',
    muted:     '#8BAE14',
    subtle:    '#1A2200',
  },

  // Borders
  border: {
    default:   '#27272A',
    strong:    '#3F3F46',
    accent:    '#EFFE5E',
  },

  // Semantic — Status colors
  status: {
    success:   '#22C55E',
    successBg: '#052E16',
    warning:   '#EAB308',
    warningBg: '#1C1400',
    error:     '#EF4444',
    errorBg:   '#1F0606',
    info:      '#3B82F6',
    infoBg:    '#0C1A3E',
  },

  // Demand status (matches web spec exactly)
  demand: {
    draft:     '#A1A1AA',
    active:    '#EFFE5E',
    paused:    '#EAB308',
    filled:    '#22C55E',
    cancelled: '#EF4444',
    pending:   '#3B82F6',
  },

  // Shortlist status
  shortlist: {
    ai_matched:  '#EFFE5E',
    shortlisted: '#3B82F6',
    rejected:    '#EF4444',
    hired:       '#22C55E',
  },

  // Interview status
  interview: {
    scheduled:  '#3B82F6',
    completed:  '#22C55E',
    cancelled:  '#EF4444',
    no_show:    '#EAB308',
  },

  // Offer status
  offer: {
    draft:     '#A1A1AA',
    sent:      '#3B82F6',
    accepted:  '#22C55E',
    declined:  '#EF4444',
    withdrawn: '#A1A1AA',
  },

  // Score colors (match web)
  score: {
    excellent: '#EFFE5E',   // ≥80
    good:      '#22C55E',   // ≥60
    fair:      '#EAB308',   // ≥40
    low:       '#EF4444',   // <40
  },
} as const;

export type ColorKey = typeof Colors;
```

### §1.2 Typography

The platform uses **Larsseit** (same as web). Font files live at:
`apps/mobile/assets/fonts/` — copy from `font/Larsseit-Sans-Serif-Font-Family/Larsseit/Larsseit/*.otf`

**Font loading pattern:**

```typescript
// apps/mobile/app/_layout.tsx — add to root layout
import { useFonts } from 'expo-font';
import * as SplashScreen from 'expo-splash-screen';

SplashScreen.preventAutoHideAsync();

// In RootLayout:
const [fontsLoaded] = useFonts({
  'Larsseit-Light':        require('../assets/fonts/Larsseit-Light.otf'),
  'Larsseit-Regular':      require('../assets/fonts/Larsseit-Regular.otf'),
  'Larsseit-Medium':       require('../assets/fonts/Larsseit-Medium.otf'),
  'Larsseit-Bold':         require('../assets/fonts/Larsseit-Bold.otf'),
  'Larsseit-ExtraBold':    require('../assets/fonts/Larsseit-ExtraBold.otf'),
});

useEffect(() => {
  if (fontsLoaded) SplashScreen.hideAsync();
}, [fontsLoaded]);

if (!fontsLoaded) return null;
```

**Typography scale constants:**

```typescript
// constants/typography.ts
export const Typography = {
  displayLg: { fontFamily: 'Larsseit-ExtraBold', fontSize: 32, lineHeight: 38, letterSpacing: -0.5 },
  displayMd: { fontFamily: 'Larsseit-Bold',      fontSize: 24, lineHeight: 30, letterSpacing: -0.3 },
  h1:        { fontFamily: 'Larsseit-Bold',      fontSize: 20, lineHeight: 26 },
  h2:        { fontFamily: 'Larsseit-Medium',    fontSize: 17, lineHeight: 22 },
  h3:        { fontFamily: 'Larsseit-Medium',    fontSize: 15, lineHeight: 20 },
  bodyLg:    { fontFamily: 'Larsseit-Regular',   fontSize: 16, lineHeight: 24 },
  body:      { fontFamily: 'Larsseit-Regular',   fontSize: 14, lineHeight: 20 },
  bodySm:    { fontFamily: 'Larsseit-Regular',   fontSize: 13, lineHeight: 18 },
  label:     { fontFamily: 'Larsseit-Medium',    fontSize: 12, lineHeight: 16 },
  caption:   { fontFamily: 'Larsseit-Regular',   fontSize: 11, lineHeight: 14 },
  mono:      { fontFamily: 'Courier', fontSize: 12, lineHeight: 16 },
} as const;
```

### §1.3 Spacing System

```typescript
// constants/spacing.ts
export const Spacing = {
  px:  1,
  0.5: 2,
  1:   4,
  1.5: 6,
  2:   8,
  2.5: 10,
  3:   12,
  3.5: 14,
  4:   16,
  5:   20,
  6:   24,
  7:   28,
  8:   32,
  10:  40,
  12:  48,
  14:  56,
  16:  64,
} as const;

// Usage: padding: Spacing[4]  → 16
// Standard screen padding: Spacing[4] (16) horizontal, never less
// Card inner padding: Spacing[4] (16)
// Tab bar height: 60 (iOS) / 56 (Android)
// Safe area: always use useSafeAreaInsets()
```

### §1.4 Border Radius

```typescript
// constants/radius.ts
export const Radius = {
  sm:   6,
  md:   8,
  lg:   12,
  xl:   16,
  '2xl': 20,
  full: 9999,
} as const;
```

### §1.5 Shadows (iOS + Android)

```typescript
// constants/shadows.ts
import { Platform } from 'react-native';

export const Shadows = {
  sm: Platform.select({
    ios: {
      shadowColor: '#000',
      shadowOffset: { width: 0, height: 1 },
      shadowOpacity: 0.25,
      shadowRadius: 2,
    },
    android: { elevation: 2 },
  }),
  md: Platform.select({
    ios: {
      shadowColor: '#000',
      shadowOffset: { width: 0, height: 2 },
      shadowOpacity: 0.35,
      shadowRadius: 6,
    },
    android: { elevation: 4 },
  }),
  accent: Platform.select({
    ios: {
      shadowColor: '#EFFE5E',
      shadowOffset: { width: 0, height: 0 },
      shadowOpacity: 0.30,
      shadowRadius: 8,
    },
    android: { elevation: 6 },
  }),
} as const;
```

### §1.6 Motion Tokens

Use **React Native Reanimated 3** for performant animations. Install: `npx expo install react-native-reanimated`

```typescript
// constants/motion.ts
export const Motion = {
  duration: {
    fast:    150,
    normal:  250,
    slow:    400,
  },
  easing: {
    spring: { damping: 20, stiffness: 300 },
    ease:   { damping: 30, stiffness: 200 },
  },
} as const;

// Usage pattern — fade-in on mount:
import Animated, { FadeIn, FadeInDown } from 'react-native-reanimated';

<Animated.View entering={FadeIn.duration(250)}>
  {/* content */}
</Animated.View>

// Card press animation:
import { useAnimatedStyle, useSharedValue, withSpring } from 'react-native-reanimated';

const scale = useSharedValue(1);
const animatedStyle = useAnimatedStyle(() => ({
  transform: [{ scale: scale.value }]
}));
// onPressIn: scale.value = withSpring(0.97)
// onPressOut: scale.value = withSpring(1)
```

### §1.7 Icon System

Use `@expo/vector-icons` — ships with Expo SDK 50, no install needed.
Use `Ionicons` exclusively for consistency.

```typescript
import { Ionicons } from '@expo/vector-icons';
import { Colors } from '@/constants/colors';

// Standard usage
<Ionicons name="briefcase-outline" size={20} color={Colors.text.secondary} />

// Accent usage (active tab, primary action)
<Ionicons name="briefcase" size={22} color={Colors.accent.primary} />
```

**Icon map — screen/action to Ionicons name:**

| Screen / Action      | Inactive icon name        | Active icon name         |
|----------------------|---------------------------|--------------------------|
| Home / Matches       | `home-outline`            | `home`                   |
| Applications         | `layers-outline`          | `layers`                 |
| Interviews           | `calendar-outline`        | `calendar`               |
| Offers               | `document-text-outline`   | `document-text`          |
| Profile              | `person-outline`          | `person`                 |
| Notifications (bell) | `notifications-outline`   | `notifications`          |
| Settings (gear)      | `settings-outline`        | `settings`               |
| Search               | `search-outline`          | `search`                 |
| Back arrow           | `arrow-back`              | —                        |
| Chevron right        | `chevron-forward`         | —                        |
| Chevron down         | `chevron-down`            | —                        |
| Check mark           | `checkmark-circle`        | —                        |
| Close / dismiss      | `close`                   | —                        |
| Upload               | `cloud-upload-outline`    | `cloud-upload`           |
| Edit                 | `pencil-outline`          | `pencil`                 |
| External link        | `open-outline`            | —                        |
| Info                 | `information-circle-outline` | —                     |
| Warning              | `warning-outline`         | —                        |
| Star / rating        | `star-outline`            | `star`                   |
| Location             | `location-outline`        | —                        |
| Clock / time         | `time-outline`            | —                        |
| Money / rate         | `cash-outline`            | —                        |
| Skills / wrench      | `construct-outline`       | —                        |
| Briefcase / role     | `briefcase-outline`       | `briefcase`              |
| Company / building   | `business-outline`        | —                        |
| Score / gauge        | `speedometer-outline`     | `speedometer`            |
| Resume / doc         | `document-outline`        | `document`               |

### §1.8 Navigation Architecture

**Target architecture:** Bottom tab navigator (5 tabs) + nested Stack for detail screens.
The current codebase uses only a Stack — **this must be converted.**

```
apps/mobile/app/
├── _layout.tsx                        # Root — providers + auth redirect
├── (auth)/
│   ├── _layout.tsx                    # Stack, headerShown: false
│   ├── login.tsx
│   ├── register.tsx
│   └── forgot-password.tsx
└── (app)/
    ├── _layout.tsx                    # TABS — 5 tabs (see below)
    ├── (home)/
    │   ├── index.tsx                  # Matches dashboard
    │   └── matches/
    │       └── [id].tsx               # Match detail
    ├── (applications)/
    │   └── index.tsx                  # My shortlists / applications
    ├── (interviews)/
    │   └── index.tsx                  # Interview schedule
    ├── (offers)/
    │   └── index.tsx                  # Offers received
    ├── (profile)/
    │   ├── index.tsx                  # Profile view/edit
    │   └── notifications.tsx          # Notifications (accessed from profile)
    ├── onboarding/
    │   ├── resume.tsx                 # Resume upload
    │   └── profile-review.tsx         # AI-generated profile review
    └── components/                    # Shared UI components
        ├── match-card.tsx
        ├── profile-editor.tsx
        ├── status-badge.tsx
        ├── score-ring.tsx
        ├── card.tsx
        ├── button.tsx
        ├── input.tsx
        ├── skeleton.tsx
        ├── empty-state.tsx
        └── section-header.tsx
```

**Tab layout implementation:**

```typescript
// apps/mobile/app/(app)/_layout.tsx
import { Tabs } from 'expo-router';
import { Ionicons } from '@expo/vector-icons';
import { Colors } from '@/constants/colors';
import { useTalentWorkflow } from '../providers/talent-workflow-provider';

export default function AppTabLayout() {
  const { unreadCount } = useTalentWorkflow();

  return (
    <Tabs
      screenOptions={{
        headerShown: false,
        tabBarStyle: {
          backgroundColor: Colors.bg.surface,
          borderTopColor: Colors.border.default,
          borderTopWidth: 1,
          height: 60,
          paddingBottom: 8,
        },
        tabBarActiveTintColor:   Colors.accent.primary,
        tabBarInactiveTintColor: Colors.text.tertiary,
        tabBarLabelStyle: {
          fontFamily: 'Larsseit-Medium',
          fontSize: 11,
        },
      }}
    >
      <Tabs.Screen
        name="(home)"
        options={{
          title: 'Matches',
          tabBarIcon: ({ color, focused }) => (
            <Ionicons name={focused ? 'home' : 'home-outline'} size={22} color={color} />
          ),
        }}
      />
      <Tabs.Screen
        name="(applications)"
        options={{
          title: 'Applied',
          tabBarIcon: ({ color, focused }) => (
            <Ionicons name={focused ? 'layers' : 'layers-outline'} size={22} color={color} />
          ),
        }}
      />
      <Tabs.Screen
        name="(interviews)"
        options={{
          title: 'Interviews',
          tabBarIcon: ({ color, focused }) => (
            <Ionicons name={focused ? 'calendar' : 'calendar-outline'} size={22} color={color} />
          ),
        }}
      />
      <Tabs.Screen
        name="(offers)"
        options={{
          title: 'Offers',
          tabBarIcon: ({ color, focused }) => (
            <Ionicons name={focused ? 'document-text' : 'document-text-outline'} size={22} color={color} />
          ),
        }}
      />
      <Tabs.Screen
        name="(profile)"
        options={{
          title: 'Profile',
          tabBarIcon: ({ color, focused }) => (
            <Ionicons name={focused ? 'person' : 'person-outline'} size={22} color={color} />
          ),
          tabBarBadge: unreadCount > 0 ? unreadCount : undefined,
          tabBarBadgeStyle: { backgroundColor: Colors.accent.primary },
        }}
      />
    </Tabs>
  );
}
```

### §1.9 Core Component Specs

All reusable components live in `app/(app)/components/`. Build these before any screens.

---

**`card.tsx`** — Base surface container
```typescript
// Props
type CardProps = {
  children: React.ReactNode;
  style?: StyleProp<ViewStyle>;
  onPress?: () => void;
  variant?: 'default' | 'raised' | 'accent';
};

// Style rules:
// default:  backgroundColor: Colors.bg.surface,  borderColor: Colors.border.default
// raised:   backgroundColor: Colors.bg.raised,   borderColor: Colors.border.default
// accent:   backgroundColor: Colors.bg.surface,  borderColor: Colors.accent.primary
// Always: borderWidth: 1, borderRadius: Radius.lg, padding: Spacing[4]
// When onPress is defined: wrap in Pressable with scale animation (0.98 on press)
```

---

**`button.tsx`** — Action button
```typescript
type ButtonProps = {
  label: string;
  onPress: () => void;
  variant?: 'primary' | 'secondary' | 'ghost' | 'destructive';
  size?: 'sm' | 'md' | 'lg';
  loading?: boolean;
  icon?: string;  // Ionicons name
  disabled?: boolean;
  fullWidth?: boolean;
};

// Variant styles:
// primary:     bg #EFFE5E, text #000000,  fontFamily Larsseit-Bold
// secondary:   bg transparent, border #27272A,  text #FFFFFF
// ghost:       bg transparent, no border, text #A1A1AA
// destructive: bg #1F0606, border #EF4444, text #EF4444

// Size heights: sm=36, md=44, lg=52
// Loading: replace label with ActivityIndicator, color matches text color
// Always: borderRadius Radius.md
```

---

**`input.tsx`** — Text input
```typescript
type InputProps = {
  label?: string;
  placeholder?: string;
  value: string;
  onChangeText: (text: string) => void;
  error?: string;
  helper?: string;
  secureTextEntry?: boolean;
  multiline?: boolean;
  numberOfLines?: number;
  keyboardType?: KeyboardTypeOptions;
  autoCapitalize?: 'none' | 'words' | 'sentences';
  icon?: string;
};

// Style rules:
// Container: borderWidth 1, borderColor Colors.border.default, borderRadius Radius.md
// Background: Colors.bg.raised
// Text: Colors.text.primary, fontFamily Larsseit-Regular, fontSize 14
// Placeholder: Colors.text.tertiary
// Focused: borderColor Colors.accent.primary
// Error: borderColor Colors.status.error
// Label: Typography.label, color Colors.text.secondary, marginBottom 4
// Error text: Typography.caption, color Colors.status.error, marginTop 4
// Height: single-line 48px, multiline auto
```

---

**`status-badge.tsx`** — Status pill
```typescript
type StatusBadgeProps = {
  status: string;
  type: 'demand' | 'shortlist' | 'interview' | 'offer' | 'verification';
};

// Renders colored pill with status text
// Maps status string to Colors.demand / Colors.shortlist etc.
// Style: borderRadius Radius.full, paddingHorizontal 8, paddingVertical 3
// Text: Typography.label, fontFamily Larsseit-Medium
// Background: always 15% opacity of status color (use hex + '26' alpha suffix)
// Border: 1px solid status color
```

---

**`score-ring.tsx`** — Circular match score display
```typescript
type ScoreRingProps = {
  score: number;        // 0–100
  size?: number;        // default 64
  strokeWidth?: number; // default 4
};

// Uses react-native-svg (npx expo install react-native-svg)
// Two circles: track (Colors.border.default) + progress (color from Colors.score)
// Center label: score% in Typography.h2, color from Colors.score
// Score color rules:
//   ≥80: Colors.score.excellent (#EFFE5E)
//   ≥60: Colors.score.good      (#22C55E)
//   ≥40: Colors.score.fair      (#EAB308)
//   <40: Colors.score.low       (#EF4444)
```

---

**`skeleton.tsx`** — Loading placeholder
```typescript
type SkeletonProps = {
  width: number | string;
  height: number;
  borderRadius?: number;
  style?: StyleProp<ViewStyle>;
};

// Uses Animated pulse between Colors.bg.surface and Colors.bg.raised
// Loop forever at 900ms duration
// Never show skeleton for more than 10 seconds — show error state if query hasn't resolved
```

---

**`empty-state.tsx`** — No data screen
```typescript
type EmptyStateProps = {
  icon: string;          // Ionicons name
  title: string;
  description: string;
  action?: { label: string; onPress: () => void };
};

// Layout: centered vertically, icon size 48 (Colors.text.tertiary),
// title Typography.h2 (Colors.text.primary), marginTop 12
// description Typography.body (Colors.text.secondary), marginTop 8, textAlign center
// action: Button variant='secondary', marginTop 24
```

---

**`section-header.tsx`** — List section title
```typescript
type SectionHeaderProps = {
  title: string;
  action?: { label: string; onPress: () => void };
  count?: number;
};

// Row: title left (Typography.h3, Colors.text.primary)
// count: badge with Colors.accent.subtle bg, Colors.accent.primary text, marginLeft 6
// action: right-aligned, Typography.label, Colors.accent.primary
```

### §1.10 Score Breakdown Display

Match scores have a `scoreBreakdown` JSON field. Parse and display as a horizontal bar list.

```typescript
type ScoreBreakdownItem = {
  label: string;    // e.g. "Skill Match"
  value: number;    // 0–100
  weight: number;   // e.g. 0.35
  weighted: number; // value * weight contribution
};

// JSON structure of scoreBreakdown:
// {
//   skillMatch: 92, experience: 80, availability: 100,
//   pricingFit: 70, locationMatch: 85, culturalFit: 60, feedbackScore: 75
// }

// Weights (from platform spec):
// skillMatch: 35%, experience: 20%, availability: 10%,
// pricingFit: 10%, locationMatch: 10%, culturalFit: 10%, feedbackScore: 5%
```

### §1.11 Verification Status Display

| verificationStatus | Badge color        | Icon                        |
|--------------------|--------------------|-----------------------------|
| PENDING            | `#EAB308` (amber)  | `time-outline`              |
| VERIFIED           | `#22C55E` (green)  | `checkmark-circle`          |
| REJECTED           | `#EF4444` (red)    | `close-circle`              |

Show in profile header. PENDING = amber banner "Awaiting admin verification".
REJECTED = red banner with `verificationNotes` text.

### §1.12 Anti-Patterns — React Native Dark Mode

| Mistake                               | Fix                                                          |
|---------------------------------------|--------------------------------------------------------------|
| `backgroundColor: '#fff'` anywhere    | Always use `Colors.bg.base` or a surface color              |
| `color: '#000'`                       | Always use `Colors.text.primary`                            |
| Not wrapping in `SafeAreaView`        | Use `useSafeAreaInsets()` always                            |
| `TouchableOpacity` with default style | Wrap with `Pressable`, use `Animated.View` for animation     |
| Hardcoded `color="#38bdf8"`           | Replace with `Colors.accent.primary` (`#EFFE5E`)            |
| `backgroundColor: "#020617"`          | Replace with `Colors.bg.base` (`#000000`)                   |
| Keyboard avoidance absent            | Use `KeyboardAvoidingView` on auth/form screens             |
| No `contentInsetAdjustmentBehavior`  | Add `automaticallyAdjustContentInsets` on ScrollView        |
| Missing `refreshControl` prop         | Add `RefreshControl` on every list screen                   |
| `ActivityIndicator` default color     | Always set `color={Colors.accent.primary}`                  |

### §1.13 Required Dependencies

Run **before** building any screens:

```bash
# Core navigation + expo
npx expo install expo-router expo-status-bar expo-font expo-splash-screen
npx expo install expo-document-picker expo-file-system expo-secure-store
npx expo install react-native-safe-area-context react-native-screens

# Animations + graphics
npx expo install react-native-reanimated react-native-svg

# Apollo GraphQL
npm install @apollo/client graphql graphql-ws

# Utilities
npm install date-fns
```

**Do NOT install:** Tailwind CSS, shadcn/ui, Next.js, Recharts, or any web-only package.
**Do NOT install**: NativeWind (not currently used — keep StyleSheet API for consistency).

---

## PART 2 — SCREEN SPECIFICATIONS

### §2.1 Auth Screens

**All auth screens share:**
- Background: `Colors.bg.base` (`#000000`)
- Padding: 24px horizontal, centered vertically with `justifyContent: 'center'`
- Keyboard avoiding: `KeyboardAvoidingView behavior={Platform.OS === 'ios' ? 'padding' : 'height'}`
- Logo: Spriteburst dot `●` + "talent" text in Larsseit-ExtraBold — or platform logo image
- Form width: max 400, centered on tablets

---

#### Login (`(auth)/login.tsx`)

**Visual structure (top to bottom):**
```
[ Logo / Brand mark ]          — centered, marginBottom 40
[ "Sign in" ]                  — Typography.displayMd, Colors.text.primary
[ "Access your talent profile" ] — Typography.body, Colors.text.secondary, marginBottom 32
[ Email input ]                — autoCapitalize=none, keyboardType=email-address
[ Password input ]             — secureTextEntry
[ Error message ]              — if error, Typography.bodySm, Colors.status.error
[ Sign in button ]             — Button primary, fullWidth, marginTop 24
[ Forgot password link ]       — Typography.body, Colors.accent.primary, marginTop 16, right-aligned
[ Create account link ]        — Typography.body, Colors.text.secondary, textAlign center, marginTop 24
  "Don't have an account? [Create one →]"
```

**State machine:**
- idle → submitting → success (redirect /) | error (show message)
- `signIn()` from `useAuth()` — handles JWT storage

---

#### Register (`(auth)/register.tsx`)

**Visual structure:**
```
[ "Create account" ]           — Typography.displayMd
[ "Join as talent, get matched" ] — Typography.body, Colors.text.secondary
[ First name input ]           — autoCapitalize=words
[ Last name input ]            — autoCapitalize=words
[ Email input ]                — autoCapitalize=none
[ Password input ]             — secureTextEntry, min 8 chars note
[ "Talent" role badge ]        — non-interactive, shows role being registered
[ Create account button ]      — Button primary, fullWidth
[ Sign in link ]               — "Already have an account? Sign in"
```

**GraphQL:** `register(input: { email, password, role: TALENT })` → then redirect to `/onboarding/resume`

---

#### Forgot Password (`(auth)/forgot-password.tsx`)

**Visual structure:**
```
[ Back arrow ]                 — top left, navigates back
[ "Reset password" ]
[ "Enter your email to receive a reset link" ]
[ Email input ]
[ Send reset link button ]     — Button primary
[ Success state ]              — green card: "If an account exists, we've prepared a link"
[ In dev: token shown ]        — Typography.mono, Colors.accent.primary, if developmentResetToken
```

---

### §2.2 Onboarding Screens

Shown only when `!profile` (talent profile doesn't exist yet). After completion → redirect to `/`.

---

#### Resume Upload (`onboarding/resume.tsx`)

**Visual structure:**
```
[ Progress indicator ]         — Step 1 of 2, accent color fill
[ "Upload your resume" ]
[ "Our AI will build your profile draft" ]
[ Drop zone card ]             — dashed border Colors.border.accent, borderRadius Radius.lg
  Tap to select PDF
  Max 10MB
  FileSystem.readAsStringAsync → base64 → uploadAsset mutation
[ File selected: name + size ] — shown after pick, with remove button
[ "Build my profile" button ]  — primary, disabled until file selected
[ Privacy note ]               — Typography.caption, Colors.text.tertiary
  "Your resume is stored securely and only visible to matched recruiters."
```

**GraphQL:** `uploadAsset(input: { fileName, mimeType: 'application/pdf', contentBase64, assetType: RESUME })`
→ response gives `resumeUrl`
→ navigate to `onboarding/profile-review` with resumeUrl param

---

#### Profile Review (`onboarding/profile-review.tsx`)

**This is the `ProfileEditor` component in context of onboarding (creating, not updating).**

**Visual structure:**
```
[ Progress indicator ]         — Step 2 of 2
[ "Review your profile" ]
[ "Edit the AI-generated draft" ]
[ Profile form tabs ]          — horizontal scroll tabs: Info | Skills | Experience | Rates
  [ Tab: Personal Info ]
    First name, Last name, Headline, Summary (multiline)
    Industries (comma-separated), Location preferences
  [ Tab: Skills ]
    Skill search + add chips, proficiency selector per skill
    Years of experience per skill
  [ Tab: Experience ]
    Add experience entries: title, company, dates, description
    Certifications: name, issuer, dates
    Education entries
  [ Tab: Rates & Availability ]
    Hourly rate min/max + currency picker (USD/EUR/GBP)
    Availability selector (immediate/2 weeks/1 month/3 months)
    Available from date
[ "Publish profile" button ]   — primary, fullWidth, creates talent profile
[ "Save draft" link ]          — secondary action
```

**GraphQL:** `createTalentProfile(input: CreateTalentProfileInput!)` → redirect to `/`

---

### §2.3 Home / Matches Screen (`(home)/index.tsx`)

**The main talent dashboard. Shows matches and availability toggle.**

**Visual structure:**
```
[ Header (no tab bar header — custom) ]
  Left: "Good morning, {firstName}" Typography.h1
  Right: Notification bell icon with unreadCount badge
         → navigate to (profile)/notifications

[ Availability row ]            — full-width card, Colors.bg.surface
  Left: "You're [available]"    — status dot + text
  Right: quick-set buttons      — IMMEDIATE | 2 WKS | 1 MTH | OFF
         active = Colors.accent.primary bg, Colors.text.inverse text
         inactive = Colors.bg.raised bg, Colors.text.secondary text

[ Profile completion banner ]   — only if profileCompleteness < 80
  amber border card
  "Profile {n}% complete" + progress bar
  "Complete your profile →" link

[ Verification banner ]         — only if verificationStatus === 'PENDING'
  info card: "Your profile is under review. You're visible to recruiters."

[ "Your matches" section header ]
  title + match count

[ Match cards list ]            — FlatList, keyExtractor by id
  Each card: <MatchCard match={item} />
  ListEmptyComponent: <EmptyState> (see §2.3a)
  refreshControl: RefreshControl, onRefresh from useTalentWorkflow

[ Onboarding CTA ]              — if no profile, show onboarding prompt instead of matches
```

**§2.3a Empty match state:**
```
icon: "telescope-outline"
title: "No matches yet"
description: "Keep your profile updated and available — recruiters are actively searching."
action: { label: "Update availability", onPress: setAvailability }
```

**GraphQL:**
- `myMatches` query (via `useTalentWorkflow`)
- `updateAvailability` mutation (via `useTalentWorkflow`)
- `unreadCount` query (via `useTalentWorkflow`)

---

### §2.4 Match Detail Screen (`(home)/matches/[id].tsx`)

**Shows full shortlist entry for a specific matched role.**

**Visual structure (ScrollView):**
```
[ Stack header ]               — title=demand title, back arrow
[ Score hero ]                 — large ScoreRing (size=96) + "Match score" label
                                 centered card at top

[ Role card ]
  Company name + logo (avatar fallback)
  Role title, seniority level badge
  Location • remotePolicy • budgetMin–budgetMax currency
  Status badges: Demand status + Shortlist status

[ AI explanation card ]
  "Why you were matched" heading, Colors.accent.subtle bg
  aiExplanation text (from shortlist)

[ Score breakdown ]            — horizontal bar chart style
  For each dimension: label, bar (width = value%), percentage
  Skill Match 35% | Experience 20% | Availability 10% | etc.

[ Required skills ]
  Chip grid of skill names + proficiency required
  Highlight skills the talent has (green check) vs gaps (amber dot)

[ Role description ]           — full demand description text
[ Project requirements ]       — if present
[ Timeline ]                   — startDate, contractDuration, createdAt "posted X days ago"

[ Action bar — fixed bottom ]
  if talentStatus === 'INTERESTED' or 'NOT_INTERESTED': already responded chip
  if talentStatus === 'PENDING':
    [ "I'm interested" button ] — primary, calls respondToMatch(INTERESTED)
    [ "Pass" button ]           — secondary, calls respondToMatch(NOT_INTERESTED)

  if interview upcoming:
    [ Interview card ] — date/time, meetingUrl link, respond buttons (ACCEPTED/DECLINED)
```

**GraphQL:**
- Data comes from `useTalentWorkflow` — find match by id from `matches` array
- `respondToMatch(input: { shortlistId, talentStatus: TalentInterestStatus })`
- `respondToInterview(input: { interviewId, talentResponseStatus })`

---

### §2.5 Profile Screen (`(profile)/index.tsx`)

**View and edit the talent's own profile. Tab-based sections.**

**Visual structure:**
```
[ Profile header card ]
  Avatar (image or initials fallback, size 72)
  Full name, Typography.displayMd
  Headline text, Typography.body, Colors.text.secondary
  Verification badge (VERIFIED / PENDING / REJECTED)
  Profile completeness bar (Colors.accent.primary fill)
  "Edit profile" button → opens ProfileEditor in edit mode

[ Tab bar: Info | Skills | Experience | Documents ]

[ Tab: Info ]
  Summary text
  Industries list (chips)
  Location preferences
  Work visa eligibility
  Portfolio URLs (tappable links)
  Hourly rate: "${min}–${max} ${currency}/hr"
  Availability: large status badge

[ Tab: Skills ]
  Group by SkillCategory
  Each skill: name, PROFICIENCY badge, X years

[ Tab: Experience ]
  Timeline list:
    Each entry: title, company, "start – end (or Present)", description
  Certifications section: name, issuer, credential link
  Education: institution, degree, dates

[ Tab: Documents ]
  Resume file (if uploaded) — filename, "View" link
  Identity documents list — each with upload date
  Upload more documents button
```

**GraphQL:**
- `myProfile` query
- `updateTalentProfile` mutation
- `uploadAsset(assetType: IDENTITY_DOC | RESUME)` mutation
- `updateAvailability` mutation
- `updatePricing` mutation

---

### §2.6 Applications Screen (`(applications)/index.tsx`)

**All shortlists where the talent has been matched. Filter by status.**

**Visual structure:**
```
[ Screen header: "Applications" ]

[ Filter bar ]                 — horizontal scroll chips
  All | Interested | Under Review | Shortlisted | Rejected
  Active chip: Colors.accent.primary bg, Colors.text.inverse
  Inactive: Colors.bg.raised, Colors.text.secondary

[ Applications list ]          — FlatList
  Each item: compact ApplicationCard
    Role title + company
    Applied date / matched date
    Shortlist status badge (from Colors.shortlist)
    Talent interest status badge
    Match score: small pill "87%"
    → tap navigates to match detail (home)/matches/[id]

[ Empty state if no applications ]
  "No applications yet"
  "When recruiters match you, your applications appear here"
```

**GraphQL:** `myMatches` — full shortlist array, client-side filtered by status

---

### §2.7 Interviews Screen (`(interviews)/index.tsx`)

**All scheduled/completed/upcoming interviews.**

**Visual structure:**
```
[ Screen header: "Interviews" ]

[ Upcoming section header ]    — "Upcoming" + count
[ Upcoming interviews list ]   — sorted by scheduledAt ascending
  Each: InterviewCard (see below)

[ Past section header ]        — "Past" + count
[ Past interviews list ]       — sorted by scheduledAt descending

---
InterviewCard layout:
  Role title + company name
  Date: "Tuesday, March 24 at 2:30 PM"
  Duration: "45 minutes"
  Status badge (Colors.interview)
  TalentResponseStatus: ACCEPTED / DECLINED / PENDING chips
  If meetingUrl: "Join meeting →" button (Linking.openURL)
  If PENDING response + upcoming:
    [ Accept ] / [ Decline ] buttons inline
```

**GraphQL:**
- Data from `myMatches` → flatten interviews from each shortlist
- `respondToInterview(input: { interviewId, talentResponseStatus })`

---

### §2.8 Offers Screen (`(offers)/index.tsx`)

**All offers received.**

**Visual structure:**
```
[ Screen header: "Offers" ]

[ Active offers ]              — SENT status, sorted by createdAt desc
[ Offer card ]
  Role title + company
  "Offer received" label + date
  Hourly rate: "$X/hr" in Typography.h2, Colors.accent.primary
  Start date / end date
  Terms: expandable text (show first 100 chars → "Show more")
  Offer status badge
  If status === SENT:
    [ Accept offer ] button — primary — calls acceptOffer
    [ Decline offer ] button — secondary (destructive) — calls declineOffer

[ Past offers ]                — ACCEPTED / DECLINED / WITHDRAWN (collapsed by default)

[ Empty state ]
  icon: "document-text-outline"
  "No offers yet"
  "Offers will appear here when recruiters send them after interviews"
```

**GraphQL:**
- Data from `myMatches` → flatten offers from each shortlist interview
- `acceptOffer(id: ID!)` mutation
- `declineOffer(id: ID!)` mutation

---

### §2.9 Notifications Screen (`(profile)/notifications.tsx`)

**Accessible from the profile tab (bell icon in header).**

**Visual structure:**
```
[ Screen header: "Notifications" ]

[ Unread count: "X unread" ]   — Typography.body, Colors.text.secondary

[ Notifications list ]         — FlatList, sorted by createdAt desc
  Each: NotificationRow
    Dot: unread = Colors.accent.primary, read = transparent
    Icon: based on type (MATCH=briefcase, INTERVIEW=calendar, OFFER=document-text,
                         SYSTEM=information-circle)
    Title: Typography.body, Colors.text.primary (bold if unread)
    Body: Typography.bodySm, Colors.text.secondary
    Time: "2 hours ago" — Typography.caption, Colors.text.tertiary
    background: unread = Colors.bg.raised, read = Colors.bg.base
    → tap: markNotificationRead, then navigate if href in metadata

[ Empty state ]
  icon: "notifications-off-outline"
  "You're all caught up"
```

**GraphQL:**
- `notifications(unreadOnly: false)` query
- `markNotificationRead(input: { notificationId })` mutation
- `unreadCount` query

---

### §2.10 Settings (in Profile tab)

**Simple list in profile tab after profile card.**

**Sections:**
1. Account — Email address (read-only), Change password
2. Preferences — Notification preferences (future), Theme (dark only — no toggle)
3. Support — Contact support, Privacy policy, Terms of service
4. Sign out — destructive action, confirm dialog before signing out

**Sign out flow:**
- Alert: "Sign out?", "You'll need to sign back in to access your account"
- Buttons: "Cancel" / "Sign out" (destructive red)
- On confirm: `signOut()` from `useAuth()` → redirect to `/login`

---

## PART 3 — BUILD PROMPTS

### §3.1 Mandatory Prompt Header

**Paste this block at the start of EVERY Cursor/AI prompt for this mobile app:**

```
MOBILE PLATFORM CONTEXT:
- Framework: Expo SDK 50, React Native, Expo Router (file-based)
- Language: TypeScript strict (no `any`, no non-null assertions)
- Navigation: Bottom tabs (5 tabs) + nested Stack for detail screens
- Styling: React Native StyleSheet API — NO Tailwind, NO NativeWind, NO CSS
- Colors: import from constants/colors.ts (Colors.bg.base, Colors.accent.primary etc.)
- Typography: import from constants/typography.ts (Typography.h1 etc.)
- Spacing: import from constants/spacing.ts (Spacing[4] = 16)
- Fonts: 'Larsseit-Regular', 'Larsseit-Medium', 'Larsseit-Bold', 'Larsseit-ExtraBold'
- Icons: Ionicons from @expo/vector-icons — icon names in §1.7
- Apollo: useQuery/useMutation from @apollo/client — never call API directly
- Auth: useAuth() hook from app/providers/auth-provider — never manage tokens manually
- Safe area: always useSafeAreaInsets() for padding — no magic numbers for status bar
- Do NOT modify: providers/, _layout.tsx files, constants/colors.ts, constants/typography.ts

BRAND CRITICAL:
- Primary accent: #EFFE5E (Colors.accent.primary) — NOT #38bdf8 (wrong)
- Background: #000000 (Colors.bg.base) — NOT #020617 (wrong)
- Never use white backgrounds, light surfaces, or default RN styling
```

### §3.2 TypeScript Interfaces for Mobile

These types must be defined in `types/mobile.ts` (or inferred from GraphQL operations):

```typescript
// types/mobile.ts

// From shortlist query (myMatches)
export type MobileShortlist = {
  id: string;
  matchScore: number;
  scoreBreakdown: string;  // JSON — parse to ScoreBreakdownData
  aiExplanation: string;
  status: 'AI_MATCHED' | 'SHORTLISTED' | 'REVIEWING' | 'REJECTED' | 'HIRED';
  talentStatus: 'PENDING' | 'INTERESTED' | 'NOT_INTERESTED';
  demand: MobileDemand;
  interviews: MobileInterview[];
  createdAt: string;
};

export type MobileDemand = {
  id: string;
  title: string;
  description: string;
  location: string;
  remotePolicy: string;
  budgetMin: number | null;
  budgetMax: number | null;
  currency: string;
  status: string;
  experienceLevel: string;
  startDate: string | null;
  contractDuration: string | null;
  requiredSkills: Array<{
    id: string;
    isRequired: boolean;
    minimumYears: number | null;
    skill: { id: string; name: string; displayName: string; category: string };
  }>;
  company: { id: string; name: string; logoUrl: string | null };
  createdAt: string;
};

export type MobileInterview = {
  id: string;
  scheduledAt: string;
  duration: number;
  meetingUrl: string | null;
  status: 'SCHEDULED' | 'COMPLETED' | 'CANCELLED' | 'NO_SHOW';
  talentResponseStatus: 'PENDING' | 'ACCEPTED' | 'DECLINED';
  feedback: string | null;
  rating: number | null;
  offer: MobileOffer | null;
};

export type MobileOffer = {
  id: string;
  hourlyRate: number;
  startDate: string;
  endDate: string | null;
  terms: string;
  status: 'DRAFT' | 'SENT' | 'ACCEPTED' | 'DECLINED' | 'WITHDRAWN';
  createdAt: string;
};

export type MobileNotification = {
  id: string;
  type: string;
  title: string;
  body: string;
  read: boolean;
  metadata: string | null;  // JSON
  createdAt: string;
};

export type ScoreBreakdownData = {
  skillMatch: number;
  experience: number;
  availability: number;
  pricingFit: number;
  locationMatch: number;
  culturalFit: number;
  feedbackScore: number;
};

export type MobileTalentProfile = {
  id: string;
  firstName: string;
  lastName: string;
  headline: string;
  summary: string;
  avatarUrl: string | null;
  resumeUrl: string | null;
  industries: string[];
  seniorityLevel: string;
  availability: string;
  availableFrom: string | null;
  hourlyRateMin: number | null;
  hourlyRateMax: number | null;
  currency: string;
  locationPreferences: string[];
  workVisaEligibility: string[];
  identityDocumentUrls: string[];
  portfolioUrls: string[];
  verificationStatus: 'PENDING' | 'VERIFIED' | 'REJECTED';
  verificationNotes: string | null;
  profileCompleteness: number;
  skills: MobileTalentSkill[];
  experiences: MobileExperience[];
  certifications: MobileCertification[];
  educationEntries: MobileEducation[];
};

export type MobileTalentSkill = {
  id: string;
  proficiency: string;
  yearsOfExperience: number;
  skill: { id: string; name: string; displayName: string; category: string };
};

export type MobileExperience = {
  id: string;
  title: string;
  companyName: string;
  location: string | null;
  startDate: string;
  endDate: string | null;
  isCurrent: boolean;
  description: string;
};

export type MobileCertification = {
  id: string;
  name: string;
  issuer: string;
  issueDate: string | null;
  expirationDate: string | null;
  credentialUrl: string | null;
};

export type MobileEducation = {
  id: string;
  institution: string;
  degree: string;
  fieldOfStudy: string | null;
  startDate: string | null;
  endDate: string | null;
};
```

### §3.3 Delivery Sequence

Build in this exact order. Each phase depends on the previous.

**Phase 0 — Foundation (do first, always)**
1. `constants/colors.ts` — full Colors object
2. `constants/typography.ts` — Typography scale
3. `constants/spacing.ts` — Spacing scale
4. `constants/radius.ts` + `constants/shadows.ts`
5. `constants/motion.ts`
6. `types/mobile.ts` — all TypeScript interfaces
7. `assets/fonts/` — copy Larsseit .otf files

**Phase 1 — Shared components (build before any screens)**
1. `components/button.tsx`
2. `components/input.tsx`
3. `components/card.tsx`
4. `components/status-badge.tsx`
5. `components/skeleton.tsx`
6. `components/empty-state.tsx`
7. `components/score-ring.tsx`    ← requires react-native-svg
8. `components/section-header.tsx`

**Phase 2 — Navigation shell**
1. Convert `(app)/_layout.tsx` → Tabs (see §1.8)
2. Update root `_layout.tsx` — add font loading (see §1.2)

**Phase 3 — Auth screens** (Group: login → register → forgot-password)

**Phase 4 — Core talent flow** (Home → Match detail)
- Use §3.4 worked prompt for home screen
- Use §3.5 worked prompt for match detail

**Phase 5 — Workflow screens** (Applications → Interviews → Offers → Notifications)

**Phase 6 — Profile + Settings**

**Phase 7 — Onboarding flow** (Resume upload → Profile review)
- Do this last (least frequently hit path)

### §3.4 Worked Prompt: Home / Matches Screen

```
ROUTE: app/(app)/(home)/index.tsx
ROLE: TALENT (authenticated)
PATTERN: List screen with floating action (availability toggle)

Build the talent home screen for the AI Talent Marketplace mobile app.

[PASTE §3.1 MANDATORY HEADER HERE]

SCREEN REQUIREMENTS:
1. Custom header (no default Stack/Tabs header):
   - Left: "Good morning, {profile.firstName}" — Typography.h1, Colors.text.primary
   - Right: Ionicons notifications-outline, size 24, Colors.text.secondary
     - Badge with unreadCount if > 0, badge bg Colors.accent.primary
     - onPress: router.push('/(profile)/notifications')

2. Availability card (full-width, Colors.bg.surface, borderColor Colors.border.default):
   - Row: left "Status" label + current availability text; right = 4 quick-toggle chips
   - Chips: IMMEDIATE | 2 WKS | 1 MTH | OFF
   - Active chip: bg Colors.accent.primary, text Colors.text.inverse, fontFamily Larsseit-Bold
   - Inactive chip: bg Colors.bg.raised, text Colors.text.secondary
   - onPress each chip: call updateAvailability mutation, optimistic update

3. Profile completeness banner (conditional):
   - Show only if profile.profileCompleteness < 80
   - Amber border, bg Colors.status.warningBg
   - Text: "Profile {completeness}% complete — recruiters want more detail"
   - Progress bar: width = completeness%, bg Colors.status.warning
   - Link: "Complete profile →" → navigate to /(profile)

4. Matches section:
   - SectionHeader title="Your Matches" count={matches.length}
   - FlatList of matches, each rendered as <MatchCard match={item} />
   - ListEmptyComponent: EmptyState (icon: telescope-outline, title: "No matches yet", 
     description: "Stay available — recruiters are actively searching for your skills")
   - RefreshControl: onRefresh from useTalentWorkflow, tintColor Colors.accent.primary

5. Loading state: show 3 Skeleton cards (height 120, borderRadius Radius.lg)

6. Error state: Card with Colors.status.errorBg, error message, "Retry" Button

DATA HOOKS:
- const { session } = useAuth()
- const { profile, isLoading } = useTalentProfile()
- const { matches, availability, unreadCount, isRefreshing, refreshWorkflow,
          setAvailability, error } = useTalentWorkflow()

GRAPHQL (via providers, not direct calls):
- myMatches query (in talent-workflow-provider)
- updateAvailability mutation (via setAvailability from provider)
- unreadCount query (in talent-workflow-provider)

DO NOT modify talent-workflow-provider.tsx or talent-profile-provider.tsx.
Use existing hook return values only.
```

### §3.5 Worked Prompt: Match Detail Screen

```
ROUTE: app/(app)/(home)/matches/[id].tsx
ROLE: TALENT (authenticated)
PATTERN: Detail screen with fixed action bar

Build the match detail screen for the AI Talent Marketplace mobile app.

[PASTE §3.1 MANDATORY HEADER HERE]

SCREEN DATA:
- Read id from useLocalSearchParams(): const { id } = useLocalSearchParams<{ id: string }>()
- Find match from talent workflow: 
  const { matches } = useTalentWorkflow()
  const match = matches.find(m => m.id === id)
- If !match: show "Match not found" EmptyState with back button
- If loading: show 4 Skeleton sections

SCROLL LAYOUT (ScrollView with bottom padding 100 for action bar):

1. Score hero section (centered card):
   - ScoreRing size=96, score=match.matchScore
   - Below ring: "Match score" label (Typography.label, Colors.text.secondary)
   - Below: large score percentage (Typography.displayLg, color from Colors.score)

2. Role summary card (Card variant=default):
   - Company name + avatar (initials fallback, 36x36, bg Colors.bg.raised)
   - Demand title (Typography.h1)
   - Row: seniority badge + status badges (StatusBadge type=demand, type=shortlist)
   - Row: location • remotePolicy • budget range
   - Row: startDate if present (Ionicons time-outline, Spacing[1.5])

3. AI explanation card (bg Colors.accent.subtle, borderColor Colors.accent.primary):
   - Header row: Ionicons sparkles-outline (Colors.accent.primary) + "Why you matched"
   - match.aiExplanation text (Typography.body, Colors.text.primary)

4. Score breakdown section:
   - SectionHeader title="Score Breakdown"
   - Parse match.scoreBreakdown JSON → ScoreBreakdownData
   - For each of 7 dimensions:
     Row: label (Typography.body) | bar | percentage (Typography.body, Colors.text.secondary)
     Bar: height 6, borderRadius 3, bg Colors.border.default, inner width=value%
     Bar fill color: same logic as ScoreRing (≥80 accent, ≥60 green, ≥40 amber, else red)

5. Required skills section:
   - SectionHeader title="Required Skills"
   - Chip grid (flexWrap: wrap, gap: 8)
   - Each chip: skill displayName + (if talent has skill: checkmark icon in Colors.status.success)
   - Required chips: solid border Colors.border.strong
   - Nice-to-have: dashed border Colors.border.default

6. Role details (two sections — collapsible):
   - "Description": demand.description
   - "Requirements": demand.projectRequirements (if present)

FIXED ACTION BAR (position absolute bottom 0, bg Colors.bg.surface, borderTop):
- if talentStatus === 'PENDING':
    Button primary "I'm interested" fullWidth (flex 1)
    Button secondary "Pass" (flex 0.4)
    → respondToMatch(shortlistId: match.id, talentStatus: INTERESTED | NOT_INTERESTED)
- if INTERESTED: green chip "You expressed interest"
- if NOT_INTERESTED: grey chip "You passed on this role"
- if interview exists (match.interviews[0]):
    Show interview summary: date + time + status badge
    If talentResponseStatus === PENDING: Accept / Decline buttons
    If ACCEPTED + meetingUrl: "Join meeting →" button (Linking.openURL)

MUTATIONS:
- respondToMatch(input: { shortlistId: match.id, talentStatus })
- respondToInterview(input: { interviewId, talentResponseStatus })
```

---

## PART 4 — INTEGRATION RULES

### §4.1 Protected Files — Do NOT Overwrite

These files are correct and must not be regenerated:

| File | Reason |
|------|--------|
| `app/_layout.tsx` | Auth redirect logic — only add font loading |
| `app/providers/auth-provider.tsx` | JWT storage + refresh logic |
| `app/providers/apollo-provider.tsx` | GraphQL client setup |
| `app/providers/talent-profile-provider.tsx` | Profile CRUD + upload logic |
| `app/providers/talent-workflow-provider.tsx` | Match + availability logic |
| `app/lib/graphql.ts` | Raw fetch utility for non-Apollo requests |
| `package.json` | Dependency versions |
| `app.json` / `app.config.ts` | Expo config |

### §4.2 GraphQL Operations — TALENT Role Only

The mobile app ONLY uses TALENT-role operations. Do NOT include RECRUITER or ADMIN operations.

**Queries used by mobile:**

| Operation | Variables | Used in |
|-----------|-----------|---------|
| `myProfile` | — | profile-provider |
| `myMatches` | — | talent-workflow-provider |
| `notifications` | `unreadOnly`, `pagination` | notifications screen |
| `unreadCount` | — | talent-workflow-provider |
| `skills` | `search`, `pagination` | profile editor skill search |

**Mutations used by mobile:**

| Operation | Input type | Used in |
|-----------|------------|---------|
| `register` | `RegisterInput` | register screen |
| `login` | `LoginInput` | login screen |
| `refreshToken` | `RefreshTokenInput` | auth-provider auto-refresh |
| `forgotPassword` | `ForgotPasswordInput` | forgot-password screen |
| `createTalentProfile` | `CreateTalentProfileInput` | profile-review onboarding |
| `updateTalentProfile` | `UpdateTalentProfileInput` | profile editor |
| `uploadAsset` | `UploadAssetInput` | resume + identity docs |
| `updateAvailability` | `UpdateAvailabilityInput` | home screen + profile |
| `updatePricing` | `UpdatePricingInput` | profile editor |
| `respondToMatch` | `RespondToMatchInput` | match detail |
| `respondToInterview` | `RespondToInterviewInput` | match detail + interviews |
| `acceptOffer` | `id: ID!` | offers screen |
| `declineOffer` | `id: ID!` | offers screen |
| `markNotificationRead` | `MarkNotificationReadInput` | notifications screen |

**Operation naming convention for gql documents:**
```typescript
// TALENT queries
export const MY_PROFILE = gql`query MyProfile { myProfile { ... } }`
export const MY_MATCHES = gql`query MyMatches { myMatches { ... } }`
export const MY_NOTIFICATIONS = gql`query MyNotifications($unreadOnly: Boolean) { notifications(unreadOnly: $unreadOnly) { ... } }`
export const UNREAD_COUNT = gql`query UnreadCount { unreadCount }`
export const SEARCH_SKILLS = gql`query SearchSkills($search: String) { skills(search: $search) { ... } }`

// TALENT mutations
export const REGISTER = gql`mutation Register($input: RegisterInput!) { register(input: $input) { ... } }`
export const LOGIN = gql`mutation Login($input: LoginInput!) { login(input: $input) { ... } }`
export const CREATE_TALENT_PROFILE = gql`mutation CreateTalentProfile($input: CreateTalentProfileInput!) { createTalentProfile(input: $input) { ... } }`
export const UPDATE_TALENT_PROFILE = gql`mutation UpdateTalentProfile($input: UpdateTalentProfileInput!) { updateTalentProfile(input: $input) { ... } }`
export const UPLOAD_ASSET = gql`mutation UploadAsset($input: UploadAssetInput!) { uploadAsset(input: $input) { file { key url } profile { id } } }`
export const UPDATE_AVAILABILITY = gql`mutation UpdateAvailability($input: UpdateAvailabilityInput!) { updateAvailability(input: $input) { id availability availableFrom } }`
export const RESPOND_TO_MATCH = gql`mutation RespondToMatch($input: RespondToMatchInput!) { respondToMatch(input: $input) { id talentStatus } }`
export const RESPOND_TO_INTERVIEW = gql`mutation RespondToInterview($input: RespondToInterviewInput!) { respondToInterview(input: $input) { id talentResponseStatus } }`
export const ACCEPT_OFFER = gql`mutation AcceptOffer($id: ID!) { acceptOffer(id: $id) { id status } }`
export const DECLINE_OFFER = gql`mutation DeclineOffer($id: ID!) { declineOffer(id: $id) { id status } }`
export const MARK_READ = gql`mutation MarkRead($input: MarkNotificationReadInput!) { markNotificationRead(input: $input) { id read } }`
```

### §4.3 Auth + Token Flow

Never manage tokens manually outside of `auth-provider.tsx`.

- Tokens stored in `expo-secure-store` under key `atm-mobile-session`
- `accessToken` injected as `Authorization: Bearer` header in `apollo-provider.tsx`
- `refreshToken` called automatically when 401 received
- `signOut()` clears SecureStore and redirects to `/login`
- Role check: `session.user.role === 'TALENT'` — if ever `RECRUITER` or `ADMIN`, still works (talent profile just won't exist)

### §4.4 Navigation Conversion (Stack → Tabs)

The current `(app)/_layout.tsx` is a Stack. Replace with the Tabs implementation from §1.8.

**Migration checklist:**
- [ ] Old Stack screen names become tab route names
- [ ] `applications`, `interviews`, `offers` move from Stack children to tab groups
- [ ] `profile` becomes tab group, not Stack screen
- [ ] `matches/[id]` stays as nested Stack inside `(home)` tab group
- [ ] `onboarding/` stays outside tabs (Stack from root)
- [ ] `notifications` moves inside `(profile)` tab group

### §4.5 Environment Configuration

```bash
# apps/mobile/.env
EXPO_PUBLIC_API_URL=http://localhost:4000/graphql
EXPO_PUBLIC_API_WS_URL=ws://localhost:4000/graphql

# Production
EXPO_PUBLIC_API_URL=https://api.your-domain.com/graphql
```

```typescript
// Access in code
const apiUrl = process.env.EXPO_PUBLIC_API_URL ?? 'http://localhost:4000/graphql';
```

### §4.6 Merge Checklist (run before every commit)

- [ ] No hardcoded `#020617` or `#38bdf8` anywhere (old wrong colors)
- [ ] All colors reference `Colors.*` from `constants/colors.ts`
- [ ] All font families use string literals matching loaded font names exactly
- [ ] No `any` types in TypeScript
- [ ] No `require('../../../constants/colors')` — use absolute path alias `@/constants/colors`
- [ ] Every screen wrapped in `SafeAreaView` or uses `useSafeAreaInsets()`
- [ ] Every async operation has loading state (Skeleton or ActivityIndicator)
- [ ] Every async operation has error state (error card, not white screen)
- [ ] Every list has an empty state
- [ ] Every mutation called within a try/catch with Alert.alert on error
- [ ] No `console.log` left in production code
- [ ] `providers/` directory unchanged
- [ ] All 5 tabs navigable without crash

---

## PART 5 — COPY SYSTEM

### §5.1 Voice and Tone (Mobile)

Mobile copy is **shorter, warmer, more direct** than web (recruiters vs talent).

| Principle     | Detail |
|---------------|--------|
| First-person  | "Your matches" not "Talent matches" |
| Action-first  | Buttons say what happens: "Accept offer" not "OK" |
| Human timing  | "2 hours ago" not "2026-03-14T10:00Z" |
| No jargon     | "Role" not "Demand", "Company" not "Employer entity" |
| Encouragement | Empty states are motivating, not apologetic |

**Banned phrases:**
- "Loading..." (use Skeleton instead)
- "An error occurred" → be specific: "Couldn't load your matches"
- "Null" / "undefined" (never render raw JS values)
- "Submit" → use action-specific label: "Save profile", "Send response"
- "Please" → sounds passive

### §5.2 Screen Titles and Tab Labels

| Screen | Tab label | Stack header title |
|--------|-----------|--------------------|
| Home / Matches | Matches | — (custom header) |
| Applications | Applied | "Applications" |
| Interviews | Interviews | "Interviews" |
| Offers | Offers | "Offers" |
| Profile | Profile | — (custom header) |
| Match detail | — | `{demand.title}` at `{company.name}` |
| Notifications | — | "Notifications" |
| Login | — | hidden |
| Register | — | hidden |
| Forgot password | — | "Reset password" |
| Resume upload | — | "Upload resume" |
| Profile review | — | "Review your profile" |

### §5.3 Empty State Formulas

```
[Screen]  → [icon] → [title] → [description]

Matches   → telescope-outline → "No matches yet" 
           → "Keep your profile updated — recruiters are actively searching for your skills"

Applied   → layers-outline → "No applications yet"
           → "When recruiters match you, your applications appear here"

Interviews → calendar-outline → "No interviews scheduled"
           → "Once a recruiter shortlists you, they'll schedule an interview here"

Offers    → document-text-outline → "No offers yet"
           → "Offers appear here after a successful interview"

Notifications → notifications-off-outline → "You're all caught up"
              → "No new notifications right now"

Skills (search) → search-outline → "No skills found"
                → "Try a different search term"
```

### §5.4 Error State Formulas

Always show: error icon + specific message + retry action.

```
Failed to load matches    → "Couldn't load your matches" → Retry
Failed to update          → "Couldn't update [field]" → Try again
Auth failed               → "Invalid email or password"  → (no retry — user must fix input)
Upload failed             → "Couldn't upload your file — check it's a PDF under 10MB"
Network error             → "No connection — check your internet and try again" → Retry
```

---

## APPENDIX

### A.1 Route → GraphQL Query Map

| Route | Primary query | Secondary |
|-------|---------------|-----------|
| `(home)/index` | `myMatches` (via provider) | `unreadCount` |
| `(home)/matches/[id]` | from `myMatches` cache | `respondToMatch`, `respondToInterview` |
| `(applications)/index` | `myMatches` (client filter) | — |
| `(interviews)/index` | `myMatches` → flatten interviews | `respondToInterview` |
| `(offers)/index` | `myMatches` → flatten offers | `acceptOffer`, `declineOffer` |
| `(profile)/index` | `myProfile` | `updateTalentProfile`, `uploadAsset` |
| `(profile)/notifications` | `notifications` | `markNotificationRead` |
| `onboarding/resume` | — | `uploadAsset` |
| `onboarding/profile-review` | — | `createTalentProfile` |
| `(auth)/login` | — | `login` |
| `(auth)/register` | — | `register` |
| `(auth)/forgot-password` | — | `forgotPassword` |

### A.2 Design Token Constants — Complete File

```typescript
// constants/index.ts — re-exports all constants
export { Colors } from './colors';
export { Typography } from './typography';
export { Spacing } from './spacing';
export { Radius } from './radius';
export { Shadows } from './shadows';
export { Motion } from './motion';

// Path alias setup (tsconfig.json):
// "paths": { "@/*": ["./*"] }
// Usage: import { Colors } from '@/constants'
```

### A.3 Full Target Directory Tree

```
apps/mobile/
├── app/
│   ├── _layout.tsx                    # Root — providers + font loading + auth guard
│   ├── (auth)/
│   │   ├── _layout.tsx
│   │   ├── login.tsx
│   │   ├── register.tsx
│   │   └── forgot-password.tsx
│   ├── (app)/
│   │   ├── _layout.tsx                # Tabs (5 tabs)
│   │   ├── (home)/
│   │   │   ├── _layout.tsx            # Stack for matches
│   │   │   ├── index.tsx              # Matches dashboard
│   │   │   └── matches/
│   │   │       └── [id].tsx           # Match detail
│   │   ├── (applications)/
│   │   │   └── index.tsx
│   │   ├── (interviews)/
│   │   │   └── index.tsx
│   │   ├── (offers)/
│   │   │   └── index.tsx
│   │   ├── (profile)/
│   │   │   ├── index.tsx              # Profile view/edit
│   │   │   └── notifications.tsx
│   │   ├── onboarding/                # Outside tabs — entered before tabs shown
│   │   │   ├── resume.tsx
│   │   │   └── profile-review.tsx
│   │   └── components/                # Shared RN components
│   │       ├── button.tsx
│   │       ├── card.tsx
│   │       ├── empty-state.tsx
│   │       ├── input.tsx
│   │       ├── match-card.tsx
│   │       ├── profile-editor.tsx
│   │       ├── score-ring.tsx
│   │       ├── section-header.tsx
│   │       ├── skeleton.tsx
│   │       └── status-badge.tsx
│   ├── providers/                     # DO NOT TOUCH
│   │   ├── apollo-provider.tsx
│   │   ├── auth-provider.tsx
│   │   ├── talent-profile-provider.tsx
│   │   └── talent-workflow-provider.tsx
│   └── lib/
│       └── graphql.ts                 # Raw fetch utility
├── assets/
│   └── fonts/                         # Larsseit .otf files go here
│       ├── Larsseit-Light.otf
│       ├── Larsseit-Regular.otf
│       ├── Larsseit-Medium.otf
│       ├── Larsseit-Bold.otf
│       └── Larsseit-ExtraBold.otf
├── constants/
│   ├── colors.ts
│   ├── typography.ts
│   ├── spacing.ts
│   ├── radius.ts
│   ├── shadows.ts
│   └── motion.ts
├── types/
│   └── mobile.ts
├── app.json
├── tsconfig.json                      # with @/* path alias
├── babel.config.js                    # with reanimated plugin
└── package.json
```

### A.4 Babel Config (for Reanimated)

```javascript
// babel.config.js
module.exports = function (api) {
  api.cache(true);
  return {
    presets: ['babel-preset-expo'],
    plugins: ['react-native-reanimated/plugin'],  // MUST be last plugin
  };
};
```

### A.5 Common Expo / React Native Failure Modes

| Symptom | Cause | Fix |
|---------|-------|-----|
| White screen on launch | Font not loaded before render | `SplashScreen.preventAutoHideAsync()` + `useFonts` pattern |
| "fontFamily is not a system font" | Wrong font string in StyleSheet | Must match exact key passed to `useFonts()` |
| Blue accent color showing | Old `#38bdf8` hardcoded | Replace all with `Colors.accent.primary` |
| Light grey backgrounds | Default `backgroundColor` unset | Explicit `backgroundColor: Colors.bg.base` on every screen root |
| Tabs not showing | Wrong Expo Router file structure | Tab routes must be in named folders: `(home)`, `(profile)` etc. |
| SVG crash on Android | SVG without Android support | `npx expo install react-native-svg` + rebuild |
| Reanimated crash | Missing Babel plugin | Add `react-native-reanimated/plugin` to `babel.config.js` |
| Keyboard covers input | No KeyboardAvoidingView | Wrap auth forms with `KeyboardAvoidingView` |
| Safe area content cut off | Missing safe area handling | `useSafeAreaInsets()` for all screens |
| Graph/chart missing | Recharts imported | Recharts is WEB ONLY — no charts in mobile |
| Apollo query never fires | Component not inside ApolloProvider | Check provider is in `_layout.tsx` above all screens |
| SecureStore undefined | Running on web (Expo Go limitation) | Mobile only — use `AsyncStorage` fallback for web target |
| Fast Refresh breaks context | Context not memoized | `useMemo` and `useCallback` all context values |
| `useLocalSearchParams` undefined | Screen not in Router stack | Ensure file is under `app/` with correct Expo Router structure |
| `response` undefined from mutation | Destructuring Apollo result wrong | `const [mutate, { data, loading, error }] = useMutation(...)` |
| Notification badge not updating | `unreadCount` not reactive | Refetch `unreadCount` after `markNotificationRead` |
| FlatList performance poor | No `keyExtractor` | Always set `keyExtractor={(item) => item.id}` |
| Image not loading | Wrong src format | Use `{ uri: url }` format for `Image source` prop, never plain string |
| Tab badge color wrong | Default badge (red) showing | Set `tabBarBadgeStyle={{ backgroundColor: Colors.accent.primary }}` |
| `router.push` doesn't navigate | Wrong route path string | Paths must match exact folder structure: `/(home)/matches/${id}` |
| Text renders as inline block | Missing `flexShrink: 1` | Add `flexShrink: 1` to Text container when in a Row |
