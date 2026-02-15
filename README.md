# 🚀 MLOps Engineering Judgment Curriculum v3.1

## Developing Real Taste Through ML Infrastructure — Constraint-First Edition

**Core Thesis:** When LLMs commoditize code implementation, the valuable skill becomes *taste*—knowing what to build, why it's ugly, and how to make it beautiful.

**Version:** 3.1 (VPS Edition)  
**Updated:** 2025

**What Changed in v3.1:**
- **Added VPS-first approach:** Build on bare metal, not managed services
- **Constraint-driven learning:** CPU/memory limits teach systems thinking
- **Predictable costs:** $10/month VPS instead of surprise cloud bills
- **Linux mastery required:** No abstraction layers hiding complexity
- Restructured community requirement as gradient, not gate
- Split Phase 1 into Build + Scale with reflection point
- Defined "ugly" concretely with a taste rubric
- Added Architecture Decision Records throughout
- Focus on self-hosted infrastructure

---

## Infrastructure Choice: Why VPS?

**This curriculum uses VPS (Virtual Private Server) exclusively.**

**VPS forces you to confront real infrastructure:**

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

**VPS teaches systems thinking from the ground up.**

**Constraint builds taste.**

**Why VPS for this curriculum:**
- **Cost:** $5-12/month flat, predictable (no surprise bills)
- **What you learn:** Systems thinking, Linux, resource constraints, how things actually work
- **Stack:** Self-hosted everything (Dagster, PostgreSQL, MinIO, MLflow)
- **Philosophy:** Learn under constraints → understand trade-offs → make better decisions

**Master VPS first. Everything else is just different tooling for the same problems.**

---

## Why This Curriculum Exists (Read This First)

**The world is shifting:** - 2020: "Can you write React?" = employable -
2025: LLMs write React competently - 2028: "Can you write React?" =
table stakes, not differentiator

**Three data points:** 1. **Boris** (created Claude Code): "The
bottleneck was always judgment, taste, and systems thinking. AI just
made that more obvious." 2. **Paul Graham** (2002): "The recipe for
great work is: very exacting taste, plus the ability to gratify it." 3.
**Job market**: Staff+ engineers are hired for judgment, not typing
speed

**LLMs are solving "ability to gratify it" (implementation).** **What
remains: Developing taste (judgment).**

**This curriculum teaches taste.**

If you just want to learn Dagster syntax, take a tutorial. If you want
to develop the judgment that survives AI disruption, do this.

------------------------------------------------------------------------

## Before You Commit: The Honest Trade-offs

**This curriculum costs 8-12 months of focused time.**

### What you're NOT doing in those 8-12 months:

-   Getting promoted to senior (immediate \$30-50K raise)
-   Interviewing for FAANG (\$50-100K+ raise)
-   Building a revenue-generating product
-   Deepening specialization in your current domain

### Opportunity cost is real

-   6 months delayed promotion = \$15-25K lost
-   This compounds over your career
-   Be honest: can you afford to optimize for 5 years out vs. 1 year
    out?

### This makes sense if:

-   Your current job has no senior engineers (self-teaching anyway)
-   Your job is coasting (not learning much)
-   You have conviction the AI thesis is right
-   You can afford long-term optimization
-   You want to be a founding engineer/CTO someday

### This does NOT make sense if:

-   You need a raise in the next 12 months
-   You have great mentors at current job
-   You're optimizing for immediate job market
-   You don't actually believe LLMs will commoditize coding
-   You prefer specialization over breadth

**Be honest about which camp you're in.**

------------------------------------------------------------------------

## The Three Agreements

Before anything else, agree to these. They override every checklist in
this document.

**1. Taste over completion** "I will not just check boxes. I will
develop the judgment to spot ugly designs. If I'm completing exercises
without my thinking changing, I will stop and go deeper."

**2. Feedback over isolation** "I will get my work reviewed by others. I
will calibrate my taste against theirs. I will not hide my work until
it's 'ready.'"

**3. Depth over breadth** "I will go deep enough to develop intuition,
not just surface knowledge. I'd rather truly understand one system than
superficially touch ten."

**Sign this (seriously):** I, \_\_\_\_\_\_\_\_\_\_\_\_, commit to:

Stopping if I'm checking boxes without my thinking changing Getting
expert feedback even when my work feels "not ready yet" Going deeper
rather than moving on when I don't understand Being honest about
opportunity costs and whether this is right for me Date:
\_\_\_\_\_\_\_\_\_\_\_\_ Share with accountability partner: Yes / No

------------------------------------------------------------------------

## The Taste Vocabulary

**You can't develop taste without a language for it.** Use this rubric
throughout the curriculum.

### What "Ugly" Means (Concretely)

An architecture is ugly when it has:

  ------------------------------------------------------------------------
  Smell               Definition                   Example
  ------------------- ---------------------------- -----------------------
  **Hidden coupling** Components that seem         Feature engineering and
                      independent but fail         model serving share a
                      together                     database connection
                                                   pool

  **Implicit          Works on the author's        Hardcoded file paths,
  assumptions**       machine, breaks elsewhere    assumes unlimited
                                                   memory

  **Proportionality   Complex solutions to simple  Kubernetes for a
  violations**        problems (or vice versa)     single-user app; no
                                                   retry logic for a
                                                   distributed system

  **Time bombs**      Works today, guaranteed to   Loading all data into
                      break at 10x                 memory, unbounded
                                                   queries

  **Operational       No way to know if it's       No metrics, no
  blindness**         healthy without reading code structured logs, no
                                                   alerts

  **Cargo culting**   Using tools because "that's  Kafka for 100
                      what you do"                 events/day;
                                                   microservices for a
                                                   2-person team

  **Cleverness over   Optimized for writing, not   Nested comprehensions,
  clarity**           reading                      magic numbers, no
                                                   comments on "why"
  ------------------------------------------------------------------------

**When reviewing any system (yours or others), name the smells.**

### What "Beautiful" Means (Concretely)

An architecture is beautiful when it has:

  ------------------------------------------------------------------------
  Quality                Definition                 Example
  ---------------------- -------------------------- ----------------------
  **Proportional         Complexity matches the     Simple pipeline for
  complexity**           problem's difficulty       simple data;
                                                    distributed system
                                                    only when needed

  **Explicit             Decisions are documented   "We chose eventual
  trade-offs**           with rationale             consistency because
                                                    latency matters more
                                                    than perfect accuracy
                                                    here"

  **Graceful             Fails partially, not       Serves cached
  degradation**          totally                    predictions when model
                                                    is down

  **Observable by        You can understand system  Dashboards, structured
  default**              health from outside        logs, meaningful
                                                    alerts

  **Deletable parts**    Components can be removed  Loose coupling, clear
                         without cascading failures interfaces

  **Obvious flow**       A new engineer can follow  Clear naming, linear
                         the data path in 5 minutes pipeline, documented
                                                    entry points
  ------------------------------------------------------------------------

------------------------------------------------------------------------

## Timeline Overview (Honest Estimates)

  ----------------------------------------------------------------------------
  Phase         Duration        Weekly Hours          What You Build
  ------------- --------------- --------------------- ------------------------
  Phase 0:      1-2 weeks       8-10 hrs              Your support network
  Setup &                                             
  Community                                           

  Phase 1A:     5-6 weeks       15-20 hrs             Working ML pipeline
  Build                                               

  Phase 1B:     4-5 weeks       15-20 hrs             Scaling report + cost
  Scale & Break                                       analysis

  Phase 1.5:    2-3 weeks       10 hrs                Gap analysis + honest
  Taste                                               checkpoint
  Calibration                                         

  Phase 2: Go   3-4 weeks       15-20 hrs             Deep expertise pulled by
  Deep                                                pain

  Phase 3:      5-6 weeks       15-20 hrs             Production-hardened
  Resilience                                          pipeline

  Phase 4:      2-3 weeks       10 hrs                Pivot decision + user
  Business                                            research
  Context                                             

  Phase 5: AI   3-4 weeks       10-15 hrs             LLM verification skills
  Oversight                                           

  Phase 6:      2-3 weeks       15-20 hrs             Real-world constraints
  Capstone                                            

  **Total**     **28-38 weeks** **Intense**           **Portfolio + Judgment**
  ----------------------------------------------------------------------------

**Sustainable alternative:** 12-15 months at 10 hrs/week

**Buffer for life:** Add 20%. Real estimate: **34-46 weeks intensive**
or **14-18 months sustainable**.

### What "15-20 hrs/week intensive" Actually Means

**Planned time:** - Coding/building: 10-15 hrs - Reading: 5-7 hrs -
Total: 15-22 hrs

**Unplanned time (that always happens):** - Debugging "why won't Docker
start": 3-5 hrs/week - Re-reading chapters that didn't stick: 2-3
hrs/week - Cohort coordination: 1-2 hrs/week - **Actual total: 21-32
hrs/week**

**If you work full-time:** - Work: 40 hrs - Curriculum: 25-30 hrs -
Total: 65-70 hr weeks

**This is not sustainable for 9 months.**

**Realistic for full-time workers: 10 hrs/week = 18-24 months.**

These estimates do NOT include monthly taste calibrations (\~4-6 hrs
each) or the 6-month return exercise. Budget those separately.

------------------------------------------------------------------------

## Phase 0: Setup & Community (1-2 Weeks)

**Goal:** Set up your environment and your feedback network. Neither is
optional.

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

**If you have a preferred stack, use it. The stack is not the point.**

### Community: A Gradient, Not a Gate

You need feedback to develop taste. But "find 5 people for a 9-month
commitment" is unrealistic advice. Instead, aim for the highest tier you
can sustain:

#### Tier 1: Minimum Viable (REQUIRED)

-   [ ] **Work in public.** Create a GitHub repo for this curriculum.
    Commit weekly.
-   [ ] **Write as you learn.** Start a blog, dev.to, or even a
    Twitter/X thread series documenting your journey. Writing forces
    articulation, which forces clarity.
-   [ ] **Engage in 2-3 communities weekly:**
    -   [MLOps Community Slack](https://mlops.community/)
    -   [r/MLOps](https://reddit.com/r/mlops)
    -   [r/ExperiencedDevs](https://reddit.com/r/ExperiencedDevs)
    -   Answer questions, ask questions, share what you're building

**Why this works even solo:** Public work attracts feedback. People
comment on repos, blog posts get responses, Slack messages start
conversations. You're creating surface area for feedback without
depending on anyone's commitment.

#### Tier 2: Good (AIM FOR THIS)

Everything in Tier 1, plus:

-   [ ] **Find 1 accountability partner.** One person is sustainable. 5
    is a project management nightmare.
    -   Post: "Starting an MLOps learning curriculum. Looking for 1
        partner for bi-weekly code reviews and architecture discussions.
        \~1 hour every 2 weeks."
    -   Try: MLOps Slack, dev Discord servers, local meetups, coworkers
-   [ ] **Bi-weekly code review exchange.** You review theirs, they
    review yours.

#### Tier 3: Great (IF YOU CAN)

Everything in Tier 2, plus ONE of:

-   [ ] **Full cohort (3-5 people)** with weekly syncs
    -   If you can make this happen, it's the highest-value option
    -   Set rules: Miss two syncs = you're out
    -   Demo days at end of each major phase
-   [ ] **Active open source contribution** to Dagster, MLflow, or Feast
    -   Realistic timeline: 1 contribution in first month (docs or small
        bug fix)
    -   Goal: See how maintainers think about design in PR reviews
    -   Don't force this into 1-2 weeks --- let it happen alongside
        Phase 1
-   [ ] **Monthly mentor check-in** with a staff+ ML/infrastructure
    engineer
    -   Use [ADPList](https://adplist.org), cold email, or your network
    -   Be specific: "Can I get 30 minutes monthly to review my
        architecture decisions?"
    -   Expect a 5-10% response rate on cold outreach --- send 20-30
        messages

**Key point:** Start at Tier 1 immediately. Upgrade to Tier 2-3 as
opportunities arise. Don't wait for the perfect community to begin.

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

**You must be able to:**
- [ ] SSH into your server
- [ ] Deploy a Docker container
- [ ] Restart services with systemd
- [ ] Read logs via `journalctl`
- [ ] Configure Nginx reverse proxy
- [ ] View Prometheus metrics
- [ ] Access Grafana dashboards

**If this is painful — good. That's learning.**

---



---

### Architecture Decision Record (ADR) Practice

Start this now. Use it throughout every phase.

Create a `decisions/` folder in your repo. For every significant choice,
write:

``` markdown
# ADR-001: Choosing Dagster Over Airflow

## Status: Accepted

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

You will write 15-25 ADRs over this curriculum. They are your taste
development journal.

------------------------------------------------------------------------

## Create Your Progress Tracker

### My Curriculum Progress

**Start Date:** \_\_\_\_\_\_\_\_\_\_\_ **Community Tier:** 1 / 2 / 3
**Accountability Partner:** \_\_\_\_\_\_\_\_\_\_\_ (or "Working in
public at: \[URL\]")

### Phase Completion

-   [ ] Phase 0: Setup (Target: \_\_\_ )
-   [ ] Phase 1A: Build (Target: \_\_\_ )
-   [ ] Phase 1B: Scale (Target: \_\_\_ )
-   [ ] Phase 1.5: Calibration (Target: \_\_\_ )
-   [ ] Phase 2: Depth (Target: \_\_\_ )
-   [ ] Phase 3: Resilience (Target: \_\_\_ )
-   [ ] Phase 4: Business (Target: \_\_\_ )
-   [ ] Phase 5: AI Oversight (Target: \_\_\_ )
-   [ ] Phase 6: Capstone (Target: \_\_\_ )

### ADR Count: \_\_\_

### Blog Posts Published: \_\_\_

### Architecture Reviews Given: \_\_\_

### Architecture Reviews Received: \_\_\_

#### Monthly Reflection (Answer end of each month)

1.  What surprised me this month?
2.  What failure taught me the most?
3.  Name one "ugly" smell I can now spot that I couldn't before.
4.  What would I do differently on my last project?
5.  Am I developing *intuition* or just *knowledge*?

------------------------------------------------------------------------

## Community Health Check

Add this to the end of each phase:

### Community Check (End of Phase \_\_\_)

-   [ ] Tier 1: Have I posted work publicly? Getting any engagement?
-   [ ] Can I upgrade to Tier 2? (If not, why? Do I need to be more
    active?)
-   [ ] If solo still: Is isolation hurting my learning? Evidence:
    \_\_\_
-   [ ] Have I gotten feedback from at least 1 other person this phase?

------------------------------------------------------------------------

## Phase 1A: Build a Working ML Pipeline (5-6 Weeks)

**Goal:** Build a complete ML pipeline from scratch AND develop your
first instincts about what makes a system elegant vs. ugly.

### Week 1-2: Study Before You Build

#### Study Failures

**Read 10 incident reports on ML system failures:** - Search: "Uber
Michelangelo postmortem", "Netflix ML incident", "Spotify recommendation
outage" - Also: Google "site:blog.\[company\].com ML pipeline failure"
for various companies - Good aggregator: SRE Weekly, Incident.io blog

For each incident, document using the taste vocabulary:

``` markdown
# Incident: [Company] [System] Failure

**What happened:** [1-2 sentences]
**Root cause:** [Technical cause]
**Taste smell:** [Which "ugly" pattern from the rubric?]
**What assumption broke at scale?**
**Could this have been predicted from the architecture alone?**
```

#### Study Excellence

**Pick 3 ML systems known for elegance:** - Uber's Michelangelo
platform - Netflix's model serving architecture - Spotify's feature
platform - (Or substitute: LinkedIn's Pro-ML, Airbnb's Bighead, Google's
TFX)

For each, document using the "beautiful" rubric:

``` markdown
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

**ADR opportunity:** After this study, write ADR-002 about a design
pattern you want to adopt and why.

### Week 3-4: Theory Fundamentals

**Read *Designing Data-Intensive Applications* Chapters 5-9:** - Chapter
5 (Replication): When do you need it? What can go wrong? - Chapter 6
(Partitioning): How to split data. Relevance to feature stores. -
Chapter 7 (Transactions): What guarantees do you actually need? -
Chapter 8 (Distributed Systems): Failure modes you must internalize. -
Chapter 9 (Consistency): Eventual vs. strong. When each matters.

**After each chapter, write a 1-paragraph summary:** "What does this
mean for my ML pipeline?"

**Understand these concepts well enough to explain them to your
accountability partner or in a blog post:** - CAP theorem (and why it's
usually misunderstood) - Backpressure and flow control - Batch
vs. stream processing trade-offs - Feature store patterns (online
vs. offline)

### Week 5-6: Build the Pipeline

#### Project: Weather Prediction ML Pipeline

**What you're building:**

**🔧 VPS Architecture:**
```text
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

``` python
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
    # Dropping rows is simple but loses data. Alternative would be
    # forward-fill or use smaller window for early rows.
    # For this use case, dropping is acceptable.
    df = df.dropna()
    
    df.to_parquet("gs://your-bucket/features/weather_features.parquet")
    context.log.info(
        f"Generated {len(df)} feature rows from {len(raw_weather_data)} raw rows"
    )
    return df
```

**Model Training:**

``` python
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
    
    Trade-off: RF is slower than linear models but more accurate
    for our non-linear weather patterns.
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

``` python
from fastapi import FastAPI, HTTPException
from pydantic import BaseModel
import mlflow.pyfunc
import logging

logger = logging.getLogger(__name__)

app = FastAPI()

# Load model once at startup — acceptable for single-model serving.
# For multi-model or frequent reloads, use a model server (Seldon, BentoML).
# See ADR-005 for this decision.
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
    - Can the model actually make predictions? (not just loaded)
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

``` python
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

#### Deliverable Phase 1A:

-   [ ] GitHub repo with complete pipeline (well-documented)
-   [ ] Working end-to-end: data in → predictions out
-   [ ] Deployed to VPS (Docker Compose stack running)
-   [ ] Basic Grafana dashboard (prediction count, latency, errors)
-   [ ] Can handle 10 requests/second
-   [ ] At least 2 ADRs written (orchestrator choice, model choice)
-   [ ] Blog post or public write-up: "What I built and what I'd change"

------------------------------------------------------------------------

### Phase 1A Reflection (Do Before Moving On)

**This is critical. Don't skip.**

``` markdown
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

If you answered "Forcing it" or "No" to the last question, pause and
reflect:

-   Maybe you need to rebuild Phase 1A with different decisions
-   Maybe you need more feedback before continuing
-   Maybe self-directed learning isn't working for you (that's okay)

------------------------------------------------------------------------

## Phase 1B: Scale It Until It Breaks (4-5 Weeks)

**Goal:** Discover where your assumptions fail under pressure. The
breaks teach more than the building.

### Week 1-2: Systematic Stress Testing

#### Test 1: Data Volume

  ------------------------------------------------------------------------
  Scale   Expected Behavior  Actual Behavior  What Broke  Time to Process
  ------- ------------------ ---------------- ----------- ----------------
  10K     Works fine                                      
  rows                                                    

  100K    Should work                                     
  rows                                                    

  1M rows Might struggle                                  

  10M     Will break                                      
  rows                                                    
  ------------------------------------------------------------------------

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

# What breaks first?
# - OOM killer (RAM exhaustion)
# - Disk fills up (storage limits)
# - CPU pegged at 100% (compute limits)
# - Connection pool exhaustion
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

# 🔧 VPS: Run locust FROM your local machine TO the VPS
locust -f locustfile.py --host https://mlops.yourdomain.com

# Ramp: 10 → 100 → 500 → 1000 users
# VPS will likely max out around 100-200 concurrent users with 1 vCPU

# At each level, record:
# - p50, p95, p99 latency
# - Error rate
# - What the Grafana dashboard shows
```

  ---------------------------------------------------------------------------
  Concurrent Users p50 Latency  p95 Latency  p99 Latency  Error Rate  Notes
  ---------------- ------------ ------------ ------------ ----------- -------
  10                                                                  

  100                                                                 

  500                                                                 

  1000                                                                
  ---------------------------------------------------------------------------

#### Test 3: Concurrent Pipeline Runs

```bash
# Trigger 5 → 10 → 20 Dagster runs simultaneously
# What happens?

# 🔧 VPS-specific failures:
# - PostgreSQL connection pool exhaustion (default: 100)
# - RAM exhaustion → OOM killer
# - Disk I/O bottleneck (check: iostat -x 1)
# - File descriptor limits (check: ulimit -n)
# - Systemd service restarts

# VPS-specific failures you'll encounter:
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

For each bottleneck, document in this format:

``` markdown
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

**Minimum:** Fix 3 bottlenecks with full documentation.

**Example bottleneck fixes:**

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
# Bottleneck 1: Memory exhaustion at 1M rows

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
# Add:
# /var/log/mlops/*.log {
#     daily
#     rotate 7
#     compress
#     delaycompress
#     missingok
#     notifempty
# }

# Clean Docker
docker system prune -a --volumes

# Impact: Freed 15GB
# Cost: $0
```

**Alternative Fix: Chunk processing**
```python
# Before (loads all into memory):
df = pd.read_parquet("gs://bucket/data.parquet")
processed = process_data(df)

# After (chunked processing):
def process_in_chunks(file_path, chunk_size=100_000):
    for chunk in pd.read_parquet(file_path, chunksize=chunk_size):
        yield process_data(chunk)

# Impact: Can now handle 10M+ rows
# Cost: Same (actually lower - smaller instance needed)
```

# Bottleneck 2: Database connection pool exhaustion

# Before: Default SQLAlchemy settings (pool_size=5)
engine = create_engine(connection_string)

# After: Tuned for concurrent access
engine = create_engine(
    connection_string,
    pool_size=20,           # More connections
    max_overflow=10,        # Burst capacity
    pool_pre_ping=True,     # Verify connections before use
    pool_recycle=3600       # Recycle connections hourly
)

# Impact: Can handle 50+ concurrent pipeline runs
# Cost: Same (connection pool is free, just configuration)

# Also tune PostgreSQL on your VPS
# Edit: /etc/postgresql/15/main/postgresql.conf
# max_connections = 50 (down from 100 - we have limited RAM)
# shared_buffers = 512MB (25% of 2GB RAM)
# effective_cache_size = 1536MB (75% of 2GB RAM)
# Restart: sudo systemctl restart postgresql
```

### Week 4-5: Resource Analysis & Cost Awareness

``` markdown
# VPS Resource Analysis

### Current VPS usage

**Check your actual usage:**
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

### Projected costs at scale

**VPS Scaling Strategy:**

| Scale | Requests/Day | VPS Config | Monthly Cost | Notes |
|-------|-------------|------------|--------------|-------|
| Current (dev) | 100 | 2GB RAM, 1 vCPU | $12 | Single VPS |
| 100 users | 1K | 4GB RAM, 2 vCPU | $24 | Upgrade VPS |
| 1K users | 10K | 8GB RAM, 4 vCPU + Redis | $60 | Larger VPS + caching |
| 10K users | 100K | Load balancer + 3x 4GB VPS | $200 | Horizontal scaling |
| 100K users | 1M | Load balancer + 10x 8GB VPS | $800 | Multiple VPS + CDN |

### Where bottlenecks come from

**Biggest constraint:** [CPU? RAM? Disk I/O? Network?]

**Resource per user:** 
- At 1K users: 2MB RAM per active user
- At 100K users: 2MB RAM per active user
- (Good sign if it stays flat - means you're scaling efficiently)

### Architecture comparison (VPS constraints)

**Current "naive" architecture:**
- Feature computation: Real-time (on every request)
- Storage: All data in PostgreSQL (no archiving)
- Caching: None (every request hits DB)
- **Peak RAM usage at 10K users:** ___ MB
- **CPU usage at 10K users:** ___% average

**Optimized architecture:**
- Feature computation: Pre-computed batch job (Dagster asset)
- Storage: Archive old predictions to MinIO (keeps PostgreSQL lean)
- Caching: Redis for hot features (95% cache hit rate)
- **Peak RAM usage at 10K users:** ___ MB
- **CPU usage at 10K users:** ___% average
- **Resource savings:** ___% less RAM, ___% less CPU

**Trade-offs in optimized version:**
- Features not real-time (acceptable for daily predictions)
- Cache warmup time on restart (~30 seconds)
- Redis adds 50MB RAM overhead (worth it for 95% cache hit)

**ADR: Architecture Resource Optimization**
```

**Key insight:** On VPS, optimization is about using what you have efficiently, not spending more money.

#### Deliverable Phase 1B:

-   [ ] Scaling report with 3+ bottlenecks documented
-   [ ] Load test results with graphs
-   [ ] Resource usage analysis with scaling projections
-   [ ] Updated Grafana dashboard
-   [ ] ADRs for each major fix decision
-   [ ] Blog post: "How my ML pipeline broke at scale (and how I fixed
    it)"

------------------------------------------------------------------------

## Phase 1.5: Taste Calibration --- The Honest Checkpoint (2-3 Weeks)

**Goal:** Calibrate your taste against experts. Determine if you're
developing judgment or just completing exercises.

**This is the most important exercise in the entire curriculum.**

### Week 1: Get Expert Feedback

**Find 3 people to review your pipeline:** - **Easiest:** Post in MLOps
Slack with link to your (public) repo - **Good:** Your accountability
partner + someone from a community - **Best:** A staff+ engineer (use
ADPList, cold outreach, or your network) - **Realistic:** You may only
get 1-2 reviews. That's fine. Quality \> quantity. Send this message:

``` text
I built this ML pipeline as a learning project (link to repo + architecture diagram).
Could you spend 15 minutes reviewing it?

Specific questions:
1. What will break first when this serves 10x more traffic?
2. What's the ugliest part of this architecture?
3. If you had to maintain this at 2 AM, what would frustrate you?
4. What's one pattern I should learn from?
```

BEFORE sending: Write down YOUR predictions for what they'll say.

``` markdown
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

``` markdown
# Taste Gap Analysis

### Reviewer 1: [Name/Source]

| My Prediction | Their Actual Feedback | Match? | Why I Missed It |
|--------------|----------------------|--------|-----------------|
| Will break: ___ | Will break: ___ | ✓/✗ | |
| Ugly: ___ | Ugly: ___ | ✓/✗ | |
| 2 AM: ___ | 2 AM: ___ | ✓/✗ | |
| Pattern: ___ | Pattern: ___ | ✓/✗ | |

### Reviewer 2: [Name/Source]
[Same table]

### Reviewer 3: [Name/Source]
[Same table]

### Aggregate Accuracy
- Predictions matched: ___/12 (___%)
- Categories I'm good at predicting: ___
- Categories I'm blind to: ___

### What This Tells Me About My Taste

**I'm good at spotting:**
[E.g., "I correctly predicted the database bottleneck"]

**I'm blind to:**
[E.g., "I completely missed operational concerns like monitoring gaps"]

**My mental model is missing:**
[E.g., "I don't think enough about maintenance - I focus on 'does it work' not 'can someone else maintain it'"]

**Specific things I'll change:**
1. ___
2. ___
3. ___
```

### Week 3: Deep Study of One Beautiful System

**Pick ONE ML platform to study deeply:** - Uber Michelangelo - Netflix
model serving - Spotify feature platform - LinkedIn Pro-ML - (Pick the
one most relevant to what you're building) **Read EVERYTHING about
it:** - Original blog post(s) - Follow-up posts about evolution -
Conference talks (YouTube) - GitHub repos if available - Design docs if
public Document:

``` markdown
# Deep Study: [System Name]

### Architecture (draw it)
[Diagram - hand-drawn is fine, upload photo]

### Beautiful Qualities (from rubric)
- **Proportional complexity:** [how?]
- **Explicit trade-offs:** [where documented?]
- **Observable by default:** [what signals?]
- **Obvious flow:** [could I follow it?]
- **Graceful degradation:** [examples?]
- **Deletable parts:** [how decoupled?]

### What They Chose NOT to Do
[Often more revealing than what they built]

### Constraints That Forced Elegance
[Beautiful systems are usually born from constraints]
- Scale constraint: ___
- Time constraint: ___
- Team constraint: ___
- Cost constraint: ___

### How My Pipeline Compares
| Aspect | Their System | My Pipeline | Gap |
|--------|-------------|-------------|-----|
| Feature serving | Pre-computed, cached | Real-time computation | Performance hit |
| Monitoring | Custom metrics, dashboards | Basic Prometheus | Less visibility |
| Deployment | Blue-green, canary | Direct deploy | More risk |

### Three Things I'm Changing in My Pipeline
1. [Specific change based on this study]
2. [Specific change based on this study]
3. [Specific change based on this study]

### ADR: Lessons from [System Name]
[Write formal ADR about what you're adopting and why]
```

------------------------------------------------------------------------

### THE HONEST CHECKPOINT

Answer these honestly. Write them down. Show them to your accountability
partner.

``` markdown
# Honest Checkpoint

### 1. Can I explain my pipeline's architecture WITHOUT looking at code?
[ ] Yes — I can whiteboard it from memory
[ ] Partially — I remember the flow but not the details
[ ] No — I need to look at the code

### 2. Did the expert feedback SURPRISE me significantly?
[ ] Yes — they found things I never considered
[ ] Somewhat — I knew about some issues but not all
[ ] No — I predicted most of their feedback

### 3. Can I name 3 things I'd do differently WITHOUT referencing notes?
[ ] Yes (list them):
    1. ___
    2. ___
    3. ___
[ ] I can name 1-2
[ ] No

### 4. Has my INTUITION about designs changed, or just my KNOWLEDGE?
[ ] Intuition — I "feel" when something is off before I can articulate why
[ ] Knowledge — I know the rules but apply them mechanically
[ ] Unsure

### 5. When I look at a new pipeline repo, can I predict problems?
[ ] Yes — I can guess 3+ issues before reading the code
[ ] Somewhat — I can guess 1-2 obvious ones
[ ] No — I need to read the code first

### 6. Do I care about this work, or am I just checking boxes?
[ ] Care — I'm excited to keep going
[ ] Neutral — It's fine, educational
[ ] Checking boxes — I'm doing it because I "should"
```

#### Interpreting Your Answers

  -----------------------------------------------------------------------
  Pattern            Diagnosis              Prescription
  ------------------ ---------------------- -----------------------------
  Yes, No, Yes,      You're developing      Keep going. You're on the
  Intuition, Yes,    taste. Proceed to      right track.
  Care               Phase 2.               

  Partially,         Normal progress.       Proceed, but slow down. Go
  Somewhat, 1-2,     You're learning but    deeper on each phase.
  Knowledge,         not yet intuitive.     Consider upgrading to Tier
  Somewhat, Neutral                         2/3 community.

  No, Yes, No,       You're completing      STOP. See Plan B below.
  Knowledge, No,     exercises, not         
  Checking boxes     developing taste.      
  -----------------------------------------------------------------------

#### Plan B (If You Scored Poorly)

If you got the third pattern above, this curriculum isn't working for
you. **That's okay.**

**Options:**

1.  **Rebuild Phase 1 from scratch with different decisions**
    -   Pick a different domain (not weather)
    -   Make different architectural choices
    -   Focus on understanding WHY, not just making it work
2.  **Get a job with strong senior engineers**
    -   Some people develop taste better through apprenticeship
    -   No shame in this --- it's often faster and more effective
    -   Self-directed learning isn't for everyone
3.  **Find a paid mentor for structured 1-on-1 teaching**
    -   If you have budget, this accelerates learning
    -   More effective than struggling alone
4.  **Take a break, come back in 3 months**
    -   Sometimes you need distance to consolidate learning
    -   Work on other things, let this percolate
5.  **Accept you might be a specialist, not a generalist**
    -   That's totally fine
    -   Focus on getting really good at one thing
    -   Depth \> breadth for some career paths

**There is no shame in any of these paths. Recognizing when something
isn't working is also taste.**

------------------------------------------------------------------------

## Phase 2: Go Deep (3-4 Weeks)

**Goal:** Go deep on something that hurt you in Phase 1. Surface
knowledge → deep understanding → taste.

### Choosing What to Go Deep On

**DO NOT pick from a menu. Instead:**

1.  Review your Phase 1B bottleneck log and Phase 1.5 gap analysis.
2.  Ask: "What broke that I couldn't fully explain?"
3.  That's what you go deep on.

**Examples of how pain maps to depth:**

  ------------------------------------------------------------------------------
  Phase 1 Pain                     Go Deep On                  Why
  -------------------------------- --------------------------- -----------------
  "Pandas ran out of memory at 1M  Data processing internals   You'll stop
  rows"                            --- chunked processing,     treating Pandas
                                   Arrow/Parquet columnar      as a black box
                                   formats, when to abandon    
                                   Pandas                      

  "Database queries got slow at    Database internals ---      You'll know why
  scale"                           indexes, query planning,    things are slow,
                                   LSM-trees vs. B-trees,      not just that
                                   connection pooling          they're slow

  "Feature engineering was slow    Feature store architecture  You'll understand
  and redundant"                   --- online vs. offline      when
                                   stores, computation         pre-computation
                                   vs. serving, caching        beats real-time
                                   strategies                  

  "Couldn't figure out if pipeline Observability deep dive --- You'll design
  was healthy"                     structured logging,         systems that tell
                                   distributed tracing, metric you they're sick
                                   design, alert fatigue       

  "Concurrent pipeline runs fought Distributed systems         You'll understand
  over resources"                  fundamentals --- locking,   contention at a
                                   consensus, resource         fundamental level
                                   isolation, scheduling       
  ------------------------------------------------------------------------------

### If Phase 1 Was Too Easy (Nothing Really Broke)

This means one of three things:

1.  **You didn't push hard enough in Phase 1B**
    -   Go back and load test to 100K requests/sec, not 1K
    -   Process 100M rows, not 1M
    -   Push until something actually breaks
2.  **Your system is actually solid** (unlikely but possible)
    -   Maybe you made good architectural choices
    -   Maybe you over-engineered appropriately
    -   If this is true, experts would confirm it
3.  **You're using overpowered infrastructure** (Too much RAM/CPU hides scaling
    issues)
    -   Downgrade your VPS to 1GB RAM to force optimization
    -   Add artificial resource limits via Docker
    -   Constrain resources to reveal issues

### If You Genuinely Don't Know What Hurt Most

Pick ONE of these structured options:

#### Option A: Database Internals

Read DDIA Chapters 3-4 deeply

Implement a simple storage engine (both LSM-tree and B-tree)

``` python
# LSM-Tree: Write-optimized (append to log, merge periodically)
# B-Tree: Read-optimized (in-place updates, balanced tree)

# Implement both. Benchmark for ML feature storage:
# - Write 1M feature vectors
# - Read random feature vectors
# - Range query (all features for user X between dates)

# When is each better?
```

Connect to your pipeline: Which is better for your feature store? Why?
Write ADR about storage engine choice for your use case

**Deliverable:** Working implementations, benchmark results, decision
framework, blog post

#### Option B: Stream Processing Deep Dive

Build a streaming feature pipeline alongside your batch pipeline:

``` python
# Use Google Pub/Sub or Kafka
# Real-time feature computation from weather sensor stream

# Handle:
# - Late arriving data (weather station reports delayed)
# - Exactly-once semantics (don't double-count)
# - Backpressure (too many events, consumer can't keep up)
# - Out-of-order events (timestamps don't match arrival order)
```

Compare batch vs. stream for your pipeline:

  Dimension     Batch     Stream    Winner For This Use Case
  ------------- --------- --------- -------------------------------
  Latency       Hours     Seconds   Stream if real-time needed
  Complexity    Low       High      Batch (our use case is daily)
  Cost          \$X       \$Y       Batch
  Correctness   Easier    Harder    Batch
  Operability   Simpler   Complex   Batch

Write ADR: When is streaming worth the complexity for ML pipelines?

**Deliverable:** Working streaming pipeline, batch vs. stream
comparison, decision framework, blog post

#### Option C: Observability Deep Dive

Read *Observability Engineering* by Charity Majors (key chapters: 1-4,
7-9)

Implement proper observability for your pipeline:

``` python
# Structured logging with correlation IDs
# Every log line traceable to a specific pipeline run

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

# Custom metrics that actually matter:
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

# Alerts that DON'T cause fatigue:
# - Alert on symptoms, not causes
# - Alert on rates of change, not absolute values
# - Every alert has a runbook
```

Design a dashboard that answers: "Is the system healthy?" in 10 seconds
Write ADR: What to monitor vs. what to log vs. what to trace

**Deliverable:** Full observability stack, dashboard screenshot, alert
design document, blog post

------------------------------------------------------------------------

### Depth Validation

**You've gone deep enough when:**

-   [ ] You can explain the concept to your accountability partner and
    answer their follow-up questions
-   [ ] You know when the technology is the WRONG choice (not just how
    to use it)
-   [ ] You've written an ADR that captures trade-offs a junior engineer
    wouldn't see
-   [ ] Your Phase 1 pipeline is better because of what you learned
-   [ ] You can write a blog post teaching this to others

**You haven't gone deep enough when:**

-   You can recite facts but can't explain trade-offs
-   You followed a tutorial but couldn't modify the approach
-   You don't know when NOT to use the technology
-   You can't explain it without looking at notes

------------------------------------------------------------------------

## Phase 3: Resilience & Production Hardening (5-6 Weeks)

**Goal:** Make your pipeline survive the chaos of production. Develop
operational taste.

### Week 1-2: Resilience Patterns

**Study first:**

Read *Release It!* by Michael Nygard, Chapters 4-8

Understand these patterns (don't just implement them --- understand WHEN
each is appropriate):

  -------------------------------------------------------------------------
  Pattern      What It Does       When to Use        When NOT to Use
  ------------ ------------------ ------------------ ----------------------
  Circuit      Stops calling a    External service   Internal function
  breaker      failing dependency calls              calls

  Retry with   Retries failed     Transient failures Permanent failures
  backoff      operations with    (network blips)    (bad input)
               increasing delay                      

  Timeout      Abandons slow      Any external call  CPU-bound computation
               operations                            

  Fallback     Provides degraded  When "something"   When wrong answer is
               but functional     \> "nothing"       worse than no answer
               response                              

  Bulkhead     Isolates failures  Multi-tenant or    Simple single-path
               to one component   multi-dependency   systems

  Dead letter  Captures failed    Async message      Synchronous
  queue        messages for later processing         request/response
               processing                            
  -------------------------------------------------------------------------

**ADR opportunity:** For each pattern you add, write an ADR explaining
why you chose it for that specific location.

### Week 2-3: Implement Resilience

**Add a validation service** (this creates a dependency we can break):

``` python
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
    """Validate weather data quality.
    
    Runs domain-specific checks that are too complex
    for simple schema validation.
    """
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

``` python
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


def local_validation_fallback(df: pd.DataFrame) -> pd.DataFrame:
    """Simple local validation when service is unavailable.
    
    Only checks basic ranges. Misses complex cross-field validation.
    """
    return df[
        (df["temperature"] >= -90) & (df["temperature"] <= 135) &
        (df["humidity"] >= 0) & (df["humidity"] <= 100) &
        (df["pressure"] >= 870) & (df["pressure"] <= 1085)
    ]
```

**Add retry with backoff:**

``` python
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
    This gives the upstream service time to recover.
    """
    response = requests.get(
        WEATHER_API_URL,
        params={"appid": api_key},
        timeout=10  # Don't wait forever
    )
    response.raise_for_status()
    return pd.DataFrame(response.json()["data"])
```

**Add timeout and fallback to serving:**

``` python
import asyncio

# Simple cache for fallback predictions
prediction_cache = {}


@app.post("/predict")
async def predict(request: PredictionRequest):
    feature_hash = hash(tuple(request.dict().values()))
    
    try:
        # 2-second timeout on prediction
        prediction = await asyncio.wait_for(
            run_prediction(request),
            timeout=2.0
        )
        # Cache successful predictions
        prediction_cache[feature_hash] = prediction
        return {"prediction": prediction, "source": "live"}
    
    except asyncio.TimeoutError:
        cached = prediction_cache.get(feature_hash)
        if cached is not None:
            logger.warning(
                "Model timeout, serving from cache",
                extra={"feature_hash": feature_hash}
            )
            return {
                "prediction": cached,
                "source": "cache",
                "warning": "live model timed out"
            }
        raise HTTPException(503, "Model unavailable and no cached prediction")
```

### Week 3-4: Chaos Engineering

**Set up Toxiproxy:**

``` bash
docker run -d --name toxiproxy \
</text>

<old_text line=1405>
  -p 20000-20010:20000-20010 \
  ghcr.io/shopify/toxiproxy
Inject failures systematically:


# Test 1: Slow dependency (5-second latency on validation service)
  -p 8474:8474 \
  -p 20000-20010:20000-20010 \
  ghcr.io/shopify/toxiproxy
Inject failures systematically:


```bash
# Test 1: Slow dependency (5-second latency on validation service)
toxiproxy-cli create validation -l 0.0.0.0:20000 -u validation-service:8000
toxiproxy-cli toxic add validation -t latency -a latency=5000

# Expected: Circuit breaker opens after 5 timeouts, fallback kicks in
# Actual: ___________
# Did it match expectations? Yes/No
# If no, why not? ___

# Test 2: Flaky dependency (50% packet loss)
toxiproxy-cli toxic add validation -t limit_data -a bytes=500

# Expected: Some requests fail, retries handle it
# Actual: ___________

# Test 3: Total outage (dependency completely gone)
toxiproxy-cli toxic add validation -t timeout -a timeout=0

# Expected: Immediate circuit break, 100% fallback
# Actual: ___________

# Test 4: Slow database
# Add latency to your database connection
# Expected: Queries time out gracefully, connection pool doesn't exhaust
# Actual: ___________
```

**Document results:**

  -------------------------------------------------------------------------
  Failure Injected Expected Behavior Actual Behavior Matched?   Fix Needed
  ---------------- ----------------- --------------- ---------- -----------
  5s latency       Circuit opens                     ✓/✗        
                   after 5 fails                                

  50% packet loss  Retries succeed                   ✓/✗        

  Total outage     100% fallback                     ✓/✗        

  Slow database    Graceful timeout                  ✓/✗        
  -------------------------------------------------------------------------

For each mismatch, write:

``` markdown
# Chaos Test Failure: [Name]

**Expected:** ___
**Actual:** ___
**Why the mismatch:** ___
**Fix applied:** ___
**Re-test result:** ___
```

### Week 5: Resource & Cost Awareness

**Goal:** Understand cost implications WITHOUT wasting money.

#### Exercise 1: Analyze Your Infrastructure Usage

**🔧 VPS Cost Analysis**

```markdown
# VPS Cost Analysis

**Monthly Fixed Costs:**
- VPS: $10/month (Hetzner CPX11)
- Domain: $1/month (amortized)
- SSL: $0 (Let's Encrypt)
- **Total: $11/month**

**Resource Usage (check with monitoring):**
- CPU: Average ___%, Peak ___%
- RAM: Average ___GB, Peak ___GB
- Disk: ___GB used of 40GB
- Network: ___GB egress/month

**Scale Decision Point:**
- Current: 2GB RAM, 1 vCPU
- Next tier: 4GB RAM, 2 vCPU = $20/month
- **Upgrade when:** RAM consistently > 80% or CPU > 70%

**At what scale do we need to upgrade?**
- Current handles: ~___ requests/day
- Upgrade needed at: ~___ requests/day
- Cost per request (current): $11/month ÷ ___ requests = $___
```

**VPS Cost Analysis**

```markdown
# VPS Resource Usage Analysis

**Check your actual usage:**
```bash
# Run on your VPS
htop                    # CPU/RAM
docker stats            # Per-container usage
df -h                   # Disk usage
vnstat -m               # Network usage (if installed)
```

### Actual Usage This Month

| Resource | Usage | VPS Limit | Utilization | Notes |
|----------|-------|-----------|-------------|-------|
| RAM | X GB | 2 GB | X% | Peak usage |
| CPU | X% avg | 100% | X% peak | |
| Disk | X GB | 50 GB | X% | |
| Network | X GB | 2 TB | X% | Included in VPS |
| **Total Cost** | | | | **$12/month** |

**Current VPS tier:** $___ per month
**Projected annual cost:** $___/year (fixed)
```

#### Exercise 2: Cost Projection at Scale

``` markdown
# What Your Architecture Would Cost at Scale

**VPS Scaling Calculator:**

**Current actual usage (from metrics):**
- API requests: ___ per day
- Data processed: ___ GB per day
- Storage: ___ GB total

### Projected Costs

| Scale | Requests/Day | Data/Day | Storage | Compute | Networking | Total/Month |
|-------|-------------|----------|---------|---------|-----------|-------------|
| Current (free) | X | Y GB | Z GB | $0 | $0 | $0 |
| 100 users | 1K | 10 GB | 100 GB | $5 | $2 | ~$15 |
| 1K users | 10K | 100 GB | 1 TB | $50 | $20 | ~$150 |
| 10K users | 100K | 1 TB | 10 TB | $500 | $200 | ~$1,500 |
| 100K users | 1M | 10 TB | 100 TB | $5K | $2K | ~$15,000 |

### Analysis

**Biggest cost driver:** [Compute? Storage? Network? Data processing?]

**Cost per user:**
- At 1K users: $0.15 per user/month
- At 100K users: $0.15 per user/month
- **Scaling linearly?** Yes/No
- (If linear = good. If super-linear = architectural problem)

**When do you need to upgrade VPS?**
- When RAM usage consistently > 85%
- When CPU usage consistently > 80%
- Current trajectory: Will need upgrade in ___ months
```

#### Exercise 3: Architecture Cost Comparison

``` markdown
# Expensive Architecture vs. Cheap Architecture

### Scenario: Serving 1M predictions/month

**Architecture A: "Naive" (what you built initially)**
- Multiple VPS instances: Always-on
- Feature computation: Real-time on every request
- Storage: All data on local disk
- **Estimated monthly cost:** $___

**Architecture B: "Optimized"**
- Single VPS with Redis caching
- Feature computation: Pre-computed batch, served from cache
- Storage: Archive old data to cheaper object storage (MinIO tiering)
- **Estimated monthly cost:** $___

**Savings:** $___/month (___%)

**Trade-offs accepted in Architecture B:**
- Cold start latency: 2-5s occasionally (acceptable for our use case)
- Features not real-time: Updated daily (acceptable for weather predictions)
- Old data access slower: 50-100ms vs. 10ms (rarely accessed anyway)

**Is it worth it?** Yes/No — Why: ___

**ADR: Architecture Cost Optimization**
```

#### Exercise 4: Find Cost Anti-Patterns in Your Code

``` python
# Review your code for expensive patterns

# EXPENSIVE: Load entire dataset into memory
df = pd.read_parquet("gs://bucket/all_data.parquet")
# Problem: If dataset is 100GB, needs huge instance
# Cost: High-memory instance = 10x more expensive

# CHEAP: Process in chunks
for chunk in pd.read_parquet("gs://bucket/all_data.parquet", chunksize=10_000):
    process(chunk)
# Cost: Can use smallest instance type

# EXPENSIVE: Store temp files in premium storage
temp_df.to_parquet("gs://bucket/temp.parquet")
# GCS Standard: $0.023/GB/month
# For 1TB temp files: $23/month

# CHEAP: Use appropriate storage class
temp_df.to_parquet("gs://bucket-nearline/temp.parquet")
# GCS Nearline: $0.010/GB/month
# For 1TB: $10/month
# Savings: $13/month (57%)

# EXPENSIVE: No caching, recompute everything
def get_features(user_id):
    # 500ms computation, every call
    return compute_features(user_id)

# CHEAP: Cache frequently accessed features
from functools import lru_cache

@lru_cache(maxsize=1000)
def get_features_cached(user_id):
    return compute_features(user_id)
# First call: 500ms, subsequent: <1ms
# For 1K daily active users: 95% cache hit rate
# Savings: 95% reduction in compute time

# EXPENSIVE: Multiple always-on VPS instances
# 5 x VPS (4GB each) + load balancer
# Cost: $150/month for capacity

# CHEAP: Single VPS with efficient caching
# 1 x VPS (2GB) + Redis
# Cost: $12/month
# Trade-off: Limited concurrent requests, must optimize
# Acceptable for: Non-latency-critical workloads
```

``` markdown
# Cost Anti-Patterns Found in My Code

| Anti-Pattern | Where | Current Cost Impact | Fix | Savings |
|-------------|-------|---------------------|-----|---------|
| | | | | |

**Total potential savings:** $___/month at 10K users
```

#### Exercise 5: Study Someone Else's Expensive Mistake

Pick one cost disaster to analyze:

-   Search: "unexpected hosting costs" or "bill shock" on Hacker News
-   Examples: Runaway processes, forgotten resources, inefficient architectures

``` markdown
# Cost Disaster Case Study

**Company/Person:** ___
**What happened:** ___

**Root cause:** ___

**Cost impact:** $___

**How long before discovery:** ___

**How it was discovered:** ___

**How it could have been prevented:**
1. ___
2. ___
3. ___

**Lessons for my architecture:**
- Alert I should set: ___
- Config I should double-check: ___
- Review I should do monthly: ___

**One thing I'm changing RIGHT NOW:** ___
```

#### Exercise 6: Set Up Cost Safeguards

``` markdown
# Cost Protection Checklist

- [ ] **Monitor VPS billing**
  - VPS provider dashboard → Billing
  - Your cost is flat: $12/month
  - Alert if you accidentally spin up extra resources

- [ ] **Monitor resource usage alerts**
  - Set up Prometheus alerts for high CPU/RAM/disk
  - Email notifications when thresholds exceeded
  - Can analyze: "What's consuming resources?"

- [ ] **Set Docker resource limits**
  - Edit docker-compose.yml to add resource constraints
  - Limit: CPU shares, memory limits per container
  - Prevents: One container consuming all VPS resources
  
  ```yaml
  services:
    dagster:
      mem_limit: 512m
      cpus: 0.5
  ```

- [ ] **Create cleanup script**
  ```bash
  #!/bin/bash
  # cleanup.sh - run weekly
  find /data/temp -mtime +7 -delete
  
  # Clean up old Docker images
  docker image prune -a --filter "until=168h" -f
  
  # Clean up logs
  journalctl --vacuum-time=7d
  ```

- [ ] **Weekly resource review**

  ```
  Calendar reminder: Every Friday
  Check: VPS resource usage (htop, df -h, docker stats)
  Ask: Any resource spikes? Disk filling up? Why?
  Document: Weekly resource usage, changes from last week
  ```

- [ ] **Resource impact review in PR template**


## Cost Impact (required for infra changes)
- [ ] Estimated cost change: +$___/month or -$___/month
- [ ] Reasoning: ___
- [ ] Approved by: ___


**Deliverable Week 5:**
- [ ] VPS resource usage analysis
- [ ] Scaling projections at 3 levels (100, 1K, 10K users)
- [ ] Architecture cost comparison
- [ ] Code anti-patterns found and fixed
- [ ] Cost disaster case study
- [ ] Cost safeguards implemented
- [ ] Blog post: "How I optimized my ML pipeline for 2GB RAM"

---

### Week 6: Blind Incident Drill

**The 2 AM Test.**

- [ ] Have your accountability partner, cohort member, or mentor inject a failure:
  - They choose what breaks
  - You don't know what it is
  - You can only use logs, metrics, and dashboards to find it

- [ ] Possible failures they can inject:
  - Kill the validation service
  - Introduce a slow database query (add `time.sleep(2)` somewhere)
  - Inject bad data (NaN values, wrong types)
  - Rate limit the upstream weather API
  - Fill up disk space with logs
  - Cause a memory leak (gradually increasing payload sizes)
  - Break a configuration (wrong env variable)

- [ ] Time yourself:
  - Detection time: ___
  - Diagnosis time: ___
  - Mitigation time: ___
  - Total: ___

- [ ] Write post-mortem:

```markdown
## Incident Report

**Date:** ___
**Duration:** Detection at T+___, Mitigated at T+___

**What Happened:**
[Describe what you observed - error rates, latency, etc.]

**Timeline:**
- T+0: [First signal - alert, dashboard spike, etc.]
- T+5: [Initial investigation]
- T+10: [Hypothesis formed]
- T+15: [Debugging steps taken]
- T+20: [Root cause identified]
- T+25: [Mitigation applied]
- T+30: [Confirmed resolved]

**Root Cause:**
[What actually broke - be specific]

**How I Found It:**
[Which logs/metrics/dashboards led me there]

**What Slowed Me Down:**
- Missing observability: ___
- Wrong hypothesis: ___
- Debugging dead ends: ___

**Mitigation:**
[What I did to stop the bleeding]

**Prevention:**
[What I'm adding to prevent/detect this faster next time]

**Taste Lesson:**
[What does this teach me about system design?]
[What architectural decision would have prevented this?]
```

#### Deliverable Phase 3:

-   [ ] Pipeline with resilience patterns (circuit breaker, retry,
    timeout, fallback)
-   [ ] Chaos test results documented
-   [ ] Resource usage analysis and optimization
-   [ ] Resource monitoring and alerts implemented
-   [ ] Blind incident post-mortem
-   [ ] ADRs for each resilience decision
-   [ ] Updated Grafana dashboards
-   [ ] Blog post: "Making my ML pipeline resilient"

------------------------------------------------------------------------

## Phase 4: Business Context & Product Thinking (2-3 Weeks)

**Goal:** Technical taste without business taste is incomplete. Learn to
make build/don't-build decisions.

### Week 1: Business Fundamentals

**Read *The Mom Test* by Rob Fitzpatrick** (short book, 2-3 days) -
**Key lesson:** People will lie to be nice. Ask about their behavior,
not their opinions. - **Examples of bad questions:** "Would you use
this?" "Is this a good idea?" "Would you pay \$X?" - **Examples of good
questions:** "How do you currently solve this?" "What did this problem
cost you last month?" Learn to calculate unit economics:

``` markdown
# Unit Economics Basics

**Cost per prediction:**

**🔧 VPS Economics:**
- Compute: $0 (included in $10/month flat fee)
- Storage: $0 (included, until disk full)
- API calls: $0.0001 per weather API call
- Total cost per prediction: ~$0.0001

**At scale:**
- 1M predictions/month = $100 API costs + $10 VPS = $110/month
- Cost per prediction: $0.00011
- **Fixed infrastructure cost is your friend**

**VPS Economics:**
- Compute: Flat $12/month (VPS includes CPU/RAM)
- Storage: Included in VPS (50GB disk)
- API calls: $0.0001 per weather API call (external API)
- Database: Included in VPS (PostgreSQL in Docker)
- Total cost per prediction: $0 marginal (fixed cost model)

**At scale:**
- 1M predictions/month = $100 API + $200-400 infrastructure = $300-500/month
- Cost per prediction: $0.0003-0.0005
- **Variable costs scale with usage**

**Revenue per prediction:**
- Pricing: $___ per prediction
- Or: $___ per month subscription / ___ predictions = $___ per prediction

**Margin:**
- VPS margin per prediction: Revenue - $0.00011 = $___
- VPS margin per prediction: Revenue - $0 (marginal cost) = $___
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

**Infrastructure Decision:**
- If serving < 100K requests/month → VPS wins on cost
- If serving > 1M requests/month → Consider horizontal scaling (multiple VPS)
- **Document this trade-off in ADR**
```

### Week 2: The Pivot Decision

Your weather pipeline exists. Now ask: should it?

**Step 1: Identify potential users (pick 3 domains)**

  -------------------------------------------------------------------------------
  Domain        User       Problem They    How Weather Prediction Existing
                Persona    Have            Helps                  Solutions
  ------------- ---------- --------------- ---------------------- ---------------
  Agriculture   Farm       Crop planning,  Reduce crop loss by X% Weather.com,
                manager    frost risk                             NOAA, local
                                                                  knowledge

  Events        Event      Outdoor event   Avoid rain             Weather.com,
                planner    decisions       cancellations          gut feeling

  Logistics     Delivery   Route           Avoid weather delays   In-house,
                company    optimization                           weather APIs

  Energy        Solar farm Solar           Better capacity        Expensive
                operator   forecasting     planning               enterprise
                                                                  solutions
  -------------------------------------------------------------------------------

**Step 2: Interview 3 potential users**

**Find them:** - Reddit communities (r/farming, r/events, etc.) -
LinkedIn (search for job titles) - Local businesses (cold email) - Your
network Use this recruiting script:

``` text
Subject: Quick question about [their domain] (not selling anything)

Hi [Name],

I'm building a tool for weather-based planning in [their domain].
Before I build the wrong thing, I'd love to understand how you currently
handle weather uncertainty.

Could I ask you 5 questions? 15 minutes max, no sales pitch.

Happy to buy you a coffee or make a $20 donation to a charity of your choice.

Thanks,
[Your name]
```

Mom Test questions (ask these, not "would you use my product"):

**1. "Walk me through the last time weather disrupted your
\[operations/event/etc.\]"** - Listen for: Specific incident, cost, pain
level

**2. "How do you currently make weather-related decisions?"** - Listen
for: Tools they use, process, who decides

**3. "What did weather uncertainty cost you last year?"** - Listen for:
Actual dollar amounts or quantifiable impact

**4. "If you could wave a magic wand, how would weather forecasting be
different?"** - Listen for: What they actually want (vs. what you built)

**5. "Have you tried other weather tools? What happened?"** - Listen
for: Why they stopped using them, what was missing

Document findings:

  --------------------------------------------------------------------------------
  User   Domain   Current        Real      Pain Level      Willing to      Notes
                  Solution       Pain?     (1-10)          Switch?         
  ------ -------- -------------- --------- --------------- --------------- -------
                                                                           

  --------------------------------------------------------------------------------

#### Step 3: The Build/Don't Build Decision

``` markdown
# Decision: Should This Product Exist?

### Evidence Assessment

**Supports building:**
- [evidence from interviews]

**Against building:**
- [evidence from interviews]

### Unit Economics Reality Check

**Cost per prediction:** $___
**What users would pay:** $___
**At break-even, need:** ___ users

### Market Analysis

| Factor | Our Product | Existing Solutions |
|--------|------------|-------------------|
| Accuracy | | |
| Price | | |
| Ease of use | | |
| Trust | | |

### Decision

[ ] BUILD — because: ___
[ ] PIVOT — to: ___ because: ___
[ ] KILL — because: ___

### If PIVOT: What Domain Instead?

**Based on user interviews:**
[What domain has more pain and fewer solutions?]

**New direction:**
[Describe the pivot]

**What changes in the architecture:**
[What stays, what changes]

**ADR: Pivot Decision**
```

#### Step 4: If you pivot, update your pipeline

Modify data ingestion for new domain Update model for specific use case
Add domain-specific features

This tests: Can you adapt existing infrastructure to new requirements?

**Why pivoting is valuable:** Real engineering careers involve constant
pivots. The ability to reuse and adapt existing systems (rather than
rebuild from scratch) is core judgment.

### Week 3: Implement the Pivot (If You Pivoted)

``` markdown
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

**Timeline:**
- Day 1-2: New data source integration
- Day 3-4: Domain-specific features
- Day 5-7: Retrain model
- Day 8-10: New output format / delivery
- Day 11-12: Test with actual user

**Success metric:**
At least 1 real user says "this is useful" or "I'd pay for this"
```

#### Deliverable Phase 4:

-   [ ] User interview notes (3 interviews, Mom Test format)
-   [ ] Build/pivot/kill decision with evidence
-   [ ] Unit economics analysis
-   [ ] If pivoted: Updated pipeline for new domain
-   [ ] If pivoted: Tested with at least 1 real user
-   [ ] ADR for the business decision
-   [ ] Blog post: "Why I pivoted from X to Y"

------------------------------------------------------------------------

## Phase 5: AI Oversight & Verification (3-4 Weeks)

**Goal:** Learn to work WITH LLMs effectively --- including knowing when
they're wrong.

### Week 1: Understanding LLM Strengths and Failure Modes

**This is NOT "find bugs in LLM code." It's developing judgment for when
and how to use LLMs.**

#### Exercise 1: Decomposition Judgment

Take a real task from your pipeline and try three approaches:

``` markdown
# Task: Add data quality monitoring to the feature pipeline

### Approach A: Ask LLM to do everything at once

**Prompt:**
"Write a complete data quality monitoring system for my ML pipeline that checks 
for drift, missing values, outliers, and schema violations, integrated with 
Prometheus and Grafana."

**Result:**
[Paste what LLM generated]

**Quality: ___/10**

**What went wrong:**
- ___

**What went right:**
- ___

### Approach B: Decompose into pieces

**Prompt 1:** "What are the most important data quality checks for an ML feature pipeline?"
**Prompt 2:** "Write a function that detects feature drift using KL divergence."
**Prompt 3:** "Write Prometheus metrics for tracking data quality over time."

**Result:**
[Paste what LLM generated]

**Quality: ___/10**

**What went wrong:**
- ___

**What went right:**
- ___

### Approach C: Use LLM for research, write it yourself

**Prompt:** "What are common data quality issues in ML pipelines and how do 
companies like Netflix and Uber detect them?"

**Then:** Write the implementation yourself using the research.

**Result:**
[Your implementation]

**Quality: ___/10**

**What went wrong:**
- ___

**What went right:**
- ___

### Judgment: Which approach worked best for this task? Why?

**Winner:** Approach ___

**Reasoning:**
- ___
- ___

**Pattern I notice:**
- LLMs are good at: ___
- LLMs struggle with: ___
- I should use them for: ___
- I should NOT use them for: ___
Exercise 2: Trust Calibration
For 10 different tasks, predict how much you'd trust LLM output, then test:


## LLM Trust Calibration

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

### Pattern I Found

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

1.  Ask an LLM to write data processing code:

**Prompt:**

``` text
Write a Python function that processes weather data:
- Forward-fill missing values
- Remove outliers beyond 3 standard deviations
- Normalize all numeric columns to [0, 1] range
- Return processed DataFrame
```

2.  Write property-based tests:

``` python
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
    ),
    "humidity": st.lists(
        st.one_of(
            st.floats(0, 100),
            st.just(np.nan)
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
    assume(len(df.dropna()) > 0)  # Need at least some valid data
    
    result = llm_process_weather_data(df)
    assert not result.isnull().any().any(), "Found NaN in output"


@given(data=weather_data)
def test_values_in_range(data):
    """All normalized values should be in [0, 1]."""
    df = pd.DataFrame(data)
    assume(len(df.dropna()) > 0)
    
    result = llm_process_weather_data(df)
    for col in result.select_dtypes(include=[np.number]).columns:
        assert result[col].min() >= 0, f"{col} has values < 0"
        assert result[col].max() <= 1, f"{col} has values > 1"


@given(data=weather_data)
def test_row_count_reasonable(data):
    """Output should have fewer or equal rows (outlier removal)."""
    df = pd.DataFrame(data)
    result = llm_process_weather_data(df)
    assert len(result) <= len(df)
    assert len(result) > 0, "All rows were removed"


# Edge cases LLMs typically miss:
def test_all_same_values():
    """When all values identical, normalization shouldn't crash."""
    df = pd.DataFrame({
        "temperature": [72.0] * 10,
        "humidity": [50.0] * 10
    })
    result = llm_process_weather_data(df)
    # Should handle division by zero gracefully
    assert len(result) > 0


def test_single_row():
    """Single row should be handled."""
    df = pd.DataFrame({
        "temperature": [72.0],
        "humidity": [50.0]
    })
    result = llm_process_weather_data(df)
    assert len(result) == 1


def test_all_nan():
    """All NaN input should not crash."""
    df = pd.DataFrame({
        "temperature": [np.nan] * 5,
        "humidity": [np.nan] * 5
    })
    result = llm_process_weather_data(df)
    # Either returns empty df or raises appropriate error
    assert isinstance(result, pd.DataFrame)

def test_first_row_nan():
    """Forward fill doesn't work on first row."""
    df = pd.DataFrame({
        "temperature": [np.nan, 72.0, 73.0],
        "humidity": [50.0, 51.0, 52.0]
    })
    result = llm_process_weather_data(df)
    # Should handle first row NaN appropriately
    assert not result.isnull().any().any()
```

3.  Document bugs found:

``` markdown
# LLM Bug Patterns Found

### Bug 1: Forward-fill on first row
- **Input:** First row has NaN
- **What happens:** First row still has NaN (forward-fill fails)
- **Why LLM missed it:** Didn't think about edge case of first row
- **Category:** Edge case
- **Fix:** Handle first row with backfill or drop

### Bug 2: Normalization when min == max
- **Input:** All values in column are identical
- **What happens:** Division by zero
- **Why LLM missed it:** Assumed data has variance
- **Category:** Edge case

### Bug 3: Outlier removal removes ALL data
- **Input:** Dataset where all values are outliers
- **What happens:** Empty DataFrame returned
- **Why LLM missed it:** Didn't consider pathological data
- **Category:** Edge case

### Pattern Summary

**LLMs consistently miss:**
- Edge cases (empty data, single row, all NaN, all same values)
- First/last element handling (forward-fill, rolling windows)
- Division by zero scenarios
- Pathological inputs (all outliers, all invalid)

**LLMs are good at:**
- Happy path implementation
- Standard library usage
- Code structure

**My testing strategy going forward:**
- ALWAYS add property-based tests for LLM code
- Focus tests on: edge cases, boundary conditions, empty inputs
- Don't trust LLM code without testing extreme inputs
```

### Week 3: Architectural Hallucination Detection (MLOps-Specific)

#### Exercise 1: Evaluate LLM System Design

**Prompt:**

``` text
Design architecture for real-time ML prediction system:
- 10K IoT devices sending 1 reading/second each
- Extract features, run predictions, store results, serve via API
- Include: data flow, tech stack, scaling strategy, error handling
```

Evaluate using taste rubric:

``` markdown
# Architectural Review

| Component | LLM Proposed | Taste Smell | Rating | Issue | Better Approach |
|-----------|-------------|-------------|--------|-------|-----------------|
| Data ingestion | | | | | |
| Processing | | | | | |
| Feature computation | | | | | |
| Model serving | | | | | |
| Storage | | | | | |
| Error handling | | | | | |
| Scaling | | | | | |
| Monitoring | | | | | |

### Overall Assessment

**Critical flaws:**
1. ___
2. ___
3. ___

**What the LLM got right:**
1. ___

**Corrected architecture:**
[Draw or describe your version]
```

#### Exercise 2: Model Monitoring Design (MLOps-Specific)

**Prompt:**

``` text
Design a model monitoring and automated retraining system for my weather 
prediction pipeline. Handle concept drift, data drift, and model degradation. 
Include retraining triggers and rollback strategy.
```

Evaluate:

``` markdown
# Model Monitoring Review

### Does the LLM design handle:

| Concern | Addressed? | Quality | What's Missing | My Fix |
|---------|-----------|---------|---------------|--------|
| Concept drift detection | | | | |
| Data drift detection | | | | |
| Training/serving skew | | | | |
| When NOT to retrain | | | | |
| Retraining trigger (statistical basis?) | | | | |
| Rollback if new model is worse | | | | |
| A/B testing new model | | | | |
| Cost of retraining | | | | |
| Data quality check before retraining | | | | |

### Common LLM Mistakes in This Domain

**Mistake 1: "Retrain every week"**
- Problem: No thought about WHY or IF retraining is needed
- Cost: Unnecessary compute
- Risk: Could make model worse

**Mistake 2: No statistical test for drift**
- Just says "monitor" without specifics
- How do you know if drift is real vs. noise?

**Mistake 3: Retrain on all data**
- Expensive
- Usually only need recent data
- Old patterns may not be relevant

**Mistake 4: No shadow mode**
- Deploy new model directly to production
- No way to verify it's better

**My corrected design:**
[Your version with specific thresholds, tests, and rollback]
```

### Week 4: Code Review Practice

Review 15 PRs on ML infrastructure repos: - Dagster PRs - MLflow PRs -
Great Expectations PRs

For each PR, write 1-sentence review BEFORE reading other comments:

``` markdown
# PR Review Log

### PR #1234: "Add retry logic to model registry"
**My take (before reading reviews):** Missing exponential backoff
**Actual reviews said:** [compare after reading]
**Did I catch it?** Yes/No
**What I missed:** ___

[Repeat for 15 PRs]

### Accuracy Over Time
| PRs 1-5 | PRs 6-10 | PRs 11-15 |
|---------|----------|-----------|
| Caught ___/5 | Caught ___/5 | Caught ___/5 |

**Am I getting better?** Yes/No
**Evidence:** ___
```

#### Deliverable Phase 5:

-   [ ] LLM decomposition and trust calibration analysis
-   [ ] Property-based test suite catching 5+ edge cases in LLM code
-   [ ] Architectural review of LLM-generated system design
-   [ ] Model monitoring review (MLOps-specific)
-   [ ] PR review accuracy log (15 PRs)
-   [ ] Blog post: "What LLMs get wrong about ML infrastructure"

------------------------------------------------------------------------

## Phase 6: The Capstone --- Real Constraints (2-3 Weeks)

**Goal:** Synthesize everything under realistic pressure. This uses a
DIFFERENT system --- because in real careers, you inherit other people's
code.

### Setup: The Inherited System

Create a deliberately flawed ML pipeline (or have your cohort member
create one):

``` markdown
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

### If working solo:
Fork an intentionally-buggy repo (create one or find community-provided)
Or: Ask LLM to generate a "messy but functional" recommendation pipeline,
then break it in 3-4 subtle ways yourself

### If working with cohort:
Each person creates a buggy pipeline, swaps with another
You fix theirs, they fix yours
```

### Week 1: Triage Under Constraints

You have 2 weeks, limited money, and a demo to deliver.

``` markdown
# Triage Decision

### System Assessment (spend 4 hours max)

| Component | Status | Severity (1-10) | Fix Time | Blocks Demo? |
|-----------|--------|----------------|----------|--------------|
| Data ingestion | | | | |
| Feature engineering | | | | |
| Model training | | | | |
| Model serving | | | | |
| Monitoring | | | | |
| Tests | | | | |
| Documentation | | | | |

### Demo Requirements (from "CEO")

**Must show:**
- ___
- ___

**Nice to have:**
- ___

**Doesn't matter for demo:**
- ___

### Triage Matrix

| Issue | Blocks Demo? | Fix Time | Fix Now? | Rationale |
|-------|-------------|----------|----------|-----------|
| | | | | |

### What I'm Choosing NOT to Fix (and why)

1. ___ — because ___
2. ___ — because ___

### Technical Debt I'm Deliberately Accepting

| Debt | Consequence | When Must Fix | Risk Level |
|------|------------|---------------|------------|
| | | | |

**ADR: Triage Decisions Under Time Constraint**
```

### Week 2: Ship Under Pressure

Build the minimum demo-able product:

``` markdown
# Sprint Plan (10 working days)

### Days 1-3: Fix blockers
- Fix: ___
- Fix: ___
- Test: Manual only (no time for automated)

### Days 4-7: Build demo flow
- Minimum UI (Streamlit or simple frontend)
- Happy path only
- Prepare backup data for when live demo fails

### Days 8-10: Polish and practice
- Demo script (exact clicks, exact words)
- Rehearse 5 times
- Failure recovery plan

### What "Good Enough" Means Here

**For demo:**
- Works for 10 minutes straight
- Handles 1 user
- Looks professional

**For production:**
- Works for 24 hours
- Handles 100 users
- Actually tested

**Gap between them:**
- Massive technical debt
- Not scalable
- Not monitored
- No error handling

**This gap is the price of speed.**
```

### Week 3: Post-Funding Reality

Scenario: You got funded! \$2M seed round. But...

``` markdown
# The Aftermath

### Problem: Demo code is now "production"
- Users are signing up
- CEO hired salespeople
- Can't stop the business to refactor

### Refactor Strategy (Expand-Contract Pattern)

#### Phase 1: Build new alongside old (Week 1-2)
- Build proper version with tests, monitoring
- Dual-write to both systems
- Users still on old system

#### Phase 2: Gradual migration (Week 3-4)
- 10% of users route to new system
- Monitor error rates, latency, accuracy
- Rollback ready: Can switch back in 1 minute

#### Phase 3: Increase to 50% (Week 5)
- If 10% went well, route half to new
- Monitor comparative metrics

### Phase 4: Full migration (Week 6)
- 100% on new system
- Keep old running for 1 week (safety)
- Decomm old after 1 week stable

### The Hiring Decision

**You can hire ONE person. Who?**

| Role | What They'd Do | Bottleneck They'd Fix | Why Not? |
|------|---------------|----------------------|----------|
| Backend eng | Ship features faster | Speed | |
| ML engineer | Better models | Accuracy | |
| SRE | Improve reliability | Stability | |
| Data engineer | Fix data quality | Data quality | |

**Decision:** Hire ___ because current bottleneck is ___.

**Trade-offs:**
- What stays slow/broken: ___
- Why that's acceptable: ___

**ADR: First Hire Decision**
```

#### Deliverable Phase 6:

-   [ ] Triage document with rationale
-   [ ] Demo sprint plan (what you actually delivered)
-   [ ] Refactor strategy (expand-contract)
-   [ ] Hiring decision analysis
-   [ ] Reflection: "What did constraints teach me about taste?"
-   [ ] Final ADR count: \_\_\_ (target: 15-25 total)
-   [ ] Blog post: "What I learned building under constraints"

------------------------------------------------------------------------

## Monthly Practices (Throughout All Phases)

### Monthly Taste Calibration: Blind Architecture Review

**Do this once per month, starting after Phase 1A.**

**1. Find 3 ML pipeline repos on GitHub**

-   Search: "ML pipeline" or "MLOps" or "feature pipeline"

**2. Before reading code, predict (10 minutes per repo):**

``` markdown
# Blind Review #___ : [Repo Name]
**Date:** ___
**Based on README and architecture diagram ONLY**

### Taste Smells I Predict

- [ ] Hidden coupling: Where? ___
- [ ] Implicit assumptions: Where? ___
- [ ] Proportionality violations: Where? ___
- [ ] Time bombs: Where? ___
- [ ] Operational blindness: Where? ___
- [ ] Cargo culting: Where? ___
- [ ] Cleverness over clarity: Where? ___

### Specific Predictions

**What breaks first at 10x scale:** ___
**Confidence:** Low / Medium / High

**Ugliest part:** ___
**Confidence:** Low / Medium / High

**Architecture rating:** ___/10
**Main reason for score:** ___
```

**3. Read issues, PRs, and discussions**

**4. Compare predictions to reality:**

``` markdown
## Reality Check

**What actually broke (from issues):** ___
**Did I predict it?** Yes / No
**If no, why did I miss it?** ___

**What contributors complained about:** ___
**Did I predict it?** Yes / No
**If no, why?** ___

**My rating was ___/10, should have been ___/10**
**What signals did I miss?** ___

### Score This Review

| Category | Predicted Correctly? | Points |
|----------|---------------------|--------|
| What breaks at scale | Yes/No | 0 or 3 |
| Ugliest part | Yes/No | 0 or 3 |
| Hidden coupling | Yes/No | 0 or 1 |
| Time bombs | Yes/No | 0 or 1 |
| Operational blindness | Yes/No | 0 or 1 |
| Proportionality | Yes/No | 0 or 1 |
| **Total** | | **/ 10** |
```

**5. Track month-over-month:**

``` markdown
# Taste Development Tracking

| Month | Repos Reviewed | Avg Score | Biggest Blind Spot | Progress Note |
|-------|---------------|-----------|-------------------|---------------|
| 1 | 3 | /10 | | |
| 2 | 3 | /10 | | |
| 3 | 3 | /10 | | |
| 4 | 3 | /10 | | |
| 5 | 3 | /10 | | |
| 6 | 3 | /10 | | |

**Target: 70%+ by month 6**
```

------------------------------------------------------------------------

### The 6-Month Return

**Do this 1 month after completing Phase 3.**

``` markdown
# Maintainability Self-Review

**Instructions:** Wait 1 month, then return to your Phase 1A code cold.

### The Test

1. Don't review code beforehand
2. Try to add a feature (e.g., add a second model, add a new data source)
3. Fix a bug you intentionally introduce
4. Time yourself

### Results

**Time to understand code flow:** ___ minutes

**Could I add feature successfully?** Yes / No

**If no, what blocked me?** ___

### What "Past Me" Did That "Maintenance Me" Hates

1. ___
2. ___
3. ___

### The 2 AM Test

**Scenario:** It's 2 AM. Predictions are returning errors.

**Could I find the problem using only logs/metrics?** Yes / No

**How long would it take?** ___ minutes

**What's missing that would help?**
- Better logs: ___
- More metrics: ___
- Clearer structure: ___

### Comparison: Then vs. Now

| Aspect | Then | Now | Why the change |
|--------|------|-----|---------------|
| Architecture | | | |
| Logging | | | |
| Error handling | | | |
| Code structure | | | |

### Taste Growth Evidence

**The biggest change in my thinking from Phase 1A to now:**
___

**Evidence this is intuition, not knowledge:**
- Can I explain why without notes? Yes / No
- Do I "feel" what's wrong before I can articulate it? Yes / No
- Have I applied this in other projects? Yes / No
```

------------------------------------------------------------------------

### The Ultimate Taste Test

**Do this after completing all phases.**

#### Test 1: The 5-Minute Architecture Review

-   [ ] Find a new ML pipeline repo on GitHub (never seen before)
-   [ ] Set timer: 5 minutes
-   [ ] Write down: What breaks, what's ugly, what you'd change, rating

``` markdown
# 5-Minute Review: [Repo]

**Time limit:** 5 minutes

### Predictions
- Breaks first: ___
- Ugliest: ___
- Would change: ___
- Rating: ___/10

### After reading issues/PRs
- Actual problems: ___
- Accuracy: ___% (what I caught / what existed)

**Did I score 70%+?** Yes / No
```

#### Test 2: The Design Review Simulation

Junior engineer proposes:

``` python
@app.post("/predict")
def predict(user_id: str):
    # Fetch all user history
    history = db.query("SELECT * FROM events WHERE user_id = %s", user_id)
    
    # Compute features from full history
    features = compute_features(history)  # 500ms
    
    # Make prediction
    prediction = model.predict(features)  # 100ms
    
    return {"prediction": prediction}
```

Can you (in \< 2 minutes):

**Spot the flaws?**

-   Unbounded query (history grows forever)
-   Synchronous 500ms computation
-   No caching (recomputes same features)
-   No timeout on DB query
-   No fallback if DB is slow

**Explain WHY each is flawed (not just "it's bad")?**

**Suggest better approaches with trade-offs?**

-   Pre-compute features → but not real-time
-   Cache features → but cache invalidation
-   Limit history window → but miss patterns

**Acknowledge when simple might be fine?**

-   At 10 users? This code is perfectly adequate

#### Test 3: Boris's Three Questions

For any system you encounter, can you answer:

**What do we build?** - Not "what's in the ticket" - But "what problem
are we solving?"

**Why? For whom?** - Not "because PM said so" - But "because these users
have this pain"

**How does it all fit together?** - Not "my service works" - But
"system + network + users = working system"

------------------------------------------------------------------------

## Graduation Criteria

### Technical Taste

-   [ ] Can predict failure modes from architecture diagram
-   [ ] Can explain WHY designs are ugly using taste vocabulary
-   [ ] Can suggest alternatives with explicit trade-offs
-   [ ] Can spot when LLM-generated code/architecture will fail
-   [ ] Knows when simple beats clever (and when it doesn't)

### Operational Taste

-   [ ] Can debug production issues using only observability tools
-   [ ] Can make triage decisions under time pressure
-   [ ] Understands cost implications of architecture choices
-   [ ] Knows when "good enough" beats "perfect"

### Product Taste

-   [ ] Can make build/don't-build decisions with evidence
-   [ ] Can interview users without leading them (Mom Test)
-   [ ] Understands unit economics of the systems they build

### Communication Taste

-   [ ] Can explain complex systems to non-technical stakeholders
-   [ ] Writes ADRs that help future engineers understand decisions
-   [ ] Provides code reviews that teach, not just criticize
-   [ ] Can defend technical decisions under hostile questioning

------------------------------------------------------------------------

## Graduation Validation

**Don't self-assess. Get external validation:**

**Minimum bar (required):**

-   [ ] 2 experienced engineers reviewed your work and said "This is
    solid mid-level work"
-   [ ] You scored 70%+ on monthly taste calibration (last 3 months
    average)
-   [ ] You can whiteboard your Phase 1 architecture and answer hostile
    questions

**Ideal bar (aspirational):**

-   [ ] 3 staff+ engineers said "I'd hire someone who built this"
-   [ ] You've contributed meaningfully to open source (merged PR with
    good design discussion)
-   [ ] You've written 3+ blog posts that got engagement (comments, not
    just views)

**If you can't hit minimum bar:**

-   You completed exercises but didn't develop taste
-   That's okay --- taste takes time
-   Either: Continue practicing, or get a job with strong mentorship

------------------------------------------------------------------------

## Your Portfolio After Completion

### What You Actually Have

**1. A Production ML System**

-   Complete pipeline, deployed to VPS
-   Tested at scale with documented bottlenecks and resource constraints
-   Resilient to failures (with evidence from chaos testing)
-   Cost-analyzed and optimized
-   Possibly pivoted to new domain based on user research

**2. Architecture Decision Records (15-25)**

-   Every major decision documented with rationale and trade-offs
-   Shows your thinking, not just your code
-   Evidence of judgment development

**3. Taste Development Evidence**

-   Monthly blind review accuracy logs (hopefully showing improvement)
-   Expert feedback gap analyses
-   Beautiful systems study
-   Post-mortems from incidents

**4. Business Judgment Artifacts**

-   User interview notes (Mom Test format)
-   Build/pivot/kill decisions with evidence
-   Unit economics analysis
-   Hiring decision analysis

**5. AI Oversight Skills**

-   LLM trust calibration framework
-   Property-based test suites
-   Architectural hallucination detection examples

------------------------------------------------------------------------

### What This Portfolio Actually Gets You

**It will help with:**

-   Junior to Mid transition (shows self-direction)
-   Startups (demonstrates breadth)
-   Technical discussions with experienced engineers (you speak the
    language)
-   Interview conversations (you can debate trade-offs intelligently)

**It will NOT help with:**

-   FAANG interviews (they want LeetCode + classic system design)
-   Senior+ roles (they want years of impact, not projects)
-   "X years required" filters (portfolio does not equal experience)
-   Roles requiring deep specialization

**Realistic job targets after this curriculum:**

-   Mid-level MLOps engineer at Series A startup
-   Junior/Mid ML platform engineer at tech company
-   Founding engineer at very early startup (if paired with domain
    expertise)

**NOT realistic:**

-   Staff engineer at Google (need 8+ YOE + organizational impact)
-   Senior at established company (usually need 5+ YOE)
-   Principal anywhere (need 10+ YOE + cross-org influence)

**The value is the taste you developed, not the resume line.**

**This curriculum gives you:**

-   Demonstrated judgment (ADRs, decisions, trade-off analysis)
-   Real project portfolio (deployed system with evidence of thoughtful
    design)
-   Articulate thinking about systems (blog posts, documented decisions)

**It does NOT substitute for:**

-   Years of production experience
-   Organizational navigation skills
-   Cross-team coordination
-   Managing technical debt at scale
-   Political skills needed at larger companies

**Be honest about what you have vs. what you need for specific roles.**

------------------------------------------------------------------------

## Resources

### Books

-   **Designing Data-Intensive Applications** — Martin Kleppmann (Phases 1-2)
-   **Release It!** — Michael Nygard (Phase 3)
-   **The Mom Test** — Rob Fitzpatrick (Phase 4)
-   **Observability Engineering** — Charity Majors et al. (Phase 2-3)
-   **Building Machine Learning Pipelines** — Hapke & Nelson (throughout)
-   🔧 **The Linux Command Line** — William Shotts (VPS users)
-   🔧 **Systems Performance** — Brendan Gregg (VPS deep dive)

### Online Resources

-   [Made With ML](https://madewithml.com) — MLOps fundamentals
-   [Full Stack Deep Learning](https://fullstackdeeplearning.com) — Production ML
-   [SRE Weekly](https://sreweekly.com) — Incident reports and operational wisdom
-   [DigitalOcean Tutorials](https://www.digitalocean.com/community/tutorials) — Linux & DevOps
-   [Hetzner Docs](https://docs.hetzner.com/) — VPS setup guides
-   [LinuxJourney](https://linuxjourney.com) — Interactive Linux learning

### VPS-Specific Learning

**Linux Fundamentals:**
-   [Linux Survival](https://linuxsurvival.com) — Interactive command line tutorial
-   [Explain Shell](https://explainshell.com) — Understand any shell command
-   [htop explained](https://peteris.rocks/blog/htop/) — System monitoring deep dive

**Docker & Systemd:**
-   [Docker Curriculum](https://docker-curriculum.com)
-   [Systemd by Example](https://systemd-by-example.com)
-   [Understanding systemd](https://www.digitalocean.com/community/tutorials/systemd-essentials-working-with-services-units-and-the-journal)

**Nginx & Reverse Proxy:**
-   [Nginx Beginner's Guide](https://nginx.org/en/docs/beginners_guide.html)
-   [SSL/TLS Best Practices](https://wiki.mozilla.org/Security/Server_Side_TLS)
-   [Let's Encrypt Documentation](https://letsencrypt.org/docs/)

**PostgreSQL Administration:**
-   [PostgreSQL Tutorial](https://www.postgresqltutorial.com)
-   [Tuning PostgreSQL](https://wiki.postgresql.org/wiki/Tuning_Your_PostgreSQL_Server)
-   [PostgreSQL Monitoring](https://www.cybertec-postgresql.com/en/monitoring-postgresql-performance/)

### Communities

-   [MLOps Community Slack](https://mlops.community/)
-   [r/MLOps](https://reddit.com/r/mlops)
-   [r/ExperiencedDevs](https://reddit.com/r/ExperiencedDevs)
-   🔧 [r/selfhosted](https://reddit.com/r/selfhosted) — Self-hosting community
-   🔧 [r/linuxadmin](https://reddit.com/r/linuxadmin) — Linux systems administration
-   🔧 [Hacker News](https://news.ycombinator.com) — Tech discussions

### Tools Documentation

-   [Dagster](https://docs.dagster.io)
-   [MLflow](https://mlflow.org/docs)
-   [MinIO](https://min.io/docs/minio/linux/index.html) — S3-compatible storage
-   [Hypothesis](https://hypothesis.readthedocs.io) — Property-based testing
-   [Locust](https://docs.locust.io) — Load testing
-   [Prometheus](https://prometheus.io/docs/introduction/overview/)
-   [Grafana](https://grafana.com/docs/)

### VPS Providers Comparison

| Provider | Best For | Monthly Cost | Locations | Notes |
|----------|----------|--------------|-----------|-------|
| [Hetzner](https://www.hetzner.com/cloud) | Best value | €4-20 | EU (Germany, Finland) | Excellent specs for price |
| [DigitalOcean](https://www.digitalocean.com) | Documentation | $6-24 | Worldwide | Great tutorials |
| [Vultr](https://www.vultr.com) | Global reach | $6-24 | 25+ locations | Similar to DO |
| [Linode](https://www.linode.com) | Reliability | $5-20 | Worldwide | Akamai-backed |
| [OVH](https://www.ovhcloud.com) | Budget | €3-15 | EU/US | Very cheap, variable quality |

------------------------------------------------------------------------

## Start Now

### Choose Your Path

**🔧 VPS Edition First Actions:**

-   [ ] Create a public GitHub repo for this curriculum
-   [ ] Sign the Three Agreements (write it down, share with someone)
-   [ ] Provision a VPS ($6-10/month — Hetzner or DigitalOcean)
-   [ ] Register a domain name ($10/year — Namecheap, Porkbun, Cloudflare)
-   [ ] SSH into your server and complete Phase 0 setup
-   [ ] Configure firewall, Nginx, SSL certificate
-   [ ] Deploy docker-compose stack (PostgreSQL, MinIO, Prometheus, Grafana)
-   [ ] Install tools: `pip install dagster dagster-webserver mlflow fastapi locust`
-   [ ] Join MLOps Community Slack
-   [ ] Write your first blog post: "Why I'm doing this curriculum (VPS edition)"
-   [ ] Tell one person you're doing this (accountability)
-   [ ] Block Phase 0 time on your calendar (this week)
-   [ ] Set Phase 1A target completion date: ___________

**First Actions:**
**Your start date:** ___________

**Your infrastructure:** VPS (This curriculum is VPS-only)

**Your community tier target:** Tier ___ initially, upgrade to Tier ___ by Phase 3

**Expected monthly cost:**
- VPS: $10-15/month (flat, predictable)
- Total: $12-17/month (predictable, flat rate)

------------------------------------------------------------------------

## Final Thoughts

> "The recipe for great work is: very exacting taste, plus the ability to gratify it."  
> — Paul Graham

**AI has solved "the ability to gratify it."**

**This curriculum develops taste.**

**Taste requires:**

-   Hard problems
-   Failure and reflection
-   Expert feedback
-   Community
-   Time
-   Honesty about what's working and what isn't
-   🔧 **Constraints** — VPS limits force better decisions

**There is no shortcut.**

Persistence is part of taste. Most people quit when it gets hard. The ones who don't are the ones who develop real judgment.

But persistence alone isn't enough. You also need honesty — the ability to recognize when something isn't working and pivot.

**VPS teaches systems thinking. Everything else builds on that foundation.**

**Constraint builds taste.**

**Be persistent, but be honest.**

---

## Final Notes

**For VPS Users:**
- When your server crashes at 2 AM, you'll learn more than any tutorial can teach
- SSH'ing into a broken system develops deep operational intuition
- Every resource constraint forces better architecture decisions
- Document EVERYTHING — your future self will thank you

**Remember:**
- Fixed costs force better architectural decisions than unlimited budgets
- Document resource constraints as carefully as technical decisions
- Understand what auto-scaling is hiding from you
- Know when to drop down to VPS-level thinking

**For Everyone:**
- The goal isn't perfect code — it's developing judgment
- Share your failures publicly (they teach more than successes)
- Get feedback early and often
- Remember: This is a 8-12 month journey, not a sprint

---

**Good luck. Build something real.**

May your servers stay up and your logs be readable.



**Now stop reading and start building.**

------------------------------------------------------------------------

## Final Notes

This styled version preserves all original content while improving: -
Visual hierarchy - Section separation - Readability - Emphasis
consistency - Markdown structure