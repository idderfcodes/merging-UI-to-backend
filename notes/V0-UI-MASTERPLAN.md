# v0 UI Master Plan — AI Talent Marketplace Platform

Inspired by: `maingoalandreference/AI Talent Marketplace Platform (SOW).md`

---

## 1) Mission of This Document

This is the **single source of truth** for how v0-generated UI should be created, reviewed, integrated, and shipped across the existing architecture:

- Web (Next.js 14 + Tailwind + shadcn/ui)
- Mobile (Expo + React Native + Expo Router)
- API (Node + Apollo GraphQL)
- AI engine (FastAPI, internal only)

It must be used from UI start to finish so every generated page is production-ready, not just visually attractive.

---

## 2) Architecture Alignment (Current Infrastructure)

### Existing Monorepo Surfaces

- `apps/web` → recruiter + admin + public/auth web UI
- `apps/mobile` → talent mobile app UI
- `apps/api` → GraphQL data/actions consumed by web/mobile
- `services/ai-engine` → internal AI endpoints called by API
- `packages/shared` / `packages/ui` / `packages/db` → shared contracts and design utilities

### Hard Constraints

1. No backend refactor for UI tasks.
2. No route architecture changes unless required by existing app conventions.
3. No secret keys, credentials, or production URLs inside UI code.
4. Keep existing RBAC behavior (TALENT / RECRUITER / ADMIN).
5. All generated UI must bind to real GraphQL operations (no persistent mock data).

---

## 3) v0 Usage Policy

## What v0 Should Do

- Generate **web page shells and components** for public/recruiter/admin surfaces.
- Generate reusable design primitives (headers, filters, tables, form shells, detail layouts, timeline sections).
- Generate consistent responsive patterns.

## What v0 Should NOT Do

- Generate mobile React Native code as final implementation.
- Define auth or RBAC logic.
- Define backend data contracts.
- Add fake static data as final source.

---

## 4) Visual System Rules (Important)

## No Card-Heavy UI

Per project direction: **avoid card-heavy layouts**.

Use this hierarchy instead:

1. Section headers + contextual toolbars
2. Structured data tables/lists
3. Split-panels and tabbed detail views
4. Inline KPI rows (not floating card grids)
5. Bordered surface blocks only when needed for clarity

Do not let v0 produce dashboard pages made of stacked decorative cards.

## Typography + Color Configuration Baseline

- Font primary: `Inter`
- Optional display font: `Manrope` (headings only, optional)
- 8px spacing system
- Radius: 10–12px maximum
- Low-shadow enterprise style
- Strong contrast for tables/forms/action states

Semantic color roles only:

- `primary`
- `accent`
- `neutral` scale
- `success`, `warning`, `destructive`, `info`

---

## 5) Animation Rules

## Web Animation (Required)

Use **Framer Motion** for web transitions:

- page enter/exit fade + slight translate (`y: 8 -> 0`)
- filter panel reveal/collapse
- row expansion in detail lists
- modal/sheet transitions
- optimistic feedback micro-interactions

Animation must be subtle:

- duration: 0.15s to 0.30s
- easing: standard ease-out
- never block user actions

## Mobile Animation Parity (Expo)

v0 web motion should be mirrored on mobile with native tooling:

- Expo + React Native Reanimated (or Moti where already used)
- Same intent, not identical CSS animation
- Keep native feel and 60fps priority

Rule: same motion language, platform-appropriate implementation.

---

## 6) Complete UI Surface Map (What Pages Exist + What’s Inside)

All pages below are expected references for v0 generation and wiring.

## A) Public + Auth Web

### 1. Landing (`/`)

Contains:

- value proposition
- platform module overview
- recruiter/admin/talent pathways
- trust + outcomes section
- CTA to login/register

### 2. Login (`/login`)

Contains:

- email/password form
- forgot-password link
- role-aware redirect behavior (wired)

### 3. Register (`/register`)

Contains:

- first/last name
- email/password
- validation messaging

### 4. Forgot Password (`/forgot-password`)

Contains:

- reset request form
- success/error state messaging

### 5. Reset Password (`/reset-password`)

Contains:

- token + password form
- validation + completion state

## B) Recruiter Web

### 1. Recruiter Dashboard

Contains:

- KPI summary row (not cards)
- recent activity list
- roles requiring action
- quick action toolbar

### 2. Post/Edit Role

Contains:

- role fields (title, skills, location, seniority, budget, dates)
- AI-assisted role description controls
- save/publish actions

### 3. Roles List

Contains:

- searchable/filterable demand table
- status chips
- row actions (view/edit/archive)

### 4. Role Detail (Tabbed)

Tabs include:

- Overview
- Shortlist
- Interviews
- Offers

Contains:

- sticky action bar
- timeline of workflow events
- role metadata panel

### 5. Smart Talent Search

Contains:

- semantic query input
- filter panel (skills, level, availability, location, pricing)
- results table/list with score + rationale

### 6. Shortlists Queue

Contains:

- ranked talent list
- score breakdown view
- shortlist actions

### 7. Interviews Queue + Detail

Contains:

- queue table with status filters
- detail panel for scheduling/reschedule/cancel/feedback

### 8. Offers Queue + Detail

Contains:

- offer status table
- send/withdraw/acceptance timeline

### 9. Recruiter Analytics

Contains:

- hiring velocity
- pipeline conversion
- role aging distribution
- top skills demand

## C) Admin Web

### 1. Admin Dashboard

Contains:

- global KPI row
- verification queue snapshot
- demand approvals snapshot
- system alerts

### 2. User Management

Contains:

- user table
- role update controls
- activate/deactivate actions

### 3. Talent Verification Queue

Contains:

- pending verification list
- approve/reject + notes

### 4. Company Management

Contains:

- company table
- recruiter assignment controls

### 5. Demand Approvals

Contains:

- review queue
- approve/reject/hard-to-fill flags

### 6. Concierge / Headhunter Assignment

Contains:

- concierge assignment workflow
- external candidate intake status

### 7. Platform Analytics

Contains:

- utilization metrics
- revenue/pricing trend views
- supply-demand gap visualizations

## D) Talent Mobile (Expo)

### 1. Auth Screens

- login
- register
- forgot password

### 2. Onboarding Screens

- resume upload
- profile review/edit
- identity/certification uploads

### 3. Talent Activity Screens

- match feed
- role detail
- applications
- interviews
- offers
- notifications
- profile + availability toggle

> Mobile visuals should mirror web design language, but implementation is native React Native components.

---

## 7) SOW Correlation Matrix

- 3.1 Registration/Profile → auth + onboarding + profile surfaces
- 3.2 Matching Engine → match feed + score/rank displays
- 3.3 Demand Management → post/edit role + roles list + demand detail
- 3.4 Role Assistant → AI-assisted role content panel
- 3.5 Shortlisting → shortlist queues + ranking UI
- 3.6 Smart Search → semantic search + advanced filters
- 3.7 Concierge → admin concierge assignment workflows
- 3.8 Interview/Hiring → interview/offer queues and detail workflows
- 3.12/3.13 Governance/Analytics → admin and recruiter analytics surfaces
- 3.15 Notifications → web/mobile notification patterns
- 4 Admin Platform → admin route group and management pages

---

## 8) v0 Prompt Contract (Use Every Time)

When generating each page in v0, include:

1. "Use Next.js + Tailwind + shadcn/ui patterns."
2. "Enterprise B2B design, no card-heavy layout."
3. "Use Framer Motion for subtle transitions (page/section/table interactions)."
4. "Provide responsive layout and accessibility-friendly structure."
5. "Include loading, empty, error, success states."
6. "Use realistic product copy, no lorem ipsum."
7. "Generate reusable components and clean props interfaces."

---

## 9) Integration Checklist (Mandatory)

For every imported v0 page:

1. Route alignment to actual app paths.
2. Auth + RBAC preserved.
3. Static data removed; GraphQL wired.
4. Form actions connected to live mutations.
5. Loading/empty/error states wired to real data flow.
6. Framer Motion integrated without performance regressions.
7. TypeScript strictness respected (no `any`).
8. Mobile parity task created for equivalent Expo screen.

---

## 10) Web-to-Mobile Parity Method

For each web page generated by v0:

1. Extract design tokens and information architecture.
2. Map to mobile screen(s) with native layout expectations.
3. Rebuild with Expo-native components and navigation.
4. Implement equivalent motion via Reanimated/Moti.
5. Validate behavior against same GraphQL data contracts.

Rule: parity in experience and hierarchy, not pixel-for-pixel CSS cloning.

---

## 11) Definition of Done (Per Page)

A UI page is complete only if all are true:

- production-quality visuals
- no-card-heavy enterprise structure applied
- Framer Motion behavior implemented (web)
- route/auth/RBAC integration complete
- real GraphQL data and actions wired
- loading/empty/error/success states complete
- responsive + accessible behavior verified
- no type or lint regressions

---

## 12) Delivery Sequence (Start to Finish)

1. Recruiter dashboard + roles list
2. Role create/edit + role detail tabs
3. Shortlist + smart search
4. Interviews + offers workflows
5. Admin dashboard + governance pages
6. Public/auth polish
7. Mobile parity pass for all talent screens
8. Final consistency sweep (motion, typography, spacing, states)

---

## 13) Hand-off Template for Each v0 Asset

Provide with each v0 output:

1. target route
2. user role surface (public/recruiter/admin)
3. required queries/mutations
4. expected states (loading/empty/error/success)
5. motion behaviors included
6. corresponding mobile parity screen(s)
7. screenshot/reference link

---

This is the enforced UI process for all remaining frontend work.

---

## 14) Current Route Matrix (Codebase-Verified)

Use this matrix when asking v0 to generate pages so route assumptions match the real app.

## Web Routes (Next.js)

### Public/Auth

- `/`
- `/login`
- `/register`
- `/forgot-password`
- `/reset-password`

### Recruiter

- `/dashboard`
- `/dashboard/roles`
- `/dashboard/roles/new`
- `/dashboard/roles/[id]`
- `/dashboard/shortlists`
- `/dashboard/search`
- `/dashboard/interviews`
- `/dashboard/interviews/[demandId]/[interviewId]`
- `/dashboard/offers`
- `/dashboard/offers/[demandId]/[offerId]`
- `/dashboard/analytics`

### Admin

- `/admin`
- `/admin/users`
- `/admin/verification`
- `/admin/companies`
- `/admin/approvals`
- `/admin/concierge`
- `/admin/analytics`

## Mobile Routes (Expo Router)

### Auth

- `(auth)/login`
- `(auth)/register`
- `(auth)/forgot-password`

### Talent App

- `(app)/index` (match feed)
- `(app)/matches/[id]`
- `(app)/applications`
- `(app)/interviews`
- `(app)/offers`
- `(app)/notifications`
- `(app)/profile`
- `(app)/onboarding/resume`
- `(app)/onboarding/profile-review`

---

## 15) Infrastructure Wiring Contract Per Page Type

For every generated page, define these before merge.

### Query/Mutation Contract

Each page PR must list:

1. GraphQL operations used
2. Required variables
3. Expected response fields
4. Mutation side-effects (cache update/refetch/redirect)

### Provider/Guard Contract

- Web pages must preserve existing auth + role protection.
- Mobile screens must remain inside current auth/app provider hierarchy.
- No direct client calls to AI engine from UI (API-only path).

### Environment Contract

- Web client uses configured GraphQL API URL via existing env chain.
- Mobile client uses Expo public GraphQL URL env.
- Never embed absolute production endpoints in page components.

---

## 16) No-Card Layout Blueprint (Mandatory Design Pattern)

Use this as the default screen structure instead of card mosaics:

1. **Page Header Row**
	- title
	- contextual status
	- primary/secondary actions
2. **Command Row**
	- search input
	- filter group
	- segment/tab switch
	- export/refresh actions
3. **Primary Data Region**
	- table/list as primary source of truth
	- sticky columns or sticky subheader for heavy workflows
4. **Detail Region**
	- side panel or tabbed detail section
	- timeline/events/actions
5. **State Regions**
	- loading skeleton
	- empty guidance
	- error recovery

Allowed surfaces:

- thin bordered containers
- split-pane layouts
- section dividers

Disallowed by default:

- dashboard built from decorative floating cards
- duplicated KPI cards with little action value

---

## 17) Animation Implementation Spec

### Web (Framer Motion)

Use shared motion tokens:

- `duration.fast = 0.15`
- `duration.base = 0.22`
- `duration.slow = 0.30`
- `ease.standard = [0.2, 0.8, 0.2, 1]`

Required motion patterns:

1. Page transition: opacity + translateY(8 -> 0)
2. Table row expansion: animated height + opacity
3. Filter drawer/panel: slide/fade in
4. Modal/sheet: scale(0.98 -> 1) + fade
5. Toast feedback: subtle upward reveal

Motion accessibility:

- Respect reduced motion preference.
- Keep core interactions usable with motion disabled.

### Mobile (Expo)

Equivalent intent via Reanimated/Moti:

1. Screen enter/exit fade/slide
2. Accordion/expansion transitions
3. Sheet/modal transitions
4. Feedback micro-interactions

Performance guardrails:

- avoid heavy layout thrashing animations
- prefer transform/opacity
- keep long lists virtualization-safe

---

## 18) v0 Prompt Templates (Copy/Paste)

Use these templates as baseline prompts and customize per page.

### Template A — Data Table Workflow Page

"Create a production-grade Next.js B2B workflow page using Tailwind + shadcn patterns. Route: [ROUTE].
Design constraints: no card-heavy layout, table-first information architecture, premium enterprise look.
Include: page header actions, filter/search row, data table with status chips and row actions, side detail panel, pagination, loading/empty/error states, and Framer Motion transitions for panel and row expand/collapse.
Use realistic recruiter/admin marketplace copy and accessible semantics."

### Template B — Tabbed Detail Page

"Create a production-grade Next.js detail page for [ENTITY] with tabs ([TAB_LIST]).
Design constraints: no decorative card grid, split layout with sticky action row and metadata panel.
Include timeline/events, primary actions, confirmations, loading/empty/error states, and subtle Framer Motion page/tab transitions.
Return reusable components with typed props."

### Template C — Public/Auth Page

"Create a modern Next.js auth/public page using Tailwind + shadcn patterns for [PAGE_NAME].
Use enterprise SaaS style, strong typography hierarchy, clean form UX, inline validation, accessible labels/focus states, success/error messaging, and responsive layout.
Avoid generic lorem text and avoid card-heavy visual treatment."

### Template D — Analytics Page

"Create a Next.js analytics page for [ROLE] with a KPI summary row (not cards), trend charts, segmented controls, and data table.
Use enterprise visual style, clear density controls, loading/empty/error states, and Framer Motion for chart/table section transitions.
Ensure reusable components and responsive layout."

---

## 19) Merge Readiness Gate (Must Pass)

A v0 UI delivery cannot merge unless all checks pass:

1. Route exists in matrix above.
2. Uses no-card blueprint.
3. Includes required states (loading/empty/error/success).
4. Uses Framer Motion (web) with reduced-motion fallback.
5. Static data replaced with GraphQL wiring.
6. Role guard behavior preserved.
7. Mobile parity mapping recorded.
8. Typecheck/lint pass.
9. No secrets/env leakage.

If any check fails, the page is considered design-only and not production-ready.

---

## 20) Copy System (Mandatory)

This section governs all product text generated by v0 and all copy merged into web/mobile UI.

## Brand Voice

Voice characteristics:

- clear
- confident
- professional
- human
- outcome-oriented

Tone by context:

- Marketing/Public pages: inspirational + direct
- Recruiter/Admin workflow pages: concise + operational
- Forms and validation: calm + actionable
- Errors: transparent + recovery-oriented

## Copy Principles

1. Say what the user can do now.
2. Prefer concrete outcomes over vague claims.
3. Use short sentences and plain language.
4. Remove jargon unless role-specific and necessary.
5. Every empty/error state must provide a next action.

## Copy Do / Don’t

Do:

- "Create a role to generate your first shortlist."
- "No interviews scheduled yet. Request one from Shortlist."
- "Verification pending. Review documents and choose approve or reject."

Don’t:

- "Unlock revolutionary hiring synergies."
- "Oops! Something went wrong."
- "Manage everything in one place" (without specifics)

## Banned/Weak Phrases

Avoid these in all product/UI copy:

- "streamline"
- "leverage"
- "synergy"
- "best-in-class"
- "revolutionary"
- "seamless" (unless concretely explained)

## Preferred Lexicon

Use these terms consistently:

- talent
- demand (not just "job")
- shortlist
- interview
- offer
- verification
- approval
- analytics
- platform admin

---

## 21) Copy Anatomy by UI Element

## Page Titles

- 2–6 words
- action or object oriented
- no marketing fluff

Examples:

- "Recruiter Dashboard"
- "Demand Approvals"
- "Smart Talent Search"

## Section Headers

- describe the data/action in that region
- no abstract language

Examples:

- "Roles Requiring Attention"
- "Interview Queue"
- "Verification Decisions"

## Body/Helper Text

- one sentence preferred
- explicit user value

Example:

- "Filter by skill, availability, and price range to find ready-to-interview candidates."

## Buttons / CTAs

- imperative verb + object
- keep to 2–4 words where possible

Examples:

- "Create Role"
- "Approve Demand"
- "Request Interview"
- "Send Offer"

## Form Labels

- concrete nouns
- no placeholders as label replacement

Examples:

- "Required Skills"
- "Budget Range"
- "Start Date"

## Empty States

Each empty state must include:

1. factual statement
2. short reason/context
3. one primary action

Template:

- "No [items] yet. [Reason/context]. [Primary action]."

## Error States

Each error must include:

1. what failed
2. what user can do next
3. optional retry action

Template:

- "We couldn’t load [resource]. Try again, or check your filters."

## Success States

Template:

- "[Entity] updated successfully."
- "Offer sent. The candidate has been notified."

---

## 22) Page-Level Copy Starter Pack

Use these as baseline copy seeds for v0 generation and final wiring.

## Public Landing (`/`)

- Hero title: "AI Talent Marketplace for High-Impact Hiring"
- Hero subtitle: "Match qualified talent faster with role intelligence, shortlists, and workflow governance in one platform."
- Primary CTA: "Get Started"
- Secondary CTA: "Sign In"

## Login (`/login`)

- Title: "Welcome Back"
- Subtitle: "Sign in to continue to your workspace."
- Primary CTA: "Sign In"
- Secondary link: "Forgot Password?"

## Recruiter Dashboard (`/dashboard`)

- Title: "Recruiter Dashboard"
- Subtitle: "Track open demands, shortlist progress, and hiring velocity."
- Primary CTA: "Create Role"

## Roles (`/dashboard/roles`)

- Title: "Role Demands"
- Subtitle: "Monitor demand status and move roles through the pipeline."
- Primary CTA: "New Role"

## Smart Search (`/dashboard/search`)

- Title: "Smart Talent Search"
- Subtitle: "Use semantic search and filters to find high-fit candidates."
- Primary CTA: "Run Search"

## Admin Dashboard (`/admin`)

- Title: "Platform Admin"
- Subtitle: "Oversee verification, approvals, and platform health."
- Primary CTA: "Review Queue"

## Verification (`/admin/verification`)

- Title: "Talent Verification"
- Subtitle: "Review submitted documents and complete verification decisions."
- Primary CTA: "Open Next Profile"

---

## 23) v0 Copy Prompt Add-On (Use With Every Prompt)

Append this block to every v0 prompt:

"Use concise enterprise product copy.
Do not use hype phrases (streamline, synergy, revolutionary, best-in-class).
All empty/error states must include a clear next action.
Use action-first CTAs (verb + object).
Use realistic recruiter/admin/talent wording aligned to hiring workflows.
Avoid lorem ipsum and generic placeholders."

---

## 24) Copy QA Gate (Required Before Merge)

Copy is approved only if all checks pass:

1. Follows brand voice (clear/confident/professional/human)
2. No banned weak phrases
3. CTAs are action-first
4. Empty states include next action
5. Error messages include recovery guidance
6. Terminology consistent with lexicon
7. Text length fits responsive layouts
8. Copy is specific to actual workflow context

If copy fails this gate, the page is not merge-ready.

---

## 25) Design Token Reference (Concrete Defaults)

Use these defaults unless explicitly overridden.

## Typography Tokens

- `font.ui = Inter, system-ui, sans-serif`
- `font.display = Manrope, Inter, system-ui, sans-serif`

- `text.xs = 12/16`
- `text.sm = 14/20`
- `text.base = 16/24`
- `text.lg = 18/28`
- `text.xl = 20/30`
- `text.2xl = 24/34`
- `text.3xl = 30/40`

Weights:

- `w.regular = 400`
- `w.medium = 500`
- `w.semibold = 600`
- `w.bold = 700`

## Spacing / Radius / Border Tokens

- Spacing base = `4px`
- Primary spacing rhythm = `8px`
- `radius.sm = 8`
- `radius.md = 10`
- `radius.lg = 12`
- `border.default = 1px solid var(--color-border)`

## Color Role Tokens (semantic, not brand-locked)

- `color.bg = #0B1020` (dark shell) / `#FFFFFF` (light shell, where applicable)
- `color.surface = #11172A`
- `color.surfaceAlt = #161E34`
- `color.text.primary = #E8ECF8`
- `color.text.secondary = #AAB4CF`
- `color.border = #27314B`

- `color.primary = #6366F1`
- `color.accent = #06B6D4`

- `color.success = #22C55E`
- `color.warning = #F59E0B`
- `color.destructive = #EF4444`
- `color.info = #3B82F6`

## Elevation / Shadow

- Prefer minimal shadows.
- Default: `shadow-sm` equivalent.
- Use border + contrast over depth for hierarchy.

---

## 26) Route-by-Route Blueprint Matrix (Execution Contract)

Use this matrix as mandatory structure for generation + integration.

| Route | Surface | Primary Goal | Must-Have Blocks | Primary Actions | Data Source Type |
|---|---|---|---|---|---|
| `/` | Public | Explain value + convert | Hero, value bullets, role pathways, CTA row | Get Started, Sign In | static + config |
| `/login` | Auth | Sign-in | Auth form, support links, error feedback | Sign In | mutation |
| `/register` | Auth | Create account | Register form, role/account hints, validation | Create Account | mutation |
| `/forgot-password` | Auth | Request reset | Email form, confirmation state | Send Reset Link | mutation |
| `/reset-password` | Auth | Complete reset | Token/password form, completion state | Reset Password | mutation |
| `/dashboard` | Recruiter | Operational overview | KPI row, activity feed, attention list, quick actions | Create Role | query |
| `/dashboard/roles` | Recruiter | Manage demands | Command row, demand table, status/filter controls | New Role, Open Role | query |
| `/dashboard/roles/new` | Recruiter | Create demand | Form sections, AI assist panel, validation states | Save Draft, Publish | mutation + AI-backed API flow |
| `/dashboard/roles/[id]` | Recruiter | Work demand lifecycle | Header, metadata rail, tabs (overview/shortlist/interviews/offers) | Request Interview, Send Offer | query + mutations |
| `/dashboard/shortlists` | Recruiter | Review ranked candidates | Filter row, ranked list/table, score explanation panel | Shortlist, Request Interview | query + mutations |
| `/dashboard/search` | Recruiter | Discover candidates | Semantic input, filter panel, result table/list | Run Search, Save Filters | query |
| `/dashboard/interviews` | Recruiter | Manage interviews | Interview queue table, status filters, schedule actions | Schedule, Reschedule, Cancel | query + mutations |
| `/dashboard/interviews/[demandId]/[interviewId]` | Recruiter | Interview detail actions | Detail header, timeline, feedback form | Submit Feedback | query + mutation |
| `/dashboard/offers` | Recruiter | Track offers | Offer queue table, status filters, aging indicators | Draft Offer, Send Offer | query + mutations |
| `/dashboard/offers/[demandId]/[offerId]` | Recruiter | Offer detail actions | Offer detail, terms summary, activity timeline | Send, Withdraw | query + mutation |
| `/dashboard/analytics` | Recruiter | Hiring analytics | KPI row, trend charts, conversion table | Export Report | query |
| `/admin` | Admin | Platform overview | KPI row, governance queues, alerts | Review Queue | query |
| `/admin/users` | Admin | Manage users | Search/filter toolbar, user table, bulk controls | Update Role, Activate/Deactivate | query + mutation |
| `/admin/verification` | Admin | Verify talent | Verification queue, document panel, decision controls | Approve, Reject | query + mutation |
| `/admin/companies` | Admin | Manage companies | Company table, assignment controls | Assign Recruiter | query + mutation |
| `/admin/approvals` | Admin | Approve demands | Approval queue, context panel, decision controls | Approve, Reject | query + mutation |
| `/admin/concierge` | Admin | Concierge workflow | Concierge queue, assignment panel, status timeline | Assign Concierge | query + mutation |
| `/admin/analytics` | Admin | Platform analytics | KPI row, trend/capacity charts, utilization tables | Export | query |

### Mobile parity mapping (quick reference)

- `/dashboard/search`, `/dashboard/shortlists` concepts ↔ `(app)/index`, `(app)/matches/[id]`
- Interview/offer lifecycle ↔ `(app)/interviews`, `(app)/offers`
- Profile/verification visibility ↔ `(app)/profile`, onboarding screens

---

## 27) Strict v0 Delivery Schema (Copy/Paste)

Every v0 handoff must provide this exact schema:

```yaml
route: "/dashboard/roles"
surface: "recruiter"
sourceFiles:
	- "components/roles-table.tsx"
	- "app/dashboard/roles/page.tsx"
designRules:
	noCardHeavyLayout: true
	framerMotionIncluded: true
	responsive: ["mobile", "tablet", "desktop"]
copyCompliance:
	bannedPhrasesUsed: false
	emptyStateHasAction: true
	errorStateHasRecovery: true
dataContract:
	queries:
		- name: "ListDemands"
			requiredFields: ["id", "title", "status", "createdAt"]
	mutations:
		- name: "ArchiveDemand"
states:
	loading: "skeleton-row"
	empty: "No demands yet. Create a role to generate your first shortlist."
	error: "We couldn’t load roles. Try again."
	success: "Role archived successfully."
mobileParity:
	relatedScreens:
		- "(app)/index"
		- "(app)/matches/[id]"
notes: "Route and query names must match real repo contracts before merge."
```

### Merge blocker checklist (binary)

- [ ] Route exists in route matrix
- [ ] No-card blueprint followed
- [ ] Framer Motion included (web)
- [ ] Static data removed
- [ ] GraphQL operations mapped
- [ ] Auth/RBAC preserved
- [ ] Copy QA gate passed
- [ ] Mobile parity mapping included
- [ ] Typecheck/lint clean

If any item is unchecked, do not merge.
