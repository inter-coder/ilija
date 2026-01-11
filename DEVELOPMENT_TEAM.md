# 💻 Role: Development Team (Razvojni Tim)

## Purpose of This File
This file is the **daily workspace** for developers implementing features for **AgroPrice Insight**. It tracks:
- Current sprint tasks and progress
- Code implementation log
- Testing checklist
- Blockers and questions
- Code review checklist

## Your Responsibilities as Development Team Member
1. **Implement Features** - Write code according to specifications
2. **Write Tests** - Unit tests, integration tests
3. **Log Progress** - Update this file daily with what you did
4. **Report Blockers** - Flag issues immediately
5. **Code Quality** - Follow standards, review code
6. **Communicate** - Ask questions to Director of Development when unclear

## Document Structure
💻 Below you'll find task board, today's focus, implementation log, testing log, and blockers.

## Rules for AI Models
- **UPDATE DAILY** when writing code
- **LOG every file you touch** in Code Implementation Log
- **TRACK testing** in Testing Log (don't skip tests!)
- **FLAG blockers immediately** - don't guess
- **ASK questions** if technical spec is unclear
- **Always update PROJECT_STATUS.md** after completing tasks

## How to Work With Other Roles
- **From Director of Development:** Receive task breakdown and technical specifications
- **To Director of Development:** Report blockers, ask clarifying questions
- **From Project Director:** Understand acceptance criteria for features

## Communication Guidelines
- **Blockers:** Be specific ("Cannot connect to Postgres, error: XYZ")
- **Questions:** Include context ("In ETL transformer, should we validate X or Y?")
- **Progress:** Concrete facts ("Implemented authentication endpoint, 3/5 tests passing")

## Task Workflow
1. **Pick Task** from Task Board (highest priority first)
2. **Implement** following technical spec
3. **Test** (write tests BEFORE marking done)
4. **Log** in Code Implementation Log
5. **Update** Task Board (move to Done)
6. **Commit** with clear commit message

## When to Update This File
- **Start of day:** Update "Today's Focus"
- **After completing task:** Log in Code Implementation Log
- **When blocked:** Add to Blockers section
- **After testing:** Update Testing Log
- **End of day:** Update Progress Tracking

## Reference Files
- **CLAUDE.md** - Technical stack, commands
- **DIRECTOR_OF_DEVELOPMENT.md** - Task breakdown, technical specs
- **PROJECT_DIRECTOR.md** - Business context, acceptance criteria

## How to Test
- **Backend:** `cd backend && npm test`
- **Frontend:** `cd frontend && npm test`
- **E2E:** (To be set up in Phase 2)
- **Manual:** Follow testing checklist in Testing Log section

---

# 💻 DEVELOPMENT TEAM - Implementation Workspace

**Project:** AgroPrice Insight
**Last Updated:** 2026-01-11 18:13
**Current Sprint:** Sprint 1 - Infrastructure
**Team Velocity:** (To be measured after Sprint 1)

---

## 🎯 Current Sprint: Sprint 1 - Infrastructure

### Sprint Goal
**Setup working development environment:** Backend (Node.js + PostgreSQL), Frontend (React + TypeScript), Docker configuration.

### Success Criteria
- [ ] `docker-compose up` starts all services (backend, frontend, database)
- [ ] Backend health endpoint returns success (`/api/health`)
- [ ] Frontend loads and can call backend API
- [ ] Database migration creates `price_indices` table
- [ ] All setup documented in README.md

**Duration:** 2026-01-11 → 2026-01-15 (5 days)

---

## 📋 Task Board

### 🔄 In Progress

#### Task: Initialize Git Repository
- **Assigned to:** Development Team
- **Estimated:** 0.5h
- **Status:** ✅ Done
- **Description:** Create Git repo, add `.gitignore`, initial commit
- **Files:**
  - `.gitignore` (Node.js, .env, IDE files)
  - Initial commit with README.md

---

#### Task: Create AI_TEMPLATE Documentation
- **Assigned to:** Development Team
- **Estimated:** 1h
- **Status:** 🔄 In Progress (90% done)
- **Description:** Create CLAUDE.md, PROJECT_DIRECTOR.md, DIRECTOR_OF_DEVELOPMENT.md, DEVELOPMENT_TEAM.md, PROJECT_STATUS.md
- **Files:**
  - [x] CLAUDE.md
  - [x] PROJECT_STATUS.md
  - [x] PROJECT_DIRECTOR.md
  - [x] DIRECTOR_OF_DEVELOPMENT.md
  - [ ] DEVELOPMENT_TEAM.md (this file - completing now)

**Next:** Finalize DEVELOPMENT_TEAM.md, commit all framework files

---

### ⏳ To Do

#### Task: Backend Setup (Node.js + Express)
- **Assigned to:** Development Team
- **Estimated:** 8h
- **Priority:** 🔴 Critical (blocks ETL)
- **Description:** Initialize backend with Express, PostgreSQL connection, Docker
- **Technical Spec:** See DIRECTOR_OF_DEVELOPMENT.md > Priority 1
- **Subtasks:**
  1. [ ] Create `/backend` directory
  2. [ ] `npm init -y` + install dependencies (express, pg, dotenv, cors)
  3. [ ] Create folder structure (`/src/routes`, `/src/services`, `/src/models`, `/src/config`)
  4. [ ] Implement database connection (`config/database.js`)
  5. [ ] Create health endpoint (`/api/health`)
  6. [ ] Write database migration (create `price_indices` table)
  7. [ ] Configure Docker (`Dockerfile`, `docker-compose.yml`)
  8. [ ] Test: `docker-compose up` + `curl http://localhost:3000/api/health`

**Acceptance Criteria:**
- [ ] Backend starts without errors
- [ ] Database connection works
- [ ] Health endpoint returns `{"status": "ok", "database": "connected"}`

**Dependencies:** None (can start immediately)

---

#### Task: Frontend Setup (Vite + React + TypeScript)
- **Assigned to:** Development Team
- **Estimated:** 6h
- **Priority:** 🟡 High (can run parallel with backend)
- **Description:** Initialize frontend with Vite, React, TypeScript
- **Technical Spec:** See DIRECTOR_OF_DEVELOPMENT.md > Priority 3
- **Subtasks:**
  1. [ ] `npm create vite@latest frontend -- --template react-ts`
  2. [ ] Install dependencies (axios, recharts, react-router-dom)
  3. [ ] Create folder structure (`/components`, `/pages`, `/services`, `/types`)
  4. [ ] Implement API client (`/services/apiClient.ts`)
  5. [ ] Create basic layout component (Header, Footer, Nav)
  6. [ ] Configure environment variables (`.env` with `VITE_API_URL`)
  7. [ ] Test: API client can call backend `/api/health`

**Acceptance Criteria:**
- [ ] Frontend starts on http://localhost:5173
- [ ] API client successfully connects to backend
- [ ] Layout renders correctly

**Dependencies:** Backend health endpoint (for testing API client)

---

#### Task: ETL Implementation
- **Assigned to:** Development Team
- **Estimated:** 12h
- **Priority:** 🔴 Critical (blocks dashboard)
- **Description:** Implement ETL process to fetch data from Open Data API
- **Technical Spec:** See DIRECTOR_OF_DEVELOPMENT.md > Priority 2
- **Status:** ⏳ Waiting for backend setup

**Dependencies:** Backend setup completed

---

#### Task: Dashboard Implementation
- **Assigned to:** Development Team
- **Estimated:** 10h
- **Priority:** 🟡 High
- **Description:** Create dashboard with data table and chart
- **Status:** ⏳ Waiting for ETL

**Dependencies:** ETL completed (or use mock data)

---

### ✅ Done

**None yet** (project just started)

---

## 🔨 Today's Focus

### 2026-01-11

**Goals:**
- [x] Complete AI_TEMPLATE framework documentation
- [ ] Start backend setup (if time permits)

**Completed:**
- Created CLAUDE.md with project overview
- Created PROJECT_STATUS.md with status tracking
- Created PROJECT_DIRECTOR.md with strategic vision
- Created DIRECTOR_OF_DEVELOPMENT.md with technical plan
- Creating DEVELOPMENT_TEAM.md (this file)

**Blockers:** None

**Tomorrow:**
- Start backend setup (create directory, npm init, install dependencies)

---

## 📝 Code Implementation Log

### 2026-01-11 18:13 - Framework Documentation
**Task:** Create AI_TEMPLATE Documentation
**Status:** 🔄 In Progress

**Files Created:**
- `/home/dusan/projects/ilija/CLAUDE.md` (347 lines)
- `/home/dusan/projects/ilija/PROJECT_STATUS.md` (82 lines)
- `/home/dusan/projects/ilija/PROJECT_DIRECTOR.md` (351 lines)
- `/home/dusan/projects/ilija/DIRECTOR_OF_DEVELOPMENT.md` (457 lines)
- `/home/dusan/projects/ilija/DEVELOPMENT_TEAM.md` (this file)

**Changes:**
- Customized all templates for AgroPrice Insight project
- Defined technical stack (Node.js, React, PostgreSQL, Docker)
- Created task breakdown for Sprint 1
- Documented architecture decisions

**Testing:** N/A (documentation only)

**Next:** Commit framework files, start backend setup

---

## 🧪 Testing Log

### Manual Testing Checklist
**Backend (after setup):**
- [ ] `docker-compose up` starts without errors
- [ ] `curl http://localhost:3000/api/health` returns 200 OK
- [ ] Database connection works (check logs for "Database connected")
- [ ] Health endpoint returns JSON: `{"status": "ok", "database": "connected"}`

**Frontend (after setup):**
- [ ] `npm run dev` starts without errors
- [ ] Application loads on http://localhost:5173
- [ ] No console errors in browser
- [ ] API client can call backend (check Network tab)

**ETL (after implementation):**
- [ ] Manual sync endpoint works: `curl -X POST http://localhost:3000/api/sync`
- [ ] Data is fetched from Open Data API
- [ ] Data is inserted into database (check `SELECT * FROM price_indices LIMIT 10`)
- [ ] Duplicate sync doesn't create duplicates (upsert works)
- [ ] Cron job runs automatically (wait 24h or trigger manually)

### Automated Tests
**None yet** (to be written during implementation)

**Planned Tests:**
- **Backend:**
  - Unit: ETL transformer (validate data parsing)
  - Integration: Full ETL process (API → Database)
  - API: Health endpoint returns 200

- **Frontend:**
  - Unit: Components render correctly
  - Integration: API client handles errors

**Test Framework:** Jest (TBD - to be setup in Sprint 1)

---

## 🚧 Blockers & Questions

### Active Blockers
**None yet**

**Potential Blockers:**
- Docker networking (backend can't connect to Postgres)
  - **Solution:** Check `docker-compose.yml` network configuration
- CORS errors (frontend can't call backend)
  - **Solution:** Add CORS middleware to Express (`app.use(cors())`)

### Questions for Director of Development
**None yet**

**Example Questions (for future):**
- "In ETL transformer, if API returns null for `index_value`, should we skip record or set to 0?"
- "Should dashboard show loading spinner during API call?"

---

## 📚 Learning & Notes

### Pattern: Layered Backend Architecture
**Location:** `/backend/src/`

**Structure:**
```
Routes (API endpoints)
  ↓ calls
Services (Business logic)
  ↓ calls
Models (Database access)
```

**Example:**
- `routes/prices.js` → defines `GET /api/prices`
- `services/priceService.js` → fetches data from database, applies filters
- `models/PriceIndex.js` → SQL queries

**Why:** Separation of concerns, easier testing

---

### Code Style: TypeScript Interfaces
**Location:** `/frontend/src/types/`

**Pattern:**
```typescript
export interface PriceIndex {
  id: number;
  period: string;  // "2024-12"
  productCode: string;
  productName: string;
  indexValue: number;
  basePeriod: string;
  createdAt: Date;
  updatedAt: Date;
}
```

**Why:** Type safety, autocomplete in IDE

---

### Gotcha: Environment Variables in Vite
**Issue:** Vite requires `VITE_` prefix for env variables

**Solution:**
```env
# ❌ Wrong
API_URL=http://localhost:3000

# ✅ Correct
VITE_API_URL=http://localhost:3000
```

**Access in code:**
```typescript
const apiUrl = import.meta.env.VITE_API_URL;
```

---

## 📊 Progress Tracking

### Daily Progress

**2026-01-11:**
- ✅ AI_TEMPLATE framework documentation created
- ✅ Task breakdown for Sprint 1 defined
- ⏳ Backend setup (planned for tomorrow)

**Velocity:** N/A (first day)

**Burndown:**
- Total Sprint 1 hours: 15.5h (backend 8h + frontend 6h + docs 1.5h)
- Completed: 1.5h (docs)
- Remaining: 14h

---

## 🔍 Code Review Checklist

**Before committing code, verify:**

### Functionality
- [ ] Code does what it's supposed to do (meets acceptance criteria)
- [ ] Edge cases handled (null values, empty arrays, errors)
- [ ] No hardcoded values (use environment variables)

### Code Quality
- [ ] Variable names are clear and descriptive
- [ ] Functions are small and focused (single responsibility)
- [ ] No commented-out code (delete it)
- [ ] No console.log left in code (use proper logging)

### Testing
- [ ] Unit tests written and passing
- [ ] Manual testing completed (checked Testing Log)
- [ ] No new warnings in console

### Documentation
- [ ] Complex logic has comments explaining "why"
- [ ] New environment variables added to `.env.example`
- [ ] API changes documented (if applicable)
- [ ] README.md updated (if setup changed)

---

## 💡 Ideas & Suggestions

### Idea #1: Mock Data for Dashboard Development
**Proposed by:** Development Team
**Date:** 2026-01-11
**Description:** Create mock price data so frontend team can develop dashboard before ETL is ready

**Benefits:**
- Parallel development (frontend doesn't wait for ETL)
- Easier testing (predictable data)

**Implementation:**
- Create `/backend/src/mock/priceData.json` with sample records
- Add endpoint `GET /api/prices/mock` that returns mock data
- Frontend can use mock endpoint during development

**Status:** 💡 Idea (awaiting Director of Development approval)

---

### Idea #2: Seed Script for Database
**Proposed by:** Development Team
**Date:** 2026-01-11
**Description:** Create seed script to populate database with sample data

**Benefits:**
- Easier local development
- Consistent data for testing
- Demo data for presentations

**Implementation:**
- Create `/backend/scripts/seed.js`
- Command: `npm run seed`
- Inserts 50-100 sample records

**Status:** 💡 Idea (low priority for MVP)

---

## 🐛 Bugs Found During Development

**None yet**

**Bug Template:**
```
### Bug #X: [Brief Description]
**Found:** [Date]
**Severity:** 🔴 Critical / 🟡 Medium / 🟢 Low
**Description:** [What went wrong]
**Steps to Reproduce:**
1. [Step 1]
2. [Step 2]
**Expected:** [What should happen]
**Actual:** [What actually happens]
**Fix:** [How it was fixed]
**Status:** 🔄 Open / ✅ Fixed
```

---

## 🎯 Next Steps

### Immediate (Next Task):
1. Finalize DEVELOPMENT_TEAM.md
2. Commit all AI_TEMPLATE framework files
   ```bash
   git add CLAUDE.md PROJECT_STATUS.md PROJECT_DIRECTOR.md DIRECTOR_OF_DEVELOPMENT.md DEVELOPMENT_TEAM.md
   git commit -m "docs: initialize AI_TEMPLATE framework"
   ```
3. Start backend setup (create `/backend` directory)

### Tomorrow:
- Initialize Node.js project in `/backend`
- Install dependencies (express, pg, dotenv, cors)
- Create folder structure
- Implement database connection

### This Week:
- Complete backend setup (8h)
- Complete frontend setup (6h)
- Integration test (backend + frontend + database)

---

## 📖 Instructions for Using This Template

This document has been customized for **AgroPrice Insight** project.

**Key Sections:**
- **Task Board:** Visual tracking of what's To Do, In Progress, Done
- **Today's Focus:** Daily goals (update every morning)
- **Code Implementation Log:** Record every file you touch (accountability)
- **Testing Log:** Don't skip testing!
- **Blockers:** Flag issues immediately

**Update Frequency:**
- **Daily:** Today's Focus, Code Implementation Log, Progress Tracking
- **As Needed:** Task Board (when task status changes), Blockers

**Daily Workflow:**
1. **Morning:** Read Task Board, update "Today's Focus"
2. **During Work:** Implement tasks, run tests
3. **After Task:** Update Code Implementation Log, Testing Log
4. **End of Day:** Update Progress Tracking, move tasks on Task Board

**When in Doubt:**
- Ask Director of Development (add to "Questions" section)
- Check DIRECTOR_OF_DEVELOPMENT.md for technical spec
- Check CLAUDE.md for commands and architecture

---

**Last Updated:** 2026-01-11 18:13 by Development Team
