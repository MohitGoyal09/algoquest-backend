# 🛡️ Sentinel Backend

> **AI-Powered Employee Insights Engine**  
> The core intelligence hub implementing the "Three Engines" architecture with privacy-first principles.

[![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=flat&logo=fastapi&logoColor=white)](https://fastapi.tiangolo.com)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-316192?style=flat&logo=postgresql&logoColor=white)](https://www.postgresql.org)
[![Python](https://img.shields.io/badge/Python-3.11+-3776AB?style=flat&logo=python&logoColor=white)](https://www.python.org)
[![License](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

---

## 📋 Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Tech Stack](#tech-stack)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Configuration](#configuration)
- [Running the Application](#running-the-application)
- [API Documentation](#api-documentation)
- [Architecture Overview](#architecture-overview)
- [Database Schema](#database-schema)
- [The Three Engines](#the-three-engines)
- [Development Guide](#development-guide)
- [Deployment](#deployment)
- [Security & Privacy](#security--privacy)

---

## Overview

Sentinel Backend is a sophisticated AI-powered employee insights platform designed to proactively detect burnout, identify hidden talent, and monitor team health while maintaining strict privacy standards. Built on a "Three Engines" architecture, it analyzes behavioral patterns through a privacy-preserving "Two-Vault" system.

### Key Capabilities

- 🔮 **Predictive Burnout Detection**: Identify at-risk employees up to 30 days in advance
- 💎 **Hidden Gem Discovery**: Uncover high-impact contributors through network analysis
- 🌡️ **Culture Health Monitoring**: Detect team-level sentiment shifts and resignation contagion
- 🔒 **Privacy by Design**: Zero-knowledge architecture with cryptographic separation

---

## Features

### 🚀 Three-Engine System

| Engine | Purpose | Key Metrics |
|--------|---------|-------------|
| **Safety Valve** | Burnout detection & prevention | Sentiment velocity, circadian entropy, belongingness score |
| **Talent Scout** | Hidden gem identification | Betweenness centrality, eigenvector centrality, unblocking count |
| **Culture Thermometer** | Team health monitoring | Graph fragmentation, communication decay, contagion risk |

### 🔐 Two-Vault Privacy Architecture

- **Vault A (Analytics)**: Stores anonymized behavioral hashes and events
- **Vault B (Identity)**: Stores encrypted identity mapping with audit trails
- **Zero-Knowledge**: Analytics engine never processes PII directly

### 📡 Real-Time Capabilities

- **WebSocket Updates**: Live risk score updates to dashboards
- **Event Streaming**: Real-time behavioral event injection for demos
- **Simulation System**: Digital twins for testing and demonstration

### 🧪 Simulation & Testing

- **Digital Twins**: Create realistic employee personas with synthetic data
- **Event Injection**: Simulate real-world scenarios (late nights, conflicts, achievements)
- **Scenario Testing**: Validate engine responses in controlled environments

---

## Tech Stack

### Core Framework
- **[FastAPI](https://fastapi.tiangolo.com/)** - Modern, high-performance web framework
- **[SQLAlchemy](https://www.sqlalchemy.org/)** - SQL toolkit and ORM
- **[Pydantic](https://docs.pydantic.dev/)** - Data validation using Python type hints

### Data & Analytics
- **[PostgreSQL](https://www.postgresql.org/)** - Primary database (supports Supabase)
- **[NetworkX](https://networkx.org/)** - Graph analysis and network metrics
- **[NumPy](https://numpy.org/) / [SciPy](https://scipy.org/)** - Numerical computing and statistics

### AI & LLM Integration
- **[LiteLLM](https://docs.litellm.ai/)** - Universal LLM API gateway
- **Provider Agnostic**: Supports OpenAI, Gemini, Anthropic, Grok, and more

### Real-Time Communication
- **WebSocket Protocol** - Bidirectional communication for live updates
- **Async Support** - Full async/await implementation for scalability

---

## Prerequisites

### Required

- **Python 3.11+** - [Download](https://www.python.org/downloads/)
- **PostgreSQL 14+** - Local instance or [Supabase](https://supabase.com/) account
- **Git** - For cloning the repository

### Optional

- **Docker** - For containerized deployment
- **Docker Compose** - For multi-service orchestration
- **uv** - Fast Python package installer (recommended)

### System Requirements

- **RAM**: 4GB minimum, 8GB recommended
- **Storage**: 2GB for application, additional space for database
- **Network**: Outbound HTTPS for LLM API calls

---

## Installation

### Option 1: Docker (Recommended for Quick Start)

```bash
# Clone the repository
git clone <repository-url>
cd sentinel/backend

# Start with Docker Compose
docker-compose up --build
```

### Option 2: Local Development

#### Step 1: Environment Setup

```bash
# Navigate to backend directory
cd backend

# Create virtual environment (using venv)
python -m venv .venv

# Activate virtual environment
# Windows:
.venv\Scripts\activate
# macOS/Linux:
source .venv/bin/activate
```

#### Step 2: Install Dependencies

**Using uv (Recommended - Faster):**
```bash
# Install uv if not already installed
pip install uv

# Install dependencies
uv pip install -r requirements.txt
```

**Using pip:**
```bash
pip install -r requirements.txt
```

#### Step 3: Environment Configuration

```bash
# Copy example environment file
cp .env.example .env

# Edit .env with your credentials
# See Configuration section for details
```

#### Step 4: Database Initialization

```bash
# The application will auto-create tables on first run
# For production, use Alembic migrations:
# alembic upgrade head
```

---

## Configuration

### Environment Variables

Create a `.env` file in the `backend/` directory with the following variables:

#### Database Configuration

| Variable | Description | Required | Example |
|----------|-------------|----------|---------|
| `DATABASE_URL` | PostgreSQL connection string | ✅ | `postgresql://user:pass@host:5432/db` |

#### Security Keys

| Variable | Description | Required | Example |
|----------|-------------|----------|---------|
| `VAULT_SALT` | Salt for identity hashing | ✅ | `random-salt-string-32-chars` |
| `ENCRYPTION_KEY` | Fernet 32-byte encryption key | ✅ | `base64-encoded-key` |

**Generating Encryption Key:**
```python
from cryptography.fernet import Fernet
key = Fernet.generate_key()
print(key.decode())  # Copy this to ENCRYPTION_KEY
```

#### LLM Configuration

| Variable | Description | Default | Options |
|----------|-------------|---------|---------|
| `LLM_PROVIDER` | LLM provider | `gemini` | `gemini`, `openai`, `anthropic` |
| `LLM_MODEL` | Model name | `gemini-pro` | Provider-specific |
| `LLM_API_KEY` | API key for chosen provider | - | Your API key |
| `OPENAI_API_KEY` | OpenAI-specific key | - | Your OpenAI key |

#### External Integrations

| Variable | Description | Required |
|----------|-------------|----------|
| `SLACK_BOT_TOKEN` | Slack Bot OAuth token | ❌ |
| `PAGERDUTY_API_KEY` | PagerDuty API key | ❌ |
| `JIRA_API_KEY` | Jira API key | ❌ |
| `GOOGLE_CALENDAR_KEY` | Google Calendar API key | ❌ |

#### Application Settings

| Variable | Description | Default |
|----------|-------------|---------|
| `SIMULATION_MODE` | Enable simulation features | `True` |
| `DATA_RETENTION_DAYS` | Days to retain analytics data | `90` |

### Complete `.env` Example

```env
# Database
DATABASE_URL=postgresql://postgres:password@localhost:5432/sentinel

# Security
VAULT_SALT=your-random-salt-string-here
ENCRYPTION_KEY=your-fernet-generated-key-here

# LLM (using Gemini)
LLM_PROVIDER=gemini
LLM_MODEL=gemini-pro
LLM_API_KEY=your-gemini-api-key

# Optional Integrations
SLACK_BOT_TOKEN=xoxb-your-slack-token
OPENAI_API_KEY=sk-your-openai-key

# Application
SIMULATION_MODE=true
DATA_RETENTION_DAYS=90
```

---

## Running the Application

### Local Development

```bash
# Start development server with hot reload
uvicorn app.main:app --reload --host 0.0.0.0 --port 8000

# Or using Python module
python -m uvicorn app.main:app --reload
```

The API will be available at:
- **API Base**: http://localhost:8000
- **Interactive Docs**: http://localhost:8000/docs (Swagger UI)
- **Alternative Docs**: http://localhost:8000/redoc (ReDoc)

### Docker

```bash
# Build and run
docker-compose up --build

# Run in background
docker-compose up -d

# View logs
docker-compose logs -f backend

# Stop
docker-compose down
```

### Production

```bash
# Using Gunicorn with Uvicorn workers
gunicorn app.main:app -w 4 -k uvicorn.workers.UvicornWorker --bind 0.0.0.0:8000

# Or with environment variables
ENVIRONMENT=production uvicorn app.main:app --host 0.0.0.0 --port 8000
```

---

## API Documentation

### Base URL

```
Development: http://localhost:8000
Production:  https://your-domain.com
```

### Authentication

Currently, the API uses hash-based identification. Each user is identified by a SHA-256 hash of their email, ensuring privacy while maintaining unique identification.

### Core Endpoints

#### Health Check

```http
GET /health
```

**Response:**
```json
{
  "status": "healthy",
  "version": "1.0.0"
}
```

#### Root Endpoint

```http
GET /
```

**Response:**
```json
{
  "status": "Sentinel",
  "engines": ["Safety Valve", "Talent Scout", "Culture Thermometer"]
}
```

### Engine Endpoints

#### Safety Valve - Burnout Analysis

```http
GET /api/v1/engines/users/{user_hash}/safety
```

**Response:**
```json
{
  "success": true,
  "data": {
    "engine": "Safety Valve",
    "risk_level": "ELEVATED",
    "velocity": 2.1,
    "confidence": 0.87,
    "belongingness_score": 0.45,
    "circadian_entropy": 0.72,
    "indicators": {
      "late_night_pattern": true,
      "weekend_work": false,
      "communication_decline": true
    }
  }
}
```

#### Talent Scout - Network Analysis

```http
GET /api/v1/engines/users/{user_hash}/talent
```

**Response:**
```json
{
  "success": true,
  "data": {
    "engine": "Talent Scout",
    "top_performers": [
      {
        "user_hash": "a1b2c3...",
        "betweenness": 0.85,
        "eigenvector": 0.72,
        "unblocking": 12,
        "is_hidden_gem": true
      }
    ]
  }
}
```

#### Culture Thermometer - Team Analysis

```http
POST /api/v1/engines/teams/culture
Content-Type: application/json

{
  "team_hashes": ["hash1", "hash2", "hash3"]
}
```

**Response:**
```json
{
  "success": true,
  "data": {
    "engine": "Culture Thermometer",
    "team_risk": "ELEVATED",
    "metrics": {
      "avg_velocity": 1.8,
      "critical_members": 1,
      "graph_fragmentation": 0.65,
      "comm_decay_rate": 0.23
    },
    "recommendation": "Schedule team retrospective within 48 hours"
  }
}
```

### Simulation Endpoints

#### Create Persona

```http
POST /api/v1/engines/personas
Content-Type: application/json

{
  "email": "demo@example.com",
  "persona_type": "alex_burnout"
}
```

**Persona Types:**
- `alex_burnout` - High burnout risk pattern
- `sarah_gem` - Hidden gem (high centrality, low visibility)
- `jordan_steady` - Stable baseline pattern
- `maria_contagion` - Team contagion risk pattern

**Response:**
```json
{
  "success": true,
  "data": {
    "user_hash": "sha256-hash",
    "events_count": 150,
    "persona": "alex_burnout"
  }
}
```

#### Inject Real-Time Event

```http
POST /api/v1/engines/events
Content-Type: application/json

{
  "user_hash": "sha256-hash",
  "current_risk": "ELEVATED"
}
```

### Context Enrichment

```http
GET /api/v1/engines/users/{user_hash}/context?timestamp=2024-01-15T10:00:00Z
```

**Response:**
```json
{
  "success": true,
  "data": {
    "user_hash": "sha256-hash",
    "timestamp": "2024-01-15T10:00:00",
    "context": {
      "is_explained": true,
      "explanation": "On-call rotation",
      "source": "pagerduty"
    }
  }
}
```

### WebSocket Protocol

Connect to WebSocket for real-time updates:

```javascript
// Personal dashboard connection
const ws = new WebSocket('ws://localhost:8000/ws/{user_hash}');

// Admin/team dashboard connection
const ws = new WebSocket('ws://localhost:8000/ws/admin/team');
```

**Client → Server Messages:**

```json
// Ping to keep connection alive
{"action": "ping"}

// Request immediate update
{"action": "request_update"}
```

**Server → Client Messages:**

```json
// Pong response
{"type": "pong", "timestamp": "2024-01-15T10:00:00Z"}

// Risk update
{
  "type": "risk_update",
  "data": {
    "user_hash": "...",
    "risk_level": "CRITICAL",
    "velocity": 3.2
  }
}

// Manual refresh response
{
  "type": "manual_refresh",
  "data": { /* full analysis */ }
}
```

---

## Architecture Overview

### Directory Structure

```
backend/
├── app/
│   ├── api/              # API layer
│   │   ├── v1/           # API version 1
│   │   │   ├── endpoints/# Route handlers
│   │   │   └── api.py    # Router aggregation
│   │   ├── deps.py       # Dependencies (DB session, auth)
│   │   └── websocket.py  # WebSocket handlers
│   ├── core/             # Core infrastructure
│   │   ├── config.py     # Application settings
│   │   ├── database.py   # SQLAlchemy setup
│   │   ├── security.py   # Encryption & hashing
│   │   └── vault.py      # Two-Vault implementation
│   ├── models/           # Database models
│   │   ├── analytics.py  # Vault A models
│   │   └── identity.py   # Vault B models
│   ├── schemas/          # Pydantic models
│   │   └── engines.py    # Request/response schemas
│   └── services/         # Business logic
│       ├── safety_valve.py      # Burnout detection
│       ├── talent_scout.py      # Network analysis
│       ├── culture_temp.py      # Team health
│       ├── simulation.py        # Digital twins
│       ├── context.py           # Context enrichment
│       ├── nudge_dispatcher.py  # Intervention system
│       ├── websocket_manager.py # Connection management
│       ├── llm.py               # LLM integration
│       └── slack.py             # Slack integration
├── tests/                # Test suite
├── .env.example          # Environment template
├── requirements.txt      # Dependencies
├── pyproject.toml        # Project metadata
└── Dockerfile            # Container definition
```

### Two-Vault System Explained

```
┌─────────────────────────────────────────────────────────────┐
│                        VAULT A (Analytics)                   │
│  ┌──────────┐  ┌──────────────┐  ┌──────────────────────┐  │
│  │  Events  │  │  Risk Scores │  │  Graph Edges         │  │
│  │ (hashed) │  │  (hashed)    │  │  (hashed)            │  │
│  └──────────┘  └──────────────┘  └──────────────────────┘  │
│                                                              │
│  • No PII stored                                            │
│  • Used for ML/AI analysis                                  │
│  • Analytics engine operates here                           │
└─────────────────────────────────────────────────────────────┘
                              │
                              │ Hash-based lookup only
                              ▼
┌─────────────────────────────────────────────────────────────┐
│                       VAULT B (Identity)                     │
│  ┌──────────────────┐  ┌──────────────────────────────┐    │
│  │  User Identity   │  │  Audit Logs                  │    │
│  │  (encrypted)     │  │  (immutable)                 │    │
│  │  - email         │  │  - nudge_sent                │    │
│  │  - slack_id      │  │  - data_deleted              │    │
│  └──────────────────┘  └──────────────────────────────┘    │
│                                                              │
│  • PII encrypted with Fernet                                │
│  • Only accessed for high-priority nudges                   │
│  • Complete audit trail                                     │
└─────────────────────────────────────────────────────────────┘
```

### Data Flow

```
┌─────────────┐     ┌──────────────┐     ┌─────────────────┐
│   Event     │────▶│  Hash &      │────▶│   Vault A       │
│   Source    │     │  Encrypt     │     │   (Analytics)   │
└─────────────┘     └──────────────┘     └─────────────────┘
                                                │
                                                ▼
                                         ┌──────────────┐
                                         │  Three       │
                                         │  Engines     │
                                         └──────────────┘
                                                │
                           ┌────────────────────┼────────────────────┐
                           ▼                    ▼                    ▼
                    ┌─────────────┐      ┌─────────────┐      ┌─────────────┐
                   Safety Valve   │     Talent Scout   │     Culture Temp │
                    └─────────────┘      └─────────────┘      └─────────────┘
                           │                    │                    │
                           └────────────────────┼────────────────────┘
                                                ▼
                                         ┌──────────────┐
                                         │  Nudge       │
                                         │  Dispatcher  │
                                         └──────────────┘
                                                │
                           ┌────────────────────┘
                           ▼
                    ┌─────────────┐
                    │  Vault B    │
                    │  (Decrypt   │
                    │   & Notify) │
                    └─────────────┘
```

---

## Database Schema

### Vault A (Analytics Schema)

#### Events Table

| Column | Type | Description |
|--------|------|-------------|
| `id` | Integer (PK) | Auto-increment ID |
| `user_hash` | String(64) | SHA-256 hash of user email |
| `timestamp` | DateTime | Event occurrence time |
| `event_type` | String(50) | Type: commit, pr_review, slack_message, unblocked |
| `target_user_hash` | String(64) | For graph edges (nullable) |
| `metadata` | JSON | Additional event data |

#### Risk Scores Table

| Column | Type | Description |
|--------|------|-------------|
| `user_hash` | String(64) (PK) | User identifier |
| `velocity` | Float | Sentiment velocity score |
| `risk_level` | String(20) | CALIBRATING, LOW, ELEVATED, CRITICAL |
| `confidence` | Float | Confidence score (0-1) |
| `thwarted_belongingness` | Float | Psychological metric |
| `updated_at` | DateTime | Last calculation time |

#### Graph Edges Table

| Column | Type | Description |
|--------|------|-------------|
| `id` | Integer (PK) | Auto-increment ID |
| `source_hash` | String(64) | Source user hash |
| `target_hash` | String(64) | Target user hash |
| `weight` | Float | Interaction frequency |
| `last_interaction` | DateTime | Last interaction timestamp |
| `edge_type` | String(20) | mentorship, collaboration, blocking |

#### Centrality Scores Table

| Column | Type | Description |
|--------|------|-------------|
| `user_hash` | String(64) (PK) | User identifier |
| `betweenness` | Float | Bridge between disconnected groups |
| `eigenvector` | Float | Connected to important people |
| `unblocking_count` | Integer | Times unblocked others |
| `knowledge_transfer_score` | Float | Knowledge sharing metric |
| `calculated_at` | DateTime | Calculation timestamp |

### Vault B (Identity Schema)

#### Users Table

| Column | Type | Description |
|--------|------|-------------|
| `user_hash` | String(64) (PK) | SHA-256 hash (links to Vault A) |
| `email_encrypted` | LargeBinary | Fernet-encrypted email |
| `slack_id_encrypted` | LargeBinary | Fernet-encrypted Slack ID |
| `created_at` | DateTime | Account creation time |

#### Audit Logs Table

| Column | Type | Description |
|--------|------|-------------|
| `id` | Integer (PK) | Auto-increment ID |
| `user_hash` | String(64) | User identifier (indexed) |
| `action` | String(50) | Action type: nudge_sent, data_deleted |
| `details` | JSON | Additional action data |
| `timestamp` | DateTime | Action timestamp |

### Relationships

```
Vault A (Analytics)              Vault B (Identity)
───────────────────              ──────────────────

Events.user_hash ───────────────▶ Users.user_hash
RiskScores.user_hash ───────────▶ Users.user_hash
GraphEdges.source_hash ─────────▶ Users.user_hash
GraphEdges.target_hash ─────────▶ Users.user_hash
AuditLogs.user_hash ────────────▶ Users.user_hash
```

---

## The Three Engines

### 🔥 Safety Valve

**Purpose**: Detect and prevent employee burnout before it becomes critical.

**How It Works**:
1. **Sentiment Velocity Analysis**: Tracks the rate of change in work patterns
2. **Circadian Entropy**: Measures disruption to normal working hours
3. **Thwarted Belongingness**: Detects social disconnection patterns

**Key Metrics**:
- **Velocity Score**: Rate of negative sentiment change
- **Risk Level**: CALIBRATING → LOW → ELEVATED → CRITICAL
- **Confidence**: Statistical confidence in the assessment

**Intervention Triggers**:
- Velocity > 1.5 → ELEVATED risk
- Velocity > 2.5 → CRITICAL risk
- Automatic nudge dispatch at CRITICAL level

### 💎 Talent Scout

**Purpose**: Identify "hidden gems" - high-impact employees who may be overlooked.

**How It Works**:
1. **Network Analysis**: Builds interaction graphs from collaboration data
2. **Centrality Metrics**: Calculates betweenness and eigenvector centrality
3. **Unblocking Detection**: Identifies who removes blockers for others

**Key Metrics**:
- **Betweenness Centrality**: Bridges between disconnected groups
- **Eigenvector Centrality**: Connected to other important people
- **Unblocking Count**: Times helped unblock colleagues
- **Knowledge Transfer Score**: Effectiveness in sharing knowledge

**Hidden Gem Criteria**:
- High betweenness (> 0.7)
- High unblocking count (> 10)
- Low traditional visibility metrics

### 🌡️ Culture Thermometer

**Purpose**: Monitor team-level health and detect resignation contagion risks.

**How It Works**:
1. **Aggregate Analysis**: Combines individual risk scores across the team
2. **Graph Fragmentation**: Measures social cohesion decay
3. **Communication Decay**: Tracks reduction in team interactions

**Key Metrics**:
- **Average Velocity**: Team-wide sentiment trend
- **Critical Members**: Count of individuals at CRITICAL risk
- **Graph Fragmentation**: 0 (cohesive) to 1 (fragmented)
- **Communication Decay Rate**: Rate of interaction decline

**Contagion Risk Levels**:
- **STABLE**: Team is healthy
- **ELEVATED**: Some concerns, monitor closely
- **HIGH_CONTAGION_RISK**: Immediate intervention recommended

---

## Development Guide

### Adding New Features

#### 1. Creating a New Endpoint

```python
# app/api/v1/endpoints/your_feature.py
from fastapi import APIRouter, Depends
from sqlalchemy.orm import Session
from app.api.deps import get_db

router = APIRouter()

@router.get("/your-endpoint")
def your_endpoint(db: Session = Depends(get_db)):
    # Your logic here
    return {"success": True, "data": {}}
```

Register in [`app/api/v1/api.py`](app/api/v1/api.py):

```python
from app.api.v1.endpoints import your_feature
router.include_router(your_feature.router, prefix="/your-feature")
```

#### 2. Adding a New Model

```python
# app/models/analytics.py (for Vault A)
from sqlalchemy import Column, String, Float, DateTime
from app.core.database import Base

class YourModel(Base):
    __tablename__ = "your_models"
    __table_args__ = {"schema": "analytics"}
    
    user_hash = Column(String(64), primary_key=True)
    your_metric = Column(Float)
    created_at = Column(DateTime, default=datetime.utcnow)
```

#### 3. Creating a New Service

```python
# app/services/your_service.py
from sqlalchemy.orm import Session

class YourService:
    def __init__(self, db: Session):
        self.db = db
    
    def analyze(self, user_hash: str):
        # Your analysis logic
        return {"result": "success"}
```

### Testing

```bash
# Run all tests
pytest

# Run with coverage
pytest --cov=app --cov-report=html

# Run specific test file
pytest tests/test_safety_valve.py

# Run with verbose output
pytest -v
```

### Code Style

```bash
# Format with black
black app/

# Lint with ruff
ruff check app/

# Type checking
mypy app/
```

---

## Deployment

### Docker Compose (Recommended)

```yaml
version: '3.8'

services:
  backend:
    build: ./backend
    ports:
      - "8000:8000"
    environment:
      - DATABASE_URL=${DATABASE_URL}
      - VAULT_SALT=${VAULT_SALT}
      - ENCRYPTION_KEY=${ENCRYPTION_KEY}
      - LLM_API_KEY=${LLM_API_KEY}
    restart: unless-stopped
    healthcheck:
      test: ["CMD", "curl", "-f", "http://localhost:8000/health"]
      interval: 30s
      timeout: 10s
      retries: 3
```

### Production Environment Variables

```env
# Database - Use connection pooling
DATABASE_URL=postgresql://user:pass@prod-db:5432/sentinel?sslmode=require

# Security - Use strong, unique keys
VAULT_SALT=prod-random-salt-32-chars-min
ENCRYPTION_KEY=prod-fernet-key-32-bytes

# LLM - Production API keys
LLM_PROVIDER=openai
LLM_MODEL=gpt-4
LLM_API_KEY=sk-prod-key

# Application - Production settings
SIMULATION_MODE=false
DATA_RETENTION_DAYS=365
```

### Cloud Deployment

#### Railway/Render
1. Connect your GitHub repository
2. Set environment variables in dashboard
3. Deploy automatically on push

#### AWS ECS/Fargate
```bash
# Build and push to ECR
docker build -t sentinel-backend .
docker tag sentinel-backend:latest $ECR_REPO:latest
docker push $ECR_REPO:latest

# Deploy to ECS
aws ecs update-service --cluster sentinel --service backend --force-new-deployment
```

#### Kubernetes
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: sentinel-backend
spec:
  replicas: 3
  selector:
    matchLabels:
      app: sentinel-backend
  template:
    metadata:
      labels:
        app: sentinel-backend
    spec:
      containers:
      - name: backend
        image: sentinel-backend:latest
        ports:
        - containerPort: 8000
        envFrom:
        - secretRef:
            name: sentinel-secrets
```

---

## Security & Privacy

### Cryptographic Flow

```
┌─────────────┐     ┌──────────────┐     ┌─────────────────┐
│   Email     │────▶│  SHA-256     │────▶│   user_hash     │
│  (PII)      │     │   + Salt     │     │   (Vault A ID)  │
└─────────────┘     └──────────────┘     └─────────────────┘
                                                │
                                                │
                           ┌────────────────────┘
                           ▼
                    ┌─────────────┐
                    │  Fernet     │
                    │ Encryption  │
                    └─────────────┘
                           │
                           ▼
                    ┌─────────────┐
                    │  Encrypted  │
                    │   Email     │
                    │ (Vault B)   │
                    └─────────────┘
```

### Privacy Guarantees

1. **Zero-Knowledge Analytics**: Vault A never contains PII
2. **Irreversible Hashing**: SHA-256 with salt prevents rainbow table attacks
3. **Encryption at Rest**: All PII encrypted with Fernet (AES-128-CBC + HMAC)
4. **Audit Trail**: Every identity access logged immutably
5. **Right to be Forgotten**: Complete data deletion capability

### Security Best Practices

- Rotate `ENCRYPTION_KEY` annually
- Use unique `VAULT_SALT` per deployment
- Enable SSL/TLS for all connections
- Store secrets in environment variables or secret managers
- Regular security audits of access patterns

---

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](../LICENSE) file for details.

---

## 🤝 Contributing

Contributions are welcome! Please read our [Contributing Guide](../CONTRIBUTING.md) for details on our code of conduct and the process for submitting pull requests.

---

## 📞 Support

- **Documentation**: [Full Documentation](../docs/)
- **Issues**: [GitHub Issues](https://github.com/your-org/sentinel/issues)
- **Discussions**: [GitHub Discussions](https://github.com/your-org/sentinel/discussions)

---

<p align="center">
  Built with ❤️ by the Sentinel Team
</p>
