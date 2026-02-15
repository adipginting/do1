# 🚀 MLOps Engineering Judgment Curriculum v3.1

## Developing Real Taste Through ML Infrastructure — Constraint-First Edition

> **Core Thesis:** When LLMs commoditize code implementation, the valuable skill becomes *taste*—knowing what to build, why it's ugly, and how to make it beautiful.

**Version:** 3.1 (VPS Edition)  
**Updated:** 2025

---

## 📋 Table of Contents

- [What Changed in v3.1](#what-changed-in-v31)
- [Infrastructure Choice: Why VPS?](#infrastructure-choice-why-vps)
- [Why This Curriculum Exists](#why-this-curriculum-exists)
- [Before You Commit: The Honest Trade-offs](#before-you-commit-the-honest-trade-offs)
- [The Three Agreements](#the-three-agreements)
- [The Taste Vocabulary](#the-taste-vocabulary)
- [Timeline Overview](#timeline-overview)
- [Phase 0: Setup & Community](#phase-0-setup--community-1-2-weeks)
- [Phase 1A: Build a Working ML Pipeline](#phase-1a-build-a-working-ml-pipeline-5-6-weeks)
- [Phase 1B: Scale It Until It Breaks](#phase-1b-scale-it-until-it-breaks-4-5-weeks)
- [Phase 1.5: Taste Calibration](#phase-15-taste-calibration--the-honest-checkpoint-2-3-weeks)
- [Phase 2: Go Deep](#phase-2-go-deep-3-4-weeks)
- [Phase 3: Resilience & Production Hardening](#phase-3-resilience--production-hardening-5-6-weeks)
- [Phase 4: Business Context & Product Thinking](#phase-4-business-context--product-thinking-2-3-weeks)
- [Phase 5: AI Oversight & Verification](#phase-5-ai-oversight--verification-3-4-weeks)
- [Phase 6: The Capstone](#phase-6-the-capstone--real-constraints-2-3-weeks)
- [Monthly Practices](#monthly-practices-throughout-all-phases)

---

## 🆕 What Changed in v3.1

- ✅ **Added VPS-first approach:** Build on bare metal, not managed services
- ✅ **Constraint-driven learning:** CPU/memory limits teach systems thinking
- ✅ **Predictable costs:** $10/month VPS instead of surprise cloud bills
- ✅ **Linux mastery required:** No abstraction layers hiding complexity
- ✅ Restructured community requirement as gradient, not gate
- ✅ Split Phase 1 into Build + Scale with reflection point
- ✅ Defined "ugly" concretely with a taste rubric
- ✅ Added Architecture Decision Records throughout
- ✅ Focus on self-hosted infrastructure

---

## 🖥️ Infrastructure Choice: Why VPS?

> **This curriculum uses VPS (Virtual Private Server) exclusively.**

### Why VPS Forces Real Learning

VPS forces you to confront real infrastructure:

| Challenge | What You Learn |
|-----------|----------------|
| Limited CPU/RAM | Resource optimization & pressure awareness |
| Manual database setup | PostgreSQL tuning & recovery |
| No load balancer | Nginx configuration & reverse proxy |
| No logging service | Log rotation & journalctl |
| Process management | Systemd unit files |
| SSL certificates | Let's Encrypt setup |
| Network configuration | Linux networking & firewalls |
| Fixed costs | Architectural trade-offs under constraints |

### Why VPS for This Curriculum

- **💰 Cost:** $5-12/month flat, predictable (no surprise bills)
- **📚 What you learn:** Systems thinking, Linux, resource constraints, how things actually work
- **🔧 Stack:** Self-hosted everything (Dagster, PostgreSQL, MinIO, MLflow)
- **🎯 Philosophy:** Learn under constraints → understand trade-offs → make better decisions

> **Master VPS first. Everything else is just different tooling for the same problems.**

---

## 🤔 Why This Curriculum Exists (Read This First)

### The World is Shifting

- **2020:** "Can you write React?" = employable
- **2025:** LLMs write React competently
- **2028:** "Can you write React?" = table stakes, not differentiator

### Three Data Points

1. **Boris** (created Claude Code) (via Addy Osmani tweet): 
   > "The bottleneck was always judgment, taste, and systems thinking. AI just made that more obvious."

2. **Paul Graham** (2002): 
   > "The recipe for great work is: very exacting taste, plus the ability to gratify it."

3. **Job market**: Staff+ engineers are hired for judgment, not typing speed

**LLMs are solving "ability to gratify it" (implementation).**  
**What remains: Developing taste (judgment).**

> **This curriculum teaches taste.**

If you just want to learn Dagster syntax, take a tutorial. If you want to develop the judgment that survives AI disruption, do this.

---

## ⚖️ Before You Commit: The Honest Trade-offs

**This curriculum costs 8-12 months of focused time.**

### What You're NOT Doing in Those 8-12 Months

- Getting promoted to senior (immediate $30-50K raise)
- Interviewing for FAANG ($50-100K+ raise)
- Building a revenue-generating product
- Deepening specialization in your current domain

### 💸 Opportunity Cost is Real

- 6 months delayed promotion = $15-25K lost
- This compounds over your career
- Be honest: can you afford to optimize for 5 years out vs. 1 year out?

### ✅ This Makes Sense If

- Your current job has no senior engineers (self-teaching anyway)
- Your job is coasting (not learning much)
- You have conviction the AI thesis is right
- You can afford long-term optimization
- You want to be a founding engineer/CTO someday

### ❌ This Does NOT Make Sense If

- You need a raise in the next 12 months
- You have great mentors at current job
- You're optimizing for immediate job market
- You don't actually believe LLMs will commoditize coding
- You prefer specialization over breadth

> **Be honest about which camp you're in.**

---

## 📝 The Three Agreements

Before anything else, agree to these. They override every checklist in this document.

### 1. Taste over Completion

> "I will not just check boxes. I will develop the judgment to spot ugly designs. If I'm completing exercises without my thinking changing, I will stop and go deeper."

### 2. Feedback over Isolation

> "I will get my work reviewed by others. I will calibrate my taste against theirs. I will not hide my work until it's 'ready.'"

### 3. Depth over Breadth

> "I will go deep enough to develop intuition, not just surface knowledge. I'd rather truly understand one system than superficially touch ten."

### 🖊️ Sign This (Seriously)

**I, _________________, commit to:**

- [ ] Stopping if I'm checking boxes without my thinking changing
- [ ] Getting expert feedback even when my work feels "not ready yet"
- [ ] Going deeper rather than moving on when I don't understand
- [ ] Being honest about opportunity costs and whether this is right for me

**Date:** _____________  
**Share with accountability partner:** Yes / No

---

## 🎨 The Taste Vocabulary

> **You can't develop taste without a language for it.**

Use this rubric throughout the curriculum.

### What "Ugly" Means (Concretely)

An architecture is ugly when it has:

| Smell | Definition | Example |
|-------|------------|---------|
| **Hidden coupling** | Components that seem independent but fail together | Feature engineering and model serving share a database connection pool |
| **Implicit assumptions** | Works on the author's machine, breaks elsewhere | Hardcoded file paths, assumes unlimited memory |
| **Proportionality violations** | Complex solutions to simple problems (or vice versa) | Kubernetes for a single-user app; no retry logic for a distributed system |
| **Time bombs** | Works today, guaranteed to break at 10x | Loading all data into memory, unbounded queries |
| **Operational blindness** | No way to know if it's healthy without reading code | No metrics, no structured logs, no alerts |
| **Cargo culting** | Using tools because "that's what you do" | Kafka for 100 events/day; microservices for a 2-person team |
| **Cleverness over clarity** | Optimized for writing, not reading | Nested comprehensions, magic numbers, no comments on "why" |

> **When reviewing any system (yours or others), name the smells.**

### What "Beautiful" Means (Concretely)

An architecture is beautiful when it has:

| Quality | Definition | Example |
|---------|------------|---------|
| **Proportional complexity** | Complexity matches the problem's difficulty | Simple pipeline for simple data; distributed system only when needed |
| **Explicit trade-offs** | Decisions are documented with rationale | "We chose eventual consistency because latency matters more than perfect accuracy here" |
| **Graceful degradation** | Fails partially, not totally | Serves cached predictions when model is down |
| **Observable by default** | You can understand system health from outside | Dashboards, structured logs, meaningful alerts |
| **Deletable parts** | Components can be removed without cascading failures | Loose coupling, clear interfaces |
| **Obvious flow** | A new engineer can follow the data path in 5 minutes | Clear naming, linear pipeline, documented entry points |

---

## ⏱️ Timeline Overview (Honest Estimates)

| Phase | Duration | Weekly Hours | What You Build |
|-------|----------|--------------|----------------|
| **Phase 0:** Setup & Community | 1-2 weeks | 8-10 hrs | Your support network |
| **Phase 1A:** Build | 5-6 weeks | 15-20 hrs | Working ML pipeline |
| **Phase 1B:** Scale & Break | 4-5 weeks | 15-20 hrs | Scaling report + cost analysis |
| **Phase 1.5:** Taste Calibration | 2-3 weeks | 10 hrs | Gap analysis + honest checkpoint |
| **Phase 2:** Go Deep | 3-4 weeks | 15-20 hrs | Deep expertise pulled by pain |
| **Phase 3:** Resilience | 5-6 weeks | 15-20 hrs | Production-hardened pipeline |
| **Phase 4:** Business Context | 2-3 weeks | 10 hrs | Pivot decision + user research |
| **Phase 5:** AI Oversight | 3-4 weeks | 10-15 hrs | LLM verification skills |
| **Phase 6:** Capstone | 2-3 weeks | 15-20 hrs | Real-world constraints |
| **Total** | **28-38 weeks** | **Intense** | **Portfolio + Judgment** |

**Sustainable alternative:** 12-15 months at 10 hrs/week

**Buffer for life:** Add 20%. Real estimate: **34-46 weeks intensive** or **14-18 months sustainable**

### What "15-20 hrs/week intensive" Actually Means

**Planned time:**
- Coding/building: 10-15 hrs
- Reading: 5-7 hrs
- **Total: 15-22 hrs**

**Unplanned time (that always happens):**
- Debugging "why won't Docker start": 3-5 hrs/week
- Re-reading chapters that didn't stick: 2-3 hrs/week
- Cohort coordination: 1-2 hrs/week
- **Actual total: 21-32 hrs/week**

**If you work full-time:**
- Work: 40 hrs
- Curriculum: 25-30 hrs
- **Total: 65-70 hr weeks**

> **This is not sustainable for 9 months.**

**Realistic for full-time workers: 10 hrs/week = 18-24 months.**

> These estimates do NOT include monthly taste calibrations (~4-6 hrs each) or the 6-month return exercise. Budget those separately.

---

## 🚀 Phase 0: Setup & Community (1-2 Weeks)

**Goal:** Set up your environment and your feedback network. Neither is optional.

### Your Technology Stack

**Recommended stack:**

- **Infrastructure:** VPS (Hetzner/DigitalOcean/Vultr, 2GB RAM minimum)
- **OS:** Ubuntu 22.04 LTS
- **Orchestrator:** Dagster (better DX than Airflow for learning)
- **Language:** Python 3.9+
- **Containers:** Docker + Docker Compose
- **Database:** PostgreSQL 15
- **Object Storage:** MinIO (S3-compatible)
- **Monitoring:** Prometheus + Grafana
- **ML Tracking:** MLflow
- **API:** FastAPI + Gunicorn
- **Web Server:** Nginx (reverse proxy)
- **Load Testing:** Locust

> **If you have a preferred stack, use it. The stack is not the point.**

### Community: A Gradient, Not a Gate

You need feedback to develop taste. But "find 5 people for a 9-month commitment" is unrealistic advice. Instead, aim for the highest tier you can sustain:

#### 🥉 Tier 1: Minimum Viable (REQUIRED)

- **Work in public.** Create a GitHub repo for this curriculum. Commit weekly.
- **Write as you learn.** Start a blog, dev.to, or even a Twitter/X thread series documenting your journey.
- **Engage in 2-3 communities weekly:**
  - [MLOps Community Slack](https://mlops.community/)
  - [r/MLOps](https://reddit.com/r/mlops)
  - [r/ExperiencedDevs](https://reddit.com/r/ExperiencedDevs)
  - Answer questions, ask questions, share what you're building

**Why this works even solo:** Public work attracts feedback. People comment on repos, blog posts get responses, Slack messages start conversations.

#### 🥈 Tier 2: Good (AIM FOR THIS)

Everything in Tier 1, plus:

- **Find 1 accountability partner.** One person is sustainable. 5 is a project management nightmare.
  - Post: "Starting an MLOps learning curriculum. Looking for 1 partner for bi-weekly code reviews and architecture discussions. ~1 hour every 2 weeks."
  - Try: MLOps Slack, dev Discord servers, local meetups, coworkers
- **Bi-weekly code review exchange.** You review theirs, they review yours.

#### 🥇 Tier 3: Great (IF YOU CAN)

Everything in Tier 2, plus ONE of:

- **Full cohort (3-5 people)** with weekly syncs
  - If you can make this happen, it's the highest-value option
  - Set rules: Miss two syncs = you're out
  - Demo days at end of each major phase

- **Active open source contribution** to Dagster, MLflow, or Feast
  - Realistic timeline: 1 contribution in first month (docs or small bug fix)
  - Goal: See how maintainers think about design in PR reviews

- **Monthly mentor check-in** with a staff+ ML/infrastructure engineer
  - Use [ADPList](https://adplist.org), cold email, or your network
  - Be specific: "Can I get 30 minutes monthly to review my architecture decisions?"
  - Expect a 5-10% response rate on cold outreach — send 20-30 messages

> **Key point:** Start at Tier 1 immediately. Upgrade to Tier 2-3 as opportunities arise. Don't wait for the perfect community to begin.

### Environment Setup

#### VPS Setup

**Step 1: Provision VPS**

Choose a provider:
- [Hetzner](https://www.hetzner.com/cloud) — Best value, EU-based
- [DigitalOcean](https://www.digitalocean.com/) — Good docs, worldwide
- [Vultr](https://www.vultr.com/) — Similar to DO, more locations

Minimum specs:
- **RAM:** 2GB (4GB recommended)
- **CPU:** 1 vCPU (2 recommended)
- **Disk:** 40GB SSD
- **Cost:** $6-12/month

**Step 2: Initial Server Setup**

```bash
# SSH into your server
ssh root@your-server-ip

# Update system
apt update && apt upgrade -y

# Install Docker
curl -fsSL https://get.docker.com -o get-docker.sh
sh get-docker.sh

# Install Docker Compose
apt install docker-compose -y

# Create non-root user
adduser mlops
usermod -aG sudo mlops
usermod -aG docker mlops

# Configure firewall
ufw allow OpenSSH
ufw allow 80/tcp
ufw allow 443/tcp
ufw enable

# Install Nginx
apt install nginx -y
systemctl enable nginx

# Install Certbot for SSL
apt install certbot python3-certbot-nginx -y
```

**Step 3: Setup DNS & SSL**

```bash
# Point your domain to server IP (A record)
# example: mlops.yourdomain.com -> your-server-ip

# Get SSL certificate
certbot --nginx -d mlops.yourdomain.com
```

**Step 4: Install Python Stack**

```bash
# Install Python tools
apt install python3-pip python3-venv -y

# Create virtual environment
python3 -m venv /home/mlops/venv
source /home/mlops/venv/bin/activate

# Install packages
pip install dagster dagster-webserver dagster-docker
pip install scikit-learn pandas numpy mlflow
pip install fastapi uvicorn gunicorn
pip install locust
pip install psycopg2-binary boto3
```

**Step 5: Setup Docker Compose Stack**

Create `/home/mlops/docker-compose.yml`:

```yaml
version: '3.8'

services:
  postgres:
    image: postgres:15
    environment:
      POSTGRES_USER: mlops
      POSTGRES_PASSWORD: changeme
      POSTGRES_DB: mlops
    volumes:
      - postgres_data:/var/lib/postgresql/data
    restart: unless-stopped

  minio:
    image: minio/minio
    command: server /data --console-address ":9001"
    environment:
      MINIO_ROOT_USER: minioadmin
      MINIO_ROOT_PASSWORD: changeme
    volumes:
      - minio_data:/data
    ports:
      - "9000:9000"
      - "9001:9001"
    restart: unless-stopped

  prometheus:
    image: prom/prometheus
    volumes:
      - ./prometheus.yml:/etc/prometheus/prometheus.yml
      - prometheus_data:/prometheus
    ports:
      - "9090:9090"
    restart: unless-stopped

  grafana:
    image: grafana/grafana
    volumes:
      - grafana_data:/var/lib/grafana
    ports:
      - "3000:3000"
    restart: unless-stopped

volumes:
  postgres_data:
  minio_data:
  prometheus_data:
  grafana_data:
```

```bash
# Start services
cd /home/mlops
docker-compose up -d
```

### You Must Be Able To

- ✅ SSH into your server
- ✅ Deploy a Docker container
- ✅ Restart services with systemd
- ✅ Read logs via `journalctl`
- ✅ Configure Nginx reverse proxy
- ✅ View Prometheus metrics
- ✅ Access Grafana dashboards

> **If this is painful — good. That's learning.**

---

### Architecture Decision Record (ADR) Practice

Start this now. Use it throughout every phase.

Create a `decisions/` folder in your repo. For every significant choice, write:

```markdown
# ADR-001: Choosing Dagster Over Airflow

## Status
Accepted

## Context
Need an orchestrator for ML pipeline. Main options: Airflow, Dagster, Prefect.

## Decision
Dagster.

## Rationale
- Better local development experience (faster iteration)
- Asset-based model fits ML workflows better than task-based
- Growing adoption in MLOps community
- Good documentation for learning

## Trade-offs Accepted
- Smaller community than Airflow (less Stack Overflow answers)
- Less battle-tested at massive scale
- May need to learn Airflow later for some jobs

## What Would Change This Decision
- If deploying to a company that's standardized on Airflow
- If we needed 1000+ concurrent pipelines (Airflow's scheduler is more proven)
```

> You will write 15-25 ADRs over this curriculum. They are your taste development journal.

---

### Create Your Progress Tracker

```markdown
# My Curriculum Progress

**Start Date:** _______________
**Community Tier:** 1 / 2 / 3
**Accountability Partner:** _______________ (or "Working in public at: [URL]")

## Phase Completion

- [ ] Phase 0: Setup (Target: ___ )
- [ ] Phase 1A: Build (Target: ___ )
- [ ] Phase 1B: Scale (Target: ___ )
- [ ] Phase 1.5: Calibration (Target: ___ )
- [ ] Phase 2: Depth (Target: ___ )
- [ ] Phase 3: Resilience (Target: ___ )
- [ ] Phase 4: Business (Target: ___ )
- [ ] Phase 5: AI Oversight (Target: ___ )
- [ ] Phase 6: Capstone (Target: ___ )

## Metrics

- **ADR Count:** ___
- **Blog Posts Published:** ___
- **Architecture Reviews Given:** ___
- **Architecture Reviews Received:** ___

## Monthly Reflection (Answer end of each month)

1. What surprised me this month?
2. What failure taught me the most?
3. Name one "ugly" smell I can now spot that I couldn't before.
4. What would I do differently on my last project?
5. Am I developing *intuition* or just *knowledge*?
```

### Community Health Check

Add this to the end of each phase:

```markdown
## Community Check (End of Phase ___)

- [ ] Tier 1: Have I posted work publicly? Getting any engagement?
- [ ] Can I upgrade to Tier 2? (If not, why? Do I need to be more active?)
- [ ] If solo still: Is isolation hurting my learning? Evidence: ___
- [ ] Have I gotten feedback from at least 1 other person this phase?
```

---

## 🏗️ Phase 1A: Build a Working ML Pipeline (5-6 Weeks)

**Goal:** Build a complete ML pipeline from scratch AND develop your first instincts about what makes a system elegant vs. ugly.

### Week 1-2: Study Before You Build

#### Study Failures

**Read 10 incident reports on ML system failures:**

- Search: "Uber Michelangelo postmortem", "Netflix ML incident", "Spotify recommendation outage"
- Also: Google "site:blog.[company].com ML pipeline failure" for various companies
- Good aggregator: SRE Weekly, Incident.io blog

For each incident, document using the taste vocabulary:

```markdown
# Incident: [Company] [System] Failure

**What happened:** [1-2 sentences]
**Root cause:** [Technical cause]
**Taste smell:** [Which "ugly" pattern from the rubric?]
**What assumption broke at scale?**
**Could this have been predicted from the architecture alone?**
```

#### Study Excellence

**Pick 3 ML systems known for elegance:**

- Uber's Michelangelo platform
- Netflix's model serving architecture
- Spotify's feature platform
- (Or substitute: LinkedIn's Pro-ML, Airbnb's Bighead, Google's TFX)

For each, document using the "beautiful" rubric:

```markdown
# Beautiful System: [Name]

**Architecture overview:** [Draw it — pen and paper is fine]

**Which "beautiful" qualities does it have?**
- Proportional complexity? How?
- Explicit trade-offs? Where documented?
- Observable by default? What signals?
- Obvious flow? Could a new hire follow it?

**What they chose NOT to do:**
- [This is often more revealing than what they did]

**What constraints forced the elegant solution:**
- [Beautiful systems are usually born from constraints, not freedom]

**One pattern I want to try in my own pipeline:**
[Description]
```

**ADR opportunity:** After this study, write ADR-002 about a design pattern you want to adopt and why.

### Week 3-4: Theory Fundamentals

**Read *Designing Data-Intensive Applications* Chapters 5-9:**

- Chapter 5 (Replication): When do you need it? What can go wrong?
- Chapter 6 (Partitioning): How to split data. Relevance to feature stores.
- Chapter 7 (Transactions): What guarantees do you actually need?
- Chapter 8 (Distributed Systems): Failure modes you must internalize.
- Chapter 9 (Consistency): Eventual vs. strong. When each matters.

**After each chapter, write a 1-paragraph summary:**  
"What does this mean for my ML pipeline?"

**Understand these concepts well enough to explain them:**

- CAP theorem (and why it's usually misunderstood)
- Backpressure and flow control
- Batch vs. stream processing trade-offs
- Feature store patterns (online vs. offline)

### Week 5-6: Build the Pipeline

#### Project: Weather Prediction ML Pipeline

**What you're building:**

```
🔧 VPS Architecture:

Data Source (Weather API: OpenWeather or NOAA)
    ↓
Ingestion (Dagster asset running on VPS)
    ↓
Storage (MinIO bucket — raw parquet files)
    ↓
Feature Engineering (Dagster asset)
    ↓
Model Training (scikit-learn, tracked with self-hosted MLflow)
    ↓
Model Registry (MLflow model registry on VPS)
    ↓
Serving (FastAPI + Gunicorn behind Nginx)
    ↓
Monitoring (Prometheus + Grafana on VPS)
```

**Data Ingestion:**

```python
from dagster import asset, AssetExecutionContext
import requests
import pandas as pd
import os

@asset
def raw_weather_data(context: AssetExecutionContext) -> pd.DataFrame:
    """Fetch weather data from OpenWeather API.
    
    Fetches historical weather data and stores as parquet.
    Currently loads all data into memory — this is a known
    limitation that will break at ~1M rows (see Phase 1B).
    
    We're accepting this limitation for now because:
    - Easier to build and test with small datasets
    - VPS has limited RAM (forces optimization in Phase 1B)
    - Phase 1B will force us to fix it
    """
    df = fetch_weather_data(api_key=os.environ["OPENWEATHER_KEY"])
    
    # Store to MinIO (S3-compatible)
    storage_path = os.environ.get("STORAGE_PATH", "s3://mlops/raw/weather.parquet")
    df.to_parquet(storage_path)
    
    context.log.info(f"Ingested {len(df)} rows")
    return df


def fetch_weather_data(api_key: str) -> pd.DataFrame:
    """Fetch data from OpenWeather API.
    
    Note: No retry logic yet. Will add in Phase 3.
    """
    response = requests.get(
        "https://api.openweathermap.org/data/2.5/forecast",
        params={"appid": api_key, "units": "metric"},
        timeout=10
    )
    response.raise_for_status()
    return pd.DataFrame(response.json()["list"])
```

**Feature Engineering:**

```python
@asset
def weather_features(
    context: AssetExecutionContext,
    raw_weather_data: pd.DataFrame
) -> pd.DataFrame:
    """Engineer features for weather prediction.
    
    Creates temporal features and rolling statistics.
    
    Note: Rolling windows assume sorted, continuous timestamps.
    If data has gaps, rolling calculations will be misleading.
    This is acceptable for now (weather data is continuous), but
    would need handling for sparse data. See ADR-003.
    """
    df = raw_weather_data.copy()
    
    # Temporal features
    df["hour"] = df["timestamp"].dt.hour
    df["day_of_week"] = df["timestamp"].dt.dayofweek
    df["month"] = df["timestamp"].dt.month
    
    # Rolling statistics (7-day window = 168 hours)
    df["temp_rolling_mean"] = df["temperature"].rolling(window=168).mean()
    df["temp_rolling_std"] = df["temperature"].rolling(window=168).std()
    
    # Handle NaN from rolling window
    df = df.dropna()
    
    df.to_parquet("s3://bucket/features/weather_features.parquet")
    context.log.info(f"Generated {len(df)} feature rows")
    return df
```

**Model Training:**

```python
@asset
def trained_model(
    context: AssetExecutionContext,
    weather_features: pd.DataFrame
):
    """Train weather prediction model and log to MLflow.
    
    Uses RandomForest as baseline. Model choice is deliberate:
    - Handles non-linear relationships
    - Robust to feature scaling
    - Interpretable feature importances
    
    See ADR-004 for why we chose RF over gradient boosting.
    """
    import mlflow
    from sklearn.ensemble import RandomForestRegressor
    from sklearn.model_selection import train_test_split
    from sklearn.metrics import mean_absolute_error
    
    feature_cols = [
        "temperature", "humidity", "pressure",
        "hour", "day_of_week", "month",
        "temp_rolling_mean", "temp_rolling_std"
    ]
    
    X = weather_features[feature_cols]
    y = weather_features["next_day_temp"]
    
    # Time series: no shuffle
    X_train, X_test, y_train, y_test = train_test_split(
        X, y, test_size=0.2, shuffle=False
    )
    
    with mlflow.start_run():
        model = RandomForestRegressor(n_estimators=100, random_state=42)
        model.fit(X_train, y_train)
        
        # Evaluate
        predictions = model.predict(X_test)
        mae = mean_absolute_error(y_test, predictions)
        
        mlflow.log_metric("mae", mae)
        mlflow.log_param("n_estimators", 100)
        mlflow.sklearn.log_model(model, "weather_model")
        
        context.log.info(f"Model trained. MAE: {mae:.2f}")
    
    return model
```

**Model Serving:**

```python
from fastapi import FastAPI, HTTPException
from pydantic import BaseModel
import mlflow.pyfunc
import logging

logger = logging.getLogger(__name__)

app = FastAPI()

# Load model once at startup
try:
    model = mlflow.pyfunc.load_model("models:/weather_model/Production")
except Exception as e:
    logger.error(f"Failed to load model: {e}")
    model = None


class PredictionRequest(BaseModel):
    temperature: float
    humidity: float
    pressure: float
    hour: int
    day_of_week: int
    month: int
    temp_rolling_mean: float
    temp_rolling_std: float


@app.post("/predict")
def predict(request: PredictionRequest):
    if model is None:
        raise HTTPException(503, "Model not loaded")
    
    features = [list(request.dict().values())]
    prediction = model.predict(features)
    return {"prediction": float(prediction[0])}


@app.get("/health")
def health():
    """Health check endpoint.
    
    Current implementation only checks if model loaded.
    In production, should also check:
    - Can the model actually make predictions?
    - Is the database reachable?
    - Are dependencies healthy?
    
    See Phase 3 for a more robust health check.
    """
    return {
        "status": "healthy" if model is not None else "degraded",
        "model_loaded": model is not None
    }
```

**Basic Monitoring:**

```python
# Add to your FastAPI app
from prometheus_client import Counter, Histogram, generate_latest
from starlette.responses import Response
import time

prediction_count = Counter(
    "predictions_total", 
    "Total predictions made",
    ["status"]
)
prediction_latency = Histogram(
    "prediction_latency_seconds",
    "Prediction latency",
    buckets=[0.01, 0.05, 0.1, 0.25, 0.5, 1.0, 2.5]
)

@app.post("/predict")
def predict(request: PredictionRequest):
    start = time.time()
    try:
        if model is None:
            raise HTTPException(503, "Model not loaded")
        features = [list(request.dict().values())]
        result = model.predict(features)
        prediction_count.labels(status="success").inc()
        return {"prediction": float(result[0])}
    except Exception as e:
        prediction_count.labels(status="error").inc()
        raise
    finally:
        prediction_latency.observe(time.time() - start)

@app.get("/metrics")
def metrics():
    return Response(generate_latest(), media_type="text/plain")
```

### 📦 Deliverable Phase 1A

- [ ] GitHub repo with complete pipeline (well-documented)
- [ ] Working end-to-end: data in → predictions out
- [ ] Deployed to VPS (Docker Compose stack running)
- [ ] Basic Grafana dashboard (prediction count, latency, errors)
- [ ] Can handle 10 requests/second
- [ ] At least 2 ADRs written (orchestrator choice, model choice)
- [ ] Blog post or public write-up: "What I built and what I'd change"

---

### 🔍 Phase 1A Reflection (Do Before Moving On)

> **This is critical. Don't skip.**

```markdown
# Phase 1A Reflection

**What was harder than expected?**
[Be specific]

**What taste smells (from the rubric) exist in my own pipeline?**
- Hidden coupling: [yes/no - where?]
- Implicit assumptions: [yes/no - where?]
- Time bombs: [yes/no - where?]
- Operational blindness: [yes/no - where?]
- Proportionality violations: [yes/no - where?]
- Cargo culting: [yes/no - where?]

**What would I do differently if I started over?**
[Not "I'd write better code" but specific architectural decisions]

**What am I most uncertain about in my architecture?**
[What keeps you up at night?]

**Am I still excited about this, or am I forcing it?**
[ ] Excited - let's keep going
[ ] Neutral - it's fine
[ ] Forcing it - might need to reconsider

**Can I explain my architecture WITHOUT looking at code?**
[ ] Yes - I can whiteboard it from memory
[ ] Partially - I remember the flow but not details
[ ] No - I need to look at code
```

> If you answered "Forcing it" or "No" to the last question, pause and reflect.

---

## 📈 Phase 1B: Scale It Until It Breaks (4-5 Weeks)

**Goal:** Discover where your assumptions fail under pressure. The breaks teach more than the building.

### Week 1-2: Systematic Stress Testing

#### Test 1: Data Volume

| Scale | Expected Behavior | Actual Behavior | What Broke | Time to Process |
|-------|------------------|-----------------|------------|-----------------|
| 10K rows | Works fine | | | |
| 100K rows | Should work | | | |
| 1M rows | Might struggle | | | |
| 10M rows | Will break | | | |

```bash
# Generate synthetic data at increasing scales
python scripts/generate_data.py --rows 10000
python scripts/generate_data.py --rows 100000
python scripts/generate_data.py --rows 1000000
python scripts/generate_data.py --rows 10000000

# 🔧 VPS: Monitor system resources in real-time
htop  # Watch RAM usage
iotop  # Watch disk I/O
watch -n 1 'df -h'  # Watch disk space

# For each run, record:
# - Peak RAM usage (will hit 2GB limit!)
# - CPU saturation
# - Disk I/O wait time
# - OOM killer activation (check: dmesg | grep oom)
```

#### Test 2: API Load

```python
# locustfile.py
from locust import HttpUser, task, between

class WeatherUser(HttpUser):
    wait_time = between(0.1, 0.5)
    
    @task
    def predict(self):
        self.client.post("/predict", json={
            "temperature": 72.0,
            "humidity": 45.0,
            "pressure": 1013.0,
            "hour": 14,
            "day_of_week": 2,
            "month": 6,
            "temp_rolling_mean": 70.0,
            "temp_rolling_std": 5.0
        })
```

```bash
# 🔧 VPS: Run locust FROM your local machine TO the VPS
locust -f locustfile.py --host https://mlops.yourdomain.com

# Ramp: 10 → 100 → 500 → 1000 users
# VPS will likely max out around 100-200 concurrent users with 1 vCPU
```

| Concurrent Users | p50 Latency | p95 Latency | p99 Latency | Error Rate | Notes |
|-----------------|-------------|-------------|-------------|------------|-------|
| 10 | | | | | |
| 100 | | | | | |
| 500 | | | | | |
| 1000 | | | | | |

#### Test 3: Concurrent Pipeline Runs

```bash
# Trigger 5 → 10 → 20 Dagster runs simultaneously

# 🔧 VPS-specific failures you'll encounter:
# - RAM exhaustion (OOM killer)
# - CPU saturation
# - Disk I/O bottlenecks
# - Database connection pool exhaustion
# - File descriptor limits

# Do runs interfere with each other?
```

### Week 3-4: Fix Bottlenecks

**🔧 VPS Edition: Common bottlenecks you WILL hit:**

1. **OOM Killer** - Linux kills your process when RAM exhausted
2. **Disk fills up** - Logs, temp files, or data storage
3. **CPU saturation** - 100% usage, everything slows down
4. **PostgreSQL locks** - Concurrent writes blocking each other
5. **Nginx connection limits** - Default worker_connections = 768
6. **File descriptor limits** - Too many open files (ulimit -n)

For each bottleneck, document:

```markdown
# Bottleneck: [Name]

**Discovery:** How I found it (metrics, errors, observation)
**Scale it appeared:** [e.g., "At 1M rows" or "At 500 concurrent users"]
**Root cause:** [Technical explanation]
**Taste smell:** [Which "ugly" pattern from the rubric]

**Fix applied:**
[Description + code snippet]

**Performance impact:**
- Before: [metric]
- After: [metric]
- Improvement: [X%]

**Cost implication:**
- Before fix, at 100K users/month: $___/month
- After fix, at 100K users/month: $___/month

**ADR written:** ADR-00X
```

**Example Fixes:**

**🔧 VPS-Specific Fix: OOM Killer**

```bash
# Problem: Pipeline crashes at 1M rows with "Killed"
# Check: dmesg | grep -i oom
# Output: "Out of memory: Killed process 1234 (python)"

# Solution 1: Add swap space (emergency backup)
sudo fallocate -l 2G /swapfile
sudo chmod 600 /swapfile
sudo mkswap /swapfile
sudo swapon /swapfile

# Solution 2: Process in chunks (proper fix)
```

```python
# Before (loads all into memory):
df = pd.read_parquet("s3://bucket/data.parquet")  # 2GB+ in RAM!
processed = process_data(df)

# After (chunked processing):
def process_in_chunks(file_path, chunk_size=100_000):
    for chunk in pd.read_parquet(file_path, chunksize=chunk_size):
        yield process_data(chunk)

# Impact: Can now handle 10M+ rows on 2GB RAM VPS
# Cost: Same ($10/month flat)
# Trade-off: Slower processing, but completes successfully
```

**🔧 VPS-Specific Fix: Disk Space**

```bash
# Problem: Pipeline fails with "No space left on device"
# Check: df -h
# Output: /dev/sda1  40G  39G  0G  100% /

# Find what's using space
du -sh /* | sort -hr | head -10

# Common culprits:
# - /var/log (nginx, systemd logs)
# - /var/lib/docker (old images)
# - /home/mlops/data (temp files)

# Fix: Log rotation
sudo nano /etc/logrotate.d/mlops

# Clean Docker
docker system prune -a --volumes

# Impact: Freed 15GB
# Cost: $0
```

### Week 4-5: Resource Analysis & Cost Awareness

**VPS Resource Analysis:**

```bash
# Run on your VPS
htop                    # CPU/RAM usage
docker stats            # Per-container usage
df -h                   # Disk usage
free -h                 # Memory details
```

**Actual usage this week:**

| Resource | Usage | VPS Limit | Utilization | Notes |
|----------|-------|-----------|-------------|-------|
| RAM | ___ GB | 2 GB | ___% | Peak usage during pipeline runs |
| CPU | ___% avg | 100% | ___% peak | Average and peak load |
| Disk | ___ GB | 50 GB | ___% | Data + Docker images + logs |
| Network | ___ GB | 2 TB | ___% | Usually included in VPS cost |
| **Total Cost** | | | | **$12/month flat** |

**Monthly cost:** $12 (fixed, predictable)  
**Annual cost:** $144 (no surprises)

**VPS Scaling Strategy:**

| Scale | Requests/Day | VPS Config | Monthly Cost | Notes |
|-------|--------------|------------|--------------|-------|
| Current (dev) | 100 | 2GB RAM, 1 vCPU | $12 | Single VPS |
| 100 users | 1K | 4GB RAM, 2 vCPU | $24 | Upgrade VPS |
| 1K users | 10K | 8GB RAM, 4 vCPU + Redis | $60 | Larger VPS + caching |
| 10K users | 100K | Load balancer + 3x 4GB VPS | $200 | Horizontal scaling |
| 100K users | 1M | Load balancer + 10x 8GB VPS | $800 | Multiple VPS + CDN |

### 📦 Deliverable Phase 1B

- [ ] Scaling report with 3+ bottlenecks documented
- [ ] Load test results with graphs
- [ ] Resource usage analysis with scaling projections
- [ ] Updated Grafana dashboard
- [ ] ADRs for each major fix decision
- [ ] Blog post: "How my ML pipeline broke at scale (and how I fixed it)"

---

## 🎯 Phase 1.5: Taste Calibration — The Honest Checkpoint (2-3 Weeks)

**Goal:** Calibrate your taste against experts. Determine if you're developing judgment or just completing exercises.

> **This is the most important exercise in the entire curriculum.**

### Week 1: Get Expert Feedback

**Find 3 people to review your pipeline:**

- **Easiest:** Post in MLOps Slack with link to your (public) repo
- **Good:** Your accountability partner + someone from a community
- **Best:** A staff+ engineer (use ADPList, cold outreach, or your network)

Send this message:

```
I built this ML pipeline as a learning project (link to repo + architecture diagram).
Could you spend 15 minutes reviewing it?

Specific questions:
1. What will break first when this serves 10x more traffic?
2. What's the ugliest part of this architecture?
3. If you had to maintain this at 2 AM, what would frustrate you?
4. What's one pattern I should learn from?
```

**BEFORE sending:** Write down YOUR predictions for what they'll say.

```markdown
# My Predictions (BEFORE Expert Feedback)

**Reviewer 1:**
- What will break: ___
- Ugliest part: ___
- 2 AM frustration: ___
- Pattern to learn: ___

**Reviewer 2:**
- What will break: ___
- Ugliest part: ___
- 2 AM frustration: ___
- Pattern to learn: ___

**Reviewer 3:**
- What will break: ___
- Ugliest part: ___
- 2 AM frustration: ___
- Pattern to learn: ___
```

### Week 2: Gap Analysis

```markdown
# Taste Gap Analysis

## Reviewer 1: [Name/Source]

| My Prediction | Their Actual Feedback | Match? | Why I Missed It |
|--------------|----------------------|--------|-----------------|
| Will break: ___ | Will break: ___ | ✓/✗ | |
| Ugly: ___ | Ugly: ___ | ✓/✗ | |
| 2 AM: ___ | 2 AM: ___ | ✓/✗ | |
| Pattern: ___ | Pattern: ___ | ✓/✗ | |

## Aggregate Accuracy
- Predictions matched: ___/12 (___%)
- Categories I'm good at predicting: ___
- Categories I'm blind to: ___

## What This Tells Me About My Taste

**I'm good at spotting:**
[E.g., "I correctly predicted the database bottleneck"]

**I'm blind to:**
[E.g., "I completely missed operational concerns like monitoring gaps"]

**My mental model is missing:**
[E.g., "I don't think enough about maintenance"]

**Specific things I'll change:**
1. ___
2. ___
3. ___
```

### Week 3: Deep Study of One Beautiful System

**Pick ONE ML platform to study deeply:**

- Uber Michelangelo
- Netflix model serving
- Spotify feature platform
- LinkedIn Pro-ML

**Read EVERYTHING about it:**

- Original blog post(s)
- Follow-up posts about evolution
- Conference talks (YouTube)
- GitHub repos if available
- Design docs if public

Document:

```markdown
# Deep Study: [System Name]

## Architecture (draw it)
[Diagram - hand-drawn is fine, upload photo]

## Beautiful Qualities (from rubric)
- **Proportional complexity:** [how?]
- **Explicit trade-offs:** [where documented?]
- **Observable by default:** [what signals?]
- **Obvious flow:** [could I follow it?]
- **Graceful degradation:** [examples?]
- **Deletable parts:** [how decoupled?]

## What They Chose NOT to Do
[Often more revealing than what they built]

## Constraints That Forced Elegance
[Beautiful systems are usually born from constraints]
- Scale constraint: ___
- Time constraint: ___
- Team constraint: ___
- Cost constraint: ___

## How My Pipeline Compares

| Aspect | Their System | My Pipeline | Gap |
|--------|-------------|-------------|-----|
| Feature serving | Pre-computed, cached | Real-time computation | Performance hit |
| Monitoring | Custom metrics, dashboards | Basic Prometheus | Less visibility |
| Deployment | Blue-green, canary | Direct deploy | More risk |

## Three Things I'm Changing in My Pipeline
1. [Specific change based on this study]
2. [Specific change based on this study]
3. [Specific change based on this study]

## ADR: Lessons from [System Name]
[Write formal ADR about what you're adopting and why]
```

---

### 🚦 THE HONEST CHECKPOINT

Answer these honestly. Write them down. Show them to your accountability partner.

```markdown
# Honest Checkpoint

## 1. Can I explain my pipeline's architecture WITHOUT looking at code?
[ ] Yes — I can whiteboard it from memory
[ ] Partially — I remember the flow but not the details
[ ] No — I need to look at the code

## 2. Did the expert feedback SURPRISE me significantly?
[ ] Yes — they found things I never considered
[ ] Somewhat — I knew about some issues but not all
[ ] No — I predicted most of their feedback

## 3. Can I name 3 things I'd do differently WITHOUT referencing notes?
[ ] Yes (list them):
    1. ___
    2. ___
    3. ___
[ ] I can name 1-2
[ ] No

## 4. Has my INTUITION about designs changed, or just my KNOWLEDGE?
[ ] Intuition — I "feel" when something is off before I can articulate why
[ ] Knowledge — I know the rules but apply them mechanically
[ ] Unsure

## 5. When I look at a new pipeline repo, can I predict problems?
[ ] Yes — I can guess 3+ issues before reading the code
[ ] Somewhat — I can guess 1-2 obvious ones
[ ] No — I need to read the code first

## 6. Do I care about this work, or am I just checking boxes?
[ ] Care — I'm excited to keep going
[ ] Neutral — It's fine, educational
[ ] Checking boxes — I'm doing it because I "should"
```

#### Interpreting Your Answers

| Pattern | Diagnosis | Prescription |
|---------|-----------|-------------|
| Yes, No, Yes, Intuition, Yes, Care | You're developing taste. | Keep going. You're on the right track. |
| Partially, Somewhat, 1-2, Knowledge, Somewhat, Neutral | Normal progress. You're learning but not yet intuitive. | Proceed, but slow down. Go deeper on each phase. Consider upgrading to Tier 2/3 community. |
| No, Yes, No, Knowledge, No, Checking boxes | You're completing exercises, not developing taste. | STOP. See Plan B below. |

#### Plan B (If You Scored Poorly)

If you got the third pattern above, this curriculum isn't working for you. **That's okay.**

**Options:**

1. **Rebuild Phase 1 from scratch with different decisions**
   - Pick a different domain (not weather)
   - Make different architectural choices
   - Focus on understanding WHY, not just making it work

2. **Get a job with strong senior engineers**
   - Some people develop taste better through apprenticeship
   - No shame in this — it's often faster and more effective
   - Self-directed learning isn't for everyone

3. **Find a paid mentor for structured 1-on-1 teaching**
   - If you have budget, this accelerates learning
   - More effective than struggling alone

4. **Take a break, come back in 3 months**
   - Sometimes you need distance to consolidate learning
   - Work on other things, let this percolate

5. **Accept you might be a specialist, not a generalist**
   - That's totally fine
   - Focus on getting really good at one thing
   - Depth > breadth for some career paths

> **There is no shame in any of these paths. Recognizing when something isn't working is also taste.**

---

## 🔬 Phase 2: Go Deep (3-4 Weeks)

**Goal:** Go deep on something that hurt you in Phase 1. Surface knowledge → deep understanding → taste.

### Choosing What to Go Deep On

**DO NOT pick from a menu. Instead:**

1. Review your Phase 1B bottleneck log and Phase 1.5 gap analysis
2. Ask: "What broke that I couldn't fully explain?"
3. That's what you go deep on

**Examples of how pain maps to depth:**

| Phase 1 Pain | Go Deep On | Why |
|--------------|-----------|-----|
| "Pandas ran out of memory at 1M rows" | Data processing internals — chunked processing, Arrow/Parquet columnar formats, when to abandon Pandas | You'll stop treating Pandas as a black box |
| "Database queries got slow at scale" | Database internals — indexes, query planning, LSM-trees vs. B-trees, connection pooling | You'll know why things are slow, not just that they're slow |
| "Feature engineering was slow and redundant" | Feature store architecture — online vs. offline stores, computation vs. serving, caching strategies | You'll understand when pre-computation beats real-time |
| "Couldn't figure out if pipeline was healthy" | Observability deep dive — structured logging, distributed tracing, metric design, alert fatigue | You'll design systems that tell you they're sick |
| "Concurrent pipeline runs fought over resources" | Distributed systems fundamentals — locking, consensus, resource isolation, scheduling | You'll understand contention at a fundamental level |

### Depth Options

#### Option A: Database Internals

**Read DDIA Chapters 3-4 deeply**

**Implement a simple storage engine (both LSM-tree and B-tree):**

```python
# LSM-Tree: Write-optimized (append to log, merge periodically)
# B-Tree: Read-optimized (in-place updates, balanced tree)

# Implement both. Benchmark for ML feature storage:
# - Write 1M feature vectors
# - Read random feature vectors
# - Range query (all features for user X between dates)

# When is each better?
```

**Connect to your pipeline:** Which is better for your feature store? Why?

**📦 Deliverable:**
- Working implementations
- Benchmark results
- Decision framework
- Blog post

#### Option B: Stream Processing Deep Dive

Build a streaming feature pipeline alongside your batch pipeline:

```python
# Use Google Pub/Sub or Kafka
# Real-time feature computation from weather sensor stream

# Handle:
# - Late arriving data (weather station reports delayed)
# - Exactly-once semantics (don't double-count)
# - Backpressure (too many events, consumer can't keep up)
# - Out-of-order events (timestamps don't match arrival order)
```

**Compare batch vs. stream:**

| Dimension | Batch | Stream | Winner For This Use Case |
|-----------|-------|--------|-------------------------|
| Latency | Hours | Seconds | Stream if real-time needed |
| Complexity | Low | High | Batch (our use case is daily) |
| Cost | $X | $Y | Batch |
| Correctness | Easier | Harder | Batch |
| Operability | Simpler | Complex | Batch |

**📦 Deliverable:**
- Working streaming pipeline
- Batch vs. stream comparison
- Decision framework
- Blog post

#### Option C: Observability Deep Dive

**Read *Observability Engineering* by Charity Majors (key chapters: 1-4, 7-9)**

**Implement proper observability:**

```python
# Structured logging with correlation IDs
import structlog
import uuid

logger = structlog.get_logger()

@asset
def weather_features(context, raw_data):
    run_id = str(uuid.uuid4())
    logger.info(
        "feature_engineering_started",
        run_id=run_id,
        rows=len(raw_data),
        timestamp=datetime.utcnow().isoformat()
    )
    # ... processing ...
    logger.info(
        "feature_engineering_completed",
        run_id=run_id,
        output_rows=len(result),
        duration_ms=duration
    )

# Custom metrics that actually matter
from prometheus_client import Gauge, Histogram

feature_freshness = Gauge(
    "feature_freshness_hours",
    "How old are the features being served"
)

data_quality_score = Gauge(
    "data_quality_score",
    "Percentage of valid records in batch",
    ["batch_id"]
)
```

**📦 Deliverable:**
- Full observability stack
- Dashboard screenshot
- Alert design document
- Blog post

---

### Depth Validation

**You've gone deep enough when:**

- ✅ You can explain the concept to your accountability partner and answer their follow-up questions
- ✅ You know when the technology is the WRONG choice (not just how to use it)
- ✅ You've written an ADR that captures trade-offs a junior engineer wouldn't see
- ✅ Your Phase 1 pipeline is better because of what you learned
- ✅ You can write a blog post teaching this to others

**You haven't gone deep enough when:**

- ❌ You can recite facts but can't explain trade-offs
- ❌ You followed a tutorial but couldn't modify the approach
- ❌ You don't know when NOT to use the technology
- ❌ You can't explain it without looking at notes

---

## 🛡️ Phase 3: Resilience & Production Hardening (5-6 Weeks)

**Goal:** Make your pipeline survive the chaos of production. Develop operational taste.

### Week 1-2: Resilience Patterns

**Study first:** Read *Release It!* by Michael Nygard, Chapters 4-8

**Understand these patterns:**

| Pattern | What It Does | When to Use | When NOT to Use |
|---------|--------------|-------------|-----------------|
| Circuit breaker | Stops calling a failing dependency | External service calls | Internal function calls |
| Retry with backoff | Retries failed operations with increasing delay | Transient failures (network blips) | Permanent failures (bad input) |
| Timeout | Abandons slow operations | Any external call | CPU-bound computation |
| Fallback | Provides degraded but functional response | When "something" > "nothing" | When wrong answer is worse than no answer |
| Bulkhead | Isolates failures to one component | Multi-tenant or multi-dependency systems | Simple single-path systems |
| Dead letter queue | Captures failed messages for later processing | Async message processing | Synchronous request/response |

> **ADR opportunity:** For each pattern you add, write an ADR explaining why you chose it for that specific location.

### Week 2-3: Implement Resilience

**Add a validation service:**

```python
# validation_service/app.py
from fastapi import FastAPI
from pydantic import BaseModel

app = FastAPI()

class WeatherData(BaseModel):
    temperature: float
    humidity: float
    pressure: float

@app.post("/validate")
def validate_features(data: WeatherData):
    """Validate weather data quality."""
    issues = []
    
    if data.temperature < -90 or data.temperature > 135:
        issues.append(f"Temperature {data.temperature} outside physical range")
    if data.humidity < 0 or data.humidity > 100:
        issues.append(f"Humidity {data.humidity} outside valid range")
    if data.pressure < 870 or data.pressure > 1085:
        issues.append(f"Pressure {data.pressure} outside normal range")
    
    return {"valid": len(issues) == 0, "issues": issues}
```

**Add circuit breaker:**

```python
import pybreaker

# Circuit opens after 5 failures, stays open for 60 seconds
validation_breaker = pybreaker.CircuitBreaker(
    fail_max=5,
    reset_timeout=60
)

@asset
def validated_weather_data(
    context: AssetExecutionContext,
    weather_features: pd.DataFrame
) -> pd.DataFrame:
    """Validate data with circuit breaker and fallback.
    
    Primary: External validation service (richer checks)
    Fallback: Local validation (basic range checks only)
    
    Trade-off accepted: Fallback misses some edge cases,
    but serving partially-validated data is better than
    serving nothing. See ADR-007.
    """
    try:
        result = validation_breaker.call(
            validate_via_service, weather_features
        )
        context.log.info("Validated via service", extra={"rows": len(result)})
        return result
    except pybreaker.CircuitBreakerError:
        context.log.warning(
            "Validation service circuit OPEN — using fallback",
            extra={"rows": len(weather_features)}
        )
        return local_validation_fallback(weather_features)
```

**Add retry with backoff:**

```python
from tenacity import (
    retry, 
    stop_after_attempt, 
    wait_exponential,
    retry_if_exception_type,
    before_sleep_log
)
import logging

logger = logging.getLogger(__name__)

@retry(
    stop=stop_after_attempt(3),
    wait=wait_exponential(multiplier=1, min=4, max=30),
    retry=retry_if_exception_type((ConnectionError, TimeoutError)),
    before_sleep=before_sleep_log(logger, logging.WARNING)
)
def fetch_weather_data(api_key: str) -> pd.DataFrame:
    """Fetch weather data with retry.
    
    Only retries on transient network errors.
    Does NOT retry on 4xx errors (bad request = our bug, not transient).
    
    Exponential backoff: 4s, 8s, 16s (capped at 30s)
    """
    response = requests.get(
        WEATHER_API_URL,
        params={"appid": api_key},
        timeout=10
    )
    response.raise_for_status()
    return pd.DataFrame(response.json()["data"])
```

### Week 3-4: Chaos Engineering

**Set up Toxiproxy:**

```bash
docker run -d --name toxiproxy \
  -p 8474:8474 \
  -p 20000-20010:20000-20010 \
  ghcr.io/shopify/toxiproxy
```

**Inject failures systematically:**

```bash
# Test 1: Slow dependency (5-second latency on validation service)
toxiproxy-cli create validation -l 0.0.0.0:20000 -u validation-service:8000
toxiproxy-cli toxic add validation -t latency -a latency=5000

# Expected: Circuit breaker opens after 5 timeouts, fallback kicks in
# Actual: ___________

# Test 2: Flaky dependency (50% packet loss)
toxiproxy-cli toxic add validation -t limit_data -a bytes=500

# Test 3: Total outage
toxiproxy-cli toxic add validation -t timeout -a timeout=0

# Test 4: Slow database
# Add latency to your database connection
```

**Document results:**

| Failure Injected | Expected Behavior | Actual Behavior | Matched? | Fix Needed |
|-----------------|-------------------|-----------------|----------|------------|
| 5s latency | Circuit opens after 5 fails | | ✓/✗ | |
| 50% packet loss | Retries succeed | | ✓/✗ | |
| Total outage | 100% fallback | | ✓/✗ | |
| Slow database | Graceful timeout | | ✓/✗ | |

### Week 5: Resource & Cost Awareness

**🔧 VPS Cost Analysis:**

```markdown
# VPS Cost Analysis

**Monthly Fixed Costs:**
- VPS: $10/month (Hetzner CPX11)
- Domain: $1/month (amortized)
- SSL: $0 (Let's Encrypt)
- **Total: $11/month**

**Resource Usage:**
- CPU: Average ___%, Peak ___%
- RAM: Average ___GB, Peak ___GB
- Disk: ___GB used of 40GB
- Network: ___GB egress/month

**Scale Decision Point:**
- Current: 2GB RAM, 1 vCPU
- Next tier: 4GB RAM, 2 vCPU = $20/month
- **Upgrade when:** RAM consistently > 80% or CPU > 70%
```

### Week 6: Blind Incident Drill

**The 2 AM Test.**

Have your accountability partner inject a failure:
- They choose what breaks
- You don't know what it is
- You can only use logs, metrics, and dashboards to find it

**Time yourself:**
- Detection time: ___
- Diagnosis time: ___
- Mitigation time: ___
- Total: ___

**Write post-mortem:**

```markdown
# Incident Report

**Date:** ___
**Duration:** Detection at T+___, Mitigated at T+___

## What Happened
[Describe what you observed]

## Timeline
- T+0: [First signal]
- T+5: [Initial investigation]
- T+10: [Hypothesis formed]
- T+20: [Root cause identified]
- T+25: [Mitigation applied]

## Root Cause
[What actually broke]

## What Slowed Me Down
- Missing observability: ___
- Wrong hypothesis: ___
- Debugging dead ends: ___

## Prevention
[What I'm adding to prevent/detect this faster next time]

## Taste Lesson
[What does this teach me about system design?]
```

### 📦 Deliverable Phase 3

- [ ] Pipeline with resilience patterns (circuit breaker, retry, timeout, fallback)
- [ ] Chaos test results documented
- [ ] Resource usage analysis and optimization
- [ ] Resource monitoring and alerts implemented
- [ ] Blind incident post-mortem
- [ ] ADRs for each resilience decision
- [ ] Updated Grafana dashboards
- [ ] Blog post: "Making my ML pipeline resilient"

---

## 💼 Phase 4: Business Context & Product Thinking (2-3 Weeks)

**Goal:** Technical taste without business taste is incomplete. Learn to make build/don't-build decisions.

### Week 1: Business Fundamentals

**Read *The Mom Test* by Rob Fitzpatrick** (short book, 2-3 days)

**Key lesson:** People will lie to be nice. Ask about their behavior, not their opinions.

**Examples of bad questions:**
- "Would you use this?"
- "Is this a good idea?"
- "Would you pay $X?"

**Examples of good questions:**
- "How do you currently solve this?"
- "What did this problem cost you last month?"

**Learn to calculate unit economics:**

```markdown
# Unit Economics Basics

**🔧 VPS Economics:**
- Compute: $0 (included in $10/month flat fee)
- Storage: $0 (included, until disk full)
- API calls: $0.0001 per weather API call
- Total cost per prediction: ~$0.0001

**At scale:**
- 1M predictions/month = $100 API costs + $10 VPS = $110/month
- Cost per prediction: $0.00011
- **Fixed infrastructure cost is your friend**

**Revenue per prediction:**
- Pricing: $___ per prediction
- Or: $___ per month subscription / ___ predictions = $___ per prediction

**Margin:**
- VPS margin per prediction: Revenue - $0.00011 = $___
- Margin %: (Margin / Revenue) x 100 = ___%

**LTV (Lifetime Value):**
- Average customer lifespan: ___ months
- Revenue per month: $___
- Total LTV: ___ months x $___ = $___

**CAC (Customer Acquisition Cost):**
- Marketing spend per month: $___
- New customers per month: ___
- CAC: $___ / ___ = $___ per customer

**Payback period:**
- CAC / Monthly revenue per customer = ___ months
- (Want this < 12 months for healthy business)
```

### Week 2: The Pivot Decision

Your weather pipeline exists. Now ask: should it?

**Step 1: Identify potential users (pick 3 domains)**

| Domain | User Persona | Problem They Have | How Weather Prediction Helps | Existing Solutions |
|--------|-------------|-------------------|----------------------------|-------------------|
| Agriculture | Farm manager | Crop planning, frost risk | Reduce crop loss by X% | Weather.com, NOAA, local knowledge |
| Events | Event planner | Outdoor event decisions | Avoid rain cancellations | Weather.com, gut feeling |
| Logistics | Delivery company | Route optimization | Avoid weather delays | In-house, weather APIs |
| Energy | Solar farm operator | Solar forecasting | Better capacity planning | Expensive enterprise solutions |

**Step 2: Interview 3 potential users**

**Find them:**
- Reddit communities (r/farming, r/events, etc.)
- LinkedIn (search for job titles)
- Local businesses (cold email)
- Your network

**Mom Test questions:**

1. "Walk me through the last time weather disrupted your [operations/event/etc.]"
2. "How do you currently make weather-related decisions?"
3. "What did weather uncertainty cost you last year?"
4. "If you could wave a magic wand, how would weather forecasting be different?"
5. "Have you tried other weather tools? What happened?"

**Document findings:**

| User | Domain | Current Solution | Real Pain? | Pain Level (1-10) | Willing to Switch? | Notes |
|------|--------|-----------------|-----------|------------------|-------------------|-------|
| | | | | | | |

**Step 3: The Build/Don't Build Decision**

```markdown
# Decision: Should This Product Exist?

## Evidence Assessment

**Supports building:**
- [evidence from interviews]

**Against building:**
- [evidence from interviews]

## Unit Economics Reality Check

**Cost per prediction:** $___
**What users would pay:** $___
**At break-even, need:** ___ users

## Decision

[ ] BUILD — because: ___
[ ] PIVOT — to: ___ because: ___
[ ] KILL — because: ___

## If PIVOT: What Domain Instead?

**Based on user interviews:**
[What domain has more pain and fewer solutions?]

**New direction:**
[Describe the pivot]

**What changes in the architecture:**
[What stays, what changes]

**ADR: Pivot Decision**
```

### Week 3: Implement the Pivot (If You Pivoted)

```markdown
# Pivot Implementation Plan

**What stays the same:**
- Dagster orchestration
- MLflow tracking
- FastAPI serving
- Prometheus monitoring

**What changes:**
- Data source: [old] → [new]
- Features: [old] → [new]
- Model: [old] → [new]
- Output: [old] → [new]

**Success metric:**
At least 1 real user says "this is useful" or "I'd pay for this"
```

### 📦 Deliverable Phase 4

- [ ] User interview notes (3 interviews, Mom Test format)
- [ ] Build/pivot/kill decision with evidence
- [ ] Unit economics analysis
- [ ] If pivoted: Updated pipeline for new domain
- [ ] If pivoted: Tested with at least 1 real user
- [ ] ADR for the business decision
- [ ] Blog post: "Why I pivoted from X to Y"

---

## 🤖 Phase 5: AI Oversight & Verification (3-4 Weeks)

**Goal:** Learn to work WITH LLMs effectively — including knowing when they're wrong.

### Week 1: Understanding LLM Strengths and Failure Modes

**This is NOT "find bugs in LLM code." It's developing judgment for when and how to use LLMs.**

#### Exercise 1: Decomposition Judgment

Take a real task from your pipeline and try three approaches:

```markdown
# Task: Add data quality monitoring to the feature pipeline

## Approach A: Ask LLM to do everything at once

**Prompt:**
"Write a complete data quality monitoring system for my ML pipeline..."

**Result:**
[Paste what LLM generated]

**Quality: ___/10**

## Approach B: Decompose into pieces

**Prompt 1:** "What are the most important data quality checks for an ML feature pipeline?"
**Prompt 2:** "Write a function that detects feature drift using KL divergence."
**Prompt 3:** "Write Prometheus metrics for tracking data quality over time."

**Result:**
[Paste what LLM generated]

**Quality: ___/10**

## Approach C: Use LLM for research, write it yourself

**Prompt:** "What are common data quality issues in ML pipelines..."

**Then:** Write the implementation yourself using the research.

**Quality: ___/10**

## Judgment: Which approach worked best for this task? Why?

**Winner:** Approach ___

**Pattern I notice:**
- LLMs are good at: ___
- LLMs struggle with: ___
```

#### Exercise 2: Trust Calibration

For 10 different tasks, predict how much you'd trust LLM output, then test:

| Task | Predicted Trust (L/M/H) | Actual Result | Trust Justified? | Why/Why Not |
|------|------------------------|---------------|------------------|-------------|
| Boilerplate FastAPI endpoint | High | | | |
| Data validation logic | Medium | | | |
| Distributed system design | Low | | | |
| SQL query optimization | Medium | | | |
| Error handling strategy | Low | | | |
| Test generation | Medium | | | |
| Dockerfile creation | High | | | |
| Retry/backoff tuning | Low | | | |
| Documentation writing | High | | | |
| Architecture decisions | Very Low | | | |

**Pattern I Found:**

```markdown
**LLMs are trustworthy for:**
- Well-documented patterns (FastAPI, Docker)
- Syntax and boilerplate
- Research and summarization

**LLMs are dangerous for:**
- Context-specific decisions (retry tuning, architecture)
- Edge cases and failure modes
- Domain-specific logic
- Anything requiring operational experience

**My decision framework:**
- Use LLM for: ___
- Always verify: ___
- Never trust for: ___
```

### Week 2: Property-Based Testing for LLM Code

**Exercise: Find What LLMs Miss**

1. Ask an LLM to write data processing code
2. Write property-based tests

```python
import hypothesis.strategies as st
from hypothesis import given, assume, settings
import pandas as pd
import numpy as np

# Generate realistic weather data with edge cases
weather_data = st.fixed_dictionaries({
    "temperature": st.lists(
        st.one_of(
            st.floats(-50, 150),  # Normal range
            st.just(np.nan),      # Missing values
            st.floats(1000, 2000) # Outliers
        ),
        min_size=10,
        max_size=100
    )
})

@given(data=weather_data)
@settings(max_examples=200)
def test_no_nan_in_output(data):
    """Output should never contain NaN."""
    df = pd.DataFrame(data)
    assume(len(df.dropna()) > 0)
    
    result = llm_process_weather_data(df)
    assert not result.isnull().any().any(), "Found NaN in output"

# Edge cases LLMs typically miss:
def test_all_same_values():
    """When all values identical, normalization shouldn't crash."""
    df = pd.DataFrame({"temperature": [72.0] * 10})
    result = llm_process_weather_data(df)
    assert len(result) > 0
```

3. Document bugs found:

```markdown
# LLM Bug Patterns Found

## Bug 1: Forward-fill on first row
- **Input:** First row has NaN
- **What happens:** First row still has NaN
- **Why LLM missed it:** Didn't think about edge case
- **Category:** Edge case

## Pattern Summary

**LLMs consistently miss:**
- Edge cases (empty data, single row, all NaN)
- First/last element handling
- Division by zero scenarios
- Pathological inputs

**LLMs are good at:**
- Happy path implementation
- Standard library usage
- Code structure
```

### Week 3: Architectural Hallucination Detection

**Exercise: Evaluate LLM System Design**

**Prompt:**
```
Design architecture for real-time ML prediction system:
- 10K IoT devices sending 1 reading/second each
- Extract features, run predictions, store results, serve via API
```

**Evaluate using taste rubric:**

| Component | LLM Proposed | Taste Smell | Rating | Issue | Better Approach |
|-----------|-------------|-------------|--------|-------|-----------------|
| Data ingestion | | | | | |
| Processing | | | | | |
| Feature computation | | | | | |
| Model serving | | | | | |
| Storage | | | | | |

### Week 4: Code Review Practice

Review 15 PRs on ML infrastructure repos:
- Dagster PRs
- MLflow PRs
- Great Expectations PRs

For each PR, write 1-sentence review BEFORE reading other comments:

```markdown
# PR Review Log

## PR #1234: "Add retry logic to model registry"
**My take (before reading reviews):** Missing exponential backoff
**Actual reviews said:** [compare after reading]
**Did I catch it?** Yes/No
**What I missed:** ___

## Accuracy Over Time
| PRs 1-5 | PRs 6-10 | PRs 11-15 |
|---------|----------|-----------|
| Caught ___/5 | Caught ___/5 | Caught ___/5 |

**Am I getting better?** Yes/No
**Evidence:** ___
```

### 📦 Deliverable Phase 5

- [ ] LLM decomposition and trust calibration analysis
- [ ] Property-based test suite catching 5+ edge cases in LLM code
- [ ] Architectural review of LLM-generated system design
- [ ] Model monitoring review (MLOps-specific)
- [ ] PR review accuracy log (15 PRs)
- [ ] Blog post: "What LLMs get wrong about ML infrastructure"

---

## 🎓 Phase 6: The Capstone — Real Constraints (2-3 Weeks)

**Goal:** Synthesize everything under realistic pressure. This uses a DIFFERENT system — because in real careers, you inherit other people's code.

### Setup: The Inherited System

Create a deliberately flawed ML pipeline (or have your cohort member create one):

```markdown
# The Inherited System

**Scenario:** You're the new founding engineer at a startup. Day 1, you inherit:

- A partially-working recommendation pipeline (NOT weather — something new)
- Built by a contractor who's now gone
- No monitoring
- Intermittent data corruption
- Works on laptop, crashes in prod after 30 minutes
- No tests, no documentation
- CEO says: "Demo to investors in 2 weeks"
- $50K in bank, 3 months runway
```

### Week 1: Triage Under Constraints

You have 2 weeks, limited money, and a demo to deliver.

```markdown
# Triage Decision

## System Assessment (spend 4 hours max)

| Component | Status | Severity (1-10) | Fix Time | Blocks Demo? |
|-----------|--------|----------------|----------|--------------|
| Data ingestion | | | | |
| Feature engineering | | | | |
| Model training | | | | |
| Model serving | | | | |

## Triage Matrix

| Issue | Blocks Demo? | Fix Time | Fix Now? | Rationale |
|-------|-------------|----------|----------|-----------|
| | | | | |

## What I'm Choosing NOT to Fix (and why)

1. ___ — because ___
2. ___ — because ___

**ADR: Triage Decisions Under Time Constraint**
```

### Week 2: Ship Under Pressure

Build the minimum demo-able product:

```markdown
# Sprint Plan (10 working days)

## Days 1-3: Fix blockers
- Fix: ___
- Fix: ___
- Test: Manual only (no time for automated)

## Days 4-7: Build demo flow
- Minimum UI (Streamlit or simple frontend)
- Happy path only
- Prepare backup data for when live demo fails

## Days 8-10: Polish and practice
- Demo script (exact clicks, exact words)
- Rehearse 5 times
- Failure recovery plan

## What "Good Enough" Means Here

**For demo:**
- Works for 10 minutes straight
- Handles 1 user
- Looks professional

**For production:**
- Works for 24 hours
- Handles 100 users
- Actually tested

**This gap is the price of speed.**
```

### Week 3: Post-Funding Reality

Scenario: You got funded! $2M seed round. But...

```markdown
# The Aftermath

## Problem: Demo code is now "production"
- Users are signing up
- CEO hired salespeople
- Can't stop the business to refactor

## Refactor Strategy (Expand-Contract Pattern)

### Phase 1: Build new alongside old (Week 1-2)
- Build proper version with tests, monitoring
- Dual-write to both systems
- Users still on old system

### Phase 2: Gradual migration (Week 3-4)
- 10% of users route to new system
- Monitor error rates, latency, accuracy
- Rollback ready: Can switch back in 1 minute

### Phase 3: Increase to 50% (Week 5)
- If 10% went well, route half to new
- Monitor comparative metrics

### Phase 4: Full migration (Week 6)
- 100% on new system
- Keep old running for 1 week (safety)
- Decomm old after 1 week stable

## The Hiring Decision

**You can hire ONE person. Who?**

| Role | What They'd Do | Bottleneck They'd Fix | Why Not? |
|------|---------------|----------------------|----------|
| Backend eng | Ship features faster | Speed | |
| ML engineer | Better models | Accuracy | |
| SRE | Improve reliability | Stability | |
| Data engineer | Fix data quality | Data quality | |

**Decision:** Hire ___ because current bottleneck is ___.

**ADR: First Hire Decision**
```

### 📦 Deliverable Phase 6

- [ ] Triage document with rationale
- [ ] Demo sprint plan (what you actually delivered)
- [ ] Refactor strategy (expand-contract)
- [ ] Hiring decision analysis
- [ ] Reflection: "What did constraints teach me about taste?"
- [ ] Final ADR count: ___ (target: 15-25 total)
- [ ] Blog post: "What I learned building under constraints"

---

## 📅 Monthly Practices (Throughout All Phases)

### Monthly Taste Calibration: Blind Architecture Review

**Do this once per month, starting after Phase 1A.**

1. **Find 3 ML pipeline repos on GitHub**
   - Search: "ML pipeline" or "MLOps" or "feature pipeline"

2. **Before reading code, predict (10 minutes per repo):**

```markdown
# Blind Review #___ : [Repo Name]
**Date:** ___
**Based on README and architecture diagram ONLY**

## Taste Smells I Predict

- [ ] Hidden coupling: Where? ___
- [ ] Implicit assumptions: Where? ___
- [ ] Proportionality violations: Where? ___
- [ ] Time bombs: Where? ___
- [ ] Operational blindness: Where? ___

## Specific Predictions

**What breaks first at 10x scale:** ___
**Confidence:** Low / Medium / High

**Ugliest part:** ___
**Confidence:** Low / Medium / High

**Architecture rating:** ___/10
**Main reason for score:** ___
```

3. **Read issues, PRs, and discussions**

4. **Compare predictions to reality:**

```markdown
# Reality Check

**What actually broke (from issues):** ___
**Did I predict it?** Yes / No
**If no, why did I miss it?** ___

## Score This Review

| Category | Predicted Correctly? | Points |
|----------|---------------------|--------|
| What breaks at scale | Yes/No | 0 or 3 |
| Ugliest part | Yes/No | 0 or 3 |
| Hidden coupling | Yes/No | 0 or 1 |
| Time bombs | Yes/No | 0 or 1 |
| **Total** | | **/ 10** |
```

5. **Track month-over-month:**

| Month | Repos Reviewed | Avg Score | Biggest Blind Spot | Progress Note |
|-------|---------------|-----------|-------------------|---------------|
| 1 | 3 | /10 | | |
| 2 | 3 | /10 | | |
| 3 | 3 | /10 | | |

**Target: 70%+ by month 6**

---

### The 6-Month Return

**Do this 1 month after completing Phase 3.**

```markdown
# Maintainability Self-Review

**Instructions:** Wait 1 month, then return to your Phase 1A code cold.

## The Test

1. Don't review code beforehand
2. Try to add a feature (e.g., add a second model, add a new data source)
3. Fix a bug you intentionally introduce
4. Time yourself

## Results

**Time to understand code flow:** ___ minutes

**Could I add feature successfully?** Yes / No

**If no, what blocked me?** ___

## What "Past Me" Did That "Maintenance Me" Hates

1. ___
2. ___
3. ___

## What "Past Me" Did Right

1. ___
2. ___

## If I Could Send One Message to "Past Me"

___

**This teaches: The gap between "works now" and "maintainable."**
```

---

## 🎯 Final Thoughts

> **Remember:** The goal is not to complete the curriculum. The goal is to develop taste — the judgment that survives disruption.

**Signs you're succeeding:**

- ✅ You spot design problems before building
- ✅ You can predict where systems will break
- ✅ You know when NOT to use a technology
- ✅ You make trade-offs consciously, not accidentally
- ✅ Your intuition aligns with expert feedback

**This curriculum is a map, not the territory.**

Adapt it. Skip parts that don't serve you. Go deeper where you need to. The point is developing judgment, not checking boxes.

**Good luck. Build something beautiful.**

---

## 📚 Resources

### Books
- *Designing Data-Intensive Applications* by Martin Kleppmann
- *Release It!* by Michael Nygard
- *Observability Engineering* by Charity Majors
- *The Mom Test* by Rob Fitzpatrick

### Communities
- [MLOps Community Slack](https://mlops.community/)
- [r/MLOps](https://reddit.com/r/mlops)
- [r/ExperiencedDevs](https://reddit.com/r/ExperiencedDevs)

### Platforms
- [Hetzner](https://www.hetzner.com/cloud) - VPS hosting
- [DigitalOcean](https://www.digitalocean.com/) - VPS hosting
- [ADPList](https://adplist.org) - Find mentors

### Tools
- [Dagster](https://dagster.io/) - Orchestration
- [MLflow](https://mlflow.org/) - ML tracking
- [MinIO](https://min.io/) - S3-compatible storage
- [Prometheus](https://prometheus.io/) - Monitoring
- [Grafana](https://grafana.com/) - Visualization

---

## 📝 License

This curriculum is open source. Use it, adapt it, share it.

**Attribution appreciated but not required.**

---

## 🙏 Acknowledgments

Inspired by:
- Chris Paik's ["Software is Dead" article](https://docs.google.com/document/d/103cGe8qixC7ZzFsRu5Ww2VEW5YgH9zQaiaqbBsZ1lcc/)
- ExtremeWeatherBench's [Job Post](https://www.brightband.com/company/careers/software-engineer)
- Boris (Claude Code creator) [(via Addy Osmany's tweet) on judgment over implementation](https://x.com/addyosmani/status/2022822356050399673)
- Paul Graham on [taste](https://paulgraham.com/taste.html)

---

**Version 3.1** | Updated 2025 | VPS-First Edition