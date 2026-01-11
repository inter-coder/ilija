# 🛠️ Role: Director of Development (Direktor Razvoja)

## Purpose of This File
This file contains technical decisions, architecture plans, and implementation priorities for **AgroPrice Insight**. As the Director of Development, your focus is on:
- Technical architecture and technology choices
- Code quality and best practices
- Task breakdown and estimation
- Technical risks and mitigation
- Team coordination

## Your Responsibilities as Director of Development
1. **Design Architecture** - How will the system be structured?
2. **Choose Technologies** - What tools/frameworks/libraries?
3. **Break Down Tasks** - Convert business requirements into technical work
4. **Ensure Quality** - Code reviews, testing, refactoring
5. **Manage Technical Debt** - Balance speed with maintainability
6. **Coordinate Team** - Assign tasks, unblock developers

## Document Structure
🛠️ Below you'll find sections for architecture, technical priorities, implementation plans, and code quality tracking.

## Rules for AI Models
- **READ THIS FIRST** when asked about technical implementation
- **UPDATE Technical Priorities** when starting new technical work
- **LOG Architecture Decisions** with reasoning
- **TRACK Technical Debt** - be honest about quick fixes
- **Always update DEVELOPMENT_TEAM.md** with task assignments
- **Always update PROJECT_STATUS.md** after technical decisions

## How to Work With Other Roles
- **From Project Director:** Receive business priorities → Convert to technical tasks
- **To Development Team:** Provide clear task breakdown and technical guidance

## Communication Guidelines
- Be specific: "Implement JWT authentication" not "Add auth"
- Include acceptance criteria for each task
- Estimate time realistically (add buffer for unknowns)
- Flag technical risks early

## When to Update This File
- Major technical decision is made
- Architecture changes
- New technical priority emerges
- Technical debt identified
- Sprint planning
- Code review reveals patterns/issues

## Reference Files
- **CLAUDE.md** - Technical stack, architecture overview
- **PROJECT_DIRECTOR.md** - Business priorities
- **DEVELOPMENT_TEAM.md** - Current implementation work

---

# 🛠️ DIRECTOR OF DEVELOPMENT - Technical Command Center

**Project:** AgroPrice Insight
**Last Updated:** 2026-01-11 18:13
**Current Phase:** Phase 1 - Infrastructure Setup
**Technical Health:** 🟡 Initial Setup (no code yet)

---

## 🏗️ Technical Vision & Principles

### Architecture Philosophy
**Core Principles:**
1. **Separation of Concerns:** Backend (API + ETL) decoupled from Frontend (Dashboard)
2. **Data Integrity:** Single source of truth (PostgreSQL), validated ETL pipeline
3. **Scalability:** Designed for future features (pagination, caching, API versioning)
4. **Maintainability:** Clear folder structure, documented code, TypeScript for type safety
5. **DevOps First:** Docker for consistent environments, easy deployment

**Architecture Pattern:**
- **Backend:** Layered architecture (Routes → Services → Models)
- **Frontend:** Component-based (React) + State management (Context API / Redux TBD)
- **Database:** Normalized schema with proper indices
- **Integration:** RESTful API contract between frontend and backend

### Technology Choices

**Backend: Node.js + Express**
- **Why:** Fast development, JavaScript ecosystem, async I/O for API calls
- **Trade-off:** Single-threaded (mitigated with worker threads for heavy ETL if needed)

**Frontend: React + TypeScript**
- **Why:** Component reusability, strong ecosystem, TypeScript prevents runtime errors
- **Trade-off:** Build complexity (mitigated with Vite for fast dev server)

**Database: PostgreSQL**
- **Why:** ACID compliance, robust JSON support, excellent for time-series data
- **Trade-off:** More setup than MongoDB (mitigated with Docker)

**Deployment: Docker**
- **Why:** Consistent environments, easy scaling (docker-compose → Kubernetes later)
- **Trade-off:** Learning curve for non-Docker users (mitigated with clear docs)

---

## 🔧 Current Technical Priorities

### Priority 1: Backend Infrastructure (8 hours)
**Owner:** Development Team
**Status:** ⏳ Planned
**Deadline:** 2026-01-12

**Technical Tasks:**
1. Initialize Node.js project with Express
   - `npm init -y`
   - Install dependencies: `express`, `pg`, `dotenv`, `cors`
   - Create folder structure: `/src/routes`, `/src/services`, `/src/models`, `/src/config`

2. Setup PostgreSQL connection
   - Create `config/database.js` with connection pool
   - Environment variables for DB credentials (`.env`)
   - Connection test endpoint (`/api/health`)

3. Create first migration (price_indices table)
   ```sql
   CREATE TABLE price_indices (
     id SERIAL PRIMARY KEY,
     period VARCHAR(7) NOT NULL,  -- Format: "2024-12"
     product_code VARCHAR(20) NOT NULL,
     product_name VARCHAR(255) NOT NULL,
     index_value DECIMAL(10,2) NOT NULL,
     base_period VARCHAR(7),
     created_at TIMESTAMP DEFAULT NOW(),
     updated_at TIMESTAMP DEFAULT NOW(),
     UNIQUE(period, product_code)
   );
   CREATE INDEX idx_period ON price_indices(period);
   CREATE INDEX idx_product ON price_indices(product_code);
   ```

4. Docker setup
   - `Dockerfile` for backend
   - `docker-compose.yml` with PostgreSQL service
   - Health check script

**Acceptance Criteria:**
- `docker-compose up` starts backend + database
- `curl http://localhost:3000/api/health` returns `{"status": "ok", "database": "connected"}`
- Database migration creates `price_indices` table

---

### Priority 2: ETL Service (12 hours)
**Owner:** Development Team
**Status:** ⏳ Planned (depends on Priority 1)
**Deadline:** 2026-01-15

**Technical Tasks:**
1. API Client (`/services/etl/opendataClient.js`)
   - Fetch JSON from Open Data API
   - Handle errors (timeout, network failure)
   - Retry logic (3 attempts with exponential backoff)

2. Data Transformer (`/services/etl/transformer.js`)
   - Parse JSON structure
   - Validate required fields (period, product_code, index_value)
   - Normalize data format
   - Map API fields to database schema

3. Database Loader (`/services/etl/loader.js`)
   - Upsert logic (`ON CONFLICT (period, product_code) DO UPDATE`)
   - Batch insert for performance
   - Transaction handling (rollback on error)

4. Scheduler (`/services/etl/scheduler.js`)
   - Cron job (daily at 02:00 AM)
   - Manual trigger endpoint (`POST /api/sync`)
   - Logging (success/failure)

**Acceptance Criteria:**
- Manual sync fetches data and inserts into database
- Duplicate data is updated (not duplicated)
- Errors are logged with details
- Cron job runs automatically

**Technical Risks:**
- **Risk:** API structure changes → **Mitigation:** Add schema validation, alert on failure
- **Risk:** Large dataset (1000+ records) → **Mitigation:** Batch processing (100 records/batch)

---

### Priority 3: Frontend Setup (6 hours)
**Owner:** Development Team
**Status:** ⏳ Planned (can run parallel with Priority 1)
**Deadline:** 2026-01-13

**Technical Tasks:**
1. Initialize React project with Vite + TypeScript
   - `npm create vite@latest frontend -- --template react-ts`
   - Install dependencies: `axios`, `recharts` (or Chart.js), `react-router-dom`

2. Setup folder structure
   ```
   /src
     /components  (UI components)
     /pages       (Dashboard, Admin)
     /services    (API client)
     /types       (TypeScript interfaces)
     /utils       (helpers)
   ```

3. API Client (`/services/apiClient.ts`)
   - Axios instance with base URL from env
   - Type-safe interfaces for API responses
   - Error handling

4. Basic Layout Component
   - Header, Footer, Navigation
   - Responsive design (Tailwind CSS or CSS Modules TBD)

**Acceptance Criteria:**
- `npm run dev` starts frontend on http://localhost:5173
- API client successfully fetches from backend `/api/health`
- Layout renders correctly on desktop and mobile

---

## 🏛️ Architecture Decisions

### Decision #1: Database Schema Design (2026-01-11)
**Decision:** Single `price_indices` table with denormalized product names

**Reasoning:**
- **Option 1 (Chosen):** Denormalized (product_code + product_name in same table)
  - ✅ Simpler queries
  - ✅ No joins needed for dashboard
  - ❌ Data duplication (product_name repeated)

- **Option 2 (Rejected):** Normalized (separate `products` table)
  - ✅ No duplication
  - ❌ Every query needs JOIN
  - ❌ API doesn't provide product IDs (would need mapping)

**Trade-off:** Slight data duplication vs. query complexity. Since product names rarely change, denormalized is acceptable.

**Status:** ✅ Approved

---

### Decision #2: State Management (Frontend) (2026-01-11)
**Decision:** Start with React Context API, migrate to Redux if needed

**Reasoning:**
- **Context API:** Sufficient for MVP (simple state: data, filters, loading)
- **Redux:** Overkill for Phase 1, but may be needed if state becomes complex

**Implementation Plan:**
- Create `PriceContext` for storing fetched data
- Create `FilterContext` for date range, product filters

**Review Point:** End of Phase 1 - assess if Redux is needed

**Status:** ✅ Approved

---

## 📋 Implementation Plan

### Task Breakdown

**Sprint 1: Infrastructure (Jan 11-15)**
```
[x] 1. Initialize Git repository (0.5h)
[x] 2. Create AI_TEMPLATE documentation (1h)
[ ] 3. Backend setup (8h)
    [ ] 3.1 Node.js + Express initialization
    [ ] 3.2 PostgreSQL connection
    [ ] 3.3 Database migration
    [ ] 3.4 Docker configuration
[ ] 4. Frontend setup (6h)
    [ ] 4.1 Vite + React + TypeScript
    [ ] 4.2 Folder structure
    [ ] 4.3 API client
    [ ] 4.4 Basic layout
```

**Sprint 2: ETL Process (Jan 16-20)**
```
[ ] 5. ETL implementation (12h)
    [ ] 5.1 API client
    [ ] 5.2 Data transformer
    [ ] 5.3 Database loader
    [ ] 5.4 Scheduler
[ ] 6. Testing (4h)
    [ ] 6.1 Unit tests for transformer
    [ ] 6.2 Integration test for full ETL
```

**Sprint 3: Dashboard (Jan 21-25)**
```
[ ] 7. Dashboard implementation (10h)
    [ ] 7.1 Data table component
    [ ] 7.2 Chart component (line chart)
    [ ] 7.3 Date filter
    [ ] 7.4 API integration
[ ] 8. Polish (4h)
    [ ] 8.1 Loading states
    [ ] 8.2 Error handling
    [ ] 8.3 Responsive design
```

### Critical Path
```
Backend Setup (3) → ETL (5) → Dashboard (7)
Frontend Setup (4) → Dashboard (7)
```

**Bottleneck:** ETL must be completed before dashboard can show real data (can use mock data in the meantime).

---

## 🧹 Code Quality Status

### Current Technical Debt
**None yet** (project just started)

**Planned Prevention:**
- ESLint + Prettier setup (Sprint 1)
- TypeScript strict mode (catch errors early)
- Code review checklist (DEVELOPMENT_TEAM.md)

### Refactoring Needs
**To Be Assessed:** After MVP (end of Phase 1)

**Potential Areas:**
- ETL error handling (may need retry queue if API is unreliable)
- Database indices (optimize after performance testing)

### Performance Monitoring
**Metrics to Track:**
- API response time (target: < 200ms)
- ETL duration (target: < 5 min for full sync)
- Dashboard load time (target: < 2s)

**Tools (TBD):**
- Backend: `morgan` (request logging)
- Frontend: Lighthouse (performance audit)

---

## 👥 Team Coordination

### Current Sprint: Sprint 1 - Infrastructure
**Duration:** Jan 11-15, 2026
**Goal:** Working backend + frontend skeleton

### Task Assignments
| Task | Owner | Status | Deadline |
|------|-------|--------|----------|
| Backend setup | Development Team | ⏳ Planned | Jan 12 |
| Frontend setup | Development Team | ⏳ Planned | Jan 13 |
| Docker config | Development Team | ⏳ Planned | Jan 12 |
| Documentation | Development Team | 🔄 In Progress | Jan 11 |

### Blockers Log
**None yet**

**Common Blockers to Watch:**
- Docker networking issues (backend can't connect to Postgres)
- CORS errors (frontend can't call backend API)
- Environment variable misconfig

**Mitigation:** Clear `.env.example` files + troubleshooting docs

### Code Review Checklist
Before merging any code:
- [ ] TypeScript compiles with no errors
- [ ] ESLint passes (no warnings)
- [ ] Tests pass (if applicable)
- [ ] Code has comments for complex logic
- [ ] Environment variables documented in `.env.example`
- [ ] Database migrations tested (can run up/down)
- [ ] API endpoints documented (Postman collection or OpenAPI)

---

## ⚠️ Technical Risks & Mitigations

### Risk #1: Open Data API Unreliability
**Description:** API may have downtime, rate limits, or structure changes

**Impact:** 🔴 Critical (ETL fails → no fresh data)

**Mitigation:**
- Retry logic with exponential backoff
- Schema validation (detect API changes)
- Alert system (email/Slack notification on failure)
- Fallback: manual data upload (admin panel feature)

**Status:** Plan in place, to implement in Sprint 2

---

### Risk #2: Performance Bottleneck (Large Dataset)
**Description:** If dataset grows to 10,000+ records, queries may slow down

**Impact:** 🟡 Medium (dashboard becomes slow)

**Mitigation:**
- Database indices on `period` and `product_code`
- Pagination (100 records per page)
- Caching layer (Redis - Phase 2)

**Status:** Low priority for MVP, monitor performance

---

## 📚 Technical Documentation Updates Needed

### After Sprint 1:
- [ ] API Endpoint documentation (`/docs/API.md`)
- [ ] Database schema diagram (`/docs/SCHEMA.md`)
- [ ] Development setup guide (update README.md)

### After Phase 1 (MVP):
- [ ] Deployment guide (Docker production config)
- [ ] Troubleshooting guide (common errors)
- [ ] Performance tuning notes

---

## 🎯 Next Actions for Director of Development

### Immediate (Today):
- [x] Complete DIRECTOR_OF_DEVELOPMENT.md
- [ ] Review with Project Director (alignment check)
- [ ] Create task breakdown in DEVELOPMENT_TEAM.md

### This Week:
- [ ] Begin Sprint 1 implementation (backend + frontend setup)
- [ ] Daily standup: update DEVELOPMENT_TEAM.md with progress
- [ ] Resolve blockers (if any)

### This Sprint:
- [ ] Complete infrastructure setup
- [ ] Prepare Sprint 2 plan (ETL detailed design)
- [ ] Code review: first backend endpoint

---

## 📖 Instructions for Using This Template

This document has been customized for **AgroPrice Insight** project.

**Key Sections:**
- **Technical Vision:** WHY we chose these technologies
- **Technical Priorities:** WHAT to build next (with time estimates)
- **Architecture Decisions:** HOW we're solving problems (with trade-offs)
- **Implementation Plan:** WHO does WHAT and WHEN
- **Code Quality:** Tracking tech debt and standards

**Update Frequency:**
- **Daily:** During active development (update priorities, blockers)
- **Weekly:** Review technical debt, code quality
- **As Needed:** Log architecture decisions

**When in Doubt:**
- Ask: "Is this the simplest solution that works?"
- Prioritize: MVP features > perfect architecture
- Document: Every decision should have a "why"
