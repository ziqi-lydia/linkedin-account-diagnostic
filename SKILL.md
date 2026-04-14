---
name: linkedin-account-diagnostic
description: Comprehensive LinkedIn account diagnostic for early-stage creators. Analyzes posting performance, algorithm health, content mix, engagement network, and provides actionable fix plan with personalized inner circle recommendations.
---

# LinkedIn Account Diagnostic & Growth Prescription

Comprehensive diagnostic system for any LinkedIn account, especially early-stage creators (0-5K followers). Performs data-driven analysis of posting performance, algorithm health signals, content strategy, engagement network, and delivers a personalized growth prescription with curated inner circle recommendations.

## When to Use
- "Diagnose my LinkedIn account"
- "Why is my LinkedIn reach declining?"
- "Audit my LinkedIn content strategy"
- "Help me fix my LinkedIn engagement"
- "Build me a LinkedIn growth plan"
- "Find me an engagement inner circle"
- Any request about improving LinkedIn performance, reach, or engagement

## Required Context (ask if not provided)
1. **LinkedIn profile URL** (or use currently logged-in profile)
2. **Brief self-description**: What do you do? What's your role/industry?
3. **Goal**: What do you want LinkedIn to do for you? (Options: build personal brand / generate leads / job search / recruit / thought leadership / community building)
4. **Target audience**: Who do you want to reach? (roles, industries, seniority levels)
5. **Time period to analyze**: Default last 30 days, minimum 2 weeks of posting history

## Diagnostic Framework Overview

The diagnostic has 5 modules. Run ALL of them for a complete diagnosis:

| Module | What It Measures | Output |
|--------|-----------------|--------|
| A. Algorithm Health Score | Whether LinkedIn's algorithm is helping or throttling you | Score 0-100 + death spiral check |
| B. Content Strategy Audit | Content mix, format effectiveness, posting rhythm | Content scorecard + fix plan |
| C. Engagement Network Analysis | Who engages with you, network density, reciprocity | Network health map |
| D. Profile-Content Alignment | Does your profile match what you post about? | Alignment score + gaps |
| E. Growth Prescription | Personalized daily/weekly action plan + inner circle list | Actionable checklist + curated names |

---

## Module A: Algorithm Health Score

### Step 1: Collect Post Performance Data

Navigate to the user's recent activity and collect data for every post in the analysis period.

```javascript
// Navigate to user's activity page
var page = await browser.newtab("https://www.linkedin.com/in/USERNAME/recent-activity/all/")
await page.wait({ waitTime: 3 })
var snap = await page.snapshot()
```

For each post, extract:
- **Date & time posted**
- **Content type**: text-only / image / video / carousel-PDF / poll / article
- **Content category**: value-insight / story-learning / product-promotion / announcement / repost / engagement-bait
- **First 2 lines** (the "hook")
- **Full content** (click "see more" if needed)
- **Impressions** (if visible via analytics)
- **Reactions count** (likes, celebrates, etc.)
- **Comments count**
- **Reposts count**
- **Whether post contains external links**
- **Hashtags used**
- **Whether it's a repost vs original content**

Store in structured format:
```javascript
var postData = []
// For each post found:
postData.push({
  date: "2026-04-01",
  dayOfWeek: "Tuesday",
  timePosted: "9:00 AM PST",  // estimate from time indicators
  contentType: "text",  // text / image / video / carousel / poll
  contentCategory: "product",  // value / story / product / announcement / repost
  hook: "First two lines of the post...",
  fullContent: "Full post text...",
  hasExternalLink: true,
  hashtagCount: 5,
  isOriginal: true,  // false if repost
  impressions: 630,  // null if not accessible
  reactions: 0,
  comments: 0,
  reposts: 0,
  engagementRate: 0,  // (reactions + comments + reposts) / impressions * 100
})
```

### Step 2: Calculate Algorithm Health Metrics

```javascript
var algorithmHealth = {
  // Core metrics
  totalPosts: postData.length,
  avgImpressions: 0,
  avgEngagementRate: 0,
  impressionTrend: "declining",  // rising / stable / declining
  
  // Death spiral indicators
  zeroReactionPosts: 0,          // Posts with 0 reactions
  zeroReactionRate: 0,           // % of posts with 0 reactions
  impressionDeclineRate: 0,      // % decline from first post to last post
  lowestImpression: 0,
  highestImpression: 0,
  
  // Algorithm signal scores (each 0-20, total = 100)
  engagementScore: 0,            // Based on avg engagement rate
  consistencyScore: 0,           // Based on posting regularity
  contentMixScore: 0,            // Based on content category diversity
  formatScore: 0,                // Based on content type variety
  linkPenaltyScore: 0,           // Based on external link usage
}
```

**Scoring Rubric:**

**Engagement Score (0-20):**
| Avg Engagement Rate | Score |
|---------------------|-------|
| > 5% | 20 |
| 3-5% | 16 |
| 2-3% | 12 |
| 1-2% | 8 |
| 0.5-1% | 4 |
| < 0.5% | 0 |

**Consistency Score (0-20):**
| Posting Pattern | Score |
|----------------|-------|
| Daily weekday posts, even spacing | 20 |
| 4-5x/week, mostly even | 16 |
| 3-4x/week, some gaps | 12 |
| 2-3x/week, irregular | 8 |
| < 2x/week or burst-then-disappear | 4 |
| Very irregular, multi-day gaps | 0 |

**Content Mix Score (0-20):**
| Content Mix | Score |
|------------|-------|
| Close to 4:2:1 (value:story:product) | 20 |
| Some variety, slightly off ratio | 14 |
| Mostly one type but not all | 8 |
| 100% one category (especially product) | 0 |

**Format Score (0-20):**
| Format Variety | Score |
|---------------|-------|
| Mix of text, image, video, carousel | 20 |
| 2-3 formats used | 14 |
| Mostly text with occasional image | 8 |
| 100% text-only | 4 |

**Link Penalty Score (0-20):**
| External Link Usage | Score |
|--------------------|-------|
| 0% of posts have links in body | 20 |
| < 20% have links (links in comments) | 16 |
| 20-40% have links | 10 |
| 40-60% have links | 5 |
| > 60% have links in post body | 0 |

**Total Algorithm Health Score** = Sum of all 5 scores (0-100)

### Step 3: Death Spiral Detection

Check for the "Algorithm Death Spiral" pattern:

```
DEATH SPIRAL CONFIRMED if ANY of these are true:
1. Zero-reaction rate > 50% (more than half your posts get 0 reactions)
2. Impression trend shows > 50% decline from first post to most recent
3. Most recent post impressions < 200 (algorithm has essentially throttled you)
4. Average engagement rate < 0.5% across all posts
```

If death spiral is detected, flag it prominently in the report:
```
⚠️ DEATH SPIRAL DETECTED
Your account has entered an algorithmic death spiral. This means:
- LinkedIn is actively reducing your content distribution
- Each new post gets shown to fewer people than the last
- Without intervention, your reach will continue approaching zero

This is FIXABLE, but requires immediate strategy changes (see Module E).
```

---

## Module B: Content Strategy Audit

### Step 1: Content Mix Analysis

Categorize every post and calculate the actual ratio:

| Category | Count | Actual % | Ideal % | Gap |
|----------|-------|----------|---------|-----|
| Value/Insight | X | X% | 57% | -X% |
| Story/Learning | X | X% | 29% | -X% |
| Product/CTA | X | X% | 14% | +X% |
| Repost (others' content) | X | X% | 0% | +X% |

### Step 2: Hook Quality Assessment

For each post, evaluate the first 2 lines (the "hook"):

**Strong hook patterns (score 8-10):**
- Opens with a specific number/data point
- Creates tension or curiosity
- States a contrarian opinion
- Starts with a personal story moment
- Asks a provocative question

**Medium hook patterns (score 4-7):**
- Reasonable opening but generic
- States a fact without tension
- Mildly interesting but not scroll-stopping

**Weak hook patterns (score 0-3):**
- "Excited to share..." / "Thrilled to announce..."
- "AI is transforming..." / "The future of..."
- Generic industry statements
- Starts with a link or tag
- Product pitch in the first line

Calculate average hook score across all posts.

### Step 3: Posting Rhythm Analysis

Map out the posting calendar:
```
Week 1: Mon[ ] Tue[X] Wed[ ] Thu[XX] Fri[ ] Sat[ ] Sun[ ]
Week 2: Mon[ ] Tue[ ] Wed[ ] Thu[ ] Fri[ ] Sat[ ] Sun[ ]
Week 3: Mon[X] Tue[ ] Wed[X] Thu[ ] Fri[ ] Sat[ ] Sun[ ]
```

Flag issues:
- ❌ Multiple posts on the same day (self-cannibalization)
- ❌ Gaps of 3+ days (algorithm forgets you)
- ❌ Weekend-only posting (lowest reach days)
- ❌ No consistent time of day (algorithm can't predict you)
- ✅ Consistent weekday posting at similar times

### Step 4: Anti-Pattern Detection

Check for these algorithm killers:
- [ ] External links in post body (not in first comment)
- [ ] More than 5 hashtags per post
- [ ] Editing posts within 10 minutes of publishing
- [ ] Posts that are purely reshares with no added commentary
- [ ] Posts with no CTA / conversation prompt at the end
- [ ] Posts longer than 1500 characters without formatting/breaks
- [ ] Emoji overload (> 5 emojis per post)

### Step 5: Content Scorecard

Compile into a single scorecard:

```
CONTENT STRATEGY SCORECARD
===========================
Content Mix Balance:     [X/10]  (closeness to 4:2:1 ratio)
Hook Quality Average:    [X/10]  (avg hook score)
Posting Consistency:     [X/10]  (regularity + spacing)
Format Variety:          [X/10]  (types of content used)
Anti-Pattern Violations: [X/10]  (fewer violations = higher score)
---
TOTAL:                   [X/50]
```

---

## Module C: Engagement Network Analysis

### Step 1: Map Current Engagement Sources

Go through the user's recent posts and identify:

**Who reacts to your posts:**
```javascript
var engagers = {}
// For each post, check who liked/commented
// Build frequency map:
// engagers["Person Name"] = { reactions: X, comments: X, totalEngagements: X }
```

**Who you engage with:**
```javascript
// Check user's recent comments activity
await page.goto({ url: "https://www.linkedin.com/in/USERNAME/recent-activity/comments/" })
// Map who the user comments on
```

### Step 2: Network Health Metrics

```javascript
var networkHealth = {
  // Engagement circle size
  uniqueEngagers30d: 0,          // Unique people who engaged with your posts
  repeatEngagers: 0,             // People who engaged 2+ times
  superEngagers: 0,              // People who engaged 5+ times
  
  // Reciprocity
  peopleYouEngageWith: 0,        // People whose posts you comment on
  mutualEngagers: 0,             // People in both lists
  reciprocityRate: 0,            // mutual / (total unique engagers + people you engage with)
  
  // Network composition
  firstDegreeConnections: 0,     // Total 1st degree connections
  activeConnections: 0,          // Connections who posted in last 30 days
  connectionActivityRate: 0,     // active / total
  
  // Inner circle status
  hasInnerCircle: false,         // true if 5+ people engage on > 50% of posts
  innerCircleSize: 0,
  innerCircleMembers: [],
}
```

### Step 3: Connection Count Check

```javascript
// Navigate to connections page
await page.goto({ url: "https://www.linkedin.com/mynetwork/invite-connect/connections/" })
await page.wait({ waitTime: 3 })
// Extract total connection count
```

**Connection count benchmarks for early creators:**
| Connections | Status | Impact |
|-------------|--------|--------|
| < 100 | Critical | Algorithm has almost no one to show your posts to |
| 100-300 | Building | Minimum viable network, still limited distribution |
| 300-500 | Functional | Algorithm has enough seeds for initial distribution |
| 500-1000 | Growing | Good base for organic growth |
| 1000+ | Strong | Sufficient network for viral potential |

### Step 4: Engagement Circle Diagnosis

Present findings:
```
ENGAGEMENT NETWORK HEALTH
============================
Unique engagers (30d):       [X]
Repeat engagers:             [X] (engaged 2+ times)
Inner circle (engaged >50%): [X] people
Connection count:            [X]
Reciprocity rate:            [X]%

DIAGNOSIS:
[One of the following]
- 🔴 CRITICAL: No engagement circle. You're posting into a void.
- 🟡 WEAK: Small/inconsistent engagement. Need to actively build relationships.
- 🟢 HEALTHY: Active engagement circle supporting your content.
```

---

## Module D: Profile-Content Alignment Check

### Step 1: Extract Profile Positioning
```javascript
await page.goto({ url: "https://www.linkedin.com/in/USERNAME/" })
await page.wait({ waitTime: 3 })
// Extract: headline, about section, current role, featured section
var profilePositioning = {
  headline: "...",
  about: "...",
  currentRole: "...",
  featuredContent: "...",
  topSkills: [...],
}
```

### Step 2: Compare Profile vs Content Themes

Check if what the user POSTS about matches what their PROFILE says they do.

Misalignment examples:
- Profile says "Software Engineer" but posts are all about marketing → mismatch
- Profile says "AI Startup Founder" and posts about AI GTM insights → aligned
- Profile has no "About" section → missed opportunity

### Step 3: Alignment Score
```
PROFILE-CONTENT ALIGNMENT
============================
Headline matches content themes:  [Yes/Partial/No]
About section exists:              [Yes/No]
About section matches content:     [Yes/Partial/No]
Featured section utilized:         [Yes/No]
Current role clear:                [Yes/No]
---
ALIGNMENT SCORE: [X/10]
```

---

## Module E: Growth Prescription

### Step 1: Synthesize All Findings

Compile the priority issues from Modules A-D, ranked by impact:

```
PRIORITY ISSUES (ranked by impact on growth)
=============================================
🔴 P0 (Fix Immediately):
  1. [e.g., "100% product content - algorithm is penalizing you"]
  2. [e.g., "Zero engagement circle - no one sees your posts in the first 60 min"]
  
🟡 P1 (Fix This Week):
  3. [e.g., "Inconsistent posting rhythm - algorithm can't predict you"]
  4. [e.g., "Weak hooks - people scroll past your content"]

🟢 P2 (Optimize Over Time):
  5. [e.g., "No video/carousel content - missing 2-5x reach multiplier"]
  6. [e.g., "Profile headline doesn't match content themes"]
```

### Step 2: Daily Action Plan

Generate a personalized daily checklist based on the user's specific issues:

```
YOUR DAILY LINKEDIN ROUTINE (30-45 min)
=========================================

BEFORE posting (15 min):
□ Comment on 8-10 people's posts (from your Inner Circle list below)
  - Write 2-3 sentence substantive comments (NOT "great post!")
  - Reference something specific from their post
  - This warms up the algorithm and puts your name in their audience's feed

POSTING (5 min):
□ Publish 1 post (weekdays only)
  - Best times: [personalized based on their audience timezone]
  - Follow the 4:2:1 content mix ratio
  - Use the hook templates from your Content Fix Plan
  - No external links in post body (put in first comment)
  - End with a question or conversation prompt

AFTER posting (15 min, within first 60 min):
□ Reply to every comment on your post
  - Write 2-3 sentence replies (not just "thanks!")
  - Ask follow-up questions to extend the thread
  - Longer comment threads = more algorithmic distribution

THROUGHOUT the day (5 min):
□ Like 10-15 posts from your network
□ Accept/send 5 connection requests (with personalized notes)
```

### Step 3: Content Fix Plan

Based on their specific content issues:

```
YOUR CONTENT FIX PLAN
========================

Current content mix: [actual ratio]
Target content mix: 4:2:1 (Value : Story : Product)

NEXT 7 POSTS SHOULD BE:
Post 1: [Value/Insight] - Topic suggestion based on their expertise
Post 2: [Value/Insight] - Different angle on their domain
Post 3: [Story/Learning] - Personal experience or lesson
Post 4: [Value/Insight] - Industry observation or framework  
Post 5: [Value/Insight] - How-to or practical tip
Post 6: [Story/Learning] - Behind-the-scenes or building update
Post 7: [Product/CTA] - Product mention in context of solving a real problem

HOOK TEMPLATES for your niche:
1. "[Number] [time period]. [Bigger number] [things done]. [Surprising result]."
2. "Most [your audience] think [common belief]. Here's what actually works:"
3. "I spent [time] doing [activity]. The #1 lesson nobody talks about:"
4. "The biggest mistake I see [your audience] making on LinkedIn:"
5. "[Controversial opinion about your industry]. Here's why:"
```

### Step 4: Inner Circle Builder (CRITICAL)

This is the most important module. Based on the user's self-description, goals, and target audience, build a personalized inner circle recommendation.

**Ask the user:**
1. What industry/niche are you in?
2. What's your target audience?
3. Any geographic/language preferences? (e.g., Chinese professionals, Bay Area, etc.)
4. What follower range do you want to target? (Default: 1K-50K - big enough to have reach, small enough to reciprocate)

**Then search LinkedIn to build 3 tiers:**

```javascript
// Search for potential inner circle members
var searchQueries = [
  // Based on user's industry + "content creator" or "building in public"
  "[user's industry] + [user's niche] + active LinkedIn poster",
  // Based on user's target audience peers
  "[similar role] + [similar company stage] + [location if specified]",
  // Based on complementary roles
  "[adjacent roles that would benefit from mutual engagement]",
]

// For each search:
await page.goto({ url: "https://www.linkedin.com/search/results/people/?keywords=" + encodeURIComponent(query) })
await page.wait({ waitTime: 3 })
```

**Qualification criteria for inner circle candidates:**
- ✅ Posts original content at least 2x/week (not just reposts)
- ✅ Follower count in the sweet spot (1K-50K default, adjustable)
- ✅ Engages with others' content (has comments activity)
- ✅ Relevant to user's industry/niche
- ✅ Similar stage or slightly ahead (relatable, likely to reciprocate)
- ❌ Skip people who only repost without commentary
- ❌ Skip people at big corporations who post corporate content
- ❌ Skip people with 100K+ followers (unlikely to reciprocate with a small account)
- ❌ Skip inactive accounts (no posts in 2+ weeks)

**Visit each candidate's profile and verify:**
```javascript
// For each candidate
await page.goto({ url: "https://www.linkedin.com/in/SLUG/recent-activity/all/" })
await page.wait({ waitTime: 3 })
// Check:
// 1. Posting frequency (at least 2x/week)
// 2. Content is original (not just reshares)
// 3. Gets engagement (comments on their posts)
// 4. Industry relevance
```

**Output the Inner Circle list in 3 tiers:**

```
YOUR RECOMMENDED INNER CIRCLE
================================

Tier 1: Core Support Circle (8-10 people)
Engage with EVERY post they make. Goal: build mutual support relationship.
These are people at your level or slightly ahead, most likely to reciprocate.

| # | Name | Profile URL | Role & Company | Followers | Why They're a Good Fit | Suggested First Comment |
|---|------|------------|----------------|-----------|----------------------|------------------------|
| 1 | ... | linkedin.com/in/... | ... | ... | ... | ... |
| 2 | ... | ... | ... | ... | ... | ... |
...

Tier 2: Aspirational Circle (10-15 people)
Engage with their posts 2-3x/week. These are slightly bigger accounts whose audience overlaps with your target.

| # | Name | Profile URL | Role & Company | Followers | Why They're a Good Fit |
|---|------|------------|----------------|-----------|----------------------|
| 1 | ... | ... | ... | ... | ... |
...

Tier 3: Broader Network (20-30 people)
Engage occasionally (1-2x/week). These are industry voices whose content you genuinely find interesting.

| # | Name | Profile URL | Role & Company | Followers | Why They're a Good Fit |
|---|------|------------|----------------|-----------|----------------------|
| 1 | ... | ... | ... | ... | ... |
...
```

**For each Tier 1 person, also provide:**
- A suggested opening DM: "Hey [Name], I'm [brief intro]. I've been enjoying your posts about [specific topic]. Would love to connect and support each other's content."
- A suggested first comment on their next post (specific to their content style)

### Step 5: Growth Milestones

Provide personalized timeline based on their current Algorithm Health Score:

```
YOUR GROWTH MILESTONES
========================

Starting point: Algorithm Health Score [X/100]
Current connections: [X]
Current avg engagement: [X]%

Week 1-2: REPAIR PHASE
Goal: Break the death spiral / establish baseline
□ Post 5x value content (zero product mentions)
□ Comment on 50+ posts (8-10/day)
□ Send 30 connection requests (to inner circle candidates)
□ Target: 3-5 engagements per post
□ Metric to track: Are reactions going UP from post to post?

Week 3-4: BUILD PHASE
Goal: Establish posting rhythm + engagement circle
□ Consistent weekday posting (same time each day)
□ 10-15 mutual engagement relationships forming
□ Target: 10-20 engagements per post
□ Metric to track: Do you have repeat engagers?

Week 5-8: SCALE PHASE
Goal: Algorithm starts distributing beyond 1st degree
□ Content starts reaching 2nd degree connections
□ Inbound connection requests increasing
□ Target: 30-50 engagements per post
□ Metric to track: Impressions trend (should be rising)

Week 8-12: ESTABLISH PHASE
Goal: Become a recognized voice in your niche
□ Stable inner circle (20+ people engage on most posts)
□ Occasional "breakout" posts (1000+ impressions)
□ Can start mixing in more product/promotional content
□ Target: consistent 2-5% engagement rate
```

---

## Final Report Format — Professional PDF Report

After completing all 5 diagnostic modules, generate a polished, visually professional PDF report using ReportLab. The report should look like a premium consulting deliverable — NOT a raw text dump.

### PDF Report Architecture (7 pages)

| Page | Content | Design Notes |
|------|---------|--------------|
| 1 | Cover + Executive Summary | Teal accent band header, 4 score cards (Algorithm/Content/Alignment/Engagers), 4 key metrics row, overall assessment text |
| 2 | Module A: Algorithm Health | Score card + detailed metrics table (Your Value vs Benchmark vs Status) |
| 3 | Module B: Content Strategy | Score card + horizontal bar charts for content mix (actual vs ideal, teal=healthy, coral=over-indexed) + format distribution table + hook quality analysis |
| 4 | Module C: Engagement Network | Network status badge + metrics table + top engagers table (teal header) + critical gap analysis |
| 5 | Module D + E: Profile Alignment & Growth Prescription | Alignment score + profile issues + P0/P1/P2 priority issues with color coding (red/amber/green) |
| 6 | Inner Circle Recommendations | 3-tier table (Tier 1 teal header, Tier 2 indigo header, Tier 3 gray header) with Name, Followers, Topics, Why |
| 7 | 4-Week Growth Milestones + Footer | Week 1-4 milestone cards with colored left borders (coral→amber→teal→green) + Sai branding footer |

### PDF Generation Code

Use this Python template with ReportLab. Replace the mock `report_data` dictionary with actual diagnostic data collected from Modules A-E.

```python
import os, json, math
from datetime import datetime
from reportlab.lib import colors
from reportlab.lib.pagesizes import A4
from reportlab.lib.styles import getSampleStyleSheet, ParagraphStyle
from reportlab.lib.units import mm, inch
from reportlab.lib.enums import TA_LEFT, TA_CENTER, TA_RIGHT
from reportlab.platypus import (
    SimpleDocTemplate, Paragraph, Spacer, Table, TableStyle,
    PageBreak, HRFlowable
)
from reportlab.graphics.shapes import Drawing, Rect, String, Line

# ============================================================
# COLOR PALETTE
# ============================================================
NAVY = colors.HexColor("#0F172A")
DARK_BLUE = colors.HexColor("#1E293B")
TEAL = colors.HexColor("#0D9488")
TEAL_LIGHT = colors.HexColor("#CCFBF1")
TEAL_BG = colors.HexColor("#F0FDFA")
CORAL = colors.HexColor("#E8705A")
CORAL_LIGHT = colors.HexColor("#FEF2F0")
AMBER = colors.HexColor("#F59E0B")
AMBER_LIGHT = colors.HexColor("#FFFBEB")
GREEN = colors.HexColor("#10B981")
GREEN_LIGHT = colors.HexColor("#ECFDF5")
RED = colors.HexColor("#EF4444")
RED_LIGHT = colors.HexColor("#FEF2F2")
GRAY_50 = colors.HexColor("#F8FAFC")
GRAY_100 = colors.HexColor("#F1F5F9")
GRAY_200 = colors.HexColor("#E2E8F0")
GRAY_500 = colors.HexColor("#64748B")
GRAY_700 = colors.HexColor("#334155")
WHITE = colors.white

# ============================================================
# DATA — Replace with actual diagnostic results
# ============================================================
report_data = {
    "generated_date": datetime.now().strftime("%B %d, %Y"),
    "account_name": "ACCOUNT_NAME",
    "account_slug": "ACCOUNT_SLUG",
    "account_headline": "HEADLINE",
    "account_followers": 0,
    "account_connections": 0,
    "analysis_period": "PERIOD",
    "total_posts_analyzed": 0,
    # Module A
    "algorithm_score": 0,       # 0-100
    "death_spiral": False,
    "avg_impressions": 0,
    "avg_engagement_rate": 0.0,
    "impression_trend": "stable",
    "best_post_impressions": 0,
    "worst_post_impressions": 0,
    "avg_reactions": 0,
    "avg_comments": 0,
    "external_link_penalty": False,
    # Module B
    "content_score": 0,         # 0-50
    "content_mix": {
        "value_insight": {"count": 0, "pct": 0, "ideal": 57},
        "story_learning": {"count": 0, "pct": 0, "ideal": 29},
        "product_promo": {"count": 0, "pct": 0, "ideal": 14},
        "repost": {"count": 0, "pct": 0, "ideal": 0},
    },
    "format_mix": {"text_only": 0, "image": 0, "video": 0, "carousel": 0, "poll": 0},
    "avg_hook_score": 0.0,
    "posting_consistency": "irregular",
    "best_posting_time": "",
    # Module C
    "unique_engagers": 0,
    "repeat_engagers": 0,
    "engagement_reciprocity": 0.0,
    "top_engagers": [],  # [{"name": "", "engagements": 0, "reciprocated": False}]
    "network_health": "weak",   # weak / moderate / healthy
    # Module D
    "alignment_score": 0,       # 0-10
    "profile_issues": [],       # ["issue1", "issue2"]
    # Module E
    "priority_issues": [],      # [{"level": "P0", "issue": "...", "fix": "..."}]
    "inner_circle": [],         # [{"tier": 1, "name": "", "url": "", "followers": "", "topic": "", "why": ""}]
    "milestones": {"week1": "", "week2": "", "week3": "", "week4": ""},
}

d = report_data

# ============================================================
# HELPERS
# ============================================================
def score_color(score, max_s):
    pct = score / max_s
    if pct >= 0.7: return GREEN
    elif pct >= 0.4: return AMBER
    else: return RED

def score_bg(score, max_s):
    pct = score / max_s
    if pct >= 0.7: return GREEN_LIGHT
    elif pct >= 0.4: return AMBER_LIGHT
    else: return RED_LIGHT

def score_label(score, max_s):
    pct = score / max_s
    if pct >= 0.7: return "Healthy"
    elif pct >= 0.4: return "Needs Work"
    else: return "Critical"

def make_score_card(score, max_s, label, width=120, height=90):
    drawing = Drawing(width, height)
    col = score_color(score, max_s)
    bg = score_bg(score, max_s)
    drawing.add(Rect(0, 0, width, height, rx=8, ry=8, fillColor=bg, strokeColor=None))
    drawing.add(String(width/2, height-36, f"{score}/{max_s}",
                 fontSize=24, fontName='Helvetica-Bold', fillColor=col, textAnchor='middle'))
    drawing.add(String(width/2, 12, label,
                 fontSize=9, fontName='Helvetica', fillColor=GRAY_500, textAnchor='middle'))
    return drawing

def make_content_bar(actual_pct, ideal_pct, label, width=340, height=28):
    drawing = Drawing(width, height)
    bar_x, bar_w, bar_h = 90, width - 100, 10
    bar_y = (height - bar_h) / 2
    drawing.add(String(0, bar_y+1, label, fontSize=9, fontName='Helvetica', fillColor=GRAY_700))
    drawing.add(Rect(bar_x, bar_y, bar_w, bar_h, fillColor=GRAY_100, strokeColor=None, rx=4, ry=4))
    actual_w = max(2, bar_w * actual_pct / 100)
    bar_col = CORAL if actual_pct > ideal_pct * 1.5 else TEAL
    drawing.add(Rect(bar_x, bar_y, actual_w, bar_h, fillColor=bar_col, strokeColor=None, rx=4, ry=4))
    ideal_x = bar_x + bar_w * ideal_pct / 100
    drawing.add(Line(ideal_x, bar_y-3, ideal_x, bar_y+bar_h+3, strokeColor=GRAY_500, strokeWidth=1.5, strokeDashArray=[2,2]))
    drawing.add(String(bar_x + actual_w + 4, bar_y+1, f"{actual_pct}%", fontSize=8, fontName='Helvetica-Bold', fillColor=bar_col))
    return drawing

def styled_table(data, col_widths, header_color=NAVY):
    """Create a consistently styled table."""
    t = Table(data, colWidths=col_widths)
    t.setStyle(TableStyle([
        ('BACKGROUND', (0,0), (-1,0), header_color),
        ('TEXTCOLOR', (0,0), (-1,0), WHITE),
        ('FONTNAME', (0,0), (-1,0), 'Helvetica-Bold'),
        ('FONTSIZE', (0,0), (-1,-1), 9),
        ('ALIGN', (1,0), (-1,-1), 'CENTER'),
        ('VALIGN', (0,0), (-1,-1), 'MIDDLE'),
        ('GRID', (0,0), (-1,-1), 0.5, GRAY_200),
        ('ROWBACKGROUNDS', (0,1), (-1,-1), [WHITE, GRAY_50]),
        ('TOPPADDING', (0,0), (-1,-1), 6),
        ('BOTTOMPADDING', (0,0), (-1,-1), 6),
        ('LEFTPADDING', (0,0), (-1,-1), 8),
        ('RIGHTPADDING', (0,0), (-1,-1), 8),
    ]))
    return t

# ============================================================
# BUILD PDF
# ============================================================
OUTPUT_PATH = os.path.join("artifacts", "linkedin-diagnostic-report.pdf")

doc = SimpleDocTemplate(OUTPUT_PATH, pagesize=A4,
    leftMargin=20*mm, rightMargin=20*mm, topMargin=18*mm, bottomMargin=18*mm)

styles = getSampleStyleSheet()
styles.add(ParagraphStyle('Title2', fontSize=28, leading=34, textColor=NAVY, fontName='Helvetica-Bold', spaceAfter=4*mm))
styles.add(ParagraphStyle('Subtitle', fontSize=12, leading=16, textColor=GRAY_500, fontName='Helvetica', spaceAfter=8*mm))
styles.add(ParagraphStyle('Section', fontSize=18, leading=22, textColor=NAVY, fontName='Helvetica-Bold', spaceBefore=6*mm, spaceAfter=4*mm))
styles.add(ParagraphStyle('Subsection', fontSize=13, leading=17, textColor=DARK_BLUE, fontName='Helvetica-Bold', spaceBefore=4*mm, spaceAfter=2*mm))
styles.add(ParagraphStyle('Body', fontSize=10, leading=14, textColor=GRAY_700, fontName='Helvetica', spaceAfter=2*mm))
styles.add(ParagraphStyle('Small', fontSize=8.5, leading=12, textColor=GRAY_500, fontName='Helvetica'))
styles.add(ParagraphStyle('Score', fontSize=36, leading=40, textColor=TEAL, fontName='Helvetica-Bold', alignment=TA_CENTER))
styles.add(ParagraphStyle('ScoreLbl', fontSize=10, leading=13, textColor=GRAY_500, fontName='Helvetica', alignment=TA_CENTER))
styles.add(ParagraphStyle('P0', fontSize=10, leading=14, textColor=RED, fontName='Helvetica-Bold', spaceAfter=1*mm))
styles.add(ParagraphStyle('P1', fontSize=10, leading=14, textColor=AMBER, fontName='Helvetica-Bold', spaceAfter=1*mm))
styles.add(ParagraphStyle('P2', fontSize=10, leading=14, textColor=GREEN, fontName='Helvetica-Bold', spaceAfter=1*mm))
styles.add(ParagraphStyle('Fix', fontSize=9.5, leading=13, textColor=GRAY_700, fontName='Helvetica', leftIndent=12, spaceAfter=3*mm))

W, H = A4
els = []

# --- PAGE 1: COVER + EXECUTIVE SUMMARY ---
band = Drawing(W - 40*mm, 6)
band.add(Rect(0, 0, W - 40*mm, 6, fillColor=TEAL, strokeColor=None, rx=3, ry=3))
els.append(band)
els.append(Spacer(1, 6*mm))
els.append(Paragraph("LinkedIn Account<br/>Diagnostic Report", styles['Title2']))
els.append(Paragraph(
    f'{d["account_name"]} &middot; @{d["account_slug"]}<br/>'
    f'{d["account_headline"]}<br/>'
    f'Analysis Period: {d["analysis_period"]} &middot; Generated: {d["generated_date"]}',
    styles['Subtitle']))
els.append(HRFlowable(width="100%", thickness=1, color=GRAY_200, spaceAfter=5*mm))
els.append(Paragraph("Executive Summary", styles['Section']))

# Score cards row
cards = [[make_score_card(d["algorithm_score"], 100, "Algorithm Health"),
          make_score_card(d["content_score"], 50, "Content Strategy"),
          make_score_card(d["alignment_score"], 10, "Profile Alignment"),
          make_score_card(d["unique_engagers"], 100, "Unique Engagers")]]
ct = Table(cards, colWidths=[130]*4)
ct.setStyle(TableStyle([('ALIGN',(0,0),(-1,-1),'CENTER'),('VALIGN',(0,0),(-1,-1),'MIDDLE')]))
els.append(ct)
els.append(Spacer(1, 5*mm))

# Key metrics
m1 = [[Paragraph(f'<font size="18" color="{TEAL.hexval()}">{d["account_followers"]}</font>', styles['Score']),
       Paragraph(f'<font size="18" color="{TEAL.hexval()}">{d["avg_impressions"]}</font>', styles['Score']),
       Paragraph(f'<font size="18" color="{TEAL.hexval()}">{d["avg_engagement_rate"]}%</font>', styles['Score']),
       Paragraph(f'<font size="18" color="{TEAL.hexval()}">{d["total_posts_analyzed"]}</font>', styles['Score'])],
      [Paragraph("Followers", styles['ScoreLbl']),
       Paragraph("Avg Impressions", styles['ScoreLbl']),
       Paragraph("Engagement Rate", styles['ScoreLbl']),
       Paragraph("Posts Analyzed", styles['ScoreLbl'])]]
mt = Table(m1, colWidths=[130]*4)
mt.setStyle(TableStyle([('ALIGN',(0,0),(-1,-1),'CENTER'),('VALIGN',(0,0),(-1,-1),'MIDDLE'),
    ('BACKGROUND',(0,0),(-1,-1),GRAY_50),('BOX',(0,0),(-1,-1),0.5,GRAY_200),
    ('TOPPADDING',(0,0),(-1,0),10),('BOTTOMPADDING',(0,-1),(-1,-1),10)]))
els.append(mt)
els.append(Spacer(1, 5*mm))

status_text = score_label(d["algorithm_score"], 100)
ac = score_color(d["algorithm_score"], 100)
els.append(Paragraph(
    f'<font color="{ac.hexval()}">Overall: {status_text}</font> — '
    f'Your account shows signs of algorithmic throttling. See the detailed modules below for root causes and the fix plan.',
    styles['Body']))

# --- PAGE 2: ALGORITHM HEALTH ---
els.append(PageBreak())
els.append(Paragraph("Module A: Algorithm Health Score", styles['Section']))
els.append(make_score_card(d["algorithm_score"], 100, "Algorithm Health", 150, 100))
els.append(Spacer(1, 3*mm))
els.append(Paragraph("Key Findings", styles['Subsection']))
els.append(styled_table([
    ["Metric", "Your Value", "Benchmark", "Status"],
    ["Avg Impressions/Post", str(d["avg_impressions"]), "1,500+",
     "\u26a0\ufe0f Below" if d["avg_impressions"] < 1500 else "\u2705 Good"],
    ["Avg Engagement Rate", f'{d["avg_engagement_rate"]}%', "3.5%+",
     "\u26a0\ufe0f Below" if d["avg_engagement_rate"] < 3.5 else "\u2705 Good"],
    ["Avg Reactions/Post", str(d["avg_reactions"]), "25+",
     "\u26a0\ufe0f Below" if d["avg_reactions"] < 25 else "\u2705 Good"],
    ["Avg Comments/Post", str(d["avg_comments"]), "8+",
     "\u26a0\ufe0f Below" if d["avg_comments"] < 8 else "\u2705 Good"],
    ["Impression Trend", d["impression_trend"].title(), "Rising",
     "\U0001f534 Critical" if d["impression_trend"] == "declining" else "\u2705 Good"],
    ["Ext. Link Penalty", "Yes" if d["external_link_penalty"] else "No", "No",
     "\U0001f534 Critical" if d["external_link_penalty"] else "\u2705 Good"],
    ["Best Post", f'{d["best_post_impressions"]} imp.', "—", "—"],
    ["Worst Post", f'{d["worst_post_impressions"]} imp.', "—", "—"],
], col_widths=[120, 90, 80, 80]))

if d["death_spiral"]:
    els.append(Spacer(1, 3*mm))
    els.append(Paragraph(
        '<font color="#EF4444"><b>WARNING: DEATH SPIRAL DETECTED</b></font> — '
        'Impressions are declining post-over-post. Immediate intervention required.',
        styles['Body']))

# --- PAGE 3: CONTENT STRATEGY ---
els.append(PageBreak())
els.append(Paragraph("Module B: Content Strategy Audit", styles['Section']))
els.append(make_score_card(d["content_score"], 50, "Content Score", 150, 100))
els.append(Spacer(1, 3*mm))
els.append(Paragraph("Content Mix Analysis", styles['Subsection']))
els.append(Paragraph("Your content mix vs. the ideal 4:2:1 ratio (57% Value : 29% Story : 14% Product):", styles['Body']))
for ck, cl in [("value_insight","Value / Insight"),("story_learning","Story / Learning"),("product_promo","Product / CTA"),("repost","Repost")]:
    v = d["content_mix"][ck]
    els.append(make_content_bar(v["pct"], v["ideal"], cl))
    els.append(Spacer(1, 1*mm))
els.append(Spacer(1, 3*mm))
pp = d["content_mix"]["product_promo"]["pct"]
vp = d["content_mix"]["value_insight"]["pct"]
els.append(Paragraph(
    f'<font color="{CORAL.hexval()}"><b>Problem:</b></font> {pp}% of content is product/CTA '
    f'(ideal: 14%). Only {vp}% is value content (ideal: 57%). '
    f'LinkedIn\'s algorithm treats heavily promotional accounts as advertisers and reduces organic reach.',
    styles['Body']))
els.append(Paragraph("Content Format Distribution", styles['Subsection']))
fm = d["format_mix"]
tp = d["total_posts_analyzed"] or 1
els.append(styled_table([
    ["Format", "Count", "% of Total", "Avg Reach Multiplier"],
    ["Text Only", str(fm["text_only"]), f'{round(fm["text_only"]/tp*100)}%', "1.0x (baseline)"],
    ["Image", str(fm["image"]), f'{round(fm["image"]/tp*100)}%', "1.2-1.5x"],
    ["Carousel/PDF", str(fm["carousel"]), f'{round(fm["carousel"]/tp*100)}%', "2.0-3.5x"],
    ["Video", str(fm["video"]), f'{round(fm["video"]/tp*100)}%', "2.0-5.0x"],
    ["Poll", str(fm["poll"]), f'{round(fm["poll"]/tp*100)}%', "1.5-2.5x"],
], col_widths=[100, 60, 80, 130]))
els.append(Spacer(1, 3*mm))
hs = d["avg_hook_score"]
els.append(Paragraph("Hook Quality", styles['Subsection']))
els.append(Paragraph(
    f'Average hook score: <font color="{score_color(int(hs*10),100).hexval()}"><b>{hs}/10</b></font>. '
    f'Strong hooks (data openers, contrarian takes) score 8+ and drive 3x more "see more" clicks.',
    styles['Body']))

# --- PAGE 4: ENGAGEMENT NETWORK ---
els.append(PageBreak())
els.append(Paragraph("Module C: Engagement Network", styles['Section']))
nh = d["network_health"].upper()
nc = RED if nh == "WEAK" else (AMBER if nh == "MODERATE" else GREEN)
els.append(Paragraph(f'Network Status: <font color="{nc.hexval()}"><b>{nh}</b></font>', styles['Subsection']))
els.append(styled_table([
    ["Metric", "Your Value", "Target", "Status"],
    ["Unique Engagers (30d)", str(d["unique_engagers"]), "50+",
     "\u26a0\ufe0f Low" if d["unique_engagers"] < 50 else "\u2705 Good"],
    ["Repeat Engagers (2+ times)", str(d["repeat_engagers"]), "20+",
     "\U0001f534 Critical" if d["repeat_engagers"] < 20 else "\u2705 Good"],
    ["Engagement Reciprocity", f'{int(d["engagement_reciprocity"]*100)}%', "40%+",
     "\U0001f534 Critical" if d["engagement_reciprocity"] < 0.4 else "\u2705 Good"],
], col_widths=[140, 90, 80, 80]))
els.append(Spacer(1, 3*mm))
els.append(Paragraph("Top Engagers", styles['Subsection']))
eng_rows = [["Name", "Engagements", "Reciprocated"]]
for e in d["top_engagers"]:
    eng_rows.append([e["name"], str(e["engagements"]), "\u2705 Yes" if e["reciprocated"] else "\u274c No"])
els.append(styled_table(eng_rows, col_widths=[160, 100, 100], header_color=TEAL))
els.append(Spacer(1, 3*mm))
els.append(Paragraph(
    f'<font color="{CORAL.hexval()}"><b>Critical gap:</b></font> Only {d["repeat_engagers"]} repeat engagers. '
    f'LinkedIn shows posts to a small test audience first — without a reliable inner circle of 20+ regular engagers, '
    f'most posts die in the first 60 minutes.',
    styles['Body']))

# --- PAGE 5: PROFILE ALIGNMENT + PRESCRIPTION ---
els.append(PageBreak())
els.append(Paragraph("Module D: Profile-Content Alignment", styles['Section']))
els.append(make_score_card(d["alignment_score"], 10, "Alignment Score", 150, 100))
els.append(Spacer(1, 3*mm))
els.append(Paragraph("Issues Found", styles['Subsection']))
for issue in d["profile_issues"]:
    els.append(Paragraph(f'\u2022 {issue}', styles['Body']))
els.append(Spacer(1, 6*mm))
els.append(Paragraph("Module E: Growth Prescription", styles['Section']))
els.append(Paragraph("Priority Issues (Ranked by Impact)", styles['Subsection']))
for pi in d["priority_issues"]:
    lv = pi["level"]
    if lv == "P0": sn, pf = 'P0', "\U0001f534 P0 \u2014 Fix Immediately"
    elif lv == "P1": sn, pf = 'P1', "\U0001f7e1 P1 \u2014 Fix This Week"
    else: sn, pf = 'P2', "\U0001f7e2 P2 \u2014 Optimize Over Time"
    els.append(Paragraph(f'{pf}: {pi["issue"]}', styles[sn]))
    els.append(Paragraph(f'\u2192 {pi["fix"]}', styles['Fix']))

# --- PAGE 6: INNER CIRCLE ---
els.append(PageBreak())
els.append(Paragraph("Your Recommended Inner Circle", styles['Section']))
els.append(Paragraph(
    "Engage with these people daily (Tier 1), 3x/week (Tier 2), or 2x/week (Tier 3). "
    "Within 2-3 weeks they will recognize your name and begin reciprocating.",
    styles['Body']))
tier_cfg = {1: ("\U0001f947 Tier 1 \u2014 Core Circle (engage daily)", TEAL),
            2: ("\U0001f948 Tier 2 \u2014 Extended Circle (engage 3x/week)", colors.HexColor("#6366F1")),
            3: ("\U0001f949 Tier 3 \u2014 Aspirational (engage 2x/week)", GRAY_500)}
for tn in [1, 2, 3]:
    label, hc = tier_cfg[tn]
    els.append(Paragraph(label, styles['Subsection']))
    tp = [p for p in d["inner_circle"] if p["tier"] == tn]
    if tp:
        rows = [["Name", "Followers", "Topics", "Why"]]
        for p in tp:
            rows.append([p["name"], p["followers"], p["topic"], p["why"]])
        els.append(styled_table(rows, col_widths=[90, 60, 100, 150], header_color=hc))
    else:
        els.append(Paragraph("(to be populated during diagnostic)", styles['Small']))
    els.append(Spacer(1, 3*mm))

# --- PAGE 7: MILESTONES + FOOTER ---
els.append(PageBreak())
els.append(Paragraph("Your 4-Week Growth Milestones", styles['Section']))
els.append(Paragraph(
    "Follow this plan consistently for measurable improvement in reach, engagement, and follower growth.",
    styles['Body']))
week_cfg = [("week1","Week 1: Foundation",CORAL),("week2","Week 2: Recognition",AMBER),
            ("week3","Week 3: Momentum",TEAL),("week4","Week 4: Breakthrough",GREEN)]
for wk, wl, wc in week_cfg:
    mb = Drawing(W - 40*mm, 50)
    mb.add(Rect(0, 0, W - 40*mm, 50, rx=6, ry=6, fillColor=GRAY_50, strokeColor=wc, strokeWidth=1.5))
    mb.add(Rect(0, 0, 5, 50, fillColor=wc, strokeColor=None))
    mb.add(String(14, 32, wl, fontSize=11, fontName='Helvetica-Bold', fillColor=wc))
    txt = d["milestones"].get(wk, "")
    if len(txt) > 90: txt = txt[:87] + "..."
    mb.add(String(14, 12, txt, fontSize=8.5, fontName='Helvetica', fillColor=GRAY_700))
    els.append(mb)
    els.append(Spacer(1, 3*mm))

# Footer
els.append(Spacer(1, 8*mm))
els.append(HRFlowable(width="100%", thickness=1, color=GRAY_200, spaceAfter=3*mm))
els.append(Paragraph(
    f'Generated by <font color="{TEAL.hexval()}"><b>Sai</b></font> \u2014 LinkedIn Account Diagnostic Skill | '
    f'{d["generated_date"]} | simular.ai',
    ParagraphStyle('Footer', fontSize=8, textColor=GRAY_500, fontName='Helvetica', alignment=TA_CENTER)))

doc.build(els)
print(f"PDF saved to: {OUTPUT_PATH}")
```

### How to Use This Template

1. **Collect data** in Modules A-E and store results in the `report_data` dictionary structure shown above.
2. **Fill in all fields** — every module produces specific metrics that map directly to the dictionary keys.
3. **Run the script** via `exec()` to generate the PDF.
4. The PDF is saved to the `artifacts/` folder and automatically synced to the user for download.

### Design Principles

- **Color coding**: Teal = healthy/positive, Coral = warning/over-indexed, Red = critical, Amber = needs work, Green = good
- **Score cards**: Rounded rectangle backgrounds with large score numbers, color-coded by health status
- **Tables**: Navy header rows, alternating white/gray zebra stripes, 0.5pt grid lines
- **Content mix bars**: Horizontal bars with actual value (teal or coral) vs. ideal marker (dashed line)
- **Priority issues**: P0 (red), P1 (amber), P2 (green) with arrow-prefixed fix text
- **Inner circle tiers**: Tier 1 (teal header), Tier 2 (indigo header), Tier 3 (gray header)
- **Milestone cards**: Left-colored border bars progressing coral → amber → teal → green

## Export Options

After generating the PDF report, offer these additional exports:

1. **PDF Report** (primary) — The professional diagnostic report generated above. Saved to `artifacts/linkedin-diagnostic-report.pdf`.
2. **Google Sheet** — Export raw post data + inner circle list to a spreadsheet for ongoing tracking. Use `google.sheets.createSpreadsheet()` with tabs: "Post Data", "Inner Circle", "Weekly Metrics".
3. **Google Doc** — Export the full report as a formatted Google Doc for sharing and collaboration. Use `google.docs.createDocument()` + `batchUpdate()` to insert formatted text.
4. **Track progress** — Offer to re-run the diagnostic in 2-4 weeks to measure improvement. Save baseline metrics for comparison.

## Safety Rules
- **Read-only**: This skill only reads data, never posts, comments, likes, or sends requests
- **Privacy**: Don't store or share other users' profile data outside the diagnostic context
- **Random delays**: Wait 3-8 seconds between page loads, 10-20 seconds between profile visits
- **CAPTCHA check**: If any CAPTCHA or unusual prompt appears, STOP and notify user
- **Session limits**: Max 40 profile visits per diagnostic session
- **Honest assessment**: Don't sugarcoat the diagnosis. If the account is in trouble, say so clearly with specific data.

## LinkedIn Algorithm Reference (for context in analysis)

### How the Algorithm Distributes Posts
1. Post published → shown to 5-10% of 1st-degree connections (~100-300 people)
2. **60-90 minute window**: Algorithm measures engagement rate from this initial audience
3. If engagement rate > 2-5% → expand to 2nd-degree connections
4. If engagement stays high → viral distribution mode
5. If engagement rate < 1% → stop distribution, post "dies"

### Algorithm Weight Ranking
- Comments (especially long, substantive ones) > Shares/Reposts > Reactions/Likes > Views
- Author replies to comments = 2x engagement signal
- First 60 minutes of engagement = highest weight
- Dwell time (how long people spend reading) matters

### Algorithm Penalties
- External links in post body: -40-50% reach
- Editing post within 10 minutes of publishing: algorithm reset
- Multiple posts same day: self-cannibalization
- 100% promotional content: classified as spam
- Hashtags > 5: diminishing returns / looks spammy
- Long posting gaps: algorithm "forgets" your account

### Algorithm Rewards
- Consistent daily posting at similar times
- High comment-to-reaction ratio (indicates quality discussion)
- Carousel/PDF posts (highest organic reach format)
- Video content (5x reach vs text-only)
- Posts that generate comment threads (back-and-forth conversation)
- Active engagement with others' content (reciprocity signal)

### The 4:2:1 Content Rule
| Type | Ratio | Description |
|------|-------|-------------|
| Value/Insight | 4 parts (57%) | Frameworks, lessons, data, how-tos. NOT about your product. |
| Story/Learning | 2 parts (29%) | Personal experiences, failures, behind-the-scenes, building journey |
| Product/CTA | 1 part (14%) | Product in context of solving a real problem. Only AFTER trust is built. |
