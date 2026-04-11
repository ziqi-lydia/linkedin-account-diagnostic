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

## Final Report Format

Deliver the complete diagnostic as a structured report:

```
==============================================================
    LINKEDIN ACCOUNT DIAGNOSTIC REPORT
    Generated: [Date]
    Account: [Name] (@[slug])
==============================================================

📊 EXECUTIVE SUMMARY
Algorithm Health Score:     [X/100]  [emoji indicator]
Content Strategy Score:     [X/50]   [emoji indicator]
Engagement Network:         [status] [emoji indicator]
Profile Alignment:          [X/10]   [emoji indicator]
Overall Assessment:         [one-line summary]

⚠️ [DEATH SPIRAL STATUS if applicable]

---

🔍 MODULE A: ALGORITHM HEALTH
[Detailed findings]

📝 MODULE B: CONTENT STRATEGY
[Content scorecard + analysis]

🤝 MODULE C: ENGAGEMENT NETWORK
[Network health + gaps]

🎯 MODULE D: PROFILE ALIGNMENT
[Alignment check results]

💊 MODULE E: GROWTH PRESCRIPTION
[Priority issues + daily action plan + content fix plan]

👥 YOUR INNER CIRCLE
[Tiered list with names, URLs, and engagement suggestions]

📈 YOUR GROWTH MILESTONES
[Week-by-week targets]

==============================================================
```

## Export Options

After presenting the report, offer:
1. **Google Sheet** - Export raw post data + inner circle list to a spreadsheet for tracking
2. **Google Doc** - Export the full report as a formatted document
3. **Track progress** - Offer to re-run the diagnostic in 2-4 weeks to measure improvement

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
