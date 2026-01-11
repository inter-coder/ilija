# 🎯 Role: Project Director (Direktor Projekta)

## Purpose of This File
This file contains strategic decisions, priorities, and high-level direction for the **AgroPrice Insight** project. As the Project Director, your focus is on:
- Business value and user outcomes
- Stakeholder communication
- Roadmap and priorities
- Quality gates and success criteria

## Your Responsibilities as Project Director
1. **Define Vision** - What are we building and why?
2. **Set Priorities** - What matters most right now?
3. **Make Trade-offs** - Balance scope, time, quality
4. **Communicate** - Keep stakeholders informed
5. **Ensure Quality** - Define acceptance criteria

## Document Structure
📊 Below you'll find sections for vision, priorities, roadmap, decisions, and stakeholder communication.

## Rules for AI Models
- **READ THIS FIRST** when asked about project priorities or direction
- **UPDATE Active Priorities** when user changes goals
- **LOG DECISIONS** in Decisions & Trade-offs section
- **ADD TO Stakeholder Feedback** when user provides business input
- **Always update PROJECT_STATUS.md** after significant changes

## How to Work With Other Roles
- **To Director of Development:** Communicate priorities, get technical feasibility feedback
- **To Development Team:** Provide clear acceptance criteria for features

## When to Update This File
- User changes priorities or goals
- Major strategic decision is made
- Stakeholder provides feedback
- Phase/milestone is completed
- Quality gate is defined or met

---

# 📊 PROJECT DIRECTOR - Strategic Command Center

**Project:** AgroPrice Insight
**Last Updated:** 2026-01-11 18:13
**Current Phase:** Phase 1 - Initialization
**Project Health:** 🟡 Needs Attention (awaiting infrastructure setup)

---

## 🎯 Current Vision & Goals

### Project Vision
**AgroPrice Insight** omogućava poljoprivrednicima, ekonomistima i analitičarima da prate i analiziraju mesečne indekse cena proizvođača poljoprivrednih proizvoda u Srbiji. 

**Ciljna grupa:**
- Poljoprivrednici (praćenje tržišnih trendova)
- Ekonomski analitičari (izrada izveštaja)
- Državne institucije (monitoring sektora)
- Istraživači (istorijski podaci)

**Ključna vrednost:**
- Automatizovano prikupljanje podataka (umesto manuelnog preuzimanja)
- Vizuelizacija trendova (grafikoni, poređenja)
- Istorijski pregled (arhiva podataka)
- Jednostavan pristup (dashboard interfejs)

### Success Criteria (Current Phase/Quarter)

**Phase 1 - Q1 2026 (Initialization)**
- ✅ Framework dokumentacija kreirana
- ⏳ Projektna struktura inicijalizovana
- ⏳ Backend postavljen (Express + PostgreSQL)
- ⏳ Frontend postavljen (React + TypeScript)
- ⏳ ETL proces implementiran (automatski import podataka)
- ⏳ Osnovna vizuelizacija (jedna tabela/grafikon)

**Success Metrics:**
- ETL proces uspešno preuzima podatke sa API-ja (100% success rate)
- Podaci se prikazuju u dashboard-u (end-to-end funkcionisanje)
- Projekat se podiže sa `docker-compose up` (jedna komanda)

### Key Metrics
- **Data Freshness:** API sync < 24h old
- **Uptime:** 99% availability
- **Performance:** Dashboard load < 2s
- **Data Integrity:** 100% match with source API

---

## 🔥 Active Priorities

### Priority 1: Project Infrastructure Setup
**Deadline:** 2026-01-15
**Owner:** Director of Development
**Status:** 🔄 In Progress

**Goal:** Postaviti radnu verziju projekta sa backend-om, frontend-om i bazom podataka.

**Acceptance Criteria:**
- [ ] Backend direktorijum kreiran sa Express server-om
- [ ] Frontend direktorijum kreiran sa React aplikacijom
- [ ] PostgreSQL baza podignuta (Docker ili lokalno)
- [ ] Projekat se podiže sa `npm run dev` (oba servisa)
- [ ] Health check endpoint funkcioniše (`/api/health`)

**Business Value:** Omogućava početak razvoja features-a.

---

### Priority 2: ETL Process - Automatic Data Import
**Deadline:** 2026-01-20
**Owner:** Development Team
**Status:** ⏳ Planned (depends on Priority 1)

**Goal:** Implementirati automatsko preuzimanje podataka sa Open Data API-ja Srbije.

**Acceptance Criteria:**
- [ ] API call uspešno preuzima JSON podatke
- [ ] Podaci se parsiraju i validiraju
- [ ] Podaci se upisuju u PostgreSQL
- [ ] Cron job pokreće sync svakih 24h
- [ ] Error handling (retry logic, logging)

**Business Value:** Automatizacija - korisnici dobijaju najnovije podatke bez intervencije.

---

### Priority 3: Basic Dashboard Visualization
**Deadline:** 2026-01-25
**Owner:** Development Team
**Status:** ⏳ Planned (depends on Priority 2)

**Goal:** Kreirati osnovni dashboard sa tabelom i grafikonom cena.

**Acceptance Criteria:**
- [ ] Tabela prikazuje najnovije podatke (product, price, date)
- [ ] Grafikon prikazuje trend (line chart)
- [ ] Filtriranje po datumu (date picker)
- [ ] Responsivan dizajn (mobile-friendly)

**Business Value:** Korisnici mogu da vide podatke - MVP (Minimum Viable Product).

---

## 📥 Stakeholder Feedback Log

### Source: Direktorat (Initial Requirements) (2026-01-11)
**Feedback:**
- Projekat treba da koristi AI_TEMPLATE framework za dokumentaciju
- Potreban automatski import podataka sa Open Data API
- Dashboard vizuelizacija je prioritet
- PDF/Excel export je "nice to have" (nije MVP)

**Action Taken:**
- ✅ AI_TEMPLATE framework inicijalizovan
- 🔄 Prioriteti definisani (Infrastructure → ETL → Dashboard)
- 📋 PDF/Excel stavljen u backlog

---

## 🗺️ Feature Roadmap

### ✅ Completed: Project Planning (2026-01-11)
**Delivered:**
- AI_TEMPLATE framework dokumentacija
- Tehnička arhitektura definisana
- Prioriteti postavljeni

---

### 🔄 Current: Phase 1 - MVP Development (2026-01-11 → 2026-01-31)
**In Progress:**
- Infrastructure setup
- ETL process implementation
- Basic dashboard

**Deliverables:**
- Radni backend API
- Automatski data sync
- Dashboard sa jednom vizuelizacijom

---

### ⏳ Next: Phase 2 - Advanced Features (2026-02-01 → 2026-02-28)
**Planned Features:**
- Advanced filtering (product categories, date ranges)
- Multiple chart types (bar, pie, line)
- Comparison tool (year-over-year, product-to-product)
- Admin panel (manual sync trigger, logs)

---

### 📋 Backlog (Post-MVP)
**Nice-to-Have Features:**
- PDF/Excel export
- Email notifications (price alerts)
- Multi-language support (EN/SR)
- Public API with authentication
- Mobile app

---

## 🤔 Decisions & Trade-offs

### Decision #1: PostgreSQL vs MongoDB (2026-01-11)
**Decision:** PostgreSQL
**Rationale:**
- Strukturirani podaci (price indices imaju fiksnu strukturu)
- Relational queries (filtriranje, aggregation)
- Tim ima iskustvo sa SQL bazama

**Trade-off:** Manje fleksibilnosti za buduće nested/unstructured data, ali je rizik nizak.

**Status:** ✅ Approved

---

### Decision #2: Docker Deployment (2026-01-11)
**Decision:** Koristiti Docker za lokalni development i production
**Rationale:**
- Konzistentno okruženje (PostgreSQL verzija, Node verzija)
- Jednostavno pokretanje (`docker-compose up`)
- Production-ready deployment

**Trade-off:** Dodatna složenost za developere koji nisu upoznati sa Docker-om, ali je uloženo vreme isplativo.

**Status:** ✅ Approved

---

## ✅ Quality Gates

### Phase 1 Quality Gate (MVP Release)
**Must-Have:**
- [ ] All automated tests passing (unit + integration)
- [ ] ETL process successfully imports data (no errors in 3 consecutive syncs)
- [ ] Dashboard loads data within 2 seconds
- [ ] No critical security vulnerabilities (dependency audit clean)
- [ ] Docker deployment works (`docker-compose up` → application accessible)

**Nice-to-Have:**
- [ ] Code coverage > 70%
- [ ] Performance test (load testing with 1000 concurrent users)

**Release Criteria:**
- All "Must-Have" items completed
- Project Director approval
- Director of Development sign-off

---

## 📡 Communication Log

### To Development Team (2026-01-11)
**Subject:** Prioriteti za Phase 1
**Message:**
"Fokus je na MVP - Infrastructure, ETL, Basic Dashboard. Sve ostalo (export, advanced analytics) ide u Phase 2. Cilj je imati radnu verziju do kraja januara."

**Expected Response:** Task breakdown u DEVELOPMENT_TEAM.md

---

## 📝 Notes & Observations

### Observation #1: Data Source Reliability (2026-01-11)
**Note:** Open Data API Serbia je jedini zvanični izvor. Potrebno testirati stabilnost API-ja (rate limits, downtime). 

**Recommendation:** Implementirati robust error handling + retry logic u ETL procesu.

**Follow-up:** Director of Development da planira monitoring strategy.

---

## 🎬 Next Actions for Project Director

### Immediate (This Week):
- [ ] Pregledati PROJECT_DIRECTOR.md sa Development Team-om
- [ ] Odobriti DIRECTOR_OF_DEVELOPMENT.md technical plan
- [ ] Definisati mock data set za testiranje dashboard-a (pre nego što ETL bude gotov)

### Short-term (This Month):
- [ ] Weekly check-in sa Development Team (progress review)
- [ ] Pripremiti demo za krajnje korisnike (end of Phase 1)

### Long-term (This Quarter):
- [ ] Sakupiti feedback od korisnika nakon MVP release
- [ ] Planirati Phase 2 features baziran na user feedback

---

## 📖 Instructions for Using This Template

This document has been customized for **AgroPrice Insight** project. 

**Key Sections:**
- **Vision & Goals:** Strategic direction - WHERE we're going
- **Active Priorities:** What's happening NOW
- **Roadmap:** Timeline - WHEN things happen
- **Decisions:** Important choices and their reasoning
- **Quality Gates:** Standards before release

**Update Frequency:**
- **Weekly:** Review priorities and update status
- **As Needed:** Log decisions, stakeholder feedback
- **After Milestones:** Update roadmap

**When in Doubt:**
- Ask: "Does this create business value?"
- Prioritize user outcomes over technical perfection
- Communicate changes to DIRECTOR_OF_DEVELOPMENT.md
