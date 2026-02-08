# The "Department of One" Engineering Curriculum

**Developing Judgment in the Age of AI-Generated Code**

---

**Core Thesis:** When LLMs commoditize code implementation, the valuable skill becomes *judgment* — knowing what to build, how it will fail, and whether it should exist at all.

This curriculum trains you to think like an SRE, CISO, Product Manager, and Engineering Lead simultaneously. You'll learn to supervise AI-generated code the way a senior engineer supervises junior developers.

---

## Timeline Overview

| Pace | Weekly Hours | Estimated Duration |
|------|-------------|--------------------|
| Intense | 40 hrs/week | 8-11 months |
| Sustainable | 10-15 hrs/week | 24-30 months |
| Casual | 5 hrs/week | 3-4 years |

> **Critical:** Don't treat this as a checkbox exercise. The deliverables force you to develop judgment through direct experience with failure.

---

## Phase 0: Prerequisites & Setup (1-2 Weeks)

**Goal:** Remove friction so you can focus on learning, not logistics.

### Find Your People

Before starting Phase 1, secure your support network. Several exercises (the capstone board, blind incident drills, peer review) *require* other people. Treat this as a hard prerequisite, not an afterthought.

- [ ] Find a study buddy or mentor who can:
  - Review your deliverables
  - Challenge your assumptions
  - Catch blind spots you can't see
  - Hold you accountable to timelines
- [ ] Join at least one community:
  - Engineering Discord servers
  - Recurse Center
  - r/ExperiencedDevs (Reddit)
  - Local meetups
- [ ] Identify 3-5 people who could serve as your "board" for the Phase 6 capstone

### Pick Your Stack

Too many degrees of freedom in tool selection causes decision paralysis at exactly the moments where the tool doesn't matter.

**If you don't have a strong preference, use this:**

- **Language:** Python (FastAPI) or TypeScript (Express/Fastify)
- **Database:** PostgreSQL
- **Hosting:** Railway or Fly.io
- **Load Testing:** k6
- **Monitoring:** Prometheus + Grafana (free tier)

If you already have a preferred stack, use it. The stack is not the point.

### Set Up Your Progress Tracker

```
## My Progress

### Phase 0: Prerequisites & Setup
- Start Date: ___________
- Study Buddy / Mentor: ___________
- Community Joined: ___________
- Stack Chosen: ___________
- Status: [ ] Not Started / [ ] In Progress / [ ] Complete

### Phase 1: Scale & Distributed Systems
- Start Date: ___________
- Target Completion: ___________
- Status: [ ] Not Started / [ ] In Progress / [ ] Complete
- Key Insight: ___________

### Phase 2: Adversarial Thinking
- Start Date: ___________
- Target Completion: ___________
- Status: [ ] Not Started / [ ] In Progress / [ ] Complete
- Key Insight: ___________

### Phase 3: Resilience & Hardening
- Start Date: ___________
- Target Completion: ___________
- Status: [ ] Not Started / [ ] In Progress / [ ] Complete
- Key Insight: ___________

### Phase 4: Product & Business Context
- Start Date: ___________
- Target Completion: ___________
- Status: [ ] Not Started / [ ] In Progress / [ ] Complete
- Key Insight: ___________

### Phase 5: AI Oversight & Verification
- Start Date: ___________
- Target Completion: ___________
- Status: [ ] Not Started / [ ] In Progress / [ ] Complete
- Key Insight: ___________

### Phase 6: The Capstone
- Start Date: ___________
- Target Completion: ___________
- Status: [ ] Not Started / [ ] In Progress / [ ] Complete
- Key Insight: ___________

### Reflection Questions (Answer Monthly)
1. What surprised me this month?
2. What failure taught me the most?
3. What would I do differently on my last project?
4. How has my judgment changed?
```

---

## Phase 1: Scale & Distributed Systems (The SRE Role)

**Duration:** 8-12 weeks
**Goal:** Understand why code that works on your laptop fails for 10,000 users.

> **Important:** Your URL shortener is the lab environment for the next 6 months. Phases 2 and 3 build directly on it. Design it knowing you'll later need to: add a second service (analytics), implement authentication, and perform a security audit. Slightly over-engineering is fine here.

### Week 1-2: Study Real Failures

- [ ] Read 20+ incident reports on [Postmortems.app](https://postmortems.app)
- [ ] Study case studies in the [Google SRE Book](https://sre.google/sre-book/table-of-contents/)
- [ ] Focus areas: Database failures, cascading failures, cache invalidation bugs
- [ ] Key question for each: *"What assumption did the engineers make that turned out wrong?"*

### Week 3-6: Theory Fundamentals

- [ ] Read *Designing Data-Intensive Applications* by Martin Kleppmann (active reading, take notes)
- [ ] Don't skip: Chapters 5-9 (Replication, Partitioning, Transactions, Distributed Systems)
- [ ] Understand the CAP Theorem and Fallacies of Distributed Computing
- [ ] Build mental models of: eventual consistency, split-brain scenarios, thundering herd problem

### Week 7-12: The Lab Exercise

**Project: Build a URL Shortener and Find Its Breaking Points**

#### Starting Schema

Don't overthink this. Start here and evolve:

```sql
CREATE TABLE urls (
    id SERIAL PRIMARY KEY,
    short_code VARCHAR(10) UNIQUE NOT NULL,
    original_url TEXT NOT NULL,
    created_at TIMESTAMP DEFAULT NOW(),
    user_id INTEGER,          -- for Phase 2 (auth)
    click_count INTEGER DEFAULT 0
);

CREATE TABLE clicks (
    id SERIAL PRIMARY KEY,
    url_id INTEGER REFERENCES urls(id),
    clicked_at TIMESTAMP DEFAULT NOW(),
    referrer TEXT,
    user_agent TEXT
);
```

#### Success Criteria Before Load Testing

Your app should handle:

- **Create:** `POST /shorten` — accepts a URL, returns a short code
- **Read:** `GET /:code` — redirects to the original URL
- **Analytics:** `GET /:code/stats` — returns click count and basic analytics
- **List:** `GET /urls` — returns user's URLs (for Phase 2 auth)

#### Step-by-Step

1. Build the URL shortener with the above functionality
2. Deploy it to real hosting (Railway, Fly.io — **NOT localhost**)
3. Load test with k6 or Locust:
   - 10 users → 100 → 1,000 → 10,000
   - Document what breaks at each tier
4. Fix the first bottleneck (probably DB connection pool)
5. Test again — find the NEXT bottleneck (CPU? Memory? Network?)
6. Repeat until you've identified and fixed 3 different scaling issues

#### Database Deep Dive Exercise

Once your app is running:

1. Seed your database with 10M rows of URL data
2. Write a reporting query: "Top 100 most-clicked URLs this week"
3. Run `EXPLAIN ANALYZE` on the query
4. Optimize from >10s to <100ms
5. Document: What index did you add? Why did it help? What are the write-performance trade-offs?

#### Deliverable

- [ ] GitHub repo with the application
- [ ] "Scaling Report" documenting:
  - Original breaking point (e.g., "Failed at 200 concurrent users")
  - Each bottleneck discovered (connection pool exhaustion, CPU saturation, etc.)
  - How you fixed each one (connection pooling, caching, async processing)
  - Cost implications ("$50/month for 1K users, $500/month for 100K users")
  - Performance graphs showing before/after metrics
  - Database optimization results (query plan before/after, execution time improvement)

**The Lesson:** Systems don't just "scale" or "not scale" — they have cascading bottlenecks. Understanding the cascade is the skill.

### Phase 1 Checkpoint

Before moving to Phase 2, verify:

- [ ] Your URL shortener is deployed and running on real hosting
- [ ] You can explain your 3 bottlenecks to a peer without looking at notes
- [ ] Your app has the basic structure to support adding auth and a second service

**If Phase 1 doesn't click, that's okay.** You've still learned more about production engineering than most bootcamps teach. Evaluate whether to continue at full intensity or adjust scope.

---

## Phase 2: Adversarial Thinking (The CISO Role)

**Duration:** 6-10 weeks
**Goal:** Stop thinking like a builder and start thinking like a breaker.

### Week 1-3: Security Fundamentals

- [ ] Master the [OWASP Top 10](https://owasp.org/www-project-top-ten/) (understand each, don't just memorize)
- [ ] Complete [Cryptopals Crypto Challenges](https://cryptopals.com) Set 1
- [ ] Stretch goal: Complete Set 2 (if you're ahead of schedule)
- [ ] Learn why "rolling your own crypto" fails spectacularly

> **Note on Cryptopals:** Set 1 alone can take 2-4 weeks. If it's consuming your entire Phase 2 timeline, switch to studying real-world crypto failures instead:
> - Heartbleed (OpenSSL buffer over-read)
> - The Debian weak key incident (broken PRNG)
> - PlayStation 3 ECDSA fail (nonce reuse)
> - Padding oracle attacks in practice
>
> The goal is understanding *why not to roll your own crypto*, not becoming a cryptographer.

### Week 4-6: Threat Modeling Exercise

**Project: STRIDE Analysis of Your URL Shortener**

For your Phase 1 URL shortener, perform a STRIDE analysis:

| Threat | Question |
|--------|----------|
| **S**poofing | Can I pretend to be another user? |
| **T**ampering | Can I modify someone else's URLs? |
| **R**epudiation | Can I deny creating a malicious short URL? |
| **I**nformation Disclosure | Can I enumerate all URLs in the system? |
| **D**enial of Service | Can I crash the service with malformed input? |
| **E**levation of Privilege | Can I access admin functions without authorization? |

For EACH threat:

1. **Attack vector** — How would you exploit this?
2. **Mitigation** — How would you fix it?
3. **Residual risk** — What's still vulnerable after the fix?

#### Deliverable

- [ ] Threat Model document (one page per threat category)
- [ ] At least 3 implemented mitigations in your codebase
- [ ] Honest assessment: Proof you can still exploit 1 remaining vulnerability (security is about understanding limits, not claiming perfection)

### Week 7-10: Practical Exploitation

- [ ] Set up the [OWASP Juice Shop](https://owasp.org/www-project-juice-shop/) (intentionally vulnerable application)
- [ ] Complete the guided tour
- [ ] Successfully execute at least 15 challenges including:
  - SQL Injection
  - Cross-Site Scripting (XSS)
  - Broken Authentication
  - Sensitive Data Exposure
- [ ] Focus: Don't just complete challenges — understand *WHY* each vulnerability exists

**The Lesson:** Security isn't a checklist — it's a mindset of "what did I assume that could be violated?"

---

## Phase 3: Resilience & Hardening (The "Blue Team" Role)

**Duration:** 4-6 weeks
**Goal:** Design systems that fail gracefully instead of crashing catastrophically.

### Week 1-2: Resilience Patterns

- [ ] Study resilience patterns:
  - **Circuit Breakers:** Stop calling a failing service
  - **Retries:** With exponential backoff and jitter
  - **Bulkheads:** Isolate failures so they don't spread
  - **Timeouts:** Don't wait forever
  - **Fallbacks:** Degrade gracefully
- [ ] Read *Release It!* by Michael Nygard (Chapters 5-7)

### Observability Setup (Do This Before Chaos Engineering)

- [ ] Implement structured logging (JSON logs, correlation IDs)
- [ ] Add metrics (Prometheus + Grafana, or DataDog free tier)
- [ ] Set up alerts that actually matter (avoid alert fatigue)
- [ ] Create a "runbook" for common failure scenarios
- [ ] Practice debugging production issues with ONLY logs (no debugger access)

### Week 3-5: Chaos Engineering Lab

**Project: Make Your System Survive Network Failures**

Enhancement to your URL shortener:

1. **Add a second service** (analytics service that tracks clicks)
2. **Implement resilience patterns:**
   - Circuit breaker: If analytics is down, still serve URLs
   - Timeout: Don't wait forever for analytics response
   - Fallback: Serve cached click count if live count unavailable
3. **Install [Toxiproxy](https://github.com/Shopify/toxiproxy) to simulate:**
   - 5-second network latency
   - 50% packet loss
   - Complete network partition
4. **Record your system's behavior during each failure mode**

#### Database Operations Exercise

- [ ] Practice a zero-downtime schema migration on your live database:
  - Add a column to the `urls` table while the app is running
  - Document your migration strategy (expand-contract pattern, etc.)
- [ ] Perform a backup and restore:
  - Back up your database
  - Corrupt or delete some data
  - Restore from backup
  - Measure: How long did recovery take? How much data was lost?

#### Deliverable

- [ ] Updated application with resilience patterns implemented
- [ ] 3-minute demo video showing:
  - Normal operation (all services healthy)
  - Service degradation (slow but working)
  - Graceful failure (main function works, analytics disabled with clear user messaging)
- [ ] Chaos test results spreadsheet documenting:

| Failure Injected | System Behavior | User Experience Impact | Recovery Time |
|------------------|-----------------|----------------------|---------------|
| 5s latency | ... | ... | ... |
| 50% packet loss | ... | ... | ... |
| Full partition | ... | ... | ... |
| Database failover | ... | ... | ... |

### Week 6: Blind Incident Drill

**Project: Respond to an Unexpected Failure**

1. Have someone else (study buddy, mentor) inject a failure into your running system *without telling you what they did*
2. Your job:
   - Detect it from monitoring/logs only
   - Diagnose the root cause
   - Mitigate the immediate impact
   - Write a post-mortem
3. Time yourself from detection to mitigation
4. Suggested failures your partner can inject:
   - Kill the analytics service
   - Add a slow query (e.g., missing index on a new query path)
   - Fill the disk with logs
   - Introduce a memory leak
   - Change a DNS record

#### Deliverable

- [ ] Post-mortem document following this template:
  - **Detection:** How did you notice? (alert, user report, dashboard)
  - **Timeline:** Minute-by-minute from detection to resolution
  - **Root Cause:** What actually broke?
  - **Mitigation:** What did you do to stop the bleeding?
  - **Prevention:** What would prevent this from happening again?
  - **Lessons Learned:** What surprised you?

**The Lesson:** Good systems don't just fail — they fail gracefully with clear degradation paths. And debugging under pressure with only observability tools is a distinct skill from planned chaos engineering.

---

## Phase 4: Product & Business Context (The PM/CFO Role)

**Duration:** 6-8 weeks
**Goal:** Learn that "technical perfection" is often a business failure.

### Week 1-2: Business Fundamentals

- [ ] Read *The Mom Test* by Rob Fitzpatrick (learn to validate if features are actually needed)
- [ ] Learn to calculate:
  - **LTV** (Lifetime Value): How much a customer is worth over their lifetime
  - **CAC** (Customer Acquisition Cost): How much it costs to acquire a customer
  - **Payback Period:** How long until you recover CAC
  - **Burn Rate:** How fast you're spending money
- [ ] Understand the unit economics of a software business

### Week 3-4: Post-Mortem Analysis

**Project: Analyze Failed Startups**

Pick 3 real startup post-mortems (find them on [autopsy.io](https://autopsy.io), [failory.com](https://failory.com), or CB Insights):

- **One technical failure** (e.g., Knight Capital — $440M loss in 45 minutes)
- **One product-market fit failure** (e.g., Quibi — $1.75B spent, shut down in 6 months)
- **One timing failure** (e.g., Webvan — too early for grocery delivery)

For each, write a 2-page case study:

1. What they built (technical description)
2. Why it failed (root cause analysis)
3. What they SHOULD have built instead
4. What you would have done differently
5. What the "minimum viable" version would have looked like

#### Deliverable

- [ ] 3 × 2-page case study analyses
- [ ] Pattern recognition: What do these failures have in common?

### Week 5-6: Constraint Analysis Practice

**Exercise:** Before starting ANY new feature, practice this framework:

#### Constraint Triangle Analysis

```
1. TIME: How long do we have?
   - 2 days vs. 2 months changes EVERYTHING

2. QUALITY: What's "good enough"?
   - 99% uptime vs. 99.99% uptime (very different costs)

3. COST: What resources are available?
   - 1 engineer vs. 10 engineers vs. $100K AWS budget
```

For each project, explicitly write:

- What we're optimizing for (and what we're sacrificing)
- What "done" looks like
- What "good enough" means

#### Deliverable

- [ ] Apply this framework to 5 different project scenarios
- [ ] Write "investment memos" justifying your constraint choices

### Week 7-8: Real User Research (The Most Important Exercise)

**Project: Build Something and Watch Real People Use It**

#### Field Exercise

1. **Build a small tool** (anything simple):
   - Expense tracker
   - Habit tracker
   - Recipe manager
   - Chrome extension
   - Doesn't matter WHAT, just make it real

2. **Get 3-5 REAL people (not friends/family) to use it:**
   - Post in relevant subreddit/Discord/forum
   - Use this recruiting script:

   > *"I built [X] to solve [Y problem]. I'm looking for 3-5 people to try it for 20 minutes and give honest feedback. No payment, but you get early access and I'll buy you a coffee. DM me if interested."*

   - 3 users is fine. The insight density from even 3 sessions is enormous.

3. **Watch them use it** (screenshare, Zoom, in-person):
   - **DON'T** help them
   - **DON'T** explain anything
   - Just watch and take notes
   - Sessions should be 20-30 minutes max

4. **Document using this observation template:**

   | Timestamp | What user did | What user said | What user seemed to feel | Your assumption it challenged |
   |-----------|--------------|----------------|--------------------------|-------------------------------|
   | 0:00 | ... | ... | ... | ... |

5. **Write a "Would I Pivot?" memo:**
   - **Kill it** — why it's not worth pursuing
   - **Pivot** — what should change based on learnings
   - **Double down** — what validated your hypothesis

#### Deliverable

- [ ] User research notes (raw observations using template above)
- [ ] Decision memo: Kill / Pivot / Double Down (with reasoning)
- [ ] Reflection: How wrong were your initial assumptions?

**The Lesson:** Engineering without user context is just expensive hobby programming. Most features don't need to exist.

---

## Phase 5: AI Oversight & Verification (The Lead Auditor Role)

**Duration:** 4-6 weeks
**Goal:** Effectively supervise the "junior AI" that writes your code.

### Week 1-2: Code Review Mastery

- [ ] Review 20+ Pull Requests on real open source projects (choose projects you use)
- [ ] Focus on: logic errors, not style/formatting
- [ ] For each PR, ask:
  - What edge case did they miss?
  - What happens if this input is null/negative/huge?
  - What are the security implications?
  - What breaks if this runs concurrently?

### Week 3-4: Property-Based Testing

**Project: Find Where LLMs Hallucinate**

#### LLM Bug Hunt Exercise

1. **Ask an LLM (Claude, GPT-4, etc.) to write these functions:**
   - Date range validator (overlapping ranges, leap years, timezones)
   - Currency converter with rounding rules
   - Password strength checker (unicode, length, entropy)

2. **For each function, write property-based tests:**
   - What invariants should ALWAYS hold?
   - Use [Hypothesis](https://hypothesis.readthedocs.io/) (Python) or [fast-check](https://fast-check.dev/) (JavaScript)
   - Generate 1,000+ random inputs
   - Find the cases where AI code breaks

3. **Document for each failure:**
   - What the AI got wrong
   - Why it got it wrong (wrong assumption? hallucinated API?)
   - How to prompt better next time
   - What the corrected version looks like

#### Deliverable

- [ ] Test suite with failures documented
- [ ] "LLM Bug Patterns" document cataloging:
  - Common failure modes (off-by-one, edge cases, unicode handling)
  - Types of logic AI consistently gets wrong
  - Prompting strategies that reduce errors

### Week 5: Architectural Hallucination Detection

**Project: Evaluate LLM Architectural Decisions**

This catches the most dangerous LLM failure mode: code that *works* but makes fundamentally wrong structural decisions.

1. **Ask an LLM to design the architecture for a notification system** (email, SMS, push notifications) including:
   - Data model
   - API design
   - Queue/processing strategy
   - Retry logic
   - Rate limiting approach

2. **Evaluate the output against what you learned in Phases 1-3:**
   - Would this survive your Phase 1 load tests?
   - Does it use polling where it should use webhooks?
   - Is processing synchronous where it should be queued?
   - Would the data model work at $n = 1{,}000{,}000$ records?
   - Does it have the resilience patterns from Phase 3?
   - What happens when the email provider goes down?

3. **Document the architectural gaps:**
   - What looks reasonable but would fail at scale
   - What's missing entirely (monitoring, error handling, graceful degradation)
   - What the LLM chose that reveals it lacks operational experience

#### Deliverable

- [ ] Architectural review document (red/yellow/green assessment of each decision)
- [ ] Revised architecture with your corrections and reasoning

### Week 6: Domain Logic Verification

**Project: Verify Business Rules in Regulated Domains**

#### Compliance Gap Exercise

1. **Pick a regulated domain:**
   - Finance (overtime pay calculation, tax rules)
   - Healthcare (HIPAA consent workflows)
   - Legal (contract validation, data retention)

2. **Ask an LLM to generate code for a specific business rule:**
   - Example: "Calculate overtime pay for California employees"

3. **Research the ACTUAL legal rules:**
   - Read the regulations
   - Find the edge cases
   - Understand the penalties for getting it wrong

4. **Find where the LLM hallucinated or oversimplified:**
   - Missing edge cases
   - Incorrect thresholds
   - Wrong calculation formulas
   - Compliance gaps

5. **Document the delta between AI output and legal requirements**

#### Deliverable

- [ ] Compliance gap analysis (side-by-side comparison)
- [ ] Corrected implementation with citations to actual regulations
- [ ] Risk assessment: "If we shipped the AI version, what would break?"

**The Lesson:** LLMs are confidently wrong junior developers. You need the domain expertise to catch it — both in logic AND in architecture.

---

## Phase 6: The Capstone (The "Judgment" Test)

**Duration:** 2-4 weeks
**Goal:** Synthesize all roles into senior-level decision-making.

### The "Senior Decision" Scenario

**Context:** You're the tech lead for a fintech app launching in 3 weeks.

**The Problem:** Your QA team finds a race condition in the fund transfer logic:

- If two transfers happen simultaneously from the same account
- And both check balance at the exact same moment
- Both might succeed, overdrafting the account

**Your Options:**

| Option | Description | Trade-off |
|--------|-------------|-----------|
| A | Delay launch 4 weeks to fix properly (database transaction isolation) | Safety vs. time |
| B | Ship with the bug (low probability, add monitoring, accept the risk) | Speed vs. risk |
| C | Ship with a quick fix (global mutex lock = slower transfers, but safe) | Safety vs. performance |
| D | Something else? (be creative) | ??? |

**Business Context:**

- $2M already spent on marketing for the launch date (sunk cost)
- Competitors launching similar product next month (timing pressure)
- Board expects 10K users in month 1 (growth expectations)
- Average transaction: $500 (financial exposure)
- Bug bounty program: you'll cover any overdrafts caused by bugs (liability)

### Required Deliverable

#### 1. Decision Memo (2 pages maximum)

**Executive Summary:**
- Your recommendation (A/B/C/D)
- Key reasoning in 3 sentences

**Technical Analysis:**
- What's the ACTUAL risk? ($\text{probability} \times \text{impact}$)
- What testing did you do to understand the race condition?
- What's the exploit scenario in detail?
- What monitoring would detect if it occurs?

**Business Analysis:**
- Cost of each option (time, money, opportunity cost)
- Revenue impact of delay vs. risk of bug
- Competitive positioning implications
- Reputational risk assessment

**Risk Mitigation Plan:**
- If you ship, what safeguards go in place?
- Detection: How will you know if the bug occurs?
- Response: What's the incident response plan?
- Communication: How do you inform affected users?

**Rollback Plan:**
- If things go wrong, what's the escape hatch?
- How quickly can you disable fund transfers?
- What's the customer communication strategy?

#### 2. Present to a "Board"

- [ ] Find 3-5 people to be your review panel (mentors, peers, online community — you identified these in Phase 0)
- [ ] Present your decision memo
- [ ] Defend your reasoning
- [ ] Answer hostile questions:
  - *"Why didn't you consider option X?"*
  - *"What if the probability is higher than you think?"*
  - *"Who gets fired if this goes wrong?"*
- [ ] Show you've thought through 2nd and 3rd order effects

#### Deliverable

- [ ] Written decision memo
- [ ] Presentation slides (5-10 slides)
- [ ] Recording of your defense (or detailed notes from feedback session)
- [ ] Reflection: What would you change after the challenge questions?

**The Lesson:** Senior judgment is about navigating trade-offs with incomplete information under time pressure. There's no "right" answer — only well-reasoned positions.

---

## Continuous Practices (Throughout All Phases)

### Communication: Write About What You Learn

After each phase deliverable:

- [ ] Write a blog post explaining what you learned:
  - What surprised you
  - What you'd do differently
  - What patterns you noticed
- [ ] Benefits:
  - Forces synthesis of knowledge
  - Practice explaining technical concepts
  - Builds public portfolio
  - Gets feedback from readers

### Monthly Reflection

Answer these questions at the end of each month:

1. What surprised me this month?
2. What failure taught me the most?
3. What would I do differently on my last project?
4. How has my judgment changed?

---

## The Big Trap to Avoid

**Don't treat this as a checkbox curriculum.**

❌ **Wrong approach:**

> "I read the SRE book, skimmed some load tests, checked the box"
>
> "I completed the Juice Shop challenges, moved on"
>
> "I built the URL shortener, it works, done"

✅ **Right approach:**

> "I built something, watched it fail at 1,000 QPS, spent a week understanding why connection pooling matters, can now explain the trade-offs to a junior developer"
>
> "I found a SQL injection in my own code, understood how I missed it during development, changed how I think about user input forever"
>
> "I talked to 5 users, realized I built the wrong thing, killed a week of work, learned more from that failure than any tutorial"

**The deliverables aren't the point — the judgment you develop is the point.**

---

## Final Validation

If you complete this curriculum, you should be able to:

- ✅ Look at AI-generated code and immediately spot the subtle race condition
- ✅ Understand why "technically correct" might be business-wrong
- ✅ Design systems that fail gracefully instead of catastrophically
- ✅ Make senior-level trade-off decisions under pressure
- ✅ Supervise AI-generated code the way a senior engineer supervises juniors
- ✅ Articulate not just WHAT to build, but WHY (or why not)
- ✅ Evaluate LLM architectural decisions, not just functional correctness
- ✅ Respond to production incidents using only observability tools

**This is the "programmer who survives" profile in an AI-generated-code world.**

---

## Resources

### Books

| Book | Author | Relevant Phases |
|------|--------|----------------|
| *Designing Data-Intensive Applications* | Martin Kleppmann | Phase 1 |
| *Site Reliability Engineering* (Google SRE Book) | Free online | Phase 1, 3 |
| *Release It!* | Michael Nygard | Phase 3 |
| *The Mom Test* | Rob Fitzpatrick | Phase 4 |
| *The Phoenix Project* | Gene Kim | DevOps culture |

### Courses & Challenges

- [MIT 6.824 Distributed Systems](https://pdos.csail.mit.edu/6.824/) (free lectures online)
- [Cryptopals Crypto Challenges](https://cryptopals.com)
- [OWASP Top 10](https://owasp.org/www-project-top-ten/)

### Tools

| Tool | Purpose | Phase |
|------|---------|-------|
| [k6](https://k6.io/) or [Locust](https://locust.io/) | Load testing | 1 |
| [Toxiproxy](https://github.com/Shopify/toxiproxy) | Chaos engineering | 3 |
| [OWASP Juice Shop](https://owasp.org/www-project-juice-shop/) | Security practice | 2 |
| [Hypothesis](https://hypothesis.readthedocs.io/) (Python) / [fast-check](https://fast-check.dev/) (JS) | Property-based testing | 5 |
| Prometheus + Grafana | Monitoring & observability | 3 |

### Communities

- [Hacker News](https://news.ycombinator.com)
- [r/ExperiencedDevs](https://reddit.com/r/ExperiencedDevs) (Reddit)
- Local meetups and conferences
- Open source projects in your domain

---

## Start Now

**Pick your starting date:** ___________

**First actions (do these today):**

1. Star or bookmark this curriculum
2. Clone/fork it to track your progress
3. Block time on your calendar for Phase 0
4. Message one person who could be your study buddy
5. Tell someone you're doing this (accountability)

> The difference between reading this and doing this is the difference between knowing *about* judgment and *having* judgment.

**Good luck.** You'll need it — not because it's too hard, but because most people quit when things get difficult. That's actually the most important lesson: **staying power is part of the skill.**
