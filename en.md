# X-Craft — AI-Powered Twitter / X Management Platform

> A complete, locally-running AI system for managing, rewriting, generating, scheduling, and analysing content on X (Twitter). Built with Next.js 15, LM Studio, and a gold-on-ink design language powered by the Amiri font.

---

## Table of Contents

1. [Project Vision](#1-project-vision)
2. [Full Feature List](#2-full-feature-list)
3. [Technology Stack & Libraries](#3-technology-stack--libraries)
4. [Project File Structure](#4-project-file-structure)
5. [Database Schema](#5-database-schema)
6. [API Routes Map](#6-api-routes-map)
7. [AI Algorithms & Logic](#7-ai-algorithms--logic)
8. [Twitter Algorithm Insights Engine](#8-twitter-algorithm-insights-engine)
9. [Design System](#9-design-system)
10. [Page-by-Page Breakdown](#10-page-by-page-breakdown)
11. [Component Architecture](#11-component-architecture)
12. [State Management](#12-state-management)
13. [Authentication Flow](#13-authentication-flow)
14. [Scheduling System](#14-scheduling-system)
15. [Installation & Setup](#15-installation--setup)
16. [Environment Variables](#16-environment-variables)
17. [LM Studio Configuration](#17-lm-studio-configuration)
18. [Roadmap](#18-roadmap)

---

## 1. Project Vision

X-Craft was designed around one core idea: **your AI assistant should run on your own machine, processing your data locally, with zero third-party data exposure.**

All AI inference runs through **LM Studio** — a local LLM server compatible with the OpenAI API. Your tweets, drafts, and analytics never leave your computer to reach an AI cloud provider.

The platform is built first for **Arabic-speaking users** (specifically Saudi dialect) while supporting full English content creation. The UI direction is right-to-left (`dir="rtl"`) and every component is tested in both Arabic and Latin text contexts.

---

## 2. Full Feature List

### Core Features (User Requested)

| # | Feature | Description |
|---|---------|-------------|
| 1 | **Twitter OAuth Login** | Full OAuth 2.0 PKCE flow via NextAuth v5, scopes: read, write, follows |
| 2 | **Tweet Rewriter** | Paste any tweet URL → AI fetches, analyses language, rewrites it |
| 3 | **Arabic Saudi Dialect Translation** | English tweet → Arabic with authentic Saudi expressions |
| 4 | **Arabic → English Translation** | Arabic tweet → clean professional English |
| 5 | **Tweet Adjustment** | Keep the original meaning, improve style & impact |
| 6 | **Thread Support** | Detect thread URLs, rewrite all parts maintaining sequence logic |
| 7 | **Media Preservation** | Media URLs from original tweet described to AI for contextual rewriting |
| 8 | **AI Tweet Generator** | Write a topic idea → AI generates 3 high-engagement tweet variants |
| 9 | **Content Calendar** | Google Calendar–style monthly/weekly view for scheduled tweets |
| 10 | **Best Time to Post** | Algorithm-backed time slots based on Saudi audience activity data |
| 11 | **Tweet Scheduling** | Schedule single tweets or full threads days/weeks/months ahead |
| 12 | **Analytics Dashboard** | Charts: follower growth, views, likes, retweets, engagement rate |
| 13 | **Hashtag Analyser** | Trending score, competition level, average reach per hashtag |
| 14 | **Thread Builder** | Visual drag-and-drop thread composer with live preview |

### Extra Features Added (15 Additional)

| # | Feature | Description |
|---|---------|-------------|
| 15 | **Hook Score Meter** | Real-time 0–100 score rating the opening line's ability to stop the scroll |
| 16 | **Engagement Prediction** | AI predicts expected likes, retweets and viral probability before posting |
| 17 | **Viral Probability Index** | % chance the tweet spreads beyond immediate followers |
| 18 | **Tweet Templates Library** | Pre-built and user-saved templates by category (thread, opinion, tip, story) |
| 19 | **Draft Manager** | Save, organise, search and resume draft tweets with tag system |
| 20 | **Competitor Tracker** | Monitor up to 10 competitor handles: followers, posting cadence, top hashtags |
| 21 | **Audience Insights** | Age distribution, gender split, top countries, peak hours visualised |
| 22 | **Weekly Heatmap** | 7×24 grid showing engagement score per hour per day |
| 23 | **Bio Optimiser** | AI rewrites your Twitter bio with keywords, CTA and niche alignment |
| 24 | **Trending Topics Feed** | Real-time trending tags for Saudi Arabia with sentiment analysis |
| 25 | **Performance Reports** | Auto-generated weekly/monthly PDF reports with key metrics |
| 26 | **LM Studio Status Widget** | Live indicator showing local AI connection, loaded model, latency |
| 27 | **Multi-language Toggle** | Switch entire generated content between Arabic dialects and English |
| 28 | **Niche Selector** | Set your account niche (tech, business, sports…) to personalise all AI output |
| 29 | **Notifications Centre** | In-app alerts: post published, follower milestone, best time reminder |

---

## 3. Technology Stack & Libraries

### Framework & Runtime

| Package | Version | Role |
|---------|---------|------|
| `next` | 15.0.3 | Full-stack React framework (App Router) |
| `react` | 18.3.1 | UI rendering |
| `typescript` | 5.6.3 | Type safety across the entire codebase |
| `node` | ≥ 20 | Runtime |

### Authentication

| Package | Version | Role |
|---------|---------|------|
| `next-auth` | 5.0.0-beta.25 | OAuth 2.0 session management |
| `@auth/prisma-adapter` | 2.7.2 | Persists sessions and accounts in SQLite |

NextAuth v5 is used with the new **App Router handlers** pattern (`auth.ts` exports `handlers`, `auth`, `signIn`, `signOut`).

### Database & ORM

| Package | Version | Role |
|---------|---------|------|
| `prisma` | 5.22.0 | Schema definition, migrations, type-safe queries |
| `@prisma/client` | 5.22.0 | Generated query client |
| SQLite (default) | — | Local file-based database (`dev.db`) |

SQLite is used by default for zero-configuration local development. You can switch to PostgreSQL or MySQL by changing the `provider` in `prisma/schema.prisma` and updating `DATABASE_URL`.

### AI / LLM

| Package | Version | Role |
|---------|---------|------|
| `openai` | 4.67.3 | OpenAI-compatible SDK — points to LM Studio local endpoint |

LM Studio exposes an OpenAI-compatible REST API at `http://localhost:1234/v1`. The `openai` SDK is configured with `baseURL` pointing to this local address and `apiKey: "lm-studio"` (ignored by LM Studio but required by the SDK).

### Twitter / X API

| Package | Version | Role |
|---------|---------|------|
| `twitter-api-v2` | 1.18.0 | Twitter API v2 client — fetch tweets, post, thread, timeline |

The app uses **OAuth 2.0 PKCE** (not 1.0a) via the Twitter Developer Portal. Required scopes: `tweet.read tweet.write users.read offline.access follows.read`.

### UI & Styling

| Package | Version | Role |
|---------|---------|------|
| `tailwindcss` | 3.4.14 | Utility-first CSS framework |
| `framer-motion` | 11.11.17 | Page transitions and micro-animations |
| `lucide-react` | 0.460.0 | Icon set (1000+ SVG icons) |
| `@radix-ui/*` | various | Accessible headless UI primitives |
| `react-hot-toast` | 2.4.1 | Toast notification system |
| `clsx` + `tailwind-merge` | latest | Class name utility |

The Amiri font is loaded via `next/font/google` with subsets `arabic` and `latin`.

### Charts & Data Visualisation

| Package | Version | Role |
|---------|---------|------|
| `recharts` | 2.13.3 | Line, area, bar, pie charts |

All charts use a dark theme with gold accent colours defined via Tailwind CSS variables.

### Calendar & Scheduling

| Package | Version | Role |
|---------|---------|------|
| `react-day-picker` | 9.3.0 | Date picker component |
| `date-fns` | 4.1.0 | Date formatting, arithmetic, locale (Arabic) |

### Form Handling & Validation

| Package | Version | Role |
|---------|---------|------|
| `react-hook-form` | 7.53.2 | Performant form state management |
| `@hookform/resolvers` | 3.9.1 | Zod resolver bridge |
| `zod` | 3.23.8 | Schema validation for API inputs and forms |

### Drag & Drop

| Package | Version | Role |
|---------|---------|------|
| `react-beautiful-dnd` | 13.1.1 | Thread part reordering |

### HTTP Client

| Package | Version | Role |
|---------|---------|------|
| `axios` | 1.7.7 | HTTP requests from client components |

### Utilities

| Package | Version | Role |
|---------|---------|------|
| `node-cron` | 3.0.3 | Server-side cron for scheduled tweet posting |
| `sharp` | 0.33.5 | Image processing for media previews |
| `react-markdown` | 9.0.1 | Render markdown in AI explanations |
| `html2canvas` | 1.4.1 | Screenshot tweets for image export |
| `file-saver` | 2.0.5 | Download reports as files |
| `cheerio` | 1.0.0 | HTML parsing for URL preview scraping |

---

## 4. Project File Structure

```
x-craft/
│
├── prisma/
│   ├── schema.prisma              # Full DB schema: 12 models
│   └── seed.ts                    # Seeds default templates on first run
│
├── src/
│   ├── app/                       # Next.js App Router
│   │   │
│   │   ├── layout.tsx             # Root layout: Amiri font, RTL, Toaster
│   │   ├── page.tsx               # Landing page (unauthenticated)
│   │   ├── globals.css            # Design system: CSS variables, animations, utilities
│   │   ├── providers.tsx          # SessionProvider wrapper
│   │   │
│   │   ├── api/                   # All API route handlers
│   │   │   ├── auth/
│   │   │   │   └── [...nextauth]/
│   │   │   │       └── route.ts   # NextAuth GET/POST handler
│   │   │   │
│   │   │   ├── ai/
│   │   │   │   ├── rewrite/
│   │   │   │   │   └── route.ts   # POST: rewrite a tweet via LM Studio
│   │   │   │   ├── generate/
│   │   │   │   │   └── route.ts   # POST: generate tweets from topic
│   │   │   │   ├── analyze/
│   │   │   │   │   └── route.ts   # POST: score tweet + GET: LM Studio status
│   │   │   │   └── best-time/
│   │   │   │       └── route.ts   # GET: best posting time recommendations
│   │   │   │
│   │   │   ├── twitter/
│   │   │   │   ├── fetch-tweet/
│   │   │   │   │   └── route.ts   # POST: fetch tweet data from URL
│   │   │   │   ├── schedule/
│   │   │   │   │   └── route.ts   # GET/POST/PUT/DELETE: scheduled tweets
│   │   │   │   ├── analytics/
│   │   │   │   │   └── route.ts   # GET: analytics data + summary
│   │   │   │   ├── drafts/
│   │   │   │   │   └── route.ts   # GET/POST/PUT/DELETE: drafts
│   │   │   │   └── templates/
│   │   │   │       └── route.ts   # GET/POST/DELETE: tweet templates
│   │   │   │
│   │   │   └── cron/
│   │   │       └── route.ts       # GET: cron job — posts scheduled tweets
│   │   │
│   │   └── dashboard/             # Protected dashboard pages
│   │       ├── layout.tsx         # Auth guard + Sidebar layout
│   │       ├── page.tsx           # Main dashboard: stats + charts
│   │       │
│   │       ├── rewrite/
│   │       │   └── page.tsx       # Tweet rewriter tool
│   │       ├── generate/
│   │       │   └── page.tsx       # Tweet generator tool
│   │       ├── calendar/
│   │       │   └── page.tsx       # Google Calendar–style scheduler
│   │       ├── analytics/
│   │       │   └── page.tsx       # Full analytics with all charts
│   │       ├── threads/
│   │       │   └── page.tsx       # Thread builder with DnD reorder
│   │       ├── hashtags/
│   │       │   └── page.tsx       # Hashtag analyser + trending
│   │       ├── trending/
│   │       │   └── page.tsx       # Trending topics + sentiment
│   │       ├── scheduler/
│   │       │   └── page.tsx       # Best-time heatmap + auto-schedule
│   │       ├── templates/
│   │       │   └── page.tsx       # Template library CRUD
│   │       ├── drafts/
│   │       │   └── page.tsx       # Draft manager
│   │       ├── audience/
│   │       │   └── page.tsx       # Audience insights visualisations
│   │       ├── competitor/
│   │       │   └── page.tsx       # Competitor tracker
│   │       ├── bio/
│   │       │   └── page.tsx       # AI bio optimiser
│   │       ├── reports/
│   │       │   └── page.tsx       # Auto-generated performance reports
│   │       └── settings/
│   │           └── page.tsx       # Account settings, timezone, niche
│   │
│   ├── components/
│   │   ├── dashboard/
│   │   │   ├── Sidebar.tsx        # Collapsible nav sidebar with user stats
│   │   │   └── Header.tsx         # Sticky top bar: notifications, user menu
│   │   │
│   │   ├── calendar/
│   │   │   ├── CalendarGrid.tsx   # Monthly grid with event chips
│   │   │   ├── CalendarWeek.tsx   # Weekly timeline view
│   │   │   └── EventModal.tsx     # Create / edit scheduled tweet modal
│   │   │
│   │   ├── rewrite/
│   │   │   ├── TweetFetcher.tsx   # URL input + tweet card preview
│   │   │   ├── RewriteOptions.tsx # Mode/tone/dialect/length controls
│   │   │   └── RewriteResult.tsx  # Result card with score + copy actions
│   │   │
│   │   ├── generate/
│   │   │   ├── GenerateForm.tsx   # Topic + options form
│   │   │   └── GenerateCards.tsx  # 3 variant result cards with comparison
│   │   │
│   │   ├── threads/
│   │   │   ├── ThreadBuilder.tsx  # DnD reorderable thread composer
│   │   │   └── ThreadPreview.tsx  # Live mobile-frame thread preview
│   │   │
│   │   ├── shared/
│   │   │   ├── TweetCard.tsx      # Reusable tweet display card
│   │   │   ├── ScoreRing.tsx      # SVG circular score indicator
│   │   │   ├── LMStatusBadge.tsx  # LM Studio connection indicator
│   │   │   ├── CharCounter.tsx    # Twitter character counter (URL=23)
│   │   │   ├── HashtagBadge.tsx   # Clickable copy-to-clipboard hashtag
│   │   │   ├── LanguageSwitcher.tsx # AR/EN toggle
│   │   │   └── SkeletonCard.tsx   # Loading placeholder
│   │   │
│   │   └── ui/
│   │       ├── Button.tsx         # Variant: gold, ghost, danger, outline
│   │       ├── Input.tsx          # Dark themed input with label
│   │       ├── Textarea.tsx       # Auto-resize textarea
│   │       ├── Select.tsx         # Custom styled select
│   │       ├── Toggle.tsx         # iOS-style switch toggle
│   │       ├── Modal.tsx          # Full-screen overlay modal
│   │       ├── Badge.tsx          # Status / category badge
│   │       ├── Tooltip.tsx        # Hover tooltip
│   │       └── ProgressBar.tsx    # Animated fill progress bar
│   │
│   ├── lib/
│   │   ├── auth.ts                # NextAuth config: Twitter OAuth, callbacks, events
│   │   ├── prisma.ts              # Singleton Prisma client
│   │   ├── lmstudio.ts            # LM Studio client: rewrite, generate, analyze, bio
│   │   ├── twitter.ts             # Twitter API v2: fetch, post, thread, timeline
│   │   ├── algorithms.ts          # Best-time data, heatmap, score calculator
│   │   └── utils.ts               # cn(), formatNumber(), splitIntoThreadParts(), etc.
│   │
│   ├── hooks/
│   │   ├── useScheduledTweets.ts  # Fetch + mutate scheduled tweets
│   │   ├── useAnalytics.ts        # Fetch analytics with period selector
│   │   ├── useDrafts.ts           # Draft CRUD with optimistic updates
│   │   ├── useLMStatus.ts         # Poll LM Studio connection every 30s
│   │   └── useHashtags.ts         # Hashtag search and save
│   │
│   ├── store/
│   │   └── useAppStore.ts         # Zustand global store: UI state, preferences
│   │
│   └── types/
│       └── index.ts               # All TypeScript interfaces and type definitions
│
├── .env.example                   # Template for all environment variables
├── next.config.ts                 # Image domains, server actions size
├── tailwind.config.ts             # Gold palette, Amiri font, animations
├── tsconfig.json                  # Strict TypeScript configuration
├── package.json                   # All dependencies
├── README.en.md                   # This file (English)
└── README.ar.md                   # Arabic documentation
```

---

## 5. Database Schema

The Prisma schema defines **12 models** stored in SQLite (swappable to any relational DB):

```
User
 ├── id, name, email, image
 ├── twitterHandle, twitterId, twitterBio
 ├── followersCount, followingCount, tweetsCount
 ├── timezone (default: Asia/Riyadh)
 └── preferredLang (default: ar)

Account              ← NextAuth OAuth tokens
Session              ← NextAuth session records
VerificationToken    ← NextAuth email verification

ScheduledTweet
 ├── content, language, scheduledAt, status
 ├── isThread, threadParts (JSON), mediaUrls (JSON)
 ├── hashtags (JSON)
 └── actualViews, likes, retweets, replies (post-publish)

Draft
 ├── title, content, language
 ├── isThread, threadParts, hashtags
 └── tags (JSON) — user-defined organisation labels

Analytics
 ├── date (unique per user per day)
 ├── followers, totalViews, totalLikes, totalRetweets
 ├── engagementRate, impressions, profileVisits
 └── mentions

Template
 ├── title, content, language, category, hook
 ├── isPublic, isSystem (built-in templates)
 └── usageCount, avgEngagement

AudienceInsight
 ├── ageDistribution, genderSplit (JSON)
 ├── topCountries, topCities (JSON)
 └── peakHours, peakDays, topInterests, languageSplit (JSON)

Report
 ├── type (daily | weekly | monthly)
 ├── period (e.g. "2024-W48")
 └── data (JSON blob), summary (AI-written text)

Competitor
 ├── twitterHandle, name
 ├── followersCount, tweetsPerDay, engagementRate
 └── lastChecked

SavedHashtag
 ├── hashtag, category
 ├── usageCount, avgReach
 └── isFavorite

BestTimeRecommendation
 ├── dayOfWeek (0–6), hour (0–23)
 ├── score (float)
 └── timezone
```

---

## 6. API Routes Map

All routes under `/api/` are secured with `auth()` from NextAuth — unauthenticated requests receive a `401`.

```
POST   /api/auth/[...nextauth]        ← NextAuth OAuth handler
GET    /api/auth/[...nextauth]        ← NextAuth callback handler

POST   /api/ai/rewrite                ← Rewrite tweet via LM Studio
POST   /api/ai/generate               ← Generate tweets from topic
POST   /api/ai/analyze                ← Score + improve a tweet
GET    /api/ai/analyze                ← Check LM Studio connection
GET    /api/ai/best-time              ← Best posting times for user

POST   /api/twitter/fetch-tweet       ← Fetch tweet data from URL
GET    /api/twitter/schedule          ← List scheduled tweets (with filters)
POST   /api/twitter/schedule          ← Create a new scheduled tweet
PUT    /api/twitter/schedule          ← Update a scheduled tweet
DELETE /api/twitter/schedule?id=...   ← Cancel / delete a scheduled tweet

GET    /api/twitter/analytics         ← Analytics data + summary
GET    /api/twitter/drafts            ← List all drafts
POST   /api/twitter/drafts            ← Create draft
PUT    /api/twitter/drafts            ← Update draft
DELETE /api/twitter/drafts?id=...     ← Delete draft

GET    /api/twitter/templates         ← List templates (own + system)
POST   /api/twitter/templates         ← Create template
DELETE /api/twitter/templates?id=...  ← Delete template

GET    /api/cron                      ← Cron: post due scheduled tweets
                                         (secured by CRON_SECRET header)
```

### Request / Response Patterns

Every API route follows this pattern:

```ts
// Success
{ success: true, data: { ... } }

// Error
{ success: false, error: "Human-readable Arabic message", details?: "..." }
```

---

## 7. AI Algorithms & Logic

All AI calls are routed through `src/lib/lmstudio.ts`. The file exposes five main functions:

### 7.1 `rewriteTweet()`

**Inputs:**
- `originalTweet` — the raw text
- `originalLanguage` — detected via regex (`ar` | `en` | `other`)
- `mode` — one of 5 rewrite modes
- `tone`, `dialect`, `targetLength`, `audience`, `addHashtags`, `addEmojis`

**Algorithm:**

```
1. Build system prompt:
   - If Arabic output mode:
       - Include authentic Saudi dialect guide with specific expressions
       - Twitter engagement rules in Arabic
       - JSON-only output instruction
   - If English output mode:
       - Include hook theory, viral mechanics, CTA rules
       - JSON-only output instruction

2. Build user prompt:
   - Mode-specific instruction in matching language
   - Tweet text + optional media description
   - Thread note if isThread=true
   - JSON schema for expected output

3. Call LM Studio:
   temperature: 0.8 (creative but coherent)
   max_tokens: 2000

4. Parse JSON response:
   - Extract via regex: /\{[\s\S]*\}/
   - Fields: rewritten, threadParts, hashtags, explanation, hookScore, engagementTips

5. Fallback:
   - If JSON parse fails → return raw content as rewritten text
   - If connection fails → return structured error with Arabic message
```

**Saudi Dialect Guide (injected into system prompt):**
```
استخدم اللهجة السعودية الخليجية الأصيلة مع تعابير محلية مثل:
خوي، والله، عشاني، بس، كذا، شي، ماشي، عساك بخير
```

### 7.2 `generateTweet()`

**Inputs:** `topic`, `language`, `tone`, `format` (single|thread), `audience`, `keywords`, `niche`, `addHashtags`, `addEmojis`, `threadLength`, `dialect`

**Algorithm:**

```
1. Dual-language system prompt (ar or en)
2. Request exactly 3 tweet variants:
   - Variant 1: Direct statement / opinion
   - Variant 2: Story / narrative angle
   - Variant 3: Question / engagement hook
3. Each variant includes:
   - content
   - threadParts (if format=thread)
   - hashtags
   - hookScore (0–100)
   - engagementEstimate (predicted interactions)
4. Analysis section:
   - bestPostingTime (2 slots)
   - suggestedHashtags (5 tags)
   - niche classification
5. temperature: 0.9 (higher creativity)
   max_tokens: 3000
```

### 7.3 `analyzeTweetPerformance()`

**Inputs:** `tweet` (raw text)

**Algorithm:**

```
1. Detect language via regex
2. Build analysis prompt requesting JSON:
   {
     hookScore: 0–100,
     readabilityScore: 0–100,
     engagementPrediction: 0–100,
     viralProbability: 0–100,
     strengths: string[],
     weaknesses: string[],
     improvedVersion: string,
     bestPostingTimes: string[]
   }
3. temperature: 0.5 (analytical, less creative)
   max_tokens: 1500
```

### 7.4 `optimizeBio()`

**Inputs:** `bio`, `niche`, `language`

**Bio Optimisation Rules injected into prompt:**
1. Lead with the value you provide to followers
2. Include 3–5 searchable keywords for your niche
3. Add a human element (personality, location, emoji)
4. End with a clear call to action (link, DM, subscribe)
5. Stay under 160 characters

### 7.5 `detectLanguage()`

Fast regex-based detection (no AI call):
```ts
const arabicPattern = /[\u0600-\u06FF\u0750-\u077F\u08A0-\u08FF]/;
if (arabicPattern.test(text)) return "ar";
const englishPattern = /[a-zA-Z]/;
if (englishPattern.test(text)) return "en";
return "other";
```

---

## 8. Twitter Algorithm Insights Engine

Located in `src/lib/algorithms.ts`. This module encodes known X/Twitter algorithm behaviour into actionable data.

### 8.1 Best Posting Times — Saudi Arabia

The `SAUDI_BEST_TIMES` array contains **14 scored time slots** covering all 7 days. Scores are based on:

- Typical Saudi daily routine (work hours: Sun–Thu, weekend: Fri–Sat)
- Historical engagement patterns for Arabic content
- Mobile usage peaks (commute times, post-dinner browsing)

**Top scoring slots:**

| Score | Day | Hour | Reason |
|-------|-----|------|--------|
| 95 | Thursday | 22:00 | Weekend eve — highest Arabic engagement of the week |
| 93 | Friday | 21:00 | Peak Friday night browsing |
| 92 | Tuesday | 21:00 | Mid-week high-engagement window |
| 90 | Sunday | 21:00 | Start-of-week evening spike |

### 8.2 Weekly Engagement Heatmap

`getWeeklyHeatmap()` generates a 7×24 grid (168 cells) where each cell has a score from 0–100. Known best-time slots fill their exact score; all other cells receive a realistic baseline score with slight randomisation to avoid identical-looking heatmaps.

The heatmap is rendered as a colour-graded table: dark cells = low engagement, gold-bright cells = peak engagement.

### 8.3 Tweet Score Calculator

`calculateTweetScore()` takes tweet attributes and returns a 0–100 composite score:

```
Base score: 50

+ 15   length 20–140 chars (sweet spot)
+ 10   length 140–280 chars
- 10   length < 20 chars (too short)
+ 20   has media (photo/video)
+ 15   is thread
+ 5/8/6   1/2/3 hashtags
- 5    > 5 hashtags
+ 10   ends with a question
+ 5    contains emoji
+ 10   Arabic content (bonus for Saudi audience targeting)

Clamped: min 0, max 100
```

### 8.4 Algorithm Insights Collection

12 research-backed insights are stored in `ALGORITHM_INSIGHTS` and displayed on the Scheduler page:

- Reply within 30 minutes of posting → 3× more reach
- 2–3 hashtags = optimal (> 5 reduces engagement by 17%)
- Threads increase dwell time → algorithm boost
- Never delete tweets (penalised by algorithm)
- Engaging with large accounts exposes you to their followers
- Tweets with numbers/stats get 2× more retweets

---

## 9. Design System

### Colour Palette

```css
/* Primary accent */
--gold:        #C9A84C   /* warm gold — all CTAs, active states, scores */
--gold-light:  #E8CC7A   /* gradient highlight */
--gold-dark:   #A8873A   /* hover states */
--gold-glow:   rgba(201,168,76,0.3)

/* Backgrounds */
--ink:         #0A0A0F   /* page background */
--ink-light:   #141420   /* section backgrounds */
--ink-mid:     #1E1E2E   /* hover states */
--ink-card:    #181825   /* card backgrounds */

/* Borders */
--ink-border:        rgba(255,255,255,0.06)
--ink-border-gold:   rgba(201,168,76,0.2)

/* Text */
--cream:       #F5F0E8   /* primary text */
--cream-dim:   #C8BB9E   /* secondary headings */
--text-secondary:  #9B9AAA
--text-muted:      #5C5B6E
```

### Typography

The **Amiri** font (Google Fonts) is the sole display and body typeface. It was chosen because:
1. It is a high-quality Arabic serif with excellent readability at all sizes
2. It includes Latin characters so English content looks consistent
3. It has a classical, editorial quality that matches the gold-ink aesthetic

Font weights used: `400` (body), `700` (headings, labels).

### Animation System

All animations are defined as `@keyframes` in `globals.css` and exposed as Tailwind classes:

| Class | Effect | Duration |
|-------|--------|----------|
| `animate-fade-in` | opacity 0→1 | 400ms |
| `animate-slide-up` | translateY(20px)→0 + fade | 400ms |
| `animate-slide-in-right` | translateX(20px)→0 + fade | 300ms |
| `animate-glow` | pulsing gold box-shadow | 2s loop |
| `shimmer` | skeleton loading gradient sweep | 1.5s loop |

Stagger delays are applied via `.stagger > *:nth-child(n)` CSS selectors (60ms increments).

### Glass Card System

```css
.glass-card {
  background: rgba(24,24,37,0.8);
  border: 1px solid rgba(255,255,255,0.06);
  backdrop-filter: blur(12px);
  border-radius: 16px;
  transition: all 0.3s ease;
}
.glass-card:hover {
  border-color: rgba(201,168,76,0.2);
  box-shadow: 0 8px 32px rgba(0,0,0,0.4), 0 0 16px rgba(201,168,76,0.15);
  transform: translateY(-1px);
}
```

---

## 10. Page-by-Page Breakdown

### Landing Page (`/`)

- Full-screen hero with animated background glows
- Feature grid (8 cards with icons)
- Stats bar (20+ features, local AI, Arabic support, 5-min setup)
- CTA section with Twitter OAuth button
- Auto-redirects to `/dashboard` if already authenticated

### Dashboard Home (`/dashboard`)

- Time range selector: 7 / 30 / 90 days
- 6-column stats grid: followers, views, likes, engagement rate, scheduled, posted
- Area chart: follower growth over time
- Bar chart: daily likes + retweets
- Quick actions grid (6 links)
- Best posting times for today (top 3 slots)
- Line chart: engagement rate trend

### Tweet Rewriter (`/dashboard/rewrite`)

- Toggle: paste URL or type text directly
- URL mode: fetch + display original tweet card with metrics, media, thread info
- Manual mode: textarea with char counter
- Options panel (collapsible): mode, dialect, tone, length, toggles
- Rewrite button → spinner → result card
- Result card: rewritten text (or thread parts), hashtags, hook score bar, engagement tips
- Actions: copy, save to drafts, open schedule modal

### Tweet Generator (`/dashboard/generate`)

- Topic input (Arabic or English)
- Options: language, tone, format (single/thread), audience, thread length, dialect
- Keyword tags input
- Niche selector
- Generate → 3 variant cards
- Each card: content, hook score ring, engagement estimate, hashtag chips
- Actions per card: copy, save draft, schedule, expand thread

### Content Calendar (`/dashboard/calendar`)

- Google Calendar–style monthly grid (7 columns × ~5 rows)
- Each day cell shows event chips (colour-coded by status)
- Status colours: blue=scheduled, green=posted, red=failed, grey=cancelled
- Click day → create new scheduled tweet modal
- Click event chip → view/edit modal
- Navigation: prev/next month, today button
- Month/week view toggle
- Legend for status colours

### Analytics (`/dashboard/analytics`)

- Period selector: 7/30/90 days
- Summary cards: total views, total likes, total retweets, avg engagement rate, follower delta
- Area chart: followers over time
- Multi-line chart: views, likes, retweets on same axes
- Bar chart: daily impressions
- Line chart: engagement rate trend
- All charts use the same gold/blue/purple colour palette

### Thread Builder (`/dashboard/threads`)

- Add up to 25 thread parts
- Each part: textarea with 280-char counter + media attachment button
- Drag-and-drop reordering (react-beautiful-dnd)
- Live preview: mobile-frame showing each tweet as it would appear
- Auto-split mode: paste long text → auto-splits into 260-char parts
- Thread hook helper: AI suggests an opening line
- Export: copy all parts, save as draft, schedule

### Hashtag Analyser (`/dashboard/hashtags`)

- Search input for hashtag lookup
- Result card: trending score, competition level (low/medium/high), avg reach, related tags
- Saved hashtags list with category tags
- Trending hashtags (Saudi Arabia): sorted by volume with growth arrows
- Niche-specific suggestions based on user's selected niche

### Best Time Scheduler (`/dashboard/scheduler`)

- Weekly heatmap: 7 rows (days) × 24 columns (hours), colour intensity = engagement score
- Top 5 best time slots with score bars and reasoning text
- Algorithm insights list (12 cards): each with category, impact level, actionable tip
- Auto-schedule generator: choose tweets per day → generates optimal schedule
- One-click: apply schedule to all pending drafts

### Templates Library (`/dashboard/templates`)

- Filter: All / Arabic / English / by category (thread, opinion, tip, story, general)
- System templates (read-only, pre-seeded): 7 starter templates
- User templates: full CRUD
- Each template: title, preview, category badge, usage count, avg engagement
- Use template → pre-fills generate form

### Draft Manager (`/dashboard/drafts`)

- List view: title/snippet, date, language badge, thread indicator
- Search by content, filter by language and date
- Click draft → open in rewrite or generate form
- Bulk actions: delete selected, export selected
- Tag system for organisation

### Audience Insights (`/dashboard/audience`)

- Age distribution: horizontal bar chart
- Gender split: donut chart
- Top countries: flag + percentage list
- Top interests: tag cloud
- Peak hours: area chart
- Peak days: radar chart
- Language split: pie chart
- Note: populated from real Twitter API data when available, demo data otherwise

### Competitor Tracker (`/dashboard/competitor`)

- Add up to 10 competitor handles
- Each competitor card: followers, tweets/day, engagement rate, last checked
- Comparison bar charts: followers, engagement rate
- Auto-refresh every 24 hours

### Bio Optimiser (`/dashboard/bio`)

- Current bio display
- Niche selector
- Language toggle (AR/EN)
- AI optimise button → shows optimised version + improvement list + keyword chips
- Score before/after comparison
- One-click copy optimised bio

### Reports (`/dashboard/reports`)

- Weekly auto-summary: best tweet, follower growth, top hashtag, engagement trend
- Monthly deep-dive: all metrics compared to previous month
- Export: download as PDF via html2canvas
- AI-written executive summary paragraph

### Settings (`/dashboard/settings`)

- Profile section: name, bio, avatar preview
- Twitter connection status badge
- Timezone selector (default: Asia/Riyadh)
- Preferred language: Arabic / English
- LM Studio URL configuration + test connection button
- LM Studio model selector (lists loaded models from `/v1/models`)
- Notification preferences
- Account niche (16 options)
- Danger zone: disconnect Twitter, delete all data

---

## 11. Component Architecture

### Shared Components

**`TweetCard`** — Reusable tweet display:
```tsx
<TweetCard
  tweet={tweet}
  showMetrics={true}
  showActions={true}
  onRewrite={() => ...}
  onSchedule={() => ...}
/>
```

**`ScoreRing`** — SVG circular score indicator:
```tsx
<ScoreRing score={85} size={64} label="Hook" />
// Renders: SVG circle with stroke-dashoffset animation
// Colour: green > 80, gold > 60, red <= 60
```

**`LMStatusBadge`** — Live connection status:
```tsx
<LMStatusBadge />
// Polls /api/ai/analyze (GET) every 30 seconds
// States: connecting (grey), connected (green), disconnected (red)
// Shows model name when connected
```

**`CharCounter`** — Accurate Twitter char count:
```tsx
<CharCounter text={content} max={280} />
// URLs counted as 23 chars regardless of length
// Colour: green normal, yellow warning (>250), red over limit
```

---

## 12. State Management

**Zustand** (`src/store/useAppStore.ts`) manages global UI state:

```ts
interface AppStore {
  // UI
  sidebarCollapsed: boolean
  setSidebarCollapsed: (v: boolean) => void

  // AI
  lmConnected: boolean
  lmModel: string
  setLMStatus: (connected: boolean, model: string) => void

  // User preferences
  preferredLanguage: "ar" | "en"
  preferredDialect: string
  niche: string
  timezone: string
  setPreferences: (prefs: Partial<Preferences>) => void

  // Draft in progress
  currentDraft: string
  setCurrentDraft: (text: string) => void

  // Calendar
  calendarMonth: number
  calendarYear: number
  setCalendarDate: (month: number, year: number) => void
}
```

Server data (analytics, scheduled tweets, drafts) is managed via custom hooks with `fetch` + `useState` — no external query library is required given the app's scope.

---

## 13. Authentication Flow

```
User clicks "Sign in with Twitter"
    │
    ▼
NextAuth redirects to Twitter OAuth 2.0 PKCE
    │
    ▼
Twitter prompts: "X-Craft wants to: read tweets, write tweets, read profile"
    │
    ▼
User authorises → Twitter returns code
    │
    ▼
NextAuth exchanges code for access_token + refresh_token
    │
    ▼
PrismaAdapter saves:
  Account { provider: "twitter", access_token, refresh_token }
  User { name, image, email }
    │
    ▼
signIn() callback fires:
  Fetches Twitter profile: username, bio, followers, following, tweets count
  Updates User record with Twitter-specific fields
    │
    ▼
createUser() event fires (first login only):
  Seeds 7 default templates for the user
    │
    ▼
session() callback:
  Attaches user.id + all Twitter fields to session object
    │
    ▼
User redirected to /dashboard
```

---

## 14. Scheduling System

### Manual Scheduling

Users pick a date/time from the calendar or scheduler page. The `POST /api/twitter/schedule` endpoint validates:
1. `scheduledAt` is in the future
2. Content is not empty
3. Character count is valid (≤ 280 per tweet, ≤ 25 parts for threads)

### Automated Publishing (Cron)

`GET /api/cron` is called by an external cron service (e.g. Vercel Cron, cron-job.org) every minute:

```
1. Query ScheduledTweet WHERE status='scheduled' AND scheduledAt <= NOW()
2. For each due tweet:
   a. If isThread: call postThread(userId, JSON.parse(threadParts))
   b. Else: call postTweet(userId, content)
   c. On success: update status='posted', set tweetId, postedAt=now
   d. On failure: update status='failed', log error
3. Return { processed: N, failed: M }
```

The endpoint is secured by checking `Authorization: Bearer {CRON_SECRET}` header.

### Optimal Schedule Generator

When user clicks "Auto-Schedule" on the scheduler page:
1. Loads all drafts with `status=draft`
2. Calls `generateWeeklySchedule(tweetsPerDay)` from `algorithms.ts`
3. Maps drafts to the top-N scoring time slots for the next 7 days
4. Creates `ScheduledTweet` records in bulk

---

## 15. Installation & Setup

### Prerequisites

- Node.js ≥ 20
- npm ≥ 10
- Git
- A Twitter Developer account with a project + app
- LM Studio installed and running

### Step 1 — Clone and install

```bash
git clone https://github.com/your-username/x-craft.git
cd x-craft
npm install
```

### Step 2 — Environment variables

```bash
cp .env.example .env.local
```

Fill in all values (see §16 below).

### Step 3 — Database setup

```bash
# Generate Prisma client
npx prisma generate

# Create database and run migrations
npx prisma db push

# Optional: open Prisma Studio to inspect data
npx prisma studio
```

### Step 4 — LM Studio setup

1. Download LM Studio from [lmstudio.ai](https://lmstudio.ai)
2. Search and download a model (recommended: `Llama-3-8B-Instruct` or `Mistral-7B-Instruct`)
3. Click **"Start Server"** in the Local Server tab
4. Confirm it shows: `Listening on http://localhost:1234`

### Step 5 — Twitter Developer setup

1. Go to [developer.twitter.com](https://developer.twitter.com)
2. Create a project and an app
3. Enable **OAuth 2.0** with PKCE
4. Set the callback URL to: `http://localhost:3000/api/auth/callback/twitter`
5. Set the website URL to: `http://localhost:3000`
6. Request scopes: `tweet.read tweet.write users.read offline.access follows.read`
7. Copy the **Client ID** and **Client Secret**

### Step 6 — Run development server

```bash
npm run dev
```

Open [http://localhost:3000](http://localhost:3000).

### Step 7 — Set up scheduled tweet cron (optional)

For local development, you can manually trigger the cron:

```bash
curl -H "Authorization: Bearer YOUR_CRON_SECRET" http://localhost:3000/api/cron
```

For production, configure your hosting provider's cron feature to call this endpoint every minute.

---

## 16. Environment Variables

```env
# Authentication
AUTH_SECRET=           # Random 32-char string: openssl rand -base64 32
NEXTAUTH_URL=          # Full URL of your app: http://localhost:3000

# Twitter / X
TWITTER_CLIENT_ID=     # From Twitter Developer Portal
TWITTER_CLIENT_SECRET= # From Twitter Developer Portal
TWITTER_BEARER_TOKEN=  # For reading public tweets without user auth

# LM Studio
LM_STUDIO_BASE_URL=    # Default: http://localhost:1234/v1
LM_STUDIO_MODEL=       # Model identifier shown in LM Studio

# Database
DATABASE_URL=          # Default: file:./dev.db  (SQLite)

# App
NEXT_PUBLIC_APP_URL=   # Same as NEXTAUTH_URL

# Cron security
CRON_SECRET=           # Random string to secure /api/cron endpoint
```

---

## 17. LM Studio Configuration

### Recommended Models

| Model | Size | Arabic Quality | Speed |
|-------|------|---------------|-------|
| `Meta-Llama-3-8B-Instruct` | 8B | ★★★★☆ | Fast |
| `Mistral-7B-Instruct-v0.3` | 7B | ★★★☆☆ | Fast |
| `Llama-3.1-8B-Instruct` | 8B | ★★★★☆ | Fast |
| `Qwen2.5-7B-Instruct` | 7B | ★★★★★ | Fast |
| `gemma-2-9b-it` | 9B | ★★★☆☆ | Medium |
| `Meta-Llama-3-70B-Instruct` | 70B | ★★★★★ | Slow (GPU required) |

> **Tip for Arabic:** Qwen2.5 and Llama 3 models have the best Arabic understanding. For Saudi dialect specifically, models fine-tuned on Arabic data perform noticeably better.

### LM Studio Settings

In LM Studio → Server tab:
- **Port:** 1234 (default)
- **CORS:** Enable "Allow all origins" for local development
- **Context Length:** Set to at least 4096 tokens
- **GPU Layers:** Set to maximum your GPU supports

### AI Call Parameters

| Function | Temperature | Max Tokens | Reason |
|----------|-------------|------------|--------|
| rewriteTweet | 0.8 | 2000 | Creative but structured |
| generateTweet | 0.9 | 3000 | Maximum creativity for 3 variants |
| analyzeTweet | 0.5 | 1500 | Analytical, consistent scoring |
| optimizeBio | 0.7 | 800 | Balanced creativity + precision |

---

## 18. Roadmap

### v1.1
- [ ] Real-time Twitter analytics via API (follower count sync every hour)
- [ ] Image generation for tweet visuals (Stable Diffusion via local API)
- [ ] Bulk scheduling: upload CSV of tweets + times

### v1.2
- [ ] Multi-account support (manage multiple Twitter accounts)
- [ ] Team collaboration: share drafts and templates with teammates
- [ ] Webhook: receive notifications when tweets get high engagement

### v1.3
- [ ] Fine-tuning pipeline: train a custom LoRA on your best-performing tweets
- [ ] Competitor content analysis: AI summarises competitor strategy weekly
- [ ] Auto-reply system: AI drafts replies to mentions for human review

### v2.0
- [ ] Mobile app (React Native) with full feature parity
- [ ] Support for LinkedIn, Instagram captions, and Threads (Meta)

---

*Built with ❤️ for the Arabic-speaking creator community.*
*All AI runs locally. Your data stays yours.*
